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
# <a name="add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="c65c3-103">Добавить веб-приложение Node.js tooa входа</span><span class="sxs-lookup"><span data-stu-id="c65c3-103">Add sign-in tooa Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="c65c3-104">Не все сценарии Azure Active Directory и возможности работы с конечной точкой v2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="c65c3-105">toodetermine необходимость использования hello v2.0 конечная точка либо hello v1.0, узнайте, как [ограничения v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="c65c3-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="c65c3-106">В этом учебнике мы используем hello toodo Passport следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c65c3-106">In this tutorial, we use Passport toodo hello following tasks:</span></span>

* <span data-ttu-id="c65c3-107">В веб-приложении вход hello пользователя с помощью Azure Active Directory (Azure AD) и hello v2.0 конечной точки.</span><span class="sxs-lookup"><span data-stu-id="c65c3-107">In a web app, sign in hello user by using Azure Active Directory (Azure AD) and hello v2.0 endpoint.</span></span>
* <span data-ttu-id="c65c3-108">Отображение сведений о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-108">Display information about hello user.</span></span>
* <span data-ttu-id="c65c3-109">Знак hello выход пользователя из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="c65c3-110">**Passport** — промежуточный слой проверки подлинности для Node.js.</span><span class="sxs-lookup"><span data-stu-id="c65c3-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="c65c3-111">Он отличается гибкой модульной структурой, которая позволяет сравнительно незаметно размещать его в любом приложении на основе Express или веб-приложении Restify.</span><span class="sxs-lookup"><span data-stu-id="c65c3-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="c65c3-112">В Passport полный набор стратегий поддерживает процесс проверки подлинности с помощью имени пользователя и пароля, Facebook, Twitter и проч.</span><span class="sxs-lookup"><span data-stu-id="c65c3-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="c65c3-113">Мы разработали стратегию для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c65c3-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="c65c3-114">В этой статье рассказывается как tooinstall hello модуля, а затем добавьте hello Azure AD `passport-azure-ad` подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="c65c3-114">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="c65c3-115">Загрузить</span><span class="sxs-lookup"><span data-stu-id="c65c3-115">Download</span></span>
<span data-ttu-id="c65c3-116">поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="c65c3-116">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="c65c3-117">toofollow hello учебник, вы можете [загрузить приложение hello основу как ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) или основу hello клона:</span><span class="sxs-lookup"><span data-stu-id="c65c3-117">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="c65c3-118">Можно также получить приложение hello завершено в конце hello этого учебника.</span><span class="sxs-lookup"><span data-stu-id="c65c3-118">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="c65c3-119">Шаг 1. Регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="c65c3-119">1: Register an app</span></span>
<span data-ttu-id="c65c3-120">Создайте новое приложение на [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), или выполните [эти подробные шаги](active-directory-v2-app-registration.md) tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="c65c3-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="c65c3-121">Не забудьте выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c65c3-121">Make sure you:</span></span>

