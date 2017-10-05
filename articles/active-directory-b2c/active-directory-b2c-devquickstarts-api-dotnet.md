---
title: "Azure AD B2C | Документация Майкрософт"
description: "Как с помощью Azure Active Directory B2C создать веб-API .NET, защищенный маркерами доступа OAuth 2.0 для проверки подлинности."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 48749bfa2ab54a0e766a4aad4f39073cc4e90818
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="a36a1-103">Azure Active Directory B2C: создание веб-API .NET</span><span class="sxs-lookup"><span data-stu-id="a36a1-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="a36a1-104">С помощью Azure Active Directory (Azure AD) B2C можно защитить веб-API с помощью маркера доступа OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a36a1-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="a36a1-105">Эти маркеры позволяют клиентским приложениям проходить проверку подлинности для API.</span><span class="sxs-lookup"><span data-stu-id="a36a1-105">These tokens allow your client apps to authenticate to the API.</span></span> <span data-ttu-id="a36a1-106">В этой статье показано, как создать интерфейс веб-API .NET "Список дел" с использованием модели Model-View-Controller (MVC), который позволяет пользователям клиентского приложения выполнять задачи CRUD.</span><span class="sxs-lookup"><span data-stu-id="a36a1-106">This article shows you how to create a .NET MVC "to-do list" API that allows users of your client application to CRUD tasks.</span></span> <span data-ttu-id="a36a1-107">Этот веб-API защищен с помощью Azure AD B2C. Управлять списком дел могут только пользователи, прошедшие проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="a36a1-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="a36a1-108">Создание каталога Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a36a1-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="a36a1-109">Перед использованием Azure AD B2C необходимо создать каталог или клиент.</span><span class="sxs-lookup"><span data-stu-id="a36a1-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="a36a1-110">Каталог — это контейнер для данных всех ваших пользователей, приложений, групп и т. д.</span><span class="sxs-lookup"><span data-stu-id="a36a1-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="a36a1-111">Прежде чем продолжать работу с руководством, [создайте каталог B2C](active-directory-b2c-get-started.md), если вы его еще не создали.</span><span class="sxs-lookup"><span data-stu-id="a36a1-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="a36a1-112">Клиентское приложение и веб-API должны использовать один и тот же каталог Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a36a1-112">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="a36a1-113">Создание веб-API</span><span class="sxs-lookup"><span data-stu-id="a36a1-113">Create a web API</span></span>

