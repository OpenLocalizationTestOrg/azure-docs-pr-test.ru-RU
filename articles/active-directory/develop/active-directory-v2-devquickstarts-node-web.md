---
title: "Вход в веб-приложение Node.js версии 2.0 в Azure Active Directory | Документация Майкрософт"
description: "Сведения о создании веб-приложения Node js, которое поддерживает вход пользователей в систему с помощью личной учетной записи Майкрософт, а также рабочей или учебной учетной записи."
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
ms.openlocfilehash: 6d49c742f72440e22830915c90de009d9188db2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="3aa48-103">Добавление функции входа в веб-приложение Node.js</span><span class="sxs-lookup"><span data-stu-id="3aa48-103">Add sign-in to a Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="3aa48-104">Не все сценарии и компоненты Azure Active Directory поддерживают конечную точку версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="3aa48-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="3aa48-105">Чтобы определить, стоит ли вам использовать конечную точку версии 2.0 или 1.0, ознакомьтесь с [ограничениями версии 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="3aa48-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="3aa48-106">В рамках этого руководства мы используем Passport, чтобы выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="3aa48-106">In this tutorial, we use Passport to do the following tasks:</span></span>

* <span data-ttu-id="3aa48-107">Вход пользователей в веб-приложение с помощью Azure Active Directory (Azure AD) и конечной точки версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="3aa48-107">In a web app, sign in the user by using Azure Active Directory (Azure AD) and the v2.0 endpoint.</span></span>
* <span data-ttu-id="3aa48-108">Отображение информации о пользователе.</span><span class="sxs-lookup"><span data-stu-id="3aa48-108">Display information about the user.</span></span>
* <span data-ttu-id="3aa48-109">Выход пользователя из приложения.</span><span class="sxs-lookup"><span data-stu-id="3aa48-109">Sign the user out of the app.</span></span>

<span data-ttu-id="3aa48-110">**Passport** — промежуточный слой проверки подлинности для Node.js.</span><span class="sxs-lookup"><span data-stu-id="3aa48-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="3aa48-111">Он отличается гибкой модульной структурой, которая позволяет сравнительно незаметно размещать его в любом приложении на основе Express или веб-приложении Restify.</span><span class="sxs-lookup"><span data-stu-id="3aa48-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="3aa48-112">В Passport полный набор стратегий поддерживает процесс проверки подлинности с помощью имени пользователя и пароля, Facebook, Twitter и проч.</span><span class="sxs-lookup"><span data-stu-id="3aa48-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="3aa48-113">Мы разработали стратегию для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3aa48-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="3aa48-114">В этой статье описывается установка модуля и последующее добавление подключаемого модуля `passport-azure-ad` Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3aa48-114">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="3aa48-115">Загрузить</span><span class="sxs-lookup"><span data-stu-id="3aa48-115">Download</span></span>
<span data-ttu-id="3aa48-116">Код в этом учебнике размещен на портале [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="3aa48-116">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="3aa48-117">Для выполнения действий в этом руководстве вы можете [скачать заготовку приложения как ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) или клонировать структуру:</span><span class="sxs-lookup"><span data-stu-id="3aa48-117">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="3aa48-118">Вы также можете воспользоваться готовым приложением в конце этого руководства.</span><span class="sxs-lookup"><span data-stu-id="3aa48-118">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="3aa48-119">Шаг 1. Регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="3aa48-119">1: Register an app</span></span>
<span data-ttu-id="3aa48-120">Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md), чтобы зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="3aa48-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="3aa48-121">Не забудьте выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3aa48-121">Make sure you:</span></span>

* <span data-ttu-id="3aa48-122">Скопируйте **идентификатор приложения**, назначенный приложению.</span><span class="sxs-lookup"><span data-stu-id="3aa48-122">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="3aa48-123">Он потребуется для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="3aa48-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="3aa48-124">Добавьте **веб-платформу** для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="3aa48-124">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="3aa48-125">Скопируйте значение **URI перенаправления** с портала.</span><span class="sxs-lookup"><span data-stu-id="3aa48-125">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="3aa48-126">Необходимо использовать значение URI по умолчанию — `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="3aa48-126">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-to-your-directory"></a><span data-ttu-id="3aa48-127">Шаг 2. Добавление необходимых компонентов в ваш каталог</span><span class="sxs-lookup"><span data-stu-id="3aa48-127">2: Add prerequisities to your directory</span></span>
<span data-ttu-id="3aa48-128">В окне командной строки замените каталоги, чтобы перейти к корневой папке, если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="3aa48-128">At a command prompt, change directories to go to your root folder, if you are not already there.</span></span> <span data-ttu-id="3aa48-129">Выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="3aa48-129">Run the following commands:</span></span>

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

