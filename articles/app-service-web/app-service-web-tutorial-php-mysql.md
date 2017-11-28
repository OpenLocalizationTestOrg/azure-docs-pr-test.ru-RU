---
title: "aaaBuild веб-приложения PHP и MySQL в Azure | Документы Microsoft"
description: "Узнайте, как tooget приложения PHP, работа в Azure, с tooa подключения MySQL базы данных в Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="9e01f-103">Создание веб-приложения PHP в Azure с подключением к базе данных MySQL</span><span class="sxs-lookup"><span data-stu-id="9e01f-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="9e01f-104">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="9e01f-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="9e01f-105">В этом учебнике показано, как toocreate PHP веб-приложения в Azure и соедините его tooa базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="9e01f-105">This tutorial shows how toocreate a PHP web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="9e01f-106">По завершении вы получите приложение [Laravel](https://laravel.com/), работающее в веб-приложениях службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="9e01f-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![Приложение PHP, работающее в службе приложений Azure](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="9e01f-108">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="9e01f-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9e01f-109">Создание базы данных MySQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="9e01f-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="9e01f-110">Подключение tooMySQL приложения PHP</span><span class="sxs-lookup"><span data-stu-id="9e01f-110">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="9e01f-111">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="9e01f-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="9e01f-112">Обновить модель данных hello и повторно развернуть приложение hello</span><span class="sxs-lookup"><span data-stu-id="9e01f-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="9e01f-113">Потоковая передача журналов диагностики из Azure.</span><span class="sxs-lookup"><span data-stu-id="9e01f-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="9e01f-114">Управление приложение hello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9e01f-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e01f-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9e01f-115">Prerequisites</span></span>

<span data-ttu-id="9e01f-116">toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="9e01f-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="9e01f-117">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="9e01f-117">[Install Git](https://git-scm.com/)</span></span>
* <span data-ttu-id="9e01f-118">[PHP 5.6.4 или более поздней версии](http://php.net/downloads.php);</span><span class="sxs-lookup"><span data-stu-id="9e01f-118">[Install PHP 5.6.4 or above](http://php.net/downloads.php)</span></span>
* <span data-ttu-id="9e01f-119">[Composer](https://getcomposer.org/doc/00-intro.md);</span><span class="sxs-lookup"><span data-stu-id="9e01f-119">[Install Composer](https://getcomposer.org/doc/00-intro.md)</span></span>
* <span data-ttu-id="9e01f-120">Включить следующие расширения PHP Laravel потребностей hello: OpenSSL, PDO MySQL, Mbstring, разметчика, XML</span><span class="sxs-lookup"><span data-stu-id="9e01f-120">Enable hello following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* <span data-ttu-id="9e01f-121">[MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) (этот компонент потребуется запустить).</span><span class="sxs-lookup"><span data-stu-id="9e01f-121">[Install and start MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html)</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="9e01f-122">Подготовка локальной базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="9e01f-122">Prepare local MySQL</span></span>

<span data-ttu-id="9e01f-123">На этом шаге вы создадите базу данных на локальном сервере MySQL для использования в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="9e01f-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-toolocal-mysql-server"></a><span data-ttu-id="9e01f-124">Подключение сервера MySQL toolocal</span><span class="sxs-lookup"><span data-stu-id="9e01f-124">Connect toolocal MySQL server</span></span>

<span data-ttu-id="9e01f-125">В окне терминала подключение tooyour локального сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="9e01f-125">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="9e01f-126">Можно использовать это окно терминала toorun hello команды в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9e01f-126">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="9e01f-127">Если появится запрос пароля, введите пароль hello для hello `root` учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9e01f-127">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="9e01f-128">Если вы не помните пароль корневой учетной записи, см. раздел [MySQL: как tooReset hello пароль учетной записи Root](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="9e01f-128">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="9e01f-129">Если команда выполнена успешно, значит, сервер MySQL работает.</span><span class="sxs-lookup"><span data-stu-id="9e01f-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="9e01f-130">Если это не так, убедитесь в том, локальному серверу MySQL запущен из следующих hello [действий после установки MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="9e01f-130">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="9e01f-131">Локальное создание базы данных</span><span class="sxs-lookup"><span data-stu-id="9e01f-131">Create a database locally</span></span>

<span data-ttu-id="9e01f-132">В hello `mysql` запрос, создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="9e01f-132">At hello `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="9e01f-133">Завершите подключение к серверу, введя команду `quit`.</span><span class="sxs-lookup"><span data-stu-id="9e01f-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="9e01f-134">Локальное создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="9e01f-134">Create a PHP app locally</span></span>
<span data-ttu-id="9e01f-135">На этом шаге вы создадите пример приложения Laravel, настроите его подключение к базе данных и запустите это приложение в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="9e01f-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="9e01f-136">Образец hello клонирования</span><span class="sxs-lookup"><span data-stu-id="9e01f-136">Clone hello sample</span></span>

<span data-ttu-id="9e01f-137">В окне терминала hello `cd` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="9e01f-137">In hello terminal window, `cd` tooa working directory.</span></span>

<span data-ttu-id="9e01f-138">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-138">Run hello following command tooclone hello sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="9e01f-139">`cd`точная копия каталог tooyour.</span><span class="sxs-lookup"><span data-stu-id="9e01f-139">`cd` tooyour cloned directory.</span></span>
<span data-ttu-id="9e01f-140">Установите пакеты необходимых hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-140">Install hello required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="9e01f-141">Настройка подключения к MySQL</span><span class="sxs-lookup"><span data-stu-id="9e01f-141">Configure MySQL connection</span></span>

<span data-ttu-id="9e01f-142">В корневом хранилище hello, создайте файл с именем *.env*.</span><span class="sxs-lookup"><span data-stu-id="9e01f-142">In hello repository root, create a file named *.env*.</span></span> <span data-ttu-id="9e01f-143">Следующие переменные в hello hello копирования *.env* файла.</span><span class="sxs-lookup"><span data-stu-id="9e01f-143">Copy hello following variables into hello *.env* file.</span></span> <span data-ttu-id="9e01f-144">Замените hello  _&lt;root_password >_ заполнитель hello MySQL корневой пароль.</span><span class="sxs-lookup"><span data-stu-id="9e01f-144">Replace hello _&lt;root_password>_ placeholder with hello MySQL root user's password.</span></span>

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

<span data-ttu-id="9e01f-145">Дополнительные сведения об использовании hello Laravel _.env_ файла см. в разделе [конфигурации среды Laravel](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="9e01f-145">For information on how Laravel uses hello _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-hello-sample-locally"></a><span data-ttu-id="9e01f-146">Запуск образца hello локально</span><span class="sxs-lookup"><span data-stu-id="9e01f-146">Run hello sample locally</span></span>

<span data-ttu-id="9e01f-147">Запустите [миграции базы данных Laravel](https://laravel.com/docs/5.4/migrations) toocreate hello таблицы потребностей приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) toocreate hello tables hello application needs.</span></span> <span data-ttu-id="9e01f-148">таблицы, для которых создаются при миграции hello в поиск в hello toosee _базы данных или миграции_ каталог в репозитории hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-148">toosee which tables are created in hello migrations, look in hello _database/migrations_ directory in hello Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="9e01f-149">Создайте ключ приложения Laravel.</span><span class="sxs-lookup"><span data-stu-id="9e01f-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="9e01f-150">Запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-150">Run hello application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="9e01f-151">Перейдите в слишком`http://localhost:8000` в браузере.</span><span class="sxs-lookup"><span data-stu-id="9e01f-151">Navigate too`http://localhost:8000` in a browser.</span></span> <span data-ttu-id="9e01f-152">На странице приветствия добавьте несколько задач.</span><span class="sxs-lookup"><span data-stu-id="9e01f-152">Add a few tasks in hello page.</span></span>

![PHP успешно подключается tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="9e01f-154">Введите toostop PHP, `Ctrl + C` в hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="9e01f-154">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="9e01f-155">Создание базы данных MySQL в Azure</span><span class="sxs-lookup"><span data-stu-id="9e01f-155">Create MySQL in Azure</span></span>

<span data-ttu-id="9e01f-156">На этом шаге вы создадите базу данных MySQL в [базе данных Azure для MySQL (предварительная версия)](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="9e01f-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="9e01f-157">Впоследствии можно настроить базу данных toothis tooconnect приложения hello PHP.</span><span class="sxs-lookup"><span data-stu-id="9e01f-157">Later, you configure hello PHP application tooconnect toothis database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="9e01f-158">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="9e01f-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="9e01f-159">Создание сервера MySQL</span><span class="sxs-lookup"><span data-stu-id="9e01f-159">Create a MySQL server</span></span>

<span data-ttu-id="9e01f-160">Создать сервер базы данных Azure для MySQL (Предварительная версия) с hello [создать сервер mysql az](/cli/azure/mysql/server#create) команды.</span><span class="sxs-lookup"><span data-stu-id="9e01f-160">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="9e01f-161">Hello следующую команду, заменить имя сервера MySQL, где вы видите hello  _&lt;mysql_server_name >_ заполнитель (допустимые символы — `a-z`, `0-9`, и `-`).</span><span class="sxs-lookup"><span data-stu-id="9e01f-161">In hello following command, substitute your MySQL server name where you see hello _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="9e01f-162">Это имя является частью имени узла сервера MySQL hello (`<mysql_server_name>.database.windows.net`), ему toobe глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="9e01f-162">This name is part of hello MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs toobe globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="9e01f-163">При создании сервера MySQL hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="9e01f-163">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="9e01f-164">Настройка брандмауэра сервера</span><span class="sxs-lookup"><span data-stu-id="9e01f-164">Configure server firewall</span></span>

<span data-ttu-id="9e01f-165">Создать правило брандмауэра для MySQL server tooallow клиентских соединений с помощью hello [az mysql правила брандмауэра для сервера — создание](/cli/azure/mysql/server/firewall-rule#create) команды.</span><span class="sxs-lookup"><span data-stu-id="9e01f-165">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="9e01f-166">В настоящее время подключений только tooAzure служб не ограничить базы данных Azure для MySQL (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="9e01f-166">Azure Database for MySQL (Preview) doesn't currently limit connections only tooAzure services.</span></span> <span data-ttu-id="9e01f-167">Как динамически назначаются IP-адресов в Azure, это лучше tooenable все IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="9e01f-167">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses.</span></span> <span data-ttu-id="9e01f-168">Hello служба находится в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="9e01f-168">hello service is in preview.</span></span> <span data-ttu-id="9e01f-169">В ближайшем будущем будут добавлены более надежные методы защиты базы данных.</span><span class="sxs-lookup"><span data-stu-id="9e01f-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a><span data-ttu-id="9e01f-170">Подключение сервера MySQL tooproduction локально</span><span class="sxs-lookup"><span data-stu-id="9e01f-170">Connect tooproduction MySQL server locally</span></span>

<span data-ttu-id="9e01f-171">В окне терминала hello подключение toohello MySQL server в Azure.</span><span class="sxs-lookup"><span data-stu-id="9e01f-171">In hello terminal window, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="9e01f-172">Используйте значение hello, указанную ранее  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="9e01f-172">Use hello value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="9e01f-173">При появлении запроса пароля используйте _$tr0ngPa$ w0rd!_, который был указан при создании hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="9e01f-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created hello database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="9e01f-174">Создание рабочей базы данных</span><span class="sxs-lookup"><span data-stu-id="9e01f-174">Create a production database</span></span>

<span data-ttu-id="9e01f-175">В hello `mysql` запрос, создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="9e01f-175">At hello `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="9e01f-176">Создание пользователя с разрешениями</span><span class="sxs-lookup"><span data-stu-id="9e01f-176">Create a user with permissions</span></span>

<span data-ttu-id="9e01f-177">Создание пользователя базы данных с именем _phpappuser_ и присвойте ему все привилегии в hello `sampledb` базы данных.</span><span class="sxs-lookup"><span data-stu-id="9e01f-177">Create a database user called _phpappuser_ and give it all privileges in hello `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

<span data-ttu-id="9e01f-178">Закрыть соединение с сервером hello, введя `quit`.</span><span class="sxs-lookup"><span data-stu-id="9e01f-178">Exit hello server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a><span data-ttu-id="9e01f-179">Подключение приложения tooAzure MySQL</span><span class="sxs-lookup"><span data-stu-id="9e01f-179">Connect app tooAzure MySQL</span></span>

<span data-ttu-id="9e01f-180">На этом шаге подключиться hello PHP приложения toohello базы данных MySQL, созданных в базе данных Azure для MySQL (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="9e01f-180">In this step, you connect hello PHP application toohello MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="9e01f-181">Подключение к базе данных hello</span><span class="sxs-lookup"><span data-stu-id="9e01f-181">Configure hello database connection</span></span>

<span data-ttu-id="9e01f-182">Создайте в корень репозитория hello, _. env.production_ hello файл и скопируйте следующие переменные в него.</span><span class="sxs-lookup"><span data-stu-id="9e01f-182">In hello repository root, create an _.env.production_ file and copy hello following variables into it.</span></span> <span data-ttu-id="9e01f-183">Замените заполнитель hello  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="9e01f-183">Replace hello placeholder _&lt;mysql_server_name>_.</span></span>

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

<span data-ttu-id="9e01f-184">Сохраните изменения hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-184">Save hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="9e01f-185">данные подключения MySQL, этот файл уже исключен из репозитория Git hello toosecure (см. _.gitignore_ в корень репозитория hello).</span><span class="sxs-lookup"><span data-stu-id="9e01f-185">toosecure your MySQL connection information, this file is already excluded from hello Git repository (See _.gitignore_ in hello repository root).</span></span> <span data-ttu-id="9e01f-186">Позже вы узнаете, как переменные среды tooconfigure в tooyour tooconnect службы приложений базы данных в базе данных Azure для MySQL (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="9e01f-186">Later, you learn how tooconfigure environment variables in App Service tooconnect tooyour database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="9e01f-187">С помощью переменных среды не требуется hello *.env* файл в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="9e01f-187">With environment variables, you don't need hello *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="9e01f-188">Настройка SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="9e01f-188">Configure SSL certificate</span></span>

<span data-ttu-id="9e01f-189">По умолчанию база данных Azure для MySQL ограничивает SSL-соединений из клиентов.</span><span class="sxs-lookup"><span data-stu-id="9e01f-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="9e01f-190">tooconnect tooyour базы данных MySQL в Azure, необходимо использовать _.pem_ SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="9e01f-190">tooconnect tooyour MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="9e01f-191">Откройте _config/database.php_ и добавить hello _sslmode_ и _параметры_ параметры слишком`connections.mysql`, как показано в следующим hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-191">Open _config/database.php_ and add hello _sslmode_ and _options_ parameters too`connections.mysql`, as shown in hello following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="9e01f-192">toolearn как toogenerate это _certificate.pem_, в разделе [Настройка SSL-подключения в toosecurely вашего приложения подключения tooAzure базы данных MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="9e01f-192">toolearn how toogenerate this _certificate.pem_, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="9e01f-193">путь Hello _/ssl/certificate.pem_ указывает существующий tooan _certificate.pem_ файла в репозитории hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-193">hello path _/ssl/certificate.pem_ points tooan existing _certificate.pem_ file in hello Git repository.</span></span> <span data-ttu-id="9e01f-194">Этот файл предоставляется для удобства в рамках этого руководства.</span><span class="sxs-lookup"><span data-stu-id="9e01f-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="9e01f-195">Сертификаты _PEM_ не следует фиксировать в системе управления версиями.</span><span class="sxs-lookup"><span data-stu-id="9e01f-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-hello-application-locally"></a><span data-ttu-id="9e01f-196">Тестирование приложения hello локально</span><span class="sxs-lookup"><span data-stu-id="9e01f-196">Test hello application locally</span></span>

<span data-ttu-id="9e01f-197">Выполнить перенос базы данных Laravel с _. env.production_ как hello среды toocreate файл hello таблиц базы данных MySQL в базе данных Azure для MySQL (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="9e01f-197">Run Laravel database migrations with _.env.production_ as hello environment file toocreate hello tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="9e01f-198">Следует помнить, что _. env.production_ имеет базы данных MySQL tooyour hello подключения сведения в Azure.</span><span class="sxs-lookup"><span data-stu-id="9e01f-198">Remember that _.env.production_ has hello connection information tooyour MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="9e01f-199">Файл _.env.production_ еще не содержит действительный ключ приложения.</span><span class="sxs-lookup"><span data-stu-id="9e01f-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="9e01f-200">Создать новый для него в hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="9e01f-200">Generate a new one for it in hello terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="9e01f-201">Запустить образец приложения hello с _. env.production_ как файла среды hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-201">Run hello sample application with _.env.production_ as hello environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="9e01f-202">Перейдите в слишком`http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="9e01f-202">Navigate too`http://localhost:8000`.</span></span> <span data-ttu-id="9e01f-203">Если страница hello загружается без ошибок, hello приложения PHP — подключение toohello базы данных MySQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="9e01f-203">If hello page loads without errors, hello PHP application is connecting toohello MySQL database in Azure.</span></span>

<span data-ttu-id="9e01f-204">На странице приветствия добавьте несколько задач.</span><span class="sxs-lookup"><span data-stu-id="9e01f-204">Add a few tasks in hello page.</span></span>

![PHP подключается успешно tooAzure базы данных MySQL (Предварительная версия)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="9e01f-206">Введите toostop PHP, `Ctrl + C` в hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="9e01f-206">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="9e01f-207">Фиксация изменений</span><span class="sxs-lookup"><span data-stu-id="9e01f-207">Commit your changes</span></span>

<span data-ttu-id="9e01f-208">Выполните следующие команды toocommit Git hello изменения:</span><span class="sxs-lookup"><span data-stu-id="9e01f-208">Run hello following Git commands toocommit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="9e01f-209">Приложение будет готово toobe развертывания.</span><span class="sxs-lookup"><span data-stu-id="9e01f-209">Your app is ready toobe deployed.</span></span>

## <a name="deploy-tooazure"></a><span data-ttu-id="9e01f-210">Развертывание tooAzure</span><span class="sxs-lookup"><span data-stu-id="9e01f-210">Deploy tooAzure</span></span>

<span data-ttu-id="9e01f-211">На этом шаге развертывания tooAzure приложения PHP, подключенных к MySQL hello службы приложений.</span><span class="sxs-lookup"><span data-stu-id="9e01f-211">In this step, you deploy hello MySQL-connected PHP application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="9e01f-212">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="9e01f-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="9e01f-213">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9e01f-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a><span data-ttu-id="9e01f-214">Версия PHP hello Set</span><span class="sxs-lookup"><span data-stu-id="9e01f-214">Set hello PHP version</span></span>

<span data-ttu-id="9e01f-215">Набор hello PHP версии hello приложения необходимо выполнить с помощью hello [набор параметров конфигурации для веб-приложения az](/cli/azure/webapp/config#set) команды.</span><span class="sxs-lookup"><span data-stu-id="9e01f-215">Set hello PHP version that hello application requires by using hello [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="9e01f-216">Hello следующая команда задает версию too_7.0_ hello PHP.</span><span class="sxs-lookup"><span data-stu-id="9e01f-216">hello following command sets hello PHP version too_7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="9e01f-217">Настройка параметров базы данных</span><span class="sxs-lookup"><span data-stu-id="9e01f-217">Configure database settings</span></span>

<span data-ttu-id="9e01f-218">Как указывалось ранее, можно подключить tooyour базы данных MySQL в Azure с помощью переменных среды в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="9e01f-218">As pointed out previously, you can connect tooyour Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="9e01f-219">В службе приложений устанавливаются переменные среды, как _параметры приложения_ с помощью hello [az webapp конфигурации appsettings набора](/cli/azure/webapp/config/appsettings#set) команды.</span><span class="sxs-lookup"><span data-stu-id="9e01f-219">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="9e01f-220">Hello следующая команда настраивает параметры приложения hello `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, и `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="9e01f-220">hello following command configures hello app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="9e01f-221">Замените заполнители hello  _&lt;appname >_ и  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="9e01f-221">Replace hello placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="9e01f-222">Можно использовать hello PHP [getenv](http://www.php.net/manual/function.getenv.php) tooaccess метод hello параметры.</span><span class="sxs-lookup"><span data-stu-id="9e01f-222">You can use hello PHP [getenv](http://www.php.net/manual/function.getenv.php) method tooaccess hello settings.</span></span> <span data-ttu-id="9e01f-223">использует Hello кода Laravel [env](https://laravel.com/docs/5.4/helpers#method-env) оболочкой вокруг hello PHP `getenv`.</span><span class="sxs-lookup"><span data-stu-id="9e01f-223">hello Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over hello PHP `getenv`.</span></span> <span data-ttu-id="9e01f-224">Например, конфигурация hello MySQL в _config/database.php_ выглядит hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="9e01f-224">For example, hello MySQL configuration in _config/database.php_ looks like hello following code:</span></span>

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="9e01f-225">Настройка переменных среды Laravel</span><span class="sxs-lookup"><span data-stu-id="9e01f-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="9e01f-226">В среде Laravel требуется ключ приложения из службы приложений.</span><span class="sxs-lookup"><span data-stu-id="9e01f-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="9e01f-227">Его можно настроить с помощью параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="9e01f-227">You can configure it with app settings.</span></span>

<span data-ttu-id="9e01f-228">Используйте `php artisan` toogenerate новый ключ приложения без его сохранения too_.env_.</span><span class="sxs-lookup"><span data-stu-id="9e01f-228">Use `php artisan` toogenerate a new application key without saving it too_.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="9e01f-229">Задать ключ приложения hello в hello службы приложений веб-приложения с помощью hello [az webapp конфигурации appsettings набора](/cli/azure/webapp/config/appsettings#set) команды.</span><span class="sxs-lookup"><span data-stu-id="9e01f-229">Set hello application key in hello App Service web app by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="9e01f-230">Замените заполнители hello  _&lt;appname >_ и  _&lt;outputofphpartisankey: Создать >_.</span><span class="sxs-lookup"><span data-stu-id="9e01f-230">Replace hello placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="9e01f-231">`APP_DEBUG="true"`сообщает, что Laravel tooreturn отладочную информацию при hello развертывании веб-приложение сталкивается с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="9e01f-231">`APP_DEBUG="true"` tells Laravel tooreturn debugging information when hello deployed web app encounters errors.</span></span> <span data-ttu-id="9e01f-232">При выполнении приложения в рабочей среде, задать для него слишком`false`, которая является более безопасной.</span><span class="sxs-lookup"><span data-stu-id="9e01f-232">When running a production application, set it too`false`, which is more secure.</span></span>

### <a name="set-hello-virtual-application-path"></a><span data-ttu-id="9e01f-233">Задает путь к виртуальное приложение hello</span><span class="sxs-lookup"><span data-stu-id="9e01f-233">Set hello virtual application path</span></span>

<span data-ttu-id="9e01f-234">Задайте путь виртуального приложения hello hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9e01f-234">Set hello virtual application path for hello web app.</span></span> <span data-ttu-id="9e01f-235">Этот шаг является обязательным, поскольку hello [жизненного цикла приложения Laravel](https://laravel.com/docs/5.4/lifecycle) начинается в hello _открытый_ каталог вместо корневого каталога приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-235">This step is required because hello [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in hello _public_ directory instead of hello application's root directory.</span></span> <span data-ttu-id="9e01f-236">Другие платформы PHP, запуск которого жизненного цикла в корневом каталоге hello может работать без ручной настройки hello виртуальный путь к каталогу.</span><span class="sxs-lookup"><span data-stu-id="9e01f-236">Other PHP frameworks whose lifecycle start in hello root directory can work without manual configuration of hello virtual application path.</span></span>

<span data-ttu-id="9e01f-237">Набор hello виртуальный путь к каталогу с помощью hello [обновление ресурсов az](/cli/azure/resource#update) команды.</span><span class="sxs-lookup"><span data-stu-id="9e01f-237">Set hello virtual application path by using hello [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="9e01f-238">Замените hello  _&lt;appname >_ заполнителя.</span><span class="sxs-lookup"><span data-stu-id="9e01f-238">Replace hello _&lt;appname>_ placeholder.</span></span>

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

<span data-ttu-id="9e01f-239">По умолчанию службы приложений Azure указывает hello корневой виртуальный путь к каталогу (_/_) hello toohello корневого каталога развертывания файлов приложения (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="9e01f-239">By default, Azure App Service points hello root virtual application path (_/_) toohello root directory of hello deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="9e01f-240">Настойка пользователя развертывания</span><span class="sxs-lookup"><span data-stu-id="9e01f-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="9e01f-241">Настройка локального развертывания Git</span><span class="sxs-lookup"><span data-stu-id="9e01f-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a><span data-ttu-id="9e01f-242">Отправлять tooAzure из Git</span><span class="sxs-lookup"><span data-stu-id="9e01f-242">Push tooAzure from Git</span></span>

<span data-ttu-id="9e01f-243">Добавьте локальный tooyour Azure удаленный репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="9e01f-243">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="9e01f-244">Push-уведомлений приложения PHP hello Azure удаленный toodeploy toohello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-244">Push toohello Azure remote toodeploy hello PHP application.</span></span> <span data-ttu-id="9e01f-245">Запрашивается пароль hello ранее указан как часть создания hello hello пользователя развертывания.</span><span class="sxs-lookup"><span data-stu-id="9e01f-245">You are prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="9e01f-246">Во время развертывания служба приложений Azure будет взаимодействовать с Git.</span><span class="sxs-lookup"><span data-stu-id="9e01f-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> <span data-ttu-id="9e01f-247">Вы можете заметить, что процесс развертывания hello устанавливает [Composer](https://getcomposer.org/) пакеты в конце hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-247">You may notice that hello deployment process installs [Composer](https://getcomposer.org/) packages at hello end.</span></span> <span data-ttu-id="9e01f-248">Службы приложений не выполняет эти внесен во время развертывания по умолчанию, поэтому этот образец репозиторий имеет три дополнительных файлов в его корневой каталог tooenable:</span><span class="sxs-lookup"><span data-stu-id="9e01f-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory tooenable it:</span></span>
>
> - <span data-ttu-id="9e01f-249">`.deployment`— Это файл указывает службы приложений toorun `bash deploy.sh` как hello пользовательские сценарии.</span><span class="sxs-lookup"><span data-stu-id="9e01f-249">`.deployment` - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
> - <span data-ttu-id="9e01f-250">`deploy.sh`-hello пользовательские сценарии.</span><span class="sxs-lookup"><span data-stu-id="9e01f-250">`deploy.sh` - hello custom deployment script.</span></span> <span data-ttu-id="9e01f-251">При просмотре файла hello, вы увидите, что он работает `php composer.phar install` после `npm install`.</span><span class="sxs-lookup"><span data-stu-id="9e01f-251">If you review hello file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="9e01f-252">`composer.phar`-Диспетчер пакетов Composer hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-252">`composer.phar` - hello Composer package manager.</span></span>
>
> <span data-ttu-id="9e01f-253">Этот подход tooadd можно использовать любой шаг tooApp развертывания на основе Git tooyour службы.</span><span class="sxs-lookup"><span data-stu-id="9e01f-253">You can use this approach tooadd any step tooyour Git-based deployment tooApp Service.</span></span> <span data-ttu-id="9e01f-254">Дополнительные сведения см. в статье [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script) (Пользовательский сценарий развертывания).</span><span class="sxs-lookup"><span data-stu-id="9e01f-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="9e01f-255">Обзор toohello веб-приложение Azure</span><span class="sxs-lookup"><span data-stu-id="9e01f-255">Browse toohello Azure web app</span></span>

<span data-ttu-id="9e01f-256">Обзор слишком`http://<app_name>.azurewebsites.net` и добавьте список toohello несколько задач.</span><span class="sxs-lookup"><span data-stu-id="9e01f-256">Browse too`http://<app_name>.azurewebsites.net` and add a few tasks toohello list.</span></span>

![Приложение PHP, работающее в службе приложений Azure](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="9e01f-258">Вы запустили управляемое данными приложение PHP в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="9e01f-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="9e01f-259">Локальное обновление и повторное развертывание модели</span><span class="sxs-lookup"><span data-stu-id="9e01f-259">Update model locally and redeploy</span></span>

<span data-ttu-id="9e01f-260">На этом шаге вы Создание toohello простое изменение `task` данных модели и hello веб-приложения, а затем опубликовать tooAzure обновление hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-260">In this step, you make a simple change toohello `task` data model and hello webapp, and then publish hello update tooAzure.</span></span>

<span data-ttu-id="9e01f-261">Для сценария hello задачи необходимо изменить приложение hello образом можно пометить задачу как завершенную.</span><span class="sxs-lookup"><span data-stu-id="9e01f-261">For hello tasks scenario, you modify hello application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="9e01f-262">Добавление столбца</span><span class="sxs-lookup"><span data-stu-id="9e01f-262">Add a column</span></span>

<span data-ttu-id="9e01f-263">В hello терминалов перейдите toohello корень репозитория Git hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-263">In hello terminal, navigate toohello root of hello Git repository.</span></span>

<span data-ttu-id="9e01f-264">Создание новой базы данных миграции для hello `tasks` таблицы:</span><span class="sxs-lookup"><span data-stu-id="9e01f-264">Generate a new database migration for hello `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="9e01f-265">Это команда показывает hello имя файла hello миграции, который создается.</span><span class="sxs-lookup"><span data-stu-id="9e01f-265">This command shows you hello name of hello migration file that's generated.</span></span> <span data-ttu-id="9e01f-266">Найдите этот файл в каталоге _database/migrations_ и откройте его.</span><span class="sxs-lookup"><span data-stu-id="9e01f-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="9e01f-267">Замените hello `up` метод с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="9e01f-267">Replace hello `up` method with hello following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="9e01f-268">Hello предыдущий код добавляет логический столбец в hello `tasks` таблицу с именем `complete`.</span><span class="sxs-lookup"><span data-stu-id="9e01f-268">hello preceding code adds a boolean column in hello `tasks` table called `complete`.</span></span>

<span data-ttu-id="9e01f-269">Замените hello `down` метод после кода для действия отката hello hello:</span><span class="sxs-lookup"><span data-stu-id="9e01f-269">Replace hello `down` method with hello following code for hello rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="9e01f-270">В hello терминалов выполните изменения hello toomake миграции базы данных Laravel в hello локальной базы данных.</span><span class="sxs-lookup"><span data-stu-id="9e01f-270">In hello terminal, run Laravel database migrations toomake hello change in hello local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="9e01f-271">Зависимости hello [соглашение об именовании Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), модель hello `Task` (см. _app/Task.php_) сопоставляет toohello `tasks` таблицы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9e01f-271">Based on hello [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (see _app/Task.php_) maps toohello `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="9e01f-272">Обновление логики приложения</span><span class="sxs-lookup"><span data-stu-id="9e01f-272">Update application logic</span></span>

<span data-ttu-id="9e01f-273">Откройте hello *routes/web.php* файла.</span><span class="sxs-lookup"><span data-stu-id="9e01f-273">Open hello *routes/web.php* file.</span></span> <span data-ttu-id="9e01f-274">приложение Hello определяет его маршруты и здесь бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="9e01f-274">hello application defines its routes and business logic here.</span></span>

<span data-ttu-id="9e01f-275">В конце файла hello hello добавьте маршрут с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="9e01f-275">At hello end of hello file, add a route with hello following code:</span></span>

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

<span data-ttu-id="9e01f-276">Hello выше код позволяет модель данных toohello простое обновление, установив для параметра значение hello `complete`.</span><span class="sxs-lookup"><span data-stu-id="9e01f-276">hello preceding code makes a simple update toohello data model by toggling hello value of `complete`.</span></span>

### <a name="update-hello-view"></a><span data-ttu-id="9e01f-277">Обновить представление hello</span><span class="sxs-lookup"><span data-stu-id="9e01f-277">Update hello view</span></span>

<span data-ttu-id="9e01f-278">Откройте hello *resources/views/tasks.blade.php* файла.</span><span class="sxs-lookup"><span data-stu-id="9e01f-278">Open hello *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="9e01f-279">Найти hello `<tr>` открывающий тег и замените ее строкой:</span><span class="sxs-lookup"><span data-stu-id="9e01f-279">Find hello `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="9e01f-280">Здравствуйте, предшествующий код цвет строк hello меняется в зависимости от того, завершена ли задача hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-280">hello preceding code changes hello row color depending on whether hello task is complete.</span></span>

<span data-ttu-id="9e01f-281">В следующей строке hello у вас есть hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="9e01f-281">In hello next line, you have hello following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="9e01f-282">Замените всю строку hello hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="9e01f-282">Replace hello entire line with hello following code:</span></span>

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

<span data-ttu-id="9e01f-283">Hello предыдущий код добавляет кнопки "Отправить" hello, ссылается на hello маршрута, которое было определено ранее.</span><span class="sxs-lookup"><span data-stu-id="9e01f-283">hello preceding code adds hello submit button that references hello route that you defined earlier.</span></span>

### <a name="test-hello-changes-locally"></a><span data-ttu-id="9e01f-284">Тестирование hello изменения локально</span><span class="sxs-lookup"><span data-stu-id="9e01f-284">Test hello changes locally</span></span>

<span data-ttu-id="9e01f-285">Запустите из корневого каталога hello репозитории hello, сервер разработки hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-285">From hello root directory of hello Git repository, run hello development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="9e01f-286">toosee hello задач изменение состояния, переходы слишком`http://localhost:8000` и hello, установите флажок.</span><span class="sxs-lookup"><span data-stu-id="9e01f-286">toosee hello task status change, navigate too`http://localhost:8000` and select hello checkbox.</span></span>

![Добавлены флажок tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="9e01f-288">Введите toostop PHP, `Ctrl + C` в hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="9e01f-288">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="publish-changes-tooazure"></a><span data-ttu-id="9e01f-289">Публикация изменений tooAzure</span><span class="sxs-lookup"><span data-stu-id="9e01f-289">Publish changes tooAzure</span></span>

<span data-ttu-id="9e01f-290">В hello терминалов выполните Laravel миграции базы данных с hello рабочей строки toomake hello изменение соединения в hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9e01f-290">In hello terminal, run Laravel database migrations with hello production connection string toomake hello change in hello Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="9e01f-291">Применить все изменения hello в Git и затем отправьте tooAzure изменения кода hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-291">Commit all hello changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="9e01f-292">Здравствуйте, один раз `git push` завершения, перейдите toohello Azure web app и тестирования hello новые функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="9e01f-292">Once hello `git push` is complete, navigate toohello Azure web app and test hello new functionality.</span></span>

![TooAzure опубликованы изменения в модель и база данных](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="9e01f-294">Если вы добавили все задачи, они сохраняются в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="9e01f-294">If you added any tasks, they are retained in hello database.</span></span> <span data-ttu-id="9e01f-295">Схема данных toohello обновления затронута существующих данных.</span><span class="sxs-lookup"><span data-stu-id="9e01f-295">Updates toohello data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="9e01f-296">Потоковая передача журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="9e01f-296">Stream diagnostic logs</span></span>

<span data-ttu-id="9e01f-297">Пока hello приложения PHP в службе приложений Azure, вы можете получить tooyour выведенной журналы консоли hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="9e01f-297">While hello PHP application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="9e01f-298">Таким образом, можно получить hello же диагностические сообщения toohelp отладке ошибок приложения.</span><span class="sxs-lookup"><span data-stu-id="9e01f-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="9e01f-299">Журнал toostart потоковой передачи, используйте hello [заключительного фрагмента журнала webapp az](/cli/azure/webapp/log#tail) команды.</span><span class="sxs-lookup"><span data-stu-id="9e01f-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="9e01f-300">После запуска потоковой передачи журнала обновления hello Azure веб-приложения в браузере tooget hello некоторые веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="9e01f-300">Once log streaming has started, refresh hello Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="9e01f-301">Теперь можно увидеть терминалов выведенной toohello журналы консоли.</span><span class="sxs-lookup"><span data-stu-id="9e01f-301">You can now see console logs piped toohello terminal.</span></span> <span data-ttu-id="9e01f-302">Если журналы консоли не отображаются, проверьте еще раз через 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="9e01f-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="9e01f-303">Журнал toostop потоковую передачу в любое время, тип `Ctrl` + `C`.</span><span class="sxs-lookup"><span data-stu-id="9e01f-303">toostop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="9e01f-304">Приложение PHP можно использовать стандартный hello [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="9e01f-304">A PHP application can use hello standard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span></span> <span data-ttu-id="9e01f-305">Пример приложения Hello использует этот подход в _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="9e01f-305">hello sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="9e01f-306">Как это веб-платформа [Laravel использует Monolog](https://laravel.com/docs/5.4/errors) как hello регистратора.</span><span class="sxs-lookup"><span data-stu-id="9e01f-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as hello logging provider.</span></span> <span data-ttu-id="9e01f-307">toosee tooget Monolog toooutput сообщений консоли toohello разделе [PHP: как toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span><span class="sxs-lookup"><span data-stu-id="9e01f-307">toosee how tooget Monolog toooutput messages toohello console, see [PHP: How toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="9e01f-308">Управление hello Azure веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9e01f-308">Manage hello Azure web app</span></span>

<span data-ttu-id="9e01f-309">Go toohello [портал Azure](https://portal.azure.com) toomanage hello веб-приложения был создан.</span><span class="sxs-lookup"><span data-stu-id="9e01f-309">Go toohello [Azure portal](https://portal.azure.com) toomanage hello web app you created.</span></span>

<span data-ttu-id="9e01f-310">Hello в левом меню, щелкните **службы приложений**, а затем щелкните имя hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9e01f-310">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Веб-приложения портала навигации tooAzure](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="9e01f-312">Отобразится страница обзора вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9e01f-312">You see your web app's Overview page.</span></span> <span data-ttu-id="9e01f-313">Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="9e01f-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="9e01f-314">меню слева Hello предоставляет страницы настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="9e01f-314">hello left menu provides pages for configuring your app.</span></span>

![Страница службы приложений на портале Azure](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="9e01f-316">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e01f-316">Next steps</span></span>

<span data-ttu-id="9e01f-317">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="9e01f-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9e01f-318">Создание базы данных MySQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="9e01f-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="9e01f-319">Подключение tooMySQL приложения PHP</span><span class="sxs-lookup"><span data-stu-id="9e01f-319">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="9e01f-320">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="9e01f-320">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="9e01f-321">Обновить модель данных hello и повторно развернуть приложение hello</span><span class="sxs-lookup"><span data-stu-id="9e01f-321">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="9e01f-322">Потоковая передача журналов диагностики из Azure.</span><span class="sxs-lookup"><span data-stu-id="9e01f-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="9e01f-323">Управление приложение hello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9e01f-323">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="9e01f-324">Переместить следующий учебник toolearn toohello как toomap пользовательские DNS имя tooa веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9e01f-324">Advance toohello next tutorial toolearn how toomap a custom DNS name tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9e01f-325">Сопоставьте существующий пользовательский DNS имя tooAzure веб-приложений</span><span class="sxs-lookup"><span data-stu-id="9e01f-325">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
