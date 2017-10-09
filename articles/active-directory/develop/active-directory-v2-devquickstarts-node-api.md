---
title: "aaaSecure веб-API Azure Active Directory версии 2.0 с помощью Node.js | Документы Microsoft"
description: "Узнайте, как toobuild Node.js веб-API, который принимает токены из личную учетную запись Майкрософт и рабочих или учебных учетных записей."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a>Защита веб-API с помощью Node.js
> [!NOTE]
> Не все сценарии Azure Active Directory и возможности работы с конечной точкой v2.0 hello. toodetermine необходимость использования hello v2.0 конечная точка либо hello v1.0, узнайте, как [ограничения v2.0](active-directory-v2-limitations.md).
> 
> 

При использовании endpoint v2.0 hello Azure Active Directory (Azure AD), можно использовать [OAuth 2.0](active-directory-v2-protocols.md) маркеры доступа tooprotect веб-API. С помощью маркеров доступа OAuth 2.0 пользователи с личными учетными записями Майкрософт и рабочими или учебными учетными записями могут безопасно обращаться в вашему веб-API.

*Passport* — промежуточный слой проверки подлинности для Node.js. Он отличается гибкой модульной структурой, которая позволяет сравнительно незаметно размещать его в любом приложении на основе Express или веб-приложении Restify. В Passport полный набор стратегий поддерживает процесс проверки подлинности с помощью имени пользователя и пароля, Facebook, Twitter и проч. Мы разработали стратегию для Azure AD. В этой статье рассказывается как tooinstall hello модуля, а затем добавьте hello Azure AD `passport-azure-ad` подключаемого модуля.

## <a name="download"></a>Загрузить
поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs). toofollow hello учебник, вы можете [загрузить приложение hello основу как ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), или основу hello клона:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

Можно также получить приложение hello завершено в конце hello этого учебника.

## <a name="1-register-an-app"></a>Шаг 1. Регистрация приложения
Создайте новое приложение на [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), или выполните [эти подробные шаги](active-directory-v2-app-registration.md) tooregister приложения. Не забудьте выполнить следующие действия.

* Копировать hello **идентификатор приложения** назначенный tooyour приложения. Он потребуется для работы с этим руководством.
* Добавить hello **Mobile** платформы для приложения.
* Копировать hello **URI перенаправления** из портала hello. Необходимо использовать значение по умолчанию URI hello `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-install-nodejs"></a>Шаг 2. Установка Node.js
Образец hello toouse для этого учебника, необходимо [установки Node.js](http://nodejs.org).

## <a name="3-install-mongodb"></a>Шаг 3. Установка MongoDB
toosuccessfully использование этого образца, необходимо [установить MongoDB](http://www.mongodb.org). В этом образце используется MongoDB toomake постоянные REST API по экземплярам сервера.

> [!NOTE]
> В этой статье предполагается, что конечные точки установки и сервером по умолчанию hello используется для MongoDB: mongodb://localhost.
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a>4: install hello restify модулей в веб-API
Мы используем Resitfy toobuild нашем API REST. Restify — это минималистичная и гибкая платформа для приложений Node.j, созданная на основе Express. Restify имеет широкий набор функций, которые можно использовать API-интерфейс REST на основе Connect toobuild.

### <a name="install-restify"></a>Установка Restify
1.  В командной строке измените каталог hello слишком**azuread**:

    `cd azuread`

    Если hello **azuread** каталог не существует, создайте его:

    `mkdir azuread`

2.  Установите Restify.

    `npm install restify`

    Hello выходные данные этой команды должен выглядеть следующим образом:

    ```
    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a>Вы получили сообщение об ошибке?
В некоторых операционных системах при использовании hello `npm` команда, может появиться это сообщение: `Error: EPERM, chmod '/usr/local/bin/..'`. Ошибка Hello сопровождается запроса, попробуйте выполнить выполняющейся hello учетной записи с правами администратора. В этом случае команда hello `sudo` toorun `npm` на более высоком уровне привилегий.

#### <a name="did-you-get-an-error-related-toodtrace"></a>Было возникнет ошибка, связанная tooDTrace?
При установке Restify может появиться следующее сообщение:

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

Restify имеет tootrace мощный механизм, с помощью DTrace вызовы REST. Однако во многих операционных системах DTrace отсутствует. Это сообщение об ошибке можно игнорировать.


## <a name="5-install-passportjs-in-your-web-api"></a>Шаг 5. Установка Passport.js для веб-интерфейса API
1.  В командной строке hello изменить каталог hello слишком**azuread**.

