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
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a>Вход в веб-приложение ASP.NET и выход из него с помощью Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Предоставив один вход и выход с помощью всего нескольких строк кода, Azure Active Directory (Azure AD) упрощает вы toooutsource веб-приложения диспетчера удостоверений. Можно подписать пользователей и из него веб-приложения ASP.NET с использованием реализации Microsoft Привет открыть веб-интерфейс для по промежуточного слоя .NET (OWIN). Поддерживаемое сообществом ПО промежуточного слоя OWIN включено в .NET Framework 4.5. В этой статье показано, как toouse OWIN для:

* Вход пользователей tooweb приложений с помощью Azure AD как поставщика удостоверений hello.
* отображать некоторые сведения о пользователе;
* Вход пользователей из приложения hello.

## <a name="before-you-get-started"></a>Необходимые условия
* Загрузите hello [основу приложения](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) или загрузить hello [полного примера](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).
* Необходимо также клиент Azure AD, в которой приложение hello tooregister. Если у вас еще нет клиента Azure AD, [Узнайте, как один tooget](active-directory-howto-tenant.md).

Когда будете готовы, выполните процедуры hello в hello рядом в четырех разделах.

## <a name="step-1-register-hello-new-app-with-azure-ad"></a>Шаг 1: Регистрация нового приложения hello в Azure AD
tooset пользователей tooauthenticate приложения hello, зарегистрировать его в клиенте, выполнив hello ниже:

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. На верхней панели hello щелкните имя вашей учетной записи. В разделе hello **каталога** список, клиент Active Directory hello выберите нужное приложение hello tooregister.
3. Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений**, а затем выберите **Добавить**.
5. Выполните hello предлагает toocreate новый **веб-приложение или WebAPI**.
  * **Имя** описывает toousers приложения hello.
  * **URL-адрес входа** hello базовый URL-адрес приложения hello. URL-адрес по умолчанию Hello основу — https://localhost:44320 /.
6. После завершения регистрации hello Azure AD присваивает приложение hello уникальный идентификатор приложения. Скопируйте значение hello из toouse страницы приложения hello в следующих разделах hello.
7. Из hello **параметры** -> **свойства** страницы приложения, обновите URI идентификатора приложения hello. Hello **URI идентификатора приложения** — это уникальный идентификатор для приложения hello. Hello именования — `https://<tenant-domain>/<app-name>` (например, `https://contoso.onmicrosoft.com/my-first-aad-app`).

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Шаг 2: Настройка проверки подлинности конвейер OWIN hello hello приложения toouse
На этом шаге настраивается hello OWIN по промежуточного слоя toouse hello OpenID Connect протокол проверки подлинности. Использование запросов OWIN tooissue входа и выхода, управлять сеансами пользователей, получить сведения о пользователе и т.д.

1. toobegin, добавить toohello hello OWIN по промежуточного слоя NuGet пакетов проекта с помощью консоли диспетчера пакетов hello.

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. вызывается проект запуска OWIN класса toohello tooadd `Startup.cs`, щелкните правой кнопкой мыши проект hello, выберите **добавить**выберите **новый элемент**и выполните поиск **OWIN**. по промежуточного слоя OWIN Hello вызывает hello **Configuration(...)**  метод при запуске приложение hello.
3. Измените объявление класса hello слишком`public partial class Startup`. Часть этого класса уже была реализована в другом файле. В hello **Configuration(...)**  метод, вызвать слишком**ConfgureAuth(...)**  tooset проверку подлинности для приложения hello.  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. Откройте файл App_Start\Startup.Auth.cs hello, а затем реализуйте hello **ConfigureAuth(...)**  метод. Здравствуйте, параметры, указываемые в *OpenIDConnectAuthenticationOptions* служат в качестве координат для hello toocommunicate приложений с Azure AD. Необходимо также tooset копирование файла cookie проверки подлинности, так как по промежуточного слоя, OpenID Connect hello использует куки-файлы в фоновом режиме hello.

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

5. Откройте файл web.config hello в корневой hello hello проекта, а затем введите значения конфигурации hello в hello `<appSettings>` раздела.
  * `ida:ClientId`: hello GUID, был скопирован из hello портал Azure на «шаг 1: hello зарегистрировать новое приложение с Azure AD.»
  * `ida:Tenant`: hello имя вашего клиента Azure AD (например, contoso.onmicrosoft.com).
  * `ida:PostLogoutRedirectUri`: hello индикатор, который сообщает Azure AD, которому следует перенаправлять пользователя после успешного завершения запроса выхода.

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Шаг 3: Использование tooAzure AD запросов OWIN tooissue входа и выхода
приложение Hello сейчас правильно настроен toocommunicate с Azure AD с помощью протокола проверки подлинности OpenID Connect hello. OWIN обработала все подробности hello отправляемого сообщения проверки подлинности, проверки токенов из Azure AD и поддержку пользовательских сеансов. Все, что остается является toogive пользователей toosign способом в и выхода.

1. Можно использовать теги в toosign пользователей toorequire вашей контроллеров, в авторизации, перед доступом к некоторые страницы. toodo таким образом, откройте Controllers\HomeController.cs, а затем добавьте hello `[Authorize]` тега toohello о контроллере.

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. Также можно использовать запросов OWIN toodirectly проблема проверки подлинности из кода. toodo откройте Controllers\AccountController.cs. Затем в действиях SignIn() и SignOut() hello, выдавать запроса OpenID Connect и запросах на выход.

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

3. Откройте одну\_LoginPartial.cshtml tooshow hello пользователя hello приложения входа и выхода ссылки и tooprint в представлении имя пользователя hello.

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

## <a name="step-4-display-user-information"></a>Шаг 4. Отображение сведений о пользователе
При проверке подлинности пользователей с OpenID Connect, Azure AD возвращает id_token toohello приложение, которое содержит «утверждения» или утверждения о пользователе hello. Можно использовать приложение hello toopersonalize этих утверждений, выполнив hello ниже:

1. Откройте файл Controllers\HomeController.cs hello. Можно использовать утверждения пользователей hello в контроллерах через hello `ClaimsPrincipal.Current` объект субъекта безопасности.

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

2. Постройте и запустите приложение hello. Если уже еще не создан новый пользователь в клиенте с домен onmicrosoft.com, поэтому теперь является toodo время hello. Этот процесс описывается далее.

  а. Вход пользователя и обратите внимание на то, как удостоверение пользователя hello отражается на верхней панели hello.

  b. Выйдите, а затем снова войдите от имени другого пользователя в своем клиенте.

  c. Если у вас серьезные цели, зарегистрируйте и запустите другой экземпляр данного приложения (с его собственным clientId) и рассмотрите процесс единого входа в действии.

## <a name="next-steps"></a>Дальнейшие действия
Справочную информацию см. в разделе [образец hello завершения](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (без настройки).

Теперь можно переходить на toomore дополнительные разделы. Например, попробуйте использовать [защиту веб-API с помощью Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
