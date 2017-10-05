---
title: "Приступая к работе с Azure AD для веб-приложения .NET | Документация Майкрософт"
description: "Узнайте, как выполнить сборку веб-приложения .NET MVC, которое интегрируется с Azure AD для входа."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 7ac5d3e5cc28ead993e159d003244e6451acb0cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="6b58d-103">Вход в веб-приложение ASP.NET и выход из него с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b58d-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="6b58d-104">Azure Active Directory (Azure AD) позволяет легко выполнять функции управления удостоверением веб-приложения, обеспечивая единый вход и выход с помощью всего лишь нескольких строк кода.</span><span class="sxs-lookup"><span data-stu-id="6b58d-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="6b58d-105">Пользователи могут входить в веб-приложения ASP.NET и выходить из них с помощью реализованного корпорацией Майкрософт ПО промежуточного слоя OWIN (Open Web Interface for .NET).</span><span class="sxs-lookup"><span data-stu-id="6b58d-105">You can sign users in and out of ASP.NET web apps by using the Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="6b58d-106">Поддерживаемое сообществом ПО промежуточного слоя OWIN включено в .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="6b58d-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="6b58d-107">В этой статье показано, как с помощью OWIN:</span><span class="sxs-lookup"><span data-stu-id="6b58d-107">This article shows how to use OWIN to:</span></span>

