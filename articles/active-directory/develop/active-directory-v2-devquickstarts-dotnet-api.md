---
title: "Добавление функции входа в веб-API .NET MVC с помощью конечной точки Azure AD версии 2.0 | Документация Майкрософт"
description: "Как создать веб-API .NET MVC, принимающий маркеры доступа личных учетных записей Майкрософт, а также рабочих и учебных учетных записей."
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
ms.openlocfilehash: b2d7bbfcd9218698f71e9dfdb1ad5d9ff8740f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="deb45-103">Безопасность веб-API MVC</span><span class="sxs-lookup"><span data-stu-id="deb45-103">Secure an MVC web API</span></span>
<span data-ttu-id="deb45-104">Используя конечную точку Azure Active Directory версии 2.0, вы можете защитить веб-API с помощью маркеров доступа [OAuth 2.0](active-directory-v2-protocols.md) и позволить пользователям входить в систему с помощью личной, рабочей или учебной учетной записи Майкрософт для безопасного доступа к веб-API.</span><span class="sxs-lookup"><span data-stu-id="deb45-104">With Azure Active Directory the v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts to securely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="deb45-105">Не все сценарии и компоненты Azure Active Directory поддерживаются конечной точкой версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="deb45-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="deb45-106">Чтобы определить, следует ли вам использовать конечную точку версии 2.0, ознакомьтесь с [ограничениями версии 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="deb45-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="deb45-107">В веб-API ASP.NET это можно делать с помощью ПО промежуточного уровня OWIN корпорации Microsoft, включенного в .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="deb45-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="deb45-108">Мы будем использовать OWIN для создания "списка задач" веб-API MVC, который позволяет клиентам создавать и читать задачи из списка дел пользователя.</span><span class="sxs-lookup"><span data-stu-id="deb45-108">Here we’ll use OWIN to build a "To Do List" MVC Web API that allows clients to create and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="deb45-109">Этот веб-API будет проверять, содержат ли входящие запросы действительный маркер доступа, и отклонять запросы, которые не прошли проверку на защищенном маршруте.</span><span class="sxs-lookup"><span data-stu-id="deb45-109">The web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="deb45-110">Этот пример создан с помощью Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="deb45-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="deb45-111">Загрузить</span><span class="sxs-lookup"><span data-stu-id="deb45-111">Download</span></span>
<span data-ttu-id="deb45-112">Код в этом учебнике размещен на портале [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="deb45-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="deb45-113">Для понимания процесса можно [скачать основу приложения как ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) или клонировать ее:</span><span class="sxs-lookup"><span data-stu-id="deb45-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="deb45-114">Скелет приложения включает в себя весь код шаблона простого API, но в нем отсутствуют все компоненты, связанные с удостоверениями.</span><span class="sxs-lookup"><span data-stu-id="deb45-114">The skeleton app includes all the boilerplate code for a simple API, but is missing all of the identity-related pieces.</span></span> <span data-ttu-id="deb45-115">Если не хотите следовать учебнику, вместо этого можно клонировать или [скачать готовый пример](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="deb45-115">If you don't want to follow along, you can instead clone or [download the completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="deb45-116">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="deb45-116">Register an app</span></span>
<span data-ttu-id="deb45-117">Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="deb45-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="deb45-118">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="deb45-118">Make sure to:</span></span>

* <span data-ttu-id="deb45-119">Запишите назначенный вашему приложению **идентификатор приложения**. Он вскоре вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="deb45-119">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>

<span data-ttu-id="deb45-120">В этом решении Visual Studio также содержится клиент TodoListClient, который представляет собой простое приложение WPF.</span><span class="sxs-lookup"><span data-stu-id="deb45-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="deb45-121">TodoListClient используется для того, чтобы показать, как пользователь входит в систему и как клиент может отправлять запросы к вашему веб-API.</span><span class="sxs-lookup"><span data-stu-id="deb45-121">The TodoListClient is used to demonstrate how a user signs-in and how a client can issue requests to your Web API.</span></span>  <span data-ttu-id="deb45-122">В этом случае и TodoListClient, и TodoListService представлены одним приложением.</span><span class="sxs-lookup"><span data-stu-id="deb45-122">In this case, both the TodoListClient and the TodoListService are represented by the same app.</span></span>  <span data-ttu-id="deb45-123">Чтобы настроить TodoListClient, вам нужно также:</span><span class="sxs-lookup"><span data-stu-id="deb45-123">To configure the TodoListClient, you should also:</span></span>

* <span data-ttu-id="deb45-124">Добавьте для приложения **мобильную** платформу.</span><span class="sxs-lookup"><span data-stu-id="deb45-124">Add the **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="deb45-125">Установка OWIN</span><span class="sxs-lookup"><span data-stu-id="deb45-125">Install OWIN</span></span>
<span data-ttu-id="deb45-126">Зарегистрировав приложение, вам нужно настроить в нем обмен данными с конечной точкой v2.0. Это позволит проверять входящие запросы и маркеры.</span><span class="sxs-lookup"><span data-stu-id="deb45-126">Now that you’ve registered an app, you need to set up your app to communicate with the v2.0 endpoint in order to validate incoming requests & tokens.</span></span>

* <span data-ttu-id="deb45-127">Для начала откройте решение и добавьте пакеты NuGet промежуточного слоя OWIN в проект TodoListService с помощью консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="deb45-127">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="deb45-128">Настройка аутентификации OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="deb45-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="deb45-129">Добавьте класс OWIN Startup в проект TodoListService под именем `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="deb45-129">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="deb45-130">Щелкните правой кнопкой мыши проект, выберите в контекстном меню пункты **Добавить** --> **Новый элемент** и найдите OWIN.</span><span class="sxs-lookup"><span data-stu-id="deb45-130">Right click on the project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="deb45-131">При запуске вашего приложения промежуточный слой OWIN вызовет метод `Configuration(…)` .</span><span class="sxs-lookup"><span data-stu-id="deb45-131">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="deb45-132">Замените объявление класса на `public partial class Startup` — часть этого класса уже была реализована в другом файле.</span><span class="sxs-lookup"><span data-stu-id="deb45-132">Change the class declaration to `public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="deb45-133">В методе `Configuration(…)` добавьте вызов ConfgureAuth(...), чтобы настроить проверку подлинности для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="deb45-133">In the `Configuration(…)` method, make a call to ConfgureAuth(…) to set up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="deb45-134">Откройте файл `App_Start\Startup.Auth.cs` и реализуйте метод `ConfigureAuth(…)`, который настраивает веб-API для приема маркеров доступа из конечной точки версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="deb45-134">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method, which will set up the Web API to accept tokens from the v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, the TodoListClient and TodoListService
                // are represented using the same Application Id - we use
                // the Application Id to represent the audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that the user's organization (if applicable) has
                // signed up for the app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up the OWIN pipeline to use OAuth 2.0 Bearer authentication.
        // The options provided here tell the middleware about the type of tokens
        // that will be recieved, which are JWTs for the v2.0 endpoint.

        // NOTE: The usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by the v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used to fetch & use the OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="deb45-135">Теперь можно использовать атрибуты `[Authorize]` для защиты контроллеров и действий с помощью аутентификации OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="deb45-135">Now you can use `[Authorize]` attributes to protect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="deb45-136">Снабдите класс `Controllers\TodoListController.cs` тегом авторизации.</span><span class="sxs-lookup"><span data-stu-id="deb45-136">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="deb45-137">Пользователь будет вынужден войти в систему, прежде чем сможет обратиться к этой странице.</span><span class="sxs-lookup"><span data-stu-id="deb45-137">This will force the user to sign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="deb45-138">Когда авторизованный вызывающий объект успешно вызывает один из интерфейсов API `TodoListController` , может потребоваться доступ к сведениям о вызывающем объекте.</span><span class="sxs-lookup"><span data-stu-id="deb45-138">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span>  <span data-ttu-id="deb45-139">OWIN предоставляет доступ к утверждениям внутри маркера защиты посредством объекта `ClaimsPrincpal` .</span><span class="sxs-lookup"><span data-stu-id="deb45-139">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use the ClaimsPrincipal to access information about the
    // user making the call.  In this case, we use the 'sub' or
    // NameIdentifier claim to serve as a key for the tasks in the data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="deb45-140">Наконец, откройте файл `web.config` в корне проекта TodoListService, а затем введите значения конфигурации в разделе `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="deb45-140">Finally, open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="deb45-141">Ваш `ida:Audience` — это **идентификатор приложения** , введенный на портале.</span><span class="sxs-lookup"><span data-stu-id="deb45-141">Your `ida:Audience` is the **Application Id** of the app that you entered in the portal.</span></span>

## <a name="configure-the-client-app"></a><span data-ttu-id="deb45-142">Настройка клиентского приложения</span><span class="sxs-lookup"><span data-stu-id="deb45-142">Configure the client app</span></span>
<span data-ttu-id="deb45-143">Чтобы увидеть службу To Do List в действии, необходимо настроить To Do List Client для получения маркеров от конечной точки версии 2.0 и выполнения вызовов службы.</span><span class="sxs-lookup"><span data-stu-id="deb45-143">Before you can see the Todo List Service in action, you need to configure the Todo List Client so it can get tokens from the v2.0 endpoint and make calls to the service.</span></span>

* <span data-ttu-id="deb45-144">Откройте файл `App.config` проекта TodoListClient и введите значения конфигурации в разделе `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="deb45-144">In the TodoListClient project, open `App.config` and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="deb45-145">Идентификатор приложения `ida:ClientId` , скопированный на портале.</span><span class="sxs-lookup"><span data-stu-id="deb45-145">Your `ida:ClientId` Application Id you copied from the portal.</span></span>

<span data-ttu-id="deb45-146">Наконец, выполните очистку, соберите и запустите каждый из проектов.</span><span class="sxs-lookup"><span data-stu-id="deb45-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="deb45-147">Теперь у вас есть веб-API .NET MVC, принимающий маркеры доступа личных учетных записей Майкрософт, а также рабочих и учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="deb45-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="deb45-148">Войдите в TodoListClient и вызовите веб-API для добавления задач в список дел пользователя.</span><span class="sxs-lookup"><span data-stu-id="deb45-148">Sign into the TodoListClient, and call your web api to add tasks to the user's To-Do list.</span></span>

<span data-ttu-id="deb45-149">Готовый пример (без ваших значений конфигурации) [можно скачать в виде ZIP-файла здесь](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip)или клонировать с портала GitHub.</span><span class="sxs-lookup"><span data-stu-id="deb45-149">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="deb45-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="deb45-150">Next steps</span></span>
<span data-ttu-id="deb45-151">Теперь можно приступить к изучению других разделов.</span><span class="sxs-lookup"><span data-stu-id="deb45-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="deb45-152">Можно попробовать:</span><span class="sxs-lookup"><span data-stu-id="deb45-152">You may want to try:</span></span>

[<span data-ttu-id="deb45-153">Вызов веб-API из веб-приложения >></span><span class="sxs-lookup"><span data-stu-id="deb45-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="deb45-154">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="deb45-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="deb45-155">Руководство разработчика версии 2.0 >></span><span class="sxs-lookup"><span data-stu-id="deb45-155">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="deb45-156">Тег StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="deb45-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="deb45-157">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="deb45-157">Get security updates for our products</span></span>
<span data-ttu-id="deb45-158">Рекомендуем вам настроить уведомления о нарушениях безопасности. Это можно сделать, подписавшись на уведомления безопасности консультационных служб на [этой странице](https://technet.microsoft.com/security/dd252948).</span><span class="sxs-lookup"><span data-stu-id="deb45-158">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
