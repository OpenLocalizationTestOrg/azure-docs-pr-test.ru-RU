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
# <a name="add-sign-in-tooan-net-mvc-web-app"></a>Добавить веб-приложение .NET MVC tooan входа
С конечной точкой v2.0 hello можно быстро добавлять проверки подлинности tooyour веб-приложений с помощью поддержки для обоих личные учетные записи Майкрософт и рабочих учетных записей.  В веб-приложениях ASP.NET это можно делать с помощью ПО промежуточного уровня OWIN корпорации Microsoft, включенного в .NET Framework 4.5.

> [!NOTE]
> Не все сценарии Azure Active Directory и возможности поддерживаются hello v2.0 конечной точкой.  toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).
>
>

 Здесь мы выполним сборку веб-приложения, использующего пользователя hello toosign OWIN в отображаются некоторые сведения о пользователе hello и знак hello выход пользователя из приложения hello.

## <a name="download"></a>Загрузить
поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).  можно toofollow вдоль [загрузить приложение hello основу как .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) или основу hello клона:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

в конце hello в учебнике также предоставляется приложение Hello завершена.

## <a name="register-an-app"></a>регистрация приложения;
Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md).  Не забудьте:

* Копировать вниз hello **идентификатор приложения** назначены tooyour приложения, оно понадобится скоро.
* Добавить hello **Web** платформы для приложения.
* Введите правильный hello **URI перенаправления**. Hello uri перенаправления указывает tooAzure AD, где следует направлять запросы проверки подлинности — по умолчанию hello в этом учебнике используется `https://localhost:44326/`.

## <a name="install--configure-owin-authentication"></a>Установка и настройка аутентификации OWIN
Здесь мы настроим hello OWIN по промежуточного слоя toouse hello OpenID Connect протокол проверки подлинности.  OWIN быть используется tooissue запросы на вход и выход, управлять сеансом пользователя hello и получения сведений о пользователе hello, среди прочего.

1. toobegin Привет открыть `web.config` файл в корневом каталоге hello hello проекта и введите значения конфигурации приложения в hello `<appSettings>` раздела.

  * Hello `ida:ClientId` — hello **идентификатор приложения** назначенный tooyour приложения на портале регистрации hello.
  * Hello `ida:RedirectUri` — hello **Uri перенаправления** введенное на портале hello.

2. Затем добавьте hello OWIN по промежуточного слоя NuGet пакеты toohello проекта с помощью консоли диспетчера пакетов hello.

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. Добавить проект toohello «Класс запуска OWIN» вызывается `Startup.cs` вправо, щелкните проект hello--> **добавить** --> **новый элемент** --> Поиск «OWIN».  по промежуточного слоя OWIN Hello будет вызывать hello `Configuration(...)` метод при запуске приложения.
4. Измените объявление класса hello слишком`public partial class Startup` -мы уже реализовали часть этого класса для вас в другом файле.  В hello `Configuration(...)` метод, сделать tooset tooConfigureAuth(...) вызов проверку подлинности для веб-приложения  

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

5. Привет открыть файл `App_Start\Startup.Auth.cs` и реализовать hello `ConfigureAuth(...)` метод.  Здравствуйте, параметры, указываемые в `OpenIdConnectAuthenticationOptions` будет служить в качестве координат для toocommunicate вашего приложения в Azure AD.  Необходимо также tooset копирование файла Cookie проверки подлинности — hello OpenID Connect по промежуточного слоя использует файлы cookie под охватывает hello.

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

## <a name="send-authentication-requests"></a>Отправка запросов проверки подлинности
Приложение теперь будет правильно настроен toocommunicate с конечной точкой v2.0 hello, используя протокол проверки подлинности OpenID Connect hello.  OWIN Разобравшись все подробности сложный hello отправляемого сообщения проверки подлинности, проверки токенов из Azure AD и поддержания сеанса пользователя.  Все, что остается является toogive пользователей toosign способом в и выхода.

- Можно использовать теги авторизации в вашей toorequire контроллеров входе перед обращением к определенной странице.  Откройте `Controllers\HomeController.cs`и добавить hello `[Authorize]` тега toohello о контроллере.
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- Также можно использовать запросов OWIN toodirectly проблема проверки подлинности из кода.  Откройте `Controllers\AccountController.cs`.  В hello SignIn() и SignOut() действия выполните запрос OpenID Connect и запросах на выход, соответственно.

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

- Теперь откройте `Views\Shared\_LoginPartial.cshtml`.  Это, где вы Показывать hello пользовательского приложения ссылки входа и выхода из системы, а также напечатать имя пользователя hello в представлении.

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

## <a name="display-user-information"></a>Отображение сведений о пользователе
При проверке подлинности пользователей с OpenID Connect, конечная точка v2.0 hello возвращает id_token toohello приложение, которое содержит утверждения или утверждения о пользователе hello.  Можно использовать эти утверждения toopersonalize приложения:

- Откройте hello `Controllers\HomeController.cs` файла.  Можно использовать утверждения пользователей hello в контроллерах через hello `ClaimsPrincipal.Current` объект субъекта безопасности.

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

## <a name="run"></a>Выполнить
Наконец, постройте и запустите свое приложение!   Войдите, используя личную учетную запись Майкрософт или рабочую учетную запись и обратите внимание на то, как удостоверение пользователя hello отражается hello верхней панели навигации.  Теперь у вас есть веб-приложение, защищенное с помощью стандартных отраслевых протоколов, которое может проверять подлинность пользователей с помощью личных, рабочих и учебных учетных записей.

Справочник по hello выполнить пример (без настройки) [предоставляется как .zip здесь](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), или вы можете клонировать из GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a>Дальнейшие действия
Теперь можно перейти к более сложным темам.  Вы можете tootry:

[Защита веб-API с конечной точкой v2.0 hello hello >>](active-directory-devquickstarts-webapi-dotnet.md)

Дополнительные ресурсы:

* [Руководство разработчика v2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [Тег StackOverflow "azure-active-directory" >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Получение обновлений системы безопасности для наших продуктов
Мы рекомендуем вам уведомления при возникновении события безопасности, посетив tooget [эту страницу](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.
