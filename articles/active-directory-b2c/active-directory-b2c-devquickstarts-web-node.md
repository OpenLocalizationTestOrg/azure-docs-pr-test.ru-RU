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
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="9b0ee-103">Azure AD B2C: Добавление веб-приложение Node.js tooa входа</span><span class="sxs-lookup"><span data-stu-id="9b0ee-103">Azure AD B2C: Add sign-in tooa Node.js web app</span></span>

<span data-ttu-id="9b0ee-104">**Passport** — промежуточный слой проверки подлинности для Node.js.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="9b0ee-105">Гибкая модульная структура Passport позволяет незаметно устанавливать его в любом приложении на основе Express или в веб-приложении Restify.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="9b0ee-106">Полный набор стратегий поддерживает проверку подлинности с помощью имени пользователя и пароля, Facebook, Twitter и других средств.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="9b0ee-107">Мы разработали стратегию для Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b0ee-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="9b0ee-108">Будет установлено этот модуль и затем добавить hello Azure AD `passport-azure-ad` подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-108">You will install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="9b0ee-109">toodo это, необходимо:</span><span class="sxs-lookup"><span data-stu-id="9b0ee-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="9b0ee-110">Зарегистрировать приложение с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="9b0ee-111">Настройка toouse вашего приложения hello `passport-azure-ad` подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-111">Set up your app toouse hello `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="9b0ee-112">Используйте Passport tooissue входа и запросах на выход tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-112">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="9b0ee-113">Ввести данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-113">Print user data.</span></span>

