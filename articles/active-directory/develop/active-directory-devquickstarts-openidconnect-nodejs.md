---
title: "aaaGetting работы Azure AD входа в систему и выхода с помощью Node.js | Документы Microsoft"
description: "Узнайте, как toobuild Node.js Express MVC веб-приложение, которое интегрируется с Azure AD для входа в систему."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 81deecec-dbe2-4e75-8bc0-cf3788645f99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 26481899c74741743b947bd891b65ff24ffc43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a>Вход в веб-приложение Node.js и выход из него с помощью Azure AD
Мы выполним следующие действия с использованием Passport.

* Знак hello пользователя в приложении toohello с Azure Active Directory (Azure AD).
* Отображение сведений о пользователе hello.
* Знак hello выход пользователя из приложения hello.

Passport — это промежуточный слой аутентификации для Node.js. Гибкая и модульной Passport плавно могут удаляться в tooany срочные или restify веб-приложения. Он позволяет использовать разные стратегии с поддержкой аутентификации с помощью имени пользователя и пароля, учетных записей в Facebook и Twitter, и пр. Мы разработали стратегию для Microsoft Azure Active Directory. Мы установить этот модуль, а затем добавьте hello Microsoft Azure Active Directory `passport-azure-ad` подключаемого модуля.

toodo, hello выполните следующие шаги:

1. зарегистрировать приложение;
2. Настройка toouse вашего приложения hello `passport-azure-ad` стратегии.
3. Используйте Passport tooissue входа и запросах на выход tooAzure AD.
4. Печать данных о пользователе hello.

поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).  можно toofollow вдоль [загрузить приложение hello основу как ZIP-файл](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) или основу hello клона:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

в конце hello этот учебник также предоставляется приложения Hello завершена.