<span data-ttu-id="3aa48-130">Кроме этого, в схему быстрого запуска мы включили `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="3aa48-130">In addition, we use `passport-azure-ad` in the skeleton of the quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="3aa48-131">Эта команда устанавливает библиотеки, используемые `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="3aa48-131">This installs the libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="3aa48-132">Шаг 3. Настройка в приложении использования стратегии Passport-Node.js</span><span class="sxs-lookup"><span data-stu-id="3aa48-132">3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="3aa48-133">Настройте промежуточный слой Express, чтобы использовать протокол проверки подлинности OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="3aa48-133">Set up the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="3aa48-134">Passport также будет использоваться для выдачи запросов входа и выхода, управления сеансом пользователя и получения сведений о пользователе.</span><span class="sxs-lookup"><span data-stu-id="3aa48-134">You use Passport to issue sign-in and sign-out requests, manage the user's session, and get information about the user, among other things.</span></span>

1.  <span data-ttu-id="3aa48-135">Откройте файл config.js в корневой папке проекта.</span><span class="sxs-lookup"><span data-stu-id="3aa48-135">In the root of the project, open the Config.js file.</span></span> <span data-ttu-id="3aa48-136">В разделе `exports.creds` введите значения конфигурации приложения.</span><span class="sxs-lookup"><span data-stu-id="3aa48-136">In the `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="3aa48-137">`clientID`: **идентификатор приложения**, который портал Azure назначил вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="3aa48-137">`clientID`: The **Application Id** that's assigned to your app in the Azure portal.</span></span>
  * <span data-ttu-id="3aa48-138">`returnURL`: **универсальный код ресурса (URI) перенаправления**, который вы указали на портале.</span><span class="sxs-lookup"><span data-stu-id="3aa48-138">`returnURL`: The **Redirect URI** that you entered in the portal.</span></span>
  * <span data-ttu-id="3aa48-139">`clientSecret`: секрет, созданный на портале.</span><span class="sxs-lookup"><span data-stu-id="3aa48-139">`clientSecret`: The secret that you generated in the portal.</span></span>

2.  <span data-ttu-id="3aa48-140">Откройте файл app.js в корневой папке проекта.</span><span class="sxs-lookup"><span data-stu-id="3aa48-140">In the root of the project, open the App.js file.</span></span> <span data-ttu-id="3aa48-141">Чтобы вызвать стратегию OIDCStrategy, поставляемую с `passport-azure-ad`, добавьте следующий вызов:</span><span class="sxs-lookup"><span data-stu-id="3aa48-141">To invoke the OIDCStrategy stratey, which comes with `passport-azure-ad`, add the following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="3aa48-142">Чтобы обработать запросы на вход, используйте указанную стратегию:</span><span class="sxs-lookup"><span data-stu-id="3aa48-142">To handle your sign-in requests, use the strategy you just referenced:</span></span>

  ```JavaScript
  // Use the OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. The function accepts
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

