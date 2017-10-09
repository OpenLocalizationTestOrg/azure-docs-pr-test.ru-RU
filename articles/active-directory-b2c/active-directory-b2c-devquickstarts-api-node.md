---
title: "Azure AD B2C: защита веб-API с помощью Node.js | Документация Майкрософт"
description: "Как toobuild Node.js веб-API, принимающий токены из клиента B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a>Azure AD B2C: защита веб-API с помощью Node.js
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

С помощью Azure Active Directory (Azure AD) B2C можно защитить веб-API с помощью маркера доступа OAuth 2.0. Эти маркеры позволяют клиентских приложений, использующих Azure AD B2C tooauthenticate toohello API. В этой статье показано, как toocreate API «список дел», которая позволяет пользователям tooadd и список задач. веб-API Hello защищается с помощью Azure AD B2C и позволяет toomanage прошедшим проверку пользователям только их список дел.

> [!NOTE]
> Этот образец был написан toobe подключены с помощью tooby наших [iOS B2C образец приложения](active-directory-b2c-devquickstarts-ios.md). Сначала hello текущего руководство по применению, а затем следуйте вместе с этого образца.
>
>

**Passport** — промежуточный слой проверки подлинности для Node.js. Гибкая модульная структура Passport позволяет незаметно устанавливать его в любом приложении на основе Express или в веб-приложении Restify. Полный набор стратегий поддерживает проверку подлинности с помощью имени пользователя и пароля, Facebook, Twitter и других средств. Мы разработали стратегию для Azure Active Directory (Azure AD). Установите этот модуль и добавьте hello Azure AD `passport-azure-ad` подключаемого модуля.

toodo этот образец, необходимо:

1. зарегистрировать приложение в Azure AD;
2. Настройка вашего приложения toouse Passport `azure-ad-passport` подключаемого модуля.
3. Настройка клиентского приложения toocall hello «список дел» веб-API.

## <a name="get-an-azure-ad-b2c-directory"></a>Создание каталога Azure AD B2C
Перед использованием Azure AD B2C необходимо создать каталог или клиент.  Каталог — это контейнер для всех пользователей, приложений, групп и т. д.  Если каталог B2C еще не создан, [создайте его](active-directory-b2c-get-started.md), прежде чем продолжить.

## <a name="create-an-application"></a>Создание приложения
Далее необходимо toocreate приложения в каталоге B2C, которое предоставляет некоторые сведения, необходимые toosecurely Azure AD взаимодействовать с приложением. В этом случае клиентское приложение hello и веб-API представлены одним **идентификатор приложения**, так как они включают в себя один логический приложения. toocreate приложения, выполните [эти инструкции](active-directory-b2c-app-registration.md). Не забудьте сделать следующее.

* Включить **веб-приложения и веб-api** в приложение hello
* Введите `http://localhost/TodoListService` в качестве значения **URL-адреса ответа**. Это URL-адрес по умолчанию hello для этого примера кода.
* Создайте для своего приложения **секрет приложения** и скопируйте его. Эти данные понадобятся позже. Обратите внимание, что это значение должно toobe [XML переключения](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) перед его использованием.
* Копировать hello **идентификатор приложения** , назначенный tooyour приложения. Эти данные понадобятся позже.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Создание политик
В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md). Это приложение содержит два действия с удостоверениями: регистрация и вход. Требуется одна политика toocreate каждого типа, как описано в [статье политики](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).  При создании трех политик обязательно выполните указанные ниже действия.

* Выберите hello **отображаемое имя** и другие атрибуты регистрации в политике организации доступа к Интернету.
* Выберите hello **отображаемое имя** и **идентификатор объекта** утверждений приложения в каждой политике.  Можно также выбрать другие утверждения.
* Копировать вниз hello **имя** каждой политики, после его создания. Он должен иметь префикс hello `b2c_1_`.  Имена политик понадобятся вам позже.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

После создания трех политик вы будете готовы toobuild приложения.

