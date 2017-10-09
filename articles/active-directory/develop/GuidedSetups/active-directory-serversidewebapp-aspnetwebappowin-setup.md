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
## <a name="set-up-your-project"></a><span data-ttu-id="34d8a-103">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="34d8a-103">Set up your project</span></span>

<span data-ttu-id="34d8a-104">В этом разделе показаны шаги tooinstall hello и настройте hello конвейера проверки подлинности через по промежуточного слоя OWIN в проект ASP.NET с использованием OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="34d8a-104">This section shows hello steps tooinstall and configure hello authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span></span> 

> <span data-ttu-id="34d8a-105">Предпочтение toodownload проекта Visual Studio в этом примере вместо этого?</span><span class="sxs-lookup"><span data-stu-id="34d8a-105">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="34d8a-106">[Загрузка проекта](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) и пропустить toohello [шаг настройки](#create-an-application-express) образец кода hello tooconfigure перед выполнением.</span><span class="sxs-lookup"><span data-stu-id="34d8a-106">[Download a project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a><span data-ttu-id="34d8a-107">Создание проекта ASP.NET</span><span class="sxs-lookup"><span data-stu-id="34d8a-107">Create your ASP.NET project</span></span>

> 1. <span data-ttu-id="34d8a-108">В Visual Studio выберите `File` > `New` > `Project`.</span><span class="sxs-lookup"><span data-stu-id="34d8a-108">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
> 2. <span data-ttu-id="34d8a-109">В разделе *Visual C#\Web* выберите `ASP.NET Web Application (.NET Framework)`.</span><span class="sxs-lookup"><span data-stu-id="34d8a-109">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span></span>
> 3. <span data-ttu-id="34d8a-110">Присвойте имя приложению и нажмите кнопку *ОК*.</span><span class="sxs-lookup"><span data-stu-id="34d8a-110">Name your application and click *OK*</span></span>
> 4. <span data-ttu-id="34d8a-111">Выберите `Empty` и выберите hello флажок tooadd `MVC` ссылки</span><span class="sxs-lookup"><span data-stu-id="34d8a-111">Select `Empty` and select hello checkbox tooadd `MVC` references</span></span>
<!--end-collapse-->

## <a name="add-authentication-components"></a><span data-ttu-id="34d8a-112">Добавление компонентов проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="34d8a-112">Add authentication components</span></span>

1. <span data-ttu-id="34d8a-113">В Visual Studio выберите `Tools` > `Nuget Package Manager` > `Package Manager Console`.</span><span class="sxs-lookup"><span data-stu-id="34d8a-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="34d8a-114">Добавить *пакетов NuGet по промежуточного слоя OWIN* , введя следующее hello в hello в окне консоли диспетчера пакетов:</span><span class="sxs-lookup"><span data-stu-id="34d8a-114">Add *OWIN middleware NuGet packages* by typing hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a><span data-ttu-id="34d8a-115">О библиотеках</span><span class="sxs-lookup"><span data-stu-id="34d8a-115">About these libraries</span></span>

><span data-ttu-id="34d8a-116">библиотеки Hello выше Включение единого входа (SSO) через проверку подлинности на основе файлов cookie с использованием OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="34d8a-116">hello libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span></span> <span data-ttu-id="34d8a-117">После завершения проверки подлинности и hello токен, представляющий hello пользователя отправляется tooyour приложения, по промежуточного слоя OWIN создает файл cookie сеанса.</span><span class="sxs-lookup"><span data-stu-id="34d8a-117">After authentication is completed and hello token representing hello user is sent tooyour application, OWIN middleware creates a session cookie.</span></span> <span data-ttu-id="34d8a-118">Hello обозреватель использует этот файл cookie при последующих запросах, hello пользователю не нужны tooretype свой пароль и требуется дополнительная проверка.</span><span class="sxs-lookup"><span data-stu-id="34d8a-118">hello browser then uses this cookie on subsequent requests so hello user doesn't need tooretype their password, and no additional verification is needed.</span></span>
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a><span data-ttu-id="34d8a-119">Настройка проверки подлинности конвейера hello</span><span class="sxs-lookup"><span data-stu-id="34d8a-119">Configure hello authentication pipeline</span></span>
<span data-ttu-id="34d8a-120">Hello шаги, используемые toocreate OWIN по промежуточного слоя класс запуска tooconfigure OpenID Connect проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="34d8a-120">hello steps below are used toocreate an OWIN middleware Startup Class tooconfigure OpenID Connect authentication.</span></span> <span data-ttu-id="34d8a-121">Этот класс будет выполняться автоматически при запуске процесса IIS.</span><span class="sxs-lookup"><span data-stu-id="34d8a-121">This class will be executed automatically when your IIS process starts.</span></span>

> <span data-ttu-id="34d8a-122">Если ваш проект не имеет `Startup.cs` файл в корневой папке hello:</span><span class="sxs-lookup"><span data-stu-id="34d8a-122">If your project doesn't have a `Startup.cs` file in hello root folder:</span></span><br/>
> 1. <span data-ttu-id="34d8a-123">Щелкните правой кнопкой мыши корневой папки проекта hello: >`Add` > `New Item...` > `OWIN Startup class`</span><span class="sxs-lookup"><span data-stu-id="34d8a-123">Right click on hello project's root folder: >  `Add` > `New Item...` > `OWIN Startup class`</span></span><br/>
> 2. <span data-ttu-id="34d8a-124">Назовите класс `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="34d8a-124">Name it `Startup.cs`</span></span>

> <span data-ttu-id="34d8a-125">Убедитесь, что выбранный класс hello класс запуска OWIN, а не стандартный класс C#.</span><span class="sxs-lookup"><span data-stu-id="34d8a-125">Make sure hello class selected is an OWIN Startup Class and not a standard C# class.</span></span> <span data-ttu-id="34d8a-126">Проверить, проверки, если вы видите `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` выше hello пространства имен.</span><span class="sxs-lookup"><span data-stu-id="34d8a-126">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above hello namespace.</span></span>


1. <span data-ttu-id="34d8a-127">Добавить *OWIN* и *Microsoft.IdentityModel* ссылается слишком`Startup.cs`:</span><span class="sxs-lookup"><span data-stu-id="34d8a-127">Add *OWIN* and *Microsoft.IdentityModel* references too`Startup.cs`:</span></span>

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
<span data-ttu-id="34d8a-128">Замените класс запуска hello код ниже:</span><span class="sxs-lookup"><span data-stu-id="34d8a-128">Replace Startup class with hello code below:</span></span>
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
> ### <a name="more-information"></a><span data-ttu-id="34d8a-129">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="34d8a-129">More Information</span></span>

> <span data-ttu-id="34d8a-130">Здравствуйте, параметры, указываемые в *OpenIDConnectAuthenticationOptions* служат в качестве координат для hello toocommunicate приложений с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34d8a-130">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello application toocommunicate with Azure AD.</span></span> <span data-ttu-id="34d8a-131">Поскольку hello OpenID Connect по промежуточного слоя использует файлы cookie в фоновом режиме hello, необходимо также tooset копирование файла cookie проверки подлинности как код hello выше.</span><span class="sxs-lookup"><span data-stu-id="34d8a-131">Because hello OpenID Connect middleware uses cookies in hello background, you also need tooset up cookie authentication as hello code above shows.</span></span> <span data-ttu-id="34d8a-132">Hello *ValidateIssuer* значение сообщает OpenIdConnect toonot ограничить доступ tooone конкретной организации.</span><span class="sxs-lookup"><span data-stu-id="34d8a-132">hello *ValidateIssuer* value tells OpenIdConnect toonot restrict access tooone specific organization.</span></span>
<!--end-collapse-->