<span data-ttu-id="3aa48-143">Для Passport свойственно аналогичное поведение для всех стратегий (Twitter, Facebook и т. д.).</span><span class="sxs-lookup"><span data-stu-id="3aa48-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="3aa48-144">Все авторы стратегии придерживаются этого шаблона.</span><span class="sxs-lookup"><span data-stu-id="3aa48-144">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="3aa48-145">Передайте стратегию `function()`, которая использует маркер и значение `done` в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="3aa48-145">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="3aa48-146">Стратегия возвращается после того, как выполнит всю свою работу.</span><span class="sxs-lookup"><span data-stu-id="3aa48-146">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="3aa48-147">Сохраните данные пользователя и маркер, чтобы не задавать их в следующий раз повторно.</span><span class="sxs-lookup"><span data-stu-id="3aa48-147">Store the user and stash the token so you don’t need to ask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3aa48-148">Приведенный выше код принимает любого пользователя, который может пройти проверку подлинности на сервере.</span><span class="sxs-lookup"><span data-stu-id="3aa48-148">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="3aa48-149">Это называется автоматической регистрацией.</span><span class="sxs-lookup"><span data-stu-id="3aa48-149">This is known as auto-registration.</span></span> <span data-ttu-id="3aa48-150">На рабочих серверах не нужно разрешать другим пользователям выполнять операции входа без прохождения процесса регистрации, который вы сочтете приемлемым.</span><span class="sxs-lookup"><span data-stu-id="3aa48-150">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="3aa48-151">Это обычное поведение в приложениях для потребителей.</span><span class="sxs-lookup"><span data-stu-id="3aa48-151">This is usually the pattern that you see in consumer apps.</span></span> <span data-ttu-id="3aa48-152">Приложение можно зарегистрировать в Facebook, но потребуется ввести дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="3aa48-152">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="3aa48-153">Если в этом руководстве вы не использовали программу командной строки, сообщение электронной почты можно извлечь из возвращаемого объекта маркера.</span><span class="sxs-lookup"><span data-stu-id="3aa48-153">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="3aa48-154">Затем вы можете попросить пользователя ввести дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="3aa48-154">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="3aa48-155">Так как это всего лишь тестовый сервер, просто добавьте пользователей в базу данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="3aa48-155">Because this is a test server, you add the user directly to the in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="3aa48-156">Добавьте методы, которые позволяют отслеживать пользователей, выполнивших вход, в соответствии с требованиями Passport.</span><span class="sxs-lookup"><span data-stu-id="3aa48-156">Add the methods that you use to keep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="3aa48-157">Сюда относится сериализация и десериализация информации о пользователе:</span><span class="sxs-lookup"><span data-stu-id="3aa48-157">This includes serializing and deserializing the user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   To support persistent login sessions, Passport needs to be able to
  //   serialize users into, and deserialize users out of, the session. Typically,
  //   this is as simple as storing the user ID when serializing, and finding
  //   the user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array to hold signed-in users
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

