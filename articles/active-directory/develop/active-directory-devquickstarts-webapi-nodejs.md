---
title: "Приступая к работе AD Node.js aaaAzure | Документы Microsoft"
description: "Как toobuild веб-API Node.js REST, интегрируется с Azure AD для проверки подлинности."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a>Начало работы с веб-API для Node.js
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

*Passport* — промежуточный слой проверки подлинности для Node.js. Гибкая и модульной Passport плавно могут удаляться в tooany срочные или Restify веб-приложения. Он также позволяет использовать разные стратегии с поддержкой аутентификации на основе имени пользователя и пароля, учетных записей Facebook, Twitter и пр. Мы разработали стратегию для Microsoft Azure Active Directory (Azure AD). Мы установить этот модуль, а затем добавьте hello Microsoft Azure Active Directory `passport-azure-ad` подключаемого модуля.

toodo это, необходимо:

1. зарегистрировать приложение в Azure AD;
2. Настройка вашего приложения toouse Passport `passport-azure-ad` подключаемого модуля.
3. Настройка клиентского приложения toocall hello tooDo список веб-API.

поддерживается Hello кода для этого учебника [на GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).

> [!NOTE]
> Данная статья не охватывает как tooimplement вход, регистрация, или профиль управления с помощью Azure AD B2C. Этот раздел посвящен вызовах веб-API после hello пользователь уже прошел проверку подлинности.  Мы рекомендуем начать с [как toointegrate с Azure Active Directory документа](active-directory-how-to-integrate.md) toolearn об основах hello из Azure Active Directory.
>
>

Мы выпустили все hello исходного кода в этом примере выполнение в GitHub в рамках лицензии MIT, и вы можете бесплатно tooclone (или даже лучше вилки) и предоставления отзывов и запросов по запросу.

## <a name="about-nodejs-modules"></a>Информация о модулях Node.js
В этом пошаговом руководстве мы используем модули Node.js. Модули — это загружаемые пакеты JavaScript, предоставляющие вашему приложению определенные функциональные возможности. Обычно установите модули, используя hello Node.js NPM средство командной строки в каталоге установки NPM hello. Тем не менее некоторые модули, такие как HTTP-модуль hello, будут включены в пакет Node.js core hello.

Установленные модули сохраняются в hello **node_modules** каталог в корневой каталог установки Node.js hello. В каждом модуле hello **node_modules** directory поддерживает собственный **node_modules** каталог, содержащий каких-либо модулей, от которых он зависит. Кроме того, отдельный каталог **node_modules** создается для каждого требуемого модуля. Эта структура каталогов рекурсивные представляет цепочку зависимостей hello.

Эта структура цепочки зависимостей занимает много дискового пространства. Однако она также гарантирует, что соблюдены все зависимости, и этой версии hello hello модули, используемые в разработке также используется в рабочей среде. Это делает более предсказуемое поведение приложения hello производства и предотвращает проблемы управления версиями, которые могут повлиять на пользователей.

## <a name="step-1-register-an-azure-ad-tenant"></a>Шаг 1. Регистрация клиента Azure AD
toouse это образец, необходимо, чтобы клиент Azure Active Directory. Если вы точно не знаете, какой клиент — или tooget, в статье [как tooget в Azure AD для клиента](active-directory-howto-tenant.md).

## <a name="step-2-create-an-application"></a>Этап 2. Создание приложения
Далее нужно создать приложение в каталоге, что Azure AD предоставляет сведения, необходимые toosecurely взаимодействовать с приложением.  Hello клиентского приложения и веб-API представлены одним **идентификатор приложения** таким образом, так как они включают в себя один логический приложения.  toocreate приложения, выполните [эти инструкции](active-directory-how-applications-are-added.md). Если вы создаете бизнес-приложение, возможно, [вам будут полезны эти дополнительные инструкции](../active-directory-applications-guiding-developers-for-lob-applications.md).

toocreate приложения:

