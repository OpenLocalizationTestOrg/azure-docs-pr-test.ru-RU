---
title: "aaaAzure Active Directory B2C | Документы Microsoft"
description: "Как toobuild веб-приложения с регистрации-повышение или входе в систему профиля, изменение и сбросить с помощью Azure Active Directory B2C пароль."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a>Создание веб-приложения ASP.NET с возможностями регистрации, входа, редактирования профиля и сброса пароля Azure Active Directory B2C

В этом учебнике описаны следующие процедуры.

> [!div class="checklist"]
> * Добавление Azure AD B2C идентификаторов компонентов tooyour веб-приложения
> * Регистрация веб-приложения в каталоге Azure AD B2C
> * Создание политики регистрации, входа, изменения профиля и сброса пароля пользователя для веб-приложения

## <a name="prerequisites"></a>Предварительные требования

- Вашего клиента B2C tooan учетная запись Azure, необходимо подключиться. Вы можете создать бесплатную учетную запись Azure [здесь](https://azure.microsoft.com/en-us/).
- Требуется [Microsoft Visual Studio](https://www.visualstudio.com/) или аналогичные программы tooview и измените пример кода hello.

## <a name="create-an-azure-ad-b2c-directory"></a>Создание каталога Azure AD B2C

Перед использованием Azure AD B2C необходимо создать каталог или клиент. Каталог — это контейнер для всех пользователей, приложений, групп и т. д. Прежде чем продолжать работу с руководством, создайте каталог B2C, если вы его еще не создали.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> Необходимо tooconnect hello клиента B2C tooyour подписки Azure. После выбора **создать**выберите hello **toomy клиента связь существующего Azure AD B2C подписки Azure** параметр и затем в hello **клиента Azure AD B2C** раскрывающийся список, выберите Вы хотите tooassociate клиента Hello.

## <a name="create-and-register-an-application"></a>Создание и регистрация приложения

Далее требуется toocreate и зарегистрировать приложение hello в каталоге B2C. Предоставляет сведения, что Azure AD B2C должна toosecurely взаимодействовать с приложением. 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

По окончании у вас будет API и собственное приложение в параметрах приложения.

## <a name="create-policies-on-your-b2c-tenant"></a>Создание политик в клиенте B2C

В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md). Этот пример кода включает три способа идентификации: **регистрацию и вход в систему**, **изменение профиля**, а также **сброс пароля**.  Требуется одна политика toocreate каждого типа, как описано в hello [статье политики](active-directory-b2c-reference-policies.md). Для каждой политики быть убедиться, что tooselect hello отображаемое имя атрибута или утверждения и toocopy вниз hello имя политики для последующего использования.

### <a name="add-your-identity-providers"></a>Добавление поставщиков удостоверений

В разделе параметров щелкните **Поставщики удостоверений** и выберите вход с помощью имени пользователя или электронной почты.

### <a name="create-a-sign-up-and-sign-in-policy"></a>Создание политики регистрации и входа в систему

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a>Создание политики изменения профиля

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a>Создание политики сброса паролей

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

После создания политики вы готовы toobuild приложения.

## <a name="download-hello-sample-code"></a>Загрузить пример кода hello

Hello кода для этого учебника, сохраняется на [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Образец hello можно клонировать, выполнив:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

После загрузки кода образца hello запущен tooget файл .sln Visual Studio откройте hello. Hello файл решения содержит два проекта: `TaskWebApp` и `TaskService`. `TaskWebApp`— hello веб-приложение MVC, hello пользователь взаимодействует с. `TaskService`— приложение hello фоновая веб-API, который хранит список дел каждого пользователя. В этой статье рассматривается hello `TaskWebApp` приложения. toolearn как toobuild `TaskService` с помощью Azure AD B2C, в разделе [наш учебник по api .NET web](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="update-code-toouse-your-tenant-and-policies"></a>Обновить toouse код клиента и политики

Выборка — настроенное toouse hello политик и клиент идентификатор нашей демонстрационному клиенту. tooconnect его tooyour собственного клиента, необходимо tooopen `web.config` в hello `TaskWebApp` проекта а hello следующие значения:

* `ida:Tenant` именем своего клиента;
* `ida:ClientId` идентификатором клиента для веб-приложения;
* `ida:ClientSecret` секретным ключом веб-приложения;
* `ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему;
* `ida:EditProfilePolicyId` именем политики "Изменение профиля";
* `ida:ResetPasswordPolicyId` именем политики "Сброс профиля".

## <a name="launch-hello-app"></a>Запустите приложение hello
Из среды Visual Studio, запустите приложение hello. Перемещение вкладку toohello список дел и hello примечание, URL-адрес: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...

Зарегистрируйтесь для приложения hello вашей электронной почты адрес или имя пользователя. Выйдите из системы, затем войти в систему и изменить профиль hello или сбросить пароль hello. Выйдите и зарегистрируйтесь от имени другого пользователя. 

## <a name="add-social-idps"></a>Добавление поставщиков удостоверений социальных сетей

В настоящее время приложение hello поддерживает только пользователь, регистрации и входе в систему с помощью **локальные учетные записи**; учетные записи хранятся в каталоге B2C использовать имя пользователя и пароль. С помощью Azure AD B2C можно добавить поддержку для других **поставщиков удостоверений** (IDP), не изменяя код.

tooadd социальных IDPs tooyour приложение, начните с выполнения следующего hello подробные инструкции в следующих статьях. Для каждого поставщика Удостоверений требуется toosupport, нужно tooregister приложения в этой системе и получение идентификатора клиента.

* [Настройка Facebook как поставщика удостоверений](active-directory-b2c-setup-fb-app.md)
* [Настройка Google как поставщика удостоверений](active-directory-b2c-setup-goog-app.md)
* [Настройка Amazon как поставщика удостоверений](active-directory-b2c-setup-amzn-app.md)
* [Настройка LinkedIn как поставщика удостоверений](active-directory-b2c-setup-li-app.md)

После добавления tooyour Поставщики удостоверений hello каталоге B2C, редактирования каждого вашей tooinclude три политики hello новый IDPs, как описано в hello [статье политики](active-directory-b2c-reference-policies.md). После сохранения политик, снова запустите приложение hello.  Вы увидите hello, добавления новых IDPs входа и регистрации в качестве параметров каждой своими впечатлениями удостоверения.

Можно поэкспериментировать с политиками и наблюдать за тем hello влияет на примере приложения. например: добавлять или удалять поставщиков удостоверений, управлять утверждениями приложений или изменять атрибуты регистрации, а также наблюдать эффект в примере приложения. Эксперименты помогают увидеть связь между политиками, запросами на проверку подлинности и библиотекой OWIN.

## <a name="sample-code-walkthrough"></a>Пошаговое руководство по примеру кода
Hello в следующих разделах показано, как настроить код приложения образец hello. Вы можете использовать это руководство при разработке приложения в будущем.

### <a name="add-authentication-support"></a>Добавление поддержки проверки подлинности

Теперь можно настроить toouse вашего приложения Azure AD B2C. Приложение взаимодействует с Azure AD B2C, отправляя запросы проверки подлинности по протоколу OpenID Connect. Hello запросов определяют взаимодействие с пользователем hello приложение хочет tooexecute, указав hello политику. Можно использовать эти запросы toosend библиотеки OWIN корпорации Майкрософт, выполнение политик, управление пользовательских сеансов и многое другое.

#### <a name="install-owin"></a>Установка OWIN

toobegin, добавить toohello hello OWIN по промежуточного слоя NuGet пакетов проекта с помощью консоли диспетчера пакетов Visual Studio hello.

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a>Добавление класса запуска OWIN

Добавление toohello класс запуска OWIN API с именем `Startup.cs`.  Правой кнопкой мыши проект hello, выберите **добавить** и **новый элемент**и выполните поиск OWIN. по промежуточного слоя OWIN Hello будет вызывать hello `Configuration(…)` метод при запуске приложения.

В нашем примере мы изменили объявление класса hello слишком`public partial class Startup` и реализации hello hello класса в другой части `App_Start\Startup.Auth.cs`. Внутри hello `Configuration` метод, мы добавили вызов слишком`ConfigureAuth`, которая определена в `Startup.Auth.cs`. После изменения hello `Startup.cs` выглядит как hello следующее:

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

#### <a name="configure-hello-authentication-middleware"></a>Настройки по промежуточного слоя проверки подлинности hello

Привет открыть файл `App_Start\Startup.Auth.cs` и реализовать hello `ConfigureAuth(...)` метод. Здравствуйте, параметры, указываемые в `OpenIdConnectAuthenticationOptions` служат в качестве координат для toocommunicate вашего приложения с Azure AD B2C. Если вы не указываете определенные параметры, он будет использовать значение по умолчанию hello. Например, мы не указать hello `ResponseType` в образце hello, поэтому значение по умолчанию hello `code id_token` используются для каждого исходящего запроса tooAzure AD B2C.

Необходимо также tooset копирование файла cookie проверки подлинности. Hello OpenID Connect по промежуточного слоя использует файлы cookie toomaintain пользовательских сеансов, среди прочего.

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

В `OpenIdConnectAuthenticationOptions` выше, мы определяем набор функций обратного вызова для конкретных уведомлений, полученных по промежуточного слоя, OpenID Connect hello. Эти варианты поведения определяются с помощью `OpenIdConnectAuthenticationNotifications` объекта и сохраняются в hello `Notifications` переменной. В нашем примере мы определяем три различных обратных вызовов в зависимости от события hello.

### <a name="using-different-policies"></a>Использование различных политик

Hello `RedirectToIdentityProvider` уведомление будет запускаться при каждом запросе tooAzure AD B2C. В функции обратного вызова hello `OnRedirectToIdentityProvider`, мы проверяем в исходящий вызов, если мы хотим toouse hello другой политике. В порядке toodo пароль сбросить или изменить профиль необходимо toouse hello соответствующая политика такие как политики вместо «Регистрации или входа в систему» политики по умолчанию hello сброса паролей hello.

В нашем примере когда пользователь хочет tooreset hello пароль или измените профиль hello мы Добавление политики hello желательно toouse контекст OWIN hello. Что можно сделать, выполнив следующие hello:

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

Можно применить функцию обратного вызова hello `OnRedirectToIdentityProvider` , выполнив hello ниже:

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a>Обработка кодов авторизации

Hello `AuthorizationCodeReceived` уведомление срабатывает при получении кода авторизации. по промежуточного слоя, OpenID Connect Hello не поддерживает обмен коды для маркера доступа. Можно вручную обмен кода hello hello маркера в функции обратного вызова. Дополнительные сведения см. в hello [документации](active-directory-b2c-devquickstarts-web-api-dotnet.md) объясняется, каким образом.

### <a name="handling-errors"></a>Обработка ошибок

Hello `AuthenticationFailed` уведомление срабатывает при сбое проверки подлинности. В методе обратного вызова можно обрабатывать ошибки hello по своему усмотрению. Тем не менее, следует добавить проверку для кода ошибки hello `AADB2C90118`. Во время выполнения hello hello политики «Регистрации или входа в систему», hello пользователь имеет возможность tooselect hello **забыли пароль?** ссылку. В этом случае Azure AD B2C отправляет приложения код этой ошибке, указывающее, что приложения необходимо выполнить запрос, вместо этого использовать политики сброса паролей hello.

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a>Отправить tooAzure запросы проверки подлинности AD

Приложение теперь будет правильно настроен toocommunicate с Azure AD B2C с помощью протокола проверки подлинности OpenID Connect hello. OWIN управляет данными hello отправляемого сообщения проверки подлинности, проверка токены из Azure AD B2C и поддержания сеанса пользователя. Все, что остается приведена tooinitiate каждого пользователя.

Когда пользователь выбирает **входа вверх или входа**, **редактирование профиля**, или **сброс пароля** в веб-приложения hello, при вызове hello связанные действия в `Controllers\AccountController.cs`:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

Также можно использовать toosign OWIN выход hello пользователя из приложения hello. В `Controllers\AccountController.cs` у нас есть следующее:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

В дополнение tooexplicitly вызов политику, можно использовать `[Authorize]` тег в контроллерах, который выполняет политику, если hello пользователь не выполнил вход. Откройте `Controllers\HomeController.cs` и добавить hello `[Authorize]` toohello тег утверждений контроллера.  OWIN выбирает hello последние политики hello `[Authorize]` попаданий тег.

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a>Отображение сведений о пользователе

Если для проверки подлинности пользователей с помощью OpenID Connect, Azure AD B2C возвращает идентификатор маркера toohello приложение, которое содержит **утверждений**. Это утверждения о пользователе hello. Toopersonalize утверждения можно использовать приложение.

Откройте hello `Controllers\HomeController.cs` файла. Утверждения пользователей можно использовать в контроллерах через hello `ClaimsPrincipal.Current` объект субъекта безопасности.

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

Можно открыть любые претензии, что приложение получает в hello таким же способом.  Список всех утверждений hello, приложение hello Получает доступные на hello **утверждений** страницы.
