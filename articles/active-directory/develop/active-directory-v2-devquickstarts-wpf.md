---
title: "Собственное приложение .NET версии 2.0 для Azure Active Directory | Документация Майкрософт"
description: "Как создать собственное приложение .NET, которое поддерживает вход пользователей с помощью личной учетной записи Майкрософт, а также рабочей или учебной учетных записей."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 7389f55ee6fef9548abb0ca4ac1bbd0399868d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-windows-desktop-app"></a><span data-ttu-id="27802-103">Добавление функции входа в классическое приложение для Windows</span><span class="sxs-lookup"><span data-stu-id="27802-103">Add sign-in to a Windows Desktop app</span></span>
<span data-ttu-id="27802-104">Точка доступа версии 2.0 позволяет быстро реализовать в классических приложениях аутентификацию с поддержкой личных учетных записей Майкрософт, а также рабочих или учебных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="27802-104">With the the v2.0 endpoint, you can quickly add authentication to your desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="27802-105">Она также позволяет приложению безопасно обмениваться данными с серверным веб-API, а также [Microsoft Graph](https://graph.microsoft.io) и несколькими [унифицированными API Office 365](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="27802-105">It also enables your app to securely communicate with a backend web api, as well as [the Microsoft Graph](https://graph.microsoft.io) and a few of the [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="27802-106">Не все сценарии и компоненты Azure Active Directory (AD) поддерживаются конечной точкой версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="27802-106">Not all Azure Active Directory (AD) scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="27802-107">Чтобы определить, следует ли вам использовать конечную точку версии 2.0, ознакомьтесь с [ограничениями версии 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="27802-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="27802-108">Для [собственных приложений .NET, запущенных на устройстве](active-directory-v2-flows.md#mobile-and-native-apps), в Azure AD предлагается использовать библиотеку проверки подлинности Майкрософт (MSAL).</span><span class="sxs-lookup"><span data-stu-id="27802-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides the Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="27802-109">MSAL помогает приложению быстро получать маркеры доступа и вызывать веб-службы.</span><span class="sxs-lookup"><span data-stu-id="27802-109">MSAL's sole purpose in life is to make it easy for your app to get tokens for calling web services.</span></span>  <span data-ttu-id="27802-110">Чтобы показать, насколько это просто, создадим приложение To Do List (ведение списка дел) для .NET WPF, которое:</span><span class="sxs-lookup"><span data-stu-id="27802-110">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="27802-111">выполняет вход пользователя и получает маркеры доступа с помощью [протокола проверки подлинности OAuth 2.0](active-directory-v2-protocols.md);</span><span class="sxs-lookup"><span data-stu-id="27802-111">Signs the user in & gets access tokens using the [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="27802-112">безопасно вызывает серверную веб-службу списка дел, которая также защищена OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="27802-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="27802-113">обеспечивает выход пользователя из приложения.</span><span class="sxs-lookup"><span data-stu-id="27802-113">Signs the user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="27802-114">Скачивание примера кода</span><span class="sxs-lookup"><span data-stu-id="27802-114">Download sample code</span></span>
<span data-ttu-id="27802-115">Код в этом учебнике размещен на портале [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="27802-115">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="27802-116">Для понимания процесса можно [скачать основу приложения как ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) или клонировать ее:</span><span class="sxs-lookup"><span data-stu-id="27802-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="27802-117">Готовое приложение также приводится в конце этого руководства.</span><span class="sxs-lookup"><span data-stu-id="27802-117">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="27802-118">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="27802-118">Register an app</span></span>
<span data-ttu-id="27802-119">Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="27802-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="27802-120">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="27802-120">Make sure to:</span></span>

* <span data-ttu-id="27802-121">Запишите назначенный вашему приложению **идентификатор приложения**. Он вскоре вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="27802-121">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="27802-122">Добавьте для приложения **мобильную** платформу.</span><span class="sxs-lookup"><span data-stu-id="27802-122">Add the **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="27802-123">Установка и настройка MSAL</span><span class="sxs-lookup"><span data-stu-id="27802-123">Install & Configure MSAL</span></span>
<span data-ttu-id="27802-124">Ваше приложение зарегистрировано в Майкрософт. Теперь вы можете установить MSAL и написать собственный код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="27802-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="27802-125">Чтобы библиотека MSAL могла обмениваться информацией с конечной точкой версии 2.0, вам нужно предоставить определенную информацию о регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="27802-125">In order for MSAL to be able to communicate the v2.0 endpoint, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="27802-126">Сначала добавьте MSAL в проект TodoListClient с помощью консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="27802-126">Begin by adding MSAL to the TodoListClient project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="27802-127">В проекте TodoListClient откройте `app.config`.</span><span class="sxs-lookup"><span data-stu-id="27802-127">In the TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="27802-128">Замените значения элементов в разделе `<appSettings>` на значения, введенные на портале регистрации приложений.</span><span class="sxs-lookup"><span data-stu-id="27802-128">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the app registration portal.</span></span>  <span data-ttu-id="27802-129">Код будет использовать эти значения при каждом обращении к библиотеке MSAL.</span><span class="sxs-lookup"><span data-stu-id="27802-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="27802-130">`ida:ClientId` — это **идентификатор приложения** , скопированный с портала.</span><span class="sxs-lookup"><span data-stu-id="27802-130">The `ida:ClientId` is the **Application Id** of your app you copied from the portal.</span></span>
* <span data-ttu-id="27802-131">В проекте TodoList-Service откройте `web.config` в корневой папке проекта.</span><span class="sxs-lookup"><span data-stu-id="27802-131">In the TodoList-Service project, open `web.config` in the root of the project.</span></span>  
  
  * <span data-ttu-id="27802-132">Замените значение `ida:Audience` на **идентификатор приложения** с портала.</span><span class="sxs-lookup"><span data-stu-id="27802-132">Replace the `ida:Audience` value with the same **Application Id** from the portal.</span></span>

## <a name="use-msal-to-get-tokens"></a><span data-ttu-id="27802-133">Использование MSAL для получения маркеров</span><span class="sxs-lookup"><span data-stu-id="27802-133">Use MSAL to get tokens</span></span>
<span data-ttu-id="27802-134">MSAL используется следующим образом. Каждый раз, когда приложению требуется маркер доступа, оно будет просто вызывать `app.AcquireToken(...)`, а MSAL сделает все остальное.</span><span class="sxs-lookup"><span data-stu-id="27802-134">The basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does the rest.</span></span>  

* <span data-ttu-id="27802-135">В проекте `TodoListClient` откройте `MainWindow.xaml.cs` и найдите метод `OnInitialized(...)`.</span><span class="sxs-lookup"><span data-stu-id="27802-135">In the `TodoListClient` project, open `MainWindow.xaml.cs` and locate the `OnInitialized(...)` method.</span></span>  <span data-ttu-id="27802-136">Первый шаг — инициализация в приложении `PublicClientApplication` , основного класса MSAL, представляющего собственные приложения.</span><span class="sxs-lookup"><span data-stu-id="27802-136">The first step is to initialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="27802-137">На этом этапе вы отправляете в MSAL координаты, необходимые для взаимодействия с Azure AD, а также сообщаете о способе кэширования маркеров.</span><span class="sxs-lookup"><span data-stu-id="27802-137">This is where you pass MSAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="27802-138">После запуска приложения необходимо проверить, выполнил ли пользователь вход в приложение.</span><span class="sxs-lookup"><span data-stu-id="27802-138">When the app starts up, we want to check and see if the user is already signed into the app.</span></span>  <span data-ttu-id="27802-139">Однако пока нет необходимости вызывать пользовательский интерфейс входа: пользователь должен нажать кнопку "Вход".</span><span class="sxs-lookup"><span data-stu-id="27802-139">However, we don't want to invoke a sign-in UI just yet - we'll make the user click "Sign In" to do so.</span></span>  <span data-ttu-id="27802-140">Также в методе `OnInitialized(...)` :</span><span class="sxs-lookup"><span data-stu-id="27802-140">Also in the `OnInitialized(...)` method:</span></span>

```C#
// As the app starts, we want to check to see if the user is already signed in.
// You can do so by trying to get a token from MSAL, using the method
// AcquireTokenSilent.  This forces MSAL to throw an exception if it cannot
// get a token for the user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in the cache - or MSAL was able to get a new oen via refresh token.
    // Proceed to fetch the user's tasks from the TodoListService via the GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, the app should take no action,
        // and simply show the user the sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* <span data-ttu-id="27802-141">Если пользователь не выполнил вход и нажал кнопку "Вход", необходимо вызвать пользовательский интерфейс входа и запросить ввод учетных данных.</span><span class="sxs-lookup"><span data-stu-id="27802-141">If the user is not signed in and they click the "Sign In" button, we want to invoke a login UI and have the user enter their credentials.</span></span>  <span data-ttu-id="27802-142">Реализуйте обработчик кнопки "Вход".</span><span class="sxs-lookup"><span data-stu-id="27802-142">Implement the Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign the user out if they clicked the "Clear Cache" button

// If the user clicked the 'Sign-In' button, force
// MSAL to prompt the user for credentials by using
// AcquireTokenAsync, a method that is guaranteed to show a prompt to the user.
// MSAL will get a token for the TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If the user canceled the login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by the user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* <span data-ttu-id="27802-143">Если пользователь успешно выполняет вход, MSAL получает и кэширует маркер, а вы можете вызвать метод `GetTodoList()` .</span><span class="sxs-lookup"><span data-stu-id="27802-143">If the user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed to call the `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="27802-144">Осталось получить задачи пользователя — реализовать метод `GetTodoList()` .</span><span class="sxs-lookup"><span data-stu-id="27802-144">All that's left to get a user's tasks is to implement the `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try to get an access token to call the TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL to throw an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show the user a message
    // and let them click the Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once the token has been returned by MSAL,
// add it to the http authorization header,
// before making the call to access the To Do list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When the user is done managing their To-Do List, they may finally sign out of the app by clicking the "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If the user clicked the 'clear cache' button,
        // clear the MSAL token cache and show the user as signed out.
        // It's also necessary to clear the cookies from the browser
        // control so the next user has a chance to sign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a><span data-ttu-id="27802-145">Выполнить</span><span class="sxs-lookup"><span data-stu-id="27802-145">Run</span></span>
<span data-ttu-id="27802-146">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="27802-146">Congratulations!</span></span> <span data-ttu-id="27802-147">Теперь у вас есть работающее приложение .NET WPF, которое может проверять подлинность пользователей и выполнять безопасные вызовы веб-API при помощи OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="27802-147">You now have a working .NET WPF app that has the ability to authenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="27802-148">Запустите оба проекта и выполните вход с личной учетной записью Майкрософт, рабочей или учебной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="27802-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="27802-149">Добавьте задачи в список дел этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="27802-149">Add tasks to that user's To-Do list.</span></span>  <span data-ttu-id="27802-150">Выйдите из системы и выполните вход от имени других пользователей, чтобы просмотреть их списки дел.</span><span class="sxs-lookup"><span data-stu-id="27802-150">Sign out, and sign back in as another user to view their To-Do list.</span></span>  <span data-ttu-id="27802-151">Закройте приложение и снова его запустите.</span><span class="sxs-lookup"><span data-stu-id="27802-151">Close the app, and re-run it.</span></span>  <span data-ttu-id="27802-152">Обратите внимание, что сеанс пользователя при этом не прерывается, так как приложение кэширует маркеры в локальный файл.</span><span class="sxs-lookup"><span data-stu-id="27802-152">Notice how the user's session remains intact - that is because the app caches tokens in a local file.</span></span>

<span data-ttu-id="27802-153">MSAL позволяет легко включать в приложение общие функции идентификации, позволяя использовать личные и рабочие учетные записи.</span><span class="sxs-lookup"><span data-stu-id="27802-153">MSAL makes it easy to incorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="27802-154">Он отвечает за всю грязную работу: управление кэшем, поддержку протокола OAuth, предоставление пользователю пользовательского интерфейса для входа, обновление истекших маркеров и многое другое.</span><span class="sxs-lookup"><span data-stu-id="27802-154">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="27802-155">Все, что вам действительно нужно знать, — это вызов интерфейса API `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="27802-155">All you really need to know is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="27802-156">Готовый пример (без ваших значений конфигурации) [можно скачать в виде ZIP-файла здесь](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip)или клонировать с портала GitHub.</span><span class="sxs-lookup"><span data-stu-id="27802-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="27802-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="27802-157">Next steps</span></span>
<span data-ttu-id="27802-158">Теперь можно перейти к более сложным темам.</span><span class="sxs-lookup"><span data-stu-id="27802-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="27802-159">Можно попробовать:</span><span class="sxs-lookup"><span data-stu-id="27802-159">You may want to try:</span></span>

* [<span data-ttu-id="27802-160">Защита веб-API TodoListService с помощью конечной точки версии 2.0</span><span class="sxs-lookup"><span data-stu-id="27802-160">Securing the TodoListService Web API with the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="27802-161">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="27802-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="27802-162">Руководство разработчика версии 2.0 >></span><span class="sxs-lookup"><span data-stu-id="27802-162">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="27802-163">Тег "msal" на StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="27802-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="27802-164">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="27802-164">Get security updates for our products</span></span>
<span data-ttu-id="27802-165">Рекомендуем вам настроить уведомления о нарушениях безопасности. Это можно сделать, подписавшись на уведомления безопасности консультационных служб на [этой странице](https://technet.microsoft.com/security/dd252948).</span><span class="sxs-lookup"><span data-stu-id="27802-165">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

