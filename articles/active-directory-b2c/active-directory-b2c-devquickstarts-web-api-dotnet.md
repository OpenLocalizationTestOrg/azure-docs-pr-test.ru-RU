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
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a>Azure AD B2C: вызов веб-API .NET из веб-приложения .NET

С помощью Azure AD B2C, можно добавить мощные удостоверение управления функции tooyour веб-приложений и веб-API. В этой статье описывается, как toorequest маркеры доступа и выполнять вызовы из .NET «список дел» веб-tooa приложения .NET, веб-api.

Данная статья не охватывает как tooimplement вход, регистрации и управления с помощью Azure AD B2C профиля. Этот раздел посвящен вызовах веб-API после hello пользователь уже прошел проверку подлинности. Если это еще не сделано, необходимо выполнить следующие действия.

* Изучите начало работы с [веб-приложением .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)
* Изучите начало работы с [веб-API .NET](active-directory-b2c-devquickstarts-api-dotnet.md)

## <a name="prerequisite"></a>Предварительные требования

toobuild веб-приложение, которое вызывает веб-api, необходимо:

1. [Создайте клиента Azure AD B2C](active-directory-b2c-get-started.md).
2. [Зарегистрируйте веб-API](active-directory-b2c-app-registration.md#register-a-web-api).
3. [Зарегистрируйте веб-приложение](active-directory-b2c-app-registration.md#register-a-web-app).
4. [Настройте политики](active-directory-b2c-reference-policies.md).
5. [Предоставление hello web app разрешения toouse hello веб-api](active-directory-b2c-access-tokens.md#publishing-permissions).

> [!IMPORTANT]
> клиентское приложение Hello и веб-API необходимо использовать каталог B2C hello же Azure AD.
>

## <a name="download-hello-code"></a>Загрузка кода hello

Hello кода для этого учебника, сохраняется на [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Образец hello можно клонировать, выполнив:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

После загрузки кода образца hello запущен tooget файл .sln Visual Studio откройте hello. Hello файл решения содержит два проекта: `TaskWebApp` и `TaskService`. `TaskWebApp`— веб-приложение MVC, hello пользователь взаимодействует с. `TaskService`— приложение hello фоновая веб-API, который хранит список дел каждого пользователя. Данная статья не охватывает hello построение `TaskWebApp` веб-приложения или hello `TaskService` веб-api. toolearn toobuild hello .NET, веб-приложения с помощью Azure AD B2C разделе нашей [учебник по .NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md). toolearn как toobuild hello .NET веб-API, защищенного с помощью Azure AD B2C см. наш [учебника веб-API .NET](active-directory-b2c-devquickstarts-api-dotnet.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Обновите конфигурацию hello Azure AD B2C

Выборка — настроенное toouse hello политик и клиент идентификатор нашей демонстрационному клиенту. Если вы хотите toouse своим собственным клиентом:

1. Откройте `web.config` в hello `TaskService` проекта и замените значения hello

    * `ida:Tenant` именем своего клиента;
    * `ida:ClientId` идентификатором клиента для приложения веб-API;
    * `ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему;

2. Откройте `web.config` в hello `TaskWebApp` проекта и замените значения hello

    * `ida:Tenant` именем своего клиента;
    * `ida:ClientId` идентификатором клиента для веб-приложения;
    * `ida:ClientSecret` секретным ключом веб-приложения;
    * `ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему;
    * `ida:EditProfilePolicyId` именем политики "Изменение профиля";
    * `ida:ResetPasswordPolicyId` именем политики "Сброс профиля".



## <a name="requesting-and-saving-an-access-token"></a>Запрос и сохранение маркера доступа

### <a name="specify-hello-permissions"></a>Укажите разрешения hello

Порядок toomake hello вызовов toohello веб-API, нужен tooauthenticate hello пользователя (с помощью политики регистрации-повышение/вход) и [получения токена доступа](active-directory-b2c-access-tokens.md) из Azure AD B2C. В порядке tooreceive маркер доступа сначала необходимо указать разрешения hello хотелось бы toogrant токена доступа hello. Hello разрешения указаны в hello `scope` параметра при выполнении запроса toohello hello `/authorize` конечной точки. Например, tooacquire токен доступа с hello «чтение» разрешение toohello ресурсов приложения hello URI идентификатора приложения `https://contoso.onmicrosoft.com/tasks`, область hello бы `https://contoso.onmicrosoft.com/tasks/read`.

область toospecify hello в наш hello образец, откройте файл `App_Start\Startup.Auth.cs` и определить hello `Scope` переменной в OpenIdConnectAuthenticationOptions.

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

### <a name="exchange-hello-authorization-code-for-an-access-token"></a>Обмен кода авторизации hello маркера доступа

После завершения регистрации или входа в качества hello пользователя приложение получит код авторизации из Azure AD B2C. Hello OWIN OpenID Connect по промежуточного слоя будет хранить кода hello, но не обмениваются его маркера доступа. Можно использовать hello [MSAL библиотеки](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange. В нашем примере настраивался обратного вызова уведомления в по промежуточного слоя, OpenID Connect hello при получении кода авторизации. При обратном вызове hello используйте MSAL tooexchange hello код для токена и сохранить hello маркер в кэш hello.

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

## <a name="calling-hello-web-api"></a>Вызов веб-API hello

В этом разделе рассматриваются как toouse hello маркера, полученные во время регистрации-повышение и войдите в Azure AD B2C в порядке tooaccess hello веб-API.

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a>Извлечь маркер сохранен hello контроллеры hello

Hello `TasksController` несет ответственность за связь с веб-hello API и отправки tooread toohello API запросов HTTP, создание и удаление задач. Поскольку hello API обеспечивается Azure AD B2C, вам потребуется toofirst получение hello токена, сохраненный на hello перед шагом.

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

### <a name="read-tasks-from-hello-web-api"></a>Чтение задач из hello веб-API

При наличии токена, его можно присоединить toohello HTTP `GET` запроса в hello `Authorization` вызов toosecurely заголовок `TaskService`:

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

### <a name="create-and-delete-tasks-on-hello-web-api"></a>Создание и удаление задачи на hello веб-API

Выполните hello же шаблонов отправляемым `POST` и `DELETE` запрашивает toohello веб-API, с помощью маркера доступа hello tooretrieve MSAL из кэша hello.

## <a name="run-hello-sample-app"></a>Запуск образца приложения hello

Наконец сборку и запуск обоих приложений hello. Регистрация и вход и создавать задачи для пользователя, выполнившего вход hello. Выйдите и зарегистрируйтесь от имени другого пользователя. Создайте задачи для этого пользователя. Обратите внимание, как задачи hello хранимых пользователя на hello API, поскольку hello API извлекает hello учетные данные пользователя из маркера hello, получаемые им. Также попробуйте воспроизвести с помощью областей hello. Удалите разрешение hello слишком «запись», а затем попытайтесь добавить задачу. Просто убедитесь, что toosign out каждый раз при изменении области hello.

