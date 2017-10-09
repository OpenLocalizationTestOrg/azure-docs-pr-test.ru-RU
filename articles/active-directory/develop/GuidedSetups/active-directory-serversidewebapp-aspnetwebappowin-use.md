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
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a><span data-ttu-id="daa7b-103">Добавление запросов на вход и выход toohandle контроллера</span><span class="sxs-lookup"><span data-stu-id="daa7b-103">Add a controller toohandle sign-in and sign-out requests</span></span>

<span data-ttu-id="daa7b-104">Этот шаг показывает, как toocreate новый tooexpose контроллера вход и выход методы.</span><span class="sxs-lookup"><span data-stu-id="daa7b-104">This step shows how toocreate a new controller tooexpose sign-in and sign-out methods.</span></span>

1.  <span data-ttu-id="daa7b-105">Щелкните правой кнопкой мыши hello `Controllers` папку и выберите пункт`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="daa7b-105">Right click hello `Controllers` folder and select `Add` > `Controller`</span></span>
2.  <span data-ttu-id="daa7b-106">Выберите `MVC (.NET version) Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="daa7b-106">Select `MVC (.NET version) Controller – Empty`.</span></span>
3.  <span data-ttu-id="daa7b-107">Щелкните *Добавить*.</span><span class="sxs-lookup"><span data-stu-id="daa7b-107">Click *Add*</span></span>
4.  <span data-ttu-id="daa7b-108">Присвойте имя контроллеру `HomeController`, а затем щелкните *Добавить*.</span><span class="sxs-lookup"><span data-stu-id="daa7b-108">Name it `HomeController` and click *Add*</span></span>
5.  <span data-ttu-id="daa7b-109">Добавить *OWIN* ссылается на класс toohello:</span><span class="sxs-lookup"><span data-stu-id="daa7b-109">Add *OWIN* references toohello class:</span></span>

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="daa7b-110">Добавьте два метода hello ниже toohandle входа и выхода tooyour контроллера, запуская запрос проверки подлинности через код:</span><span class="sxs-lookup"><span data-stu-id="daa7b-110">Add hello two methods below toohandle sign-in and sign-out tooyour controller by initiating an authentication challenge via code:</span></span>
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

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a><span data-ttu-id="daa7b-111">Создание домашней страницы toosign приложение hello в пользователей по нажатию кнопки входа</span><span class="sxs-lookup"><span data-stu-id="daa7b-111">Create hello app's home page toosign in users via a sign-in button</span></span>

<span data-ttu-id="daa7b-112">В Visual Studio создать новое представление tooadd hello вход кнопку и отображать сведения о пользователе после проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="daa7b-112">In Visual Studio, create a new view tooadd hello sign-in button and display user information after authentication:</span></span>

