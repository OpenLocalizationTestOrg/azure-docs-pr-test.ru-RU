---
title: "aaaAzure AD v2.0 .NET, веб-приложение входа Приступая к работе | Документы Microsoft"
description: "Как toobuild веб-приложение .NET MVC, подписывает пользователей обоих личную учетную запись Майкрософт и рабочих учетных записей."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c8b97ac6-0a06-4367-81b6-7d1d98152b14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 241e9c90bd752fbecc3696ce4f1bed3f9772189d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-net-mvc-web-app"></a><span data-ttu-id="4659c-103">Добавить веб-приложение .NET MVC tooan входа</span><span class="sxs-lookup"><span data-stu-id="4659c-103">Add sign-in tooan .NET MVC web app</span></span>
<span data-ttu-id="4659c-104">С конечной точкой v2.0 hello можно быстро добавлять проверки подлинности tooyour веб-приложений с помощью поддержки для обоих личные учетные записи Майкрософт и рабочих учетных записей.</span><span class="sxs-lookup"><span data-stu-id="4659c-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="4659c-105">В веб-приложениях ASP.NET это можно делать с помощью ПО промежуточного уровня OWIN корпорации Microsoft, включенного в .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="4659c-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="4659c-106">Не все сценарии Azure Active Directory и возможности поддерживаются hello v2.0 конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="4659c-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="4659c-107">toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="4659c-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="4659c-108">Здесь мы выполним сборку веб-приложения, использующего пользователя hello toosign OWIN в отображаются некоторые сведения о пользователе hello и знак hello выход пользователя из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4659c-108">Here we'll build an web app that uses OWIN toosign hello user in, display some information about hello user, and sign hello user out of hello app.</span></span>

## <a name="download"></a><span data-ttu-id="4659c-109">Загрузить</span><span class="sxs-lookup"><span data-stu-id="4659c-109">Download</span></span>
<span data-ttu-id="4659c-110">поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="4659c-110">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="4659c-111">можно toofollow вдоль [загрузить приложение hello основу как .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) или основу hello клона:</span><span class="sxs-lookup"><span data-stu-id="4659c-111">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="4659c-112">в конце hello в учебнике также предоставляется приложение Hello завершена.</span><span class="sxs-lookup"><span data-stu-id="4659c-112">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="4659c-113">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="4659c-113">Register an app</span></span>
<span data-ttu-id="4659c-114">Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="4659c-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="4659c-115">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="4659c-115">Make sure to:</span></span>

