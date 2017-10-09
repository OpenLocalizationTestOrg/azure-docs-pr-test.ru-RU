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
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="4a004-103">Вход в веб-приложение Node.js и выход из него с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a004-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="4a004-104">Мы выполним следующие действия с использованием Passport.</span><span class="sxs-lookup"><span data-stu-id="4a004-104">Here we use Passport to:</span></span>

* <span data-ttu-id="4a004-105">Знак hello пользователя в приложении toohello с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a004-105">Sign hello user in toohello app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="4a004-106">Отображение сведений о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-106">Display information about hello user.</span></span>
* <span data-ttu-id="4a004-107">Знак hello выход пользователя из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-107">Sign hello user out of hello app.</span></span>

<span data-ttu-id="4a004-108">Passport — это промежуточный слой аутентификации для Node.js.</span><span class="sxs-lookup"><span data-stu-id="4a004-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="4a004-109">Гибкая и модульной Passport плавно могут удаляться в tooany срочные или restify веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4a004-109">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or restify web application.</span></span> <span data-ttu-id="4a004-110">Он позволяет использовать разные стратегии с поддержкой аутентификации с помощью имени пользователя и пароля, учетных записей в Facebook и Twitter, и пр.</span><span class="sxs-lookup"><span data-stu-id="4a004-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="4a004-111">Мы разработали стратегию для Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a004-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="4a004-112">Мы установить этот модуль, а затем добавьте hello Microsoft Azure Active Directory `passport-azure-ad` подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="4a004-112">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="4a004-113">toodo, hello выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="4a004-113">toodo this, take hello following steps:</span></span>

1. <span data-ttu-id="4a004-114">зарегистрировать приложение;</span><span class="sxs-lookup"><span data-stu-id="4a004-114">Register an app.</span></span>
2. <span data-ttu-id="4a004-115">Настройка toouse вашего приложения hello `passport-azure-ad` стратегии.</span><span class="sxs-lookup"><span data-stu-id="4a004-115">Set up your app toouse hello `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="4a004-116">Используйте Passport tooissue входа и запросах на выход tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="4a004-116">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="4a004-117">Печать данных о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-117">Print data about hello user.</span></span>

<span data-ttu-id="4a004-118">поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="4a004-118">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="4a004-119">можно toofollow вдоль [загрузить приложение hello основу как ZIP-файл](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) или основу hello клона:</span><span class="sxs-lookup"><span data-stu-id="4a004-119">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="4a004-120">в конце hello этот учебник также предоставляется приложения Hello завершена.</span><span class="sxs-lookup"><span data-stu-id="4a004-120">hello completed application is provided at hello end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="4a004-121">Шаг 1. Регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="4a004-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="4a004-122">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4a004-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4a004-123">В меню hello hello верхней части страницы приветствия выберите свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="4a004-123">In hello menu at hello top of hello page, select your account.</span></span> <span data-ttu-id="4a004-124">В разделе hello **каталога** выберите hello клиента Active Directory, где требуется tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="4a004-124">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="4a004-125">Выберите **более служб** в hello меню hello влево сбоку экрана приветствия, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4a004-125">Select **More Services** in hello menu on hello left side of hello screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="4a004-126">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4a004-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="4a004-127">Выполните запросы toocreate hello **веб-приложение** и/или **WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="4a004-127">Follow hello prompts toocreate a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="4a004-128">Hello **имя** из hello приложения описывает toousers вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="4a004-128">hello **name** of hello application describes your application toousers.</span></span>

  * <span data-ttu-id="4a004-129">Hello **URL-адрес входа** hello базовый URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="4a004-129">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="4a004-130">Hello в схему по умолчанию — "http://localhost:3000, auth/openid/возвращаемое ''.</span><span class="sxs-lookup"><span data-stu-id="4a004-130">hello skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="4a004-131">Когда вы закончите регистрацию, Azure AD назначит приложению уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="4a004-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="4a004-132">Необходимо, чтобы это значение в hello следующие разделы, поэтому скопируйте его со страницы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-132">You need this value in hello following sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="4a004-133">Из hello **параметры** -> **свойства** страницы приложения, обновите URI идентификатора приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-133">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="4a004-134">Hello **URI идентификатора приложения** — это уникальный идентификатор для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="4a004-134">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="4a004-135">соглашение о Hello — формат hello toouse `https://<tenant-domain>/<app-name>`, например: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="4a004-135">hello convention is toouse hello format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-tooyour-directory"></a><span data-ttu-id="4a004-136">Шаг 2: Добавьте каталог tooyour предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4a004-136">Step 2: Add prerequisites tooyour directory</span></span>
