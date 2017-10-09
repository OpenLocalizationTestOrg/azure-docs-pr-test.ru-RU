---
title: "v2.0 Active Directory aaaAzure Node.js web app вход | Документы Microsoft"
description: "Узнайте, как toobuild Node.js веб-приложение, которое выполняет вход пользователя, используя личную учетную запись Майкрософт и рабочую или учебную учетную запись."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f8ce6e2b841c215cb14e82bcf444fe849634cc88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-nodejs-web-app"></a>Добавить веб-приложение Node.js tooa входа

> [!NOTE]
> Не все сценарии Azure Active Directory и возможности работы с конечной точкой v2.0 hello. toodetermine необходимость использования hello v2.0 конечная точка либо hello v1.0, узнайте, как [ограничения v2.0](active-directory-v2-limitations.md).
> 

В этом учебнике мы используем hello toodo Passport следующие задачи:

* В веб-приложении вход hello пользователя с помощью Azure Active Directory (Azure AD) и hello v2.0 конечной точки.
* Отображение сведений о пользователе hello.
* Знак hello выход пользователя из приложения hello.

**Passport** — промежуточный слой проверки подлинности для Node.js. Он отличается гибкой модульной структурой, которая позволяет сравнительно незаметно размещать его в любом приложении на основе Express или веб-приложении Restify. В Passport полный набор стратегий поддерживает процесс проверки подлинности с помощью имени пользователя и пароля, Facebook, Twitter и проч. Мы разработали стратегию для Azure AD. В этой статье рассказывается как tooinstall hello модуля, а затем добавьте hello Azure AD `passport-azure-ad` подключаемого модуля.

## <a name="download"></a>Загрузить
поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs). toofollow hello учебник, вы можете [загрузить приложение hello основу как ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) или основу hello клона:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Можно также получить приложение hello завершено в конце hello этого учебника.

## <a name="1-register-an-app"></a>Шаг 1. Регистрация приложения
Создайте новое приложение на [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), или выполните [эти подробные шаги](active-directory-v2-app-registration.md) tooregister приложения. Не забудьте выполнить следующие действия.

* Копировать hello **идентификатор приложения** назначенный tooyour приложения. Он потребуется для работы с этим руководством.
* Добавить hello **Web** платформы для приложения.
* Копировать hello **URI перенаправления** из портала hello. Необходимо использовать значение по умолчанию URI hello `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-add-prerequisities-tooyour-directory"></a>2: добавьте каталог tooyour соответствия предварительным условиям
В командной строке измените каталоги toogo tooyour корневую папку, если вы еще не существует. Выполните следующие команды hello.

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`

Кроме того, мы используем `passport-azure-ad` в основу hello объекта hello краткое руководство:

* `npm install passport-azure-ad`

При этом устанавливаются библиотеки hello, `passport-azure-ad` использует.

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>3: Настройка стратегии приложения hello toouse passport узел js
Настройка hello Express по промежуточного слоя toouse hello протокол проверки подлинности OpenID Connect. Использовать запросы tooissue входа и выхода службы Passport, управлять hello пользовательского сеанса и получения сведений о пользователе hello, среди прочего.

1.  В корневой hello hello проекта откройте файл Config.js hello. В hello `exports.creds` введите значения конфигурации приложения.
  
  * `clientID`: hello **идентификатор приложения** , имеет назначенный tooyour приложения hello портал Azure.
  * `returnURL`: hello **URI перенаправления** , введенное на портале hello.
  * `clientSecret`: hello секрет, который был создан в портале hello.

