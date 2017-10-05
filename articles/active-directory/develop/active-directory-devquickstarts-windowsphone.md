---
title: "Приступая к работе с Windows Phone Azure AD | Документация Майкрософт"
description: "Практическое руководство по созданию приложения Windows Phone, которое интегрируется с Azure AD для входа в систему и вызывает программные интерфейсы приложения, защищаемые системой Azure AD с помощью OAuth."
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
ms.openlocfilehash: 03c4b6d225dce99d79ef6c1ba2af43af8dea3eae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="f3d12-103">Интеграция Azure AD с помощью приложения Windows Phone</span><span class="sxs-lookup"><span data-stu-id="f3d12-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="f3d12-104">Проекты для версии Windows Phone 8.1 и более ранних версий не поддерживаются в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f3d12-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="f3d12-105">Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="f3d12-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="f3d12-106">При разработке приложения Windows Phone 8.1 система Azure AD позволяет легко и просто осуществлять проверку подлинности пользователей с помощью их учетных записей в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f3d12-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="f3d12-107">Это также позволяет вашему приложению безопасно использовать любые веб-интерфейсы API, защищаемые с помощью Azure AD, например интерфейсы Office 365 API или Azure API.</span><span class="sxs-lookup"><span data-stu-id="f3d12-107">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="f3d12-108">Этот пример кода использует ADAL версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="f3d12-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="f3d12-109">С учетом развития новейших технологий, возможно, вы захотите ознакомиться с нашим [учебником по универсальным приложениям Windows, использующим ADAL версии 3.0](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="f3d12-109">For the latest technology, you may want to instead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="f3d12-110">Если вы создаете приложение для Windows Phone 8.1, это то, что вам необходимо.</span><span class="sxs-lookup"><span data-stu-id="f3d12-110">If you are indeed building an app for Windows Phone 8.1, this is the right place.</span></span>  <span data-ttu-id="f3d12-111">ADAL версии 2.0 по-прежнему полностью поддерживается и является рекомендуемым способом разработки приложений для Windows Phone 8.1 с использованием Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3d12-111">ADAL v2.0 is still fully supported, and is the recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="f3d12-112">Собственным клиентам .NET, которым необходим доступ к защищенным ресурсам, Azure AD предлагает использовать библиотеку проверки подлинности Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="f3d12-112">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="f3d12-113">Единственное предназначение ADAL — упростить процесс получения маркеров доступа.</span><span class="sxs-lookup"><span data-stu-id="f3d12-113">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="f3d12-114">Чтобы продемонстрировать, насколько простой является данная процедура, мы выполним сборку приложения Windows Phone 8.1 «DirectorySearcher», которое:</span><span class="sxs-lookup"><span data-stu-id="f3d12-114">To demonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="f3d12-115">получает маркеры доступа для вызова интерфейса Graph API Azure AD с помощью [протокола проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx);</span><span class="sxs-lookup"><span data-stu-id="f3d12-115">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="f3d12-116">осуществляет поиск пользователей в каталоге с помощью заданного UPN;</span><span class="sxs-lookup"><span data-stu-id="f3d12-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="f3d12-117">Обеспечивает функцию выхода пользователя из приложения.</span><span class="sxs-lookup"><span data-stu-id="f3d12-117">Signs users out.</span></span>

