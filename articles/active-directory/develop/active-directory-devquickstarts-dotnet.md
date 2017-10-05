---
title: "Приступая к работе с Azure AD в .NET | Документация Майкрософт"
description: "Практическое руководство по созданию классического приложения .NET Windows, которое интегрируется с Azure AD для входа в систему и вызывает программные интерфейсы приложения, защищенные Azure AD, по протоколу OAuth."
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
ms.openlocfilehash: 7a252e0e5243c7b7489373845531cb913ca1f6aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="0aa95-103">Интеграция Azure AD в классическое приложение Windows WPF</span><span class="sxs-lookup"><span data-stu-id="0aa95-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="0aa95-104">При разработке классического приложения служба Microsoft Azure Active Directory позволяет разработчику упростить проверку подлинности учетных записей пользователей в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0aa95-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="0aa95-105">Это также позволяет вашему приложению безопасно использовать любые веб-интерфейсы API, защищаемые с помощью Azure AD, например интерфейсы Office 365 API или Azure API.</span><span class="sxs-lookup"><span data-stu-id="0aa95-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="0aa95-106">Клиентские нативные приложения для .NET, которым необходим доступ к защищенным ресурсам, могут использовать библиотеку проверки подлинности Azure AD (ADAL).</span><span class="sxs-lookup"><span data-stu-id="0aa95-106">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="0aa95-107">Единственное предназначение ADAL — упростить для разработчика процесс получения маркеров доступа.</span><span class="sxs-lookup"><span data-stu-id="0aa95-107">ADAL's sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="0aa95-108">Чтобы показать, насколько это просто, создадим приложение To Do List (ведение списка дел) для .NET WPF, которое:</span><span class="sxs-lookup"><span data-stu-id="0aa95-108">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="0aa95-109">Получает маркеры доступа для вызова интерфейса Graph API Azure AD с помощью [протокола проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="0aa95-109">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="0aa95-110">Осуществляет поиск пользователей в каталоге по псевдониму.</span><span class="sxs-lookup"><span data-stu-id="0aa95-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="0aa95-111">Обеспечивает функцию выхода пользователя из приложения.</span><span class="sxs-lookup"><span data-stu-id="0aa95-111">Signs users out.</span></span>

<span data-ttu-id="0aa95-112">Для создания полного рабочего приложения необходимо:</span><span class="sxs-lookup"><span data-stu-id="0aa95-112">To build the complete working application, you'll need to:</span></span>

1. <span data-ttu-id="0aa95-113">Зарегистрировать приложение в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aa95-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="0aa95-114">установить и настроить ADAL;</span><span class="sxs-lookup"><span data-stu-id="0aa95-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="0aa95-115">использовать ADAL для получения маркеров из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aa95-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="0aa95-116">Чтобы начать работу, [скачайте схему приложения](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) или [скачайте готовый пример](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="0aa95-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="0aa95-117">Вам также потребуется клиент Azure AD, в котором можно создавать пользователей и регистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="0aa95-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="0aa95-118">Если клиента нет, [узнайте, как его получить](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="0aa95-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directorysearcher-application"></a><span data-ttu-id="0aa95-119">1. Регистрация приложения DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="0aa95-119">1. Register the DirectorySearcher Application</span></span>
<span data-ttu-id="0aa95-120">Чтобы приложение могло получать маркеры, сначала необходимо его зарегистрировать в клиенте Azure AD и предоставить ему разрешение на доступ к интерфейсу Graph API Azure AD:</span><span class="sxs-lookup"><span data-stu-id="0aa95-120">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="0aa95-121">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0aa95-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0aa95-122">На верхней панели щелкните учетную запись и в списке **Каталог** выберите клиент Active Directory, в котором хотите зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="0aa95-122">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="0aa95-123">В левой области навигации щелкните **Другие службы** и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0aa95-123">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="0aa95-124">Щелкните **Регистрация приложений** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0aa95-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="0aa95-125">Следуйте инструкциям на экране, а затем создайте новое **Собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="0aa95-125">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="0aa95-126">**Имя** приложения отображает его описание конечным пользователям.</span><span class="sxs-lookup"><span data-stu-id="0aa95-126">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="0aa95-127">**URI перенаправления** представляет собой сочетание схемы и строки, используемое Azure AD для возвращения любых маркеров, запрошенных приложением.</span><span class="sxs-lookup"><span data-stu-id="0aa95-127">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="0aa95-128">Укажите значение, специфичное для вашего приложения, например `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="0aa95-128">Enter a value specific to your application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="0aa95-129">После завершения регистрации служба Azure AD присваивает приложению уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="0aa95-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="0aa95-130">Это значение вам понадобится в следующих разделах, поэтому не забудьте скопировать его на странице приложения.</span><span class="sxs-lookup"><span data-stu-id="0aa95-130">You'll need this value in the next sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="0aa95-131">На странице **Параметры** выберите **Необходимые разрешения** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0aa95-131">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="0aa95-132">Выберите **Microsoft Graph** в качестве интерфейса API и добавьте разрешение **Чтение данных каталога** в списке **Делегированные разрешения**.</span><span class="sxs-lookup"><span data-stu-id="0aa95-132">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="0aa95-133">Это позволит приложению запрашивать интерфейс Graph API для пользователей.</span><span class="sxs-lookup"><span data-stu-id="0aa95-133">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="0aa95-134">2) Установка и настройка ADAL</span><span class="sxs-lookup"><span data-stu-id="0aa95-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="0aa95-135">Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="0aa95-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="0aa95-136">Чтобы ADAL могла обмениваться информацией с Azure AD, необходимо предоставить некоторую информацию о регистрации вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="0aa95-136">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="0aa95-137">Сначала добавьте ADAL в проект DirectorySearcher с помощью консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="0aa95-137">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="0aa95-138">В проекте DirectorySearcher откройте `app.config`.</span><span class="sxs-lookup"><span data-stu-id="0aa95-138">In the DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="0aa95-139">Замените значения элементов в разделе `<appSettings>` на значения, введенные на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0aa95-139">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="0aa95-140">Ваш код будет ссылаться на эти значения при каждом использовании ADAL.</span><span class="sxs-lookup"><span data-stu-id="0aa95-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="0aa95-141">`ida:Tenant` — это домен вашего клиента Azure AD, например contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="0aa95-141">The `ida:Tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="0aa95-142">`ida:ClientId` — это идентификатор clientId приложения, скопированный с портала.</span><span class="sxs-lookup"><span data-stu-id="0aa95-142">The `ida:ClientId` is the clientId of your application you copied from the portal.</span></span>
  * <span data-ttu-id="0aa95-143">`ida:RedirectUri` — это URL-адрес перенаправления, зарегистрированный на портале.</span><span class="sxs-lookup"><span data-stu-id="0aa95-143">The `ida:RedirectUri` is the redirect url you registered in the portal.</span></span>

