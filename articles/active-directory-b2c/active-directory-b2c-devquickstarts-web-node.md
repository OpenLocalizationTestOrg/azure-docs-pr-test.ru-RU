---
title: "веб-приложение Node.js aaaAdd tooa вход для Azure B2C | Документы Microsoft"
description: "Как toobuild Node.js веб-приложение, которое входит в число пользователей с помощью клиента B2C."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a>Azure AD B2C: Добавление веб-приложение Node.js tooa входа

**Passport** — промежуточный слой проверки подлинности для Node.js. Гибкая модульная структура Passport позволяет незаметно устанавливать его в любом приложении на основе Express или в веб-приложении Restify. Полный набор стратегий поддерживает проверку подлинности с помощью имени пользователя и пароля, Facebook, Twitter и других средств.

Мы разработали стратегию для Azure Active Directory (Azure AD). Будет установлено этот модуль и затем добавить hello Azure AD `passport-azure-ad` подключаемого модуля.

toodo это, необходимо:

1. Зарегистрировать приложение с помощью Azure AD.
2. Настройка toouse вашего приложения hello `passport-azure-ad` подключаемого модуля.
3. Используйте Passport tooissue входа и запросах на выход tooAzure AD.
4. Ввести данные пользователя.

Здравствуйте, код для этого учебника [сохраняется на сайте GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS). можно toofollow вдоль [загрузить приложение hello основу как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip). Также можно клонировать основу hello:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

в конце этого учебника в hello предоставляется приложения Hello завершена.

## <a name="get-an-azure-ad-b2c-directory"></a>Создание каталога Azure AD B2C

Перед использованием Azure AD B2C необходимо создать каталог или клиент.  Каталог — это контейнер для данных всех ваших пользователей, приложений, групп и т. д. Прежде чем продолжать работу с руководством, [создайте каталог B2C](active-directory-b2c-get-started.md), если вы его еще не создали.

## <a name="create-an-application"></a>Создание приложения

Далее необходимо toocreate приложения в каталоге B2C. Это предоставляет сведения Azure AD, что ему требуется toocommunicate безопасно вместе с приложением. Оба hello клиентского приложения и веб-API, будет представлен один **идентификатор приложения**, так как они включают в себя один логический приложения. toocreate приложения, выполните [эти инструкции](active-directory-b2c-app-registration.md). Не забудьте сделать следующее.

