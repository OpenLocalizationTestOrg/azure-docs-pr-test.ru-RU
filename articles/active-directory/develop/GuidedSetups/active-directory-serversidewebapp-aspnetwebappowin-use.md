---
title: "aaaAzure AD v2 ASP.NET Web Server Приступая к работе - Используйте | Документы Microsoft"
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
ms.openlocfilehash: 03afce6fa6598215e8c4af841c00762c143a0cd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a>Добавление запросов на вход и выход toohandle контроллера

Этот шаг показывает, как toocreate новый tooexpose контроллера вход и выход методы.

1.  Щелкните правой кнопкой мыши hello `Controllers` папку и выберите пункт`Add` > `Controller`
2.  Выберите `MVC (.NET version) Controller – Empty`.
3.  Щелкните *Добавить*.
4.  Присвойте имя контроллеру `HomeController`, а затем щелкните *Добавить*.
5.  Добавить *OWIN* ссылается на класс toohello:

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Добавьте два метода hello ниже toohandle входа и выхода tooyour контроллера, запуская запрос проверки подлинности через код:
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate hello SignIn method with hello [Authorize] attribute
/// </summary>
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}

/// <summary>
/// Send an OpenID Connect sign-out request.
/// </summary>
public void SignOut()
{
    HttpContext.GetOwinContext().Authentication.SignOut(
            OpenIdConnectAuthenticationDefaults.AuthenticationType,
            CookieAuthenticationDefaults.AuthenticationType);
}
```

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a>Создание домашней страницы toosign приложение hello в пользователей по нажатию кнопки входа

В Visual Studio создать новое представление tooadd hello вход кнопку и отображать сведения о пользователе после проверки подлинности:

1.  Щелкните правой кнопкой мыши hello `Views\Home` папку и выберите пункт`Add View`
2.  Назовите его `Index`.
3.  Добавьте следующий HTML, который включает в себя hello кнопка входа, файл toohello hello:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If hello user is not authenticated, display hello sign-in button -->
    <a href="@Url.Action("SignIn", "Home")" style="text-decoration: none;">
        <svg xmlns="http://www.w3.org/2000/svg" xml:space="preserve" width="300px" height="50px" viewBox="0 0 3278 522" class="SignInButton">
        <style type="text/css">.fil0:hover {fill: #4B4B4B;} .fnt0 {font-size: 260px;font-family: 'Segoe UI Semibold', 'Segoe UI'; text-decoration: none;}</style>
        <rect class="fil0" x="2" y="2" width="3174" height="517" fill="black" />
        <rect x="150" y="129" width="122" height="122" fill="#F35325" />
        <rect x="284" y="129" width="122" height="122" fill="#81BC06" />
        <rect x="150" y="263" width="122" height="122" fill="#05A6F0" />
        <rect x="284" y="263" width="122" height="122" fill="#FFBA08" />
        <text x="470" y="357" fill="white" class="fnt0">Sign in with Microsoft</text>
        </svg>
    </a>
}
else
{
    <span><br/>Hello @System.Security.Claims.ClaimsPrincipal.Current.FindFirst("name").Value;</span>
    <br /><br />
    @Html.ActionLink("See Your Claims", "Index", "Claims")
    <br /><br />
    @Html.ActionLink("Sign out", "SignOut", "Home")
}
@if (!string.IsNullOrWhiteSpace(Request.QueryString["errormessage"]))
{
    <div style="background-color:red;color:white;font-weight: bold;">Error: @Request.QueryString["errormessage"]</div>
}
</body>
</html>
```
<!--start-collapse-->
### <a name="more-information"></a>Дополнительные сведения
> С помощью этой страницы можно добавить кнопку входа в формате SVG с черным фоном:<br/>![Вход с учетной записью Майкрософт](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)<br/> Дополнительные кнопки входа, перейдите toohello [эту страницу](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "рекомендации по фирменной символике").
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a>Добавление утверждения пользователей toodisplay контроллера
Этот контроллер демонстрирует применение hello hello `[Authorize]` атрибута tooprotect контроллера. Этот атрибут ограничивает доступ toohello контроллера разрешив только прошедшим проверку пользователям. Здравствуйте, приведенный ниже код использует утверждения пользователей toodisplay атрибут hello, полученные в рамках hello входа в систему.

1.  Щелкните правой кнопкой мыши hello `Controllers` папки:`Add` > `Controller`
2.  Выберите `MVC {version} Controller – Empty`.
3.  Щелкните *Добавить*.
4.  Назовите класс `ClaimsController`.
5.  Замените код hello класса контроллера с кодом hello ниже - это добавляет hello `[Authorize]` toohello класс атрибута:

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims tooviewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get hello user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // hello 'preferred_username' claim can be used for showing hello username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // hello subject claim can be used toouniquely identify hello user across hello web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is hello unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Дополнительные сведения
> Из-за использования hello hello `[Authorize]` атрибута, все методы этого контроллера может быть выполнена, только если hello пользователь прошел проверку подлинности. Если пользователь hello не прошел проверку подлинности и пытается установить контроллер tooaccess hello, OWIN инициировать запрос проверки подлинности и принудительно tooauthenticate пользователя hello. Hello кода выполняет поиск в hello утверждений коллекцию hello `ClaimsPrincipal.Current` экземпляр для конкретного пользователя атрибутов, включенных в токен пользователя hello. Эти атрибуты включают hello с полным именем пользователя и имя пользователя, а также hello пользователя глобального идентификатора субъекта. Он также содержит hello *ИД клиента*, которой представляет идентификатор hello hello пользователя организации. 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a>Создание представления утверждения toodisplay hello пользователей

В Visual Studio создайте новое представление утверждения toodisplay hello пользователей на веб-странице:

1.  Щелкните правой кнопкой мыши hello `Views\Claims` папки и:`Add View`
2.  Назовите его `Index`.
3.  Добавьте следующие файл toohello HTML hello:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Sample</title>
    <link href="@Url.Content("~/Content/bootstrap.min.css")" rel="stylesheet" type="text/css" />
</head>
<body style="padding:50px">
    <h3>Main Claims:</h3>
    <table class="table table-striped table-bordered table-hover">
        <tr><td>Name</td><td>@ViewBag.Name</td></tr>
        <tr><td>Username</td><td>@ViewBag.Username</td></tr>
        <tr><td>Subject</td><td>@ViewBag.Subject</td></tr>
        <tr><td>TenantId</td><td>@ViewBag.TenantId</td></tr>
    </table>
    <br />
    <h3>All Claims:</h3>
    <table class="table table-striped table-bordered table-hover table-condensed">
    @foreach (var claim in System.Security.Claims.ClaimsPrincipal.Current.Claims)
    {
        <tr><td>@claim.Type</td><td>@claim.Value</td></tr>
    }
</table>
    <br />
    <br />
    @Html.ActionLink("Sign out", "SignOut", "Home", null, new { @class = "btn btn-primary" })
</body>
</html>
```