## <a name="3----use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="0aa95-144">3.    Использование библиотеки ADAL для получения маркеров из AAD</span><span class="sxs-lookup"><span data-stu-id="0aa95-144">3.    Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="0aa95-145">Основной принцип ADAL состоит в следующем: каждый раз, когда вашему приложению необходим маркер доступа, оно будет просто вызывать `authContext.AcquireTokenAsync(...)`, а ADAL сделает все остальное.</span><span class="sxs-lookup"><span data-stu-id="0aa95-145">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="0aa95-146">В проекте `DirectorySearcher` откройте `MainWindow.xaml.cs` и найдите метод `MainWindow()`.</span><span class="sxs-lookup"><span data-stu-id="0aa95-146">In the `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate the `MainWindow()` method.</span></span>  <span data-ttu-id="0aa95-147">Первый шаг состоит в инициализации `AuthenticationContext` — основного класса ADAL.</span><span class="sxs-lookup"><span data-stu-id="0aa95-147">The first step is to initialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="0aa95-148">Здесь вы отправляете в библиотеку ADAL координаты, которые ей требуются для взаимодействия с Azure AD, и сообщаете о способе кэширования маркеров.</span><span class="sxs-lookup"><span data-stu-id="0aa95-148">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="0aa95-149">Теперь найдите метод `Search(...)` , который будет вызываться при нажатии кнопки "Поиск" в пользовательском интерфейсе приложения.</span><span class="sxs-lookup"><span data-stu-id="0aa95-149">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="0aa95-150">Этот метод выполняет запрос GET в интерфейс Graph API службы Azure AD для запроса списка пользователей, чьи UPN начинаются с данного слова поиска.</span><span class="sxs-lookup"><span data-stu-id="0aa95-150">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="0aa95-151">Но для отправки запросов в Graph API необходимо включить access_token в заголовок `Authorization` запроса — именно отсюда ADAL начинает свою работу.</span><span class="sxs-lookup"><span data-stu-id="0aa95-151">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate the Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for the To Do item name");
        return;
    }

    // Get an Access Token for the Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled the sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="0aa95-152">Когда приложение запрашивает маркер путем вызова `AcquireTokenAsync(...)`, библиотека ADAL пытается вернуть маркер без запроса учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="0aa95-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="0aa95-153">Если ADAL решит, что пользователь должен войти в систему для получения маркера, то служба отобразит диалоговое окно входа, соберет учетные данные пользователя и вернет маркер после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0aa95-153">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="0aa95-154">Если библиотеке ADAL не удастся по какой-либо причине вернуть маркер, она вызовет исключение `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="0aa95-154">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="0aa95-155">Обратите внимание, что объект `AuthenticationResult` содержит объект `UserInfo`, который может использоваться для сбора сведений, необходимых приложению.</span><span class="sxs-lookup"><span data-stu-id="0aa95-155">Notice that the `AuthenticationResult` object contains a `UserInfo` object that can be used to collect information your app may need.</span></span>  <span data-ttu-id="0aa95-156">В DirectorySearcher объект `UserInfo` используется для настройки пользовательского интерфейса приложения на основе идентификатора пользователя.</span><span class="sxs-lookup"><span data-stu-id="0aa95-156">In the DirectorySearcher, `UserInfo` is used to customize the app's UI with the user's id.</span></span>
