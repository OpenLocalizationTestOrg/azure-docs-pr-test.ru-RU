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
# <a name="build-a-php-and-mysql-web-app-in-azure"></a>Создание веб-приложения PHP в Azure с подключением к базе данных MySQL

[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости. В этом учебнике показано, как toocreate PHP веб-приложения в Azure и соедините его tooa базы данных MySQL. По завершении вы получите приложение [Laravel](https://laravel.com/), работающее в веб-приложениях службы приложений Azure.

![Приложение PHP, работающее в службе приложений Azure](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * Создание базы данных MySQL в Azure.
> * Подключение tooMySQL приложения PHP
> * Развертывание tooAzure приложения hello
> * Обновить модель данных hello и повторно развернуть приложение hello
> * Потоковая передача журналов диагностики из Azure.
> * Управление приложение hello в hello портал Azure

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника:

* [установите Git](https://git-scm.com/);
* [PHP 5.6.4 или более поздней версии](http://php.net/downloads.php);
* [Composer](https://getcomposer.org/doc/00-intro.md);
* Включить следующие расширения PHP Laravel потребностей hello: OpenSSL, PDO MySQL, Mbstring, разметчика, XML
* [MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) (этот компонент потребуется запустить). 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a>Подготовка локальной базы данных MySQL

На этом шаге вы создадите базу данных на локальном сервере MySQL для использования в этом руководстве.

### <a name="connect-toolocal-mysql-server"></a>Подключение сервера MySQL toolocal

В окне терминала подключение tooyour локального сервера MySQL. Можно использовать это окно терминала toorun hello команды в этом учебнике.

```bash
mysql -u root -p
```

Если появится запрос пароля, введите пароль hello для hello `root` учетной записи. Если вы не помните пароль корневой учетной записи, см. раздел [MySQL: как tooReset hello пароль учетной записи Root](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Если команда выполнена успешно, значит, сервер MySQL работает. Если это не так, убедитесь в том, локальному серверу MySQL запущен из следующих hello [действий после установки MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database-locally"></a>Локальное создание базы данных

В hello `mysql` запрос, создать базу данных.

```sql 
CREATE DATABASE sampledb;
```

Завершите подключение к серверу, введя команду `quit`.

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a>Локальное создание приложения PHP
На этом шаге вы создадите пример приложения Laravel, настроите его подключение к базе данных и запустите это приложение в локальной среде. 

### <a name="clone-hello-sample"></a>Образец hello клонирования

В окне терминала hello `cd` tooa рабочий каталог.

Выполнения hello следующая команда репозитории примеров tooclone hello.

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

`cd`точная копия каталог tooyour.
Установите пакеты необходимых hello.

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a>Настройка подключения к MySQL

В корневом хранилище hello, создайте файл с именем *.env*. Следующие переменные в hello hello копирования *.env* файла. Замените hello  _&lt;root_password >_ заполнитель hello MySQL корневой пароль.

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

Дополнительные сведения об использовании hello Laravel _.env_ файла см. в разделе [конфигурации среды Laravel](https://laravel.com/docs/5.4/configuration#environment-configuration).

### <a name="run-hello-sample-locally"></a>Запуск образца hello локально

Запустите [миграции базы данных Laravel](https://laravel.com/docs/5.4/migrations) toocreate hello таблицы потребностей приложения hello. таблицы, для которых создаются при миграции hello в поиск в hello toosee _базы данных или миграции_ каталог в репозитории hello.

```bash
php artisan migrate
```

Создайте ключ приложения Laravel.

```bash
php artisan key:generate
```

Запустите приложение hello.

```bash
php artisan serve
```

Перейдите в слишком`http://localhost:8000` в браузере. На странице приветствия добавьте несколько задач.

![PHP успешно подключается tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

Введите toostop PHP, `Ctrl + C` в hello терминалов.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a>Создание базы данных MySQL в Azure

На этом шаге вы создадите базу данных MySQL в [базе данных Azure для MySQL (предварительная версия)](/azure/mysql). Впоследствии можно настроить базу данных toothis tooconnect приложения hello PHP.

### <a name="create-a-resource-group"></a>Создание группы ресурсов

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a>Создание сервера MySQL

Создать сервер базы данных Azure для MySQL (Предварительная версия) с hello [создать сервер mysql az](/cli/azure/mysql/server#create) команды.

Hello следующую команду, заменить имя сервера MySQL, где вы видите hello  _&lt;mysql_server_name >_ заполнитель (допустимые символы — `a-z`, `0-9`, и `-`). Это имя является частью имени узла сервера MySQL hello (`<mysql_server_name>.database.windows.net`), ему toobe глобально уникальным.

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

При создании сервера MySQL hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:

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

### <a name="configure-server-firewall"></a>Настройка брандмауэра сервера

Создать правило брандмауэра для MySQL server tooallow клиентских соединений с помощью hello [az mysql правила брандмауэра для сервера — создание](/cli/azure/mysql/server/firewall-rule#create) команды.

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> В настоящее время подключений только tooAzure служб не ограничить базы данных Azure для MySQL (Предварительная версия). Как динамически назначаются IP-адресов в Azure, это лучше tooenable все IP-адреса. Hello служба находится в предварительной версии. В ближайшем будущем будут добавлены более надежные методы защиты базы данных.
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a>Подключение сервера MySQL tooproduction локально

В окне терминала hello подключение toohello MySQL server в Azure. Используйте значение hello, указанную ранее  _&lt;mysql_server_name >_.

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

При появлении запроса пароля используйте _$tr0ngPa$ w0rd!_, который был указан при создании hello базы данных.

### <a name="create-a-production-database"></a>Создание рабочей базы данных

В hello `mysql` запрос, создать базу данных.

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a>Создание пользователя с разрешениями

Создание пользователя базы данных с именем _phpappuser_ и присвойте ему все привилегии в hello `sampledb` базы данных.

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

Закрыть соединение с сервером hello, введя `quit`.

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a>Подключение приложения tooAzure MySQL

На этом шаге подключиться hello PHP приложения toohello базы данных MySQL, созданных в базе данных Azure для MySQL (Предварительная версия).

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a>Подключение к базе данных hello

Создайте в корень репозитория hello, _. env.production_ hello файл и скопируйте следующие переменные в него. Замените заполнитель hello  _&lt;mysql_server_name >_.

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

Сохраните изменения hello.

> [!TIP]
> данные подключения MySQL, этот файл уже исключен из репозитория Git hello toosecure (см. _.gitignore_ в корень репозитория hello). Позже вы узнаете, как переменные среды tooconfigure в tooyour tooconnect службы приложений базы данных в базе данных Azure для MySQL (Предварительная версия). С помощью переменных среды не требуется hello *.env* файл в службе приложений.
>

### <a name="configure-ssl-certificate"></a>Настройка SSL-сертификата

По умолчанию база данных Azure для MySQL ограничивает SSL-соединений из клиентов. tooconnect tooyour базы данных MySQL в Azure, необходимо использовать _.pem_ SSL-сертификат.

Откройте _config/database.php_ и добавить hello _sslmode_ и _параметры_ параметры слишком`connections.mysql`, как показано в следующим hello.

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

toolearn как toogenerate это _certificate.pem_, в разделе [Настройка SSL-подключения в toosecurely вашего приложения подключения tooAzure базы данных MySQL](../mysql/howto-configure-ssl.md).

> [!TIP]
> путь Hello _/ssl/certificate.pem_ указывает существующий tooan _certificate.pem_ файла в репозитории hello. Этот файл предоставляется для удобства в рамках этого руководства. Сертификаты _PEM_ не следует фиксировать в системе управления версиями. 
>

### <a name="test-hello-application-locally"></a>Тестирование приложения hello локально

Выполнить перенос базы данных Laravel с _. env.production_ как hello среды toocreate файл hello таблиц базы данных MySQL в базе данных Azure для MySQL (Предварительная версия). Следует помнить, что _. env.production_ имеет базы данных MySQL tooyour hello подключения сведения в Azure.

```bash
php artisan migrate --env=production --force
```

Файл _.env.production_ еще не содержит действительный ключ приложения. Создать новый для него в hello терминалов.

```bash
php artisan key:generate --env=production --force
```

Запустить образец приложения hello с _. env.production_ как файла среды hello.

```bash
php artisan serve --env=production
```

Перейдите в слишком`http://localhost:8000`. Если страница hello загружается без ошибок, hello приложения PHP — подключение toohello базы данных MySQL в Azure.

На странице приветствия добавьте несколько задач.

![PHP подключается успешно tooAzure базы данных MySQL (Предварительная версия)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

Введите toostop PHP, `Ctrl + C` в hello терминалов.

### <a name="commit-your-changes"></a>Фиксация изменений

Выполните следующие команды toocommit Git hello изменения:

```bash
git add .
git commit -m "database.php updates"
```

Приложение будет готово toobe развертывания.

## <a name="deploy-tooazure"></a>Развертывание tooAzure

На этом шаге развертывания tooAzure приложения PHP, подключенных к MySQL hello службы приложений.

### <a name="create-an-app-service-plan"></a>Создание плана службы приложений

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a>Создание веб-приложения

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a>Версия PHP hello Set

Набор hello PHP версии hello приложения необходимо выполнить с помощью hello [набор параметров конфигурации для веб-приложения az](/cli/azure/webapp/config#set) команды.

Hello следующая команда задает версию too_7.0_ hello PHP.

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a>Настройка параметров базы данных

Как указывалось ранее, можно подключить tooyour базы данных MySQL в Azure с помощью переменных среды в службе приложений.

В службе приложений устанавливаются переменные среды, как _параметры приложения_ с помощью hello [az webapp конфигурации appsettings набора](/cli/azure/webapp/config/appsettings#set) команды.

Hello следующая команда настраивает параметры приложения hello `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, и `DB_PASSWORD`. Замените заполнители hello  _&lt;appname >_ и  _&lt;mysql_server_name >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

Можно использовать hello PHP [getenv](http://www.php.net/manual/function.getenv.php) tooaccess метод hello параметры. использует Hello кода Laravel [env](https://laravel.com/docs/5.4/helpers#method-env) оболочкой вокруг hello PHP `getenv`. Например, конфигурация hello MySQL в _config/database.php_ выглядит hello, следующий код:

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

### <a name="configure-laravel-environment-variables"></a>Настройка переменных среды Laravel

В среде Laravel требуется ключ приложения из службы приложений. Его можно настроить с помощью параметров приложения.

Используйте `php artisan` toogenerate новый ключ приложения без его сохранения too_.env_.

```bash
php artisan key:generate --show
```

Задать ключ приложения hello в hello службы приложений веб-приложения с помощью hello [az webapp конфигурации appsettings набора](/cli/azure/webapp/config/appsettings#set) команды. Замените заполнители hello  _&lt;appname >_ и  _&lt;outputofphpartisankey: Создать >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

`APP_DEBUG="true"`сообщает, что Laravel tooreturn отладочную информацию при hello развертывании веб-приложение сталкивается с ошибкой. При выполнении приложения в рабочей среде, задать для него слишком`false`, которая является более безопасной.

### <a name="set-hello-virtual-application-path"></a>Задает путь к виртуальное приложение hello

Задайте путь виртуального приложения hello hello веб-приложения. Этот шаг является обязательным, поскольку hello [жизненного цикла приложения Laravel](https://laravel.com/docs/5.4/lifecycle) начинается в hello _открытый_ каталог вместо корневого каталога приложения hello. Другие платформы PHP, запуск которого жизненного цикла в корневом каталоге hello может работать без ручной настройки hello виртуальный путь к каталогу.

Набор hello виртуальный путь к каталогу с помощью hello [обновление ресурсов az](/cli/azure/resource#update) команды. Замените hello  _&lt;appname >_ заполнителя.

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

По умолчанию службы приложений Azure указывает hello корневой виртуальный путь к каталогу (_/_) hello toohello корневого каталога развертывания файлов приложения (_sites\wwwroot_).

### <a name="configure-a-deployment-user"></a>Настойка пользователя развертывания

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a>Настройка локального развертывания Git

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a>Отправлять tooAzure из Git

Добавьте локальный tooyour Azure удаленный репозиторий Git.

```bash
git remote add azure <paste_copied_url_here>
```

Push-уведомлений приложения PHP hello Azure удаленный toodeploy toohello. Запрашивается пароль hello ранее указан как часть создания hello hello пользователя развертывания.

```bash
git push azure master
```

Во время развертывания служба приложений Azure будет взаимодействовать с Git.

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
> Вы можете заметить, что процесс развертывания hello устанавливает [Composer](https://getcomposer.org/) пакеты в конце hello. Службы приложений не выполняет эти внесен во время развертывания по умолчанию, поэтому этот образец репозиторий имеет три дополнительных файлов в его корневой каталог tooenable:
>
> - `.deployment`— Это файл указывает службы приложений toorun `bash deploy.sh` как hello пользовательские сценарии.
> - `deploy.sh`-hello пользовательские сценарии. При просмотре файла hello, вы увидите, что он работает `php composer.phar install` после `npm install`.
> - `composer.phar`-Диспетчер пакетов Composer hello.
>
> Этот подход tooadd можно использовать любой шаг tooApp развертывания на основе Git tooyour службы. Дополнительные сведения см. в статье [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script) (Пользовательский сценарий развертывания).
>

### <a name="browse-toohello-azure-web-app"></a>Обзор toohello веб-приложение Azure

Обзор слишком`http://<app_name>.azurewebsites.net` и добавьте список toohello несколько задач.

![Приложение PHP, работающее в службе приложений Azure](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

Вы запустили управляемое данными приложение PHP в службе приложений Azure.

## <a name="update-model-locally-and-redeploy"></a>Локальное обновление и повторное развертывание модели

На этом шаге вы Создание toohello простое изменение `task` данных модели и hello веб-приложения, а затем опубликовать tooAzure обновление hello.

Для сценария hello задачи необходимо изменить приложение hello образом можно пометить задачу как завершенную.

### <a name="add-a-column"></a>Добавление столбца

В hello терминалов перейдите toohello корень репозитория Git hello.

Создание новой базы данных миграции для hello `tasks` таблицы:

```bash
php artisan make:migration add_complete_column --table=tasks
```

Это команда показывает hello имя файла hello миграции, который создается. Найдите этот файл в каталоге _database/migrations_ и откройте его.

Замените hello `up` метод с hello, следующий код:

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

Hello предыдущий код добавляет логический столбец в hello `tasks` таблицу с именем `complete`.

Замените hello `down` метод после кода для действия отката hello hello:

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

В hello терминалов выполните изменения hello toomake миграции базы данных Laravel в hello локальной базы данных.

```bash
php artisan migrate
```

Зависимости hello [соглашение об именовании Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), модель hello `Task` (см. _app/Task.php_) сопоставляет toohello `tasks` таблицы по умолчанию.

### <a name="update-application-logic"></a>Обновление логики приложения

Откройте hello *routes/web.php* файла. приложение Hello определяет его маршруты и здесь бизнес-логики.

В конце файла hello hello добавьте маршрут с hello, следующий код:

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

Hello выше код позволяет модель данных toohello простое обновление, установив для параметра значение hello `complete`.

### <a name="update-hello-view"></a>Обновить представление hello

Откройте hello *resources/views/tasks.blade.php* файла. Найти hello `<tr>` открывающий тег и замените ее строкой:

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

Здравствуйте, предшествующий код цвет строк hello меняется в зависимости от того, завершена ли задача hello.

В следующей строке hello у вас есть hello, следующий код:

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

Замените всю строку hello hello, следующий код:

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

Hello предыдущий код добавляет кнопки "Отправить" hello, ссылается на hello маршрута, которое было определено ранее.

### <a name="test-hello-changes-locally"></a>Тестирование hello изменения локально

Запустите из корневого каталога hello репозитории hello, сервер разработки hello.

```bash
php artisan serve
```

toosee hello задач изменение состояния, переходы слишком`http://localhost:8000` и hello, установите флажок.

![Добавлены флажок tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

Введите toostop PHP, `Ctrl + C` в hello терминалов.

### <a name="publish-changes-tooazure"></a>Публикация изменений tooAzure

В hello терминалов выполните Laravel миграции базы данных с hello рабочей строки toomake hello изменение соединения в hello базы данных SQL Azure.

```bash
php artisan migrate --env=production --force
```

Применить все изменения hello в Git и затем отправьте tooAzure изменения кода hello.

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

Здравствуйте, один раз `git push` завершения, перейдите toohello Azure web app и тестирования hello новые функциональные возможности.

![TooAzure опубликованы изменения в модель и база данных](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Если вы добавили все задачи, они сохраняются в базе данных hello. Схема данных toohello обновления затронута существующих данных.

## <a name="stream-diagnostic-logs"></a>Потоковая передача журналов диагностики

Пока hello приложения PHP в службе приложений Azure, вы можете получить tooyour выведенной журналы консоли hello терминалов. Таким образом, можно получить hello же диагностические сообщения toohelp отладке ошибок приложения.

Журнал toostart потоковой передачи, используйте hello [заключительного фрагмента журнала webapp az](/cli/azure/webapp/log#tail) команды.

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

После запуска потоковой передачи журнала обновления hello Azure веб-приложения в браузере tooget hello некоторые веб-трафика. Теперь можно увидеть терминалов выведенной toohello журналы консоли. Если журналы консоли не отображаются, проверьте еще раз через 30 секунд.

Журнал toostop потоковую передачу в любое время, тип `Ctrl` + `C`.

> [!TIP]
> Приложение PHP можно использовать стандартный hello [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello консоли. Пример приложения Hello использует этот подход в _app/Http/routes.php_.
>
> Как это веб-платформа [Laravel использует Monolog](https://laravel.com/docs/5.4/errors) как hello регистратора. toosee tooget Monolog toooutput сообщений консоли toohello разделе [PHP: как toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).
>
>

## <a name="manage-hello-azure-web-app"></a>Управление hello Azure веб-приложения

Go toohello [портал Azure](https://portal.azure.com) toomanage hello веб-приложения был создан.

Hello в левом меню, щелкните **службы приложений**, а затем щелкните имя hello Azure веб-приложения.

![Веб-приложения портала навигации tooAzure](./media/app-service-web-tutorial-php-mysql/access-portal.png)

Отобразится страница обзора вашего веб-приложения. Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.

меню слева Hello предоставляет страницы настройки приложения.

![Страница службы приложений на портале Azure](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a>Дальнейшие действия

Из этого руководства вы узнали, как выполнять такие задачи:

> [!div class="checklist"]
> * Создание базы данных MySQL в Azure.
> * Подключение tooMySQL приложения PHP
> * Развертывание tooAzure приложения hello
> * Обновить модель данных hello и повторно развернуть приложение hello
> * Потоковая передача журналов диагностики из Azure.
> * Управление приложение hello в hello портал Azure

Переместить следующий учебник toolearn toohello как toomap пользовательские DNS имя tooa веб-приложения.

> [!div class="nextstepaction"]
> [Сопоставьте существующий пользовательский DNS имя tooAzure веб-приложений](app-service-web-tutorial-custom-domain.md)