toolearn о том, как работают политики в Azure AD B2C, начинаться с hello [.NET web app начало учебника](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="download-hello-code"></a>Загрузка кода hello
Здравствуйте, код для этого учебника [сохраняется на сайте GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS). Образец hello toobuild как можно перейти, вы можете [загрузить каркас проект как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip). Также можно клонировать основу hello:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

также является приложение Hello завершения [доступны как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) или на hello `complete` ветви hello одного репозитория.

## <a name="download-nodejs-for-your-platform"></a>Загрузка Node.js для платформы
в этом примере использовать toosuccessfully, состоящая из Node.js.

Установите Node.js с сайта [nodejs.org](http://nodejs.org).

## <a name="install-mongodb-for-your-platform"></a>Установка MongoDB на платформе
в этом примере использовать toosuccessfully, состоящая из MongoDB. Мы используем MongoDB toomake постоянного REST API по экземплярам сервера.

Установите MongoDB с сайта [mongodb.org](http://www.mongodb.org).

> [!NOTE]
> Это пошаговое руководство предполагает, что можно использовать конечные точки установки и сервером по умолчанию hello для MongoDB, являющийся на момент написания этой статьи hello `mongodb://localhost`.
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a>Установка модулей Restify hello в веб-API
Мы используем Restify toobuild API-интерфейса REST. Restify — это минимальная гибкая платформа приложений Node.j, производная от Express. Она располагает широким набором функций, позволяющих реализовать интерфейсы REST API поверх Connect.

### <a name="install-restify"></a>Установка Restify
Из командной строки hello, измените каталог слишком`azuread`. Если hello `azuread` каталог не существует, создайте его.

`cd azuread` или `mkdir azuread;`

Введите следующую команду hello:

`npm install restify`

Эта команда устанавливает Restify.

#### <a name="did-you-get-an-error"></a>Вы получили сообщение об ошибке?
В некоторых операционных системах при использовании `npm`, появляется сообщение об ошибке hello `Error: EPERM, chmod '/usr/local/bin/..'` и запроса на выполнение hello учетной записи с правами администратора. При возникновении этой проблемы, используйте hello `sudo` toorun команда `npm` на более высоком уровне привилегий.

#### <a name="did-you-get-a-dtrace-error"></a>Вы получили сообщение об ошибке DTrace?
При установке Restify вы можете увидеть что-то подобное:

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
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

Restify предоставляет мощный механизм для трассировки вызовов REST с помощью DTrace. Однако во многих операционных системах DTrace отсутствует. Эти ошибки можно игнорировать.

аналогичный текст toothis должны быть выведены Hello hello команды:

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
    └── bunyan@0.22.0 (mv@0.0.5)

## <a name="install-passport-in-your-web-api"></a>Установка Passport в веб-API
Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует.

Установите службы Passport, с помощью hello следующую команду:

`npm install passport`

Hello выходные данные команды hello должно быть аналогичный текст toothis:

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a>Добавить веб-API tooyour passport azuread
Добавьте стратегии hello OAuth с помощью `passport-azuread`, набор стратегии, которые подключения Azure AD с Passport. Используйте эту стратегию для маркеров носителя в образце hello REST API.

> [!NOTE]
> Несмотря на то что OAuth2 предоставляет платформу, на которой может быть выдан токен любого известного типа, широкое распространение получили токены только некоторых типов. Hello маркеры для защиты конечных точек являются маркерами носителя. Эти типы маркеров являются наиболее широко выданных OAuth2 hello. Многие предполагают, что токены носителя являются единственным типом маркера, выданного hello.
>
>

Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует.

Установка hello Passport `passport-azure-ad` модуля с помощью hello следующую команду:

`npm install passport-azure-ad`

Hello выходные данные команды hello должно быть аналогичный текст toothis:

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a>Добавить MongoDB модули tooyour веб-API
В этом примере для хранения данных используется MongoDB. Для этого нужно установить Mongoose, широко используемый подключаемый модуль для управления моделями и схемами.

* `npm install mongoose`

## <a name="install-additional-modules"></a>Установка дополнительных модулей
После этого установите hello оставшихся необходимые модули.

Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:

`cd azuread`

Установка модулей hello в вашей `node_modules` каталога:

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a>Создание файла server.js с зависимостями
Hello `server.js` файл обеспечивает hello большую часть функций hello для сервера веб-API.

Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:

`cd azuread`

Создайте в текстовом редакторе файл `server.js` . Добавьте hello следующую информацию:

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

Сохраните файл hello. Возвращает tooit позже.

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a>Создать файл config.js toostore параметры Azure AD
Этот файл код передает hello параметры конфигурации из вашего toohello портала Azure AD `Passport.js` файла. Эти значения конфигурации, созданный при добавлении API toohello hello веб-портала в первой части hello hello руководство по применению. После копирования кода hello рассказывается какие tooput hello значениями этих параметров.

Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:

`cd azuread`

Создайте в текстовом редакторе файл `config.js` . Добавьте hello следующую информацию:

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a>Обязательные значения
`clientID`: hello идентификатор клиента приложения веб-API.

`IdentityMetadata`: Это место, куда `passport-azure-ad` ищет данные конфигурации для поставщика удостоверений hello. Он также ищет веб-маркеры JSON hello hello ключи toovalidate.

`audience`: hello универсальный код ресурса (URI) с портала hello, определяющий вызывающего приложения.

`tenantName`: имя клиента (например, **contoso.onmicrosoft.com**).

`policyName`: hello политики, которую toovalidate токены hello, поступающие в tooyour server. Этот параметр должен быть hello же политики, используемого в клиентское приложение hello для входа в систему.

> [!NOTE]
> Пока же hello использование политик для установки клиента и сервера. Если вы уже выполнили Пошаговое руководство и создали эти политики, не требуется toodo и опять же. Поскольку вы выполнили Пошаговое руководство hello, не следует должны tooset копирование новых политик для клиентских приложений на сайте hello.
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a>Добавьте файл server.js tooyour конфигурации
значения hello tooread из hello `config.js` файл был создан, добавить hello `.config` файл как необходимый ресурс в приложении, а затем задайте toothose hello глобальные переменные в hello `config.js` документа.

Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:

`cd azuread`

Откройте hello `server.js` файл в редакторе. Добавьте hello следующую информацию:

```Javascript
var config = require('./config');
```
Добавить новый раздел слишком`server.js` , включающего hello, следующий код:

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

Далее добавим некоторые заполнители для пользователей hello, мы получаем от вызывающего приложения.

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

Также создадим средство ведения журнала.

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Добавить hello MongoDB модели и данные схемы с помощью Mongoose
Hello предыдущих подготовки обеспечивает как вводить эти три файла друг с другом в службе REST API.

Для этого пошагового руководства используйте MongoDB toostore задач, как было сказано ранее.

В hello `config.js` файла, именем базы данных **tasklist**. Это имя также было поместить в конце hello hello `mongoose_auth_local` URL-адрес подключения. Не нужно toocreate базы данных, заранее в MongoDB. Hello базы данных создается автоматически при первом запуске серверное приложение hello.

После сообщить hello server какие toouse базы данных MongoDB, необходимо toowrite некоторые модели hello toocreate дополнительного кода и схемы для сервера задач.

### <a name="expand-hello-model"></a>Разверните узел модели hello
Эта модель схемы очень проста. При необходимости можно развернуть ее.

`owner`: Кто назначается toohello задачи. Значение указывается в формате **string**(строка).  

`Text`: саму задачу hello. Значение указывается в формате **string**(строка).

`date`: hello Дата выполнения этой задачи hello. Значение указывается в формате **datetime**(дата и время).

`completed`: Если hello задача завершена. Значение указывается в формате **Boolean**(логическое).

### <a name="create-hello-schema-in-hello-code"></a>Создание схемы hello в коде hello
Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:

`cd azuread`

Откройте hello `server.js` файл в редакторе. Добавьте следующую информацию ниже запись конфигурации hello hello:

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
Сначала создается схема hello и создайте объект модели, используемой toostore данных по всему hello кода при определении вашей **маршруты**.

## <a name="add-routes-for-your-rest-api-task-server"></a>Добавление маршрутов для сервера задач REST API
Теперь, когда toowork модели базы данных с помощью добавления hello маршрутов, которые можно использовать для сервера REST API.

### <a name="about-routes-in-restify"></a>О маршрутах в Restify
Маршруты работать в Restify в hello таким же способом, что они работают при использовании стека Express hello. Определения маршрутов с помощью hello URI, что предполагается toocall приложения hello клиента.

Типичный шаблон для маршрута Restify выглядит следующим образом:

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

В Restify и Express доступны более мощные функциональные возможности, например определение типов приложений и выполнение сложной маршрутизации между разными конечными точками. Для целей этого учебника hello нам усложнять эти маршруты.

#### <a name="add-default-routes-tooyour-server"></a>Добавление сервера tooyour маршруты по умолчанию
Теперь добавьте hello основные CRUD маршрутам **создания** и **списка** для наших API REST. Другие маршруты можно найти в hello `complete` ветви образца hello.

Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:

`cd azuread`

Откройте hello `server.js` файл в редакторе. Ниже записи в базе данных hello внесенные выше добавить hello следующую информацию:

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a>Добавьте обработку ошибок для маршрутов hello
Добавление обработки ошибок, чтобы вы могли взаимодействовать проблемы возникают задней toohello клиента, в результате которого оно было понятно.

Добавьте следующий код hello:

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a>Создание сервера
Теперь база данных определена, а маршруты созданы. Hello худшее вы toodo — экземпляр сервера hello tooadd, который управляет вызовов.

Restify Express предоставляют обширные возможности для настройки сервера REST API, а вариант установки основных hello.

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a>Добавление сервера toohello маршруты hello (без проверки подлинности)
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a>Добавление сервера API-интерфейса REST tooyour проверки подлинности
Теперь, когда есть работающий сервер REST API, можно подготовить его к использованию в Azure AD.

Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Использовать hello OIDCBearerStrategy, который входит в состав passport azure ad
> [!TIP]
> При написании API, следует всегда связывать уникальный из токена hello, hello пользователя toosomething данных hello подменить. Когда элементы ToDo хранятся на сервере hello, используется таким образом на основании hello **oid** пользователя hello в маркере hello (называемые через token.oid), который переходит в поле hello «владелец». Благодаря этому только владелец сможет получить доступ к своим элементам ToDo. Нет отсутствие проблем в hello API «владелец», поэтому внешний пользователь может запросить элементов ToDo других пользователей, даже если они проходят проверку подлинности.
>
>

Затем с помощью стратегии носителя hello, входящий в состав `passport-azure-ad`.

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

Passport использует hello же шаблон для всех стратегий. Вы передаете ему функцию `function()` с параметрами `token` и `done`. Стратегия Hello возвращаются tooyou после его всю свою работу. Следует хранить пользователя hello и сохранить токен hello tooask для него не требуется еще раз.

> [!IMPORTANT]
> Приведенный выше код Hello принимает любой пользователь, который происходит tooauthenticate tooyour сервера. Этот процесс называется автоматической регистрацией. В рабочей среде не позволяйте в любой API hello доступа пользователей без необходимости их пройти процесс регистрации. Этот процесс обычно является шаблон hello в пользовательские приложения, которые позволяет tooregister с помощью Facebook, а затем попросите toofill дополнительных сведений. Если эта программа не была программы командной строки, нам удалось извлекли hello электронной почты из hello токен объекта, который возвращается и затем предложено toofill пользователям Дополнительные сведения. Так как это образец мы их добавить tooan базы данных в памяти.
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a>Запустите tooverify приложения на сервере что он отклоняет вы
Можно использовать `curl` toosee при наличии защиты OAuth2 теперь для конечных точек. Hello возвращены заголовки должно быть достаточно tootell, вы используете правильный путь hello.

Убедитесь, что ваш экземпляр MongoDB работает.

    $sudo mongodb

Измените каталог toohello и выполнения hello server:

    $ cd azuread
    $ node server.js

Запустите команду `curl`

Попробуйте выполнить базовую команду POST:

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

Ошибку 401 — ответ hello, которые нужно. Указывает, откуда Passport hello пытается tooredirect toohello конечной точки для проверки подлинности.

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a>Теперь у вас есть служба REST API, использующая OAuth2
Вы завершили создание REST API с использованием Restify и OAuth. Теперь у вас есть достаточные кода, можно продолжить toodevelop службы и сборку в этом примере. До сих пор вы применяли этот сервер без использования клиента, совместимого с OAuth2. Для данного шага далее использовать дополнительные руководство по применению как нашей [подключения tooa веб-API с помощью операций ввода-вывода с B2C](active-directory-b2c-devquickstarts-ios.md) Пошаговое руководство.

## <a name="next-steps"></a>Дальнейшие действия
Теперь можно переместить toomore дополнительные разделы, такие как:

[Подключиться с помощью операций ввода-вывода с B2C tooa веб-API](active-directory-b2c-devquickstarts-ios.md)