1. <span data-ttu-id="4a004-137">Из командной строки hello, изменить каталоги tooyour корневую папку, если вы еще не существует, и затем выполнения hello следующие команды:</span><span class="sxs-lookup"><span data-stu-id="4a004-137">From hello command line, change directories tooyour root folder if you're not already there, and then run hello following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="4a004-138">Кроме того, вам потребуется `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="4a004-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="4a004-139">При этом устанавливаются библиотеки hello, `passport-azure-ad` зависит.</span><span class="sxs-lookup"><span data-stu-id="4a004-139">This installs hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="4a004-140">Шаг 3: Настройка стратегии приложения hello toouse passport узел js</span><span class="sxs-lookup"><span data-stu-id="4a004-140">Step 3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="4a004-141">Здесь мы настраиваем Express toouse hello OpenID Connect протокол проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4a004-141">Here, we configure Express toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="4a004-142">Passport — используется toodo различные действия, включая проблемы входа и выхода, управление сеансом пользователя hello и получения сведений о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-142">Passport is used toodo various things, including issue sign-in and sign-out requests, manage hello user's session, and get information about hello user.</span></span>

1. <span data-ttu-id="4a004-143">toobegin Привет открыть `config.js` файл в корне hello hello проекта, а затем введите значения конфигурации приложения в hello `exports.creds` раздела.</span><span class="sxs-lookup"><span data-stu-id="4a004-143">toobegin, open hello `config.js` file at hello root of hello project, and then enter your app's configuration values in hello `exports.creds` section.</span></span>

  * <span data-ttu-id="4a004-144">Hello `clientID` — hello **идентификатор приложения** , имеет назначенный tooyour приложения на портале регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-144">hello `clientID` is hello **Application Id** that's assigned tooyour app in hello registration portal.</span></span>

  * <span data-ttu-id="4a004-145">Hello `returnURL` — hello **Uri перенаправления** , введенное на портале hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-145">hello `returnURL` is hello **Redirect Uri** that you entered in hello portal.</span></span>

  * <span data-ttu-id="4a004-146">Hello `clientSecret` — hello секрет, который был создан в портале hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-146">hello `clientSecret` is hello secret that you generated in hello portal.</span></span>

