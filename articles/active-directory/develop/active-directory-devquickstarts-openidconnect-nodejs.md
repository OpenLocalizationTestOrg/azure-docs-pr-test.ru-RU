---
title: "Приступая к работе со входом и выходом в Azure AD с помощью Node.js | Документация Майкрософт"
description: "Узнайте, как создать веб-приложение Node.js Express MVC, которое интегрируется с Azure AD для входа."
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
ms.openlocfilehash: 13317b016f9ff3955f376b858645c42668b0de42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="fbe01-103">Вход в веб-приложение Node.js и выход из него с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbe01-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="fbe01-104">Мы выполним следующие действия с использованием Passport.</span><span class="sxs-lookup"><span data-stu-id="fbe01-104">Here we use Passport to:</span></span>

* <span data-ttu-id="fbe01-105">Вход пользователя в приложение с помощью Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbe01-105">Sign the user in to the app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="fbe01-106">Отображение информации о пользователе.</span><span class="sxs-lookup"><span data-stu-id="fbe01-106">Display information about the user.</span></span>
* <span data-ttu-id="fbe01-107">Выход пользователя из приложения.</span><span class="sxs-lookup"><span data-stu-id="fbe01-107">Sign the user out of the app.</span></span>

<span data-ttu-id="fbe01-108">Passport — это промежуточный слой аутентификации для Node.js.</span><span class="sxs-lookup"><span data-stu-id="fbe01-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="fbe01-109">Он отличается гибкой модульной структурой, которая позволяет сравнительно незаметно размещать его в любом приложении на основе Express или веб-приложении Restify.</span><span class="sxs-lookup"><span data-stu-id="fbe01-109">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or restify web application.</span></span> <span data-ttu-id="fbe01-110">Он позволяет использовать разные стратегии с поддержкой аутентификации с помощью имени пользователя и пароля, учетных записей в Facebook и Twitter, и пр.</span><span class="sxs-lookup"><span data-stu-id="fbe01-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="fbe01-111">Мы разработали стратегию для Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fbe01-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="fbe01-112">Теперь мы установим этот модуль и добавим подключаемый модуль Microsoft Azure Active Directory `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="fbe01-112">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="fbe01-113">Для этого вам нужно:</span><span class="sxs-lookup"><span data-stu-id="fbe01-113">To do this, take the following steps:</span></span>

1. <span data-ttu-id="fbe01-114">зарегистрировать приложение;</span><span class="sxs-lookup"><span data-stu-id="fbe01-114">Register an app.</span></span>
2. <span data-ttu-id="fbe01-115">настроить в нем использование стратегии `passport-azure-ad`;</span><span class="sxs-lookup"><span data-stu-id="fbe01-115">Set up your app to use the `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="fbe01-116">использовать Passport для выдачи запросов на вход и выход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbe01-116">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="fbe01-117">вывести данные о пользователе.</span><span class="sxs-lookup"><span data-stu-id="fbe01-117">Print data about the user.</span></span>

