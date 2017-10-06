---
title: "aaaAzure AD B2C | Документы Microsoft"
description: "Как toobuild веб-API .NET с помощью Azure Active Directory B2C безопасность с помощью маркера доступа OAuth 2.0 для проверки подлинности."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="13d5f-103">Azure Active Directory B2C: создание веб-API .NET</span><span class="sxs-lookup"><span data-stu-id="13d5f-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="13d5f-104">С помощью Azure Active Directory (Azure AD) B2C можно защитить веб-API с помощью маркера доступа OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="13d5f-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="13d5f-105">Эти маркеры позволяют ваш клиент toohello tooauthenticate приложения API.</span><span class="sxs-lookup"><span data-stu-id="13d5f-105">These tokens allow your client apps tooauthenticate toohello API.</span></span> <span data-ttu-id="13d5f-106">В этой статье показано, как toocreate API .NET MVC «список дел», которая позволяет пользователям клиента tooCRUD задач приложения.</span><span class="sxs-lookup"><span data-stu-id="13d5f-106">This article shows you how toocreate a .NET MVC "to-do list" API that allows users of your client application tooCRUD tasks.</span></span> <span data-ttu-id="13d5f-107">веб-API Hello защищается с помощью Azure AD B2C и позволяет toomanage прошедшим проверку пользователям только их список дел.</span><span class="sxs-lookup"><span data-stu-id="13d5f-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="13d5f-108">Создание каталога Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="13d5f-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="13d5f-109">Перед использованием Azure AD B2C необходимо создать каталог или клиент.</span><span class="sxs-lookup"><span data-stu-id="13d5f-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="13d5f-110">Каталог — это контейнер для данных всех ваших пользователей, приложений, групп и т. д.</span><span class="sxs-lookup"><span data-stu-id="13d5f-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="13d5f-111">Прежде чем продолжать работу с руководством, [создайте каталог B2C](active-directory-b2c-get-started.md), если вы его еще не создали.</span><span class="sxs-lookup"><span data-stu-id="13d5f-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="13d5f-112">клиентское приложение Hello и веб-API необходимо использовать каталог B2C hello же Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13d5f-112">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="13d5f-113">Создание веб-API</span><span class="sxs-lookup"><span data-stu-id="13d5f-113">Create a web API</span></span>

