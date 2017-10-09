---
title: "Приступая к работе веб-приложение .NET aaaAzure AD | Документы Microsoft"
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
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="31206-103">Вход в веб-приложение ASP.NET и выход из него с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="31206-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="31206-104">Предоставив один вход и выход с помощью всего нескольких строк кода, Azure Active Directory (Azure AD) упрощает вы toooutsource веб-приложения диспетчера удостоверений.</span><span class="sxs-lookup"><span data-stu-id="31206-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you toooutsource web-app identity management.</span></span> <span data-ttu-id="31206-105">Можно подписать пользователей и из него веб-приложения ASP.NET с использованием реализации Microsoft Привет открыть веб-интерфейс для по промежуточного слоя .NET (OWIN).</span><span class="sxs-lookup"><span data-stu-id="31206-105">You can sign users in and out of ASP.NET web apps by using hello Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="31206-106">Поддерживаемое сообществом ПО промежуточного слоя OWIN включено в .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="31206-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="31206-107">В этой статье показано, как toouse OWIN для:</span><span class="sxs-lookup"><span data-stu-id="31206-107">This article shows how toouse OWIN to:</span></span>

* <span data-ttu-id="31206-108">Вход пользователей tooweb приложений с помощью Azure AD как поставщика удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="31206-108">Sign users in tooweb apps by using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="31206-109">отображать некоторые сведения о пользователе;</span><span class="sxs-lookup"><span data-stu-id="31206-109">Display some user information.</span></span>
* <span data-ttu-id="31206-110">Вход пользователей из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="31206-110">Sign users out of hello apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="31206-111">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="31206-111">Before you get started</span></span>
* <span data-ttu-id="31206-112">Загрузите hello [основу приложения](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) или загрузить hello [полного примера](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="31206-112">Download hello [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download hello [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="31206-113">Необходимо также клиент Azure AD, в которой приложение hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="31206-113">You also need an Azure AD tenant in which tooregister hello app.</span></span> <span data-ttu-id="31206-114">Если у вас еще нет клиента Azure AD, [Узнайте, как один tooget](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="31206-114">If you don't already have an Azure AD tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="31206-115">Когда будете готовы, выполните процедуры hello в hello рядом в четырех разделах.</span><span class="sxs-lookup"><span data-stu-id="31206-115">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-register-hello-new-app-with-azure-ad"></a><span data-ttu-id="31206-116">Шаг 1: Регистрация нового приложения hello в Azure AD</span><span class="sxs-lookup"><span data-stu-id="31206-116">Step 1: Register hello new app with Azure AD</span></span>
<span data-ttu-id="31206-117">tooset пользователей tooauthenticate приложения hello, зарегистрировать его в клиенте, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="31206-117">tooset up hello app tooauthenticate users, first register it in your tenant by doing hello following:</span></span>

1. <span data-ttu-id="31206-118">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31206-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="31206-119">На верхней панели hello щелкните имя вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="31206-119">On hello top bar, click your account name.</span></span> <span data-ttu-id="31206-120">В разделе hello **каталога** список, клиент Active Directory hello выберите нужное приложение hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="31206-120">Under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="31206-121">Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="31206-121">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="31206-122">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="31206-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="31206-123">Выполните hello предлагает toocreate новый **веб-приложение или WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="31206-123">Follow hello prompts toocreate a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="31206-124">**Имя** описывает toousers приложения hello.</span><span class="sxs-lookup"><span data-stu-id="31206-124">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="31206-125">**URL-адрес входа** hello базовый URL-адрес приложения hello.</span><span class="sxs-lookup"><span data-stu-id="31206-125">**Sign-On URL** is hello base URL of hello app.</span></span> <span data-ttu-id="31206-126">URL-адрес по умолчанию Hello основу — https://localhost:44320 /.</span><span class="sxs-lookup"><span data-stu-id="31206-126">hello skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="31206-127">После завершения регистрации hello Azure AD присваивает приложение hello уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="31206-127">After you've completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="31206-128">Скопируйте значение hello из toouse страницы приложения hello в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="31206-128">Copy hello value from hello app page toouse in hello next sections.</span></span>
7. <span data-ttu-id="31206-129">Из hello **параметры** -> **свойства** страницы приложения, обновите URI идентификатора приложения hello.</span><span class="sxs-lookup"><span data-stu-id="31206-129">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="31206-130">Hello **URI идентификатора приложения** — это уникальный идентификатор для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="31206-130">hello **App ID URI** is a unique identifier for hello app.</span></span> <span data-ttu-id="31206-131">Hello именования — `https://<tenant-domain>/<app-name>` (например, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="31206-131">hello naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="31206-132">Шаг 2: Настройка проверки подлинности конвейер OWIN hello hello приложения toouse</span><span class="sxs-lookup"><span data-stu-id="31206-132">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="31206-133">На этом шаге настраивается hello OWIN по промежуточного слоя toouse hello OpenID Connect протокол проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="31206-133">In this step, you configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="31206-134">Использование запросов OWIN tooissue входа и выхода, управлять сеансами пользователей, получить сведения о пользователе и т.д.</span><span class="sxs-lookup"><span data-stu-id="31206-134">You use OWIN tooissue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="31206-135">toobegin, добавить toohello hello OWIN по промежуточного слоя NuGet пакетов проекта с помощью консоли диспетчера пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="31206-135">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="31206-136">вызывается проект запуска OWIN класса toohello tooadd `Startup.cs`, щелкните правой кнопкой мыши проект hello, выберите **добавить**выберите **новый элемент**и выполните поиск **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="31206-136">tooadd an OWIN Startup class toohello project called `Startup.cs`, right-click hello project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="31206-137">по промежуточного слоя OWIN Hello вызывает hello **Configuration(...)**  метод при запуске приложение hello.</span><span class="sxs-lookup"><span data-stu-id="31206-137">hello OWIN middleware invokes hello **Configuration(...)** method when hello app starts.</span></span>
3. <span data-ttu-id="31206-138">Измените объявление класса hello слишком`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="31206-138">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="31206-139">Часть этого класса уже была реализована в другом файле.</span><span class="sxs-lookup"><span data-stu-id="31206-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="31206-140">В hello **Configuration(...)**  метод, вызвать слишком**ConfgureAuth(...)**  tooset проверку подлинности для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="31206-140">In hello **Configuration(...)** method, make a call too**ConfgureAuth(...)** tooset up authentication for hello app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="31206-141">Откройте файл App_Start\Startup.Auth.cs hello, а затем реализуйте hello **ConfigureAuth(...)**  метод.</span><span class="sxs-lookup"><span data-stu-id="31206-141">Open hello App_Start\Startup.Auth.cs file, and then implement hello **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="31206-142">Здравствуйте, параметры, указываемые в *OpenIDConnectAuthenticationOptions* служат в качестве координат для hello toocommunicate приложений с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31206-142">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello app toocommunicate with Azure AD.</span></span> <span data-ttu-id="31206-143">Необходимо также tooset копирование файла cookie проверки подлинности, так как по промежуточного слоя, OpenID Connect hello использует куки-файлы в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="31206-143">You also need tooset up cookie authentication, because hello OpenID Connect middleware uses cookies in hello background.</span></span>

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

5. <span data-ttu-id="31206-144">Откройте файл web.config hello в корневой hello hello проекта, а затем введите значения конфигурации hello в hello `<appSettings>` раздела.</span><span class="sxs-lookup"><span data-stu-id="31206-144">Open hello web.config file in hello root of hello project, and then enter hello configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="31206-145">`ida:ClientId`: hello GUID, был скопирован из hello портал Azure на «шаг 1: hello зарегистрировать новое приложение с Azure AD.»</span><span class="sxs-lookup"><span data-stu-id="31206-145">`ida:ClientId`: hello GUID you copied from hello Azure portal in "Step 1: Register hello new app with Azure AD."</span></span>
  * <span data-ttu-id="31206-146">`ida:Tenant`: hello имя вашего клиента Azure AD (например, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="31206-146">`ida:Tenant`: hello name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="31206-147">`ida:PostLogoutRedirectUri`: hello индикатор, который сообщает Azure AD, которому следует перенаправлять пользователя после успешного завершения запроса выхода.</span><span class="sxs-lookup"><span data-stu-id="31206-147">`ida:PostLogoutRedirectUri`: hello indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="31206-148">Шаг 3: Использование tooAzure AD запросов OWIN tooissue входа и выхода</span><span class="sxs-lookup"><span data-stu-id="31206-148">Step 3: Use OWIN tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="31206-149">приложение Hello сейчас правильно настроен toocommunicate с Azure AD с помощью протокола проверки подлинности OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="31206-149">hello app is now properly configured toocommunicate with Azure AD by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="31206-150">OWIN обработала все подробности hello отправляемого сообщения проверки подлинности, проверки токенов из Azure AD и поддержку пользовательских сеансов.</span><span class="sxs-lookup"><span data-stu-id="31206-150">OWIN has handled all of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="31206-151">Все, что остается является toogive пользователей toosign способом в и выхода.</span><span class="sxs-lookup"><span data-stu-id="31206-151">All that remains is toogive your users a way toosign in and sign out.</span></span>

1. <span data-ttu-id="31206-152">Можно использовать теги в toosign пользователей toorequire вашей контроллеров, в авторизации, перед доступом к некоторые страницы.</span><span class="sxs-lookup"><span data-stu-id="31206-152">You can use authorize tags in your controllers toorequire users toosign in before they access certain pages.</span></span> <span data-ttu-id="31206-153">toodo таким образом, откройте Controllers\HomeController.cs, а затем добавьте hello `[Authorize]` тега toohello о контроллере.</span><span class="sxs-lookup"><span data-stu-id="31206-153">toodo so, open Controllers\HomeController.cs, and then add hello `[Authorize]` tag toohello About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="31206-154">Также можно использовать запросов OWIN toodirectly проблема проверки подлинности из кода.</span><span class="sxs-lookup"><span data-stu-id="31206-154">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span> <span data-ttu-id="31206-155">toodo откройте Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="31206-155">toodo so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="31206-156">Затем в действиях SignIn() и SignOut() hello, выдавать запроса OpenID Connect и запросах на выход.</span><span class="sxs-lookup"><span data-stu-id="31206-156">Then, in hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

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

3. <span data-ttu-id="31206-157">Откройте одну\_LoginPartial.cshtml tooshow hello пользователя hello приложения входа и выхода ссылки и tooprint в представлении имя пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="31206-157">Open Views\Shared\_LoginPartial.cshtml tooshow hello user hello app sign-in and sign-out links, and tooprint out hello user's name in a view.</span></span>

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

## <a name="step-4-display-user-information"></a><span data-ttu-id="31206-158">Шаг 4. Отображение сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="31206-158">Step 4: Display user information</span></span>
<span data-ttu-id="31206-159">При проверке подлинности пользователей с OpenID Connect, Azure AD возвращает id_token toohello приложение, которое содержит «утверждения» или утверждения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="31206-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token toohello app that contains "claims," or assertions about hello user.</span></span> <span data-ttu-id="31206-160">Можно использовать приложение hello toopersonalize этих утверждений, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="31206-160">You can use these claims toopersonalize hello app by doing hello following:</span></span>

1. <span data-ttu-id="31206-161">Откройте файл Controllers\HomeController.cs hello.</span><span class="sxs-lookup"><span data-stu-id="31206-161">Open hello Controllers\HomeController.cs file.</span></span> <span data-ttu-id="31206-162">Можно использовать утверждения пользователей hello в контроллерах через hello `ClaimsPrincipal.Current` объект субъекта безопасности.</span><span class="sxs-lookup"><span data-stu-id="31206-162">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

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

2. <span data-ttu-id="31206-163">Постройте и запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="31206-163">Build and run hello app.</span></span> <span data-ttu-id="31206-164">Если уже еще не создан новый пользователь в клиенте с домен onmicrosoft.com, поэтому теперь является toodo время hello.</span><span class="sxs-lookup"><span data-stu-id="31206-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is hello time toodo so.</span></span> <span data-ttu-id="31206-165">Этот процесс описывается далее.</span><span class="sxs-lookup"><span data-stu-id="31206-165">Here's how:</span></span>

  <span data-ttu-id="31206-166">а.</span><span class="sxs-lookup"><span data-stu-id="31206-166">a.</span></span> <span data-ttu-id="31206-167">Вход пользователя и обратите внимание на то, как удостоверение пользователя hello отражается на верхней панели hello.</span><span class="sxs-lookup"><span data-stu-id="31206-167">Sign in with that user, and note how hello user's identity is reflected on hello top bar.</span></span>

  <span data-ttu-id="31206-168">b.</span><span class="sxs-lookup"><span data-stu-id="31206-168">b.</span></span> <span data-ttu-id="31206-169">Выйдите, а затем снова войдите от имени другого пользователя в своем клиенте.</span><span class="sxs-lookup"><span data-stu-id="31206-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="31206-170">c.</span><span class="sxs-lookup"><span data-stu-id="31206-170">c.</span></span> <span data-ttu-id="31206-171">Если у вас серьезные цели, зарегистрируйте и запустите другой экземпляр данного приложения (с его собственным clientId) и рассмотрите процесс единого входа в действии.</span><span class="sxs-lookup"><span data-stu-id="31206-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31206-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31206-172">Next steps</span></span>
<span data-ttu-id="31206-173">Справочную информацию см. в разделе [образец hello завершения](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (без настройки).</span><span class="sxs-lookup"><span data-stu-id="31206-173">For reference, see [hello completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="31206-174">Теперь можно переходить на toomore дополнительные разделы.</span><span class="sxs-lookup"><span data-stu-id="31206-174">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="31206-175">Например, попробуйте использовать [защиту веб-API с помощью Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="31206-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