5.  <span data-ttu-id="3aa48-158">Добавьте код для загрузки ядра Express.</span><span class="sxs-lookup"><span data-stu-id="3aa48-158">Add the code that loads the Express engine.</span></span> <span data-ttu-id="3aa48-159">Здесь мы используем шаблон по умолчанию /views и /routes, предоставляемый Express.</span><span class="sxs-lookup"><span data-stu-id="3aa48-159">You use the default /views and /routes pattern that Express provides:</span></span>

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
    // Initialize Passport!  Also use passport.session() middleware, to support
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="3aa48-160">Добавьте маршруты POST, которые будут передавать фактические запросы на вход в ядро `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="3aa48-160">Add the POST routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. The first step in OpenID authentication involves redirecting
  //   the user to the user's OpenID provider. After authenticating, the OpenID
  //   provider redirects the user back to this application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in the sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called.
  //   In this example, it redirects the user to the home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called. 
  //   In this example, it redirects the user to the home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="3aa48-161">Шаг 4. Использование Passport для выдачи запросов на вход и выход в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3aa48-161">4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="3aa48-162">Теперь приложение правильно настроено для взаимодействия с конечной точкой версии 2.0 с использованием протокола проверки подлинности OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="3aa48-162">Your app is now set up to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="3aa48-163">Стратегия `passport-azure-ad` берет на себя создание сообщений проверки подлинности, проверку маркеров из Azure AD и поддержку сеансов пользователя.</span><span class="sxs-lookup"><span data-stu-id="3aa48-163">The `passport-azure-ad` strategy takes care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining the user session.</span></span> <span data-ttu-id="3aa48-164">Осталось предоставить пользователям возможности входа и выхода, а также собрать дополнительную информацию о вошедших в систему пользователях.</span><span class="sxs-lookup"><span data-stu-id="3aa48-164">All that is left to do is to give your users a way to sign in and sign out, and to gather more information about the user who is signed in.</span></span>

1.  <span data-ttu-id="3aa48-165">Добавьте в файл app.js метод **по умолчанию**, а также методы **входа**, **учетной записи** и **выхода**.</span><span class="sxs-lookup"><span data-stu-id="3aa48-165">Add the **default**, **login**, **account**, and **logout** methods to your App.js file:</span></span>

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
      log.info('Login was called in the sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="3aa48-166">Дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="3aa48-166">Here are the details:</span></span>
    
    * <span data-ttu-id="3aa48-167">Маршрут `/` выполняет перенаправление в представление index.ejs.</span><span class="sxs-lookup"><span data-stu-id="3aa48-167">The `/` route redirects to the index.ejs view.</span></span> <span data-ttu-id="3aa48-168">Он передает сведения о пользователе в запросе (если он существует).</span><span class="sxs-lookup"><span data-stu-id="3aa48-168">It passes the user in the request (if it exists).</span></span>
    * <span data-ttu-id="3aa48-169">Маршрут `/account` сначала *позволяет пройти проверку подлинности* (реализация выполняется в примере кода ниже).</span><span class="sxs-lookup"><span data-stu-id="3aa48-169">The `/account` route first *ensures that you are authenticated* (you implement that in the following code).</span></span> <span data-ttu-id="3aa48-170">Затем он передает сведения о пользователе в запросе.</span><span class="sxs-lookup"><span data-stu-id="3aa48-170">Then, it passes the user in the request.</span></span> <span data-ttu-id="3aa48-171">Таким образом вы можете получить больше сведений о пользователе.</span><span class="sxs-lookup"><span data-stu-id="3aa48-171">This is so you can get more information about the user.</span></span>
    * <span data-ttu-id="3aa48-172">Маршрут `/login` вызывает структуру проверки подлинности `azuread-openidconnect` из `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="3aa48-172">The `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="3aa48-173">Если вызов завершается ошибкой, пользователь перенаправляется обратно на страницу `/login`.</span><span class="sxs-lookup"><span data-stu-id="3aa48-173">If that doesn't succeed, it redirects the user back to `/login`.</span></span>
    * <span data-ttu-id="3aa48-174">Маршрут `/logout` вызывает представление logout.ejs (и маршрут).</span><span class="sxs-lookup"><span data-stu-id="3aa48-174">The `/logout` route calls the logout.ejs view (and route).</span></span> <span data-ttu-id="3aa48-175">Это приводит к очистке файлов cookie, а затем он перенаправляет пользователя обратно к представлению index.ejs.</span><span class="sxs-lookup"><span data-stu-id="3aa48-175">This clears cookies, and then returns the user back to index.ejs.</span></span>

2.  <span data-ttu-id="3aa48-176">Добавьте метод **EnsureAuthenticated**, использованный ранее в `/account`:</span><span class="sxs-lookup"><span data-stu-id="3aa48-176">Add the **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware to ensure the user is authenticated (section 4)

  //   Use this route middleware on any resource that needs to be protected. If
  //   the request is authenticated (typically via a persistent login session),
  //   the request proceeds. Otherwise, the user is redirected to the
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="3aa48-177">В файле app.js создайте сервер:</span><span class="sxs-lookup"><span data-stu-id="3aa48-177">In App.js, create the server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-the-views-and-routes-in-express-that-you-show-your-user-on-the-website"></a><span data-ttu-id="3aa48-178">Шаг 5. Создание представлений и маршрутов в Express для отображения пользователя на веб-сайте</span><span class="sxs-lookup"><span data-stu-id="3aa48-178">5: Create the views and routes in Express that you show your user on the website</span></span>
<span data-ttu-id="3aa48-179">Добавьте маршруты и представления, отображающие сведения для пользователя.</span><span class="sxs-lookup"><span data-stu-id="3aa48-179">Add the routes and views that show information to the user.</span></span> <span data-ttu-id="3aa48-180">Маршруты и представления также обрабатывают созданные маршруты `/logout` и `/login`.</span><span class="sxs-lookup"><span data-stu-id="3aa48-180">The routes and views also handle the `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="3aa48-181">Создайте маршрут `/routes/index.js` в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="3aa48-181">In the root directory, create the `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="3aa48-182">Создайте маршрут `/routes/user.js` в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="3aa48-182">In the root directory, create the `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="3aa48-183">Маршруты `/routes/index.js` и `/routes/user.js` являются простыми маршрутами, которые передают запрос в представления, включая пользователя, если он существует.</span><span class="sxs-lookup"><span data-stu-id="3aa48-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along the request to your views, including the user, if present.</span></span>

