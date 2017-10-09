---
title: "aaaAzure AD .NET, веб-API Приступая к работе | Документы Microsoft"
description: "Как toobuild веб-API .NET MVC, интегрируется с Azure AD для проверки подлинности и авторизации."
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
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="bc4fe-103">Защита веб-API с помощью токенов носителя из Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc4fe-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="bc4fe-104">При создании приложения, которое предоставляет доступ tooprotected ресурсы, необходимые tooknow как tooprevent несанкционированному доступ к ресурсам toothose.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-104">If you’re building an application that provides access tooprotected resources, you need tooknow how tooprevent unwarranted access toothose resources.</span></span>
<span data-ttu-id="bc4fe-105">Azure Active Directory (Azure AD) позволяет легко и просто toohelp защитить веб-API с помощью маркера доступа OAuth 2.0 носителя с помощью всего нескольких строк кода.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-105">Azure Active Directory (Azure AD) makes it simple and straightforward toohelp protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="bc4fe-106">В веб-приложениях ASP.NET такая защита можно выполнить с помощью реализации Microsoft hello hello сообщество ведет по промежуточного слоя OWIN включены в .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-106">In ASP.NET web apps, you can accomplish this protection by using hello Microsoft implementation of hello community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="bc4fe-107">Здесь мы будем использовать OWIN toobuild «tooDo список» веб-API:</span><span class="sxs-lookup"><span data-stu-id="bc4fe-107">Here we’ll use OWIN toobuild a "tooDo List" web API that:</span></span>

* <span data-ttu-id="bc4fe-108">указывает, какие API защищены;</span><span class="sxs-lookup"><span data-stu-id="bc4fe-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="bc4fe-109">Проверяет, что вызовы веб-API hello содержит действительный маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-109">Validates that hello web API calls contain a valid access token.</span></span>

<span data-ttu-id="bc4fe-110">tooDo hello toobuild список API, сначала необходимо:</span><span class="sxs-lookup"><span data-stu-id="bc4fe-110">toobuild hello tooDo List API, you first need to:</span></span>

1. <span data-ttu-id="bc4fe-111">зарегистрировать приложение в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bc4fe-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="bc4fe-112">Настройка проверки подлинности конвейер OWIN hello hello приложения toouse.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-112">Set up hello app toouse hello OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="bc4fe-113">Настройка клиентского приложения toocall hello веб-API.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-113">Configure a client application toocall hello web API.</span></span>

