---
title: "aaaAzure AD v2.0 .NET, веб-приложения вызовах API Приступая к работе | Документы Microsoft"
description: "Как toobuild веб-приложение .NET MVC, который вызывает веб-службы с помощью Microsoft личных учетных записей и работы или учебы учетные записи для входа в систему."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1a70791418bc2a7d1fdfbafb9b5126a033a32292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="167de-103">Вызов веб-API из веб-приложения .NET</span><span class="sxs-lookup"><span data-stu-id="167de-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="167de-104">С конечной точкой v2.0 hello можно быстро добавлять проверки подлинности tooyour веб-приложений и веб-API с поддержки для обоих личных учетных записей Майкрософт и рабочих учетных записей.</span><span class="sxs-lookup"><span data-stu-id="167de-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="167de-105">Мы создадим веб-приложение MVC, которое поддерживает вход пользователей с помощью OpenID Connect с использованием ПО промежуточного слоя OWIN Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="167de-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="167de-106">Hello веб-приложения получение маркера доступа OAuth 2.0 для веб-api, защищенного OAuth 2.0, которая позволяет создавать, читать и delete для данного пользователя «список дел».</span><span class="sxs-lookup"><span data-stu-id="167de-106">hello web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="167de-107">Этот учебник будет связана главным образом с использованием MSAL tooacquire и использовать токены доступа в веб-приложения, описанные в полном объеме [здесь](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="167de-107">This tutorial will focus primarily on using MSAL tooacquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="167de-108">В качестве необходимых компонентов, вы можете toofirst Узнайте, каким образом слишком[добавить основные tooa веб-приложения](active-directory-v2-devquickstarts-dotnet-web.md) или как слишком[правильно обеспечить безопасность веб-API](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="167de-108">As prerequisites, you may want toofirst learn how too[add basic sign-in tooa web app](active-directory-v2-devquickstarts-dotnet-web.md) or how too[properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="167de-109">Не все сценарии Azure Active Directory и возможности поддерживаются hello v2.0 конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="167de-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="167de-110">toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="167de-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="167de-111">Скачивание примера кода</span><span class="sxs-lookup"><span data-stu-id="167de-111">Download sample code</span></span>
<span data-ttu-id="167de-112">поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="167de-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="167de-113">можно toofollow вдоль [загрузить приложение hello основу как .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) или основу hello клона:</span><span class="sxs-lookup"><span data-stu-id="167de-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="167de-114">Кроме того, можно [загрузить приложение hello завершена как .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) или hello выполнить клонирование приложений:</span><span class="sxs-lookup"><span data-stu-id="167de-114">Alternatively, you can [download hello completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone hello completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="167de-115">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="167de-115">Register an app</span></span>
<span data-ttu-id="167de-116">Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="167de-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="167de-117">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="167de-117">Make sure to:</span></span>

* <span data-ttu-id="167de-118">Копировать вниз hello **идентификатор приложения** назначены tooyour приложения, оно понадобится скоро.</span><span class="sxs-lookup"><span data-stu-id="167de-118">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="167de-119">Создание **секрет приложения** из hello **пароль** тип и копирования вниз его значение на более поздний срок</span><span class="sxs-lookup"><span data-stu-id="167de-119">Create an **App Secret** of hello **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="167de-120">Добавить hello **Web** платформы для приложения.</span><span class="sxs-lookup"><span data-stu-id="167de-120">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="167de-121">Введите правильный hello **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="167de-121">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="167de-122">Hello uri перенаправления указывает tooAzure AD, где следует направлять запросы проверки подлинности — по умолчанию hello в этом учебнике используется `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="167de-122">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="167de-123">Установка OWIN</span><span class="sxs-lookup"><span data-stu-id="167de-123">Install OWIN</span></span>
<span data-ttu-id="167de-124">Добавление пакетов NuGet toohello для hello OWIN по промежуточного слоя `TodoList-WebApp` проектов с помощью консоли диспетчера пакетов "hello".</span><span class="sxs-lookup"><span data-stu-id="167de-124">Add hello OWIN middleware NuGet packages toohello `TodoList-WebApp` project using hello Package Manager Console.</span></span>  <span data-ttu-id="167de-125">по промежуточного слоя OWIN Hello быть используется tooissue запросы на вход и выход, управлять сеансом пользователя hello и получения сведений о пользователе hello, среди прочего.</span><span class="sxs-lookup"><span data-stu-id="167de-125">hello OWIN middleware will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a><span data-ttu-id="167de-126">Вход пользователя hello в</span><span class="sxs-lookup"><span data-stu-id="167de-126">Sign hello user in</span></span>
<span data-ttu-id="167de-127">Теперь настройка hello toouse по промежуточного слоя OWIN hello [протокол проверки подлинности OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="167de-127">Now configure hello OWIN middleware toouse hello [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="167de-128">Откройте hello `web.config` файл в корне hello hello `TodoList-WebApp` проекта, а затем введите значения конфигурации приложения в hello `<appSettings>` раздела.</span><span class="sxs-lookup"><span data-stu-id="167de-128">Open hello `web.config` file in hello root of hello `TodoList-WebApp` project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="167de-129">Hello `ida:ClientId` — hello **идентификатор приложения** назначенный tooyour приложения на портале регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="167de-129">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="167de-130">Hello `ida:ClientSecret` — hello **секрет приложения** вы создали на портале регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="167de-130">hello `ida:ClientSecret` is hello **App Secret** you created in hello registration portal.</span></span>
  * <span data-ttu-id="167de-131">Hello `ida:RedirectUri` — hello **Uri перенаправления** введенное на портале hello.</span><span class="sxs-lookup"><span data-stu-id="167de-131">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>
* <span data-ttu-id="167de-132">Откройте hello `web.config` файл в корне hello hello `TodoList-Service` проекта, а hello `ida:Audience` с hello же **идентификатор приложения** как описано выше.</span><span class="sxs-lookup"><span data-stu-id="167de-132">Open hello `web.config` file in hello root of hello `TodoList-Service` project, and replace hello `ida:Audience` with hello same **Application Id** as above.</span></span>
* <span data-ttu-id="167de-133">Привет открыть файл `App_Start\Startup.Auth.cs` и добавьте `using` инструкций для библиотек hello выше.</span><span class="sxs-lookup"><span data-stu-id="167de-133">Open hello file `App_Start\Startup.Auth.cs` and add `using` statements for hello libraries from above.</span></span>
* <span data-ttu-id="167de-134">В hello того же файла, реализовать hello `ConfigureAuth(...)` метод.</span><span class="sxs-lookup"><span data-stu-id="167de-134">In hello same file, implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="167de-135">Здравствуйте, параметры, указываемые в `OpenIDConnectAuthenticationOptions` будет служить в качестве координат для toocommunicate вашего приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="167de-135">hello parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

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
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // hello `AuthorizationCodeReceived` notification is used toocapture and redeem hello authorization_code that hello v2.0 endpoint returns tooyour app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-tooget-access-tokens"></a><span data-ttu-id="167de-136">Использование маркера доступа tooget MSAL</span><span class="sxs-lookup"><span data-stu-id="167de-136">Use MSAL tooget access tokens</span></span>
<span data-ttu-id="167de-137">В hello `AuthorizationCodeReceived` уведомления, мы хотим toouse [OAuth 2.0 в сочетании с OpenID Connect](active-directory-v2-protocols.md) значение authorization_code hello tooredeem для токена toohello доступ службы списка задач.</span><span class="sxs-lookup"><span data-stu-id="167de-137">In hello `AuthorizationCodeReceived` notification, we want toouse [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code for an access token toohello To-Do List Service.</span></span>  <span data-ttu-id="167de-138">MSAL может упростить этот процесс.</span><span class="sxs-lookup"><span data-stu-id="167de-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="167de-139">Во-первых установите предварительную версию hello MSAL:</span><span class="sxs-lookup"><span data-stu-id="167de-139">First, install hello preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="167de-140">И добавьте еще один `using` toohello инструкции `App_Start\Startup.Auth.cs` файл для MSAL.</span><span class="sxs-lookup"><span data-stu-id="167de-140">And add another `using` statement toohello `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="167de-141">Теперь добавьте новый метод hello `OnAuthorizationCodeReceived` обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="167de-141">Now add a new method, hello `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="167de-142">Этот обработчик будет использовать MSAL tooacquire toohello токена доступа к API список дел и сохранит hello маркера в кэше токенов MSAL на более поздний срок:</span><span class="sxs-lookup"><span data-stu-id="167de-142">This handler will use MSAL tooacquire an access token toohello To-Do List API, and will store hello token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="167de-143">В веб-приложениях MSAL имеет расширяемый кэш токена, может быть используется toostore маркеры.</span><span class="sxs-lookup"><span data-stu-id="167de-143">In web apps, MSAL has an extensible token cache that can be used toostore tokens.</span></span>  <span data-ttu-id="167de-144">В этом примере реализуется hello `NaiveSessionCache` с использованием маркеров toocache хранилища сеансов http.</span><span class="sxs-lookup"><span data-stu-id="167de-144">This sample implements hello `NaiveSessionCache` which uses http session storage toocache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a><span data-ttu-id="167de-145">Hello вызовов веб-API</span><span class="sxs-lookup"><span data-stu-id="167de-145">Call hello Web API</span></span>
<span data-ttu-id="167de-146">Теперь пора tooactually использовать access_token hello, полученного в шаге 3.</span><span class="sxs-lookup"><span data-stu-id="167de-146">Now it's time tooactually use hello access_token you acquired in step 3.</span></span>  <span data-ttu-id="167de-147">Привет открыть веб-приложение `Controllers\TodoListController.cs` файл, который делает все hello CRUD запросы toohello API список дел.</span><span class="sxs-lookup"><span data-stu-id="167de-147">Open hello web app's `Controllers\TodoListController.cs` file, which makes all hello CRUD requests toohello To-Do List API.</span></span>

* <span data-ttu-id="167de-148">Можно использовать MSAL попытку здесь access_tokens toofetch из hello MSAL кэша.</span><span class="sxs-lookup"><span data-stu-id="167de-148">You can use MSAL again here toofetch access_tokens from hello MSAL cache.</span></span>  <span data-ttu-id="167de-149">Сначала добавьте `using` инструкции для MSAL toothis файла.</span><span class="sxs-lookup"><span data-stu-id="167de-149">First, add a `using` statement for MSAL toothis file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="167de-150">В hello `Index` действия, используйте MSAL `AcquireTokenSilentAsync` tooget метод access_token, может быть используется tooread данные из hello список дел службы:</span><span class="sxs-lookup"><span data-stu-id="167de-150">In hello `Index` action, use MSAL's `AcquireTokenSilentAsync` method tooget an access_token that can be used tooread data from hello To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="167de-151">Hello образец добавляет hello полученный маркер toohello запроса HTTP GET на составляющие hello `Authorization` заголовок, какая служба список дел hello использует запрос tooauthenticate hello.</span><span class="sxs-lookup"><span data-stu-id="167de-151">hello sample then adds hello resulting token toohello HTTP GET request as hello `Authorization` header, which hello To-Do List service uses tooauthenticate hello request.</span></span>
* <span data-ttu-id="167de-152">Возвращает список дел службы hello `401 Unauthorized` ответ access_tokens hello в MSAL ставшие недействительными для какой-либо причине.</span><span class="sxs-lookup"><span data-stu-id="167de-152">If hello To-Do List service returns a `401 Unauthorized` response, hello access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="167de-153">В этом случае необходимо удалить все access_tokens из кэша MSAL hello и показывать hello пользовательского сообщения, может возникнуть необходимость toosign в снова, которой будет перезагружен hello получения маркера потока.</span><span class="sxs-lookup"><span data-stu-id="167de-153">In this case, you should drop any access_tokens from hello MSAL cache and show hello user a message that they may need toosign in again, which will restart hello token acquisition flow.</span></span>

```C#
// ...
// If hello call failed with access denied, then drop hello current access token from hello cache,
// and show hello user an error indicating they might need toosign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need toosign in again.");
}
// ...
```

* <span data-ttu-id="167de-154">Аналогично Если не удается tooreturn access_token MSAL по любой причине, toosign пользователя hello в следует поручить еще раз.</span><span class="sxs-lookup"><span data-stu-id="167de-154">Similarly, if MSAL is unable tooreturn an access_token for any reason, you should instruct hello user toosign in again.</span></span>  <span data-ttu-id="167de-155">Для этого нужно всего лишь перехватить любой `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="167de-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* <span data-ttu-id="167de-156">Hello точного же `AcquireTokenSilentAsync` вызывается implementd в hello `Create` и `Delete` действия.</span><span class="sxs-lookup"><span data-stu-id="167de-156">hello exact same `AcquireTokenSilentAsync` call is implementd in hello `Create` and `Delete` actions.</span></span>  <span data-ttu-id="167de-157">В веб-приложениях можно использовать этот access_tokens tooget метод MSAL всякий раз, когда они нужны в приложении.</span><span class="sxs-lookup"><span data-stu-id="167de-157">In web apps, you can use this MSAL method tooget access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="167de-158">MSAL получает, кэширует и обновляет маркеры для вас.</span><span class="sxs-lookup"><span data-stu-id="167de-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="167de-159">Наконец, постройте и запустите свое приложение!</span><span class="sxs-lookup"><span data-stu-id="167de-159">Finally, build and run your app!</span></span>  <span data-ttu-id="167de-160">Войдите, используя учетную запись Майкрософт или учетной записи Azure AD и обратите внимание на то, как удостоверение пользователя hello отражается hello верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="167de-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="167de-161">Добавлять и удалять некоторые элементы из списка дел hello пользователь вызывает hello toosee прощелкать OAuth 2.0 API в действии.</span><span class="sxs-lookup"><span data-stu-id="167de-161">Add and delete some items from hello user's To-Do List toosee hello OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="167de-162">Теперь у вас есть веб-приложение и веб-API, защищенные с помощью стандартных отраслевых протоколов, которые могут проверять подлинность пользователей с помощью личных, рабочих и учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="167de-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="167de-163">Справочник по hello выполнить пример (без настройки) [представлена ниже](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="167de-163">For reference, hello completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="167de-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="167de-164">Next Steps</span></span>
<span data-ttu-id="167de-165">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="167de-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="167de-166">Руководство разработчика v2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="167de-166">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="167de-167">Тег StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="167de-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="167de-168">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="167de-168">Get security updates for our products</span></span>
<span data-ttu-id="167de-169">Мы рекомендуем вам уведомления при возникновении события безопасности, посетив tooget [эту страницу](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.</span><span class="sxs-lookup"><span data-stu-id="167de-169">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