2. <span data-ttu-id="4a004-147">Затем откройте hello `app.js` файл в корневой hello hello проекта.</span><span class="sxs-lookup"><span data-stu-id="4a004-147">Next, open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="4a004-148">Затем добавьте следующий вызов tooinvoke hello hello `OIDCStrategy` стратегии, входящий в состав `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="4a004-148">Then add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="4a004-149">После этого с помощью стратегии hello, мы просто ссылаться toohandle нашей запросов на вход в.</span><span class="sxs-lookup"><span data-stu-id="4a004-149">After that, use hello strategy we just referenced toohandle our sign-in requests.</span></span>

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
<span data-ttu-id="4a004-150">Для Passport свойственно аналогичное поведение для всех стратегий (Twitter, Facebook и т. д.); это поведение учитывают все разработчики модулей стратегий.</span><span class="sxs-lookup"><span data-stu-id="4a004-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="4a004-151">Глядя стратегии hello, видно, что мы передаем его функции, которая содержит маркер и выполняются как параметры hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-151">Looking at hello strategy, you see that we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="4a004-152">Стратегия Hello поставляется обратно toous после он выполняет свою работу.</span><span class="sxs-lookup"><span data-stu-id="4a004-152">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="4a004-153">Затем мы хотим toostore hello пользователя и маркер hello образа, поэтому нам не нужен tooask его еще раз.</span><span class="sxs-lookup"><span data-stu-id="4a004-153">Then we want toostore hello user and stash hello token so we don't need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="4a004-154">Предыдущий код Hello принимает любой пользователь, который происходит tooauthenticate tooour сервера.</span><span class="sxs-lookup"><span data-stu-id="4a004-154">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="4a004-155">Это называется автоматической регистрацией.</span><span class="sxs-lookup"><span data-stu-id="4a004-155">This is known as auto-registration.</span></span> <span data-ttu-id="4a004-156">Рекомендуется, чтобы не дать любой пользователь проверку подлинности tooa рабочего сервера без необходимости их регистрации через процесс выбора.</span><span class="sxs-lookup"><span data-stu-id="4a004-156">We    recommend that you don't let anyone authenticate tooa production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="4a004-157">Обычно это является шаблон hello в потребительские приложения, которые позволяет tooregister с Facebook, а затем попросите tooprovide дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="4a004-157">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you tooprovide additional information.</span></span> <span data-ttu-id="4a004-158">Если это не были образец приложения, мы удалось извлекли адрес электронной почты пользователя hello из hello токен объекта, который возвращается и затем предложено hello toofill пользователя дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="4a004-158">If this weren't a sample application, we could have extracted hello user's email address from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="4a004-159">Так как на тестовом сервере, мы их добавить toohello базы данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="4a004-159">Because this is a test server, we add them toohello in-memory database.</span></span>


4. <span data-ttu-id="4a004-160">Далее добавим hello методы, позволяющие определить tootrack hello вошедших пользователей, необходимые службы Passport.</span><span class="sxs-lookup"><span data-stu-id="4a004-160">Next, let's add hello methods that enable us tootrack hello signed-in users as required by Passport.</span></span> <span data-ttu-id="4a004-161">Эти методы включают сериализацию и десериализацию сведений о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-161">These methods include serializing and deserializing hello user's information.</span></span>

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

5.  <span data-ttu-id="4a004-162">Далее добавим механизм Express hello tooload кода hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-162">Next, let's add hello code tooload hello Express engine.</span></span> <span data-ttu-id="4a004-163">Здесь мы используем /views по умолчанию hello и предоставляет шаблон /routes, Express.</span><span class="sxs-lookup"><span data-stu-id="4a004-163">Here we use hello default /views and /routes pattern that Express provides.</span></span>

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

6. <span data-ttu-id="4a004-164">Наконец, добавим hello направляет, передайте hello фактических запросов toohello `passport-azure-ad` ядра:</span><span class="sxs-lookup"><span data-stu-id="4a004-164">Finally, let's add hello routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>


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


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="4a004-165">Шаг 4: Используйте Passport tooissue входа и запросах на выход tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="4a004-165">Step 4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="4a004-166">Приложение теперь будет правильно настроен toocommunicate с конечной точкой hello с помощью протокола проверки подлинности OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-166">Your app is now properly configured toocommunicate with hello endpoint by using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="4a004-167">`passport-azure-ad`Разобравшись все параметры hello отправляемого сообщения проверки подлинности, проверки токенов из Azure AD и поддержку пользовательских сеансов.</span><span class="sxs-lookup"><span data-stu-id="4a004-167">`passport-azure-ad` has taken care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="4a004-168">Все, что остается предоставление пользователям способ toosign в и выхода, а сбор дополнительных сведений о hello вошедших пользователей.</span><span class="sxs-lookup"><span data-stu-id="4a004-168">All that remains is giving your users a way toosign in and sign out, and gathering additional information about hello signed-in users.</span></span>

1. <span data-ttu-id="4a004-169">Во-первых давайте добавим по умолчанию hello, вход, учетной записи и выхода методов tooour `app.js` файла:</span><span class="sxs-lookup"><span data-stu-id="4a004-169">First, let's add hello default, sign-in, account, and sign-out methods tooour `app.js` file:</span></span>

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

2.  <span data-ttu-id="4a004-170">Рассмотрим это подробно.</span><span class="sxs-lookup"><span data-stu-id="4a004-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="4a004-171">Hello `/`маршрута перенаправляет toohello index.ejs представлении, передавая hello пользователя в запросе hello, (если он существует).</span><span class="sxs-lookup"><span data-stu-id="4a004-171">hello `/`route redirects toohello index.ejs view, passing hello user in hello request (if it exists).</span></span>
  * <span data-ttu-id="4a004-172">Hello `/account` сначала *гарантирует, проходят проверку* (Мы реализовали, в следующий пример hello), а затем передает hello пользователя в запросе hello, чтобы мы могли получить дополнительные сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-172">hello `/account` route first *ensures we are authenticated* (we implement that in hello following example), and then passes hello user in hello request so that we can get additional information about hello user.</span></span>
  * <span data-ttu-id="4a004-173">Hello `/login` маршрут вызывает наши средства проверки подлинности azuread openidconnect из `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="4a004-173">hello `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="4a004-174">Если, не удается, он перенаправляет hello назад слишком или имя входа пользователя.</span><span class="sxs-lookup"><span data-stu-id="4a004-174">If that doesn't succeed, it redirects hello user back too/login.</span></span>
  * <span data-ttu-id="4a004-175">Hello `/logout` маршрута просто вызывает hello logout.ejs и маршрута, какие файлы cookie очищает, а затем возвращает hello задней tooindex.ejs пользователя.</span><span class="sxs-lookup"><span data-stu-id="4a004-175">hello `/logout` route simply calls hello logout.ejs (and route), which clears cookies and then returns hello user back tooindex.ejs.</span></span>

3. <span data-ttu-id="4a004-176">Для hello последнюю часть `app.js`, добавим hello **EnsureAuthenticated** метод, используемый в `/account`, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="4a004-176">For hello last part of `app.js`, let's add hello **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

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

4. <span data-ttu-id="4a004-177">Наконец, давайте создадим сам сервер hello в `app.js`:</span><span class="sxs-lookup"><span data-stu-id="4a004-177">Finally, let's create hello server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a><span data-ttu-id="4a004-178">Шаг 5: toodisplay нашей пользователя на веб-сайте hello, создание представления hello и маршруты в экспресс-выпуск</span><span class="sxs-lookup"><span data-stu-id="4a004-178">Step 5: toodisplay our user in hello website, create hello views and routes in Express</span></span>
<span data-ttu-id="4a004-179">Теперь файл `app.js` готов.</span><span class="sxs-lookup"><span data-stu-id="4a004-179">Now `app.js` is complete.</span></span> <span data-ttu-id="4a004-180">Мы просто необходимые маршруты tooadd hello и представления отображаются сведения hello мы получить toohello пользователя, а также обрабатывать hello `/logout` и `/login` маршрутов, которая была создана.</span><span class="sxs-lookup"><span data-stu-id="4a004-180">We simply need tooadd hello routes and views that show hello information we get toohello user, as well as handle hello `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="4a004-181">Создать hello `/routes/index.js` маршрута в корневом каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-181">Create hello `/routes/index.js` route under hello root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="4a004-182">Создать hello `/routes/user.js` маршрута в корневом каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-182">Create hello `/routes/user.js` route under hello root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="4a004-183">Они передают представлений tooour hello запросов, включая hello пользователя при его наличии.</span><span class="sxs-lookup"><span data-stu-id="4a004-183">These pass along hello request tooour views, including hello user if present.</span></span>

