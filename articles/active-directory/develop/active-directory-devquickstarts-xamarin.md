---
title: "Приступая к работе с Xamarin Azure AD | Документация Майкрософт"
description: "Создание приложений Xamarin, которые интегрируются с Azure AD для входа в систему и вызывают программные интерфейсы, защищенные Azure AD, с помощью OAuth."
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 54ee403f283bc5dc79911e2e813dd513ff595828
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="f84ef-103">Интеграция Azure AD с приложениями Xamarin</span><span class="sxs-lookup"><span data-stu-id="f84ef-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="f84ef-104">Среда Xamarin позволяет создавать мобильные приложения на C#, которые могут работать в iOS, Android и Windows (на мобильных устройствах и ПК).</span><span class="sxs-lookup"><span data-stu-id="f84ef-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="f84ef-105">При разработке приложения с помощью Xamarin служба Azure Active Directory (Azure AD) позволяет легко и просто осуществлять проверку подлинности пользователей с помощью их учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f84ef-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple to authenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="f84ef-106">Кроме того, приложение может безопасно использовать любые веб-интерфейсы API, защищаемые с помощью Azure AD, например API-интерфейсы Office 365 или Azure.</span><span class="sxs-lookup"><span data-stu-id="f84ef-106">The app can also securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="f84ef-107">Для приложений Xamarin, которым требуется доступ к защищенным ресурсам, Azure AD предоставляет библиотеку проверки подлинности Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="f84ef-107">For Xamarin apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="f84ef-108">Единственное предназначение ADAL — упростить процесс получения маркеров доступа.</span><span class="sxs-lookup"><span data-stu-id="f84ef-108">The sole purpose of ADAL is to make it easy for apps to get access tokens.</span></span> <span data-ttu-id="f84ef-109">В этой статье показано, насколько это легко, на примере создания приложений DirectorySearcher, которые обладают следующими преимуществами:</span><span class="sxs-lookup"><span data-stu-id="f84ef-109">To demonstrate how easy it is, this article shows how to build DirectorySearcher apps that:</span></span>