<span data-ttu-id="bc4fe-114">tooget к работе, [загрузить каркас приложения hello](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) или [загрузить образец hello завершения](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="bc4fe-114">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="bc4fe-115">Каждый из них является решением Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="bc4fe-116">Необходимо также клиент Azure AD, в которой tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-116">You also need an Azure AD tenant in which tooregister your application.</span></span> <span data-ttu-id="bc4fe-117">Если вы их еще нет, [Узнайте, как один tooget](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="bc4fe-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="bc4fe-118">Шаг 1. Регистрация приложения в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc4fe-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="bc4fe-119">toohelp защитить приложение, сначала нужно toocreate приложения в клиенте и предоставить Azure AD несколько основные сведения.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-119">toohelp secure your application, you first need toocreate an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="bc4fe-120">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bc4fe-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="bc4fe-121">На верхней панели hello выберите свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-121">On hello top bar, click your account.</span></span> <span data-ttu-id="bc4fe-122">В hello **каталога** выберите клиента hello Azure AD, где требуется tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-122">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="bc4fe-123">Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-123">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="bc4fe-124">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="bc4fe-125">Следуйте инструкциям hello и создайте новый **веб-приложение или веб-API**.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-125">Follow hello prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="bc4fe-126">**Имя** описывает toousers вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-126">**Name** describes your application toousers.</span></span> <span data-ttu-id="bc4fe-127">Введите **tooDo службы списка**.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-127">Enter **tooDo List Service**.</span></span>
  * <span data-ttu-id="bc4fe-128">**Uri перенаправления** представляет собой комбинацию схему и строки, используемый tooreturn все маркеры, запросил приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-128">**Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn any tokens that your app has requested.</span></span> <span data-ttu-id="bc4fe-129">Укажите `https://localhost:44321/` для этого параметра.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="bc4fe-130">Из hello **параметры** -> **свойства** страницы приложения, обновите URI идентификатора приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="bc4fe-131">Введите идентификатор конкретного клиента.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="bc4fe-132">Например, введите `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="bc4fe-133">Сохранение конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-133">Save hello configuration.</span></span> <span data-ttu-id="bc4fe-134">Не закрывайте портал hello, так как необходимо tooregister клиентского приложения вскоре.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-134">Leave hello portal open, because you'll also need tooregister your client application shortly.</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="bc4fe-135">Шаг 2: Настройка проверки подлинности конвейер OWIN hello hello приложения toouse</span><span class="sxs-lookup"><span data-stu-id="bc4fe-135">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="bc4fe-136">toovalidate входящие запросы и токены, необходимо tooset копирование toocommunicate вашего приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-136">toovalidate incoming requests and tokens, you need tooset up your application toocommunicate with Azure AD.</span></span>

1. <span data-ttu-id="bc4fe-137">toobegin, откройте решение hello и добавьте hello NuGet по промежуточного слоя OWIN пакеты проект TodoListService toohello с помощью консоли диспетчера пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-137">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="bc4fe-138">Добавить проект TodoListService запуска OWIN класса toohello вызывается `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-138">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="bc4fe-139">Щелкните правой кнопкой мыши проект hello, выберите **добавить** > **новый элемент**и выполните поиск **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-139">Right-click hello project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="bc4fe-140">по промежуточного слоя OWIN Hello будет вызывать hello `Configuration(…)` метод при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-140">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="bc4fe-141">Измените объявление класса hello слишком`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-141">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="bc4fe-142">Часть этого класса уже была реализована в другом файле.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="bc4fe-143">В hello `Configuration(…)` метод, вызвать слишком`ConfgureAuth(…)` tooset проверку подлинности для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-143">In hello `Configuration(…)` method, make a call too`ConfgureAuth(…)` tooset up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="bc4fe-144">Привет открыть файл `App_Start\Startup.Auth.cs` и реализовать hello `ConfigureAuth(…)` метод.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-144">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="bc4fe-145">Здравствуйте, параметры, указываемые в `WindowsAzureActiveDirectoryBearerAuthenticationOptions` будет служить в качестве координат для toocommunicate вашего приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-145">hello parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

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

5. <span data-ttu-id="bc4fe-146">Теперь вы можете использовать `[Authorize]` toohelp атрибуты защиты контроллеров и действий с помощью проверки подлинности носителя JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="bc4fe-146">Now you can use `[Authorize]` attributes toohelp protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="bc4fe-147">Украшение hello `Controllers\TodoListController.cs` класса с помощью тега authorize.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-147">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="bc4fe-148">Это заставит toosign пользователя hello в перед получением доступа к этой странице.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-148">This will force hello user toosign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="bc4fe-149">Когда вызывающий объект авторизованным успешно вызывает один hello `TodoListController` API-интерфейсы, действие hello может иметь доступа tooinformation о вызывающем модуле hello.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-149">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span> <span data-ttu-id="bc4fe-150">OWIN предоставляет доступ toohello утверждения в маркер носителя hello через hello `ClaimsPrincpal` объекта.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-150">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="bc4fe-151">Общим требованием для веб-API — hello toovalidate «областей» присутствует в маркере hello.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-151">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="bc4fe-152">Это гарантирует, что этот пользователь hello согласился toohello разрешений требуется tooaccess hello tooDo службы списка.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-152">This ensures that hello user has consented toohello permissions required tooaccess hello tooDo List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="bc4fe-153">Откройте hello `web.config` файл в корне hello проект TodoListService hello и введите значения конфигурации в hello `<appSettings>` раздела.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-153">Open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="bc4fe-154">`ida:Tenant`— имя вашего клиента Azure AD — например, contoso.onmicrosoft.com hello.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-154">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="bc4fe-155">`ida:Audience`hello URI ИД приложения hello, введенного в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-155">`ida:Audience` is hello App ID URI of hello application that you entered in hello Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a><span data-ttu-id="bc4fe-156">Шаг 3: Настройте клиентское приложение и запустить службу hello</span><span class="sxs-lookup"><span data-stu-id="bc4fe-156">Step 3: Configure a client application and run hello service</span></span>
<span data-ttu-id="bc4fe-157">Перед просмотром hello tooDo службы списка в действии, необходимо tooconfigure hello tooDo список клиентов, чтобы можно было получить токены из Azure AD и сделать службу toohello вызовы.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-157">Before you can see hello tooDo List Service in action, you need tooconfigure hello tooDo List client so it can get tokens from Azure AD and make calls toohello service.</span></span>

1. <span data-ttu-id="bc4fe-158">Вернитесь к предыдущему окну toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bc4fe-158">Go back toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="bc4fe-159">Создайте новое приложение в клиенте Azure AD и выберите **собственное клиентское приложение** в результирующей строке hello.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in hello resulting prompt.</span></span>
  * <span data-ttu-id="bc4fe-160">**Имя** описывает toousers вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-160">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="bc4fe-161">Введите `http://TodoListClient/` для hello **Uri перенаправления** значение.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-161">Enter `http://TodoListClient/` for hello **Redirect Uri** value.</span></span>

3. <span data-ttu-id="bc4fe-162">После завершения регистрации Azure AD присваивает значение приложении tooyour приложения уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-162">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="bc4fe-163">Это значение необходимо в следующих шагах hello, поэтому скопируйте его на приложение hello в окне.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-163">You’ll need this value in hello next steps, so copy it from hello application page.</span></span>

4. <span data-ttu-id="bc4fe-164">Из hello **параметры** выберите **требуемые разрешения**, а затем выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-164">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="bc4fe-165">Найдите и выберите tooDo hello список служб, добавьте hello **TodoListService доступа** разрешение в списке **делегированные разрешения**, а затем нажмите кнопку **сделать**.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-165">Locate and select hello tooDo List Service, add hello **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="bc4fe-166">В Visual Studio откройте `App.config` в hello TodoListClient проекта, а затем введите значения конфигурации в hello `<appSettings>` раздела.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-166">In Visual Studio, open `App.config` in hello TodoListClient project, and then enter your configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="bc4fe-167">`ida:Tenant`— имя вашего клиента Azure AD — например, contoso.onmicrosoft.com hello.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-167">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="bc4fe-168">`ida:ClientId`— Идентификатор приложения hello, скопированный из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-168">`ida:ClientId` is hello app ID that you copied from hello Azure portal.</span></span>
  * <span data-ttu-id="bc4fe-169">`todo:TodoListResourceId`— URI идентификатора приложения hello tooDo приложения службы списка, введенное на портал Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-169">`todo:TodoListResourceId` is hello App ID URI of hello tooDo List Service application that you entered in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc4fe-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bc4fe-170">Next steps</span></span>
<span data-ttu-id="bc4fe-171">Наконец, выполните очистку и сборку, а затем запустите каждый из проектов.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="bc4fe-172">Если это еще не сделано, пришло время toocreate hello нового пользователя в клиенте с *. onmicrosoft.com домена.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-172">If you haven’t already, now is hello time toocreate a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="bc4fe-173">Войдите в клиент список tooDo toohello с этим пользователем и добавить список дел toohello пользователей некоторые задачи.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-173">Sign in toohello tooDo List client with that user, and add some tasks toohello user's to-do list.</span></span>

<span data-ttu-id="bc4fe-174">Для ссылки, пример hello завершена (без настройки) доступен в [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="bc4fe-174">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="bc4fe-175">Теперь можно переходить на сценариях toomore удостоверений.</span><span class="sxs-lookup"><span data-stu-id="bc4fe-175">You can now move on toomore identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
