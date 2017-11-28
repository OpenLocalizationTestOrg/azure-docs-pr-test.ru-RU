---
title: "Приступая к работе Windows Phone AD aaaAzure | Документы Microsoft"
description: "Как toobuild приложения Windows Phone, который интегрируется с Azure AD для входа и вызывает Azure AD защищен с помощью OAuth API-интерфейсы."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="14548-103">Интеграция Azure AD с помощью приложения Windows Phone</span><span class="sxs-lookup"><span data-stu-id="14548-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="14548-104">Проекты для версии Windows Phone 8.1 и более ранних версий не поддерживаются в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="14548-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="14548-105">Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="14548-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="14548-106">При разработке приложения Windows Phone 8.1, Azure AD позволяет простым и понятным для вас tooauthenticate пользователей с их учетными записями Active Directory.</span><span class="sxs-lookup"><span data-stu-id="14548-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="14548-107">Toosecurely вашего приложения также позволяет использовать любой веб-API, защищенные Azure AD, таких как hello API Office 365 или hello Azure API.</span><span class="sxs-lookup"><span data-stu-id="14548-107">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="14548-108">Этот пример кода использует ADAL версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="14548-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="14548-109">Для hello новейшие технологии, вы можете tooinstead try нашей [универсальной учебника Windows с помощью ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="14548-109">For hello latest technology, you may want tooinstead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="14548-110">При построении приложения для Windows Phone 8.1 на самом деле, это подходящее место hello.</span><span class="sxs-lookup"><span data-stu-id="14548-110">If you are indeed building an app for Windows Phone 8.1, this is hello right place.</span></span>  <span data-ttu-id="14548-111">ADAL v2.0 по-прежнему полностью поддерживаются, и является hello рекомендуемый способ agianst разработки приложений Windows Phone 8.1 с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14548-111">ADAL v2.0 is still fully supported, and is hello recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="14548-112">Для .NET собственных клиентов, которым требуется tooaccess защищенные ресурсы Azure AD предоставляет hello библиотеку аутентификации Active Directory или ADAL.</span><span class="sxs-lookup"><span data-stu-id="14548-112">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="14548-113">Единственной целью ADAL в жизни является toomake легко и маркеры доступа tooget вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="14548-113">ADAL’s sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="14548-114">toodemonstrate, насколько просто здесь мы выполним сборку «Directory модуль поиска» приложения Windows Phone 8.1:</span><span class="sxs-lookup"><span data-stu-id="14548-114">toodemonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="14548-115">Получает маркеры для вызова API Azure AD Graph hello, с помощью hello доступа [протокол проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="14548-115">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="14548-116">осуществляет поиск пользователей в каталоге с помощью заданного UPN;</span><span class="sxs-lookup"><span data-stu-id="14548-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="14548-117">Обеспечивает функцию выхода пользователя из приложения.</span><span class="sxs-lookup"><span data-stu-id="14548-117">Signs users out.</span></span>

<span data-ttu-id="14548-118">toobuild hello полное рабочее приложение, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="14548-118">toobuild hello complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="14548-119">Зарегистрировать приложение в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14548-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="14548-120">установить и настроить ADAL;</span><span class="sxs-lookup"><span data-stu-id="14548-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="14548-121">Используйте ADAL tooget токены из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14548-121">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="14548-122">запущена, tooget [загрузить каркас проекта](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) или [загрузить образец hello завершения](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="14548-122">tooget started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="14548-123">Каждый из них является решением Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="14548-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="14548-124">Вам также потребуется клиент Azure AD, в котором можно создавать пользователей и регистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="14548-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="14548-125">Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="14548-125">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directory-searcher-application"></a><span data-ttu-id="14548-126">1. Регистрация hello Directory время приложения</span><span class="sxs-lookup"><span data-stu-id="14548-126">1. Register hello Directory Searcher Application</span></span>
<span data-ttu-id="14548-127">tooenable маркеров tooget вашего приложения, сначала необходимо tooregister его в Azure AD клиента и предоставить ему разрешение tooaccess hello API Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="14548-127">tooenable your app tooget tokens, you’ll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="14548-128">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="14548-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="14548-129">На верхней панели hello, нажмите кнопку в вашей учетной записи, а также в разделе hello **каталога** выберите hello клиента Active Directory, где будут tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="14548-129">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="14548-130">Щелкните **более служб** в hello левую панель навигации и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="14548-130">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="14548-131">Щелкните **Регистрация приложений** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="14548-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="14548-132">Следуйте инструкциям hello и создайте новый **собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="14548-132">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="14548-133">Hello **имя** из hello приложения будет описывать tooend пользователей вашего приложения</span><span class="sxs-lookup"><span data-stu-id="14548-133">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="14548-134">Hello **Uri перенаправления** представляет собой комбинацию схему и строки, использование маркеров ответы tooreturn Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14548-134">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="14548-135">Введите значение заполнителя, например, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="14548-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="14548-136">Это значение мы заменим позже.</span><span class="sxs-lookup"><span data-stu-id="14548-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="14548-137">После завершения регистрации служба Azure AD присваивает приложению уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="14548-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="14548-138">Это значение необходимо в следующих разделах hello, поэтому скопируйте его с вкладка "приложение" hello.</span><span class="sxs-lookup"><span data-stu-id="14548-138">You’ll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="14548-139">Из hello **параметры** выберите **требуемые разрешения** и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="14548-139">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="14548-140">Выберите hello **Microsoft Graph** как hello API и добавьте hello **чтение данных каталога** разрешение в списке **делегированные разрешения**.</span><span class="sxs-lookup"><span data-stu-id="14548-140">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="14548-141">Это позволит вашей hello tooquery приложения Graph API для пользователей.</span><span class="sxs-lookup"><span data-stu-id="14548-141">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="14548-142">2. Установка и настройка ADAL</span><span class="sxs-lookup"><span data-stu-id="14548-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="14548-143">Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="14548-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="14548-144">Чтобы может toocommunicate ADAL toobe с Azure AD, необходимо tooprovide его с некоторые сведения о регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="14548-144">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="14548-145">Сначала добавьте проект DirectorySearcher ADAL toohello с помощью консоли диспетчера пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="14548-145">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="14548-146">В проекте DirectorySearcher hello откройте `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="14548-146">In hello DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="14548-147">Замените значения hello hello `Config Values` hello tooreflect области значений входных данных в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="14548-147">Replace hello values in hello `Config Values` region tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="14548-148">Ваш код будет ссылаться на эти значения при каждом использовании ADAL.</span><span class="sxs-lookup"><span data-stu-id="14548-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="14548-149">Hello `tenant` hello домен вашего клиента Azure AD, например, contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="14548-149">hello `tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="14548-150">Hello `clientId` — hello clientId приложения скопирован с портала hello.</span><span class="sxs-lookup"><span data-stu-id="14548-150">hello `clientId` is hello clientId of your application you copied from hello portal.</span></span>
* <span data-ttu-id="14548-151">Uri обратного вызова hello toodiscover теперь требуется для приложения Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="14548-151">You now need toodiscover hello callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="14548-152">Установите точку останова в этой строке в hello `MainPage` метод:</span><span class="sxs-lookup"><span data-stu-id="14548-152">Set a breakpoint on this line in hello `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="14548-153">Выполните приложение hello и скопируйте выделенное значение hello `redirectUri` при попадании в точку останова hello.</span><span class="sxs-lookup"><span data-stu-id="14548-153">Run hello app, and copy aside hello value of `redirectUri` when hello breakpoint is hit.</span></span>  <span data-ttu-id="14548-154">Оно должно иметь примерно следующий вид:</span><span class="sxs-lookup"><span data-stu-id="14548-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="14548-155">Включите hello **Настройка** вкладка приложения hello портала управления Azure, замените значение hello hello **RedirectUri** с этим значением.</span><span class="sxs-lookup"><span data-stu-id="14548-155">Back on hello **Configure** tab of your application in hello Azure Management Portal, replace hello value of hello **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="14548-156">3. Использование токенов ADAL tooGet из AAD</span><span class="sxs-lookup"><span data-stu-id="14548-156">3. Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="14548-157">Hello базовый принцип ADAL — что всякий раз, когда ваше приложение должно маркер доступа, он просто вызывает `authContext.AcquireToken(…)`, и ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="14548-157">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="14548-158">Hello первым шагом является tooinitialize приложения `AuthenticationContext` -ADAL основной класс.</span><span class="sxs-lookup"><span data-stu-id="14548-158">hello first step is tooinitialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="14548-159">Это происходит, где передается ADAL hello координаты, он должен toocommunicate с Azure AD и о том, как toocache маркеры.</span><span class="sxs-lookup"><span data-stu-id="14548-159">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="14548-160">Теперь найдите hello `Search(...)` метод, который вызывается, если пользователь cliks hello hello кнопки «Поиск» в пользовательском Интерфейсе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="14548-160">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="14548-161">Этот метод делает tooquery toohello API Azure AD Graph запрос GET для пользователей, имя участника-пользователя начинается с заданного условия поиска hello.</span><span class="sxs-lookup"><span data-stu-id="14548-161">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="14548-162">Но в порядке tooquery hello Graph API, необходимо tooinclude access_token в hello `Authorization` заголовок hello запрос — где вступает в дело ADAL.</span><span class="sxs-lookup"><span data-stu-id="14548-162">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="14548-163">При необходимости в интерактивной проверки подлинности ADAL будет использовать Windows Phone Web Authentication Broker (адресной книги Windows) и [продолжения модели](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) страница входа toodisplay hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14548-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD sign in page.</span></span>  <span data-ttu-id="14548-164">При входе в систему пользователя hello, приложение должно toopass ADAL hello результаты взаимодействия адресной книги Windows hello.</span><span class="sxs-lookup"><span data-stu-id="14548-164">When hello user signs in, your app needs toopass ADAL hello results of hello WAB interaction.</span></span>  <span data-ttu-id="14548-165">Это сводится реализации hello `ContinueWebAuthentication` интерфейс:</span><span class="sxs-lookup"><span data-stu-id="14548-165">This is as simple as implementing hello `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="14548-166">Теперь настало время hello toouse `AuthenticationResult` , ADAL, возвращается tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="14548-166">Now it's time toouse hello `AuthenticationResult` that ADAL returned tooyour app.</span></span>  <span data-ttu-id="14548-167">В hello `QueryGraph(...)` обратного вызова, присоединение hello access_token вы приобрели toohello запрос GET в заголовке авторизации hello:</span><span class="sxs-lookup"><span data-stu-id="14548-167">In hello `QueryGraph(...)` callback, attach hello access_token you acquired toohello GET request in hello Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="14548-168">Можно также использовать hello `AuthenticationResult` объекта toodisplay сведения о пользователе hello в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="14548-168">You can also use hello `AuthenticationResult` object toodisplay information about hello user in your app.</span></span> <span data-ttu-id="14548-169">В hello `QueryGraph(...)` метод, используйте hello результат tooshow hello идентификатор пользователя на странице приветствия:</span><span class="sxs-lookup"><span data-stu-id="14548-169">In hello `QueryGraph(...)` method, use hello result tooshow hello user's id on hello page:</span></span>

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="14548-170">Наконец можно использовать ADAL toosign hello выход пользователя из приложения, а также.</span><span class="sxs-lookup"><span data-stu-id="14548-170">Finally, you can use ADAL toosign hello user out of hte application as well.</span></span>  <span data-ttu-id="14548-171">Hello пользователь нажимает кнопку «Выйти» hello, мы хотим tooensure, слишком hello следующего вызова`AcquireTokenSilentAsync(...)` завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="14548-171">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="14548-172">С помощью ADAL это так же легко, как очистить кэш токена hello:</span><span class="sxs-lookup"><span data-stu-id="14548-172">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="14548-173">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="14548-173">Congratulations!</span></span> <span data-ttu-id="14548-174">Теперь у рабочего приложения Windows Phone hello возможность tooauthenticate пользователей, безопасно вызвать веб-API с помощью OAuth 2.0 и получить основные сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="14548-174">You now have a working Windows Phone app that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="14548-175">Если это еще не сделано, пришло время toopopulate hello вашего клиента с некоторым пользователям.</span><span class="sxs-lookup"><span data-stu-id="14548-175">If you haven’t already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="14548-176">Запустите свое приложение DirectorySearcher и войдите под именем одного из таких пользователей.</span><span class="sxs-lookup"><span data-stu-id="14548-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="14548-177">Осуществите поиск других пользователей по их имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="14548-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="14548-178">Закройте приложение hello и выполните его повторно.</span><span class="sxs-lookup"><span data-stu-id="14548-178">Close hello app, and re-run it.</span></span>  <span data-ttu-id="14548-179">Обратите внимание на то, как hello пользовательского сеанса остается без изменений.</span><span class="sxs-lookup"><span data-stu-id="14548-179">Notice how hello user’s session remains intact.</span></span>  <span data-ttu-id="14548-180">Выйдите и снова войдите под именем другого пользователя.</span><span class="sxs-lookup"><span data-stu-id="14548-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="14548-181">ADAL упрощает легко tooincorporate все эти общие функции управления удостоверениями в приложения.</span><span class="sxs-lookup"><span data-stu-id="14548-181">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="14548-182">Он отвечает за всю работу dirty hello вам - управления кэша, поддержка протокола OAuth, предоставляя hello пользователя с именем входа пользовательского интерфейса, обновление маркеры с истекшим сроком действия и многое другое.</span><span class="sxs-lookup"><span data-stu-id="14548-182">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="14548-183">Действительно требуется tooknow всего в одном вызове API `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="14548-183">All you really need tooknow is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="14548-184">Справочник по образец hello завершена (без настройки) предоставляется [здесь](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="14548-184">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="14548-185">Теперь можно переходить на сценариях tooadditional удостоверений.</span><span class="sxs-lookup"><span data-stu-id="14548-185">You can now move on tooadditional identity scenarios.</span></span>  <span data-ttu-id="14548-186">Вы можете tootry:</span><span class="sxs-lookup"><span data-stu-id="14548-186">You may want tootry:</span></span>

[<span data-ttu-id="14548-187">Защита веб-API с помощью Azure AD для .NET >></span><span class="sxs-lookup"><span data-stu-id="14548-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