* <span data-ttu-id="f84ef-110">выполняются в iOS, Android, Windows Desktop, Windows Phone и Магазине Windows;</span><span class="sxs-lookup"><span data-stu-id="f84ef-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="f84ef-111">используют единую переносимую библиотеку классов (PCL) для проверки подлинности пользователей и получения маркеров для интерфейса API Graph в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f84ef-111">Use a single portable class library (PCL) to authenticate users and get tokens for the Azure AD Graph API.</span></span>
* <span data-ttu-id="f84ef-112">осуществляют поиск пользователей в каталоге с помощью заданного имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="f84ef-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="f84ef-113">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="f84ef-113">Before you get started</span></span>
* <span data-ttu-id="f84ef-114">Скачайте [схему проекта](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip) или [готовый пример](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f84ef-114">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="f84ef-115">Каждая из этих загрузок является решением Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="f84ef-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="f84ef-116">Вам также необходим клиент Azure AD для создания пользователей и регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="f84ef-116">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="f84ef-117">Если клиента нет, [узнайте, как его получить](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="f84ef-117">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="f84ef-118">Когда будете готовы, выполните процедуры, описанные в следующих четырех разделах.</span><span class="sxs-lookup"><span data-stu-id="f84ef-118">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="f84ef-119">Шаг 1. Настройка среды разработки Xamarin</span><span class="sxs-lookup"><span data-stu-id="f84ef-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="f84ef-120">Это руководство содержит проекты для iOS, Android и Windows, поэтому вам потребуются Visual Studio и Xamarin.</span><span class="sxs-lookup"><span data-stu-id="f84ef-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="f84ef-121">Для создания необходимой среды следуйте инструкциям в разделе [Настройка и установка](https://msdn.microsoft.com/library/mt613162.aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="f84ef-121">To create the necessary environment, complete the process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="f84ef-122">Эти инструкции содержат материалы, которые можно просмотреть, чтобы больше узнать о Xamarin, пока вы ожидаете завершения процессов установки.</span><span class="sxs-lookup"><span data-stu-id="f84ef-122">The instructions include material that you can review to learn more about Xamarin while you're waiting for the installations to be completed.</span></span>

<span data-ttu-id="f84ef-123">После завершения настройки откройте решение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f84ef-123">After you've completed the setup, open the solution in Visual Studio.</span></span> <span data-ttu-id="f84ef-124">Вы увидите шесть проектов: пять проектов для конкретной платформы и одну переносимую библиотеку классов DirectorySearcher.cs, которая будет общей для всех платформ.</span><span class="sxs-lookup"><span data-stu-id="f84ef-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-the-directorysearcher-app"></a><span data-ttu-id="f84ef-125">Шаг 2. Регистрация приложения DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="f84ef-125">Step 2: Register the DirectorySearcher app</span></span>
<span data-ttu-id="f84ef-126">Чтобы приложение могло получать маркеры, сначала необходимо его зарегистрировать в клиенте Azure AD и предоставить ему разрешение на доступ к интерфейсу API Graph для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f84ef-126">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="f84ef-127">Этот процесс описывается далее.</span><span class="sxs-lookup"><span data-stu-id="f84ef-127">Here's how:</span></span>

1. <span data-ttu-id="f84ef-128">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f84ef-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f84ef-129">На верхней панели щелкните свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="f84ef-129">On the top bar, click your account.</span></span> <span data-ttu-id="f84ef-130">Затем в списке **Каталог** выберите клиент Active Directory для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="f84ef-130">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="f84ef-131">В области слева щелкните **Больше служб** и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f84ef-131">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="f84ef-132">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f84ef-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="f84ef-133">Следуйте инструкциям на экране, чтобы создать **собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="f84ef-133">To create a new **Native Client Application**, follow the prompts.</span></span>
  * <span data-ttu-id="f84ef-134">**Имя** — описание приложения для пользователей.</span><span class="sxs-lookup"><span data-stu-id="f84ef-134">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="f84ef-135">**URI перенаправления** представляет собой сочетание схемы и строки, используемое Azure AD для возвращения ответов маркеров.</span><span class="sxs-lookup"><span data-stu-id="f84ef-135">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="f84ef-136">Введите значение (например, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="f84ef-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="f84ef-137">После завершения регистрации Azure AD присваивает приложению уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="f84ef-137">After you’ve completed registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="f84ef-138">Скопируйте значение на вкладке **Приложение**. Оно потребуется вам позже.</span><span class="sxs-lookup"><span data-stu-id="f84ef-138">Copy the value from the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="f84ef-139">На странице **Параметры** выберите **Необходимые разрешения** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f84ef-139">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="f84ef-140">Выберите API **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="f84ef-140">Select **Microsoft Graph** as the API.</span></span> <span data-ttu-id="f84ef-141">В разделе **Делегированные разрешения** добавьте разрешение **Чтение данных каталога**.</span><span class="sxs-lookup"><span data-stu-id="f84ef-141">Under **Delegated Permissions**, add the **Read Directory Data** permission.</span></span>  
<span data-ttu-id="f84ef-142">Это действие позволяет приложению отправлять запросы в API Graph для пользователей.</span><span class="sxs-lookup"><span data-stu-id="f84ef-142">This action enables the app to query the Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="f84ef-143">Шаг 3. Установка и настройка ADAL</span><span class="sxs-lookup"><span data-stu-id="f84ef-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="f84ef-144">Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="f84ef-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="f84ef-145">Чтобы обеспечить взаимодействие библиотеки ADAL с Azure AD, необходимо указать определенные сведения о регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="f84ef-145">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="f84ef-146">Добавьте ADAL в проект DirectorySearcher с помощью консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="f84ef-146">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    <span data-ttu-id="f84ef-147">Обратите внимание, что в каждый проект добавляются две ссылки на библиотеку: часть PCL в ADAL и специфическая для платформы часть.</span><span class="sxs-lookup"><span data-stu-id="f84ef-147">Note that two library references are added to each project: the PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="f84ef-148">В проекте DirectorySearcherLib откройте файл DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="f84ef-148">In the DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="f84ef-149">Замените значения членов класса значениями, введенными на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f84ef-149">Replace the class member values with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="f84ef-150">Ваш код будет ссылаться на эти значения при каждом использовании ADAL.</span><span class="sxs-lookup"><span data-stu-id="f84ef-150">Your code refers to these values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="f84ef-151">*tenant* — это домен вашего клиента Azure AD (например, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="f84ef-151">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="f84ef-152">*clientId* — идентификатор клиента приложения, скопированный с портала.</span><span class="sxs-lookup"><span data-stu-id="f84ef-152">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
  * <span data-ttu-id="f84ef-153">*returnUri* — URI перенаправления, который вы указали на портале (например, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="f84ef-153">The *returnUri* is the redirect URI that you entered in the portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="f84ef-154">Шаг 4. Использование ADAL для получения маркеров из Azure AD</span><span class="sxs-lookup"><span data-stu-id="f84ef-154">Step 4: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="f84ef-155">Практически вся логика для проверки подлинности приложения находится в `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="f84ef-155">Almost all of the app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="f84ef-156">Специфические для платформы проекты должны отправлять контекстный параметр в PCL `DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="f84ef-156">All that's necessary in the platform-specific projects is to pass a contextual parameter to the `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="f84ef-157">Откройте файл DirectorySearcher.cs, а затем добавьте новый параметр в метод `SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="f84ef-157">Open DirectorySearcher.cs, and then add a new parameter to the `SearchByAlias(...)` method.</span></span> <span data-ttu-id="f84ef-158">`IPlatformParameters` — это контекстный параметр, инкапсулирующий специфические для платформы объекты, которые нужны ADAL для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f84ef-158">`IPlatformParameters` is the contextual parameter that encapsulates the platform-specific objects that ADAL needs to perform the authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="f84ef-159">Инициализируйте `AuthenticationContext` — основной класс ADAL.</span><span class="sxs-lookup"><span data-stu-id="f84ef-159">Initialize `AuthenticationContext`, which is the primary class of ADAL.</span></span>  
<span data-ttu-id="f84ef-160">Это действие отправляет в библиотеку ADAL координаты, которые требуются ей для взаимодействия с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f84ef-160">This action passes ADAL the coordinates it needs to communicate with Azure AD.</span></span>
3. <span data-ttu-id="f84ef-161">Вызовите метод `AcquireTokenAsync(...)`, который принимает объект `IPlatformParameters` и будет вызывать последовательность проверки подлинности, необходимую для возврата маркера в приложение.</span><span class="sxs-lookup"><span data-stu-id="f84ef-161">Call `AcquireTokenAsync(...)`, which accepts the `IPlatformParameters` object and invokes the authentication flow that's necessary to return a token to the app.</span></span>

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    <span data-ttu-id="f84ef-162">`AcquireTokenAsync(...)` сначала попытается вернуть маркер для запрошенного ресурса (в данном случае API Graph) и не будет предлагать пользователю вводить учетные данные (путем кэширования или обновления старых маркеров).</span><span class="sxs-lookup"><span data-stu-id="f84ef-162">`AcquireTokenAsync(...)` first attempts to return a token for the requested resource (the Graph API in this case) without prompting users to enter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="f84ef-163">При необходимости перед получением запрошенного маркера для пользователя отображается страница входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f84ef-163">As necessary, it shows users the Azure AD sign-in page before acquiring the requested token.</span></span>
4. <span data-ttu-id="f84ef-164">Присоедините маркер доступа к запросу API Graph в заголовке **авторизации**:</span><span class="sxs-lookup"><span data-stu-id="f84ef-164">Attach the access token to the Graph API request in the **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="f84ef-165">Это все, что нужно сделать для PCL `DirectorySearcher` и кода, связанного с удостоверением приложения.</span><span class="sxs-lookup"><span data-stu-id="f84ef-165">That's all for the `DirectorySearcher` PCL and the app's identity-related code.</span></span> <span data-ttu-id="f84ef-166">Остается только вызвать метод `SearchByAlias(...)` во всех представлениях для платформы и при необходимости добавить код для правильной обработки жизненного цикла пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f84ef-166">All that remains is to call the `SearchByAlias(...)` method in each platform's views and, where necessary, to add code for correctly handling the UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="f84ef-167">Android</span><span class="sxs-lookup"><span data-stu-id="f84ef-167">Android</span></span>
1. <span data-ttu-id="f84ef-168">В файле MainActivity.cs добавьте вызов в `SearchByAlias(...)` в обработчике нажатия кнопки:</span><span class="sxs-lookup"><span data-stu-id="f84ef-168">In MainActivity.cs, add a call to `SearchByAlias(...)` in the button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="f84ef-169">Переопределите метод жизненного цикла `OnActivityResult` для пересылки операций перенаправления проверки подлинности обратно в соответствующий метод.</span><span class="sxs-lookup"><span data-stu-id="f84ef-169">Override the `OnActivityResult` lifecycle method to forward any authentication redirects back to the appropriate method.</span></span> <span data-ttu-id="f84ef-170">Для этого ADAL предоставляет вспомогательный метод в Android:</span><span class="sxs-lookup"><span data-stu-id="f84ef-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="f84ef-171">Классические приложения</span><span class="sxs-lookup"><span data-stu-id="f84ef-171">Windows Desktop</span></span>
<span data-ttu-id="f84ef-172">В файле MainWindow.xaml.cs отправьте вызов в `SearchByAlias(...)`, передав `WindowInteropHelper` в объекте `PlatformParameters` классического приложения:</span><span class="sxs-lookup"><span data-stu-id="f84ef-172">In MainWindow.xaml.cs, make a call to `SearchByAlias(...)` by passing a `WindowInteropHelper` in the desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="f84ef-173">iOS</span><span class="sxs-lookup"><span data-stu-id="f84ef-173">iOS</span></span>
<span data-ttu-id="f84ef-174">В файле DirSearchClient_iOSViewController.cs объект iOS `PlatformParameters` принимает ссылку на контроллер представления:</span><span class="sxs-lookup"><span data-stu-id="f84ef-174">In DirSearchClient_iOSViewController.cs, the iOS `PlatformParameters` object takes a reference to the View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="f84ef-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="f84ef-175">Windows Universal</span></span>
<span data-ttu-id="f84ef-176">В универсальной платформе Windows откройте файл MainPage.xaml.cs, а затем реализуйте метод `Search`.</span><span class="sxs-lookup"><span data-stu-id="f84ef-176">In Windows Universal, open MainPage.xaml.cs, and then implement the `Search` method.</span></span> <span data-ttu-id="f84ef-177">Этот метод использует вспомогательный метод в общем проекте, чтобы обновлять пользовательский интерфейс при необходимости.</span><span class="sxs-lookup"><span data-stu-id="f84ef-177">This method uses a helper method in a shared project to update UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="f84ef-178">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="f84ef-178">What's next</span></span>
<span data-ttu-id="f84ef-179">Теперь у нас есть рабочее приложение Xamarin, которое позволяет проверять подлинность пользователей и безопасным образом вызывать веб-интерфейсы API с помощью OAuth 2.0 на пяти различных платформах.</span><span class="sxs-lookup"><span data-stu-id="f84ef-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="f84ef-180">Если в клиент еще не добавлены пользователи, сейчас самое время это сделать.</span><span class="sxs-lookup"><span data-stu-id="f84ef-180">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>

1. <span data-ttu-id="f84ef-181">Запустите приложение DirectorySearcher и войдите как один из пользователей.</span><span class="sxs-lookup"><span data-stu-id="f84ef-181">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="f84ef-182">Осуществите поиск других пользователей по их имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="f84ef-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="f84ef-183">ADAL упрощает процесс включения общих возможностей идентификации в приложение.</span><span class="sxs-lookup"><span data-stu-id="f84ef-183">ADAL makes it easy to incorporate common identity features into the app.</span></span> <span data-ttu-id="f84ef-184">Эта библиотека отвечает за всю "грязную работу": управление кэшем, поддержку протокола OAuth, предоставление пользователю пользовательского интерфейса для входа и обновление истекших маркеров.</span><span class="sxs-lookup"><span data-stu-id="f84ef-184">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="f84ef-185">Вам нужно знать только один вызов API — `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="f84ef-185">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="f84ef-186">Скачайте для справки [готовый пример](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (без ваших значений конфигурации).</span><span class="sxs-lookup"><span data-stu-id="f84ef-186">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="f84ef-187">Теперь можно приступить к дополнительным сценариям идентификации.</span><span class="sxs-lookup"><span data-stu-id="f84ef-187">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="f84ef-188">Например, попробуйте использовать [защиту веб-API для .NET с помощью Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f84ef-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