2.  В корневой hello hello проекта откройте файл в файле App.js hello. stratey OIDCStrategy tooinvoke hello, который поставляется вместе с `passport-azure-ad`, добавьте следующий вызовом hello:

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  toohandle запросов входа в систему, используйте только ссылка на стратегию hello:

  ```JavaScript
  // Use hello OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. hello function accepts
  //   credentials (in this case, an OpenID identifier), and invokes a callback
  //   with a user object.
  passport.use( new OIDCStrategy({
      callbackURL: config.creds.returnURL,
      realm: config.creds.realm,
      clientID: config.creds.clientID,
      clientSecret: config.creds.clientSecret,
      oidcIssuer: config.creds.issuer,
      identityMetadata: config.creds.identityMetadata,
      responseType: config.creds.responseType,
      responseMode: config.creds.responseMode,
      skipUserProfile: config.creds.skipUserProfile
      scope: config.creds.scope
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
      log.info('Example: Email address we received was: ', profile.email);
      // Asynchronous verification, for effect...
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

Для Passport свойственно аналогичное поведение для всех стратегий (Twitter, Facebook и т. д.). Все записи стратегии придерживаться toohello шаблон. Передайте hello стратегии `function()` , использует токен и `done` в качестве параметров. Стратегия Hello возвращается после его свою работу. Пользователь hello хранилища и образа hello маркер tooask для него требуется еще раз.

  > [!IMPORTANT]
  > Hello выше код принимает любой пользователь, который может проверить подлинность сервера tooyour. Это называется автоматической регистрацией. На рабочем сервере не стоит toolet любой пользователь без необходимости их пройти процесс регистрации, выборе. Обычно это hello шаблон, который вы видите в потребительские приложения. приложение Hello может разрешить tooregister с Facebook, но затем вас просят tooenter дополнительных сведений. Если с помощью программы командной строки не были в этом учебнике, можно извлечь из hello объекта маркера, который возвращается hello электронной почты. Затем задайте себе вопрос: hello пользователя tooenter Дополнительные сведения. Так как на тестовом сервере, можно добавить пользователя hello непосредственно toohello в памяти базы данных.
  > 
  > 

4.  Добавьте методы hello используется отслеживание tookeep пользователей, которые выполнили вход, как требует Passport. Сюда входят сериализацию и десериализацию сведений о пользователе hello:

  ```JavaScript

  // Passport session setup (section 2)

  //   toosupport persistent login sessions, Passport needs toobe able to
  //   serialize users into, and deserialize users out of, hello session. Typically,
  //   this is as simple as storing hello user ID when serializing, and finding
  //   hello user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array toohold signed-in users
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

5.  Добавьте код hello, загружает модуль экспресс-выпуск hello. Использовать /views по умолчанию hello и предоставляет шаблон /routes, Express:

  ```JavaScript

  // Set up Express (section 2)

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

6.  Добавить hello POST направляет, передайте hello фактических запросов toohello `passport-azure-ad` ядра:

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. hello first step in OpenID authentication involves redirecting
  //   hello user toohello user's OpenID provider. After authenticating, hello OpenID
  //   provider redirects hello user back toothis application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in hello sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called.
  //   In this example, it redirects hello user toohello home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called. 
  //   In this example, it redirects hello user toohello home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>4: используйте Passport tooissue входа и выхода запрашивает tooAzure AD
Приложение теперь имеет toocommunicate с конечной точкой hello v2.0 с помощью протокола проверки подлинности OpenID Connect hello. Hello `passport-azure-ad` стратегии берет на себя все сведения hello отправляемого сообщения проверки подлинности, проверки токенов из Azure AD и поддержания сеанса пользователя hello. ALL, которая остается toodo является toogive пользователей toosign способом в и знак ожидания и toogather Дополнительные сведения о hello пользователю, вошедшему в систему.

1.  Добавить hello **по умолчанию**, **входа**, **учетной записи**, и **выхода** методы tooyour в файле App.js файла:

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
      log.info('Login was called in hello sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  Ниже приведены сведения о hello.
    
    * Hello `/` toohello index.ejs представление перенаправляет маршрута. Он передает hello пользователя в запросе hello (если он существует).
    * Hello `/account` сначала *гарантирует, что Вы авторизованы* (реализации, в hello после кода). Затем он передает hello пользователя в запросе hello. Это, чтобы получить дополнительные сведения о пользователе hello.
    * Hello `/login` маршрутизацию вызовов к `azuread-openidconnect` проверки подлинности из `passport-azuread`. Если, не удается, он перенаправляет пользователя hello обратно слишком`/login`.
    * Hello `/logout` маршрута вызывает hello logout.ejs Просмотр (и маршрутизации). Это приведет к очистке файлы cookie, а затем возвращает hello задней tooindex.ejs пользователя.

2.  Добавить hello **EnsureAuthenticated** метод, который использовался ранее в `/account`:

  ```JavaScript

  // Route middleware tooensure hello user is authenticated (section 4)

  //   Use this route middleware on any resource that needs toobe protected. If
  //   hello request is authenticated (typically via a persistent login session),
  //   hello request proceeds. Otherwise, hello user is redirected toothe
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  В файле App.js создайте hello server:

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a>5: создавать представления hello и маршруты в экспресс-выпуск, что показывает пользователя на веб-сайте hello
Добавьте маршруты hello и представления, отображающие сведения toohello пользователя. маршруты Hello и представлений также обрабатывать hello `/logout` и `/login` маршруты, которые были созданы.

