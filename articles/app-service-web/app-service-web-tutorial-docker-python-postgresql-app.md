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
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a>Создание в Azure веб-приложения Docker Python с подключением к базе данных PostgreSQL

Веб-приложения Azure — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости. В этом учебнике показано, как toocreate основные Python Docker веб-приложения в Azure. Эта база данных PostgreSQL tooa приложения будет подключиться. После выполнения всех действий у вас будет приложение Python Flask, работающее в контейнере Docker в [веб-приложениях службы приложений Azure](app-service-web-overview.md).

![Приложение Docker Python Flask в службе приложений Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

Вы можете использовать описанные ниже шаги hello на macOS. Инструкции для Linux и Windows являются одинаковыми hello в большинстве случаев, но не hello различия описаны в этом учебнике.
 
## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника:

1. [установите Git](https://git-scm.com/);
1. [установите Python](https://www.python.org/downloads/).
1. [установите и запустите PostgreSQL](https://www.postgresql.org/download/);
1. [установите Docker Community Edition](https://www.docker.com/community-edition).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-postgresql-installation-and-create-a-database"></a>Проверка локальной установки PostgreSQL и создание базы данных

Откройте окно терминала hello и выполните `psql postgres` tooconnect tooyour локального сервера PostgreSQL.

```bash
psql postgres
```

Если подключение успешно установлено, это означает, что база данных PostgreSQL запущена. В противном случае убедитесь, что локальной базы данных PostgresQL запущена с hello процедуры, описанной в [загружает - Core распространения PostgreSQL](https://www.postgresql.org/download/).

Создайте базу данных *eventregistration* и настройте отдельного пользователя базы данных пользователя *manager* с паролем *supersecretpass*.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
Тип *\q* tooexit hello PostgreSQL клиента. 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a>Создание локального приложения Python Flask

На этом шаге настраивается hello локального проекта термосе Python.

### <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

Hello откройте окно терминала, и `CD` tooa рабочий каталог.  

Выполнения hello следующими командами tooclone hello образец репозитория и go toohello *initialapp 0,1* выпуска.

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

Этот пример репозитория содержит приложение [Flask](http://flask.pocoo.org/). 

### <a name="run-hello-application"></a>Запустите приложение hello

> [!NOTE] 
> На более позднем этапе упрощают процесс путем построения toouse контейнера Docker с hello рабочей базы данных.

Установка hello необходимые пакеты и запуск приложения hello.

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

После полной загрузки приложение hello, вы увидите нечто похожее toohello следующие сообщения:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Перейдите toohttp://127.0.0.1:5000 в браузере. Щелкните **Зарегистрировать** и создайте тестового пользователя.

![Приложение Python Flask, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

термосе пример приложения Hello хранятся данные пользователя в базе данных hello. Если сбой регистрации пользователя, приложение производит запись данных toohello локальных данных PostgreSQL.

сервер термосе toostop hello в любое время, введите сочетание клавиш Ctrl + C в hello терминалов. 

## <a name="create-a-production-postgresql-database"></a>Создание рабочей базы данных PostgreSQL

На этом шаге вы создадите базу данных PostgreSQL в Azure. Когда приложение будет развернутой tooAzure, он будет использовать эту базу данных в облаке.

### <a name="log-in-tooazure"></a>Войдите в tooAzure

В этом случае будет toouse hello Azure CLI 2.0 toocreate hello ресурсы необходимости toohost Python приложения в службе приложений Azure.  Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям. 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание [группы ресурсов](../azure-resource-manager/resource-group-overview.md) с hello [Создание группы az](/cli/azure/group#create). 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Hello следующий пример создает группу ресурсов в hello Запад США:

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

Используйте hello [список расположений az appservice](/cli/azure/appservice#list-locations) Azure CLI команды toolist доступных расположений.

### <a name="create-an-azure-database-for-postgresql-server"></a>Создание сервера базы данных Azure для PostgreSQL

Создать сервер PostgreSQL с hello [az postgres server создать](/cli/azure/documentdb#create) команды.

Hello следующую команду, подставьте уникальным именем сервера для hello  *\<postgresql_name >* заполнитель и имя пользователя для hello  *\<admin_username >* заполнителя . Имя сервера Hello используется как часть конечной точки PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), поэтому hello имя должно toobe уникальным для всех серверов в Azure. имя пользователя Hello предназначен для учетной записи администратора базы данных начальной hello. Все запрашиваемые toopick пароль для этого пользователя.

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

При создании hello базы данных Azure для сервера PostgreSQL hello Azure CLI показано toohello аналогичные сведения, следующий пример:

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

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a>Создание правила брандмауэра для hello базы данных Azure для сервера PostgreSQL

Запустите hello следующих Azure CLI команда tooallow toohello базы данных со всех IP-адресов.

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

Hello Azure CLI аналогичные toohello вывода следующий пример подтверждает hello создания правила брандмауэра:

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

## <a name="connect-your-python-flask-application-toohello-database"></a>Подключение базы данных приложения toohello термосе Python

На этом шаге подключения вашей термосе Python образец приложения toohello базы данных Azure для созданный сервер PostgreSQL.

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a>Создание пустой базы данных и настройка нового пользователя приложения базы данных

Создайте пользователя базы данных с tooa одной базы данных access только. Вы будете использовать эти учетные данные tooavoid, предоставляя полный доступ toohello hello приложения сервера.

Подключение базы данных toohello (появится запрос пароля администратора).

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

Создание базы данных hello и пользователя с hello PostgreSQL CLI.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

Тип *\q* tooexit hello PostgreSQL клиента.

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a>Тестирование приложения hello локально для базы данных Azure PostgreSQL hello 

Вернемся теперь toohello *приложения* папки hello клонированы репозитории Github, приложение hello термосе Python можно запустить, обновив hello переменные среды базы данных.

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

После полной загрузки приложение hello, вы увидите нечто похожее toohello следующие сообщения:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Перейдите toohttp://127.0.0.1:5000 в браузере. Щелкните **Зарегистрировать** и создайте тестовую регистрацию. Теперь вы пишете toohello базу данных в Azure.

![Приложение Python Flask, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a>Запуск приложения hello из контейнера Docker

Создать образ контейнера Docker hello.

```bash
cd ..
docker build -t flask-postgresql-sample .
```

Docker отображает подтверждение hello контейнера успешно создана.

```bash
Successfully built 7548f983a36b
```

Добавление переменной файла базы данных среды переменные tooan среды *db.env*. приложение Hello подключится к рабочей базе данных PostgreSQL toohello в Azure.

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

Запустите приложение hello из контейнера Docker hello. Hello следующая команда указывает файл переменных среды hello и сопоставляет hello по умолчанию термосе 5000 toolocal порта 5000.

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

Hello выходные данные выглядят аналогично toowhat, который приводился выше. Однако hello миграции первоначальная база данных больше не требуется выполнять toobe и таким образом пропускается.

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

Hello базы данных уже содержит регистрации hello, созданный ранее.

![Приложение Python Flask из контейнера Docker, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a>Отправка в реестре контейнеров tooa контейнера Docker hello

На этом шаге необходимо отправить реестре контейнеров tooa контейнера Docker hello. Вы будете использовать реестр контейнеров Azure, однако можно также использовать другие популярные реестры контейнеров, например Docker Hub.

### <a name="create-an-azure-container-registry"></a>Создание реестра контейнеров Azure

Замените в hello, следующая команда toocreate реестре контейнеров  *\<registry_name >* с именем реестра уникальный контейнер Azure по своему усмотрению.

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

Выходные данные
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

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a>Получить учетные данные реестра hello для принудительной отправки и извлекать образы Docker

tooshow учетные данные реестра, сначала включите режим администратора.

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

Вы увидите два пароля. Запишите имя пользователя hello и hello первый пароль.

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

### <a name="upload-your-docker-container-tooazure-container-registry"></a>Отправьте ваш tooAzure контейнера Docker реестра контейнера

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a>Развертывание tooAzure приложения hello термосе Python Docker

На этом шаге развертывания вашего Docker на основе контейнера термосе Python приложения tooAzure службы приложений.

### <a name="create-an-app-service-plan"></a>Создание плана службы приложений

Создать план служб приложений с hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команды. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Hello следующий пример создает план службы приложений под управлением Linux, с именем *myAppServicePlan* hello S1 ценовой категории с помощью:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

При создании плана служб приложений hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:

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

### <a name="create-a-web-app"></a>Создание веб-приложения

Создание веб-приложения в hello *myAppServicePlan* план служб приложений с hello [создать веб-приложение az](/cli/azure/webapp#create) команды. 

Предоставляет приложение Hello веб вы размещения пространство toodeploy кода и предоставляет URL-адрес для вас tooview hello развернутого приложения. Используйте toocreate hello веб-приложения. 

Hello следующую команду, замените hello  *\<имя_приложения >* заполнитель с именем уникальный приложения. Это имя является частью URL-адреса для веб-приложения hello, по умолчанию hello, поэтому hello имя должно toobe уникальным для всех приложений в службе приложений Azure. 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

При создании веб-приложения hello hello Azure CLI показано toohello аналогичные сведения, следующий пример: 

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

### <a name="configure-hello-database-environment-variables"></a>Настройка переменных среды hello базы данных

Ранее в учебнике hello определенные базы данных PostgreSQL tooyour tooconnect переменных среды.

В службе приложений устанавливаются переменные среды, как _параметры приложения_ с помощью hello [az webapp конфигурации appsettings набора](/cli/azure/webapp/config#set) команды. 

Hello пример указывает сведения о подключении базы данных hello как параметры приложения. Она также использует hello *ПОРТ* переменной toomap PORT 5000 из контейнера Docker трафика tooreceive HTTP на ПОРТ 80.

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a>Настройка развертывания контейнера Docker 

Служба приложений может автоматически скачать и запустить контейнер Docker.

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

При обновлении контейнера Docker hello или изменить параметры hello, перезапустите приложение hello. Перезапуск гарантирует, что все параметры будут применены и последнюю контейнера hello извлекается из реестра hello.

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a>Обзор toohello веб-приложение Azure 

Обзор toohello развертывания веб-приложения с помощью веб-браузере. 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> Hello веб-приложения требует больше времени, tooload, так как hello контейнер содержит toobe загружается и запускается после изменения конфигурации контейнера hello.

Вы увидите ранее зарегистрированного Гости, сохраненные в предыдущем шаге hello toohello Azure рабочей базы данных.

![Приложение Python Flask из контейнера Docker, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

**Поздравляем!** Вы запустили приложение Python Flask из контейнера Docker в службе приложений Azure.

## <a name="update-data-model-and-redeploy"></a>Обновление модели данных и повторное развертывание

На этом шаге необходимо добавить номер hello регистрации событий tooeach участников, обновив hello гостевой модели.

Извлечение hello *миграции 0,2* выпуска с hello следующую команду git:

```bash
git checkout tags/0.2-migration
```

Этот выпуск уже внесены hello tooviews необходимые изменения, контроллеры и модели. Он также включает в себя перенос базы данных с использованием *Alembic* (`flask db migrate`). Можно просмотреть все изменения, сделанные посредством hello следующую команду git:

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a>Проверьте изменения локально.

Запустите следующие команды tootest hello изменения локально, работающего сервера термосе hello.

MAC и Linux:
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Перейдите toohttp://127.0.0.1:5000 изменения hello tooview браузера. Создайте тестовую регистрацию.

![Приложение Python Flask из контейнера Docker, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a>Публикация изменений tooAzure

Создать новый образ docker hello, принудительно отправить его toohello контейнер реестра и перезапустите приложение hello.

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

Перейдите tooyour веб-приложение Azure и испытать новые функции hello. Создайте еще одну регистрацию событий.

```bash 
http://<app_name>.azurewebsites.net 
```

![Приложение Docker Python Flask в службе приложений Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a>Управление веб-приложением Azure

Go toohello [портал Azure](https://portal.azure.com) toosee hello веб-приложения был создан.

Hello в левом меню, щелкните **службы приложений**, затем щелкните имя hello Azure веб-приложения.

![Веб-приложения портала навигации tooAzure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

По умолчанию hello портал отображает веб-приложения **Обзор** страницы. Здесь вы можете наблюдать за работой приложения. Вы также можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление. Hello вкладках hello левой части страницы приветствия отображаются страницы hello другой конфигурации, которые можно открыть.

![Страница службы приложений на портале Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a>Дальнейшие действия

Переместить следующий учебник toolearn toohello как toomap пользовательские DNS имя tooyour веб-приложения.

> [!div class="nextstepaction"] 
> [Сопоставьте существующий пользовательский DNS имя tooAzure веб-приложений](app-service-web-tutorial-custom-domain.md)