- Включить **веб-приложения**/**веб-API** в приложение hello.
- Введите `http://localhost:3000/auth/openid/return` в качестве значения **URL-адреса ответа**. Это URL-адрес по умолчанию hello для этого примера кода.
- Создайте для своего приложения **секрет приложения** и скопируйте его. Оно понадобится вам позднее. Обратите внимание, что это значение должно toobe [XML переключения](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) перед его использованием.
- Копировать hello **идентификатор приложения** , назначенный tooyour приложения. Этот идентификатор также понадобится вам позднее.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Создание политик

В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md). Это приложение содержит три вида идентификации: регистрация, вход и вход с помощью учетной записи Facebook. Необходимые toocreate этой политики каждого типа, как описано в [статье политики](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). При создании трех политик обязательно выполните указанные ниже действия.

- Выберите hello **отображаемое имя** и другие атрибуты регистрации в политике организации доступа к Интернету.
- Выберите hello **отображаемое имя** и **идентификатор объекта** утверждений приложения в каждой политике. Можно также выбрать другие утверждения.
- Копировать hello **имя** каждой политики, после его создания. Он должен иметь префикс hello `b2c_1_`.  Эти имена политик понадобятся вам через некоторое время.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

После создания трех политик, вы будете готовы toobuild приложения.

Обратите внимание, что данная статья не охватывает как toouse hello политик вы только что создали. toolearn о том, как работают политики в Azure AD B2C, начинаться с hello [.NET web app начало учебника](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="add-prerequisites-tooyour-directory"></a>Добавьте каталог tooyour предварительные требования

Из командной строки hello измените каталоги tooyour корневую папку, если вы не являетесь уже существует. Выполните следующие команды hello.

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

Кроме того, мы использовали `passport-azure-ad` нашей предварительной версии в основу hello объекта hello краткое руководство.

- `npm install passport-azure-ad`

Будет выполнена установка библиотеки hello, `passport-azure-ad` зависит.

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a>Настройка вашего приложения toouse hello стратегии Passport Node.js
Настройте hello Express по промежуточного слоя toouse hello протокол проверки подлинности OpenID Connect. Passport будет используется tooissue запросы входа и выхода, управлять сеансами пользователей, а получение сведений о пользователях, среди других действий.

Откройте hello `config.js` файл в корневом каталоге hello проекта hello и введите значения конфигурации приложения в hello `exports.creds` раздела.
- `clientID`: hello **идентификатор приложения** назначенный tooyour приложения на портале регистрации hello.
- `returnURL`: hello **URI перенаправления** введенное на портале hello.
- `tenantName`: hello имя клиентского приложения, например, **contoso.onmicrosoft.com**.

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Откройте hello `app.js` файл в корневой hello hello проекта. Добавьте следующий вызов tooinvoke hello hello `OIDCStrategy` стратегии, входящий в состав `passport-azure-ad`.


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

Используйте только ссылка на запросов на вход в toohandle стратегию hello.

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
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
Passport использует аналогичный шаблон для всех своих стратегий (в том числе Twitter и Facebook). Все записи стратегии придерживаться toothis шаблон. При просмотре hello стратегии можно увидеть, передать его `function()` с маркером и `done` как параметры hello. Стратегия Hello возвращаются tooyou после его всю свою работу. Хранить пользователя hello и задание hello маркер, чтобы tooask для него не требуется еще раз.

> [!IMPORTANT]
Hello выше код принимает все пользователи, которым hello проводит проверку подлинности. Это называется автоматической регистрацией. При использовании рабочих серверов требуется запретить toolet пользователей, если только они прошли через процесс регистрации, который вы настроили. Этот шаблон часто используется в потребительских приложениях. Это позволяет tooregister с помощью Facebook, а затем он просит toofill дополнительных сведений. Если приложения были не образец, мы может извлечь из hello объекта маркера, который возвращается адрес электронной почты, а затем попросите hello toofill пользователя дополнительных сведений. Так как на тестовом сервере, мы просто добавьте пользователей базы данных в памяти toohello.

Добавьте hello методы, позволяющие отслеживать tookeep пользователей, вошедших в, как требует Passport. Сюда относится сериализация и десериализация информации о пользователе:

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
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

Добавьте модуль экспресс-выпуск hello tooload кода hello. В следующих hello, вы увидите, что используется по умолчанию hello `/views` и `/routes` шаблон, предоставляющий экспресс-выпуск.

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

Добавить hello `POST` маршруты, в которых сдачей hello фактических запросов toohello `passport-azure-ad` ядра:

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Используйте Passport tooissue входа и запросах на выход tooAzure AD

Приложение теперь будет правильно настроен toocommunicate с конечной точкой hello v2.0 с помощью протокола проверки подлинности OpenID Connect hello. `passport-azure-ad`Разобравшись сведения hello отправляемого сообщения проверки подлинности, проверки токенов из Azure AD и поддержания сеанса пользователя. Все, что остается является toogive пользователей toosign способом в и выполните выход и toogather Дополнительные сведения о пользователях, вошедших в.

Сначала добавьте по умолчанию hello, вход, учетной записи и выхода методов tooyour `app.js` файла:

```JavaScript

//Routes (Section 4)

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

tooreview эти методы подробно:
- Hello `/` маршрут перенаправляет toohello `index.ejs` представлении, передавая hello пользователя в запросе hello (если он существует).
- Hello `/account` маршрута сначала проверяет, проходят проверку подлинности (hello реализацию для этой ниже). Затем инфраструктура службы передает hello пользователя в запросе hello так, чтобы получить дополнительные сведения о пользователе hello.
- Hello `/login` hello вызовов маршрута `azuread-openidconnect` проверки подлинности из `passport-azure-ad`. Если не выполнены успешно, маршрут hello hello пользователь перенаправляется обратно слишком`/login`.
- `/logout` просто вызывает `logout.ejs` (и соответствующий маршрут). Это приведет к очистке файлы cookie и затем возвращает hello пользователя обратно слишком`index.ejs`.


Для hello последнюю часть `app.js`, добавить hello `EnsureAuthenticated` метод, используемый в hello `/account` маршрута.

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

Наконец, создайте сам сервер hello в `app.js`.

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a>Создание представлений hello и направляет в Express toocall политик

`app.js` готово. Необходимо просто tooadd hello маршруты и представления, которые позволяют hello toocall входа и регистрации политики. Они также обрабатывать hello `/logout` и `/login` маршруты, вы создали.

Создать hello `/routes/index.js` маршрута в корневом каталоге hello.

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

Создать hello `/routes/user.js` маршрута в корневом каталоге hello.

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

Эти простые маршруты передавать запросы tooyour представления. Они включают hello пользователя, если такая имеется.

Создать hello `/views/index.ejs` представления в корневом каталоге hello. Это простая страница, которая вызывает политики входа и выхода. Ее можно также использовать toograb сведения об учетной записи. Обратите внимание, можно использовать условные hello `if (!user)` как hello пользователя передается в запрос hello tooprovide свидетельства hello пользователя вход в систему.

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

Создать hello `/views/account.ejs` открыть в корневом каталоге hello, можно просмотреть дополнительные сведения, `passport-azure-ad` поместить в запросе пользователя hello.

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
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

Выполните сборку и запустите приложение.

Запустите `node app.js` и перейдите в слишком`http://localhost:3000`


Регистрация или вход в приложение toohello с помощью электронной почты или Facebook. Выйдите и снова войдите от имени другого пользователя.

##<a name="next-steps"></a>Дальнейшие действия

Справочник по hello выполнить пример (без настройки) [предоставляется как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip). Кроме того, его можно клонировать из GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

Теперь можно переходить на toomore дополнительные разделы. Попробуйте ознакомиться с такими материалами:

[Безопасность веб-API с помощью модели hello B2C в Node.js](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
