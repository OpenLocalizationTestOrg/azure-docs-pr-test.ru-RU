---
title: "Приступая к работе с Azure AD для веб-API .NET | Документация Майкрософт"
description: "Практическое руководство по созданию веб-API для .NET MVC, который интегрируется с Azure AD для аутентификации и авторизации."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f44d75f45073a5d9aa9b1863ed227aba4efcf785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="158c3-103">Защита веб-API с помощью токенов носителя из Azure AD</span><span class="sxs-lookup"><span data-stu-id="158c3-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="158c3-104">Если вы создаете приложение, которое предоставляет доступ к конфиденциальным ресурсам, то необходимо знать, как предотвратить несанкционированный доступ к этим ресурсам.</span><span class="sxs-lookup"><span data-stu-id="158c3-104">If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.</span></span>
<span data-ttu-id="158c3-105">Azure Active Directory (Azure AD) упрощает для разработчика процесс защиты веб-API с помощью токенов носителя OAuth 2.0 — потребуется добавить всего несколько строк кода.</span><span class="sxs-lookup"><span data-stu-id="158c3-105">Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="158c3-106">В веб-приложениях ASP.NET эту защиту можно реализовать с помощью поддерживаемого сообществом ПО промежуточного слоя OWIN корпорации Майкрософт, включенного в .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="158c3-106">In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="158c3-107">Мы будем использовать OWIN для создания веб-API To Do List, который:</span><span class="sxs-lookup"><span data-stu-id="158c3-107">Here we’ll use OWIN to build a "To Do List" web API that:</span></span>

* <span data-ttu-id="158c3-108">указывает, какие API защищены;</span><span class="sxs-lookup"><span data-stu-id="158c3-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="158c3-109">проверяет, содержат ли вызовы веб-API действительный маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="158c3-109">Validates that the web API calls contain a valid access token.</span></span>

<span data-ttu-id="158c3-110">Для сборки API списка дел сначала необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="158c3-110">To build the To Do List API, you first need to:</span></span>

1. <span data-ttu-id="158c3-111">зарегистрировать приложение в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="158c3-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="158c3-112">Настроить приложение для использования конвейера аутентификации OWIN.</span><span class="sxs-lookup"><span data-stu-id="158c3-112">Set up the app to use the OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="158c3-113">Настроить клиентское приложение для вызова веб-API.</span><span class="sxs-lookup"><span data-stu-id="158c3-113">Configure a client application to call the web API.</span></span>

