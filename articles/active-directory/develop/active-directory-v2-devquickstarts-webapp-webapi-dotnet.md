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
# <a name="calling-a-web-api-from-a-net-web-app"></a>Вызов веб-API из веб-приложения .NET
С конечной точкой v2.0 hello можно быстро добавлять проверки подлинности tooyour веб-приложений и веб-API с поддержки для обоих личных учетных записей Майкрософт и рабочих учетных записей.  Мы создадим веб-приложение MVC, которое поддерживает вход пользователей с помощью OpenID Connect с использованием ПО промежуточного слоя OWIN Майкрософт.  Hello веб-приложения получение маркера доступа OAuth 2.0 для веб-api, защищенного OAuth 2.0, которая позволяет создавать, читать и delete для данного пользователя «список дел».

Этот учебник будет связана главным образом с использованием MSAL tooacquire и использовать токены доступа в веб-приложения, описанные в полном объеме [здесь](active-directory-v2-flows.md#web-apps).  В качестве необходимых компонентов, вы можете toofirst Узнайте, каким образом слишком[добавить основные tooa веб-приложения](active-directory-v2-devquickstarts-dotnet-web.md) или как слишком[правильно обеспечить безопасность веб-API](active-directory-v2-devquickstarts-dotnet-api.md).

> [!NOTE]
> Не все сценарии Azure Active Directory и возможности поддерживаются hello v2.0 конечной точкой.  toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-sample-code"></a>Скачивание примера кода
поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).  можно toofollow вдоль [загрузить приложение hello основу как .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) или основу hello клона:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

Кроме того, можно [загрузить приложение hello завершена как .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) или hello выполнить клонирование приложений:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a>регистрация приложения;
Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md).  Не забудьте:

* Копировать вниз hello **идентификатор приложения** назначены tooyour приложения, оно понадобится скоро.
* Создание **секрет приложения** из hello **пароль** тип и копирования вниз его значение на более поздний срок
* Добавить hello **Web** платформы для приложения.
* Введите правильный hello **URI перенаправления**. Hello uri перенаправления указывает tooAzure AD, где следует направлять запросы проверки подлинности — по умолчанию hello в этом учебнике используется `https://localhost:44326/`.

## <a name="install-owin"></a>Установка OWIN
Добавление пакетов NuGet toohello для hello OWIN по промежуточного слоя `TodoList-WebApp` проектов с помощью консоли диспетчера пакетов "hello".  по промежуточного слоя OWIN Hello быть используется tooissue запросы на вход и выход, управлять сеансом пользователя hello и получения сведений о пользователе hello, среди прочего.

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a>Вход пользователя hello в
Теперь настройка hello toouse по промежуточного слоя OWIN hello [протокол проверки подлинности OpenID Connect](active-directory-v2-protocols.md).  

* Откройте hello `web.config` файл в корне hello hello `TodoList-WebApp` проекта, а затем введите значения конфигурации приложения в hello `<appSettings>` раздела.
  * Hello `ida:ClientId` — hello **идентификатор приложения** назначенный tooyour приложения на портале регистрации hello.
  * Hello `ida:ClientSecret` — hello **секрет приложения** вы создали на портале регистрации hello.
  * Hello `ida:RedirectUri` — hello **Uri перенаправления** введенное на портале hello.
* Откройте hello `web.config` файл в корне hello hello `TodoList-Service` проекта, а hello `ida:Audience` с hello же **идентификатор приложения** как описано выше.
* Привет открыть файл `App_Start\Startup.Auth.cs` и добавьте `using` инструкций для библиотек hello выше.
* В hello того же файла, реализовать hello `ConfigureAuth(...)` метод.  Здравствуйте, параметры, указываемые в `OpenIDConnectAuthenticationOptions` будет служить в качестве координат для toocommunicate вашего приложения в Azure AD.

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

## <a name="use-msal-tooget-access-tokens"></a>Использование маркера доступа tooget MSAL
В hello `AuthorizationCodeReceived` уведомления, мы хотим toouse [OAuth 2.0 в сочетании с OpenID Connect](active-directory-v2-protocols.md) значение authorization_code hello tooredeem для токена toohello доступ службы списка задач.  MSAL может упростить этот процесс.

* Во-первых установите предварительную версию hello MSAL:

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* И добавьте еще один `using` toohello инструкции `App_Start\Startup.Auth.cs` файл для MSAL.
* Теперь добавьте новый метод hello `OnAuthorizationCodeReceived` обработчика событий.  Этот обработчик будет использовать MSAL tooacquire toohello токена доступа к API список дел и сохранит hello маркера в кэше токенов MSAL на более поздний срок:

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

* В веб-приложениях MSAL имеет расширяемый кэш токена, может быть используется toostore маркеры.  В этом примере реализуется hello `NaiveSessionCache` с использованием маркеров toocache хранилища сеансов http.

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a>Hello вызовов веб-API
Теперь пора tooactually использовать access_token hello, полученного в шаге 3.  Привет открыть веб-приложение `Controllers\TodoListController.cs` файл, который делает все hello CRUD запросы toohello API список дел.

* Можно использовать MSAL попытку здесь access_tokens toofetch из hello MSAL кэша.  Сначала добавьте `using` инструкции для MSAL toothis файла.
  
    `using Microsoft.Identity.Client;`
* В hello `Index` действия, используйте MSAL `AcquireTokenSilentAsync` tooget метод access_token, может быть используется tooread данные из hello список дел службы:

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

* Hello образец добавляет hello полученный маркер toohello запроса HTTP GET на составляющие hello `Authorization` заголовок, какая служба список дел hello использует запрос tooauthenticate hello.
* Возвращает список дел службы hello `401 Unauthorized` ответ access_tokens hello в MSAL ставшие недействительными для какой-либо причине.  В этом случае необходимо удалить все access_tokens из кэша MSAL hello и показывать hello пользовательского сообщения, может возникнуть необходимость toosign в снова, которой будет перезагружен hello получения маркера потока.

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

* Аналогично Если не удается tooreturn access_token MSAL по любой причине, toosign пользователя hello в следует поручить еще раз.  Для этого нужно всего лишь перехватить любой `MSALException`:

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* Hello точного же `AcquireTokenSilentAsync` вызывается implementd в hello `Create` и `Delete` действия.  В веб-приложениях можно использовать этот access_tokens tooget метод MSAL всякий раз, когда они нужны в приложении.  MSAL получает, кэширует и обновляет маркеры для вас.

Наконец, постройте и запустите свое приложение!  Войдите, используя учетную запись Майкрософт или учетной записи Azure AD и обратите внимание на то, как удостоверение пользователя hello отражается hello верхней панели навигации.  Добавлять и удалять некоторые элементы из списка дел hello пользователь вызывает hello toosee прощелкать OAuth 2.0 API в действии.  Теперь у вас есть веб-приложение и веб-API, защищенные с помощью стандартных отраслевых протоколов, которые могут проверять подлинность пользователей с помощью личных, рабочих и учебных учетных записей.

Справочник по hello выполнить пример (без настройки) [представлена ниже](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).  

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные ресурсы:

* [Руководство разработчика v2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [Тег StackOverflow "azure-active-directory" >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Получение обновлений системы безопасности для наших продуктов
Мы рекомендуем вам уведомления при возникновении события безопасности, посетив tooget [эту страницу](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.