* <span data-ttu-id="6b58d-108">выполнять вход пользователей в веб-приложения с использованием Azure AD как поставщика удостоверений;</span><span class="sxs-lookup"><span data-stu-id="6b58d-108">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="6b58d-109">отображать некоторые сведения о пользователе;</span><span class="sxs-lookup"><span data-stu-id="6b58d-109">Display some user information.</span></span>
* <span data-ttu-id="6b58d-110">выполнять выход пользователей из приложений.</span><span class="sxs-lookup"><span data-stu-id="6b58d-110">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="6b58d-111">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="6b58d-111">Before you get started</span></span>
* <span data-ttu-id="6b58d-112">Скачайте [схему приложения](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) или [готовый пример](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="6b58d-112">Download the [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download the [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="6b58d-113">Вам также необходим клиент Azure AD для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="6b58d-113">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="6b58d-114">Если у вас еще нет клиента Azure AD, [узнайте, как его получить](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="6b58d-114">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="6b58d-115">Когда будете готовы, выполните процедуры, описанные в следующих четырех разделах.</span><span class="sxs-lookup"><span data-stu-id="6b58d-115">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="6b58d-116">Шаг 1. Регистрация нового приложения в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b58d-116">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="6b58d-117">Чтобы настроить приложение для аутентификации пользователей, сначала зарегистрируйте его в клиенте. Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6b58d-117">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="6b58d-118">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6b58d-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6b58d-119">На верхней панели щелкните имя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6b58d-119">On the top bar, click your account name.</span></span> <span data-ttu-id="6b58d-120">В списке **Каталог** выберите клиент Active Directory для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="6b58d-120">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="6b58d-121">В области слева щелкните **Больше служб** и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6b58d-121">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="6b58d-122">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6b58d-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="6b58d-123">Следуйте инструкциям на экране, чтобы создать **веб-приложение и (или) веб-API**.</span><span class="sxs-lookup"><span data-stu-id="6b58d-123">Follow the prompts to create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="6b58d-124">**Имя** — это описание приложения для пользователей.</span><span class="sxs-lookup"><span data-stu-id="6b58d-124">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="6b58d-125">**URL-адрес входа** — это базовый URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="6b58d-125">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="6b58d-126">Формат URL-адреса по умолчанию — https://localhost:44320/.</span><span class="sxs-lookup"><span data-stu-id="6b58d-126">The skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="6b58d-127">После завершения регистрации Azure AD присваивает приложению уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="6b58d-127">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="6b58d-128">Скопируйте значение на странице приложения, чтобы использовать его в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="6b58d-128">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="6b58d-129">На странице **Параметры** -> **Свойства** приложения обновите его универсальный код ресурса (URI) идентификатора.</span><span class="sxs-lookup"><span data-stu-id="6b58d-129">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="6b58d-130">**URI кода приложения** — это уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="6b58d-130">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="6b58d-131">Соглашение об именовании — `https://<tenant-domain>/<app-name>` (например, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="6b58d-131">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="6b58d-132">Шаг 2. Настройка приложения для использования конвейера аутентификации OWIN</span><span class="sxs-lookup"><span data-stu-id="6b58d-132">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="6b58d-133">На этом шаге настраивается ПО промежуточного слоя OWIN для использования протокола проверки подлинности OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="6b58d-133">In this step, you configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="6b58d-134">OWIN используется для выдачи запросов на вход и выход, управления сеансами пользователей, получения сведений о пользователях и т. д.</span><span class="sxs-lookup"><span data-stu-id="6b58d-134">You use OWIN to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="6b58d-135">Чтобы начать, добавьте пакеты NuGet ПО промежуточного слоя OWIN в проект с помощью консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="6b58d-135">To begin, add the OWIN middleware NuGet packages to the project by using the Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="6b58d-136">Чтобы добавить класс запуска OWIN в проект с именем `Startup.cs`, щелкните этот проект правой кнопкой мыши, выберите **Добавить**, затем выберите **Новый элемент** и найдите **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="6b58d-136">To add an OWIN Startup class to the project called `Startup.cs`, right-click the project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="6b58d-137">При запуске приложения ПО промежуточного слоя OWIN вызывает метод **Configuration(...)**.</span><span class="sxs-lookup"><span data-stu-id="6b58d-137">The OWIN middleware invokes the **Configuration(...)** method when the app starts.</span></span>
3. <span data-ttu-id="6b58d-138">Замените объявление класса `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="6b58d-138">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="6b58d-139">Часть этого класса уже была реализована в другом файле.</span><span class="sxs-lookup"><span data-stu-id="6b58d-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="6b58d-140">В методе **Configuration(...)** отправьте вызов в **ConfigureAuth(...)**, чтобы настроить аутентификацию для приложения.</span><span class="sxs-lookup"><span data-stu-id="6b58d-140">In the **Configuration(...)** method, make a call to **ConfgureAuth(...)** to set up authentication for the app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="6b58d-141">Откройте файл App_Start\Startup.Auth.cs, а затем реализуйте метод **ConfigureAuth(...)**.</span><span class="sxs-lookup"><span data-stu-id="6b58d-141">Open the App_Start\Startup.Auth.cs file, and then implement the **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="6b58d-142">Параметры, указанные в *OpenIDConnectAuthenticationOptions*, будут служить координатами приложения для взаимодействия с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b58d-142">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the app to communicate with Azure AD.</span></span> <span data-ttu-id="6b58d-143">Также необходимо настроить аутентификацию на основе файлов cookie, так как ПО промежуточного слоя OpenID Connect использует файлы cookie в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="6b58d-143">You also need to set up cookie authentication, because the OpenID Connect middleware uses cookies in the background.</span></span>

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. <span data-ttu-id="6b58d-144">Откройте файл web.config в корне проекта, а затем введите значения конфигурации в разделе `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="6b58d-144">Open the web.config file in the root of the project, and then enter the configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="6b58d-145">`ida:ClientId`: GUID, скопированный с портала Azure на шаге 1 (Регистрация нового приложения в Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b58d-145">`ida:ClientId`: The GUID you copied from the Azure portal in "Step 1: Register the new app with Azure AD."</span></span>
  * <span data-ttu-id="6b58d-146">`ida:Tenant`: имя вашего клиента Azure AD (например, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="6b58d-146">`ida:Tenant`: The name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="6b58d-147">`ida:PostLogoutRedirectUri`: индикатор, указывающий системе Azure AD, куда должен перенаправляться пользователь после успешного выполнения запроса выхода.</span><span class="sxs-lookup"><span data-stu-id="6b58d-147">`ida:PostLogoutRedirectUri`: The indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="6b58d-148">Шаг 3. Использование OWIN для выдачи запросов входа и выхода в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b58d-148">Step 3: Use OWIN to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="6b58d-149">Теперь приложение правильно настроено для взаимодействия с Azure AD с использованием протокола проверки подлинности OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="6b58d-149">The app is now properly configured to communicate with Azure AD by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="6b58d-150">OWIN полностью возьмет на себя выполнение процессов создания сообщений аутентификации, проверки маркеров из Azure AD и поддержки сеансов пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b58d-150">OWIN has handled all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="6b58d-151">Остается лишь предоставить пользователям возможность выполнять вход и выход.</span><span class="sxs-lookup"><span data-stu-id="6b58d-151">All that remains is to give your users a way to sign in and sign out.</span></span>

1. <span data-ttu-id="6b58d-152">Вы можете использовать теги авторизации в своих контроллерах, чтобы обязать пользователей выполнять вход перед доступом к конкретным страницам.</span><span class="sxs-lookup"><span data-stu-id="6b58d-152">You can use authorize tags in your controllers to require users to sign in before they access certain pages.</span></span> <span data-ttu-id="6b58d-153">Для этого откройте файл Controllers\HomeController.cs и добавьте тег `[Authorize]` в контроллер About.</span><span class="sxs-lookup"><span data-stu-id="6b58d-153">To do so, open Controllers\HomeController.cs, and then add the `[Authorize]` tag to the About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="6b58d-154">Вы также можете использовать OWIN для выдачи запросов проверки подлинности прямо из своего кода.</span><span class="sxs-lookup"><span data-stu-id="6b58d-154">You can also use OWIN to directly issue authentication requests from within your code.</span></span> <span data-ttu-id="6b58d-155">Для этого откройте файл Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="6b58d-155">To do so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="6b58d-156">Затем в действиях SignIn() и SignOut() выдавайте соответственно запросы входа и выхода из OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="6b58d-156">Then, in the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. <span data-ttu-id="6b58d-157">Откройте файл Views\Shared\_LoginPartial.cshtml, чтобы показывать пользователю ссылки для входа и выхода из приложения, а также отображать имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b58d-157">Open Views\Shared\_LoginPartial.cshtml to show the user the app sign-in and sign-out links, and to print out the user's name in a view.</span></span>

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
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

## <a name="step-4-display-user-information"></a><span data-ttu-id="6b58d-158">Шаг 4. Отображение сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="6b58d-158">Step 4: Display user information</span></span>
<span data-ttu-id="6b58d-159">При аутентификации пользователей с помощью OpenID Connect служба Azure AD возвращает в приложение маркер id_token, который содержит "утверждения" о пользователе.</span><span class="sxs-lookup"><span data-stu-id="6b58d-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token to the app that contains "claims," or assertions about the user.</span></span> <span data-ttu-id="6b58d-160">Эти утверждения можно использовать для настройки приложения. Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6b58d-160">You can use these claims to personalize the app by doing the following:</span></span>

1. <span data-ttu-id="6b58d-161">Откройте файл Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="6b58d-161">Open the Controllers\HomeController.cs file.</span></span> <span data-ttu-id="6b58d-162">Для доступа к утверждениям о пользователе в своих контроллерах можно использовать объект субъекта безопасности `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="6b58d-162">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. <span data-ttu-id="6b58d-163">Выполните сборку и запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="6b58d-163">Build and run the app.</span></span> <span data-ttu-id="6b58d-164">Если вы еще этого не сделали, то создайте пользователя в своем клиенте с доменом onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="6b58d-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is the time to do so.</span></span> <span data-ttu-id="6b58d-165">Этот процесс описывается далее.</span><span class="sxs-lookup"><span data-stu-id="6b58d-165">Here's how:</span></span>

  <span data-ttu-id="6b58d-166">а.</span><span class="sxs-lookup"><span data-stu-id="6b58d-166">a.</span></span> <span data-ttu-id="6b58d-167">Выполните вход от имени этого пользователя и обратите внимание на то, как удостоверение пользователя отображается на верхней панели.</span><span class="sxs-lookup"><span data-stu-id="6b58d-167">Sign in with that user, and note how the user's identity is reflected on the top bar.</span></span>

  <span data-ttu-id="6b58d-168">b.</span><span class="sxs-lookup"><span data-stu-id="6b58d-168">b.</span></span> <span data-ttu-id="6b58d-169">Выйдите, а затем снова войдите от имени другого пользователя в своем клиенте.</span><span class="sxs-lookup"><span data-stu-id="6b58d-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="6b58d-170">c.</span><span class="sxs-lookup"><span data-stu-id="6b58d-170">c.</span></span> <span data-ttu-id="6b58d-171">Если у вас серьезные цели, зарегистрируйте и запустите другой экземпляр данного приложения (с его собственным clientId) и рассмотрите процесс единого входа в действии.</span><span class="sxs-lookup"><span data-stu-id="6b58d-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b58d-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6b58d-172">Next steps</span></span>
<span data-ttu-id="6b58d-173">Для справки просмотрите [готовый пример](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (без ваших значений конфигурации).</span><span class="sxs-lookup"><span data-stu-id="6b58d-173">For reference, see [the completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="6b58d-174">Теперь можно перейти к более сложным темам.</span><span class="sxs-lookup"><span data-stu-id="6b58d-174">You can now move on to more advanced topics.</span></span> <span data-ttu-id="6b58d-175">Например, попробуйте использовать [защиту веб-API с помощью Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="6b58d-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