* <span data-ttu-id="4659c-116">Копировать вниз hello **идентификатор приложения** назначены tooyour приложения, оно понадобится скоро.</span><span class="sxs-lookup"><span data-stu-id="4659c-116">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="4659c-117">Добавить hello **Web** платформы для приложения.</span><span class="sxs-lookup"><span data-stu-id="4659c-117">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="4659c-118">Введите правильный hello **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="4659c-118">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="4659c-119">Hello uri перенаправления указывает tooAzure AD, где следует направлять запросы проверки подлинности — по умолчанию hello в этом учебнике используется `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="4659c-119">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="4659c-120">Установка и настройка аутентификации OWIN</span><span class="sxs-lookup"><span data-stu-id="4659c-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="4659c-121">Здесь мы настроим hello OWIN по промежуточного слоя toouse hello OpenID Connect протокол проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4659c-121">Here, we'll configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="4659c-122">OWIN быть используется tooissue запросы на вход и выход, управлять сеансом пользователя hello и получения сведений о пользователе hello, среди прочего.</span><span class="sxs-lookup"><span data-stu-id="4659c-122">OWIN will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

1. <span data-ttu-id="4659c-123">toobegin Привет открыть `web.config` файл в корневом каталоге hello hello проекта и введите значения конфигурации приложения в hello `<appSettings>` раздела.</span><span class="sxs-lookup"><span data-stu-id="4659c-123">toobegin, open hello `web.config` file in hello root of hello project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="4659c-124">Hello `ida:ClientId` — hello **идентификатор приложения** назначенный tooyour приложения на портале регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="4659c-124">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="4659c-125">Hello `ida:RedirectUri` — hello **Uri перенаправления** введенное на портале hello.</span><span class="sxs-lookup"><span data-stu-id="4659c-125">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>

2. <span data-ttu-id="4659c-126">Затем добавьте hello OWIN по промежуточного слоя NuGet пакеты toohello проекта с помощью консоли диспетчера пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="4659c-126">Next, add hello OWIN middleware NuGet packages toohello project using hello Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="4659c-127">Добавить проект toohello «Класс запуска OWIN» вызывается `Startup.cs` вправо, щелкните проект hello--> **добавить** --> **новый элемент** --> Поиск «OWIN».</span><span class="sxs-lookup"><span data-stu-id="4659c-127">Add an "OWIN Startup Class" toohello project called `Startup.cs`  Right click on hello project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="4659c-128">по промежуточного слоя OWIN Hello будет вызывать hello `Configuration(...)` метод при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="4659c-128">hello OWIN middleware will invoke hello `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="4659c-129">Измените объявление класса hello слишком`public partial class Startup` -мы уже реализовали часть этого класса для вас в другом файле.</span><span class="sxs-lookup"><span data-stu-id="4659c-129">Change hello class declaration too`public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="4659c-130">В hello `Configuration(...)` метод, сделать tooset tooConfigureAuth(...) вызов проверку подлинности для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4659c-130">In hello `Configuration(...)` method, make a call tooConfigureAuth(...) tooset up authentication for your web app</span></span>  

        ```C#
        [assembly: OwinStartup(typeof(Startup))]
        
        namespace TodoList_WebApp
        {
            public partial class Startup
            {
                public void Configuration(IAppBuilder app)
                {
                    ConfigureAuth(app);
                }
            }
        }
        ```

5. <span data-ttu-id="4659c-131">Привет открыть файл `App_Start\Startup.Auth.cs` и реализовать hello `ConfigureAuth(...)` метод.</span><span class="sxs-lookup"><span data-stu-id="4659c-131">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="4659c-132">Здравствуйте, параметры, указываемые в `OpenIdConnectAuthenticationOptions` будет служить в качестве координат для toocommunicate вашего приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4659c-132">hello parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>  <span data-ttu-id="4659c-133">Необходимо также tooset копирование файла Cookie проверки подлинности — hello OpenID Connect по промежуточного слоя использует файлы cookie под охватывает hello.</span><span class="sxs-lookup"><span data-stu-id="4659c-133">You'll also need tooset up Cookie Authentication - hello OpenID Connect middleware uses cookies underneath hello covers.</span></span>

        ```C#
        public void ConfigureAuth(IAppBuilder app)
                     {
                             app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);
        
                             app.UseCookieAuthentication(new CookieAuthenticationOptions());
        
                             app.UseOpenIdConnectAuthentication(
                                     new OpenIdConnectAuthenticationOptions
                                     {
                                             // hello `Authority` represents hello v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                                             // hello `Scope` describes hello permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                                             // In a real application you could use issuer validation for additional checks, like making sure hello user's organization has signed up for your app, for instance.
        
                                             ClientId = clientId,
                                             Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0"),
                                             RedirectUri = redirectUri,
                                             Scope = "openid email profile",
                                             ResponseType = "id_token",
                                             PostLogoutRedirectUri = redirectUri,
                                             TokenValidationParameters = new TokenValidationParameters
                                             {
                                                     ValidateIssuer = false,
                                             },
                                             Notifications = new OpenIdConnectAuthenticationNotifications
                                             {
                                                     AuthenticationFailed = OnAuthenticationFailed,
                                             }
                                     });
                     }
        ```

## <a name="send-authentication-requests"></a><span data-ttu-id="4659c-134">Отправка запросов проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="4659c-134">Send authentication requests</span></span>
<span data-ttu-id="4659c-135">Приложение теперь будет правильно настроен toocommunicate с конечной точкой v2.0 hello, используя протокол проверки подлинности OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="4659c-135">Your app is now properly configured toocommunicate with hello v2.0 endpoint using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="4659c-136">OWIN Разобравшись все подробности сложный hello отправляемого сообщения проверки подлинности, проверки токенов из Azure AD и поддержания сеанса пользователя.</span><span class="sxs-lookup"><span data-stu-id="4659c-136">OWIN has taken care of all of hello ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="4659c-137">Все, что остается является toogive пользователей toosign способом в и выхода.</span><span class="sxs-lookup"><span data-stu-id="4659c-137">All that remains is toogive your users a way toosign in and sign out.</span></span>

- <span data-ttu-id="4659c-138">Можно использовать теги авторизации в вашей toorequire контроллеров входе перед обращением к определенной странице.</span><span class="sxs-lookup"><span data-stu-id="4659c-138">You can use authorize tags in your controllers toorequire that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="4659c-139">Откройте `Controllers\HomeController.cs`и добавить hello `[Authorize]` тега toohello о контроллере.</span><span class="sxs-lookup"><span data-stu-id="4659c-139">Open `Controllers\HomeController.cs`, and add hello `[Authorize]` tag toohello About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="4659c-140">Также можно использовать запросов OWIN toodirectly проблема проверки подлинности из кода.</span><span class="sxs-lookup"><span data-stu-id="4659c-140">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span>  <span data-ttu-id="4659c-141">Откройте `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="4659c-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="4659c-142">В hello SignIn() и SignOut() действия выполните запрос OpenID Connect и запросах на выход, соответственно.</span><span class="sxs-lookup"><span data-stu-id="4659c-142">In hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with hello v2.0 endpoint is not yet supported.  Here, we just end hello session with hello web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="4659c-143">Теперь откройте `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="4659c-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="4659c-144">Это, где вы Показывать hello пользовательского приложения ссылки входа и выхода из системы, а также напечатать имя пользователя hello в представлении.</span><span class="sxs-lookup"><span data-stu-id="4659c-144">This is where you'll show hello user your app's sign-in and sign-out links, and print out hello user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves.*@
        
                        Hello, @(System.Security.Claims.ClaimsPrincipal.Current.FindFirst("preferred_username").Value)!
                    </li>
                    <li>
                        @Html.ActionLink("Sign out", "SignOut", "Account")
                    </li>
                </ul>
            </text>
        }
        else
        {
            <ul class="nav navbar-nav navbar-right">
                <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
            </ul>
        }
        ```

## <a name="display-user-information"></a><span data-ttu-id="4659c-145">Отображение сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="4659c-145">Display user information</span></span>
<span data-ttu-id="4659c-146">При проверке подлинности пользователей с OpenID Connect, конечная точка v2.0 hello возвращает id_token toohello приложение, которое содержит утверждения или утверждения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="4659c-146">When authenticating users with OpenID Connect, hello v2.0 endpoint returns an id_token toohello app that contains claims, or assertions about hello user.</span></span>  <span data-ttu-id="4659c-147">Можно использовать эти утверждения toopersonalize приложения:</span><span class="sxs-lookup"><span data-stu-id="4659c-147">You can use these claims toopersonalize your app:</span></span>

- <span data-ttu-id="4659c-148">Откройте hello `Controllers\HomeController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="4659c-148">Open hello `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="4659c-149">Можно использовать утверждения пользователей hello в контроллерах через hello `ClaimsPrincipal.Current` объект субъекта безопасности.</span><span class="sxs-lookup"><span data-stu-id="4659c-149">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // hello object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // hello subject or nameidentifier claim can be used toouniquely identify hello user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="4659c-150">Выполнить</span><span class="sxs-lookup"><span data-stu-id="4659c-150">Run</span></span>
<span data-ttu-id="4659c-151">Наконец, постройте и запустите свое приложение!</span><span class="sxs-lookup"><span data-stu-id="4659c-151">Finally, build and run your app!</span></span>   <span data-ttu-id="4659c-152">Войдите, используя личную учетную запись Майкрософт или рабочую учетную запись и обратите внимание на то, как удостоверение пользователя hello отражается hello верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="4659c-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="4659c-153">Теперь у вас есть веб-приложение, защищенное с помощью стандартных отраслевых протоколов, которое может проверять подлинность пользователей с помощью личных, рабочих и учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="4659c-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="4659c-154">Справочник по hello выполнить пример (без настройки) [предоставляется как .zip здесь](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), или вы можете клонировать из GitHub:</span><span class="sxs-lookup"><span data-stu-id="4659c-154">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="4659c-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4659c-155">Next steps</span></span>
<span data-ttu-id="4659c-156">Теперь можно перейти к более сложным темам.</span><span class="sxs-lookup"><span data-stu-id="4659c-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="4659c-157">Вы можете tootry:</span><span class="sxs-lookup"><span data-stu-id="4659c-157">You may want tootry:</span></span>

[<span data-ttu-id="4659c-158">Защита веб-API с конечной точкой v2.0 hello hello >></span><span class="sxs-lookup"><span data-stu-id="4659c-158">Secure a Web API with hello hello v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="4659c-159">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="4659c-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="4659c-160">Руководство разработчика v2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="4659c-160">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="4659c-161">Тег StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="4659c-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="4659c-162">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="4659c-162">Get security updates for our products</span></span>
<span data-ttu-id="4659c-163">Мы рекомендуем вам уведомления при возникновении события безопасности, посетив tooget [эту страницу](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.</span><span class="sxs-lookup"><span data-stu-id="4659c-163">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