<span data-ttu-id="fbe01-118">Код в этом учебнике размещен на портале [GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="fbe01-118">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="fbe01-119">Вы можете [скачать заготовку приложения как ZIP-файл](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) или клонировать структуру:</span><span class="sxs-lookup"><span data-stu-id="fbe01-119">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="fbe01-120">Готовое приложение также приводится в конце этого руководства.</span><span class="sxs-lookup"><span data-stu-id="fbe01-120">The completed application is provided at the end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="fbe01-121">Шаг 1. Регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="fbe01-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="fbe01-122">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fbe01-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="fbe01-123">В меню в верхней части страницы выберите учетную запись.</span><span class="sxs-lookup"><span data-stu-id="fbe01-123">In the menu at the top of the page, select your account.</span></span> <span data-ttu-id="fbe01-124">В списке **Каталог** выберите клиент Active Directory для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="fbe01-124">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="fbe01-125">Выберите **Больше служб** в меню в левой части экрана, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbe01-125">Select **More Services** in the menu on the left side of the screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="fbe01-126">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fbe01-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="fbe01-127">Следуйте инструкциям на экране, чтобы создать новое **веб-приложение** и (или) **веб-интерфейс API**.</span><span class="sxs-lookup"><span data-stu-id="fbe01-127">Follow the prompts to create a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="fbe01-128">**Имя** приложения является его описанием для пользователей.</span><span class="sxs-lookup"><span data-stu-id="fbe01-128">The **name** of the application describes your application to users.</span></span>

  * <span data-ttu-id="fbe01-129">**URL-адрес входа** — это базовый URL-адрес вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="fbe01-129">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="fbe01-130">Схема по умолчанию — `http://localhost:3000/auth/openid/return`\`.</span><span class="sxs-lookup"><span data-stu-id="fbe01-130">The skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="fbe01-131">Когда вы закончите регистрацию, Azure AD назначит приложению уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="fbe01-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="fbe01-132">Это значение вам понадобится в следующих разделах, поэтому обязательно скопируйте его на странице приложения.</span><span class="sxs-lookup"><span data-stu-id="fbe01-132">You need this value in the following sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="fbe01-133">На странице **Параметры** -> **Свойства** приложения обновите его универсальный код ресурса (URI) идентификатора.</span><span class="sxs-lookup"><span data-stu-id="fbe01-133">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="fbe01-134">**URI идентификатора приложения** — это уникальный идентификатор вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="fbe01-134">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="fbe01-135">Существует негласная договоренность использовать формат `https://<tenant-domain>/<app-name>`, например: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="fbe01-135">The convention is to use the format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-to-your-directory"></a><span data-ttu-id="fbe01-136">Шаг 2. Добавление предварительных требований в каталог</span><span class="sxs-lookup"><span data-stu-id="fbe01-136">Step 2: Add prerequisites to your directory</span></span>
1. <span data-ttu-id="fbe01-137">В командной строке перейдите в корневую папку (если вы еще не там) и выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="fbe01-137">From the command line, change directories to your root folder if you're not already there, and then run the following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="fbe01-138">Кроме того, вам потребуется `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="fbe01-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="fbe01-139">Эта команда устанавливает библиотеки, от которых зависит `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="fbe01-139">This installs the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="fbe01-140">Шаг 3. Настройка приложения для использования стратегии passport-node-js</span><span class="sxs-lookup"><span data-stu-id="fbe01-140">Step 3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="fbe01-141">Здесь мы настроим Express для использования протокола аутентификации OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="fbe01-141">Here, we configure Express to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="fbe01-142">Passport позволяет выполнять разные действия, в том числе выдавать запросы на вход и выход, управлять сеансами пользователя и получать сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="fbe01-142">Passport is used to do various things, including issue sign-in and sign-out requests, manage the user's session, and get information about the user.</span></span>

1. <span data-ttu-id="fbe01-143">Сначала откройте файл `config.js` из корневого каталога проекта, а затем укажите параметры конфигурации приложения в разделе `exports.creds`.</span><span class="sxs-lookup"><span data-stu-id="fbe01-143">To begin, open the `config.js` file at the root of the project, and then enter your app's configuration values in the `exports.creds` section.</span></span>

  * <span data-ttu-id="fbe01-144">`clientID` — это **идентификатор приложения**, присвоенный приложению на портале регистрации.</span><span class="sxs-lookup"><span data-stu-id="fbe01-144">The `clientID` is the **Application Id** that's assigned to your app in the registration portal.</span></span>

  * <span data-ttu-id="fbe01-145">`returnURL` — это **универсальный код ресурса (URI) перенаправления**, который вы указали на портале.</span><span class="sxs-lookup"><span data-stu-id="fbe01-145">The `returnURL` is the **Redirect Uri** that you entered in the portal.</span></span>

  * <span data-ttu-id="fbe01-146">`clientSecret` — это секрет, созданный на портале.</span><span class="sxs-lookup"><span data-stu-id="fbe01-146">The `clientSecret` is the secret that you generated in the portal.</span></span>

2. <span data-ttu-id="fbe01-147">Теперь откройте файл `app.js` в корневой папке проекта.</span><span class="sxs-lookup"><span data-stu-id="fbe01-147">Next, open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="fbe01-148">Добавьте следующий вызов, чтобы использовать стратегию `OIDCStrategy`, которая предоставляется с `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="fbe01-148">Then add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="fbe01-149">Теперь вы можете использовать стратегию, на которую мы только что сослались, чтобы обрабатывать запросы на вход.</span><span class="sxs-lookup"><span data-stu-id="fbe01-149">After that, use the strategy we just referenced to handle our sign-in requests.</span></span>

    ```JavaScript
    // Use the OIDCStrategy within Passport. (Section 2)
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
<span data-ttu-id="fbe01-150">Для Passport свойственно аналогичное поведение для всех стратегий (Twitter, Facebook и т. д.); это поведение учитывают все разработчики модулей стратегий.</span><span class="sxs-lookup"><span data-stu-id="fbe01-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="fbe01-151">В коде стратегии видно, что мы передаем ей функцию с параметрами token и done.</span><span class="sxs-lookup"><span data-stu-id="fbe01-151">Looking at the strategy, you see that we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="fbe01-152">Стратегия будет возвращена, когда завершит свою работу.</span><span class="sxs-lookup"><span data-stu-id="fbe01-152">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="fbe01-153">Теперь нам нужно сохранить пользователя и обработать маркер, чтобы не запрашивать его повторно.</span><span class="sxs-lookup"><span data-stu-id="fbe01-153">Then we want to store the user and stash the token so we don't need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="fbe01-154">Приведенный выше код обрабатывает данные о любом пользователе, который выполняет аутентификацию на сервере.</span><span class="sxs-lookup"><span data-stu-id="fbe01-154">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="fbe01-155">Это называется автоматической регистрацией.</span><span class="sxs-lookup"><span data-stu-id="fbe01-155">This is known as auto-registration.</span></span> <span data-ttu-id="fbe01-156">На рабочих серверах мы не рекомендуем разрешать аутентификацию без прохождения определенного процесса регистрации, который вы сочтете приемлемым.</span><span class="sxs-lookup"><span data-stu-id="fbe01-156">We    recommend that you don't let anyone authenticate to a production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="fbe01-157">Это типично для клиентских приложений, в которых разрешается регистрация через Facebook, но затем следуют запросы на предоставление дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="fbe01-157">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to provide additional information.</span></span> <span data-ttu-id="fbe01-158">Если бы это не был пример приложения, мы могли бы извлечь электронный адрес пользователя из возвращенного объекта маркера и затем запросить у пользователя дополнительную информацию.</span><span class="sxs-lookup"><span data-stu-id="fbe01-158">If this weren't a sample application, we could have extracted the user's email address from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="fbe01-159">Так как это всего лишь тестовый сервер, мы добавим пользователей в базу данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="fbe01-159">Because this is a test server, we add them to the in-memory database.</span></span>


4. <span data-ttu-id="fbe01-160">Далее мы добавим методы, которые позволят отслеживать вошедших пользователей, как того требует Passport.</span><span class="sxs-lookup"><span data-stu-id="fbe01-160">Next, let's add the methods that enable us to track the signed-in users as required by Passport.</span></span> <span data-ttu-id="fbe01-161">Сюда входят методы сериализации и десериализации информации о пользователе.</span><span class="sxs-lookup"><span data-stu-id="fbe01-161">These methods include serializing and deserializing the user's information.</span></span>

    ```JavaScript

            // Passport session setup. (Section 2)

            //   To support persistent sign-in sessions, Passport needs to be able to
            //   serialize users into the session and deserialize them out of the session. Typically,
            //   this is done simply by storing the user ID when serializing and finding
            //   the user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array to hold signed-in users
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

5.  <span data-ttu-id="fbe01-162">Далее добавим код для загрузки подсистемы Express.</span><span class="sxs-lookup"><span data-stu-id="fbe01-162">Next, let's add the code to load the Express engine.</span></span> <span data-ttu-id="fbe01-163">Здесь мы используем шаблон по умолчанию /views и /routes, предоставляемый Express.</span><span class="sxs-lookup"><span data-stu-id="fbe01-163">Here we use the default /views and /routes pattern that Express provides.</span></span>

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
          // Initialize Passport!  Also use passport.session() middleware, to support
          // persistent login sessions (recommended).
          app.use(passport.initialize());
          app.use(passport.session());
          app.use(app.router);
          app.use(express.static(__dirname + '/../../public'));
        });

    ```

6. <span data-ttu-id="fbe01-164">Наконец, добавьте маршруты, которые будут передавать фактические запросы на вход, в подсистему `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="fbe01-164">Finally, let's add the routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware to authenticate the
        //   request. The first step in OpenID authentication involves redirecting
        //   the user to their OpenID provider. After authenticating, the OpenID
        //   provider redirects the user back to this application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in the Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="fbe01-165">Шаг 4. Использование Passport для выдачи запросов на вход и выход в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbe01-165">Step 4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="fbe01-166">Теперь приложение правильно настроено для взаимодействия с конечной точкой с использованием протокола проверки подлинности OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="fbe01-166">Your app is now properly configured to communicate with the endpoint by using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="fbe01-167">`passport-azure-ad` берет на себя создание сообщений проверки подлинности, проверку токенов из Azure AD и поддержку сеансов пользователя.</span><span class="sxs-lookup"><span data-stu-id="fbe01-167">`passport-azure-ad` has taken care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="fbe01-168">Осталось предоставить пользователям возможности входа и выхода, а также собрать дополнительную информацию о вошедших в систему пользователях.</span><span class="sxs-lookup"><span data-stu-id="fbe01-168">All that remains is giving your users a way to sign in and sign out, and gathering additional information about the signed-in users.</span></span>

1. <span data-ttu-id="fbe01-169">Сначала нужно добавить в файл `app.js` метод по умолчанию, а также методы входа, учетной записи и выхода.</span><span class="sxs-lookup"><span data-stu-id="fbe01-169">First, let's add the default, sign-in, account, and sign-out methods to our `app.js` file:</span></span>

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
            log.info('Login was called in the Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  <span data-ttu-id="fbe01-170">Рассмотрим это подробно.</span><span class="sxs-lookup"><span data-stu-id="fbe01-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="fbe01-171">Маршрут `/` выполняет перенаправление в представление index.ejs, передавая пользователя в запросе (если он существует).</span><span class="sxs-lookup"><span data-stu-id="fbe01-171">The `/`route redirects to the index.ejs view, passing the user in the request (if it exists).</span></span>
  * <span data-ttu-id="fbe01-172">Маршрут `/account` сначала *проверяет, выполнена ли аутентификация* (это мы реализуем в следующем примере), а затем передает пользователя в запросе. Так мы можем получить дополнительные сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="fbe01-172">The `/account` route first *ensures we are authenticated* (we implement that in the following example), and then passes the user in the request so that we can get additional information about the user.</span></span>
  * <span data-ttu-id="fbe01-173">Маршрут `/login` вызывает наше средство аутентификации azuread-openidconnect из `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="fbe01-173">The `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="fbe01-174">Если вызов завершается ошибкой, пользователь перенаправляется обратно на страницу /login.</span><span class="sxs-lookup"><span data-stu-id="fbe01-174">If that doesn't succeed, it redirects the user back to /login.</span></span>
  * <span data-ttu-id="fbe01-175">Маршрут `/logout` просто вызывает logout.ejs (и соответствующий маршрут), который очищает файлы cookie и возвращает пользователя к index.ejs.</span><span class="sxs-lookup"><span data-stu-id="fbe01-175">The `/logout` route simply calls the logout.ejs (and route), which clears cookies and then returns the user back to index.ejs.</span></span>

3. <span data-ttu-id="fbe01-176">В конец файла `app.js` мы добавляем метод **EnsureAuthenticated**, который используется в `/account`, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="fbe01-176">For the last part of `app.js`, let's add the **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

    ```JavaScript

        // Simple route middleware to ensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs to be protected. If
        //   the request is authenticated (typically via a persistent sign-in session),
        //   the request proceeds. Otherwise, the user is redirected to the
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. <span data-ttu-id="fbe01-177">Наконец, давайте создадим сам сервер в `app.js`.</span><span class="sxs-lookup"><span data-stu-id="fbe01-177">Finally, let's create the server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-to-display-our-user-in-the-website-create-the-views-and-routes-in-express"></a><span data-ttu-id="fbe01-178">Шаг 5. Создание представлений и маршрутов в Express для отображения пользователя на веб-сайте</span><span class="sxs-lookup"><span data-stu-id="fbe01-178">Step 5: To display our user in the website, create the views and routes in Express</span></span>
<span data-ttu-id="fbe01-179">Теперь файл `app.js` готов.</span><span class="sxs-lookup"><span data-stu-id="fbe01-179">Now `app.js` is complete.</span></span> <span data-ttu-id="fbe01-180">Нам осталось только добавить маршруты и представления, которые отобразят для пользователя получаемую информацию, а также обработают созданные нами маршруты `/logout` и `/login`.</span><span class="sxs-lookup"><span data-stu-id="fbe01-180">We simply need to add the routes and views that show the information we get to the user, as well as handle the `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="fbe01-181">Создайте маршрут `/routes/index.js` в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="fbe01-181">Create the `/routes/index.js` route under the root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="fbe01-182">Создайте маршрут `/routes/user.js` в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="fbe01-182">Create the `/routes/user.js` route under the root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="fbe01-183">Эти маршруты передают запрос в наши представления, включая пользователя, если он имеется.</span><span class="sxs-lookup"><span data-stu-id="fbe01-183">These pass along the request to our views, including the user if present.</span></span>

3. <span data-ttu-id="fbe01-184">Создайте представление `/views/index.ejs` в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="fbe01-184">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="fbe01-185">Это простая страница, которая вызывает наши методы входа и выхода и позволяет получить информацию об учетной записи.</span><span class="sxs-lookup"><span data-stu-id="fbe01-185">This is a simple page that calls our login and logout methods and enables us to grab account information.</span></span> <span data-ttu-id="fbe01-186">Обратите внимание, что вы можете использовать условное выражение `if (!user)`, так как сведения о пользователе, передаваемые в запросе, свидетельствуют о том, что в систему вошел пользователь.</span><span class="sxs-lookup"><span data-stu-id="fbe01-186">Notice that we can use the conditional `if (!user)` as the user being passed through in the request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="fbe01-187">Создайте представление `/views/account.ejs` в корневом каталоге, чтобы мы могли просматривать дополнительную информацию, помещенную `passport-azuread` в запрос пользователя.</span><span class="sxs-lookup"><span data-stu-id="fbe01-187">Create the `/views/account.ejs` view under the root directory so that we can view additional information that `passport-azuread` has put in the user request.</span></span>

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

5. <span data-ttu-id="fbe01-188">Теперь давайте все красиво оформим, добавив макет.</span><span class="sxs-lookup"><span data-stu-id="fbe01-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="fbe01-189">Создайте представление /views/layout.ejs в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="fbe01-189">Create the '/views/layout.ejs' view under the root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="fbe01-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fbe01-190">Next steps</span></span>
<span data-ttu-id="fbe01-191">Наконец, создайте и запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="fbe01-191">Finally, build and run your app.</span></span> <span data-ttu-id="fbe01-192">Выполните `node app.js` и откройте в браузере страницу `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="fbe01-192">Run `node app.js`, and then go to `http://localhost:3000`.</span></span>

<span data-ttu-id="fbe01-193">Выполните вход с личной, рабочей или учебной учетной записью Майкрософт. Проверьте, как удостоверение пользователя отображается в списке /account.</span><span class="sxs-lookup"><span data-stu-id="fbe01-193">Sign in with either a personal Microsoft account or a work or school account, and notice how the user's identity is reflected in the /account list.</span></span> <span data-ttu-id="fbe01-194">Теперь у вас есть веб-приложение, защищенное с помощью стандартных отраслевых протоколов, которое может выполнять аутентификацию пользователей с использованием личных, рабочих и учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="fbe01-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="fbe01-195">Полный пример (без ваших значений конфигурации) можно загрузить в виде [ZIP-архива](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="fbe01-195">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="fbe01-196">Вы также можете клонировать его из репозитория GitHub:</span><span class="sxs-lookup"><span data-stu-id="fbe01-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="fbe01-197">Теперь можно перейти к более сложным темам.</span><span class="sxs-lookup"><span data-stu-id="fbe01-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="fbe01-198">Вы можете попробовать следующее:</span><span class="sxs-lookup"><span data-stu-id="fbe01-198">You might want to try:</span></span>

[<span data-ttu-id="fbe01-199">Приступая к работе с веб-интерфейсом API для узла</span><span class="sxs-lookup"><span data-stu-id="fbe01-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