3. <span data-ttu-id="4a004-184">Создать hello `/views/index.ejs` представления в корневом каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-184">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="4a004-185">Это простой страницы, который вызывает методы нашей входа и выхода из системы и позволяет нам toograb сведения об учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4a004-185">This is a simple page that calls our login and logout methods and enables us toograb account information.</span></span> <span data-ttu-id="4a004-186">Обратите внимание, что мы используем hello условного `if (!user)` как свидетельство у нас есть пользователя, выполнившего вход пользователя hello, передаваемых через запрос hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-186">Notice that we can use hello conditional `if (!user)` as hello user being passed through in hello request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="4a004-187">Создать hello `/views/account.ejs` просмотра в корневом каталоге hello, чтобы мы могли просматривать дополнительные сведения, `passport-azuread` приостановил в запросе пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="4a004-187">Create hello `/views/account.ejs` view under hello root directory so that we can view additional information that `passport-azuread` has put in hello user request.</span></span>

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

5. <span data-ttu-id="4a004-188">Теперь давайте все красиво оформим, добавив макет.</span><span class="sxs-lookup"><span data-stu-id="4a004-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="4a004-189">Создать hello "/ views/layout.ejs" в разделе "hello корневой каталог.</span><span class="sxs-lookup"><span data-stu-id="4a004-189">Create hello '/views/layout.ejs' view under hello root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="4a004-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4a004-190">Next steps</span></span>
<span data-ttu-id="4a004-191">Наконец, создайте и запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="4a004-191">Finally, build and run your app.</span></span> <span data-ttu-id="4a004-192">Запустите `node app.js`, а затем перейдите слишком`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="4a004-192">Run `node app.js`, and then go too`http://localhost:3000`.</span></span>

<span data-ttu-id="4a004-193">Войдите, используя личную учетную запись Майкрософт или рабочую учетную запись и обратите внимание на то, как удостоверение пользователя hello отражается в списке hello/Account.</span><span class="sxs-lookup"><span data-stu-id="4a004-193">Sign in with either a personal Microsoft account or a work or school account, and notice how hello user's identity is reflected in hello /account list.</span></span> <span data-ttu-id="4a004-194">Теперь у вас есть веб-приложение, защищенное с помощью стандартных отраслевых протоколов, которое может выполнять аутентификацию пользователей с использованием личных, рабочих и учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="4a004-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="4a004-195">Справочник по hello выполнить пример (без настройки) [предоставляется как ZIP-файл](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="4a004-195">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="4a004-196">Вы также можете клонировать его из репозитория GitHub:</span><span class="sxs-lookup"><span data-stu-id="4a004-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="4a004-197">Теперь можно перейти к более сложным темам.</span><span class="sxs-lookup"><span data-stu-id="4a004-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="4a004-198">Может потребоваться tootry:</span><span class="sxs-lookup"><span data-stu-id="4a004-198">You might want tootry:</span></span>

[<span data-ttu-id="4a004-199">Приступая к работе с веб-интерфейсом API для узла</span><span class="sxs-lookup"><span data-stu-id="4a004-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