1. В корневом каталоге hello, создать hello `/routes/index.js` маршрута.

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  В корневом каталоге hello, создать hello `/routes/user.js` маршрута.

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  `/routes/index.js`и `/routes/user.js` простой маршруты, которые передают представлений tooyour hello запросов, включая hello пользователя, если он имеется.

3.  В корневом каталоге hello, создать hello `/views/index.ejs` представления. Эта страница вызывает методы **входа** и **выхода**. Можно также использовать hello `/views/index.ejs` просмотра toocapture сведения об учетной записи. Можно использовать условные hello `if (!user)` имени пользователя hello, передаваемых через запрос hello. свидетельствуют о том, что он вошел в систему.

  ```JavaScript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
      <h2>Hello, <%= user.displayName %>.</h2>
      <a href="/account">Account info</a></br>
      <a href="/logout">Sign out</a>
  <% } %>
  ```

4.  В корневом каталоге hello, создать hello `/views/account.ejs` представления. Hello `/views/account.ejs` представление позволяет tooview дополнительной информацией, `passport-azuread` помещает в запросе пользователя hello.

  ```Javascript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
  <p>displayName: <%= user.displayName %></p>
  <p>givenName: <%= user.name.givenName %></p>
  <p>familyName: <%= user.name.familyName %></p>
  <p>UPN: <%= user._json.upn %></p>
  <p>Profile ID: <%= user.id %></p>
  <p>Full Claimes</p>
  <%- JSON.stringify(user) %>
  <p></p>
  <a href="/logout">Sign out</a>
  <% } %>
  ```

5.  Добавьте макет. В корневом каталоге hello, создать hello `/views/layout.ejs` представления.

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
              <a href="/login">Sign in</a>
              </p>
          <% } else { %>
              <p>
              <a href="/">Home</a> |
              <a href="/account">Account</a> |
              <a href="/logout">Sign out</a>
              </p>
          <% } %>
          <%- body %>
      </body>
  </html>
  ```

6.  toobuild и запустить приложение, запустите `node app.js`. Перейдите слишком`http://localhost:3000`.

7.  Войдите с помощью личной учетной записи Майкрософт либо рабочей или учебной учетной записи. Обратите внимание, что удостоверение пользователя hello в списке hello/Account. 

Теперь у вас есть веб-приложение, защищенное с помощью стандартных протоколов. Вы можете выполнить проверку подлинности пользователей в приложении с помощью личных, рабочих или учебных учетных записей.

## <a name="next-steps"></a>Дальнейшие действия
Справочник по образец hello завершена (без настройки) предоставляется как [ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip). Кроме того, его можно клонировать из GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Затем можно переместить на toomore дополнительные разделы. Может потребоваться tootry:

[Безопасность веб-API Node.js с помощью конечной точки v2.0 hello](active-directory-v2-devquickstarts-node-api.md)

Ниже приведены некоторые дополнительные ресурсы.

* [Вход для пользователей учетных записей Майкрософт и Azure AD в одном приложении](active-directory-appmodel-v2-overview.md)
* [Тег StackOverflow "azure-active-directory"](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Получение обновлений системы безопасности для наших продуктов
Мы рекомендуем toosign копирование toobe уведомлений при внесении угрозы безопасности. На hello [выпуске](https://technet.microsoft.com/security/dd252948) страницы, подписаться на оповещения tooSecurity рекомендации.

