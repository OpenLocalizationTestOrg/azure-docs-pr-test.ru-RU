---
title: "aaaBuild Node.js и MongoDB веб-приложения в Azure | Документы Microsoft"
description: "Узнайте, как tooget приложение Node.js в Azure, с tooa подключения Cosmos DB базы данных со строкой соединения MongoDB."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a>Разработка веб-приложения на основе Node.js и MongoDB в Azure

Веб-приложения Azure — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости. В этом учебнике показано, как веб-приложения в Azure и подключить его базы данных MongoDB tooa toocreate Node.js. После выполнения действий, описанных в этом руководстве, у вас появится приложение MEAN (MongoDB, Express, AngularJS и Node.js), выполняющееся в [службе приложений Azure](app-service-web-overview.md). Для простоты примера приложения hello используется hello [MEAN.js веб-платформа](http://meanjs.org/).

![Приложение MEAN.js, которое запущено в службе приложений Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * Создание базы данных MongoDB в Azure.
> * Подключение tooMongoDB приложение Node.js
> * Развертывание tooAzure приложения hello
> * Обновить модель данных hello и повторно развернуть приложение hello
> * Потоковая передача журналов диагностики из Azure.
> * Управление приложение hello в hello портал Azure

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника:

1. [установите Git](https://git-scm.com/);
1. [установите Node.j и NPM](https://nodejs.org/).
1. [Gulp.js](http://gulpjs.com/) (требуется для [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started));
1. [Установите и запустите MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/). 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-mongodb"></a>Проверка локальной базы данных MongoDB

Hello откройте окно терминала и `cd` toohello `bin` каталог установки MongoDB. Можно использовать это окно терминала toorun hello команды в этом учебнике.

Запустите `mongo` hello терминалов tooconnect tooyour локальном сервере, MongoDB.

```bash
mongo
```

Если подключение успешно установлено, это означает, что локальная база данных MongoDB запущена. В противном случае убедитесь, что локальной базы данных MongoDB запущена с hello процедуры, описанной в [установить MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/). Часто MongoDB установлена, но по-прежнему нужна toostart его, выполнив `mongod`. 

После завершения тестирования базы данных MongoDB, введите `Ctrl+C` в hello терминалов. 

## <a name="create-local-nodejs-app"></a>Создание локального приложения Node.js

На этом шаге настраивается hello локального проекта Node.js.

### <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

В окне терминала hello `cd` tooa рабочий каталог.  

Выполнения hello следующая команда репозитории примеров tooclone hello. 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

Этот образец репозиторий содержит копию hello [MEAN.js репозитория](https://github.com/meanjs/mean). Это измененный toorun на службы приложений (Дополнительные сведения см. в разделе репозитория hello MEAN.js [файл README](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).

### <a name="run-hello-application"></a>Запустите приложение hello

Выполните следующие команды tooinstall hello необходимые пакеты hello и запустите приложение hello.

```bash
cd meanjs
npm install
npm start
```

После полной загрузки приложение hello, вы увидите нечто похожее toohello следующие сообщения:

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

Перейдите toohttp://localhost:3000 в браузере. Нажмите кнопку **зарегистрироваться** в верхнем меню hello и Создание тестового пользователя. 

MEAN.js пример приложения Hello хранятся данные пользователя в базе данных hello. Если не возникает при создании пользователя, и вход в приложение записи базы данных локального MongoDB данных toohello.

![MEAN.js успешно подключается tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

Выберите **администрирования > Управление статьи** tooadd некоторые статьи.

toostop Node.js в любой момент нажмите `Ctrl+C` в hello терминалов. 

## <a name="create-production-mongodb"></a>Создание рабочей базы данных MongoDB

На этом шаге вы создадите базу данных MongoDB в Azure. Когда приложение будет развернутой tooAzure, база данных облака используется.

В качестве MongoDB в этом руководстве используется [Azure Cosmos DB](/azure/documentdb/). Cosmos DB поддерживает подключения клиентов MongoDB.

### <a name="log-in-tooazure"></a>Войдите в tooAzure

Вы будете использовать приложение toohost ресурсы, необходимые для hello toocreate hello Azure CLI 2.0 в Azure. Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Hello следующий пример создает группу ресурсов в Западной Европе hello.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

Используйте hello [список расположений az appservice](/cli/azure/appservice#list-locations) Azure CLI команды toolist доступных расположений. 

### <a name="create-a-cosmos-db-account"></a>Создание учетной записи Cosmos DB

Создать учетную запись Cosmos DB с hello [az cosmosdb создать](/cli/azure/cosmosdb#create) команды.

Hello следующую команду, подставьте уникальное имя для hello Cosmos DB  *\<cosmosdb_name >* заполнителя. Это имя используется в рамках hello hello Cosmos DB конечной точки, `https://<cosmosdb_name>.documents.azure.com/`, поэтому hello имя должно toobe уникальный всех учетных записей, Cosmos DB в Azure. Hello имя должно содержать только строчные буквы, цифры и знак дефиса (-) hello и должен находиться в диапазоне от 3 до 50 символов.

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

Hello *--kind MongoDB* обеспечивает MongoDB клиентских подключений.

При создании hello учетной записи Cosmos DB hello Azure CLI показано toohello аналогичные сведения, следующий пример:

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-tooproduction-mongodb"></a>Подключение приложения tooproduction MongoDB

На этом шаге подключиться MEAN.js образец приложения toohello Cosmos DB базы данных только что созданный, используя строку подключения MongoDB. 

### <a name="retrieve-hello-database-key"></a>Получить ключ hello базы данных

tooconnect toohello Cosmos DB базы данных, необходим ключ hello базы данных. Используйте hello [список ключей az cosmosdb](/cli/azure/cosmosdb#list-keys) команда tooretrieve hello первичный ключ.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

Hello Azure CLI показано toohello аналогичные сведения, следующий пример:

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Скопируйте значение hello `primaryMasterKey`. Эти сведения в следующем шаге hello необходимы.

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Настройка строки подключения hello в приложении Node.js

В репозитории MEAN.js откройте файл _config/env/production.js_.

В hello `db` объекта, обновите значение hello `uri`:

* Замените hello двух  *\<cosmosdb_name >* местозаполнителей Cosmos DB имя базы данных.
* Замените hello  *\<primary_master_key >* заполнитель с ключом hello, скопированным на предыдущем шаге hello.

Hello код отображает hello `db` объекта:

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

Hello `ssl=true` параметр является обязательным, поскольку [Cosmos DB необходим протокол SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 

Сохраните изменения.

### <a name="test-hello-application-in-production-mode"></a>Тестирование приложения hello в рабочий режим 

Выполните следующие команды toominify и пакет скриптов для производственной среды hello hello. Этот процесс создает hello файлов, необходимых hello рабочей среде.

```bash
gulp prod
```

Выполнения hello, следующая команда toouse hello строку соединения, то в _config/env/production.js_.

```bash
NODE_ENV=production node server.js
```

`NODE_ENV=production`Задает переменную среды hello, которая сообщает Node.js toorun в рабочей среде hello.  `node server.js`Здравствуйте, запускает сервер Node.js с `server.js` в корне репозитория. Так приложение Node.js загружается в Azure. 

При загрузке приложения hello, проверьте, выполняется в рабочей среде hello toomake:

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

Перейдите toohttp://localhost:8443 в браузере. Нажмите кнопку **зарегистрироваться** в верхнем меню hello и Создание тестового пользователя. Если успешного создания пользователя и выполните вход, приложение производит запись данных toohello Cosmos DB в Azure. 

В hello терминалов остановить Node.js, введя команду `Ctrl+C`. 

## <a name="deploy-app-tooazure"></a>Развертывание приложения tooAzure

На этом шаге развертывания вашего tooAzure приложений Node.js подключен MongoDB службы приложений.

### <a name="create-an-app-service-plan"></a>Создание плана службы приложений

Создать план служб приложений с hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команды. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Hello следующий пример создает план службы приложений с именем _myAppServicePlan_ с помощью hello **FREE** ценовой категории:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

При создании плана служб приложений hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a>Создание веб-приложения

Создание веб-приложения в hello `myAppServicePlan` план служб приложений с hello [создать веб-приложение az](/cli/azure/webapp#create) команды. 

Предоставляет приложение Hello веб вы размещения пространство toodeploy кода и предоставляет URL-адрес для вас tooview hello развернутого приложения. Используйте toocreate hello веб-приложения. 

Hello следующую команду, замените hello  *\<имя_приложения >* заполнитель с именем уникальный приложения. Это имя используется как часть URL-адрес по умолчанию hello в hello для веб-приложения hello, поэтому hello имя должно toobe уникальным для всех приложений в службе приложений Azure. 

```azurecli-interactive
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

### <a name="configure-an-environment-variable"></a>Настройка переменной среды

Ранее в hello учебник, вы жестко закодировано hello строку подключения базы данных в _config/env/production.js_. В соответствии с концепцией рекомендации по безопасности требуется tookeep конфиденциальные данные из своего репозитория Git. При запуске приложения в Azure строка подключения будет храниться в переменной среды.

В службе приложений устанавливаются переменные среды, как _параметры приложения_ с помощью hello [обновление конфигурации appsettings az webapp](/cli/azure/webapp/config/appsettings#update) команды. 

Hello следующий пример настраивает `MONGODB_URI` параметр приложения в Azure веб-приложения. Замените hello  *\<имя_приложения >*,  *\<cosmosdb_name >*, и  *\<primary_master_key >* заполнители.

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

В коде Node.js для доступа к этому параметру приложения, как и к любой переменной среды, используется `process.env.MONGODB_URI`. 

Теперь можно отмените вашей too_config/env/production.js_ изменения с hello следующую команду:

```bash
git checkout -- .
```

Повторно откройте файл _config/env/production.js_. Обратите внимание, приложение hello MEAN.js по умолчанию уже настроенного toouse hello `MONGODB_URI` созданной переменной среды.

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a>Настройка локального развертывания Git 

Используйте hello [набора пользователей для развертывания веб-приложения az](/cli/azure/webapp/deployment/user#set) команды toocreate учетные данные для развертывания.

Вы можете развернуть tooAzure вашего приложения службы приложений, различными способами, включая FTP, local Git, GitHub, Visual Studio Team Services и BitBucket. Для FTP и local Git, не нужны toohave пользователя развертывания на сервер tooauthenticate hello развертывание настроено. Этот пользователь развертывания уровня учетной записи, которая отличается от учетной записи подписки Azure. Требуется только tooconfigure этого пользователя развертывания один раз.

В hello следующую команду, замените  *\<имя пользователя >* и  *\<пароль >* новое имя пользователя и пароль. Hello имя пользователя должно быть уникальным. Hello пароль должен содержать по крайней мере 8 символов, с двумя hello следующие три элемента: буквы, цифры, символы. Если вы получаете ` 'Conflict'. Details: 409` ошибки, имя пользователя изменить hello. Если появляется сообщение об ошибке ` 'Bad Request'. Details: 400`, используйте более надежный пароль.

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

Запись hello имя пользователя и пароль для использования в последующих шагах, при развертывании приложения hello.

Используйте hello [развертывания источника az webapp config локальной git](/cli/azure/webapp/deployment/source#config-local-git) команда tooconfigure локальный Git доступа toohello веб-приложение Azure. 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

При настройке пользователя развертывания hello hello Azure CLI показаны hello следующая формата URL-адрес развертывания hello Azure веб-приложения.

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

Копировать выходные данные терминалов hello hello, как будет использоваться в следующем шаге hello. 

### <a name="push-tooazure-from-git"></a>Отправлять tooAzure из Git

Добавьте локальный tooyour Azure удаленный репозиторий Git. 

```bash
git remote add azure <paste_copied_url_here> 
```

Принудительно toohello Azure удаленный toodeploy приложение Node.js. Появится для hello пароль введен ранее в процессе создания hello hello пользователя развертывания. 

```bash
git push azure master
```

Во время развертывания служба приложений Azure будет взаимодействовать с Git.

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

Вы можете заметить, что выполняется процесс развертывания hello [Gulp](http://gulpjs.com/) после `npm install`. Службы приложений не выполняет Gulp или Grunt задач во время развертывания, поэтому этот репозиторий образец содержит два дополнительных файлов в его корневой каталог tooenable: 

- _.Deployment_ -это файл указывает toorun службы приложений `bash deploy.sh` как hello пользовательские сценарии.
- _Deploy.sh_ -hello пользовательские сценарии. При просмотре файла hello, вы увидите, что он работает `gulp prod` после `npm install` и `bower install`. 

Можно использовать этот подход tooadd tooyour любой шаг развертывания на основе Git. При перезапуске веб-приложения Azure в любой момент времени служба приложений не перезапускает эти задачи автоматизации.

### <a name="browse-toohello-azure-web-app"></a>Обзор toohello веб-приложение Azure 

Обзор toohello развертывания веб-приложения с помощью веб-браузере. 

```bash 
http://<app_name>.azurewebsites.net 
``` 

Нажмите кнопку **зарегистрироваться** в hello в верхнем меню, а также создать пустой. 

Если вы выполняются успешно, и приложение hello автоматически регистрируется в toohello создается пользователь, а затем MEAN.js приложения в Azure имеет базу данных MongoDB (Cosmos DB) toohello подключения. 

![Приложение MEAN.js, которое запущено в службе приложений Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Выберите **администрирования > Управление статьи** tooadd некоторые статьи. 

**Поздравляем!** Вы запустили управляемое данными приложение Node.js в службе приложений Azure.

## <a name="update-data-model-and-redeploy"></a>Обновление модели данных и повторное развертывание

На этом этапе вы измените hello `article` данных модели и публикация вашего tooAzure изменений.

### <a name="update-hello-data-model"></a>Обновление модели данных hello

Откройте файл _modules/articles/server/models/article.server.model.js_.

В `ArticleSchema` добавьте тип `String` с именем `comment`. Когда все будет готово, код схемы должен выглядеть следующим образом:

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-hello-articles-code"></a>Обновление кода hello статей

Обновить hello остальной части вашего `articles` кода toouse `comment`.

Существует пять файлов необходимо toomodify: hello server контроллера и представления hello четырех клиентов. 

Откройте файл _modules/articles/server/controllers/articles.server.controller.js_.

В hello `update` функцию, добавьте назначение для `article.comment`. Hello код отображает hello завершения `update` функции:

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

Откройте файл _modules/articles/client/views/view-article.client.view.html_.

Перед закрывающей hello `</section>` , добавьте следующие строки toodisplay hello `comment` вместе с rest hello hello данных статьи:

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

Откройте файл _modules/articles/client/views/list-articles.client.view.html_.

Перед закрывающей hello `</a>` , добавьте следующие строки toodisplay hello `comment` вместе с rest hello hello данных статьи:

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

Откройте файл _modules/articles/client/views/admin/list-articles.client.view.html_.

Внутри hello `<div class="list-group">` элемент и перед закрывающей hello `</a>` , добавьте следующие строки toodisplay hello `comment` вместе с rest hello hello данных статьи:

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

Откройте файл _modules/articles/client/views/admin/form-article.client.view.html_.

Найти hello `<div class="form-group">` элемент, содержащий hello кнопки "Отправить", которая выглядит следующим образом:

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

Непосредственно над этот тег добавьте еще один `<div class="form-group">` элемент, который позволит пользователям редактировать hello `comment` поля. Новый элемент должен выглядеть следующим образом:

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a>Проверьте изменения локально.

Сохраните изменения.

Проверьте изменения в рабочем режиме.

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> Следует помнить, что ваш _config/env/production.js_ была отменена и hello `MONGODB_URI` только задана переменная среды в Azure веб-приложения, а не на локальном компьютере. Если взглянуть на файл конфигурации hello обнаружится, что hello рабочую конфигурацию по умолчанию toouse локальной базы данных MongoDB. Это гарантирует, что при локальном тестировании изменений кода рабочие данные не будут затронуты.

Перейдите в слишком`http://localhost:8443` в браузере и убедитесь в том, что вы выполнили вход.

Выберите **администрирования > Управление статьи**, затем добавьте статью, выбрав hello  **+**  кнопки.

Вы видите hello новый `Comment` теперь текстовое поле.

![Добавлен комментарий tooArticles поля](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

В hello терминалов остановить Node.js, введя команду `Ctrl+C`. 

### <a name="publish-changes-tooazure"></a>Публикация изменений tooAzure

Фиксация изменений в Git, то принудительная tooAzure изменения кода hello.

```bash
git commit -am "added article comment"
git push azure master
```

Здравствуйте, один раз `git push` завершения, перейдите tooyour веб-приложение Azure и испытать новые функции hello.

![TooAzure опубликованы изменения в модель и база данных](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

Если вы добавляли статьи ранее, то вы увидите, что они по-прежнему отображаются. Существующие данные в Cosmos DB не теряются. Кроме того, схема данных toohello обновлений и оставляет без изменений существующих данных.

## <a name="stream-diagnostic-logs"></a>Потоковая передача журналов диагностики 

Во время работы приложения Node.js в службе приложений Azure, вы можете получить tooyour выведенной журналы консоли hello терминалов. Таким образом, можно получить hello же диагностические сообщения toohelp отладке ошибок приложения.

Журнал toostart потоковой передачи, используйте hello [заключительного фрагмента журнала webapp az](/cli/azure/webapp/log#tail) команды.

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

После запуска потоковой передачи журнала обновления Azure веб-приложения в браузере tooget hello некоторые веб-трафика. Теперь отображается журналы консоли по конвейеру tooyour терминала.

Чтобы в любое время отменить потоковую передачу журналов, введите `Ctrl+C`. 

## <a name="manage-your-azure-web-app"></a>Управление веб-приложением Azure

Go toohello [портал Azure](https://portal.azure.com) toosee hello веб-приложения был создан.

Hello в левом меню, щелкните **службы приложений**, затем щелкните имя hello Azure веб-приложения.

![Веб-приложения портала навигации tooAzure](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

По умолчанию hello портал отображает веб-приложения **Обзор** страницы. Здесь вы можете наблюдать за работой приложения. Вы также можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление. Hello вкладках hello левой части страницы приветствия отображаются страницы hello другой конфигурации, которые можно открыть.

![Страница службы приложений на портале Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a>Дальнейшие действия

Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Создание базы данных MongoDB в Azure.
> * Подключение tooMongoDB приложение Node.js
> * Развертывание tooAzure приложения hello
> * Обновить модель данных hello и повторно развернуть приложение hello
> * Журналы Azure tooyour терминалов потока
> * Управление приложение hello в hello портал Azure

Переместить следующий учебник toolearn toohello как toomap пользовательские DNS имя tooyour веб-приложения.

> [!div class="nextstepaction"] 
> [Сопоставьте существующий пользовательский DNS имя tooAzure веб-приложений](app-service-web-tutorial-custom-domain.md)
