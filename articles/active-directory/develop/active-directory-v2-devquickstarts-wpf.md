---
title: "Active Directory aaaAzure v2.0 собственное приложение .NET | Документы Microsoft"
description: "Как toobuild собственное приложение .NET, подписывает пользователей обоих личную учетную запись Майкрософт и рабочих учетных записей."
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
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a><span data-ttu-id="3af06-103">Добавить tooa входа в приложение рабочего стола Windows</span><span class="sxs-lookup"><span data-stu-id="3af06-103">Add sign-in tooa Windows Desktop app</span></span>
<span data-ttu-id="3af06-104">С конечной точкой v2.0 hello hello можно быстро добавлять проверки подлинности tooyour классических приложений с помощью поддержки для обоих личные учетные записи Майкрософт и рабочих учетных записей.</span><span class="sxs-lookup"><span data-stu-id="3af06-104">With hello hello v2.0 endpoint, you can quickly add authentication tooyour desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="3af06-105">Он также позволяет взаимодействовать toosecurely вашего приложения с серверной части веб-api, а также [hello Microsoft Graph](https://graph.microsoft.io) и несколько hello [API-интерфейсы Office 365 единой](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="3af06-105">It also enables your app toosecurely communicate with a backend web api, as well as [hello Microsoft Graph](https://graph.microsoft.io) and a few of hello [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="3af06-106">Не все сценарии Azure Active Directory (AD) и функции поддерживаются hello v2.0 конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="3af06-106">Not all Azure Active Directory (AD) scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="3af06-107">toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="3af06-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="3af06-108">Для [.NET собственных приложений на устройстве](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD предоставляет hello библиотеки проверки подлинности удостоверений Microsoft или MSAL.</span><span class="sxs-lookup"><span data-stu-id="3af06-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides hello Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="3af06-109">Единственной целью MSAL элемента в жизни является toomake легким для вашего приложения tooget токены для вызова веб-служб.</span><span class="sxs-lookup"><span data-stu-id="3af06-109">MSAL's sole purpose in life is toomake it easy for your app tooget tokens for calling web services.</span></span>  <span data-ttu-id="3af06-110">toodemonstrate, насколько просто здесь мы создадим приложение .NET WPF задача список:</span><span class="sxs-lookup"><span data-stu-id="3af06-110">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="3af06-111">Подписывает hello пользователя в & получает доступ к маркеры с помощью hello [протокол проверки подлинности OAuth 2.0](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="3af06-111">Signs hello user in & gets access tokens using hello [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="3af06-112">безопасно вызывает серверную веб-службу списка дел, которая также защищена OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3af06-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="3af06-113">Подписывает hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="3af06-113">Signs hello user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="3af06-114">Скачивание примера кода</span><span class="sxs-lookup"><span data-stu-id="3af06-114">Download sample code</span></span>
<span data-ttu-id="3af06-115">поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="3af06-115">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="3af06-116">можно toofollow вдоль [загрузить приложение hello основу как .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) или основу hello клона:</span><span class="sxs-lookup"><span data-stu-id="3af06-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="3af06-117">в конце hello в учебнике также предоставляется приложение Hello завершена.</span><span class="sxs-lookup"><span data-stu-id="3af06-117">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="3af06-118">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="3af06-118">Register an app</span></span>
<span data-ttu-id="3af06-119">Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="3af06-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="3af06-120">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="3af06-120">Make sure to:</span></span>

* <span data-ttu-id="3af06-121">Копировать вниз hello **идентификатор приложения** назначены tooyour приложения, оно понадобится скоро.</span><span class="sxs-lookup"><span data-stu-id="3af06-121">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="3af06-122">Добавить hello **Mobile** платформы для приложения.</span><span class="sxs-lookup"><span data-stu-id="3af06-122">Add hello **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="3af06-123">Установка и настройка MSAL</span><span class="sxs-lookup"><span data-stu-id="3af06-123">Install & Configure MSAL</span></span>
<span data-ttu-id="3af06-124">Ваше приложение зарегистрировано в Майкрософт. Теперь вы можете установить MSAL и написать собственный код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="3af06-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="3af06-125">Чтобы MSAL toobe может toocommunicate hello v2.0 конечной точки, необходимо tooprovide его с некоторые сведения о регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="3af06-125">In order for MSAL toobe able toocommunicate hello v2.0 endpoint, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="3af06-126">Начните с добавления MSAL toohello TodoListClient проекта с помощью консоли диспетчера пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="3af06-126">Begin by adding MSAL toohello TodoListClient project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="3af06-127">В проекте TodoListClient hello откройте `app.config`.</span><span class="sxs-lookup"><span data-stu-id="3af06-127">In hello TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="3af06-128">Замените значения hello элементов hello в hello `<appSettings>` раздел tooreflect hello значения входных данных в портал регистрации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3af06-128">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello app registration portal.</span></span>  <span data-ttu-id="3af06-129">Код будет использовать эти значения при каждом обращении к библиотеке MSAL.</span><span class="sxs-lookup"><span data-stu-id="3af06-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="3af06-130">Hello `ida:ClientId` — hello **идентификатор приложения** приложения скопирован с портала hello.</span><span class="sxs-lookup"><span data-stu-id="3af06-130">hello `ida:ClientId` is hello **Application Id** of your app you copied from hello portal.</span></span>
* <span data-ttu-id="3af06-131">В проекте hello TodoList службы откройте `web.config` в корневом каталоге hello hello проекта.</span><span class="sxs-lookup"><span data-stu-id="3af06-131">In hello TodoList-Service project, open `web.config` in hello root of hello project.</span></span>  
  
  * <span data-ttu-id="3af06-132">Замените hello `ida:Audience` значение с hello же **идентификатор приложения** из портала hello.</span><span class="sxs-lookup"><span data-stu-id="3af06-132">Replace hello `ida:Audience` value with hello same **Application Id** from hello portal.</span></span>

## <a name="use-msal-tooget-tokens"></a><span data-ttu-id="3af06-133">Использование маркеров tooget MSAL</span><span class="sxs-lookup"><span data-stu-id="3af06-133">Use MSAL tooget tokens</span></span>
<span data-ttu-id="3af06-134">Hello базовый принцип MSAL — всякий раз, когда ваше приложение должно маркер доступа, просто вызвать метод `app.AcquireToken(...)`, и MSAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="3af06-134">hello basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does hello rest.</span></span>  

* <span data-ttu-id="3af06-135">В hello `TodoListClient` откройте проект `MainWindow.xaml.cs` и найдите hello `OnInitialized(...)` метод.</span><span class="sxs-lookup"><span data-stu-id="3af06-135">In hello `TodoListClient` project, open `MainWindow.xaml.cs` and locate hello `OnInitialized(...)` method.</span></span>  <span data-ttu-id="3af06-136">Hello первым шагом является tooinitialize приложения `PublicClientApplication` -MSAL в основной класс, представляющий приложений в машинном коде.</span><span class="sxs-lookup"><span data-stu-id="3af06-136">hello first step is tooinitialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="3af06-137">Это происходит, где передается MSAL hello координаты, он должен toocommunicate с Azure AD и о том, как toocache маркеры.</span><span class="sxs-lookup"><span data-stu-id="3af06-137">This is where you pass MSAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="3af06-138">При запуске приложение hello, мы должны toocheck и см. Если hello пользователь уже выполнил вход в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="3af06-138">When hello app starts up, we want toocheck and see if hello user is already signed into hello app.</span></span>  <span data-ttu-id="3af06-139">Тем не менее мы не хотим tooinvoke пользовательский Интерфейс входа в систему, пока: мы выполним hello пользователя нажмите кнопку «Вход» toodo таким образом.</span><span class="sxs-lookup"><span data-stu-id="3af06-139">However, we don't want tooinvoke a sign-in UI just yet - we'll make hello user click "Sign In" toodo so.</span></span>  <span data-ttu-id="3af06-140">Кроме того, в hello `OnInitialized(...)` метод:</span><span class="sxs-lookup"><span data-stu-id="3af06-140">Also in hello `OnInitialized(...)` method:</span></span>

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
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

* <span data-ttu-id="3af06-141">Если hello пользователь не выполнил вход и нажатии кнопки «Вход» hello, мы должны tooinvoke пользовательский Интерфейс входа и введите свои учетные данные пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="3af06-141">If hello user is not signed in and they click hello "Sign In" button, we want tooinvoke a login UI and have hello user enter their credentials.</span></span>  <span data-ttu-id="3af06-142">Реализация обработчика кнопки hello вход:</span><span class="sxs-lookup"><span data-stu-id="3af06-142">Implement hello Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

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
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
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

* <span data-ttu-id="3af06-143">Если hello пользователь успешно выполняет вход, MSAL будет получать и кэшировать маркер для вас и продолжением toocall hello `GetTodoList()` метод уверенно.</span><span class="sxs-lookup"><span data-stu-id="3af06-143">If hello user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed toocall hello `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="3af06-144">Все, что покинул tooget задачи пользователя — tooimplement hello `GetTodoList()` метод.</span><span class="sxs-lookup"><span data-stu-id="3af06-144">All that's left tooget a user's tasks is tooimplement hello `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

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

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

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

## <a name="run"></a><span data-ttu-id="3af06-145">Выполнить</span><span class="sxs-lookup"><span data-stu-id="3af06-145">Run</span></span>
<span data-ttu-id="3af06-146">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="3af06-146">Congratulations!</span></span> <span data-ttu-id="3af06-147">Теперь есть рабочее приложение .NET WPF hello возможность tooauthenticate пользователей & безопасно вызывать веб-API с помощью OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3af06-147">You now have a working .NET WPF app that has hello ability tooauthenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="3af06-148">Запустите оба проекта и выполните вход с личной учетной записью Майкрософт, рабочей или учебной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="3af06-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="3af06-149">Добавьте список дел задачи toothat пользователя.</span><span class="sxs-lookup"><span data-stu-id="3af06-149">Add tasks toothat user's To-Do list.</span></span>  <span data-ttu-id="3af06-150">Выйдите из системы и войти как другой пользователь tooview их список дел.</span><span class="sxs-lookup"><span data-stu-id="3af06-150">Sign out, and sign back in as another user tooview their To-Do list.</span></span>  <span data-ttu-id="3af06-151">Закройте приложение hello и выполните его повторно.</span><span class="sxs-lookup"><span data-stu-id="3af06-151">Close hello app, and re-run it.</span></span>  <span data-ttu-id="3af06-152">Обратите внимание на то, как hello пользовательского сеанса остается без изменений — это потому, что приложение hello кэширует маркеры в локальном файле.</span><span class="sxs-lookup"><span data-stu-id="3af06-152">Notice how hello user's session remains intact - that is because hello app caches tokens in a local file.</span></span>

<span data-ttu-id="3af06-153">MSAL позволяет легко tooincorporate общие функции управления удостоверениями в приложения, использование личных и рабочих учетных записей.</span><span class="sxs-lookup"><span data-stu-id="3af06-153">MSAL makes it easy tooincorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="3af06-154">Он отвечает за всю работу dirty hello вам - управления кэша, поддержка протокола OAuth, предоставляя hello пользователя с именем входа пользовательского интерфейса, обновление маркеры с истекшим сроком действия и многое другое.</span><span class="sxs-lookup"><span data-stu-id="3af06-154">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="3af06-155">Действительно требуется tooknow всего в одном вызове API `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="3af06-155">All you really need tooknow is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="3af06-156">Справочник по hello выполнить пример (без настройки) [предоставляется как .zip здесь](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), или вы можете клонировать из GitHub:</span><span class="sxs-lookup"><span data-stu-id="3af06-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="3af06-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3af06-157">Next steps</span></span>
<span data-ttu-id="3af06-158">Теперь можно перейти к более сложным темам.</span><span class="sxs-lookup"><span data-stu-id="3af06-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="3af06-159">Вы можете tootry:</span><span class="sxs-lookup"><span data-stu-id="3af06-159">You may want tootry:</span></span>

* [<span data-ttu-id="3af06-160">Обеспечение безопасности hello TodoListService веб-API с конечной точкой v2.0 hello</span><span class="sxs-lookup"><span data-stu-id="3af06-160">Securing hello TodoListService Web API with hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="3af06-161">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="3af06-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="3af06-162">Руководство разработчика v2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="3af06-162">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="3af06-163">Тег "msal" на StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="3af06-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="3af06-164">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="3af06-164">Get security updates for our products</span></span>
<span data-ttu-id="3af06-165">Мы рекомендуем вам уведомления при возникновении события безопасности, посетив tooget [эту страницу](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.</span><span class="sxs-lookup"><span data-stu-id="3af06-165">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