* <span data-ttu-id="c65c3-122">Копировать hello **идентификатор приложения** назначенный tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="c65c3-122">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="c65c3-123">Он потребуется для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="c65c3-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="c65c3-124">Добавить hello **Web** платформы для приложения.</span><span class="sxs-lookup"><span data-stu-id="c65c3-124">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="c65c3-125">Копировать hello **URI перенаправления** из портала hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-125">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="c65c3-126">Необходимо использовать значение по умолчанию URI hello `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="c65c3-126">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-tooyour-directory"></a><span data-ttu-id="c65c3-127">2: добавьте каталог tooyour соответствия предварительным условиям</span><span class="sxs-lookup"><span data-stu-id="c65c3-127">2: Add prerequisities tooyour directory</span></span>
<span data-ttu-id="c65c3-128">В командной строке измените каталоги toogo tooyour корневую папку, если вы еще не существует.</span><span class="sxs-lookup"><span data-stu-id="c65c3-128">At a command prompt, change directories toogo tooyour root folder, if you are not already there.</span></span> <span data-ttu-id="c65c3-129">Выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-129">Run hello following commands:</span></span>

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

<span data-ttu-id="c65c3-130">Кроме того, мы используем `passport-azure-ad` в основу hello объекта hello краткое руководство:</span><span class="sxs-lookup"><span data-stu-id="c65c3-130">In addition, we use `passport-azure-ad` in hello skeleton of hello quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="c65c3-131">При этом устанавливаются библиотеки hello, `passport-azure-ad` использует.</span><span class="sxs-lookup"><span data-stu-id="c65c3-131">This installs hello libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="c65c3-132">3: Настройка стратегии приложения hello toouse passport узел js</span><span class="sxs-lookup"><span data-stu-id="c65c3-132">3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="c65c3-133">Настройка hello Express по промежуточного слоя toouse hello протокол проверки подлинности OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="c65c3-133">Set up hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="c65c3-134">Использовать запросы tooissue входа и выхода службы Passport, управлять hello пользовательского сеанса и получения сведений о пользователе hello, среди прочего.</span><span class="sxs-lookup"><span data-stu-id="c65c3-134">You use Passport tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, among other things.</span></span>

1.  <span data-ttu-id="c65c3-135">В корневой hello hello проекта откройте файл Config.js hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-135">In hello root of hello project, open hello Config.js file.</span></span> <span data-ttu-id="c65c3-136">В hello `exports.creds` введите значения конфигурации приложения.</span><span class="sxs-lookup"><span data-stu-id="c65c3-136">In hello `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="c65c3-137">`clientID`: hello **идентификатор приложения** , имеет назначенный tooyour приложения hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c65c3-137">`clientID`: hello **Application Id** that's assigned tooyour app in hello Azure portal.</span></span>
  * <span data-ttu-id="c65c3-138">`returnURL`: hello **URI перенаправления** , введенное на портале hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-138">`returnURL`: hello **Redirect URI** that you entered in hello portal.</span></span>
  * <span data-ttu-id="c65c3-139">`clientSecret`: hello секрет, который был создан в портале hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-139">`clientSecret`: hello secret that you generated in hello portal.</span></span>

2.  <span data-ttu-id="c65c3-140">В корневой hello hello проекта откройте файл в файле App.js hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-140">In hello root of hello project, open hello App.js file.</span></span> <span data-ttu-id="c65c3-141">stratey OIDCStrategy tooinvoke hello, который поставляется вместе с `passport-azure-ad`, добавьте следующий вызовом hello:</span><span class="sxs-lookup"><span data-stu-id="c65c3-141">tooinvoke hello OIDCStrategy stratey, which comes with `passport-azure-ad`, add hello following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="c65c3-142">toohandle запросов входа в систему, используйте только ссылка на стратегию hello:</span><span class="sxs-lookup"><span data-stu-id="c65c3-142">toohandle your sign-in requests, use hello strategy you just referenced:</span></span>

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

