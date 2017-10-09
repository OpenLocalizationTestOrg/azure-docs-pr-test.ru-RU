---
title: "aaaAzure AD v2 ASP.NET Web Server Приступая к работе - установки | Документы Microsoft"
description: "Реализация входа Майкрософт в решении ASP.NET с традиционным браузерным приложением с использованием стандарта OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: eadc59666557e9cd294e6e99391001120579144c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Настройка проекта

В этом разделе показаны шаги tooinstall hello и настройте hello конвейера проверки подлинности через по промежуточного слоя OWIN в проект ASP.NET с использованием OpenID Connect. 

> Предпочтение toodownload проекта Visual Studio в этом примере вместо этого? [Загрузка проекта](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) и пропустить toohello [шаг настройки](#create-an-application-express) образец кода hello tooconfigure перед выполнением.

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a>Создание проекта ASP.NET

> 1. В Visual Studio выберите `File` > `New` > `Project`.<br/>
> 2. В разделе *Visual C#\Web* выберите `ASP.NET Web Application (.NET Framework)`.
> 3. Присвойте имя приложению и нажмите кнопку *ОК*.
> 4. Выберите `Empty` и выберите hello флажок tooadd `MVC` ссылки
<!--end-collapse-->

## <a name="add-authentication-components"></a>Добавление компонентов проверки подлинности

1. В Visual Studio выберите `Tools` > `Nuget Package Manager` > `Package Manager Console`.
2. Добавить *пакетов NuGet по промежуточного слоя OWIN* , введя следующее hello в hello в окне консоли диспетчера пакетов:

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a>О библиотеках

>библиотеки Hello выше Включение единого входа (SSO) через проверку подлинности на основе файлов cookie с использованием OpenID Connect. После завершения проверки подлинности и hello токен, представляющий hello пользователя отправляется tooyour приложения, по промежуточного слоя OWIN создает файл cookie сеанса. Hello обозреватель использует этот файл cookie при последующих запросах, hello пользователю не нужны tooretype свой пароль и требуется дополнительная проверка.
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a>Настройка проверки подлинности конвейера hello
Hello шаги, используемые toocreate OWIN по промежуточного слоя класс запуска tooconfigure OpenID Connect проверки подлинности. Этот класс будет выполняться автоматически при запуске процесса IIS.

> Если ваш проект не имеет `Startup.cs` файл в корневой папке hello:<br/>
> 1. Щелкните правой кнопкой мыши корневой папки проекта hello: >`Add` > `New Item...` > `OWIN Startup class`<br/>
> 2. Назовите класс `Startup.cs`.

> Убедитесь, что выбранный класс hello класс запуска OWIN, а не стандартный класс C#. Проверить, проверки, если вы видите `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` выше hello пространства имен.


1. Добавить *OWIN* и *Microsoft.IdentityModel* ссылается слишком`Startup.cs`:

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Замените класс запуска hello код ниже:
</li>
</ol>

```csharp
public class Startup
{        
    // hello Client ID is used by hello application toouniquely identify itself tooAzure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is hello URL where hello user will be redirected tooafter they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is hello tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is hello URL for authority, composed by Azure Active Directory v2 endpoint and hello tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN toouse OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets hello ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is hello page that users will be redirected tooafter sign-out. In this case, it is using hello home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set toorequest hello id_token - which contains basic information about hello signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set toofalse tooallow personal and work accounts from any organization toosign in tooyour application
                // tooonly allow users from a single organizations, set ValidateIssuer tootrue and 'tenant' setting in web.config toohello tenant name
                // tooallow users from only a list of specific organizations, set ValidateIssuer tootrue and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN toosend notification of failed authentications tooOnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting hello user toohello home page with an error in hello query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a>Дополнительные сведения

> Здравствуйте, параметры, указываемые в *OpenIDConnectAuthenticationOptions* служат в качестве координат для hello toocommunicate приложений с Azure AD. Поскольку hello OpenID Connect по промежуточного слоя использует файлы cookie в фоновом режиме hello, необходимо также tooset копирование файла cookie проверки подлинности как код hello выше. Hello *ValidateIssuer* значение сообщает OpenIdConnect toonot ограничить доступ tooone конкретной организации.
<!--end-collapse-->