* <span data-ttu-id="0aa95-157">Когда пользователь нажимает кнопку выхода, необходимо, чтобы при следующем вызове `AcquireTokenAsync(...)` пользователю было предложено войти.</span><span class="sxs-lookup"><span data-stu-id="0aa95-157">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenAsync(...)` will ask the user to sign in.</span></span>  <span data-ttu-id="0aa95-158">С ADAL это так же просто, как и очистка кэша маркера:</span><span class="sxs-lookup"><span data-stu-id="0aa95-158">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear the token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="0aa95-159">Если пользователь не нажимает кнопку выхода, то можно реализовать восстановление данных сеанса пользователя при следующем запуске приложения DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="0aa95-159">However, if the user does not click the "Sign Out" button, you will want to maintain the user's session for the next time they run the DirectorySearcher.</span></span>  <span data-ttu-id="0aa95-160">При запуске приложения можно проверить кэш маркеров библиотеки ADAL на наличие соответствующего маркера и соответственно обновить пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="0aa95-160">When the app launches, you can check ADAL's token cache for an existing token and update the UI accordingly.</span></span>  <span data-ttu-id="0aa95-161">В методе `CheckForCachedToken()` выполните другой вызов `AcquireTokenAsync(...)`, на этот раз передав параметр `PromptBehavior.Never`.</span><span class="sxs-lookup"><span data-stu-id="0aa95-161">In the `CheckForCachedToken()` method, make another call to `AcquireTokenAsync(...)`, this time passing in the `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="0aa95-162">`PromptBehavior.Never` сообщает ADAL, что пользователю не следует предлагать войти, и вместо этого библиотека ADAL должна породить исключение, если не удается вернуть маркер.</span><span class="sxs-lookup"><span data-stu-id="0aa95-162">`PromptBehavior.Never` will tell ADAL that the user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable to return a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As the application starts, try to get an access token without prompting the user.  If one exists, show the user as signed in.
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

        // If user interaction is required, proceed to main page without singing the user in.
        return;
    }

    // A valid token is in the cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="0aa95-163">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="0aa95-163">Congratulations!</span></span> <span data-ttu-id="0aa95-164">Теперь у нас есть рабочее приложение .NET WPF, которое позволяет проверять подлинность пользователей, безопасно вызывать методы веб-интерфейсов API по протоколу OAuth 2.0 и получать основные сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="0aa95-164">You now have a working .NET WPF application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="0aa95-165">Если же вы этого еще не сделали, пришло время добавить в клиент нескольких пользователей.</span><span class="sxs-lookup"><span data-stu-id="0aa95-165">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="0aa95-166">Запустите приложение DirectorySearcher и войдите как один из этих пользователей.</span><span class="sxs-lookup"><span data-stu-id="0aa95-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="0aa95-167">Осуществите поиск других пользователей по их имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="0aa95-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="0aa95-168">Закройте приложение и снова запустите его.</span><span class="sxs-lookup"><span data-stu-id="0aa95-168">Close the app, and re-run it.</span></span>  <span data-ttu-id="0aa95-169">Обратите внимание на то, что пользовательский сеанс остался без изменений.</span><span class="sxs-lookup"><span data-stu-id="0aa95-169">Notice how the user's session remains intact.</span></span>  <span data-ttu-id="0aa95-170">Выйдите и снова войдите от имени другого пользователя.</span><span class="sxs-lookup"><span data-stu-id="0aa95-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="0aa95-171">ADAL упрощает процесс включения всех этих общих возможностей идентификации в приложение.</span><span class="sxs-lookup"><span data-stu-id="0aa95-171">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="0aa95-172">Он отвечает за всю грязную работу: управление кэшем, поддержку протокола OAuth, предоставление пользователю пользовательского интерфейса для входа, обновление истекших маркеров и многое другое.</span><span class="sxs-lookup"><span data-stu-id="0aa95-172">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="0aa95-173">Все, что вам действительно нужно знать, — это вызов интерфейса API `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="0aa95-173">All you really need to know is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="0aa95-174">Завершенный образец (без ваших настроек) вы можете загрузить [отсюда](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="0aa95-174">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="0aa95-175">Теперь можно приступить к изучению других сценариев.</span><span class="sxs-lookup"><span data-stu-id="0aa95-175">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="0aa95-176">Можно попробовать:</span><span class="sxs-lookup"><span data-stu-id="0aa95-176">You may want to try:</span></span>

[<span data-ttu-id="0aa95-177">Защита веб-API с помощью Azure AD для .NET >></span><span class="sxs-lookup"><span data-stu-id="0aa95-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