2.  Установите Passport.js.

    `npm install passport`

    Hello выходные данные команды hello должен выглядеть следующим образом:

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a>6: Добавление веб-API tooyour passport azure ad
Добавьте hello OAuth стратегии, с помощью passport azuread. `passport-azuread` — это набор стратегий, который устанавливает подключение Azure AD к Passport. В этом примере REST API мы будем использовать эту стратегию для токенов носителя.

> [!NOTE]
> Платформа OAuth 2.0 позволяет выдавать маркеры любого известного типа, но в большинстве случаев используются маркеры только нескольких типов. Токены носителя, часто используемые tooprotect конечных точек. Токены носителя — тип hello наиболее широко выданного маркера в OAuth 2.0. Многие реализации OAuth 2.0 предполагают, что токены носителя являются единственным типом маркера, выданного hello.
> 
> 

1.  В командной строке измените каталог hello слишком**azuread**.

    `cd azuread`

2.  Установка hello Passport.js `passport-azure-ad` модуля:

    `npm install passport-azure-ad`

    Hello выходные данные команды hello должен выглядеть следующим образом:

    ```
    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a>7: Добавление MongoDB модули tooyour веб-API
В этом примере мы используем MongoDB в качестве хранилища данных. 

1.  Установить Mongoose, широко используемый подключаемый модуль, toomanage моделей и схем: 

    `npm install mongoose`

2.  Установите hello драйвер базы данных MongoDB, которая также называется MongoDB.

    `npm install mongodb`

## <a name="8-install-additional-modules"></a>Шаг 8. Установка дополнительных модулей
Установите hello оставшихся необходимые модули.

1.  В командной строке измените каталог hello слишком**azuread**:

    `cd azuread`

2.  Введите следующие команды hello. Hello команды устанавливают следующие модули в папке node_modules hello:

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a>Шаг 9. Создание файла Server.js для зависимостей
Файл Server.js содержит hello большую часть функций hello API веб-сервера. Добавьте большая часть файла с кодом toothis. Для производственных целей рефакторинг функции hello разбиваются на меньшие файлы как для отдельных маршрутов и контроллеров. В этой статье мы используем Server.js.

1.  В командной строке измените каталог hello слишком**azuread**:

    `cd azuread`

2.  С помощью редактора по своему усмотрению создайте файл server.js. Добавьте следующие сведения toohello файл hello:

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  Сохраните файл hello. Скоро будет возвращать tooit.

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a>10: создать файл конфигурации toostore параметры Azure AD
Этот файл код передает hello параметры конфигурации из вашего tooPassport.js портала Azure AD. Эти значения конфигурации, созданный при добавлении API toohello hello веб-портала в начале статьи hello hello. После копирования кода hello объясняется, какие tooput hello значениями этих параметров.

1.  В командной строке измените каталог hello слишком**azuread**:

    `cd azuread`

2.  В редакторе создайте файл Config.js. Добавьте hello следующую информацию:

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a>Обязательные значения

*   **IdentityMetadata**: это место, куда `passport-azure-ad` ищет данные конфигурации для hello поставщика удостоверений (IDP) и ключи toovalidate hello hello веб-маркеры JSON (JWT). При использовании Azure AD, скорее всего, не следует toochange это.

*   **аудитория**: на URI перенаправления из портала hello.

> [!NOTE]
> Рекомендуется часто менять ключи. Убедитесь, что всегда извлекаются из URL-адреса «openid_keys» hello, и приложение hello можно открыть hello Интернета.
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a>11: добавить файл Server.js tooyour конфигурации hello
Приложению tooread hello значения из файла конфигурации hello, которую вы только что создали. Добавьте файл .config hello из требуемых ресурсов в приложении. Задать toothose hello глобальные переменные, которые находятся в Config.js.

1.  В командной строке hello изменить каталог hello слишком**azuread**:

    `cd azuread`

2.  В редакторе откройте файл Server.js. Добавьте hello следующую информацию:

    ```Javascript
    var config = require('./config');
    ```

3.  Добавьте новый tooServer.js раздела:

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>12: Добавление hello MongoDB модели и данные схемы с помощью Mongoose
Затем подключите эти три файла в службе REST API.

В этой статье мы используем MongoDB toostore нашей задачи. Этот вопрос обсуждается на *шаге 4*.

В файле Config.js hello, созданный на шаге 11, базы данных называется *tasklist*. Это было поместить в конце hello URL-адрес подключения mongoose_auth_local. Не нужно toocreate базы данных, заранее в MongoDB. Hello база данных создается на hello сначала выполнения приложения сервера (при условии, что hello базы данных еще не существует).

Hello server рассказали какие toouse базы данных MongoDB. Далее необходимо toowrite некоторые модели hello toocreate дополнительного кода и схемы для вашего сервера задач.

### <a name="hello-model"></a>модель Hello
модель схемы Hello является очень простым. При необходимости ее можно расширить. 

модель схемы Hello может принимать следующие значения:

*   **Имя**. Задача назначенного toohello Hello человека. Это **строковое** значение.
*   **Задача**. Hello имя задачи «hello». Это **строковое** значение.
*   **Дата**. Hello Дата выполнения этой задачи hello. Это значение **datetime**.
*   **Завершено**. Является ли hello задача завершена. Это **логическое** значение.

### <a name="create-hello-schema-in-hello-code"></a>Создание схемы hello в коде hello
1.  В командной строке измените каталог hello слишком**azuread**:

    `cd azuread`

2.  В редакторе откройте файл Server.js. Запись конфигурации hello добавьте hello следующую информацию:

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

Он подключает toohello MongoDB сервера. Он также возвращает объект схемы.

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a>С помощью схемы hello, создайте модели в коде hello
Hello предшествующий код добавьте hello, следующий код:

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

Как можно видеть из кода hello, сначала создать схему. Затем создайте объект модели. Используйте hello модели объекта toostore данных по всему hello кода при определении вашей **маршруты**.

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a>Шаг 13. Добавление маршрутов для сервера REST API задачи
Теперь, когда toowork модели базы данных с добавьте hello маршруты, который будет использоваться для сервера API-интерфейса REST.

### <a name="about-routes-in-restify"></a>О маршрутах в Restify
Маршруты в restify рабочих точно hello так же, как при использовании hello стека, экспресс-выпуск. Определения маршрутов с помощью hello URI, что предполагается toocall приложения hello клиента. Как правило, свои маршруты вы определяете в отдельном файле. В этом руководстве мы помещаем маршруты в файл Server.js. Для систем в рабочей среде мы рекомендуем вынести их в отдельный файл.

Типичный шаблон для маршрута Restify выглядит следующим образом:

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


Это шаблон hello на самом базовом уровне hello. Restify (и Express) предоставляет гораздо более глубокую функциональные возможности, как типы приложений toodefine возможность hello и сложные маршрутизации между разными конечными точками.

#### <a name="add-default-routes-tooyour-server"></a>Добавление сервера tooyour маршруты по умолчанию
Добавить базовый CRUD маршруты hello: **создания**, **получить**, **обновление**, и **удалить**.

1.  В командной строке измените каталог hello слишком**azuread**:

    `cd azuread`

2.  В редакторе откройте файл Server.js. Ниже записи в базе данных hello ранее сделанные, добавить hello следующую информацию:

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();
    _task.save(function(err) {
    if (err) {
    req.log.warn(err, 'createTask: unable toosave');
    next(err);
    } else {
    res.send(201, _task);
    }
    });
    return next();
    }
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable toodelete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in hello database. Add one!");
    }
    if (!owner) {
    log.warn(err, "You did not pass an owner when listing tasks.");
    } else {
    res.json(data);
    }
    });
    return next();
    }
    ```