<span data-ttu-id="13d5f-114">Далее необходимо toocreate API веб-приложения в каталоге B2C.</span><span class="sxs-lookup"><span data-stu-id="13d5f-114">Next, you need toocreate a web API app in your B2C directory.</span></span> <span data-ttu-id="13d5f-115">Это дает сведения о Azure AD, что его нуждается toosecurely взаимодействовать с приложением.</span><span class="sxs-lookup"><span data-stu-id="13d5f-115">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="13d5f-116">toocreate приложения, выполните [эти инструкции](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="13d5f-116">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="13d5f-117">Не забудьте сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="13d5f-117">Be sure to:</span></span>

* <span data-ttu-id="13d5f-118">Включить **веб-приложения** или **веб-API** в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="13d5f-118">Include a **web app** or **web API** in hello application.</span></span>
* <span data-ttu-id="13d5f-119">Используйте hello **URI перенаправления** `https://localhost:44332/` для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="13d5f-119">Use hello **Redirect URI** `https://localhost:44332/` for hello web app.</span></span> <span data-ttu-id="13d5f-120">Это расположение по умолчанию hello hello веб-приложение клиента для этого примера кода.</span><span class="sxs-lookup"><span data-stu-id="13d5f-120">This is hello default location of hello web app client for this code sample.</span></span>
* <span data-ttu-id="13d5f-121">Копировать hello **идентификатор приложения** , назначенный tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="13d5f-121">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="13d5f-122">Он понадобится вам позднее.</span><span class="sxs-lookup"><span data-stu-id="13d5f-122">You'll need it later.</span></span>
* <span data-ttu-id="13d5f-123">Введите идентификатор приложения в поле **URI кода приложения**.</span><span class="sxs-lookup"><span data-stu-id="13d5f-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="13d5f-124">Добавить разрешения с помощью hello **публикации областей** меню.</span><span class="sxs-lookup"><span data-stu-id="13d5f-124">Add permissions through hello **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="13d5f-125">Создание политик</span><span class="sxs-lookup"><span data-stu-id="13d5f-125">Create your policies</span></span>

<span data-ttu-id="13d5f-126">В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="13d5f-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="13d5f-127">Вам потребуется toocreate toocommunicate политики с Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="13d5f-127">You will need toocreate a policy toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="13d5f-128">Рекомендуется с помощью hello политики регистрации-повышение или вход в сочетании, как описано в hello [статье политики](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="13d5f-128">We recommend using hello combined sign-up/sign-in policy, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="13d5f-129">При создании политики обязательно сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="13d5f-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="13d5f-130">В политике укажите **отображаемое имя** и другие атрибуты регистрации.</span><span class="sxs-lookup"><span data-stu-id="13d5f-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="13d5f-131">В каждой политике в качестве утверждения приложения выберите утверждения **Отображаемое имя** и **Идентификатор объекта**.</span><span class="sxs-lookup"><span data-stu-id="13d5f-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="13d5f-132">Можно также выбрать другие утверждения.</span><span class="sxs-lookup"><span data-stu-id="13d5f-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="13d5f-133">Копировать hello **имя** каждой политики, после его создания.</span><span class="sxs-lookup"><span data-stu-id="13d5f-133">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="13d5f-134">Имя политики hello потребуется позднее.</span><span class="sxs-lookup"><span data-stu-id="13d5f-134">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="13d5f-135">После успешного создания политики hello вы будете готовы toobuild приложения.</span><span class="sxs-lookup"><span data-stu-id="13d5f-135">After you have successfully created hello policy, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="13d5f-136">Загрузка кода hello</span><span class="sxs-lookup"><span data-stu-id="13d5f-136">Download hello code</span></span>

<span data-ttu-id="13d5f-137">Hello кода для этого учебника, сохраняется на [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="13d5f-137">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="13d5f-138">Образец hello можно клонировать, выполнив:</span><span class="sxs-lookup"><span data-stu-id="13d5f-138">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="13d5f-139">После загрузки кода образца hello запущен tooget файл .sln Visual Studio откройте hello.</span><span class="sxs-lookup"><span data-stu-id="13d5f-139">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="13d5f-140">Hello файл решения содержит два проекта: `TaskWebApp` и `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="13d5f-140">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="13d5f-141">`TaskWebApp`— веб-приложение MVC, hello пользователь взаимодействует с.</span><span class="sxs-lookup"><span data-stu-id="13d5f-141">`TaskWebApp` is an MVC web application that hello user interacts with.</span></span> <span data-ttu-id="13d5f-142">`TaskService`— приложение hello фоновая веб-API, который хранит список дел каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="13d5f-142">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="13d5f-143">В этой статье рассматривается hello `TaskService` приложения.</span><span class="sxs-lookup"><span data-stu-id="13d5f-143">This article will only discuss hello `TaskService` application.</span></span> <span data-ttu-id="13d5f-144">toolearn как toobuild `TaskWebApp` с помощью Azure AD B2C, в разделе [наш учебник по .NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="13d5f-144">toolearn how toobuild `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="13d5f-145">Обновите конфигурацию hello Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="13d5f-145">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="13d5f-146">Выборка — настроенное toouse hello политик и клиент идентификатор нашей демонстрационному клиенту.</span><span class="sxs-lookup"><span data-stu-id="13d5f-146">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="13d5f-147">Если вы хотите toouse клиента, необходимо будет hello toodo следующие:</span><span class="sxs-lookup"><span data-stu-id="13d5f-147">If you would like toouse your own tenant, you will need toodo hello following:</span></span>

1. <span data-ttu-id="13d5f-148">Откройте `web.config` в hello `TaskService` проекта и замените значения hello</span><span class="sxs-lookup"><span data-stu-id="13d5f-148">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>
    * <span data-ttu-id="13d5f-149">`ida:Tenant` именем своего клиента;</span><span class="sxs-lookup"><span data-stu-id="13d5f-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="13d5f-150">`ida:ClientId` идентификатором клиента для приложения веб-API;</span><span class="sxs-lookup"><span data-stu-id="13d5f-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="13d5f-151">`ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему;</span><span class="sxs-lookup"><span data-stu-id="13d5f-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="13d5f-152">Откройте `web.config` в hello `TaskWebApp` проекта и замените значения hello</span><span class="sxs-lookup"><span data-stu-id="13d5f-152">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>
    * <span data-ttu-id="13d5f-153">`ida:Tenant` именем своего клиента;</span><span class="sxs-lookup"><span data-stu-id="13d5f-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="13d5f-154">`ida:ClientId` идентификатором клиента для веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="13d5f-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="13d5f-155">`ida:ClientSecret` секретным ключом веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="13d5f-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="13d5f-156">`ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему;</span><span class="sxs-lookup"><span data-stu-id="13d5f-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="13d5f-157">`ida:EditProfilePolicyId` именем политики "Изменение профиля";</span><span class="sxs-lookup"><span data-stu-id="13d5f-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="13d5f-158">`ida:ResetPasswordPolicyId` именем политики "Сброс профиля".</span><span class="sxs-lookup"><span data-stu-id="13d5f-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-hello-api"></a><span data-ttu-id="13d5f-159">Защита hello API</span><span class="sxs-lookup"><span data-stu-id="13d5f-159">Secure hello API</span></span>

<span data-ttu-id="13d5f-160">Теперь, когда у вас есть клиент, который вызывает API, можно защитить API (например, `TaskService`) с помощью токенов носителя OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="13d5f-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="13d5f-161">Это гарантирует, что каждый запрос tooyour API будет действителен только если hello запрос содержит токен носителя.</span><span class="sxs-lookup"><span data-stu-id="13d5f-161">This ensures that each request tooyour API will only be valid if hello request has a bearer token.</span></span> <span data-ttu-id="13d5f-162">API может принимать и проверять токены носителя с помощью библиотеки OWIN от Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="13d5f-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="13d5f-163">Установка OWIN</span><span class="sxs-lookup"><span data-stu-id="13d5f-163">Install OWIN</span></span>

<span data-ttu-id="13d5f-164">Перед началом установки hello конвейера проверки подлинности OWIN OAuth с помощью hello консоль диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="13d5f-164">Begin by installing hello OWIN OAuth authentication pipeline by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="13d5f-165">Будет выполнена установка hello OWIN по промежуточного слоя, будут приниматься и проверяться токены носителя.</span><span class="sxs-lookup"><span data-stu-id="13d5f-165">This will install hello OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="13d5f-166">Добавление класса запуска OWIN</span><span class="sxs-lookup"><span data-stu-id="13d5f-166">Add an OWIN startup class</span></span>

<span data-ttu-id="13d5f-167">Добавление toohello класс запуска OWIN API с именем `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="13d5f-167">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="13d5f-168">Правой кнопкой мыши проект hello, выберите **добавить** и **новый элемент**и выполните поиск OWIN.</span><span class="sxs-lookup"><span data-stu-id="13d5f-168">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="13d5f-169">по промежуточного слоя OWIN Hello будет вызывать hello `Configuration(…)` метод при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="13d5f-169">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="13d5f-170">В нашем примере мы изменили объявление класса hello слишком`public partial class Startup` и реализации hello hello класса в другой части `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="13d5f-170">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="13d5f-171">Внутри hello `Configuration` метод, мы добавили вызов слишком`ConfigureAuth`, которая определена в `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="13d5f-171">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="13d5f-172">После изменения hello `Startup.cs` выглядит как hello следующее:</span><span class="sxs-lookup"><span data-stu-id="13d5f-172">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="13d5f-173">Настройка проверки подлинности OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="13d5f-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="13d5f-174">Привет открыть файл `App_Start\Startup.Auth.cs`и реализовать hello `ConfigureAuth(...)` метод.</span><span class="sxs-lookup"><span data-stu-id="13d5f-174">Open hello file `App_Start\Startup.Auth.cs`, and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="13d5f-175">Например он может выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="13d5f-175">For example, it could look like hello following:</span></span>

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a><span data-ttu-id="13d5f-176">Контроллер задач безопасного hello</span><span class="sxs-lookup"><span data-stu-id="13d5f-176">Secure hello task controller</span></span>

<span data-ttu-id="13d5f-177">После проверки подлинности настроенных toouse OAuth 2.0, приложение hello можно защитить web API, добавив `[Authorize]` контроллер задач toohello тег.</span><span class="sxs-lookup"><span data-stu-id="13d5f-177">After hello app is configured toouse OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag toohello task controller.</span></span> <span data-ttu-id="13d5f-178">Это контроллер hello, где все операции списка задач выполняется, поэтому необходимо обеспечить безопасность всей контроллера hello на уровне класса hello.</span><span class="sxs-lookup"><span data-stu-id="13d5f-178">This is hello controller where all to-do list manipulation takes place, so you should secure hello entire controller at hello class level.</span></span> <span data-ttu-id="13d5f-179">Можно также добавить hello `[Authorize]` тег действия tooindividual для более точное управление.</span><span class="sxs-lookup"><span data-stu-id="13d5f-179">You can also add hello `[Authorize]` tag tooindividual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a><span data-ttu-id="13d5f-180">Получение сведений о пользователе из hello маркера</span><span class="sxs-lookup"><span data-stu-id="13d5f-180">Get user information from hello token</span></span>

<span data-ttu-id="13d5f-181">`TasksController`сохраняет задачи в базе данных, где каждый объект имеет связанный пользователь «владеет» задачу hello.</span><span class="sxs-lookup"><span data-stu-id="13d5f-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" hello task.</span></span> <span data-ttu-id="13d5f-182">Владелец Hello идентифицируется hello пользователя **идентификатор объекта**.</span><span class="sxs-lookup"><span data-stu-id="13d5f-182">hello owner is identified by hello user's **object ID**.</span></span> <span data-ttu-id="13d5f-183">(Вот почему требуется идентификатор tooadd hello объекта, как приложение утверждения во всех политик.)</span><span class="sxs-lookup"><span data-stu-id="13d5f-183">(This is why you needed tooadd hello object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a><span data-ttu-id="13d5f-184">Проверки разрешений hello в маркере hello</span><span class="sxs-lookup"><span data-stu-id="13d5f-184">Validate hello permissions in hello token</span></span>

<span data-ttu-id="13d5f-185">Общим требованием для веб-API — hello toovalidate «областей» присутствует в маркере hello.</span><span class="sxs-lookup"><span data-stu-id="13d5f-185">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="13d5f-186">Это гарантирует, что этой hello пользователь согласился службы списка дел hello необходимые tooaccess toohello разрешения.</span><span class="sxs-lookup"><span data-stu-id="13d5f-186">This ensures that hello user has consented toohello permissions required tooaccess hello to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="13d5f-187">Запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="13d5f-187">Run hello sample app</span></span>

<span data-ttu-id="13d5f-188">Наконец, выполните сборку и запустите `TaskWebApp` и `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="13d5f-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="13d5f-189">Создавать некоторые задачи в список дел пользователя hello и обратите внимание на то, как они сохраняются в hello API даже после остановки и перезапуска hello клиента.</span><span class="sxs-lookup"><span data-stu-id="13d5f-189">Create some tasks on hello user's to-do list and notice how they are persisted in hello API even after you stop and restart hello client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="13d5f-190">Изменение политик</span><span class="sxs-lookup"><span data-stu-id="13d5f-190">Edit your policies</span></span>

<span data-ttu-id="13d5f-191">После защиты API с помощью Azure AD B2C можно поэкспериментировать с знак в-регистрации-повышение политики и представления эффекты hello (или его отсутствие) на hello API.</span><span class="sxs-lookup"><span data-stu-id="13d5f-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view hello effects (or lack thereof) on hello API.</span></span> <span data-ttu-id="13d5f-192">Можно управлять утверждений приложения hello в политиках hello и изменение сведений о пользователе hello, доступные в hello веб-API.</span><span class="sxs-lookup"><span data-stu-id="13d5f-192">You can manipulate hello application claims in hello policies and change hello user information that is available in hello web API.</span></span> <span data-ttu-id="13d5f-193">Все добавленные утверждения будут доступных tooyour .NET MVC веб-API в hello `ClaimsPrincipal` объекта, как описано ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="13d5f-193">Any claims that you add will be available tooyour .NET MVC web API in hello `ClaimsPrincipal` object, as described earlier in this article.</span></span>