<span data-ttu-id="158c3-114">Чтобы начать работу, [скачайте схему приложения](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) или [скачайте готовый пример](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="158c3-114">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="158c3-115">Каждый из них является решением Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="158c3-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="158c3-116">Вам также потребуется клиент Azure AD для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="158c3-116">You also need an Azure AD tenant in which to register your application.</span></span> <span data-ttu-id="158c3-117">Если у вас нет клиента, [узнайте, как его получить](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="158c3-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="158c3-118">Шаг 1. Регистрация приложения в Azure AD</span><span class="sxs-lookup"><span data-stu-id="158c3-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="158c3-119">Для защиты приложения необходимо сначала создать приложение в клиенте и предоставить Azure AD некоторую важную информации.</span><span class="sxs-lookup"><span data-stu-id="158c3-119">To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="158c3-120">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="158c3-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="158c3-121">На верхней панели щелкните свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="158c3-121">On the top bar, click your account.</span></span> <span data-ttu-id="158c3-122">В списке **Каталог** выберите клиент Azure AD, в котором будет зарегистрировано приложение.</span><span class="sxs-lookup"><span data-stu-id="158c3-122">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>

3. <span data-ttu-id="158c3-123">В области слева щелкните **Больше служб** и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="158c3-123">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="158c3-124">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="158c3-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="158c3-125">Следуйте инструкциям на экране, а затем создайте **веб-приложение и (или) веб-API**.</span><span class="sxs-lookup"><span data-stu-id="158c3-125">Follow the prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="158c3-126">**Имя** приложения является его описанием для пользователей.</span><span class="sxs-lookup"><span data-stu-id="158c3-126">**Name** describes your application to users.</span></span> <span data-ttu-id="158c3-127">Введите **Служба списка дел**.</span><span class="sxs-lookup"><span data-stu-id="158c3-127">Enter **To Do List Service**.</span></span>
  * <span data-ttu-id="158c3-128">**URI перенаправления** представляет собой сочетание схемы и строки, используемое Azure AD для возвращения любых токенов, запрошенных приложением.</span><span class="sxs-lookup"><span data-stu-id="158c3-128">**Redirect Uri** is a scheme and string combination that Azure AD uses to return any tokens that your app has requested.</span></span> <span data-ttu-id="158c3-129">Укажите `https://localhost:44321/` для этого параметра.</span><span class="sxs-lookup"><span data-stu-id="158c3-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="158c3-130">На странице **Параметры** -> **Свойства** приложения обновите его универсальный код ресурса (URI) идентификатора.</span><span class="sxs-lookup"><span data-stu-id="158c3-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="158c3-131">Введите идентификатор конкретного клиента.</span><span class="sxs-lookup"><span data-stu-id="158c3-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="158c3-132">Например, введите `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="158c3-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="158c3-133">Сохраните конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="158c3-133">Save the configuration.</span></span> <span data-ttu-id="158c3-134">Не закрывайте портал, так как через некоторое время потребуется зарегистрировать клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="158c3-134">Leave the portal open, because you'll also need to register your client application shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="158c3-135">Шаг 2. Настройка приложения для использования конвейера аутентификации OWIN</span><span class="sxs-lookup"><span data-stu-id="158c3-135">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="158c3-136">Чтобы проверять входящие запросы и токены, необходимо настроить приложение для взаимодействия с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="158c3-136">To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.</span></span>

1. <span data-ttu-id="158c3-137">Для начала откройте решение и добавьте пакеты NuGet для ПО промежуточного слоя OWIN в проект TodoListService с помощью консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="158c3-137">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="158c3-138">Добавьте класс OWIN Startup в проект TodoListService под именем `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="158c3-138">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="158c3-139">Щелкните проект правой кнопкой мыши и выберите **Добавить** > **Новый элемент**, после чего найдите **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="158c3-139">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="158c3-140">При запуске вашего приложения промежуточный слой OWIN вызовет метод `Configuration(…)` .</span><span class="sxs-lookup"><span data-stu-id="158c3-140">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="158c3-141">Замените объявление класса `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="158c3-141">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="158c3-142">Часть этого класса уже была реализована в другом файле.</span><span class="sxs-lookup"><span data-stu-id="158c3-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="158c3-143">В методе `Configuration(…)` отправьте вызов в `ConfgureAuth(…)`, чтобы настроить аутентификацию для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="158c3-143">In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="158c3-144">Откройте файл `App_Start\Startup.Auth.cs` и реализуйте метод `ConfigureAuth(…)`.</span><span class="sxs-lookup"><span data-stu-id="158c3-144">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="158c3-145">Параметры, указанные в `WindowsAzureActiveDirectoryBearerAuthenticationOptions`, будут служить координатами приложения для взаимодействия с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="158c3-145">The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. <span data-ttu-id="158c3-146">Теперь можно использовать атрибуты `[Authorize]` для защиты контроллеров и действий с помощью аутентификации носителей JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="158c3-146">Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="158c3-147">Снабдите класс `Controllers\TodoListController.cs` тегом авторизации.</span><span class="sxs-lookup"><span data-stu-id="158c3-147">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="158c3-148">Пользователь будет вынужден войти в систему, прежде чем сможет обратиться к этой странице.</span><span class="sxs-lookup"><span data-stu-id="158c3-148">This will force the user to sign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="158c3-149">Когда авторизованный вызывающий объект успешно вызывает один из интерфейсов API `TodoListController` , может потребоваться доступ к сведениям о вызывающем объекте.</span><span class="sxs-lookup"><span data-stu-id="158c3-149">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span> <span data-ttu-id="158c3-150">OWIN предоставляет доступ к утверждениям внутри маркера защиты посредством объекта `ClaimsPrincpal` .</span><span class="sxs-lookup"><span data-stu-id="158c3-150">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="158c3-151">Общим требованием для веб-API является проверка областей (scope) в токене.</span><span class="sxs-lookup"><span data-stu-id="158c3-151">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="158c3-152">Это гарантирует, что пользователь предоставил разрешения, необходимые для доступа к службе списка дел.</span><span class="sxs-lookup"><span data-stu-id="158c3-152">This ensures that the user has consented to the permissions required to access the To Do List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="158c3-153">Откройте файл `web.config` в корне проекта TodoListService и введите значения конфигурации в разделе `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="158c3-153">Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="158c3-154">`ida:Tenant` — это имя вашего клиента Azure AD, например contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="158c3-154">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="158c3-155">`ida:Audience` — это URI идентификатора приложения, введенное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="158c3-155">`ida:Audience` is the App ID URI of the application that you entered in the Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-the-service"></a><span data-ttu-id="158c3-156">Шаг 3. Настройка клиентского приложения и запуск службы</span><span class="sxs-lookup"><span data-stu-id="158c3-156">Step 3: Configure a client application and run the service</span></span>
<span data-ttu-id="158c3-157">Чтобы увидеть службу списка дел в действии, необходимо настроить клиент списка дел для получения токенов от Azure AD и выполнения вызовов службы.</span><span class="sxs-lookup"><span data-stu-id="158c3-157">Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.</span></span>

1. <span data-ttu-id="158c3-158">Вернитесь на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="158c3-158">Go back to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="158c3-159">Создайте новое приложение в клиенте Azure AD и выберите **Собственное клиентское приложение** в конечном запросе.</span><span class="sxs-lookup"><span data-stu-id="158c3-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.</span></span>
  * <span data-ttu-id="158c3-160">**Имя** приложения является его описанием для пользователей.</span><span class="sxs-lookup"><span data-stu-id="158c3-160">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="158c3-161">В качестве **URI перенаправления** введите значение `http://TodoListClient/`.</span><span class="sxs-lookup"><span data-stu-id="158c3-161">Enter `http://TodoListClient/` for the **Redirect Uri** value.</span></span>

3. <span data-ttu-id="158c3-162">Когда вы завершите регистрацию, Azure AD присвоит приложению уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="158c3-162">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="158c3-163">Это значение вам понадобится для следующих действий, поэтому скопируйте его на странице приложения.</span><span class="sxs-lookup"><span data-stu-id="158c3-163">You’ll need this value in the next steps, so copy it from the application page.</span></span>

4. <span data-ttu-id="158c3-164">На странице **Параметры** выберите **Необходимые разрешения** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="158c3-164">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="158c3-165">Найдите и выберите службу списка дел, добавьте разрешение **Access TodoListService** (Доступ к службе списка дел) в списке **Делегированные разрешения**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="158c3-165">Locate and select the To Do List Service, add the **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="158c3-166">В Visual Studio откройте файл `App.config` в проекте TodoListClient и введите значения конфигурации в раздел `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="158c3-166">In Visual Studio, open `App.config` in the TodoListClient project, and then enter your configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="158c3-167">`ida:Tenant` — это имя вашего клиента Azure AD, например contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="158c3-167">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="158c3-168">`ida:ClientId` — это идентификатор приложения, скопированный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="158c3-168">`ida:ClientId` is the app ID that you copied from the Azure portal.</span></span>
  * <span data-ttu-id="158c3-169">`todo:TodoListResourceId` — это URI идентификатора приложения службы списка дел, введенный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="158c3-169">`todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="158c3-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="158c3-170">Next steps</span></span>
<span data-ttu-id="158c3-171">Наконец, выполните очистку и сборку, а затем запустите каждый из проектов.</span><span class="sxs-lookup"><span data-stu-id="158c3-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="158c3-172">Если вы еще этого не сделали, создайте нового пользователя в своем клиенте с доменом *.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="158c3-172">If you haven’t already, now is the time to create a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="158c3-173">Войдите в клиент списка дел от имени данного пользователя и добавьте несколько задач в его список дел.</span><span class="sxs-lookup"><span data-stu-id="158c3-173">Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.</span></span>

<span data-ttu-id="158c3-174">Готовый пример (для которого лишь осталось задать конфигурацию) можно найти в [репозитории GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="158c3-174">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="158c3-175">Теперь можно приступить к другим сценариям идентификации.</span><span class="sxs-lookup"><span data-stu-id="158c3-175">You can now move on to more identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
