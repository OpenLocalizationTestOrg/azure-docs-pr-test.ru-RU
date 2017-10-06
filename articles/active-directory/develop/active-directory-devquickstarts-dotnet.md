---
title: "Приступая к работе .NET aaaAzure AD | Документы Microsoft"
description: "Как toobuild .NET классическое приложение Windows, интегрируется с Azure AD для входа и вызывает Azure AD защищен с помощью OAuth API-интерфейсы."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="d1864-103">Интеграция Azure AD в классическое приложение Windows WPF</span><span class="sxs-lookup"><span data-stu-id="d1864-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="d1864-104">Если вы разрабатываете приложение рабочей среды, Azure AD упрощает простыми и понятными для вас tooauthenticate пользователей с их учетными записями Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d1864-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="d1864-105">Toosecurely вашего приложения также позволяет использовать любой веб-API, защищенные Azure AD, таких как hello API Office 365 или hello Azure API.</span><span class="sxs-lookup"><span data-stu-id="d1864-105">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="d1864-106">Для .NET собственных клиентов, которым требуется tooaccess защищенные ресурсы Azure AD предоставляет hello библиотеку аутентификации Active Directory или ADAL.</span><span class="sxs-lookup"><span data-stu-id="d1864-106">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="d1864-107">Единственной целью ADAL в жизни является toomake легко и маркеры доступа tooget вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d1864-107">ADAL's sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="d1864-108">toodemonstrate, насколько просто здесь мы создадим приложение .NET WPF задача список:</span><span class="sxs-lookup"><span data-stu-id="d1864-108">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="d1864-109">Получает маркеры для вызова API Azure AD Graph hello, с помощью hello доступа [протокол проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1864-109">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="d1864-110">Осуществляет поиск пользователей в каталоге по псевдониму.</span><span class="sxs-lookup"><span data-stu-id="d1864-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="d1864-111">Обеспечивает функцию выхода пользователя из приложения.</span><span class="sxs-lookup"><span data-stu-id="d1864-111">Signs users out.</span></span>

<span data-ttu-id="d1864-112">toobuild hello полное рабочее приложение, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="d1864-112">toobuild hello complete working application, you'll need to:</span></span>

1. <span data-ttu-id="d1864-113">Зарегистрировать приложение в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1864-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="d1864-114">установить и настроить ADAL;</span><span class="sxs-lookup"><span data-stu-id="d1864-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="d1864-115">Используйте ADAL tooget токены из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1864-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="d1864-116">tooget к работе, [загрузить каркас приложения hello](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) или [загрузить образец hello завершения](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d1864-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="d1864-117">Вам также потребуется клиент Azure AD, в котором можно создавать пользователей и регистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="d1864-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="d1864-118">Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="d1864-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directorysearcher-application"></a><span data-ttu-id="d1864-119">1. Регистрация приложения DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="d1864-119">1. Register hello DirectorySearcher Application</span></span>
<span data-ttu-id="d1864-120">tooenable маркеров tooget вашего приложения, сначала необходимо tooregister его в Azure AD клиента и предоставить ему разрешение tooaccess hello API Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="d1864-120">tooenable your app tooget tokens, you'll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="d1864-121">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d1864-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d1864-122">На верхней панели hello, нажмите кнопку в вашей учетной записи, а также в разделе hello **каталога** выберите hello клиента Active Directory, где будут tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="d1864-122">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="d1864-123">Щелкните **более служб** в hello левую панель навигации и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1864-123">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="d1864-124">Щелкните **Регистрация приложений** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d1864-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="d1864-125">Следуйте инструкциям hello и создайте новый **собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="d1864-125">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="d1864-126">Hello **имя** из hello приложения будет описывать tooend пользователей вашего приложения</span><span class="sxs-lookup"><span data-stu-id="d1864-126">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="d1864-127">Hello **Uri перенаправления** представляет собой комбинацию схему и строки, использование маркеров ответы tooreturn Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1864-127">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="d1864-128">Введите приложении tooyour определенного значения, например `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="d1864-128">Enter a value specific tooyour application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="d1864-129">После завершения регистрации служба Azure AD присваивает приложению уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="d1864-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="d1864-130">Это значение необходимо в следующих разделах hello, поэтому скопируйте его со страницы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d1864-130">You'll need this value in hello next sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="d1864-131">Из hello **параметры** выберите **требуемые разрешения** и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="d1864-131">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="d1864-132">Выберите hello **Microsoft Graph** как hello API и добавьте hello **чтение данных каталога** разрешение в списке **делегированные разрешения**.</span><span class="sxs-lookup"><span data-stu-id="d1864-132">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="d1864-133">Это позволит вашей hello tooquery приложения Graph API для пользователей.</span><span class="sxs-lookup"><span data-stu-id="d1864-133">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="d1864-134">2. Установка и настройка ADAL</span><span class="sxs-lookup"><span data-stu-id="d1864-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="d1864-135">Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="d1864-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="d1864-136">Чтобы может toocommunicate ADAL toobe с Azure AD, необходимо tooprovide его с некоторые сведения о регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="d1864-136">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="d1864-137">Сначала добавьте проект DirectorySearcher ADAL toohello с помощью консоли диспетчера пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="d1864-137">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="d1864-138">В проекте DirectorySearcher hello откройте `app.config`.</span><span class="sxs-lookup"><span data-stu-id="d1864-138">In hello DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="d1864-139">Замените значения hello элементов hello в hello `<appSettings>` раздел tooreflect hello значения входных данных в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="d1864-139">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="d1864-140">Ваш код будет ссылаться на эти значения при каждом использовании ADAL.</span><span class="sxs-lookup"><span data-stu-id="d1864-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="d1864-141">Hello `ida:Tenant` hello домен вашего клиента Azure AD, например, contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="d1864-141">hello `ida:Tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="d1864-142">Hello `ida:ClientId` — hello clientId приложения скопирован с портала hello.</span><span class="sxs-lookup"><span data-stu-id="d1864-142">hello `ida:ClientId` is hello clientId of your application you copied from hello portal.</span></span>
  * <span data-ttu-id="d1864-143">Hello `ida:RedirectUri` — hello зарегистрирован в портале hello URL-адрес перенаправления.</span><span class="sxs-lookup"><span data-stu-id="d1864-143">hello `ida:RedirectUri` is hello redirect url you registered in hello portal.</span></span>