<span data-ttu-id="c65c3-143">Для Passport свойственно аналогичное поведение для всех стратегий (Twitter, Facebook и т. д.).</span><span class="sxs-lookup"><span data-stu-id="c65c3-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="c65c3-144">Все записи стратегии придерживаться toohello шаблон.</span><span class="sxs-lookup"><span data-stu-id="c65c3-144">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="c65c3-145">Передайте hello стратегии `function()` , использует токен и `done` в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="c65c3-145">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="c65c3-146">Стратегия Hello возвращается после его свою работу.</span><span class="sxs-lookup"><span data-stu-id="c65c3-146">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="c65c3-147">Пользователь hello хранилища и образа hello маркер tooask для него требуется еще раз.</span><span class="sxs-lookup"><span data-stu-id="c65c3-147">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c65c3-148">Hello выше код принимает любой пользователь, который может проверить подлинность сервера tooyour.</span><span class="sxs-lookup"><span data-stu-id="c65c3-148">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="c65c3-149">Это называется автоматической регистрацией.</span><span class="sxs-lookup"><span data-stu-id="c65c3-149">This is known as auto-registration.</span></span> <span data-ttu-id="c65c3-150">На рабочем сервере не стоит toolet любой пользователь без необходимости их пройти процесс регистрации, выборе.</span><span class="sxs-lookup"><span data-stu-id="c65c3-150">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="c65c3-151">Обычно это hello шаблон, который вы видите в потребительские приложения.</span><span class="sxs-lookup"><span data-stu-id="c65c3-151">This is usually hello pattern that you see in consumer apps.</span></span> <span data-ttu-id="c65c3-152">приложение Hello может разрешить tooregister с Facebook, но затем вас просят tooenter дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="c65c3-152">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="c65c3-153">Если с помощью программы командной строки не были в этом учебнике, можно извлечь из hello объекта маркера, который возвращается hello электронной почты.</span><span class="sxs-lookup"><span data-stu-id="c65c3-153">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="c65c3-154">Затем задайте себе вопрос: hello пользователя tooenter Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="c65c3-154">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="c65c3-155">Так как на тестовом сервере, можно добавить пользователя hello непосредственно toohello в памяти базы данных.</span><span class="sxs-lookup"><span data-stu-id="c65c3-155">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="c65c3-156">Добавьте методы hello используется отслеживание tookeep пользователей, которые выполнили вход, как требует Passport.</span><span class="sxs-lookup"><span data-stu-id="c65c3-156">Add hello methods that you use tookeep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="c65c3-157">Сюда входят сериализацию и десериализацию сведений о пользователе hello:</span><span class="sxs-lookup"><span data-stu-id="c65c3-157">This includes serializing and deserializing hello user's information:</span></span>

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

5.  <span data-ttu-id="c65c3-158">Добавьте код hello, загружает модуль экспресс-выпуск hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-158">Add hello code that loads hello Express engine.</span></span> <span data-ttu-id="c65c3-159">Использовать /views по умолчанию hello и предоставляет шаблон /routes, Express:</span><span class="sxs-lookup"><span data-stu-id="c65c3-159">You use hello default /views and /routes pattern that Express provides:</span></span>

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

6.  <span data-ttu-id="c65c3-160">Добавить hello POST направляет, передайте hello фактических запросов toohello `passport-azure-ad` ядра:</span><span class="sxs-lookup"><span data-stu-id="c65c3-160">Add hello POST routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

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

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="c65c3-161">4: используйте Passport tooissue входа и выхода запрашивает tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="c65c3-161">4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="c65c3-162">Приложение теперь имеет toocommunicate с конечной точкой hello v2.0 с помощью протокола проверки подлинности OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-162">Your app is now set up toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="c65c3-163">Hello `passport-azure-ad` стратегии берет на себя все сведения hello отправляемого сообщения проверки подлинности, проверки токенов из Azure AD и поддержания сеанса пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-163">hello `passport-azure-ad` strategy takes care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining hello user session.</span></span> <span data-ttu-id="c65c3-164">ALL, которая остается toodo является toogive пользователей toosign способом в и знак ожидания и toogather Дополнительные сведения о hello пользователю, вошедшему в систему.</span><span class="sxs-lookup"><span data-stu-id="c65c3-164">All that is left toodo is toogive your users a way toosign in and sign out, and toogather more information about hello user who is signed in.</span></span>

