---
title: "Начало работы с веб-приложением Azure AD v2.0 .NET с поддержкой входа | Документация Майкрософт"
description: "Как создать веб-приложение .NET MVC, которое поддерживает вход пользователей в систему с помощью личной, рабочей и учебной учетных записей Майкрософт."
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
ms.openlocfilehash: ba5bdf7daba6086b70aec54ebe25d4445fa708c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-net-mvc-web-app"></a><span data-ttu-id="98489-103">Добавление функции входа в веб-приложение .NET MVC</span><span class="sxs-lookup"><span data-stu-id="98489-103">Add sign-in to an .NET MVC web app</span></span>
<span data-ttu-id="98489-104">Конечная точка версии 2.0 позволяет быстро реализовать аутентификацию в веб-приложениях с поддержкой личных учетных записей Майкрософт, а также рабочих или учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="98489-104">With the v2.0 endpoint, you can quickly add authentication to your web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="98489-105">В веб-приложениях ASP.NET это можно делать с помощью ПО промежуточного уровня OWIN корпорации Microsoft, включенного в .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="98489-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="98489-106">Не все сценарии и компоненты Azure Active Directory поддерживаются конечной точкой версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="98489-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="98489-107">Чтобы определить, следует ли вам использовать конечную точку версии 2.0, ознакомьтесь с [ограничениями версии 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="98489-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="98489-108">Здесь мы создадим веб-приложение, использующее OWIN для выполнения входа пользователя, отображения информации о нем и выполнения выхода пользователя из приложения.</span><span class="sxs-lookup"><span data-stu-id="98489-108">Here we'll build an web app that uses OWIN to sign the user in, display some information about the user, and sign the user out of the app.</span></span>

## <a name="download"></a><span data-ttu-id="98489-109">Загрузить</span><span class="sxs-lookup"><span data-stu-id="98489-109">Download</span></span>
<span data-ttu-id="98489-110">Код в этом учебнике размещен на портале [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="98489-110">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="98489-111">Для понимания процесса можно [скачать основу приложения как ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) или клонировать ее:</span><span class="sxs-lookup"><span data-stu-id="98489-111">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="98489-112">Готовое приложение также приводится в конце этого руководства.</span><span class="sxs-lookup"><span data-stu-id="98489-112">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="98489-113">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="98489-113">Register an app</span></span>
<span data-ttu-id="98489-114">Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="98489-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="98489-115">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="98489-115">Make sure to:</span></span>

* <span data-ttu-id="98489-116">Запишите назначенный вашему приложению **идентификатор приложения**. Он вскоре вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="98489-116">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="98489-117">Добавьте **веб-платформу** для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="98489-117">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="98489-118">Введите правильный **универсальный код ресурса (URI) перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="98489-118">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="98489-119">URI перенаправления сообщает Azure AD, куда следует направлять ответы проверки подлинности. Значение по умолчанию в этом руководстве — `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="98489-119">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="98489-120">Установка и настройка аутентификации OWIN</span><span class="sxs-lookup"><span data-stu-id="98489-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="98489-121">Здесь мы настроим промежуточный слой OWIN для использования протокола проверки подлинности OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="98489-121">Here, we'll configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="98489-122">Кроме всего прочего, OWIN будет использоваться для выдачи запросов входа и выхода, управления сеансом пользователя и получения сведений о пользователе.</span><span class="sxs-lookup"><span data-stu-id="98489-122">OWIN will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

1. <span data-ttu-id="98489-123">Сначала откройте файл `web.config` в корневом каталоге проекта, а затем укажите параметры конфигурации приложения в разделе `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="98489-123">To begin, open the `web.config` file in the root of the project, and enter your app's configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="98489-124">`ida:ClientId` — это **идентификатор приложения** , присвоенный приложению на портале регистрации.</span><span class="sxs-lookup"><span data-stu-id="98489-124">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="98489-125">`ida:RedirectUri` — это **универсальный код ресурса (URI) перенаправления** , который вы указали на портале.</span><span class="sxs-lookup"><span data-stu-id="98489-125">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>

2. <span data-ttu-id="98489-126">Затем с помощью консоли диспетчера пакетов добавьте в проект пакеты NuGet ПО промежуточного слоя OWIN.</span><span class="sxs-lookup"><span data-stu-id="98489-126">Next, add the OWIN middleware NuGet packages to the project using the Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="98489-127">Добавьте класс запуска OWIN в проект с именем `Startup.cs`. Щелкните проект правой кнопкой мыши, выберите пункты **Добавить** --> **Новый элемент** и найдите "OWIN".</span><span class="sxs-lookup"><span data-stu-id="98489-127">Add an "OWIN Startup Class" to the project called `Startup.cs`  Right click on the project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="98489-128">При запуске вашего приложения промежуточный слой OWIN вызовет метод `Configuration(...)` .</span><span class="sxs-lookup"><span data-stu-id="98489-128">The OWIN middleware will invoke the `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="98489-129">Замените объявление класса на `public partial class Startup` — часть этого класса уже была реализована в другом файле.</span><span class="sxs-lookup"><span data-stu-id="98489-129">Change the class declaration to `public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="98489-130">В методе `Configuration(...)` вызовите метод ConfgureAuth(...), чтобы настроить аутентификацию для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="98489-130">In the `Configuration(...)` method, make a call to ConfigureAuth(...) to set up authentication for your web app</span></span>  

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

5. <span data-ttu-id="98489-131">Откройте файл `App_Start\Startup.Auth.cs` и реализуйте метод `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="98489-131">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="98489-132">Параметры, указанные в `OpenIdConnectAuthenticationOptions` , будут служить координатами приложения для взаимодействия с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98489-132">The parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>  <span data-ttu-id="98489-133">Также будет необходимо настроить проверку подлинности для файлов Cookie — промежуточный слой OpenID Connect использует файлы cookie под обложками.</span><span class="sxs-lookup"><span data-stu-id="98489-133">You'll also need to set up Cookie Authentication - the OpenID Connect middleware uses cookies underneath the covers.</span></span>

        ```C#
        public void ConfigureAuth(IAppBuilder app)
                     {
                             app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);
        
                             app.UseCookieAuthentication(new CookieAuthenticationOptions());
        
                             app.UseOpenIdConnectAuthentication(
                                     new OpenIdConnectAuthenticationOptions
                                     {
                                             // The `Authority` represents the v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                                             // The `Scope` describes the permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                                             // In a real application you could use issuer validation for additional checks, like making sure the user's organization has signed up for your app, for instance.
        
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

## <a name="send-authentication-requests"></a><span data-ttu-id="98489-134">Отправка запросов проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="98489-134">Send authentication requests</span></span>
<span data-ttu-id="98489-135">Теперь приложение правильно настроено для взаимодействия с конечной точки версии 2.0 с использованием протокола проверки подлинности OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="98489-135">Your app is now properly configured to communicate with the v2.0 endpoint using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="98489-136">OWIN полностью возьмет на себя выполнение процессов создания сообщений проверки подлинности, проверки маркеров из Azure AD и поддержки сеанса пользователя.</span><span class="sxs-lookup"><span data-stu-id="98489-136">OWIN has taken care of all of the ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="98489-137">Остается лишь предоставить пользователям возможность выполнять вход и выход.</span><span class="sxs-lookup"><span data-stu-id="98489-137">All that remains is to give your users a way to sign in and sign out.</span></span>

- <span data-ttu-id="98489-138">Вы можете использовать теги авторизации в своих контроллерах, чтобы обязать пользователя выполнять вход перед доступом к конкретной странице.</span><span class="sxs-lookup"><span data-stu-id="98489-138">You can use authorize tags in your controllers to require that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="98489-139">Откройте `Controllers\HomeController.cs` и добавьте тег `[Authorize]` в контроллер «О программе».</span><span class="sxs-lookup"><span data-stu-id="98489-139">Open `Controllers\HomeController.cs`, and add the `[Authorize]` tag to the About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="98489-140">Вы также можете использовать OWIN для выдачи запросов проверки подлинности прямо из своего кода.</span><span class="sxs-lookup"><span data-stu-id="98489-140">You can also use OWIN to directly issue authentication requests from within your code.</span></span>  <span data-ttu-id="98489-141">Откройте `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="98489-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="98489-142">В действиях SignIn() и SignOut() выдавайте соответственно запросы входа и выхода из OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="98489-142">In the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with the v2.0 endpoint is not yet supported.  Here, we just end the session with the web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="98489-143">Теперь откройте `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="98489-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="98489-144">Здесь вы будете показывать пользователю ссылки для входа и выхода из приложения, а также выводить имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98489-144">This is where you'll show the user your app's sign-in and sign-out links, and print out the user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves.*@
        
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

## <a name="display-user-information"></a><span data-ttu-id="98489-145">Отображение сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="98489-145">Display user information</span></span>
<span data-ttu-id="98489-146">При проверке подлинности пользователей с помощью OpenID Connect конечная точка версии 2.0 возвращает в приложение маркер идентификатора, который содержит утверждения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="98489-146">When authenticating users with OpenID Connect, the v2.0 endpoint returns an id_token to the app that contains claims, or assertions about the user.</span></span>  <span data-ttu-id="98489-147">Эти утверждения можно использовать для настройки своего приложения:</span><span class="sxs-lookup"><span data-stu-id="98489-147">You can use these claims to personalize your app:</span></span>

- <span data-ttu-id="98489-148">Откройте файл `Controllers\HomeController.cs` .</span><span class="sxs-lookup"><span data-stu-id="98489-148">Open the `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="98489-149">Для доступа к утверждениям о пользователе в своих контроллерах можно использовать объект субъекта безопасности `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="98489-149">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // The object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // The subject or nameidentifier claim can be used to uniquely identify the user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="98489-150">Выполнить</span><span class="sxs-lookup"><span data-stu-id="98489-150">Run</span></span>
<span data-ttu-id="98489-151">Наконец, постройте и запустите свое приложение!</span><span class="sxs-lookup"><span data-stu-id="98489-151">Finally, build and run your app!</span></span>   <span data-ttu-id="98489-152">Выполните вход с личной учетной записью Майкрософт, рабочей или учебной учетной записью и обратите внимание на то, как удостоверение пользователя отображается в верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="98489-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="98489-153">Теперь у вас есть веб-приложение, защищенное с помощью стандартных отраслевых протоколов, которое может проверять подлинность пользователей с помощью личных, рабочих и учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="98489-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="98489-154">Готовый пример (без ваших значений конфигурации) [можно скачать в виде ZIP-файла здесь](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip)или клонировать с портала GitHub.</span><span class="sxs-lookup"><span data-stu-id="98489-154">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="98489-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98489-155">Next steps</span></span>
<span data-ttu-id="98489-156">Теперь можно перейти к более сложным темам.</span><span class="sxs-lookup"><span data-stu-id="98489-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="98489-157">Можно попробовать:</span><span class="sxs-lookup"><span data-stu-id="98489-157">You may want to try:</span></span>

[<span data-ttu-id="98489-158">Защита веб-API с помощью конечной точки версии 2.0 >></span><span class="sxs-lookup"><span data-stu-id="98489-158">Secure a Web API with the the v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="98489-159">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="98489-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="98489-160">Руководство разработчика версии 2.0 >></span><span class="sxs-lookup"><span data-stu-id="98489-160">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="98489-161">Тег StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="98489-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="98489-162">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="98489-162">Get security updates for our products</span></span>
<span data-ttu-id="98489-163">Рекомендуем вам настроить уведомления о нарушениях безопасности. Это можно сделать, подписавшись на уведомления безопасности консультационных служб на [этой странице](https://technet.microsoft.com/security/dd252948).</span><span class="sxs-lookup"><span data-stu-id="98489-163">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