1. Войдите в toohello [портал Azure](https://portal.azure.com).

2. Hello в верхнем меню выберите свою учетную запись. После этого в разделе hello **каталога** выберите hello клиента Active Directory, где требуется tooregister приложения.

3. Выберите в меню hello слева hello, **более служб**, а затем выберите **Azure Active Directory**.

4. Щелкните **Регистрация приложений**, а затем выберите **Добавить**.

5. Выполните запросы toocreate hello **веб-приложение или WebAPI**.

      * Hello **имя** из hello приложения описывает tooend пользователей приложения.

      * Hello **URL-адрес входа** hello базовый URL-адрес приложения.  Здравствуйте, по умолчанию используется URL-адрес образца кода hello `https://localhost:8080`.

6. Когда вы закончите регистрацию, Azure AD назначит приложению уникальный идентификатор. Это значение требуется в следующих разделах hello, поэтому скопируйте его со страницы приложения hello.

7. Из hello **параметры** -> **свойства** страницы приложения, обновите URI идентификатора приложения hello. Hello **URI идентификатора приложения** — это уникальный идентификатор для вашего приложения. соглашение о Hello — toouse `https://<tenant-domain>/<app-name>`, например: `https://contoso.onmicrosoft.com/my-first-aad-app`.

8. Создание **ключ** для вашего приложения hello **параметры** страницы и скопируйте его в любом месте. Скоро он вам понадобится.

## <a name="step-3-download-nodejs-for-your-platform"></a>Шаг 3. Скачивание Node.js для своей платформы
toosuccessfully использование этого образца, необходимо иметь состоящая из Node.js.

Установите Node.js с сайта [http://nodejs.org](http://nodejs.org).

## <a name="step-4-install-mongodb-on-your-platform"></a>Шаг 4. Установка MongoDB на вашей платформе
toosuccessfully использование этого образца, необходимо иметь состоящая из MongoDB. Используйте hello toomake MongoDB постоянные API-интерфейса REST по экземплярам сервера.

Установите MongoDB с сайта [http://mongodb.org](http://www.mongodb.org).

> [!NOTE]
> В этом пошаговом руководстве предполагается использовать конечные точки установки и сервером по умолчанию hello для MongoDB, что на момент написания этой статьи hello является mongodb://localhost.
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a>Шаг 5: Установка модулей Restify hello в веб-API
Мы используем Restify toobuild нашем API REST. Restify — это минималистичная и гибкая платформа для приложений Node.j, созданная на основе Express. Она располагает широким набором функций, позволяющих реализовать интерфейсы REST API поверх Connect.

### <a name="install-restify"></a>Установка Restify
1. Из командной строки hello, измените каталоги toohello **azuread** каталога. Если hello **azuread** каталог не существует, создайте его.

        `cd azuread - or- mkdir azuread; cd azuread`

2. Введите следующую команду hello:

    `npm install restify`

    Эта команда устанавливает Restify.

#### <a name="did-you-get-an-error"></a>Вы получили сообщение об ошибке?
В некоторых операционных системах при использовании параметра NPM может появиться такое сообщение об ошибке (**Error: EPERM, chmod '/usr/local/bin/..'**). и предложения, попробуйте выполнить выполняющейся hello учетной записи с правами администратора. В этом случае используйте toorun команда hello sudo NPM с более высоким уровнем привилегий.

#### <a name="did-you-get-an-error-regarding-dtrace"></a>Вы получили сообщение об ошибке, которая относится к DTRACE?
При установке Restify может появиться примерно следующее сообщение об ошибке:

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
Restify предоставляет мощный механизм для трассировки вызовов REST с помощью DTrace. Но во многих операционных системах DTrace отсутствует. Эти ошибки можно игнорировать.

Hello выходные данные этой команды должен выглядеть примерно toohello следующие выходные данные:

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


## <a name="step-6-install-passportjs-in-your-web-api"></a>Шаг 6. Установка Passport.js для веб-интерфейса API
[Passport](http://passportjs.org/) — промежуточный слой проверки подлинности для Node.js. Гибкая и модульной Passport плавно могут удаляться в tooany срочные или Restify веб-приложения. Он также позволяет использовать разные стратегии с поддержкой аутентификации на основе имени пользователя и пароля, учетных записей Facebook, Twitter и пр.

Мы разработали стратегию для Azure Active Directory. Мы установить этот модуль, а затем добавьте подключаемого модуля стратегии hello Azure Active Directory.

1. Из командной строки hello, измените каталоги toohello **azuread** каталога.

2. tooinstall passport.js введите hello следующую команду:

    `npm install passport`

    Hello выходные данные команды hello должен выглядеть примерно toohello следующее:

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a>Шаг 7: Добавление веб-API tooyour Passport Azure AD
Далее добавим стратегии hello OAuth с помощью `passport-azure-ad`, набор стратегии, которые подключаются tooPassport Azure Active Directory. В этом примере REST API мы будем использовать эту стратегию для токенов носителя.

> [!NOTE]
> Платформа OAuth2 позволяет выдавать маркеры любого известного типа, но в большинстве случаев используются маркеры только нескольких типов. Токены носителя являются маркерами hello чаще всего используется для защиты конечных точек. Они имеют тип hello наиболее широко выданного маркера в OAuth2. Многие предполагают, что токены носителя являются единственным типом токены, выданные hello.
>
>

Из командной строки hello, измените каталоги toohello **azuread** каталога.

Тип hello следующая команда tooinstall hello Passport.js `passport-azure-ad module`:

`npm install passport-azure-ad`

Hello выходные данные команды hello должен выглядеть примерно toohello следующие выходные данные:


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a>Шаг 8: Добавление MongoDB модули tooyour веб-API
Мы используем MongoDB в качестве хранилища данных. По этой причине мы должны tooinstall hello широко используется подключаемый модуль вызываемой модели toomanage Mongoose и схемы. Также нужно tooinstall hello базы данных драйверов для MongoDB (который также называется MongoDB).

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a>Шаг 9. Установка дополнительных модулей
Далее приведены инструкции по установке hello оставшихся необходимые модули.

1. Из командной строки hello, измените каталоги toohello **azuread** папку, если вы не являетесь уже существует.

    `cd azuread`

2. Введите следующие команды tooinstall hello эти модули в вашей **node_modules** каталога:

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a>Шаг 10. Создание server.js с зависимостями
Hello server.js обеспечивает большую часть функций hello API веб-сервере. Мы добавляем большая часть наших toothis файл кода. В рабочей среде рекомендуется выполнить рефакторинг функции hello на меньшие файлы, такие как отдельные маршруты и контроллеров. В этом демонстрационном примере мы включим все эти механизмы в файл server.js.

1. Из командной строки hello, измените каталоги toohello **azuread** папку, если вы не являетесь уже существует.

    `cd azuread`

2. Создание `server.js` файл в любом редакторе, а затем добавьте hello следующую информацию:

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. Сохраните файл hello. Мы вернемся вскоре tooit.

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a>Шаг 11: Создание файла конфигурации toostore настройки Azure AD
Этот файл код передает hello параметры конфигурации из вашего tooPassport.js портала Azure Active Directory. Эти значения конфигурации, созданный при добавлении API toohello hello веб-портала в первой части пошагового руководства hello hello. После копирования кода hello рассказывается какие tooput hello значениями этих параметров.

1. Из командной строки hello, измените каталоги toohello **azuread** папку, если вы не являетесь уже существует.

    `cd azuread`

2. Создание `config.js` файл в любом редакторе, а затем добавьте hello следующую информацию:

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. Сохраните файл hello.

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a>Шаг 12: Добавление значений tooyour server.js файла конфигурации
Мы должны tooread эти значения из hello config-файл, созданный для нашего приложения. toodo это, мы добавляем hello config-файл как необходимый ресурс в приложении. Мы Установка hello глобальные переменные toomatch hello переменных в документе config.js hello.

1. Из командной строки hello, измените каталоги toohello **azuread** папку, если вы не являетесь уже существует.

    `cd azuread`

2. Откройте ваш `server.js` файл в любом редакторе, а затем добавьте hello следующую информацию:

    ```Javascript
    var config = require('./config');
    ```
3. Затем добавьте новый раздел слишком`server.js` с hello, следующий код:

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. Сохраните файл hello.

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Шаг 13: Добавление hello MongoDB модели и данные схемы с помощью Mongoose
Теперь эта Подготовка будет toostart оплата, как мы объединять эти три файла в службу REST API.

В данном пошаговом руководстве мы используем MongoDB toostore нашей задачи, как описано в шаге 4.

В hello `config.js` файла, созданного на шаге 11, мы позвонили базе данных `tasklist`, так как это было поместить в конце hello нашей **mogoose_auth_local** URL-адрес подключения. Не нужно toocreate базы данных, заранее в MongoDB. Вместо этого MongoDB это за нас на hello сначала создает выполнения приложения сервера (при условии, что hello базы данных еще не существует).

Теперь, когда мы рассказали hello сервера базы данных MongoDB, который мы хотели бы toouse, то необходимо toowrite некоторые модели hello toocreate дополнительного кода и схемы для наших сервера задач.

### <a name="discussion-of-hello-model"></a>Обсуждение модели hello
Мы используем очень простую модель схемы. Вы можете дополнить ее в соответствии с потребностями.

Имя: имя hello hello, кто назначается toohello задачи. Тип **Строка**.

ЗАДАЧИ: hello саму задачу. Тип **Строка**.

Дата: hello Дата задачи hello оплаты. Тип **Дата и время**.

ЗАВЕРШЕНО: Если задачу «hello» была завершена или нет. Тип **Логическое значение**.

### <a name="creating-hello-schema-in-hello-code"></a>Создание схемы hello в коде hello
1. Из командной строки hello, измените каталоги toohello **azuread** папку, если вы не являетесь уже существует.

    `cd azuread`

2. Откройте ваш `server.js` файл в любом редакторе, а затем добавьте следующую информацию ниже запись конфигурации hello hello:

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
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
Как видно из кода hello нашей схемы сначала создается. Затем мы создадим объекта модели, мы используем наши данные во всей hello кода при определении toostore наших **маршруты**.

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a>Шаг 14. Добавление маршрутов для сервера задач REST API
Теперь, когда у нас есть toowork модели базы данных с, добавим hello маршруты, мы применяемые постоянной серверов REST API.

### <a name="about-routes-in-restify"></a>О маршрутах в Restify
Маршруты незавершенное Restify hello таким же образом, они в hello Express стека. Определения маршрутов с помощью hello URI, что предполагается toocall приложения hello клиента. Как правило, свои маршруты вы определяете в отдельном файле. Для наших целей мы поместили нашей маршруты в файле server.js hello. Для систем в рабочей среде мы рекомендуем вынести их в отдельный файл.

Типичный шаблон Restify для маршрута выглядит следующим образом:

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


Это шаблон hello на самом базовом уровне. В Restify (как и в Express) доступны очень мощные функциональные возможности, например для определения типов приложений и выполнения сложной маршрутизации между несколькими конечными точками. В нашем примере мы используем самые простые маршруты.

### <a name="add-default-routes-tooour-server"></a>Добавление сервера tooour маршруты по умолчанию
Теперь мы добавить hello основные маршруты CRUD для создания, извлечения, обновления и удаления.

1. Из командной строки hello, измените каталоги toohello **azuread** папку, если вы еще не существует:

    `cd azuread`

2. Откройте hello `server.js` файл в любом редакторе, а затем добавьте следующую информацию ниже hello предыдущей базы данных записи, сделанные hello:

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a>Добавление обработки ошибок в интерфейсы API
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a>Шаг 15. Создание сервера
Мы уже определили базу данных и создали все маршруты. последний самое toodo Hello добавить hello экземпляр сервера, который управляет наши вызовы.

В Restify (и Express) можно выполнять множество настройки для сервера REST API, а снова будет самый простой установки hello toouse для наших целей.

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a>Шаг 16: Добавьте сервер toohello маршруты hello (без проверки подлинности, сейчас)
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a>Шаг 17: Запуск сервера hello (перед добавлением поддержка OAuth)
Прежде чем добавить аутентификацию, давайте протестируем сервер.

наиболее простым способом tootest Hello сервера — с помощью перелистывание в командной строке. Перед этим мы должны служебную программу, которая позволяет нам tooparse выходные данные в формате JSON.

1. Установите hello следующие средства JSON (это средство используется всех hello следующие примеры):

    `$npm install -g jsontool`

    При этом устанавливаются средства JSON hello глобально. Теперь, когда мы выполнена, давайте воспроизведения с сервером hello:

2. Сначала убедитесь, что запущен экземпляр MongoDB:

    `$sudo mongod`

3. Затем измените toohello каталог и запустите изгиб:

    `$ cd azuread` `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. Затем можно добавить задачу следующим образом:

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

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
    Для перечисления задач для Brandon можно использовать следующий способ:

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Если все это работает, мы готовы tooadd OAuth toohello REST API сервера.

У вас уже есть сервер REST API с MongoDB!

## <a name="step-18-add-authentication-tooour-rest-api-server"></a>Шаг 18: Добавление сервера API-интерфейса REST tooour проверки подлинности
Теперь, когда у нас запущен сервер REST API, мы можем использовать его для работы с Azure AD.

Из командной строки hello, измените каталоги toohello **azuread** папку, если вы не являетесь уже существует.

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Использовать hello OIDCBearerStrategy, который входит в состав passport azure ad
Мы создали стандартный сервер REST TODO без какой-либо авторизации. Самое время добавить такую функцию.

1. Во-первых мы должны tooindicate, что мы хотим toouse Passport. Сделайте это сразу после конфигурации другого сервера:

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > При написании API, рекомендуется связывать уникальный из токена hello, hello пользователя toosomething данных hello подменить. Когда этот сервер сохраняет элементы TODO, она сохраняет их на основе кода hello объекта пользователя hello в маркере hello (называемые через token.oid), который мы поместили в поле «владелец» hello. Благодаря этому только владелец сможет получить доступ к своим элементам списка дел. Нет отсутствие проблем в hello API «владелец», поэтому внешний пользователь может запросить hello TODOs других пользователей, даже если они проходят проверку подлинности.                    

2. Далее используем стратегии носителя hello, входящий в состав `passport-azure-ad`. Посмотрите на код hello сейчас и hello rest будут описаны чуть ниже. Вставьте этот текст после добавленного ранее:

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

Для Passport свойственно аналогичное поведение для всех стратегий (Twitter, Facebook и т. д.); это поведение учитывают все разработчики модулей стратегий. Просматривая стратегии hello, видно, что мы передаем функции, которая содержит маркер и выполняются как параметры hello. Стратегия Hello поставляется обратно toous после он выполняет свою работу. Да, мы храните hello пользователя и маркер hello образа, нам не нужно tooask его еще раз.

> [!IMPORTANT]
> Предыдущий код Hello принимает любой пользователь, который происходит tooauthenticate tooour сервера. Это называется автоматической регистрацией. На рабочих серверах мы не рекомендуем разрешать вход без прохождения определенного процесса регистрации, который вы сочтете приемлемым. Обычно это является шаблон hello в потребительские приложения, которые позволяет tooregister с Facebook, а затем попросите toofill дополнительных сведений. Если это не было программы командной строки, мы удалось извлекли hello электронной почты из hello токен объекта, который возвращается и затем предложено hello toofill пользователя дополнительных сведений. Так как на тестовом сервере, мы просто добавьте toohello базы данных в памяти.
>
>

### <a name="protect-some-endpoints"></a>Защита некоторых конечных точек
Защита конечных точек, указав hello `passport.authenticate()` вызов с протоколом hello, которые должны toouse.

toomake наш код сервера сделать что-нибудь интереснее, изменим hello маршрута.

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a>Шаг 19. Снова запустите свой сервер приложения и убедитесь, что он вас отклоняет.
Воспользуемся `curl` снова toosee Если теперь у нас есть OAuth2 защиты на основе наших конечных точек. Этот тест мы выполним до того, как запускать клиентские пакеты SDK для этой конечной точки. Hello заголовки, которые возвращаются должно быть достаточно tootell нам, если мы будем вниз hello правильный путь.

1. Сначала убедитесь, что запущен экземпляр MongoDB:

    `$sudo mongod`

2. Затем измените toohello каталог и запустите изгиб.

      `$ cd azuread` `$ node server.js`

3. Попробуйте выполнить простую команду POST.

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

401 — ответ hello, которую вы ищете здесь. Этот ответ означает, что этот слой Passport hello пытается tooredirect toohello прав конечной точки, что именно вы хотите.

## <a name="next-steps"></a>Дальнейшие действия
Мы уже сделали с этим сервером все, что можно реализовать без использования клиента OAuth2. Вам потребуется toogo через дополнительные пошагового руководства.

Вы узнали как tooimplement API REST с помощью Restify и OAuth2. Также имеется более чем достаточно tookeep кода при разработке службы, а также знание как toobuild по этому примеру.

Если вы заинтересованы в следующие шаги hello в поездке ADAL, ниже приведены некоторые поддерживаемые клиенты ADAL, мы рекомендуем, чтобы продолжить работу с.

Клонировать работу машины tooyour разработчика и настроить, как описано в пошаговом руководстве hello.

[ADAL для iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[ADAL для Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