<span data-ttu-id="9b0ee-114">Здравствуйте, код для этого учебника [сохраняется на сайте GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="9b0ee-114">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="9b0ee-115">можно toofollow вдоль [загрузить приложение hello основу как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="9b0ee-115">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="9b0ee-116">Также можно клонировать основу hello:</span><span class="sxs-lookup"><span data-stu-id="9b0ee-116">You can also clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="9b0ee-117">в конце этого учебника в hello предоставляется приложения Hello завершена.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-117">hello completed application is provided at hello end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="9b0ee-118">Создание каталога Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="9b0ee-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="9b0ee-119">Перед использованием Azure AD B2C необходимо создать каталог или клиент.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="9b0ee-120">Каталог — это контейнер для данных всех ваших пользователей, приложений, групп и т. д.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="9b0ee-121">Прежде чем продолжать работу с руководством, [создайте каталог B2C](active-directory-b2c-get-started.md), если вы его еще не создали.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="9b0ee-122">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="9b0ee-122">Create an application</span></span>

<span data-ttu-id="9b0ee-123">Далее необходимо toocreate приложения в каталоге B2C.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-123">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="9b0ee-124">Это предоставляет сведения Azure AD, что ему требуется toocommunicate безопасно вместе с приложением.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-124">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="9b0ee-125">Оба hello клиентского приложения и веб-API, будет представлен один **идентификатор приложения**, так как они включают в себя один логический приложения.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-125">Both hello client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="9b0ee-126">toocreate приложения, выполните [эти инструкции](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="9b0ee-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="9b0ee-127">Не забудьте сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-127">Be sure to:</span></span>

- <span data-ttu-id="9b0ee-128">Включить **веб-приложения**/**веб-API** в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-128">Include a **web app**/**web API** in hello application.</span></span>
- <span data-ttu-id="9b0ee-129">Введите `http://localhost:3000/auth/openid/return` в качестве значения **URL-адреса ответа**.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="9b0ee-130">Это URL-адрес по умолчанию hello для этого примера кода.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-130">It is hello default URL for this code sample.</span></span>
- <span data-ttu-id="9b0ee-131">Создайте для своего приложения **секрет приложения** и скопируйте его.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="9b0ee-132">Оно понадобится вам позднее.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-132">You will need it later.</span></span> <span data-ttu-id="9b0ee-133">Обратите внимание, что это значение должно toobe [XML переключения](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) перед его использованием.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="9b0ee-134">Копировать hello **идентификатор приложения** , назначенный tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="9b0ee-135">Этот идентификатор также понадобится вам позднее.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="9b0ee-136">Создание политик</span><span class="sxs-lookup"><span data-stu-id="9b0ee-136">Create your policies</span></span>

<span data-ttu-id="9b0ee-137">В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="9b0ee-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="9b0ee-138">Это приложение содержит три вида идентификации: регистрация, вход и вход с помощью учетной записи Facebook.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="9b0ee-139">Необходимые toocreate этой политики каждого типа, как описано в [статье политики](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="9b0ee-139">You need toocreate this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="9b0ee-140">При создании трех политик обязательно выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="9b0ee-141">Выберите hello **отображаемое имя** и другие атрибуты регистрации в политике организации доступа к Интернету.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="9b0ee-142">Выберите hello **отображаемое имя** и **идентификатор объекта** утверждений приложения в каждой политике.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="9b0ee-143">Можно также выбрать другие утверждения.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="9b0ee-144">Копировать hello **имя** каждой политики, после его создания.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-144">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="9b0ee-145">Он должен иметь префикс hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="9b0ee-146">Эти имена политик понадобятся вам через некоторое время.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="9b0ee-147">После создания трех политик, вы будете готовы toobuild приложения.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-147">After you create your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="9b0ee-148">Обратите внимание, что данная статья не охватывает как toouse hello политик вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-148">Note that this article does not cover how toouse hello policies you just created.</span></span> <span data-ttu-id="9b0ee-149">toolearn о том, как работают политики в Azure AD B2C, начинаться с hello [.NET web app начало учебника](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9b0ee-149">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-tooyour-directory"></a><span data-ttu-id="9b0ee-150">Добавьте каталог tooyour предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9b0ee-150">Add prerequisites tooyour directory</span></span>

<span data-ttu-id="9b0ee-151">Из командной строки hello измените каталоги tooyour корневую папку, если вы не являетесь уже существует.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-151">From hello command line, change directories tooyour root folder, if you're not already there.</span></span> <span data-ttu-id="9b0ee-152">Выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-152">Run hello following commands:</span></span>

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

<span data-ttu-id="9b0ee-153">Кроме того, мы использовали `passport-azure-ad` нашей предварительной версии в основу hello объекта hello краткое руководство.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-153">In addition, we used `passport-azure-ad` for our preview in hello skeleton of hello Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="9b0ee-154">Будет выполнена установка библиотеки hello, `passport-azure-ad` зависит.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-154">This will install hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a><span data-ttu-id="9b0ee-155">Настройка вашего приложения toouse hello стратегии Passport Node.js</span><span class="sxs-lookup"><span data-stu-id="9b0ee-155">Set up your app toouse hello Passport-Node.js strategy</span></span>
<span data-ttu-id="9b0ee-156">Настройте hello Express по промежуточного слоя toouse hello протокол проверки подлинности OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-156">Configure hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="9b0ee-157">Passport будет используется tooissue запросы входа и выхода, управлять сеансами пользователей, а получение сведений о пользователях, среди других действий.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-157">Passport will be used tooissue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="9b0ee-158">Откройте hello `config.js` файл в корневом каталоге hello проекта hello и введите значения конфигурации приложения в hello `exports.creds` раздела.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-158">Open hello `config.js` file in hello root of hello project and enter your app's configuration values in hello `exports.creds` section.</span></span>
- <span data-ttu-id="9b0ee-159">`clientID`: hello **идентификатор приложения** назначенный tooyour приложения на портале регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-159">`clientID`: hello **Application ID** assigned tooyour app in hello registration portal.</span></span>
- <span data-ttu-id="9b0ee-160">`returnURL`: hello **URI перенаправления** введенное на портале hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-160">`returnURL`: hello **Redirect URI** you entered in hello portal.</span></span>
- <span data-ttu-id="9b0ee-161">`tenantName`: hello имя клиентского приложения, например, **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-161">`tenantName`: hello tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="9b0ee-162">Откройте hello `app.js` файл в корневой hello hello проекта.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-162">Open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="9b0ee-163">Добавьте следующий вызов tooinvoke hello hello `OIDCStrategy` стратегии, входящий в состав `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-163">Add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="9b0ee-164">Используйте только ссылка на запросов на вход в toohandle стратегию hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-164">Use hello strategy you just referenced toohandle sign-in requests.</span></span>

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
<span data-ttu-id="9b0ee-165">Passport использует аналогичный шаблон для всех своих стратегий (в том числе Twitter и Facebook).</span><span class="sxs-lookup"><span data-stu-id="9b0ee-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="9b0ee-166">Все записи стратегии придерживаться toothis шаблон.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-166">All strategy writers adhere toothis pattern.</span></span> <span data-ttu-id="9b0ee-167">При просмотре hello стратегии можно увидеть, передать его `function()` с маркером и `done` как параметры hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-167">When you look at hello strategy, you can see that you pass it a `function()` that has a token and a `done` as hello parameters.</span></span> <span data-ttu-id="9b0ee-168">Стратегия Hello возвращаются tooyou после его всю свою работу.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-168">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="9b0ee-169">Хранить пользователя hello и задание hello маркер, чтобы tooask для него не требуется еще раз.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-169">Store hello user and stash hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="9b0ee-170">Hello выше код принимает все пользователи, которым hello проводит проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-170">hello preceding code takes all users whom hello server authenticates.</span></span> <span data-ttu-id="9b0ee-171">Это называется автоматической регистрацией.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-171">This is autoregistration.</span></span> <span data-ttu-id="9b0ee-172">При использовании рабочих серверов требуется запретить toolet пользователей, если только они прошли через процесс регистрации, который вы настроили.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-172">When you use production servers, you don’t want toolet in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="9b0ee-173">Этот шаблон часто используется в потребительских приложениях.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="9b0ee-174">Это позволяет tooregister с помощью Facebook, а затем он просит toofill дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-174">These allow you tooregister by using Facebook, but then they ask you toofill out additional information.</span></span> <span data-ttu-id="9b0ee-175">Если приложения были не образец, мы может извлечь из hello объекта маркера, который возвращается адрес электронной почты, а затем попросите hello toofill пользователя дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-175">If our application wasn’t a sample, we could extract an email address from hello token object that is returned, and then ask hello user toofill out additional information.</span></span> <span data-ttu-id="9b0ee-176">Так как на тестовом сервере, мы просто добавьте пользователей базы данных в памяти toohello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-176">Because this is a test server, we simply add users toohello in-memory database.</span></span>

<span data-ttu-id="9b0ee-177">Добавьте hello методы, позволяющие отслеживать tookeep пользователей, вошедших в, как требует Passport.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-177">Add hello methods that allow you tookeep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="9b0ee-178">Сюда относится сериализация и десериализация информации о пользователе:</span><span class="sxs-lookup"><span data-stu-id="9b0ee-178">This includes serializing and deserializing user information:</span></span>

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

<span data-ttu-id="9b0ee-179">Добавьте модуль экспресс-выпуск hello tooload кода hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-179">Add hello code tooload hello Express engine.</span></span> <span data-ttu-id="9b0ee-180">В следующих hello, вы увидите, что используется по умолчанию hello `/views` и `/routes` шаблон, предоставляющий экспресс-выпуск.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-180">In hello following, you can see that we use hello default `/views` and `/routes` pattern that Express provides.</span></span>

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

<span data-ttu-id="9b0ee-181">Добавить hello `POST` маршруты, в которых сдачей hello фактических запросов toohello `passport-azure-ad` ядра:</span><span class="sxs-lookup"><span data-stu-id="9b0ee-181">Add hello `POST` routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

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

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="9b0ee-182">Используйте Passport tooissue входа и запросах на выход tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="9b0ee-182">Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>

<span data-ttu-id="9b0ee-183">Приложение теперь будет правильно настроен toocommunicate с конечной точкой hello v2.0 с помощью протокола проверки подлинности OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-183">Your app is now properly configured toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="9b0ee-184">`passport-azure-ad`Разобравшись сведения hello отправляемого сообщения проверки подлинности, проверки токенов из Azure AD и поддержания сеанса пользователя.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-184">`passport-azure-ad` has taken care of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="9b0ee-185">Все, что остается является toogive пользователей toosign способом в и выполните выход и toogather Дополнительные сведения о пользователях, вошедших в.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-185">All that remains is toogive your users a way toosign in and sign out, and toogather additional information on users who have signed in.</span></span>

<span data-ttu-id="9b0ee-186">Сначала добавьте по умолчанию hello, вход, учетной записи и выхода методов tooyour `app.js` файла:</span><span class="sxs-lookup"><span data-stu-id="9b0ee-186">First, add hello default, sign-in, account, and sign-out methods tooyour `app.js` file:</span></span>

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

<span data-ttu-id="9b0ee-187">tooreview эти методы подробно:</span><span class="sxs-lookup"><span data-stu-id="9b0ee-187">tooreview these methods in detail:</span></span>
- <span data-ttu-id="9b0ee-188">Hello `/` маршрут перенаправляет toohello `index.ejs` представлении, передавая hello пользователя в запросе hello (если он существует).</span><span class="sxs-lookup"><span data-stu-id="9b0ee-188">hello `/` route redirects toohello `index.ejs` view by passing hello user in hello request (if it exists).</span></span>
- <span data-ttu-id="9b0ee-189">Hello `/account` маршрута сначала проверяет, проходят проверку подлинности (hello реализацию для этой ниже).</span><span class="sxs-lookup"><span data-stu-id="9b0ee-189">hello `/account` route first verifies that you are authenticated (hello implementation for this is below).</span></span> <span data-ttu-id="9b0ee-190">Затем инфраструктура службы передает hello пользователя в запросе hello так, чтобы получить дополнительные сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-190">It then passes hello user in hello request so that you can get additional information about hello user.</span></span>
- <span data-ttu-id="9b0ee-191">Hello `/login` hello вызовов маршрута `azuread-openidconnect` проверки подлинности из `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-191">hello `/login` route calls hello `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="9b0ee-192">Если не выполнены успешно, маршрут hello hello пользователь перенаправляется обратно слишком`/login`.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-192">If it doesn't succeed, hello route redirects hello user back too`/login`.</span></span>
- <span data-ttu-id="9b0ee-193">`/logout` просто вызывает `logout.ejs` (и соответствующий маршрут).</span><span class="sxs-lookup"><span data-stu-id="9b0ee-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="9b0ee-194">Это приведет к очистке файлы cookie и затем возвращает hello пользователя обратно слишком`index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-194">This clears cookies and then returns hello user back too`index.ejs`.</span></span>


<span data-ttu-id="9b0ee-195">Для hello последнюю часть `app.js`, добавить hello `EnsureAuthenticated` метод, используемый в hello `/account` маршрута.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-195">For hello last part of `app.js`, add hello `EnsureAuthenticated` method that is used in hello `/account` route.</span></span>

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

<span data-ttu-id="9b0ee-196">Наконец, создайте сам сервер hello в `app.js`.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-196">Finally, create hello server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a><span data-ttu-id="9b0ee-197">Создание представлений hello и направляет в Express toocall политик</span><span class="sxs-lookup"><span data-stu-id="9b0ee-197">Create hello views and routes in Express toocall your policies</span></span>

<span data-ttu-id="9b0ee-198">`app.js` готово.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="9b0ee-199">Необходимо просто tooadd hello маршруты и представления, которые позволяют hello toocall входа и регистрации политики.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-199">You just need tooadd hello routes and views that allow you toocall hello sign-in and sign-up policies.</span></span> <span data-ttu-id="9b0ee-200">Они также обрабатывать hello `/logout` и `/login` маршруты, вы создали.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-200">These also handle hello `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="9b0ee-201">Создать hello `/routes/index.js` маршрута в корневом каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-201">Create hello `/routes/index.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="9b0ee-202">Создать hello `/routes/user.js` маршрута в корневом каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-202">Create hello `/routes/user.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="9b0ee-203">Эти простые маршруты передавать запросы tooyour представления.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-203">These simple routes pass along requests tooyour views.</span></span> <span data-ttu-id="9b0ee-204">Они включают hello пользователя, если такая имеется.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-204">They include hello user, if one is present.</span></span>

<span data-ttu-id="9b0ee-205">Создать hello `/views/index.ejs` представления в корневом каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-205">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="9b0ee-206">Это простая страница, которая вызывает политики входа и выхода. Ее можно также использовать toograb сведения об учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-206">This is a simple page that calls policies for sign-in and sign-out. You can also use it toograb account information.</span></span> <span data-ttu-id="9b0ee-207">Обратите внимание, можно использовать условные hello `if (!user)` как hello пользователя передается в запрос hello tooprovide свидетельства hello пользователя вход в систему.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-207">Note that you can use hello conditional `if (!user)` as hello user is passed through in hello request tooprovide evidence that hello user is signed in.</span></span>

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

<span data-ttu-id="9b0ee-208">Создать hello `/views/account.ejs` открыть в корневом каталоге hello, можно просмотреть дополнительные сведения, `passport-azure-ad` поместить в запросе пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-208">Create hello `/views/account.ejs` view under hello root directory so that you can view additional information that `passport-azure-ad` put in hello user request.</span></span>

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

<span data-ttu-id="9b0ee-209">Выполните сборку и запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-209">You can now build and run your app.</span></span>

<span data-ttu-id="9b0ee-210">Запустите `node app.js` и перейдите в слишком`http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="9b0ee-210">Run `node app.js` and navigate too`http://localhost:3000`</span></span>


<span data-ttu-id="9b0ee-211">Регистрация или вход в приложение toohello с помощью электронной почты или Facebook.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-211">Sign up or sign in toohello app by using email or Facebook.</span></span> <span data-ttu-id="9b0ee-212">Выйдите и снова войдите от имени другого пользователя.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-212">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="9b0ee-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9b0ee-213">Next steps</span></span>

<span data-ttu-id="9b0ee-214">Справочник по hello выполнить пример (без настройки) [предоставляется как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="9b0ee-214">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="9b0ee-215">Кроме того, его можно клонировать из GitHub:</span><span class="sxs-lookup"><span data-stu-id="9b0ee-215">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="9b0ee-216">Теперь можно переходить на toomore дополнительные разделы.</span><span class="sxs-lookup"><span data-stu-id="9b0ee-216">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="9b0ee-217">Попробуйте ознакомиться с такими материалами:</span><span class="sxs-lookup"><span data-stu-id="9b0ee-217">You might try:</span></span>

[<span data-ttu-id="9b0ee-218">Безопасность веб-API с помощью модели hello B2C в Node.js</span><span class="sxs-lookup"><span data-stu-id="9b0ee-218">Secure a web API by using hello B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