1.  <span data-ttu-id="daa7b-113">Щелкните правой кнопкой мыши hello `Views\Home` папку и выберите пункт`Add View`</span><span class="sxs-lookup"><span data-stu-id="daa7b-113">Right click hello `Views\Home` folder and select `Add View`</span></span>
2.  <span data-ttu-id="daa7b-114">Назовите его `Index`.</span><span class="sxs-lookup"><span data-stu-id="daa7b-114">Name it `Index`.</span></span>
3.  <span data-ttu-id="daa7b-115">Добавьте следующий HTML, который включает в себя hello кнопка входа, файл toohello hello:</span><span class="sxs-lookup"><span data-stu-id="daa7b-115">Add hello following HTML, which includes hello sign-in button, toohello file:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="daa7b-116">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="daa7b-116">More Information</span></span>
> <span data-ttu-id="daa7b-117">С помощью этой страницы можно добавить кнопку входа в формате SVG с черным фоном:</span><span class="sxs-lookup"><span data-stu-id="daa7b-117">This page adds a sign-in button in SVG format with a black background:</span></span><br/><span data-ttu-id="daa7b-118">![Вход с учетной записью Майкрософт](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span><span class="sxs-lookup"><span data-stu-id="daa7b-118">![Sign-in with Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span></span><br/> <span data-ttu-id="daa7b-119">Дополнительные кнопки входа, перейдите toohello [эту страницу](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "рекомендации по фирменной символике").</span><span class="sxs-lookup"><span data-stu-id="daa7b-119">For more sign-in buttons, please go toohello [this page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span></span>
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a><span data-ttu-id="daa7b-120">Добавление утверждения пользователей toodisplay контроллера</span><span class="sxs-lookup"><span data-stu-id="daa7b-120">Add a controller toodisplay user's claims</span></span>
<span data-ttu-id="daa7b-121">Этот контроллер демонстрирует применение hello hello `[Authorize]` атрибута tooprotect контроллера.</span><span class="sxs-lookup"><span data-stu-id="daa7b-121">This controller demonstrates hello uses of hello `[Authorize]` attribute tooprotect a controller.</span></span> <span data-ttu-id="daa7b-122">Этот атрибут ограничивает доступ toohello контроллера разрешив только прошедшим проверку пользователям.</span><span class="sxs-lookup"><span data-stu-id="daa7b-122">This attribute restricts access toohello controller by only allowing authenticated users.</span></span> <span data-ttu-id="daa7b-123">Здравствуйте, приведенный ниже код использует утверждения пользователей toodisplay атрибут hello, полученные в рамках hello входа в систему.</span><span class="sxs-lookup"><span data-stu-id="daa7b-123">hello code below makes use of hello attribute toodisplay user claims that were retrieved as part of hello sign-in.</span></span>

1.  <span data-ttu-id="daa7b-124">Щелкните правой кнопкой мыши hello `Controllers` папки:`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="daa7b-124">Right click hello `Controllers` folder: `Add` > `Controller`</span></span>
2.  <span data-ttu-id="daa7b-125">Выберите `MVC {version} Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="daa7b-125">Select `MVC {version} Controller – Empty`.</span></span>
3.  <span data-ttu-id="daa7b-126">Щелкните *Добавить*.</span><span class="sxs-lookup"><span data-stu-id="daa7b-126">Click *Add*</span></span>
4.  <span data-ttu-id="daa7b-127">Назовите класс `ClaimsController`.</span><span class="sxs-lookup"><span data-stu-id="daa7b-127">Name it `ClaimsController`</span></span>
5.  <span data-ttu-id="daa7b-128">Замените код hello класса контроллера с кодом hello ниже - это добавляет hello `[Authorize]` toohello класс атрибута:</span><span class="sxs-lookup"><span data-stu-id="daa7b-128">Replace hello code of your controller class with hello code below - this adds hello `[Authorize]` attribute toohello class:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="daa7b-129">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="daa7b-129">More Information</span></span>
> <span data-ttu-id="daa7b-130">Из-за использования hello hello `[Authorize]` атрибута, все методы этого контроллера может быть выполнена, только если hello пользователь прошел проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="daa7b-130">Because of hello use of hello `[Authorize]` attribute, all methods of this controller can only be executed if hello user is authenticated.</span></span> <span data-ttu-id="daa7b-131">Если пользователь hello не прошел проверку подлинности и пытается установить контроллер tooaccess hello, OWIN инициировать запрос проверки подлинности и принудительно tooauthenticate пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="daa7b-131">If hello user is not authenticated and tries tooaccess hello controller, OWIN will initiate an authentication challenge and force hello user tooauthenticate.</span></span> <span data-ttu-id="daa7b-132">Hello кода выполняет поиск в hello утверждений коллекцию hello `ClaimsPrincipal.Current` экземпляр для конкретного пользователя атрибутов, включенных в токен пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="daa7b-132">hello code above looks at hello claims collection of hello `ClaimsPrincipal.Current` instance for specific user attributes included in hello user’s token.</span></span> <span data-ttu-id="daa7b-133">Эти атрибуты включают hello с полным именем пользователя и имя пользователя, а также hello пользователя глобального идентификатора субъекта.</span><span class="sxs-lookup"><span data-stu-id="daa7b-133">These attributes include hello user’s full name and username, as well as hello global user identifier subject.</span></span> <span data-ttu-id="daa7b-134">Он также содержит hello *ИД клиента*, которой представляет идентификатор hello hello пользователя организации.</span><span class="sxs-lookup"><span data-stu-id="daa7b-134">It also contains hello *Tenant ID*, which represents hello ID for hello user’s organization.</span></span> 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a><span data-ttu-id="daa7b-135">Создание представления утверждения toodisplay hello пользователей</span><span class="sxs-lookup"><span data-stu-id="daa7b-135">Create a view toodisplay hello user's claims</span></span>

<span data-ttu-id="daa7b-136">В Visual Studio создайте новое представление утверждения toodisplay hello пользователей на веб-странице:</span><span class="sxs-lookup"><span data-stu-id="daa7b-136">In Visual Studio, create a new view toodisplay hello user's claims in a web page:</span></span>

1.  <span data-ttu-id="daa7b-137">Щелкните правой кнопкой мыши hello `Views\Claims` папки и:`Add View`</span><span class="sxs-lookup"><span data-stu-id="daa7b-137">Right click hello `Views\Claims` folder and: `Add View`</span></span>
2.  <span data-ttu-id="daa7b-138">Назовите его `Index`.</span><span class="sxs-lookup"><span data-stu-id="daa7b-138">Name it `Index`.</span></span>
3.  <span data-ttu-id="daa7b-139">Добавьте следующие файл toohello HTML hello:</span><span class="sxs-lookup"><span data-stu-id="daa7b-139">Add hello following HTML toohello file:</span></span>

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