<span data-ttu-id="f3d12-118">Для создания полного рабочего приложения необходимо:</span><span class="sxs-lookup"><span data-stu-id="f3d12-118">To build the complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="f3d12-119">Зарегистрировать приложение в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3d12-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="f3d12-120">установить и настроить ADAL;</span><span class="sxs-lookup"><span data-stu-id="f3d12-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="f3d12-121">использовать ADAL для получения маркеров из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3d12-121">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="f3d12-122">Чтобы начать работу, [скачайте проект схемы](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) или [готовый пример](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f3d12-122">To get started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="f3d12-123">Каждый из них является решением Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="f3d12-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="f3d12-124">Вам также потребуется клиент Azure AD, в котором можно создавать пользователей и регистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="f3d12-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="f3d12-125">Если клиента нет, [узнайте, как его получить](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="f3d12-125">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directory-searcher-application"></a><span data-ttu-id="f3d12-126">1. Регистрация приложения Directory Searcher</span><span class="sxs-lookup"><span data-stu-id="f3d12-126">1. Register the Directory Searcher Application</span></span>
<span data-ttu-id="f3d12-127">Чтобы приложение могло получать маркеры, сначала необходимо его зарегистрировать в клиенте Azure AD и предоставить ему разрешение на доступ к интерфейсу Graph API Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3d12-127">To enable your app to get tokens, you’ll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="f3d12-128">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f3d12-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f3d12-129">На верхней панели щелкните учетную запись и в списке **Каталог** выберите клиент Active Directory, в котором хотите зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="f3d12-129">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="f3d12-130">В левой области навигации щелкните **Другие службы** и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f3d12-130">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="f3d12-131">Щелкните **Регистрация приложений** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f3d12-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="f3d12-132">Следуйте инструкциям на экране, а затем создайте новое **Собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="f3d12-132">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="f3d12-133">**Имя** приложения отображает его описание конечным пользователям.</span><span class="sxs-lookup"><span data-stu-id="f3d12-133">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="f3d12-134">**Uri перенаправления** представляет собой комбинацию схемы и строки, которую Azure AD будет использовать для возврата ответов на маркеры.</span><span class="sxs-lookup"><span data-stu-id="f3d12-134">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="f3d12-135">Введите значение заполнителя, например, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="f3d12-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="f3d12-136">Это значение мы заменим позже.</span><span class="sxs-lookup"><span data-stu-id="f3d12-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="f3d12-137">После завершения регистрации служба Azure AD присваивает приложению уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="f3d12-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="f3d12-138">Это значение вам понадобится в следующих разделах, поэтому скопируйте его с вкладки приложения.</span><span class="sxs-lookup"><span data-stu-id="f3d12-138">You’ll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="f3d12-139">На странице **Параметры** выберите **Необходимые разрешения** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f3d12-139">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="f3d12-140">Выберите **Microsoft Graph** в качестве интерфейса API и добавьте разрешение **Чтение данных каталога** в списке **Делегированные разрешения**.</span><span class="sxs-lookup"><span data-stu-id="f3d12-140">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="f3d12-141">Это позволит приложению запрашивать интерфейс Graph API для пользователей.</span><span class="sxs-lookup"><span data-stu-id="f3d12-141">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="f3d12-142">2) Установка и настройка ADAL</span><span class="sxs-lookup"><span data-stu-id="f3d12-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="f3d12-143">Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="f3d12-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="f3d12-144">Чтобы ADAL могла обмениваться информацией с Azure AD, необходимо предоставить некоторую информацию о регистрации вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f3d12-144">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="f3d12-145">Сначала добавьте ADAL в проект DirectorySearcher с помощью консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="f3d12-145">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="f3d12-146">В проекте DirectorySearcher откройте `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="f3d12-146">In the DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="f3d12-147">Замените значения в разделе `Config Values` , чтобы отразить значения, введенные на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f3d12-147">Replace the values in the `Config Values` region to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="f3d12-148">Ваш код будет ссылаться на эти значения при каждом использовании ADAL.</span><span class="sxs-lookup"><span data-stu-id="f3d12-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="f3d12-149">`tenant` — это домен вашего клиента Azure AD, например contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="f3d12-149">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="f3d12-150">`clientId` — это идентификатор clientId приложения, скопированный с портала.</span><span class="sxs-lookup"><span data-stu-id="f3d12-150">The `clientId` is the clientId of your application you copied from the portal.</span></span>
* <span data-ttu-id="f3d12-151">Теперь необходимо обнаружить uri обратного вызова для вашего приложения Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="f3d12-151">You now need to discover the callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="f3d12-152">Установите точку останова в этой строке в методе `MainPage` :</span><span class="sxs-lookup"><span data-stu-id="f3d12-152">Set a breakpoint on this line in the `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="f3d12-153">Запустите приложение и скопируйте значение `redirectUri` при попадании в точку останова.</span><span class="sxs-lookup"><span data-stu-id="f3d12-153">Run the app, and copy aside the value of `redirectUri` when the breakpoint is hit.</span></span>  <span data-ttu-id="f3d12-154">Оно должно иметь примерно следующий вид:</span><span class="sxs-lookup"><span data-stu-id="f3d12-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="f3d12-155">Вернитесь на вкладку **Настройка** своего приложения на портале управления Azure и вместо значения **RedirectUri** введите скопированное значение.</span><span class="sxs-lookup"><span data-stu-id="f3d12-155">Back on the **Configure** tab of your application in the Azure Management Portal, replace the value of the **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="f3d12-156">3. Использование библиотеки ADAL для получения маркеров из AAD</span><span class="sxs-lookup"><span data-stu-id="f3d12-156">3. Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="f3d12-157">Основной принцип ADAL состоит в следующем: каждый раз, когда вашему приложению необходим маркер доступа, оно будет просто вызывать `authContext.AcquireToken(…)`, а ADAL сделает все остальное.</span><span class="sxs-lookup"><span data-stu-id="f3d12-157">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="f3d12-158">Первый шаг состоит в инициализации `AuthenticationContext` приложения, что является основным классом ADAL.</span><span class="sxs-lookup"><span data-stu-id="f3d12-158">The first step is to initialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="f3d12-159">Здесь вы отправляете в ADAL координаты, которые ему требуются для взаимодействия с Azure AD, и сообщаете о способе кэширования маркеров.</span><span class="sxs-lookup"><span data-stu-id="f3d12-159">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="f3d12-160">Теперь найдите метод `Search(...)` , который будет вызываться при нажатии кнопки "Поиск" в пользовательском интерфейсе приложения.</span><span class="sxs-lookup"><span data-stu-id="f3d12-160">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="f3d12-161">Этот метод выполняет запрос GET в интерфейс Graph API службы Azure AD для запроса списка пользователей, чьи UPN начинаются с данного слова поиска.</span><span class="sxs-lookup"><span data-stu-id="f3d12-161">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="f3d12-162">Но для отправки запросов в Graph API необходимо включить access_token в заголовок `Authorization` запроса — именно отсюда ADAL начинает свою работу.</span><span class="sxs-lookup"><span data-stu-id="f3d12-162">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try to get a token without triggering any user prompt.
    // ADAL will check whether the requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained the QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="f3d12-163">Если требуется интерактивная проверка подлинности, для отображения страницы входа в Azure AD ADAL будет использовать брокер веб-проверки подлинности (WAB) приложения Windows Phone и [модель продолжения](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) .</span><span class="sxs-lookup"><span data-stu-id="f3d12-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) to display the Azure AD sign in page.</span></span>  <span data-ttu-id="f3d12-164">При входе пользователя приложение должно отправлять в ADAL результаты взаимодействия с WAB.</span><span class="sxs-lookup"><span data-stu-id="f3d12-164">When the user signs in, your app needs to pass ADAL the results of the WAB interaction.</span></span>  <span data-ttu-id="f3d12-165">Это простая процедура, идентичная реализации интерфейса `ContinueWebAuthentication` :</span><span class="sxs-lookup"><span data-stu-id="f3d12-165">This is as simple as implementing the `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when the application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass the authentication interaction results to ADAL, which will
    // conclude the token acquisition operation and invoke the callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="f3d12-166">Теперь настало время использовать `AuthenticationResult` , которое ADAL вернуло в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="f3d12-166">Now it's time to use the `AuthenticationResult` that ADAL returned to your app.</span></span>  <span data-ttu-id="f3d12-167">В обратном вызове `QueryGraph(...)` включите полученный маркер access_token в запрос GET в заголовке авторизации:</span><span class="sxs-lookup"><span data-stu-id="f3d12-167">In the `QueryGraph(...)` callback, attach the access_token you acquired to the GET request in the Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add the access token to the Authorization Header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="f3d12-168">Для отображения сведений о пользователе в вашем приложении также можно использовать объект `AuthenticationResult` .</span><span class="sxs-lookup"><span data-stu-id="f3d12-168">You can also use the `AuthenticationResult` object to display information about the user in your app.</span></span> <span data-ttu-id="f3d12-169">В методе `QueryGraph(...)` используйте результат для отображения на странице идентификатора пользователя:</span><span class="sxs-lookup"><span data-stu-id="f3d12-169">In the `QueryGraph(...)` method, use the result to show the user's id on the page:</span></span>

```C#
// Update the Page UI to represent the signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="f3d12-170">Наконец, для выхода пользователя из приложения также можно использовать ADAL.</span><span class="sxs-lookup"><span data-stu-id="f3d12-170">Finally, you can use ADAL to sign the user out of hte application as well.</span></span>  <span data-ttu-id="f3d12-171">Когда пользователь нажимает кнопку "Выход", необходимо убедиться, что при следующем вызове `AcquireTokenSilentAsync(...)` произойдет сбой.</span><span class="sxs-lookup"><span data-stu-id="f3d12-171">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="f3d12-172">Благодаря применению ADAL это будет так же просто, как и очистка кэша маркера:</span><span class="sxs-lookup"><span data-stu-id="f3d12-172">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from the token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="f3d12-173">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="f3d12-173">Congratulations!</span></span> <span data-ttu-id="f3d12-174">Теперь у нас есть рабочее приложение Windows Phone, которое позволяет проверять подлинность пользователей, безопасно вызывать веб-интерфейсы API с помощью OAuth 2.0 и получать основные сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="f3d12-174">You now have a working Windows Phone app that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="f3d12-175">Если вы это еще не сделали, сейчас можно добавить несколько пользователей вашему клиенту.</span><span class="sxs-lookup"><span data-stu-id="f3d12-175">If you haven’t already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="f3d12-176">Запустите свое приложение DirectorySearcher и войдите под именем одного из таких пользователей.</span><span class="sxs-lookup"><span data-stu-id="f3d12-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="f3d12-177">Осуществите поиск других пользователей по их имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="f3d12-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="f3d12-178">Закройте приложение и снова его запустите.</span><span class="sxs-lookup"><span data-stu-id="f3d12-178">Close the app, and re-run it.</span></span>  <span data-ttu-id="f3d12-179">Обратите внимание на то, что пользовательский сеанс не изменяется.</span><span class="sxs-lookup"><span data-stu-id="f3d12-179">Notice how the user’s session remains intact.</span></span>  <span data-ttu-id="f3d12-180">Выйдите и снова войдите под именем другого пользователя.</span><span class="sxs-lookup"><span data-stu-id="f3d12-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="f3d12-181">ADAL упрощает процесс включения всех этих общих возможностей идентификации в приложение.</span><span class="sxs-lookup"><span data-stu-id="f3d12-181">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="f3d12-182">Он отвечает за всю грязную работу: управление кэшем, поддержку протокола OAuth, предоставление пользователю пользовательского интерфейса для входа, обновление истекших маркеров и многое другое.</span><span class="sxs-lookup"><span data-stu-id="f3d12-182">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="f3d12-183">Все, что вам действительно нужно знать, — это вызов интерфейса API `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="f3d12-183">All you really need to know is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="f3d12-184">Для справки следует отметить, что готовый пример (без ваших значений конфигурации) находится [здесь](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f3d12-184">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="f3d12-185">Теперь можно приступить к дополнительным сценариям идентификации.</span><span class="sxs-lookup"><span data-stu-id="f3d12-185">You can now move on to additional identity scenarios.</span></span>  <span data-ttu-id="f3d12-186">Можно попробовать:</span><span class="sxs-lookup"><span data-stu-id="f3d12-186">You may want to try:</span></span>

[<span data-ttu-id="f3d12-187">Защита веб-API с помощью Azure AD для .NET >></span><span class="sxs-lookup"><span data-stu-id="f3d12-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

