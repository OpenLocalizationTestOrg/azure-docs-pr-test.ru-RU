---
title: "aaaAzure Active Directory B2C | Документы Microsoft"
description: "Как toobuild .NET веб-приложения и вызова веб-api с помощью маркера доступа Azure Active Directory B2C и OAuth 2.0."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 9b248e3bf18968e12aae73c07083fa8278befb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="49d94-103">Azure AD B2C: вызов веб-API .NET из веб-приложения .NET</span><span class="sxs-lookup"><span data-stu-id="49d94-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="49d94-104">С помощью Azure AD B2C, можно добавить мощные удостоверение управления функции tooyour веб-приложений и веб-API.</span><span class="sxs-lookup"><span data-stu-id="49d94-104">By using Azure AD B2C, you can add powerful identity management features tooyour web apps and web APIs.</span></span> <span data-ttu-id="49d94-105">В этой статье описывается, как toorequest маркеры доступа и выполнять вызовы из .NET «список дел» веб-tooa приложения .NET, веб-api.</span><span class="sxs-lookup"><span data-stu-id="49d94-105">This article discusses how toorequest access tokens and make calls from a .NET "to-do list" web app tooa .NET web api.</span></span>

<span data-ttu-id="49d94-106">Данная статья не охватывает как tooimplement вход, регистрации и управления с помощью Azure AD B2C профиля.</span><span class="sxs-lookup"><span data-stu-id="49d94-106">This article does not cover how tooimplement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="49d94-107">Этот раздел посвящен вызовах веб-API после hello пользователь уже прошел проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="49d94-107">It focuses on calling web APIs after hello user is already authenticated.</span></span> <span data-ttu-id="49d94-108">Если это еще не сделано, необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="49d94-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="49d94-109">Изучите начало работы с [веб-приложением .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="49d94-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="49d94-110">Изучите начало работы с [веб-API .NET](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="49d94-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="49d94-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="49d94-111">Prerequisite</span></span>

<span data-ttu-id="49d94-112">toobuild веб-приложение, которое вызывает веб-api, необходимо:</span><span class="sxs-lookup"><span data-stu-id="49d94-112">toobuild a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="49d94-113">[Создайте клиента Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="49d94-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="49d94-114">[Зарегистрируйте веб-API](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="49d94-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="49d94-115">[Зарегистрируйте веб-приложение](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="49d94-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="49d94-116">[Настройте политики](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="49d94-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="49d94-117">[Предоставление hello web app разрешения toouse hello веб-api](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="49d94-117">[Grant hello web app permissions toouse hello web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49d94-118">клиентское приложение Hello и веб-API необходимо использовать каталог B2C hello же Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49d94-118">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="download-hello-code"></a><span data-ttu-id="49d94-119">Загрузка кода hello</span><span class="sxs-lookup"><span data-stu-id="49d94-119">Download hello code</span></span>

<span data-ttu-id="49d94-120">Hello кода для этого учебника, сохраняется на [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="49d94-120">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="49d94-121">Образец hello можно клонировать, выполнив:</span><span class="sxs-lookup"><span data-stu-id="49d94-121">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="49d94-122">После загрузки кода образца hello запущен tooget файл .sln Visual Studio откройте hello.</span><span class="sxs-lookup"><span data-stu-id="49d94-122">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="49d94-123">Hello файл решения содержит два проекта: `TaskWebApp` и `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="49d94-123">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="49d94-124">`TaskWebApp`— веб-приложение MVC, hello пользователь взаимодействует с.</span><span class="sxs-lookup"><span data-stu-id="49d94-124">`TaskWebApp` is a MVC web application that hello user interacts with.</span></span> <span data-ttu-id="49d94-125">`TaskService`— приложение hello фоновая веб-API, который хранит список дел каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="49d94-125">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="49d94-126">Данная статья не охватывает hello построение `TaskWebApp` веб-приложения или hello `TaskService` веб-api.</span><span class="sxs-lookup"><span data-stu-id="49d94-126">This article does not cover building hello `TaskWebApp` web app or hello `TaskService` web api.</span></span> <span data-ttu-id="49d94-127">toolearn toobuild hello .NET, веб-приложения с помощью Azure AD B2C разделе нашей [учебник по .NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="49d94-127">toolearn how toobuild hello .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="49d94-128">toolearn как toobuild hello .NET веб-API, защищенного с помощью Azure AD B2C см. наш [учебника веб-API .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="49d94-128">toolearn how toobuild hello .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="49d94-129">Обновите конфигурацию hello Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="49d94-129">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="49d94-130">Выборка — настроенное toouse hello политик и клиент идентификатор нашей демонстрационному клиенту.</span><span class="sxs-lookup"><span data-stu-id="49d94-130">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="49d94-131">Если вы хотите toouse своим собственным клиентом:</span><span class="sxs-lookup"><span data-stu-id="49d94-131">If you would like toouse your own tenant:</span></span>

1. <span data-ttu-id="49d94-132">Откройте `web.config` в hello `TaskService` проекта и замените значения hello</span><span class="sxs-lookup"><span data-stu-id="49d94-132">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>

    * <span data-ttu-id="49d94-133">`ida:Tenant` именем своего клиента;</span><span class="sxs-lookup"><span data-stu-id="49d94-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="49d94-134">`ida:ClientId` идентификатором клиента для приложения веб-API;</span><span class="sxs-lookup"><span data-stu-id="49d94-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="49d94-135">`ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему;</span><span class="sxs-lookup"><span data-stu-id="49d94-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="49d94-136">Откройте `web.config` в hello `TaskWebApp` проекта и замените значения hello</span><span class="sxs-lookup"><span data-stu-id="49d94-136">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>

    * <span data-ttu-id="49d94-137">`ida:Tenant` именем своего клиента;</span><span class="sxs-lookup"><span data-stu-id="49d94-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="49d94-138">`ida:ClientId` идентификатором клиента для веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="49d94-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="49d94-139">`ida:ClientSecret` секретным ключом веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="49d94-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="49d94-140">`ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему;</span><span class="sxs-lookup"><span data-stu-id="49d94-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="49d94-141">`ida:EditProfilePolicyId` именем политики "Изменение профиля";</span><span class="sxs-lookup"><span data-stu-id="49d94-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="49d94-142">`ida:ResetPasswordPolicyId` именем политики "Сброс профиля".</span><span class="sxs-lookup"><span data-stu-id="49d94-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="49d94-143">Запрос и сохранение маркера доступа</span><span class="sxs-lookup"><span data-stu-id="49d94-143">Requesting and saving an access token</span></span>

### <a name="specify-hello-permissions"></a><span data-ttu-id="49d94-144">Укажите разрешения hello</span><span class="sxs-lookup"><span data-stu-id="49d94-144">Specify hello permissions</span></span>

<span data-ttu-id="49d94-145">Порядок toomake hello вызовов toohello веб-API, нужен tooauthenticate hello пользователя (с помощью политики регистрации-повышение/вход) и [получения токена доступа](active-directory-b2c-access-tokens.md) из Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="49d94-145">In order toomake hello call toohello web API, you need tooauthenticate hello user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="49d94-146">В порядке tooreceive маркер доступа сначала необходимо указать разрешения hello хотелось бы toogrant токена доступа hello.</span><span class="sxs-lookup"><span data-stu-id="49d94-146">In order tooreceive an access token, you first must specify hello permissions you would like hello access token toogrant.</span></span> <span data-ttu-id="49d94-147">Hello разрешения указаны в hello `scope` параметра при выполнении запроса toohello hello `/authorize` конечной точки.</span><span class="sxs-lookup"><span data-stu-id="49d94-147">hello permissions are specified in hello `scope` parameter when you make hello request toohello `/authorize` endpoint.</span></span> <span data-ttu-id="49d94-148">Например, tooacquire токен доступа с hello «чтение» разрешение toohello ресурсов приложения hello URI идентификатора приложения `https://contoso.onmicrosoft.com/tasks`, область hello бы `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="49d94-148">For example, tooacquire an access token with hello “read” permission toohello resource application that has hello App ID URI of `https://contoso.onmicrosoft.com/tasks`, hello scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="49d94-149">область toospecify hello в наш hello образец, откройте файл `App_Start\Startup.Auth.cs` и определить hello `Scope` переменной в OpenIdConnectAuthenticationOptions.</span><span class="sxs-lookup"><span data-stu-id="49d94-149">toospecify hello scope in our sample, open hello file `App_Start\Startup.Auth.cs` and define hello `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-hello-authorization-code-for-an-access-token"></a><span data-ttu-id="49d94-150">Обмен кода авторизации hello маркера доступа</span><span class="sxs-lookup"><span data-stu-id="49d94-150">Exchange hello authorization code for an access token</span></span>

<span data-ttu-id="49d94-151">После завершения регистрации или входа в качества hello пользователя приложение получит код авторизации из Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="49d94-151">After an user completes hello sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="49d94-152">Hello OWIN OpenID Connect по промежуточного слоя будет хранить кода hello, но не обмениваются его маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="49d94-152">hello OWIN OpenID Connect middleware will store hello code, but will not exchange it for an access token.</span></span> <span data-ttu-id="49d94-153">Можно использовать hello [MSAL библиотеки](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange.</span><span class="sxs-lookup"><span data-stu-id="49d94-153">You can use hello [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange.</span></span> <span data-ttu-id="49d94-154">В нашем примере настраивался обратного вызова уведомления в по промежуточного слоя, OpenID Connect hello при получении кода авторизации.</span><span class="sxs-lookup"><span data-stu-id="49d94-154">In our sample, we configured a notification callback into hello OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="49d94-155">При обратном вызове hello используйте MSAL tooexchange hello код для токена и сохранить hello маркер в кэш hello.</span><span class="sxs-lookup"><span data-stu-id="49d94-155">In hello callback, we use MSAL tooexchange hello code for a token and save hello token into hello cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract hello code from hello response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange hello code for a token. Make sure toospecify hello necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-hello-web-api"></a><span data-ttu-id="49d94-156">Вызов веб-API hello</span><span class="sxs-lookup"><span data-stu-id="49d94-156">Calling hello web API</span></span>

<span data-ttu-id="49d94-157">В этом разделе рассматриваются как toouse hello маркера, полученные во время регистрации-повышение и войдите в Azure AD B2C в порядке tooaccess hello веб-API.</span><span class="sxs-lookup"><span data-stu-id="49d94-157">This section discusses how toouse hello token received during sign-up/sign-in with Azure AD B2C in order tooaccess hello web API.</span></span>

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a><span data-ttu-id="49d94-158">Извлечь маркер сохранен hello контроллеры hello</span><span class="sxs-lookup"><span data-stu-id="49d94-158">Retrieve hello saved token in hello controllers</span></span>

<span data-ttu-id="49d94-159">Hello `TasksController` несет ответственность за связь с веб-hello API и отправки tooread toohello API запросов HTTP, создание и удаление задач.</span><span class="sxs-lookup"><span data-stu-id="49d94-159">hello `TasksController` is responsible for communicating with hello web API and for sending HTTP requests toohello API tooread, create, and delete tasks.</span></span> <span data-ttu-id="49d94-160">Поскольку hello API обеспечивается Azure AD B2C, вам потребуется toofirst получение hello токена, сохраненный на hello перед шагом.</span><span class="sxs-lookup"><span data-stu-id="49d94-160">Because hello API is secured by Azure AD B2C, you need toofirst retrieve hello token you saved in hello above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL tooretrieve hello token from hello cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve hello token using hello provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-hello-web-api"></a><span data-ttu-id="49d94-161">Чтение задач из hello веб-API</span><span class="sxs-lookup"><span data-stu-id="49d94-161">Read tasks from hello web API</span></span>

<span data-ttu-id="49d94-162">При наличии токена, его можно присоединить toohello HTTP `GET` запроса в hello `Authorization` вызов toosecurely заголовок `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="49d94-162">When you have a token, you can attach it toohello HTTP `GET` request in hello `Authorization` header toosecurely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve hello token with hello specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token toohello Authorization header and make hello request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-hello-web-api"></a><span data-ttu-id="49d94-163">Создание и удаление задачи на hello веб-API</span><span class="sxs-lookup"><span data-stu-id="49d94-163">Create and delete tasks on hello web API</span></span>

<span data-ttu-id="49d94-164">Выполните hello же шаблонов отправляемым `POST` и `DELETE` запрашивает toohello веб-API, с помощью маркера доступа hello tooretrieve MSAL из кэша hello.</span><span class="sxs-lookup"><span data-stu-id="49d94-164">Follow hello same pattern when you send `POST` and `DELETE` requests toohello web API, using MSAL tooretrieve hello access token from hello cache.</span></span>

## <a name="run-hello-sample-app"></a><span data-ttu-id="49d94-165">Запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="49d94-165">Run hello sample app</span></span>

<span data-ttu-id="49d94-166">Наконец сборку и запуск обоих приложений hello.</span><span class="sxs-lookup"><span data-stu-id="49d94-166">Finally, build and run both hello apps.</span></span> <span data-ttu-id="49d94-167">Регистрация и вход и создавать задачи для пользователя, выполнившего вход hello.</span><span class="sxs-lookup"><span data-stu-id="49d94-167">Sign up and sign in, and create tasks for hello signed-in user.</span></span> <span data-ttu-id="49d94-168">Выйдите и зарегистрируйтесь от имени другого пользователя.</span><span class="sxs-lookup"><span data-stu-id="49d94-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="49d94-169">Создайте задачи для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="49d94-169">Create tasks for that user.</span></span> <span data-ttu-id="49d94-170">Обратите внимание, как задачи hello хранимых пользователя на hello API, поскольку hello API извлекает hello учетные данные пользователя из маркера hello, получаемые им.</span><span class="sxs-lookup"><span data-stu-id="49d94-170">Notice how hello tasks are stored per-user on hello API, because hello API extracts hello user's identity from hello token it receives.</span></span> <span data-ttu-id="49d94-171">Также попробуйте воспроизвести с помощью областей hello.</span><span class="sxs-lookup"><span data-stu-id="49d94-171">Also try playing with hello scopes.</span></span> <span data-ttu-id="49d94-172">Удалите разрешение hello слишком «запись», а затем попытайтесь добавить задачу.</span><span class="sxs-lookup"><span data-stu-id="49d94-172">Remove hello permission too"write" and then try adding a task.</span></span> <span data-ttu-id="49d94-173">Просто убедитесь, что toosign out каждый раз при изменении области hello.</span><span class="sxs-lookup"><span data-stu-id="49d94-173">Just make sure toosign out each time you change hello scope.</span></span>