## <a name="step-1-register-an-app"></a>Шаг 1. Регистрация приложения
1. Войдите в toohello [портал Azure](https://portal.azure.com).

2. В меню hello hello верхней части страницы приветствия выберите свою учетную запись. В разделе hello **каталога** выберите hello клиента Active Directory, где требуется tooregister приложения.

3. Выберите **более служб** в hello меню hello влево сбоку экрана приветствия, а затем выберите **Azure Active Directory**.

4. Щелкните **Регистрация приложений**, а затем выберите **Добавить**.

5. Выполните запросы toocreate hello **веб-приложение** и/или **WebAPI**.
  * Hello **имя** из hello приложения описывает toousers вашего приложения.

  * Hello **URL-адрес входа** hello базовый URL-адрес приложения.  Hello в схему по умолчанию — "http://localhost:3000, auth/openid/возвращаемое ''.

6. Когда вы закончите регистрацию, Azure AD назначит приложению уникальный идентификатор. Необходимо, чтобы это значение в hello следующие разделы, поэтому скопируйте его со страницы приложения hello.
7. Из hello **параметры** -> **свойства** страницы приложения, обновите URI идентификатора приложения hello. Hello **URI идентификатора приложения** — это уникальный идентификатор для вашего приложения. соглашение о Hello — формат hello toouse `https://<tenant-domain>/<app-name>`, например: `https://contoso.onmicrosoft.com/my-first-aad-app`.

## <a name="step-2-add-prerequisites-tooyour-directory"></a>Шаг 2: Добавьте каталог tooyour предварительные требования
1. Из командной строки hello, изменить каталоги tooyour корневую папку, если вы еще не существует, и затем выполнения hello следующие команды:

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. Кроме того, вам потребуется `passport-azure-ad`:
    * `npm install passport-azure-ad`

При этом устанавливаются библиотеки hello, `passport-azure-ad` зависит.

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>Шаг 3: Настройка стратегии приложения hello toouse passport узел js
Здесь мы настраиваем Express toouse hello OpenID Connect протокол проверки подлинности.  Passport — используется toodo различные действия, включая проблемы входа и выхода, управление сеансом пользователя hello и получения сведений о пользователе hello.

1. toobegin Привет открыть `config.js` файл в корне hello hello проекта, а затем введите значения конфигурации приложения в hello `exports.creds` раздела.

  * Hello `clientID` — hello **идентификатор приложения** , имеет назначенный tooyour приложения на портале регистрации hello.

  * Hello `returnURL` — hello **Uri перенаправления** , введенное на портале hello.

  * Hello `clientSecret` — hello секрет, который был создан в портале hello.

2. Затем откройте hello `app.js` файл в корневой hello hello проекта. Затем добавьте следующий вызов tooinvoke hello hello `OIDCStrategy` стратегии, входящий в состав `passport-azure-ad`.

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. После этого с помощью стратегии hello, мы просто ссылаться toohandle нашей запросов на вход в.

    ```JavaScript
    // Use hello OIDCStrategy within Passport. (Section 2)
    //
    //   Strategies in passport require a `validate` function that accepts
    //   credentials (in this case, an OpenID identifier), and invokes a callback
    //   with a user object.
    passport.use(new OIDCStrategy({
        callbackURL: config.creds.returnURL,
        realm: config.creds.realm,
        clientID: config.creds.clientID,
        clientSecret: config.creds.clientSecret,
        oidcIssuer: config.creds.issuer,
        identityMetadata: config.creds.identityMetadata,
        skipUserProfile: config.creds.skipUserProfile,
        responseType: config.creds.responseType,
        responseMode: config.creds.responseMode
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
        if (!profile.email) {
        return done(new Error("No email found"), null);
        }
        // asynchronous verification, for effect...
        process.nextTick(function () {
        findByEmail(profile.email, function(err, user) {
            if (err) {
            return done(err);
            }
            if (!user) {
            // "Auto-registration"
            users.push(profile);
            return done(null, profile);
            }
            return done(null, user);
        });
        });
    }
    ));
    ```
Для Passport свойственно аналогичное поведение для всех стратегий (Twitter, Facebook и т. д.); это поведение учитывают все разработчики модулей стратегий. Глядя стратегии hello, видно, что мы передаем его функции, которая содержит маркер и выполняются как параметры hello. Стратегия Hello поставляется обратно toous после он выполняет свою работу. Затем мы хотим toostore hello пользователя и маркер hello образа, поэтому нам не нужен tooask его еще раз.

> [!IMPORTANT]
Предыдущий код Hello принимает любой пользователь, который происходит tooauthenticate tooour сервера. Это называется автоматической регистрацией. Рекомендуется, чтобы не дать любой пользователь проверку подлинности tooa рабочего сервера без необходимости их регистрации через процесс выбора. Обычно это является шаблон hello в потребительские приложения, которые позволяет tooregister с Facebook, а затем попросите tooprovide дополнительных сведений. Если это не были образец приложения, мы удалось извлекли адрес электронной почты пользователя hello из hello токен объекта, который возвращается и затем предложено hello toofill пользователя дополнительных сведений. Так как на тестовом сервере, мы их добавить toohello базы данных в памяти.


4. Далее добавим hello методы, позволяющие определить tootrack hello вошедших пользователей, необходимые службы Passport. Эти методы включают сериализацию и десериализацию сведений о пользователе hello.

    ```JavaScript

            // Passport session setup. (Section 2)

            //   toosupport persistent sign-in sessions, Passport needs toobe able to
            //   serialize users into hello session and deserialize them out of hello session. Typically,
            //   this is done simply by storing hello user ID when serializing and finding
            //   hello user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array toohold signed-in users
            var users = [];

            var findByEmail = function(email, fn) {
            for (var i = 0, len = users.length; i < len; i++) {
                var user = users[i];
            log.info('we are using user: ', user);
                if (user.email === email) {
                return fn(null, user);
                }
            }
            return fn(null, null);
            };
    ```

5.  Далее добавим механизм Express hello tooload кода hello. Здесь мы используем /views по умолчанию hello и предоставляет шаблон /routes, Express.

    ```JavaScript

        // configure Express (section 2)

            var app = express();
            app.configure(function() {
          app.set('views', __dirname + '/views');
          app.set('view engine', 'ejs');
          app.use(express.logger());
          app.use(express.methodOverride());
          app.use(cookieParser());
          app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
          app.use(bodyParser.urlencoded({ extended : true }));
          // Initialize Passport!  Also use passport.session() middleware, toosupport
          // persistent login sessions (recommended).
          app.use(passport.initialize());
          app.use(passport.session());
          app.use(app.router);
          app.use(express.static(__dirname + '/../../public'));
        });

    ```

6. Наконец, добавим hello направляет, передайте hello фактических запросов toohello `passport-azure-ad` ядра:


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware tooauthenticate the
        //   request. hello first step in OpenID authentication involves redirecting
        //   hello user tootheir OpenID provider. After authenticating, hello OpenID
        //   provider redirects hello user back toothis application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in hello Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Шаг 4: Используйте Passport tooissue входа и запросах на выход tooAzure AD
Приложение теперь будет правильно настроен toocommunicate с конечной точкой hello с помощью протокола проверки подлинности OpenID Connect hello.  `passport-azure-ad`Разобравшись все параметры hello отправляемого сообщения проверки подлинности, проверки токенов из Azure AD и поддержку пользовательских сеансов. Все, что остается предоставление пользователям способ toosign в и выхода, а сбор дополнительных сведений о hello вошедших пользователей.

1. Во-первых давайте добавим по умолчанию hello, вход, учетной записи и выхода методов tooour `app.js` файла:

    ```JavaScript

        //Routes (section 4)

        app.get('/', function(req, res){
          res.render('index', { user: req.user });
        });

        app.get('/account', ensureAuthenticated, function(req, res){
          res.render('account', { user: req.user });
        });

        app.get('/login',
          passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
          function(req, res) {
            log.info('Login was called in hello Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  Рассмотрим это подробно.

  * Hello `/`маршрута перенаправляет toohello index.ejs представлении, передавая hello пользователя в запросе hello, (если он существует).
  * Hello `/account` сначала *гарантирует, проходят проверку* (Мы реализовали, в следующий пример hello), а затем передает hello пользователя в запросе hello, чтобы мы могли получить дополнительные сведения о пользователе hello.
  * Hello `/login` маршрут вызывает наши средства проверки подлинности azuread openidconnect из `passport-azuread`. Если, не удается, он перенаправляет hello назад слишком или имя входа пользователя.
  * Hello `/logout` маршрута просто вызывает hello logout.ejs и маршрута, какие файлы cookie очищает, а затем возвращает hello задней tooindex.ejs пользователя.

3. Для hello последнюю часть `app.js`, добавим hello **EnsureAuthenticated** метод, используемый в `/account`, как показано выше.

    ```JavaScript

        // Simple route middleware tooensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs toobe protected. If
        //   hello request is authenticated (typically via a persistent sign-in session),
        //   hello request proceeds. Otherwise, hello user is redirected toothe
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. Наконец, давайте создадим сам сервер hello в `app.js`:

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a>Шаг 5: toodisplay нашей пользователя на веб-сайте hello, создание представления hello и маршруты в экспресс-выпуск
Теперь файл `app.js` готов. Мы просто необходимые маршруты tooadd hello и представления отображаются сведения hello мы получить toohello пользователя, а также обрабатывать hello `/logout` и `/login` маршрутов, которая была создана.

1. Создать hello `/routes/index.js` маршрута в корневом каталоге hello.

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. Создать hello `/routes/user.js` маршрута в корневом каталоге hello.

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 Они передают представлений tooour hello запросов, включая hello пользователя при его наличии.

3. Создать hello `/views/index.ejs` представления в корневом каталоге hello. Это простой страницы, который вызывает методы нашей входа и выхода из системы и позволяет нам toograb сведения об учетной записи. Обратите внимание, что мы используем hello условного `if (!user)` как свидетельство у нас есть пользователя, выполнившего вход пользователя hello, передаваемых через запрос hello.

    ```JavaScript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
        <h2>Hello, <%= user.displayName %>.</h2>
        <a href="/account">Account Info</a></br>
        <a href="/logout">Log Out</a>
    <% } %>
    ```

4. Создать hello `/views/account.ejs` просмотра в корневом каталоге hello, чтобы мы могли просматривать дополнительные сведения, `passport-azuread` приостановил в запросе пользователя hello.

    ```Javascript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
    <p>displayName: <%= user.displayName %></p>
    <p>givenName: <%= user.name.givenName %></p>
    <p>familyName: <%= user.name.familyName %></p>
    <p>UPN: <%= user._json.upn %></p>
    <p>Profile ID: <%= user.id %></p>
  ##Next steps  <p>Full Claimes</p>
    <%- JSON.stringify(user) %>
    <p></p>
    <a href="/logout">Log Out</a>
    <% } %>
    ```

5. Теперь давайте все красиво оформим, добавив макет. Создать hello "/ views/layout.ejs" в разделе "hello корневой каталог.

    ```HTML

    <!DOCTYPE html>
    <html>
        <head>
            <title>Passport-OpenID Example</title>
        </head>
        <body>
            <% if (!user) { %>
                <p>
                <a href="/">Home</a> |
                <a href="/login">Log In</a>
                </p>
            <% } else { %>
                <p>
                <a href="/">Home</a> |
                <a href="/account">Account</a> |
                <a href="/logout">Log Out</a>
                </p>
            <% } %>
            <%- body %>
        </body>
    </html>
    ```

##<a name="next-steps"></a>Дальнейшие действия
Наконец, создайте и запустите приложение. Запустите `node app.js`, а затем перейдите слишком`http://localhost:3000`.

Войдите, используя личную учетную запись Майкрософт или рабочую учетную запись и обратите внимание на то, как удостоверение пользователя hello отражается в списке hello/Account. Теперь у вас есть веб-приложение, защищенное с помощью стандартных отраслевых протоколов, которое может выполнять аутентификацию пользователей с использованием личных, рабочих и учебных учетных записей.

Справочник по hello выполнить пример (без настройки) [предоставляется как ZIP-файл](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip). Вы также можете клонировать его из репозитория GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

Теперь можно перейти к более сложным темам. Может потребоваться tootry:

[Приступая к работе с веб-интерфейсом API для узла](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