1.  <span data-ttu-id="c65c3-165">Добавить hello **по умолчанию**, **входа**, **учетной записи**, и **выхода** методы tooyour в файле App.js файла:</span><span class="sxs-lookup"><span data-stu-id="c65c3-165">Add hello **default**, **login**, **account**, and **logout** methods tooyour App.js file:</span></span>

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

  <span data-ttu-id="c65c3-166">Ниже приведены сведения о hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-166">Here are hello details:</span></span>
    
    * <span data-ttu-id="c65c3-167">Hello `/` toohello index.ejs представление перенаправляет маршрута.</span><span class="sxs-lookup"><span data-stu-id="c65c3-167">hello `/` route redirects toohello index.ejs view.</span></span> <span data-ttu-id="c65c3-168">Он передает hello пользователя в запросе hello (если он существует).</span><span class="sxs-lookup"><span data-stu-id="c65c3-168">It passes hello user in hello request (if it exists).</span></span>
    * <span data-ttu-id="c65c3-169">Hello `/account` сначала *гарантирует, что Вы авторизованы* (реализации, в hello после кода).</span><span class="sxs-lookup"><span data-stu-id="c65c3-169">hello `/account` route first *ensures that you are authenticated* (you implement that in hello following code).</span></span> <span data-ttu-id="c65c3-170">Затем он передает hello пользователя в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-170">Then, it passes hello user in hello request.</span></span> <span data-ttu-id="c65c3-171">Это, чтобы получить дополнительные сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-171">This is so you can get more information about hello user.</span></span>
    * <span data-ttu-id="c65c3-172">Hello `/login` маршрутизацию вызовов к `azuread-openidconnect` проверки подлинности из `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="c65c3-172">hello `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="c65c3-173">Если, не удается, он перенаправляет пользователя hello обратно слишком`/login`.</span><span class="sxs-lookup"><span data-stu-id="c65c3-173">If that doesn't succeed, it redirects hello user back too`/login`.</span></span>
    * <span data-ttu-id="c65c3-174">Hello `/logout` маршрута вызывает hello logout.ejs Просмотр (и маршрутизации).</span><span class="sxs-lookup"><span data-stu-id="c65c3-174">hello `/logout` route calls hello logout.ejs view (and route).</span></span> <span data-ttu-id="c65c3-175">Это приведет к очистке файлы cookie, а затем возвращает hello задней tooindex.ejs пользователя.</span><span class="sxs-lookup"><span data-stu-id="c65c3-175">This clears cookies, and then returns hello user back tooindex.ejs.</span></span>

2.  <span data-ttu-id="c65c3-176">Добавить hello **EnsureAuthenticated** метод, который использовался ранее в `/account`:</span><span class="sxs-lookup"><span data-stu-id="c65c3-176">Add hello **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

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

3.  <span data-ttu-id="c65c3-177">В файле App.js создайте hello server:</span><span class="sxs-lookup"><span data-stu-id="c65c3-177">In App.js, create hello server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a><span data-ttu-id="c65c3-178">5: создавать представления hello и маршруты в экспресс-выпуск, что показывает пользователя на веб-сайте hello</span><span class="sxs-lookup"><span data-stu-id="c65c3-178">5: Create hello views and routes in Express that you show your user on hello website</span></span>
<span data-ttu-id="c65c3-179">Добавьте маршруты hello и представления, отображающие сведения toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="c65c3-179">Add hello routes and views that show information toohello user.</span></span> <span data-ttu-id="c65c3-180">маршруты Hello и представлений также обрабатывать hello `/logout` и `/login` маршруты, которые были созданы.</span><span class="sxs-lookup"><span data-stu-id="c65c3-180">hello routes and views also handle hello `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="c65c3-181">В корневом каталоге hello, создать hello `/routes/index.js` маршрута.</span><span class="sxs-lookup"><span data-stu-id="c65c3-181">In hello root directory, create hello `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="c65c3-182">В корневом каталоге hello, создать hello `/routes/user.js` маршрута.</span><span class="sxs-lookup"><span data-stu-id="c65c3-182">In hello root directory, create hello `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="c65c3-183">`/routes/index.js`и `/routes/user.js` простой маршруты, которые передают представлений tooyour hello запросов, включая hello пользователя, если он имеется.</span><span class="sxs-lookup"><span data-stu-id="c65c3-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along hello request tooyour views, including hello user, if present.</span></span>

3.  <span data-ttu-id="c65c3-184">В корневом каталоге hello, создать hello `/views/index.ejs` представления.</span><span class="sxs-lookup"><span data-stu-id="c65c3-184">In hello root directory, create hello `/views/index.ejs` view.</span></span> <span data-ttu-id="c65c3-185">Эта страница вызывает методы **входа** и **выхода**.</span><span class="sxs-lookup"><span data-stu-id="c65c3-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="c65c3-186">Можно также использовать hello `/views/index.ejs` просмотра toocapture сведения об учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c65c3-186">You also use hello `/views/index.ejs` view toocapture account information.</span></span> <span data-ttu-id="c65c3-187">Можно использовать условные hello `if (!user)` имени пользователя hello, передаваемых через запрос hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-187">You can use hello conditional `if (!user)` as hello user being passed through in hello request.</span></span> <span data-ttu-id="c65c3-188">свидетельствуют о том, что он вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="c65c3-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="c65c3-189">В корневом каталоге hello, создать hello `/views/account.ejs` представления.</span><span class="sxs-lookup"><span data-stu-id="c65c3-189">In hello root directory, create hello `/views/account.ejs` view.</span></span> <span data-ttu-id="c65c3-190">Hello `/views/account.ejs` представление позволяет tooview дополнительной информацией, `passport-azuread` помещает в запросе пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="c65c3-190">hello `/views/account.ejs` view allows you tooview additional information that `passport-azuread` puts in hello user request.</span></span>

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

5.  <span data-ttu-id="c65c3-191">Добавьте макет.</span><span class="sxs-lookup"><span data-stu-id="c65c3-191">Add a layout.</span></span> <span data-ttu-id="c65c3-192">В корневом каталоге hello, создать hello `/views/layout.ejs` представления.</span><span class="sxs-lookup"><span data-stu-id="c65c3-192">In hello root directory, create hello `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="c65c3-193">toobuild и запустить приложение, запустите `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="c65c3-193">toobuild and run your app, run `node app.js`.</span></span> <span data-ttu-id="c65c3-194">Перейдите слишком`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="c65c3-194">Then, go too`http://localhost:3000`.</span></span>