<span data-ttu-id="a36a1-114">Теперь необходимо создать приложение веб-API в каталоге B2C.</span><span class="sxs-lookup"><span data-stu-id="a36a1-114">Next, you need to create a web API app in your B2C directory.</span></span> <span data-ttu-id="a36a1-115">Это дает Azure AD информацию, необходимую для безопасного взаимодействия с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="a36a1-115">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="a36a1-116">Чтобы создать приложение, следуйте [этим инструкциям](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a36a1-116">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="a36a1-117">Не забудьте сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="a36a1-117">Be sure to:</span></span>

* <span data-ttu-id="a36a1-118">Включите в приложение **веб-приложение** или **веб-API**.</span><span class="sxs-lookup"><span data-stu-id="a36a1-118">Include a **web app** or **web API** in the application.</span></span>
* <span data-ttu-id="a36a1-119">Используйте **URI перенаправления** `https://localhost:44332/` для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a36a1-119">Use the **Redirect URI** `https://localhost:44332/` for the web app.</span></span> <span data-ttu-id="a36a1-120">Это стандартное расположение клиента веб-приложения для этого примера.</span><span class="sxs-lookup"><span data-stu-id="a36a1-120">This is the default location of the web app client for this code sample.</span></span>
* <span data-ttu-id="a36a1-121">Скопируйте **идентификатор приложения** , назначенный приложению.</span><span class="sxs-lookup"><span data-stu-id="a36a1-121">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="a36a1-122">Он понадобится вам позднее.</span><span class="sxs-lookup"><span data-stu-id="a36a1-122">You'll need it later.</span></span>
* <span data-ttu-id="a36a1-123">Введите идентификатор приложения в поле **URI кода приложения**.</span><span class="sxs-lookup"><span data-stu-id="a36a1-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="a36a1-124">Добавьте разрешения с помощью меню **Published scopes** (Опубликованные области).</span><span class="sxs-lookup"><span data-stu-id="a36a1-124">Add permissions through the **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="a36a1-125">Создание политик</span><span class="sxs-lookup"><span data-stu-id="a36a1-125">Create your policies</span></span>

<span data-ttu-id="a36a1-126">В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="a36a1-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="a36a1-127">Вам понадобится создать политику для взаимодействия с Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a36a1-127">You will need to create a policy to communicate with Azure AD B2C.</span></span> <span data-ttu-id="a36a1-128">Мы советуем использовать объединенную политику регистрации и входа, как описано в статье [Azure Active Directory B2C: расширяемая инфраструктура политик](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="a36a1-128">We recommend using the combined sign-up/sign-in policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="a36a1-129">При создании политики обязательно сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a36a1-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="a36a1-130">В политике укажите **отображаемое имя** и другие атрибуты регистрации.</span><span class="sxs-lookup"><span data-stu-id="a36a1-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="a36a1-131">В каждой политике в качестве утверждения приложения выберите утверждения **Отображаемое имя** и **Идентификатор объекта**.</span><span class="sxs-lookup"><span data-stu-id="a36a1-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="a36a1-132">Можно также выбрать другие утверждения.</span><span class="sxs-lookup"><span data-stu-id="a36a1-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="a36a1-133">Скопируйте **имя** каждой созданной политики.</span><span class="sxs-lookup"><span data-stu-id="a36a1-133">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="a36a1-134">Эти имена политик понадобятся вам позже.</span><span class="sxs-lookup"><span data-stu-id="a36a1-134">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="a36a1-135">Создав политику, можно приступать к созданию приложения.</span><span class="sxs-lookup"><span data-stu-id="a36a1-135">After you have successfully created the policy, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="a36a1-136">Загрузка кода</span><span class="sxs-lookup"><span data-stu-id="a36a1-136">Download the code</span></span>

<span data-ttu-id="a36a1-137">Код примеров для этого руководства размещен на портале [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="a36a1-137">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="a36a1-138">Вы можете клонировать пример, выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="a36a1-138">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="a36a1-139">Скачав пример кода, откройте SLN-файл Visual Studio, чтобы начать работу.</span><span class="sxs-lookup"><span data-stu-id="a36a1-139">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="a36a1-140">Теперь решение содержит два проекта: `TaskWebApp` и `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="a36a1-140">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="a36a1-141">`TaskWebApp` — это веб-приложение MVC, с которым взаимодействует пользователь.</span><span class="sxs-lookup"><span data-stu-id="a36a1-141">`TaskWebApp` is an MVC web application that the user interacts with.</span></span> <span data-ttu-id="a36a1-142">`TaskService` — веб-API серверной части приложения, в котором хранится список дел для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="a36a1-142">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="a36a1-143">В этой статье рассматривается только приложение `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="a36a1-143">This article will only discuss the `TaskService` application.</span></span> <span data-ttu-id="a36a1-144">Сведения о создании `TaskWebApp` с помощью Azure AD B2C см. в [этом руководстве по веб-приложениям .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="a36a1-144">To learn how to build `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="a36a1-145">Обновление конфигурации Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a36a1-145">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="a36a1-146">В нашем примере настроено использование политик и идентификатора клиента демонстрационного клиента.</span><span class="sxs-lookup"><span data-stu-id="a36a1-146">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="a36a1-147">Если вы хотите использовать собственный клиент, необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="a36a1-147">If you would like to use your own tenant, you will need to do the following:</span></span>

1. <span data-ttu-id="a36a1-148">Откройте `web.config` в проекте `TaskService` и замените следующие значения:</span><span class="sxs-lookup"><span data-stu-id="a36a1-148">Open `web.config` in the `TaskService` project and replace the values for</span></span>
    * <span data-ttu-id="a36a1-149">`ida:Tenant` именем своего клиента;</span><span class="sxs-lookup"><span data-stu-id="a36a1-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="a36a1-150">`ida:ClientId` идентификатором клиента для приложения веб-API;</span><span class="sxs-lookup"><span data-stu-id="a36a1-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="a36a1-151">`ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему.</span><span class="sxs-lookup"><span data-stu-id="a36a1-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="a36a1-152">Откройте `web.config` в проекте `TaskWebApp` и замените следующие значения:</span><span class="sxs-lookup"><span data-stu-id="a36a1-152">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>
    * <span data-ttu-id="a36a1-153">`ida:Tenant` именем своего клиента;</span><span class="sxs-lookup"><span data-stu-id="a36a1-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="a36a1-154">`ida:ClientId` идентификатором клиента для веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="a36a1-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="a36a1-155">`ida:ClientSecret` секретным ключом веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="a36a1-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="a36a1-156">`ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему;</span><span class="sxs-lookup"><span data-stu-id="a36a1-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="a36a1-157">`ida:EditProfilePolicyId` именем политики "Изменение профиля";</span><span class="sxs-lookup"><span data-stu-id="a36a1-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="a36a1-158">`ida:ResetPasswordPolicyId` именем политики "Сброс профиля".</span><span class="sxs-lookup"><span data-stu-id="a36a1-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-the-api"></a><span data-ttu-id="a36a1-159">Защита API</span><span class="sxs-lookup"><span data-stu-id="a36a1-159">Secure the API</span></span>

<span data-ttu-id="a36a1-160">Теперь, когда у вас есть клиент, который вызывает API, можно защитить API (например, `TaskService`) с помощью токенов носителя OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="a36a1-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="a36a1-161">Это гарантирует, что каждый запрос к API будет действителен, только если содержит токен носителя.</span><span class="sxs-lookup"><span data-stu-id="a36a1-161">This ensures that each request to your API will only be valid if the request has a bearer token.</span></span> <span data-ttu-id="a36a1-162">API может принимать и проверять токены носителя с помощью библиотеки OWIN от Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="a36a1-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="a36a1-163">Установка OWIN</span><span class="sxs-lookup"><span data-stu-id="a36a1-163">Install OWIN</span></span>

<span data-ttu-id="a36a1-164">Начните с установки конвейера проверки подлинности OWIN OAuth с помощью консоли диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a36a1-164">Begin by installing the OWIN OAuth authentication pipeline by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="a36a1-165">Будет выполнена установка ПО промежуточного слоя OWIN, которое будет принимать и проверять токены носителя.</span><span class="sxs-lookup"><span data-stu-id="a36a1-165">This will install the OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="a36a1-166">Добавление класса запуска OWIN</span><span class="sxs-lookup"><span data-stu-id="a36a1-166">Add an OWIN startup class</span></span>

<span data-ttu-id="a36a1-167">Добавьте класс запуска OWIN в API с именем `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="a36a1-167">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="a36a1-168">Щелкните проект правой кнопкой мыши и выберите **Добавить** и **Новый элемент**, после чего найдите OWIN.</span><span class="sxs-lookup"><span data-stu-id="a36a1-168">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="a36a1-169">При запуске вашего приложения промежуточный слой OWIN вызовет метод `Configuration(…)` .</span><span class="sxs-lookup"><span data-stu-id="a36a1-169">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="a36a1-170">В нашем примере мы изменили объявление класса на `public partial class Startup` и реализовали другую часть класса в `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="a36a1-170">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="a36a1-171">Внутри метода `Configuration` мы добавили вызов `ConfigureAuth`, определенный в `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="a36a1-171">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="a36a1-172">После внесения изменений `Startup.cs` выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a36a1-172">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="a36a1-173">Настройка проверки подлинности OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="a36a1-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="a36a1-174">Откройте файл `App_Start\Startup.Auth.cs` и реализуйте метод `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="a36a1-174">Open the file `App_Start\Startup.Auth.cs`, and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="a36a1-175">Это может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a36a1-175">For example, it could look like the following:</span></span>

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure the authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where the audience of the token is equal to the client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches the Azure AD B2C metadata & signing keys from the OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-the-task-controller"></a><span data-ttu-id="a36a1-176">Настройка защиты контроллера задач</span><span class="sxs-lookup"><span data-stu-id="a36a1-176">Secure the task controller</span></span>

<span data-ttu-id="a36a1-177">Теперь, когда приложение настроено для использования проверки подлинности OAuth 2.0, вы можете добавить тег `[Authorize]` к контроллеру задач для защиты веб-API.</span><span class="sxs-lookup"><span data-stu-id="a36a1-177">After the app is configured to use OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag to the task controller.</span></span> <span data-ttu-id="a36a1-178">В этом контроллере выполняются все операции со списками дел, поэтому нужно защитить весь контроллер на уровне класса.</span><span class="sxs-lookup"><span data-stu-id="a36a1-178">This is the controller where all to-do list manipulation takes place, so you should secure the entire controller at the class level.</span></span> <span data-ttu-id="a36a1-179">Для более точного управления можно добавить тег `[Authorize]` к отдельным действиям.</span><span class="sxs-lookup"><span data-stu-id="a36a1-179">You can also add the `[Authorize]` tag to individual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-the-token"></a><span data-ttu-id="a36a1-180">Получение сведений о пользователе из токена.</span><span class="sxs-lookup"><span data-stu-id="a36a1-180">Get user information from the token</span></span>

<span data-ttu-id="a36a1-181">`TasksController` сохраняет задачи в базе данных, где каждой задаче соответствует пользователь, являющийся ее владельцем.</span><span class="sxs-lookup"><span data-stu-id="a36a1-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" the task.</span></span> <span data-ttu-id="a36a1-182">Владелец определяется **идентификатором объекта**пользователя.</span><span class="sxs-lookup"><span data-stu-id="a36a1-182">The owner is identified by the user's **object ID**.</span></span> <span data-ttu-id="a36a1-183">(Поэтому необходимо добавить идентификатор объекта в качестве утверждения приложения во все свои политики.)</span><span class="sxs-lookup"><span data-stu-id="a36a1-183">(This is why you needed to add the object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-the-permissions-in-the-token"></a><span data-ttu-id="a36a1-184">Проверка разрешений в токене</span><span class="sxs-lookup"><span data-stu-id="a36a1-184">Validate the permissions in the token</span></span>

<span data-ttu-id="a36a1-185">Общим требованием для веб-API является проверка областей (scope) в токене.</span><span class="sxs-lookup"><span data-stu-id="a36a1-185">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="a36a1-186">Это гарантирует, что пользователь предоставил разрешения, необходимые для доступа к службе списка дел.</span><span class="sxs-lookup"><span data-stu-id="a36a1-186">This ensures that the user has consented to the permissions required to access the to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "The Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="a36a1-187">Запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="a36a1-187">Run the sample app</span></span>

<span data-ttu-id="a36a1-188">Наконец, выполните сборку и запустите `TaskWebApp` и `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="a36a1-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="a36a1-189">Создайте несколько задач в списке дел. Обратите внимание, что они сохраняются в API даже после остановки и перезапуска клиента.</span><span class="sxs-lookup"><span data-stu-id="a36a1-189">Create some tasks on the user's to-do list and notice how they are persisted in the API even after you stop and restart the client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="a36a1-190">Изменение политик</span><span class="sxs-lookup"><span data-stu-id="a36a1-190">Edit your policies</span></span>

<span data-ttu-id="a36a1-191">Теперь, когда у вас есть API, защищенный с помощью Azure AD B2C, можно поэкспериментировать с политиками регистрации и входа и понаблюдать, как это влияет (или не влияет) на API.</span><span class="sxs-lookup"><span data-stu-id="a36a1-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view the effects (or lack thereof) on the API.</span></span> <span data-ttu-id="a36a1-192">Вы можете управлять утверждениями приложения в политиках и изменять сведения о пользователе, доступные в веб-API.</span><span class="sxs-lookup"><span data-stu-id="a36a1-192">You can manipulate the application claims in the policies and change the user information that is available in the web API.</span></span> <span data-ttu-id="a36a1-193">Любые дополнительные утверждения, которые вы добавляете, будут доступны для веб-API .NET MVC в объекте `ClaimsPrincipal` , как описано ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a36a1-193">Any claims that you add will be available to your .NET MVC web API in the `ClaimsPrincipal` object, as described earlier in this article.</span></span>