## <a name="3----use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="d1864-144">3.    Использование токенов ADAL tooGet из AAD</span><span class="sxs-lookup"><span data-stu-id="d1864-144">3.    Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="d1864-145">Hello базовый принцип ADAL — что всякий раз, когда ваше приложение должно маркер доступа, он просто вызывает `authContext.AcquireTokenAsync(...)`, и ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="d1864-145">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="d1864-146">В hello `DirectorySearcher` откройте проект `MainWindow.xaml.cs` и найдите hello `MainWindow()` метод.</span><span class="sxs-lookup"><span data-stu-id="d1864-146">In hello `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate hello `MainWindow()` method.</span></span>  <span data-ttu-id="d1864-147">Hello первым шагом является tooinitialize приложения `AuthenticationContext` -ADAL основной класс.</span><span class="sxs-lookup"><span data-stu-id="d1864-147">hello first step is tooinitialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="d1864-148">Это происходит, где передается ADAL hello координаты, он должен toocommunicate с Azure AD и о том, как toocache маркеры.</span><span class="sxs-lookup"><span data-stu-id="d1864-148">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="d1864-149">Теперь найдите hello `Search(...)` метод, который вызывается, если пользователь cliks hello hello кнопки «Поиск» в пользовательском Интерфейсе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d1864-149">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="d1864-150">Этот метод делает tooquery toohello API Azure AD Graph запрос GET для пользователей, имя участника-пользователя начинается с заданного условия поиска hello.</span><span class="sxs-lookup"><span data-stu-id="d1864-150">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="d1864-151">Но в порядке tooquery hello Graph API, необходимо tooinclude access_token в hello `Authorization` заголовок hello запрос — где вступает в дело ADAL.</span><span class="sxs-lookup"><span data-stu-id="d1864-151">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="d1864-152">Когда приложение запрашивает маркер путем вызова `AcquireTokenAsync(...)`, ADAL попытается tooreturn маркер без запроса учетных данных пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="d1864-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="d1864-153">Если ADAL определит, что данный пользователь hello должен toosign в tooget маркер, оно отображает диалоговое окно входа в систему, собирать hello учетные данные пользователя и возвращает токен после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d1864-153">If ADAL determines that hello user needs toosign in tooget a token, it will display a login dialog, collect hello user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="d1864-154">Если не удается tooreturn токен ADAL для какой-либо причине, он будет вызывать `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="d1864-154">If ADAL is unable tooreturn a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="d1864-155">Обратите внимание, что hello `AuthenticationResult` объект содержит `UserInfo` объект, который может быть toocollect используется информация приложения может потребоваться.</span><span class="sxs-lookup"><span data-stu-id="d1864-155">Notice that hello `AuthenticationResult` object contains a `UserInfo` object that can be used toocollect information your app may need.</span></span>  <span data-ttu-id="d1864-156">В hello DirectorySearcher `UserInfo` является приложение hello используется toocustomize пользовательского интерфейса с идентификатором hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="d1864-156">In hello DirectorySearcher, `UserInfo` is used toocustomize hello app's UI with hello user's id.</span></span>
* <span data-ttu-id="d1864-157">Hello пользователь нажимает кнопку «Выйти» hello, мы хотим tooensure, слишком hello следующего вызова`AcquireTokenAsync(...)` запросит toosign пользователя hello в.</span><span class="sxs-lookup"><span data-stu-id="d1864-157">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenAsync(...)` will ask hello user toosign in.</span></span>  <span data-ttu-id="d1864-158">С помощью ADAL это так же легко, как очистить кэш токена hello:</span><span class="sxs-lookup"><span data-stu-id="d1864-158">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="d1864-159">Тем не менее если пользователь hello не нажать кнопку hello «Выход», требуется toomaintain hello пользовательский сеанс для hello очередном запуске hello DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="d1864-159">However, if hello user does not click hello "Sign Out" button, you will want toomaintain hello user's session for hello next time they run hello DirectorySearcher.</span></span>  <span data-ttu-id="d1864-160">При запуске приложения hello, могут возвращать кэш токена ADAL для существующего маркера и соответствующим образом обновить hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d1864-160">When hello app launches, you can check ADAL's token cache for an existing token and update hello UI accordingly.</span></span>  <span data-ttu-id="d1864-161">В hello `CheckForCachedToken()` метода, выполнение другого вызова слишком`AcquireTokenAsync(...)`, на этот раз, передавая hello `PromptBehavior.Never` параметра.</span><span class="sxs-lookup"><span data-stu-id="d1864-161">In hello `CheckForCachedToken()` method, make another call too`AcquireTokenAsync(...)`, this time passing in hello `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="d1864-162">`PromptBehavior.Never`сообщает ADAL hello пользователь не должен появиться запрос для входа, которое ADAL следует вместо создания исключения, если это не удается tooreturn маркер.</span><span class="sxs-lookup"><span data-stu-id="d1864-162">`PromptBehavior.Never` will tell ADAL that hello user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable tooreturn a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="d1864-163">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="d1864-163">Congratulations!</span></span> <span data-ttu-id="d1864-164">Теперь имеют работающее приложение .NET WPF hello возможность tooauthenticate пользователей, безопасно вызвать веб-API с помощью OAuth 2.0 и получить основные сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="d1864-164">You now have a working .NET WPF application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="d1864-165">Если это еще не сделано, пришло время toopopulate hello вашего клиента с некоторым пользователям.</span><span class="sxs-lookup"><span data-stu-id="d1864-165">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="d1864-166">Запустите свое приложение DirectorySearcher и войдите под именем одного из таких пользователей.</span><span class="sxs-lookup"><span data-stu-id="d1864-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="d1864-167">Осуществите поиск других пользователей по их имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="d1864-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="d1864-168">Закройте приложение hello и выполните его повторно.</span><span class="sxs-lookup"><span data-stu-id="d1864-168">Close hello app, and re-run it.</span></span>  <span data-ttu-id="d1864-169">Обратите внимание на то, как hello пользовательского сеанса остается без изменений.</span><span class="sxs-lookup"><span data-stu-id="d1864-169">Notice how hello user's session remains intact.</span></span>  <span data-ttu-id="d1864-170">Выйдите и снова войдите под именем другого пользователя.</span><span class="sxs-lookup"><span data-stu-id="d1864-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="d1864-171">ADAL упрощает легко tooincorporate все эти общие функции управления удостоверениями в приложения.</span><span class="sxs-lookup"><span data-stu-id="d1864-171">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="d1864-172">Он отвечает за всю работу dirty hello вам - управления кэша, поддержка протокола OAuth, предоставляя hello пользователя с именем входа пользовательского интерфейса, обновление маркеры с истекшим сроком действия и многое другое.</span><span class="sxs-lookup"><span data-stu-id="d1864-172">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="d1864-173">Действительно требуется tooknow всего в одном вызове API `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="d1864-173">All you really need tooknow is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="d1864-174">Справочник по образец hello завершена (без настройки) предоставляется [здесь](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d1864-174">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="d1864-175">Теперь можно переходить на tooadditional сценариев.</span><span class="sxs-lookup"><span data-stu-id="d1864-175">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="d1864-176">Вы можете tootry:</span><span class="sxs-lookup"><span data-stu-id="d1864-176">You may want tootry:</span></span>

[<span data-ttu-id="d1864-177">Защита веб-API с помощью Azure AD для .NET >></span><span class="sxs-lookup"><span data-stu-id="d1864-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

