---
title: "aaaAdd tooa входа в веб-API .NET MVC с помощью hello конечная точка Azure AD v2.0 | Документы Microsoft"
description: "Как toobuild веб-Api .NET MVC, который принимает токены из обоих личную учетную запись Майкрософт и рабочих учетных записей."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="f7839-103">Безопасность веб-API MVC</span><span class="sxs-lookup"><span data-stu-id="f7839-103">Secure an MVC web API</span></span>
<span data-ttu-id="f7839-104">С конечной точкой v2.0 hello Azure Active Directory, чтобы защитить веб-API с помощью [OAuth 2.0](active-directory-v2-protocols.md) маркеры доступа, позволяя пользователей с обоих личную учетную запись Майкрософт и рабочих учетных записей toosecurely доступ к веб-API.</span><span class="sxs-lookup"><span data-stu-id="f7839-104">With Azure Active Directory hello v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts toosecurely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="f7839-105">Не все сценарии Azure Active Directory и возможности поддерживаются hello v2.0 конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="f7839-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="f7839-106">toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="f7839-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="f7839-107">В веб-API ASP.NET это можно делать с помощью ПО промежуточного уровня OWIN корпорации Microsoft, включенного в .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f7839-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="f7839-108">Здесь мы будем использовать OWIN toobuild веб-API MVC «tooDo списка», позволяющую клиентам toocreate и чтения задачи в список дел пользователя.</span><span class="sxs-lookup"><span data-stu-id="f7839-108">Here we’ll use OWIN toobuild a "tooDo List" MVC Web API that allows clients toocreate and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="f7839-109">Hello веб-API будет проверять входящие запросы содержат действительный маркер доступа и отклонять запросы, которые не прошли проверку на защищенном маршрут.</span><span class="sxs-lookup"><span data-stu-id="f7839-109">hello web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="f7839-110">Этот пример создан с помощью Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="f7839-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="f7839-111">Загрузить</span><span class="sxs-lookup"><span data-stu-id="f7839-111">Download</span></span>
<span data-ttu-id="f7839-112">поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="f7839-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="f7839-113">можно toofollow вдоль [загрузить приложение hello основу как .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) или основу hello клона:</span><span class="sxs-lookup"><span data-stu-id="f7839-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="f7839-114">каркас приложение Hello включает все hello стандартный код для простой API-Интерфейс, но не удалось обнаружить все компоненты, связанные с идентификаторами hello.</span><span class="sxs-lookup"><span data-stu-id="f7839-114">hello skeleton app includes all hello boilerplate code for a simple API, but is missing all of hello identity-related pieces.</span></span> <span data-ttu-id="f7839-115">Если вы не хотите toofollow вдоль, вместо этого можно клонировать или [загрузить образец hello завершения](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f7839-115">If you don't want toofollow along, you can instead clone or [download hello completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="f7839-116">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="f7839-116">Register an app</span></span>
<span data-ttu-id="f7839-117">Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f7839-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="f7839-118">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="f7839-118">Make sure to:</span></span>

* <span data-ttu-id="f7839-119">Копировать вниз hello **идентификатор приложения** назначены tooyour приложения, оно понадобится скоро.</span><span class="sxs-lookup"><span data-stu-id="f7839-119">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>

<span data-ttu-id="f7839-120">В этом решении Visual Studio также содержится клиент TodoListClient, который представляет собой простое приложение WPF.</span><span class="sxs-lookup"><span data-stu-id="f7839-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="f7839-121">Hello TodoListClient является toodemonstrate используется как пользователь выполняет вход и каким образом клиент может выдавать запросы tooyour веб-API.</span><span class="sxs-lookup"><span data-stu-id="f7839-121">hello TodoListClient is used toodemonstrate how a user signs-in and how a client can issue requests tooyour Web API.</span></span>  <span data-ttu-id="f7839-122">В этом случае hello TodoListClient и hello TodoListService представляются hello то же приложение.</span><span class="sxs-lookup"><span data-stu-id="f7839-122">In this case, both hello TodoListClient and hello TodoListService are represented by hello same app.</span></span>  <span data-ttu-id="f7839-123">tooconfigure Здравствуйте TodoListClient, также следует:</span><span class="sxs-lookup"><span data-stu-id="f7839-123">tooconfigure hello TodoListClient, you should also:</span></span>

* <span data-ttu-id="f7839-124">Добавить hello **Mobile** платформы для приложения.</span><span class="sxs-lookup"><span data-stu-id="f7839-124">Add hello **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="f7839-125">Установка OWIN</span><span class="sxs-lookup"><span data-stu-id="f7839-125">Install OWIN</span></span>
<span data-ttu-id="f7839-126">Теперь, после регистрации приложения, нужно tooset копирование toocommunicate вашего приложения с конечной точкой v2.0 hello в порядке toovalidate входящие запросы и ответы маркеры.</span><span class="sxs-lookup"><span data-stu-id="f7839-126">Now that you’ve registered an app, you need tooset up your app toocommunicate with hello v2.0 endpoint in order toovalidate incoming requests & tokens.</span></span>

* <span data-ttu-id="f7839-127">toobegin, откройте решение hello и добавьте hello OWIN по промежуточного слоя NuGet пакеты toohello TodoListService проекта с помощью консоли диспетчера пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="f7839-127">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="f7839-128">Настройка аутентификации OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="f7839-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="f7839-129">Добавить проект TodoListService запуска OWIN класса toohello вызывается `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="f7839-129">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="f7839-130">Щелкните правой кнопкой мыши на проекте hello--> **добавить** --> **новый элемент** --> Поиск «OWIN».</span><span class="sxs-lookup"><span data-stu-id="f7839-130">Right click on hello project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="f7839-131">по промежуточного слоя OWIN Hello будет вызывать hello `Configuration(…)` метод при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="f7839-131">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="f7839-132">Измените объявление класса hello слишком`public partial class Startup` -мы уже реализовали часть этого класса для вас в другом файле.</span><span class="sxs-lookup"><span data-stu-id="f7839-132">Change hello class declaration too`public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="f7839-133">В hello `Configuration(…)` метод, сделать tooset tooConfgureAuth(...) вызов проверку подлинности для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f7839-133">In hello `Configuration(…)` method, make a call tooConfgureAuth(…) tooset up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="f7839-134">Привет открыть файл `App_Start\Startup.Auth.cs` и реализовать hello `ConfigureAuth(…)` метод, который будет Настройка маркеров tooaccept hello веб-API от конечной точки v2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="f7839-134">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method, which will set up hello Web API tooaccept tokens from hello v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="f7839-135">Теперь вы можете использовать `[Authorize]` атрибуты tooprotect контроллеров и действий с помощью проверки подлинности носителя OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="f7839-135">Now you can use `[Authorize]` attributes tooprotect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="f7839-136">Украшение hello `Controllers\TodoListController.cs` класса с помощью тега authorize.</span><span class="sxs-lookup"><span data-stu-id="f7839-136">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="f7839-137">Это заставит toosign пользователя hello в перед получением доступа к этой странице.</span><span class="sxs-lookup"><span data-stu-id="f7839-137">This will force hello user toosign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="f7839-138">Когда вызывающий объект авторизованным успешно вызывает один hello `TodoListController` API-интерфейсы, действие hello может иметь доступа tooinformation о вызывающем модуле hello.</span><span class="sxs-lookup"><span data-stu-id="f7839-138">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span>  <span data-ttu-id="f7839-139">OWIN предоставляет доступ toohello утверждения в маркер носителя hello через hello `ClaimsPrincpal` объекта.</span><span class="sxs-lookup"><span data-stu-id="f7839-139">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="f7839-140">Наконец, откройте hello `web.config` файл в корне hello проект TodoListService hello и введите значения конфигурации в hello `<appSettings>` раздела.</span><span class="sxs-lookup"><span data-stu-id="f7839-140">Finally, open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="f7839-141">Ваш `ida:Audience` — hello **идентификатор приложения** приложения hello, введенное на портале hello.</span><span class="sxs-lookup"><span data-stu-id="f7839-141">Your `ida:Audience` is hello **Application Id** of hello app that you entered in hello portal.</span></span>

## <a name="configure-hello-client-app"></a><span data-ttu-id="f7839-142">Настройка клиентского приложения hello</span><span class="sxs-lookup"><span data-stu-id="f7839-142">Configure hello client app</span></span>
<span data-ttu-id="f7839-143">Чтобы увидеть hello службы Todo List в действии, необходимо tooconfigure hello Todo List Client, чтобы можно было получить токены из конечной точки v2.0 hello и сделать службу toohello вызовы.</span><span class="sxs-lookup"><span data-stu-id="f7839-143">Before you can see hello Todo List Service in action, you need tooconfigure hello Todo List Client so it can get tokens from hello v2.0 endpoint and make calls toohello service.</span></span>

* <span data-ttu-id="f7839-144">В проекте TodoListClient hello откройте `App.config` и введите значения конфигурации в hello `<appSettings>` раздела.</span><span class="sxs-lookup"><span data-stu-id="f7839-144">In hello TodoListClient project, open `App.config` and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="f7839-145">Ваш `ida:ClientId` идентификатор приложения, скопированные из портала hello.</span><span class="sxs-lookup"><span data-stu-id="f7839-145">Your `ida:ClientId` Application Id you copied from hello portal.</span></span>

<span data-ttu-id="f7839-146">Наконец, выполните очистку, соберите и запустите каждый из проектов.</span><span class="sxs-lookup"><span data-stu-id="f7839-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="f7839-147">Теперь у вас есть веб-API .NET MVC, принимающий маркеры доступа личных учетных записей Майкрософт, а также рабочих и учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="f7839-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="f7839-148">Вход в hello TodoListClient и вызовите список дел web api tooadd задачи toohello конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="f7839-148">Sign into hello TodoListClient, and call your web api tooadd tasks toohello user's To-Do list.</span></span>

<span data-ttu-id="f7839-149">Справочник по hello выполнить пример (без настройки) [предоставляется как .zip здесь](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), или вы можете клонировать из GitHub:</span><span class="sxs-lookup"><span data-stu-id="f7839-149">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="f7839-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f7839-150">Next steps</span></span>
<span data-ttu-id="f7839-151">Теперь можно приступить к изучению других разделов.</span><span class="sxs-lookup"><span data-stu-id="f7839-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="f7839-152">Вы можете tootry:</span><span class="sxs-lookup"><span data-stu-id="f7839-152">You may want tootry:</span></span>

[<span data-ttu-id="f7839-153">Вызов веб-API из веб-приложения >></span><span class="sxs-lookup"><span data-stu-id="f7839-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="f7839-154">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="f7839-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="f7839-155">Руководство разработчика v2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="f7839-155">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="f7839-156">Тег StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="f7839-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="f7839-157">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="f7839-157">Get security updates for our products</span></span>
<span data-ttu-id="f7839-158">Мы рекомендуем вам уведомления при возникновении события безопасности, посетив tooget [эту страницу](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.</span><span class="sxs-lookup"><span data-stu-id="f7839-158">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