### <a name="add-error-handling-for-hello-routes"></a>Добавьте обработку ошибок для маршрутов hello
Добавьте некоторые обработку ошибок, могут взаимодействовать задней toohello клиента о проблеме hello, которыми вы столкнулись.

Добавьте следующий код ниже кода hello, который уже написаны hello:

```Javascript
///--- Errors for communicating something more information back toohello client.
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="14-create-your-server"></a>Шаг 14. Создание сервера
Здравствуйте последнего самое toodo является tooadd свой экземпляр сервера. экземпляр сервера Hello управляет вызовов.

Restify (и Express) предлагают эффективные возможности настройки, которые можно использовать на сервере REST API. В этом учебнике мы используем hello наиболее базовой установки.

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a>15: добавить маршруты hello (без проверки подлинности, сейчас)
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a>16: запускать сервер hello
Это tootest рекомендуется перед добавлением проверки подлинности сервера.

Самый простой способ tootest Hello сервера — с помощью перелистывание в командной строке. toodo, требуется простой программы, можно использовать tooparse результаты как JSON. 

1.  Установите средство JSON hello, мы используем hello следующие примеры:

    `$npm install -g jsontool`

    При этом устанавливаются средства JSON hello глобально.

2.  Убедитесь, что ваш экземпляр MongoDB работает.

    `$sudo mongod`

3.  Измените каталог hello слишком**azuread**, а затем запустите перелистывание:

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  tooadd задачи:

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    Hello ответа должно быть:

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  Перечисление задач для Brandon:

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Если все эти команды выполняются без ошибок, не требуется сервер готов tooadd OAuth toohello REST API.

*Теперь у вас есть сервер REST API с MongoDB!*

## <a name="17-add-authentication-tooyour-rest-api-server"></a>17: Добавление сервера API-интерфейса REST tooyour проверки подлинности
Теперь, когда выполнение API REST, он настраивается toouse его с Azure AD.

В командной строке измените каталог hello слишком**azuread**:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a>Использовать oidcbearerstrategy hello, предоставляемую с passport azure ad
На данный момент вы создали стандартный сервер REST TODO без какой-либо авторизации. Теперь добавьте проверку подлинности.

Во-первых требуется укажите toouse Passport. Сделайте это сразу после конфигурации сервера.

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> При написании API-интерфейсы, это toosomething данных отличается от маркера hello, hello пользователя подменить приветствия ссылку tooalways рекомендуется. Когда этот сервер сохраняет элементы TODO, она сохраняет их на основе идентификатора подписки пользователя hello в маркере hello (называемые через token.sub). В поле «владелец» hello, поместите hello token.sub. Это гарантирует доступность TODOs hello пользователя только данный пользователь. Никто не может получить доступ к TODOs hello, которые были введены. Нет отсутствие проблем в hello API для «владелец». Внешний пользователь может запросить элементы списка дел (TODO) других пользователей, даже если они прошли проверку подлинности.
> 
> 

Затем с помощью стратегии носителя подключения откройте Идентификатором hello, входящий в состав `passport-azure-ad`. Вставьте это после добавленного ранее:

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

Для Passport свойственно аналогичное поведение для всех стратегий (Twitter, Facebook и т. д.). Все записи стратегии придерживаться toohello шаблон. Передайте hello стратегии `function()` , использует токен и `done` в качестве параметров. Стратегия Hello возвращается после его свою работу. Пользователь hello хранилища и образа hello маркер tooask для него требуется еще раз.

> [!IMPORTANT]
> Hello выше код принимает любой пользователь, который может проверить подлинность сервера tooyour. Это называется автоматической регистрацией. На рабочем сервере не стоит toolet любой пользователь без необходимости их пройти процесс регистрации, выборе. Обычно это является шаблон hello в потребительские приложения. приложение Hello может разрешить tooregister с Facebook, но затем вас просят tooenter дополнительных сведений. Если с помощью программы командной строки не были в этом учебнике, можно извлечь из hello объекта маркера, который возвращается hello электронной почты. Затем задайте себе вопрос: hello пользователя tooenter Дополнительные сведения. Так как на тестовом сервере, можно добавить пользователя hello непосредственно toohello в памяти базы данных.
> 
> 

### <a name="protect-endpoints"></a>Защита конечных точек
Защита конечных точек, указав hello **passport.authenticate()** вызов с протоколом hello, которые должны toouse.

Вы можете изменить маршрут в коде сервера для более продвинутого использования:

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a>Шаг 18. Повторный запуск серверного приложения
Используйте curl снова toosee при наличии защиты OAuth 2.0 для конечных точек. Сделайте это до запуска любого клиентского пакета SDK для этой конечной точки. заголовки Hello вернул должен сообщить, правильно ли работает проверки подлинности.

1.  Убедитесь, что ваш экземпляр MongoDB работает.

    `$sudo mongod`

2.  Изменить toohello **azuread** каталога, а затем используйте curl:

    `$ cd azuread`

    `$ node server.js`

3.  Попробуйте выполнить базовую команду POST:

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

Ответ 401 указывает уровень Passport hello пытается tooredirect toohello конечную точку авторизации, что именно вы хотите.

*Теперь у вас есть служба REST API, использующая OAuth 2.0!*

Вы уже сделали с этим сервером все, что можно реализовать без использования клиента, совместимого с OAuth 2.0. Для этого потребуется tooreview дополнительных учебника.

## <a name="next-steps"></a>Дальнейшие действия
Справочник по образец hello завершена (без настройки) предоставляется как [ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip). Кроме того, его можно клонировать из GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

Теперь можно переместить на toomore дополнительные разделы. Может потребоваться tootry [защитить веб-приложение Node.js с помощью конечной точки v2.0 hello](active-directory-v2-devquickstarts-node-web.md).

Ниже приведены некоторые дополнительные ресурсы.

* [Вход для пользователей учетных записей Майкрософт и Azure AD в одном приложении](active-directory-appmodel-v2-overview.md)
* [Тег StackOverflow "azure-active-directory"](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Получение обновлений системы безопасности для наших продуктов
Мы рекомендуем toosign копирование toobe уведомлений при внесении угрозы безопасности. На hello [выпуске](https://technet.microsoft.com/security/dd252948) страницы, подписаться на оповещения tooSecurity рекомендации.