3.  <span data-ttu-id="3aa48-184">Создайте представление `/views/index.ejs` в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="3aa48-184">In the root directory, create the `/views/index.ejs` view.</span></span> <span data-ttu-id="3aa48-185">Эта страница вызывает методы **входа** и **выхода**.</span><span class="sxs-lookup"><span data-stu-id="3aa48-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="3aa48-186">Вам также необходимо использовать представление `/views/index.ejs`, чтобы записать сведения об учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3aa48-186">You also use the `/views/index.ejs` view to capture account information.</span></span> <span data-ttu-id="3aa48-187">Вы можете использовать условное выражение `if (!user)`, так как сведения о пользователе, передаваемые в запросе,</span><span class="sxs-lookup"><span data-stu-id="3aa48-187">You can use the conditional `if (!user)` as the user being passed through in the request.</span></span> <span data-ttu-id="3aa48-188">свидетельствуют о том, что он вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="3aa48-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="3aa48-189">Создайте представление `/views/account.ejs` в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="3aa48-189">In the root directory, create the `/views/account.ejs` view.</span></span> <span data-ttu-id="3aa48-190">Представление `/views/account.ejs` позволяет просмотреть дополнительные сведения, которые `passport-azuread` помещает в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="3aa48-190">The `/views/account.ejs` view allows you to view additional information that `passport-azuread` puts in the user request.</span></span>

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

5.  <span data-ttu-id="3aa48-191">Добавьте макет.</span><span class="sxs-lookup"><span data-stu-id="3aa48-191">Add a layout.</span></span> <span data-ttu-id="3aa48-192">Создайте представление `/views/layout.ejs` в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="3aa48-192">In the root directory, create the `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="3aa48-193">Чтобы создать и запустить приложение, запустите `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="3aa48-193">To build and run your app, run `node app.js`.</span></span> <span data-ttu-id="3aa48-194">Затем перейдите сюда: `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="3aa48-194">Then, go to `http://localhost:3000`.</span></span>

7.  <span data-ttu-id="3aa48-195">Войдите с помощью личной учетной записи Майкрософт либо рабочей или учебной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3aa48-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="3aa48-196">Обратите внимание, что удостоверение пользователя отображается в списке /account.</span><span class="sxs-lookup"><span data-stu-id="3aa48-196">Note that the user's identity is reflected in the /account list.</span></span> 

<span data-ttu-id="3aa48-197">Теперь у вас есть веб-приложение, защищенное с помощью стандартных протоколов.</span><span class="sxs-lookup"><span data-stu-id="3aa48-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="3aa48-198">Вы можете выполнить проверку подлинности пользователей в приложении с помощью личных, рабочих или учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="3aa48-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3aa48-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3aa48-199">Next steps</span></span>
<span data-ttu-id="3aa48-200">Полный пример (без ваших значений конфигурации) можно загрузить в виде [ZIP-архива](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="3aa48-200">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="3aa48-201">Кроме того, его можно клонировать из GitHub:</span><span class="sxs-lookup"><span data-stu-id="3aa48-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="3aa48-202">Теперь можно перейти к более сложным темам.</span><span class="sxs-lookup"><span data-stu-id="3aa48-202">Next, you can move on to more advanced topics.</span></span> <span data-ttu-id="3aa48-203">Вы можете попробовать следующее:</span><span class="sxs-lookup"><span data-stu-id="3aa48-203">You might want to try:</span></span>

[<span data-ttu-id="3aa48-204">Защита веб-API с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="3aa48-204">Secure a Node.js web API by using the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="3aa48-205">Ниже приведены некоторые дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3aa48-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="3aa48-206">Вход для пользователей учетных записей Майкрософт и Azure AD в одном приложении</span><span class="sxs-lookup"><span data-stu-id="3aa48-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="3aa48-207">Тег StackOverflow "azure-active-directory"</span><span class="sxs-lookup"><span data-stu-id="3aa48-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="3aa48-208">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="3aa48-208">Get security updates for our products</span></span>
<span data-ttu-id="3aa48-209">Мы рекомендуем вам зарегистрироваться для получения уведомлений о нарушениях безопасности.</span><span class="sxs-lookup"><span data-stu-id="3aa48-209">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="3aa48-210">Это можно сделать, подписавшись на уведомления безопасности консультационных служб на странице [технического центра безопасности](https://technet.microsoft.com/security/dd252948).</span><span class="sxs-lookup"><span data-stu-id="3aa48-210">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