7.  <span data-ttu-id="c65c3-195">Войдите с помощью личной учетной записи Майкрософт либо рабочей или учебной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c65c3-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="c65c3-196">Обратите внимание, что удостоверение пользователя hello в списке hello/Account.</span><span class="sxs-lookup"><span data-stu-id="c65c3-196">Note that hello user's identity is reflected in hello /account list.</span></span> 

<span data-ttu-id="c65c3-197">Теперь у вас есть веб-приложение, защищенное с помощью стандартных протоколов.</span><span class="sxs-lookup"><span data-stu-id="c65c3-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="c65c3-198">Вы можете выполнить проверку подлинности пользователей в приложении с помощью личных, рабочих или учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="c65c3-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c65c3-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c65c3-199">Next steps</span></span>
<span data-ttu-id="c65c3-200">Справочник по образец hello завершена (без настройки) предоставляется как [ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="c65c3-200">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="c65c3-201">Кроме того, его можно клонировать из GitHub:</span><span class="sxs-lookup"><span data-stu-id="c65c3-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="c65c3-202">Затем можно переместить на toomore дополнительные разделы.</span><span class="sxs-lookup"><span data-stu-id="c65c3-202">Next, you can move on toomore advanced topics.</span></span> <span data-ttu-id="c65c3-203">Может потребоваться tootry:</span><span class="sxs-lookup"><span data-stu-id="c65c3-203">You might want tootry:</span></span>

[<span data-ttu-id="c65c3-204">Безопасность веб-API Node.js с помощью конечной точки v2.0 hello</span><span class="sxs-lookup"><span data-stu-id="c65c3-204">Secure a Node.js web API by using hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="c65c3-205">Ниже приведены некоторые дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c65c3-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="c65c3-206">Вход для пользователей учетных записей Майкрософт и Azure AD в одном приложении</span><span class="sxs-lookup"><span data-stu-id="c65c3-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="c65c3-207">Тег StackOverflow "azure-active-directory"</span><span class="sxs-lookup"><span data-stu-id="c65c3-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="c65c3-208">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="c65c3-208">Get security updates for our products</span></span>
<span data-ttu-id="c65c3-209">Мы рекомендуем toosign копирование toobe уведомлений при внесении угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="c65c3-209">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="c65c3-210">На hello [выпуске](https://technet.microsoft.com/security/dd252948) страницы, подписаться на оповещения tooSecurity рекомендации.</span><span class="sxs-lookup"><span data-stu-id="c65c3-210">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

