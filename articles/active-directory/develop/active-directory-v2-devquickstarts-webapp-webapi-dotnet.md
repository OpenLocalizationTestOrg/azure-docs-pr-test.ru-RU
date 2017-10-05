---
title: "Начало работы с веб-приложением Azure AD v2.0 .NET с поддержкой вызова API | Документация Майкрософт"
description: "Как создать веб-приложение .NET MVC, вызывающее веб-службы, используя личные учетные записи Майкрософт, а также рабочие и учебные учетные записи для входа."
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
ms.openlocfilehash: dc3162ae8e6ce622139125c2e78fa45d2e90d534
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="57727-103">Вызов веб-API из веб-приложения .NET</span><span class="sxs-lookup"><span data-stu-id="57727-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="57727-104">Конечная точка версии 2.0 позволяет быстро реализовать в веб-приложениях и веб-API аутентификацию с поддержкой личных учетных записей Майкрософт, а также рабочих и учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="57727-104">With the v2.0 endpoint, you can quickly add authentication to your web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="57727-105">Мы создадим веб-приложение MVC, которое поддерживает вход пользователей с помощью OpenID Connect с использованием ПО промежуточного слоя OWIN Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="57727-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="57727-106">Веб-приложение будет получать маркеры доступа OAuth 2.0 для веб-API, защищенного OAuth 2.0, который позволяет создавать, читать и удалять элементы "списка дел" данного пользователя.</span><span class="sxs-lookup"><span data-stu-id="57727-106">The web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="57727-107">Этот учебник в основном посвящен применению MSAL для получения и использования маркеров доступа в веб-приложении, что полностью описано [здесь](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="57727-107">This tutorial will focus primarily on using MSAL to acquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="57727-108">Для начала вам может потребоваться изучить, как [добавить базовые возможности входа в веб-приложение](active-directory-v2-devquickstarts-dotnet-web.md) или как [правильно защитить веб-API](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="57727-108">As prerequisites, you may want to first learn how to [add basic sign-in to a web app](active-directory-v2-devquickstarts-dotnet-web.md) or how to [properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="57727-109">Не все сценарии и компоненты Azure Active Directory поддерживаются конечной точкой версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="57727-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="57727-110">Чтобы определить, следует ли вам использовать конечную точку версии 2.0, ознакомьтесь с [ограничениями версии 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="57727-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="57727-111">Скачивание примера кода</span><span class="sxs-lookup"><span data-stu-id="57727-111">Download sample code</span></span>
<span data-ttu-id="57727-112">Код в этом учебнике размещен на портале [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="57727-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="57727-113">Для понимания процесса можно [скачать основу приложения как ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) или клонировать ее:</span><span class="sxs-lookup"><span data-stu-id="57727-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="57727-114">Кроме того, можно [скачать завершенное приложение как ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) или клонировать его.</span><span class="sxs-lookup"><span data-stu-id="57727-114">Alternatively, you can [download the completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone the completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="57727-115">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="57727-115">Register an app</span></span>
<span data-ttu-id="57727-116">Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="57727-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="57727-117">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="57727-117">Make sure to:</span></span>

* <span data-ttu-id="57727-118">Запишите назначенный вашему приложению **идентификатор приложения**. Он вскоре вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="57727-118">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="57727-119">Создайте **секрет приложения** типа **Пароль** и скопируйте его для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="57727-119">Create an **App Secret** of the **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="57727-120">Добавьте **веб-платформу** для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="57727-120">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="57727-121">Введите правильный **универсальный код ресурса (URI) перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="57727-121">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="57727-122">URI перенаправления сообщает Azure AD, куда следует направлять ответы проверки подлинности. Значение по умолчанию в этом руководстве — `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="57727-122">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="57727-123">Установка OWIN</span><span class="sxs-lookup"><span data-stu-id="57727-123">Install OWIN</span></span>
<span data-ttu-id="57727-124">Добавьте пакеты NuGet для ПО промежуточного слоя OWIN в проект `TodoList-WebApp` с помощью консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="57727-124">Add the OWIN middleware NuGet packages to the `TodoList-WebApp` project using the Package Manager Console.</span></span>  <span data-ttu-id="57727-125">Кроме прочего, ПО промежуточного слоя OWIN будет использоваться для выдачи запросов входа и выхода, управления сеансом пользователя и получения сведений о пользователе.</span><span class="sxs-lookup"><span data-stu-id="57727-125">The OWIN middleware will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-the-user-in"></a><span data-ttu-id="57727-126">Вход пользователя</span><span class="sxs-lookup"><span data-stu-id="57727-126">Sign the user in</span></span>
<span data-ttu-id="57727-127">Теперь настройте ПО промежуточного слоя OWIN для использования [протокола аутентификации OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="57727-127">Now configure the OWIN middleware to use the [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="57727-128">Откройте файл `web.config` в корне проекта `TodoList-WebApp` и введите значения конфигурации приложения в разделе `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="57727-128">Open the `web.config` file in the root of the `TodoList-WebApp` project, and enter your app's configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="57727-129">`ida:ClientId` — это **идентификатор приложения** , присвоенный приложению на портале регистрации.</span><span class="sxs-lookup"><span data-stu-id="57727-129">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="57727-130">`ida:ClientSecret` — это **секрет приложения** , созданный на портале регистрации.</span><span class="sxs-lookup"><span data-stu-id="57727-130">The `ida:ClientSecret` is the **App Secret** you created in the registration portal.</span></span>
  * <span data-ttu-id="57727-131">`ida:RedirectUri` — это **универсальный код ресурса (URI) перенаправления** , который вы указали на портале.</span><span class="sxs-lookup"><span data-stu-id="57727-131">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>
* <span data-ttu-id="57727-132">Откройте файл `web.config` в корневом каталоге проекта `TodoList-Service` и замените `ida:Audience` **идентификатором приложения**, указанным выше.</span><span class="sxs-lookup"><span data-stu-id="57727-132">Open the `web.config` file in the root of the `TodoList-Service` project, and replace the `ida:Audience` with the same **Application Id** as above.</span></span>
* <span data-ttu-id="57727-133">Откройте файл `App_Start\Startup.Auth.cs` и добавьте операторы `using` для библиотек, указанных выше.</span><span class="sxs-lookup"><span data-stu-id="57727-133">Open the file `App_Start\Startup.Auth.cs` and add `using` statements for the libraries from above.</span></span>
* <span data-ttu-id="57727-134">В том же файле реализуйте метод `ConfigureAuth(...)` .</span><span class="sxs-lookup"><span data-stu-id="57727-134">In the same file, implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="57727-135">Параметры, указанные в `OpenIDConnectAuthenticationOptions` , будут служить координатами приложения для взаимодействия с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57727-135">The parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

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
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // The `AuthorizationCodeReceived` notification is used to capture and redeem the authorization_code that the v2.0 endpoint returns to your app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-to-get-access-tokens"></a><span data-ttu-id="57727-136">Использование MSAL для получения маркеров доступа</span><span class="sxs-lookup"><span data-stu-id="57727-136">Use MSAL to get access tokens</span></span>
<span data-ttu-id="57727-137">В уведомлении `AuthorizationCodeReceived` мы будем использовать [OAuth 2.0 вместе с OpenID Connect](active-directory-v2-protocols.md), чтобы использовать код авторизации маркера доступа для службы списка дел.</span><span class="sxs-lookup"><span data-stu-id="57727-137">In the `AuthorizationCodeReceived` notification, we want to use [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) to redeem the authorization_code for an access token to the To-Do List Service.</span></span>  <span data-ttu-id="57727-138">MSAL может упростить этот процесс.</span><span class="sxs-lookup"><span data-stu-id="57727-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="57727-139">Сначала установите предварительную версию MSAL:</span><span class="sxs-lookup"><span data-stu-id="57727-139">First, install the preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="57727-140">Добавьте еще один оператор `using` в файл `App_Start\Startup.Auth.cs` для MSAL.</span><span class="sxs-lookup"><span data-stu-id="57727-140">And add another `using` statement to the `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="57727-141">Теперь добавьте новый метод `OnAuthorizationCodeReceived` обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="57727-141">Now add a new method, the `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="57727-142">Этот обработчик обращается к MSAL для получения маркера доступа к API списка дел и сохраняет этот маркер в кэше маркеров MSAL для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="57727-142">This handler will use MSAL to acquire an access token to the To-Do List API, and will store the token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="57727-143">В веб-приложениях MSAL использует расширяемый кэш маркеров, который можно применять для хранения маркеров.</span><span class="sxs-lookup"><span data-stu-id="57727-143">In web apps, MSAL has an extensible token cache that can be used to store tokens.</span></span>  <span data-ttu-id="57727-144">В этом примере реализуется `NaiveSessionCache` , использующий хранилище сеансов HTTP для кэширования маркеров.</span><span class="sxs-lookup"><span data-stu-id="57727-144">This sample implements the `NaiveSessionCache` which uses http session storage to cache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-the-web-api"></a><span data-ttu-id="57727-145">Вызов веб-API</span><span class="sxs-lookup"><span data-stu-id="57727-145">Call the Web API</span></span>
<span data-ttu-id="57727-146">Теперь настало время использовать маркер доступа, полученный на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="57727-146">Now it's time to actually use the access_token you acquired in step 3.</span></span>  <span data-ttu-id="57727-147">Откройте файл `Controllers\TodoListController.cs` веб-приложения, который выполняет все запросы CRUD к интерфейсу API списка дел.</span><span class="sxs-lookup"><span data-stu-id="57727-147">Open the web app's `Controllers\TodoListController.cs` file, which makes all the CRUD requests to the To-Do List API.</span></span>

* <span data-ttu-id="57727-148">Здесь снова можно использовать MSAL маркеров доступа из кэша MSAL.</span><span class="sxs-lookup"><span data-stu-id="57727-148">You can use MSAL again here to fetch access_tokens from the MSAL cache.</span></span>  <span data-ttu-id="57727-149">Сначала добавьте оператор `using` для MSAL в этот файл.</span><span class="sxs-lookup"><span data-stu-id="57727-149">First, add a `using` statement for MSAL to this file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="57727-150">В действии `Index` используйте метод `AcquireTokenSilentAsync` MSAL, чтобы получить маркер доступа, который может использоваться для чтения данных из службы списка дел.</span><span class="sxs-lookup"><span data-stu-id="57727-150">In the `Index` action, use MSAL's `AcquireTokenSilentAsync` method to get an access_token that can be used to read data from the To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="57727-151">Затем пример добавляет полученный маркер в запрос HTTP GET в качестве заголовка `Authorization`, который служба списка дел использует для проверки подлинности запроса.</span><span class="sxs-lookup"><span data-stu-id="57727-151">The sample then adds the resulting token to the HTTP GET request as the `Authorization` header, which the To-Do List service uses to authenticate the request.</span></span>
* <span data-ttu-id="57727-152">Если служба списка дел возвращает ответ `401 Unauthorized`, это значит, что по какой-то причине маркеры доступа в MSAL стали недействительными.</span><span class="sxs-lookup"><span data-stu-id="57727-152">If the To-Do List service returns a `401 Unauthorized` response, the access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="57727-153">В этом случае следует удалить все маркеры доступа из кэша MSAL и показать пользователю сообщение о том, что требуется снова войти в систему. После этого входа перезапускается поток получения маркера.</span><span class="sxs-lookup"><span data-stu-id="57727-153">In this case, you should drop any access_tokens from the MSAL cache and show the user a message that they may need to sign in again, which will restart the token acquisition flow.</span></span>

```C#
// ...
// If the call failed with access denied, then drop the current access token from the cache,
// and show the user an error indicating they might need to sign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need to sign in again.");
}
// ...
```

* <span data-ttu-id="57727-154">Аналогично, если MSAL не удалось вернуть маркер доступа по какой-либо причине, следует сообщить пользователю о необходимости повторного входа.</span><span class="sxs-lookup"><span data-stu-id="57727-154">Similarly, if MSAL is unable to return an access_token for any reason, you should instruct the user to sign in again.</span></span>  <span data-ttu-id="57727-155">Для этого нужно всего лишь перехватить любой `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="57727-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show the user an error indicating they might need to sign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading To Do List: " + ee.Message + " You might need to log out and log back in.");
}
// ...
```

* <span data-ttu-id="57727-156">Такой же вызов `AcquireTokenSilentAsync` реализован в действиях `Create` и `Delete`.</span><span class="sxs-lookup"><span data-stu-id="57727-156">The exact same `AcquireTokenSilentAsync` call is implementd in the `Create` and `Delete` actions.</span></span>  <span data-ttu-id="57727-157">В веб-приложениях этот метод MSAL можно использовать для получения маркеров доступа, когда они требуются в приложении.</span><span class="sxs-lookup"><span data-stu-id="57727-157">In web apps, you can use this MSAL method to get access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="57727-158">MSAL получает, кэширует и обновляет маркеры для вас.</span><span class="sxs-lookup"><span data-stu-id="57727-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="57727-159">Наконец, постройте и запустите свое приложение!</span><span class="sxs-lookup"><span data-stu-id="57727-159">Finally, build and run your app!</span></span>  <span data-ttu-id="57727-160">Выполните вход с учетной записью Майкрософт или учетной записью Azure AD и обратите внимание на то, как удостоверение пользователя отображается в верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="57727-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="57727-161">Добавьте и удалите несколько элементов из списка дел пользователя, чтобы увидеть защищенные с помощью OAuth 2.0 вызовы API в действии.</span><span class="sxs-lookup"><span data-stu-id="57727-161">Add and delete some items from the user's To-Do List to see the OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="57727-162">Теперь у вас есть веб-приложение и веб-API, защищенные с помощью стандартных отраслевых протоколов, которые могут проверять подлинность пользователей с помощью личных, рабочих и учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="57727-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="57727-163">Для справки следует отметить, что готовый пример (без ваших значений конфигурации) находится [здесь](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="57727-163">For reference, the completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="57727-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="57727-164">Next Steps</span></span>
<span data-ttu-id="57727-165">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="57727-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="57727-166">Руководство разработчика версии 2.0 >></span><span class="sxs-lookup"><span data-stu-id="57727-166">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="57727-167">Тег StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="57727-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="57727-168">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="57727-168">Get security updates for our products</span></span>
<span data-ttu-id="57727-169">Рекомендуем вам настроить уведомления о нарушениях безопасности. Это можно сделать, подписавшись на уведомления безопасности консультационных служб на [этой странице](https://technet.microsoft.com/security/dd252948).</span><span class="sxs-lookup"><span data-stu-id="57727-169">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

