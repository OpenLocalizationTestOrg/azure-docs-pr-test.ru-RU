---
title: "Приступая к работе AD Xamarin aaaAzure | Документы Microsoft"
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
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="e015b-103">Интеграция Azure AD с приложениями Xamarin</span><span class="sxs-lookup"><span data-stu-id="e015b-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="e015b-104">Среда Xamarin позволяет создавать мобильные приложения на C#, которые могут работать в iOS, Android и Windows (на мобильных устройствах и ПК).</span><span class="sxs-lookup"><span data-stu-id="e015b-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="e015b-105">При создании приложения с помощью Xamarin Azure Active Directory (Azure AD) позволяет пользователям простой tooauthenticate с их учетными записями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e015b-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple tooauthenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="e015b-106">приложение Hello может безопасно использовать любой веб-API, защищенные Azure AD, например hello API Office 365 или hello Azure API.</span><span class="sxs-lookup"><span data-stu-id="e015b-106">hello app can also securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="e015b-107">Для приложений Xamarin, требуется tooaccess защищенных ресурсов Azure AD предоставляет hello библиотеку проверки подлинности Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="e015b-107">For Xamarin apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="e015b-108">Цель Hello ADAL — toomake легко и маркеры доступа tooget приложений.</span><span class="sxs-lookup"><span data-stu-id="e015b-108">hello sole purpose of ADAL is toomake it easy for apps tooget access tokens.</span></span> <span data-ttu-id="e015b-109">Это, в этой статье показано, как просто toodemonstrate как toobuild DirectorySearcher приложений:</span><span class="sxs-lookup"><span data-stu-id="e015b-109">toodemonstrate how easy it is, this article shows how toobuild DirectorySearcher apps that:</span></span>

* <span data-ttu-id="e015b-110">выполняются в iOS, Android, Windows Desktop, Windows Phone и Магазине Windows;</span><span class="sxs-lookup"><span data-stu-id="e015b-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="e015b-111">Используйте отдельный класс переносимой библиотеки tooauthenticate пользователей и получить маркеры для hello API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="e015b-111">Use a single portable class library (PCL) tooauthenticate users and get tokens for hello Azure AD Graph API.</span></span>
* <span data-ttu-id="e015b-112">осуществляют поиск пользователей в каталоге с помощью заданного имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="e015b-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="e015b-113">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="e015b-113">Before you get started</span></span>
* <span data-ttu-id="e015b-114">Загрузите hello [проект](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), или загрузить hello [полного примера](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="e015b-114">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="e015b-115">Каждая из этих загрузок является решением Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="e015b-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="e015b-116">Необходимо также клиент Azure AD в toocreate пользователей и зарегистрировать приложение hello.</span><span class="sxs-lookup"><span data-stu-id="e015b-116">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="e015b-117">Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="e015b-117">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="e015b-118">Когда будете готовы, выполните процедуры hello в hello рядом в четырех разделах.</span><span class="sxs-lookup"><span data-stu-id="e015b-118">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="e015b-119">Шаг 1. Настройка среды разработки Xamarin</span><span class="sxs-lookup"><span data-stu-id="e015b-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="e015b-120">Это руководство содержит проекты для iOS, Android и Windows, поэтому вам потребуются Visual Studio и Xamarin.</span><span class="sxs-lookup"><span data-stu-id="e015b-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="e015b-121">toocreate hello необходимые среде процесс завершения hello в [задать Настройка и установка Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="e015b-121">toocreate hello necessary environment, complete hello process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="e015b-122">Hello инструкциях содержатся материалы, вы можете просмотреть дополнительные сведения о Xamarin toolearn во время ожидания для завершения toobe установок hello.</span><span class="sxs-lookup"><span data-stu-id="e015b-122">hello instructions include material that you can review toolearn more about Xamarin while you're waiting for hello installations toobe completed.</span></span>

<span data-ttu-id="e015b-123">После завершения установки hello, откройте hello решение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e015b-123">After you've completed hello setup, open hello solution in Visual Studio.</span></span> <span data-ttu-id="e015b-124">Вы увидите шесть проектов: пять проектов для конкретной платформы и одну переносимую библиотеку классов DirectorySearcher.cs, которая будет общей для всех платформ.</span><span class="sxs-lookup"><span data-stu-id="e015b-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-hello-directorysearcher-app"></a><span data-ttu-id="e015b-125">Шаг 2: Регистрация приложения hello DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="e015b-125">Step 2: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="e015b-126">токены tooget приложения hello tooenable, необходимо сначала tooregister его в Azure AD для клиента и предоставить ему разрешение tooaccess hello API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="e015b-126">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="e015b-127">Этот процесс описывается далее.</span><span class="sxs-lookup"><span data-stu-id="e015b-127">Here's how:</span></span>

1. <span data-ttu-id="e015b-128">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e015b-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e015b-129">На верхней панели hello выберите свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="e015b-129">On hello top bar, click your account.</span></span> <span data-ttu-id="e015b-130">После этого в разделе hello **каталога** список, клиент Active Directory hello выберите нужное приложение hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="e015b-130">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="e015b-131">Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e015b-131">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="e015b-132">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e015b-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="e015b-133">toocreate новый **собственное клиентское приложение**, следуйте инструкциям hello.</span><span class="sxs-lookup"><span data-stu-id="e015b-133">toocreate a new **Native Client Application**, follow hello prompts.</span></span>
  * <span data-ttu-id="e015b-134">**Имя** описывает toousers приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e015b-134">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="e015b-135">**URI перенаправления** представляет собой комбинацию схему и строки, Azure AD использует tooreturn маркера ответов.</span><span class="sxs-lookup"><span data-stu-id="e015b-135">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="e015b-136">Введите значение (например, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="e015b-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="e015b-137">После завершения регистрации Azure AD присваивает приложение hello уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="e015b-137">After you’ve completed registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="e015b-138">Скопируйте значение hello из hello **приложения** вкладки, так как он потребуется позже.</span><span class="sxs-lookup"><span data-stu-id="e015b-138">Copy hello value from hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="e015b-139">На hello **параметры** выберите **требуемые разрешения**, а затем выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="e015b-139">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="e015b-140">Выберите **Microsoft Graph** как hello API.</span><span class="sxs-lookup"><span data-stu-id="e015b-140">Select **Microsoft Graph** as hello API.</span></span> <span data-ttu-id="e015b-141">В разделе **делегированные разрешения**, добавить hello **чтение данных каталога** разрешение.</span><span class="sxs-lookup"><span data-stu-id="e015b-141">Under **Delegated Permissions**, add hello **Read Directory Data** permission.</span></span>  
<span data-ttu-id="e015b-142">Это действие активирует приложение hello tooquery hello Graph API для пользователей.</span><span class="sxs-lookup"><span data-stu-id="e015b-142">This action enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="e015b-143">Шаг 3. Установка и настройка ADAL</span><span class="sxs-lookup"><span data-stu-id="e015b-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="e015b-144">Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="e015b-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="e015b-145">ADAL toocommunicate tooenable с Azure AD, ей следует присвоить некоторые сведения о регистрации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e015b-145">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="e015b-146">Добавьте проект DirectorySearcher ADAL toohello с помощью консоли диспетчера пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="e015b-146">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

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

    <span data-ttu-id="e015b-147">Обратите внимание, что две ссылки на библиотеки добавлены tooeach проекта: hello PCL часть ADAL и часть, специфический для платформы.</span><span class="sxs-lookup"><span data-stu-id="e015b-147">Note that two library references are added tooeach project: hello PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="e015b-148">В проекте DirectorySearcherLib hello откройте DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="e015b-148">In hello DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="e015b-149">Замените значения членов класса hello hello значениями, указанными в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e015b-149">Replace hello class member values with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="e015b-150">Ваш код ссылается toothese значений при каждом использовании ADAL.</span><span class="sxs-lookup"><span data-stu-id="e015b-150">Your code refers toothese values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="e015b-151">Hello *клиента* hello домен вашего клиента Azure AD (например, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="e015b-151">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="e015b-152">Hello *clientId* — hello идентификатор клиента приложения hello, который копируется из портала hello.</span><span class="sxs-lookup"><span data-stu-id="e015b-152">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
  * <span data-ttu-id="e015b-153">Hello *returnUri* hello перенаправления URI, введенное на портале hello (например, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="e015b-153">hello *returnUri* is hello redirect URI that you entered in hello portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="e015b-154">Шаг 4: Используйте ADAL tooget токены из Azure AD</span><span class="sxs-lookup"><span data-stu-id="e015b-154">Step 4: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="e015b-155">Большая часть логики проверки подлинности приложение hello заключается в `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="e015b-155">Almost all of hello app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="e015b-156">Все, что является необходимым в проекты под конкретные платформы hello — toopass toohello параметра `DirectorySearcher` PCL.</span><span class="sxs-lookup"><span data-stu-id="e015b-156">All that's necessary in hello platform-specific projects is toopass a contextual parameter toohello `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="e015b-157">Откройте DirectorySearcher.cs, а затем добавьте новый параметр toohello `SearchByAlias(...)` метод.</span><span class="sxs-lookup"><span data-stu-id="e015b-157">Open DirectorySearcher.cs, and then add a new parameter toohello `SearchByAlias(...)` method.</span></span> <span data-ttu-id="e015b-158">`IPlatformParameters`является hello параметра, инкапсулирующий hello платформой объекты, что проверка подлинности ADAL потребности tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="e015b-158">`IPlatformParameters` is hello contextual parameter that encapsulates hello platform-specific objects that ADAL needs tooperform hello authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="e015b-159">Инициализировать `AuthenticationContext`, который является основной класс hello объекта ADAL.</span><span class="sxs-lookup"><span data-stu-id="e015b-159">Initialize `AuthenticationContext`, which is hello primary class of ADAL.</span></span>  
<span data-ttu-id="e015b-160">Это ADAL hello передает действие координат его toocommunicate потребности в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e015b-160">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD.</span></span>
3. <span data-ttu-id="e015b-161">Вызовите `AcquireTokenAsync(...)`, который принимает hello `IPlatformParameters` объекта и вызывает hello поток проверки подлинности, необходимые tooreturn приложения маркера toohello.</span><span class="sxs-lookup"><span data-stu-id="e015b-161">Call `AcquireTokenAsync(...)`, which accepts hello `IPlatformParameters` object and invokes hello authentication flow that's necessary tooreturn a token toohello app.</span></span>

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

    <span data-ttu-id="e015b-162">`AcquireTokenAsync(...)`Первый tooreturn попыток маркер для hello запрашиваемый ресурс (hello Graph API в данном случае) без запроса учетных данных (через кэширование или обновление старых токены) tooenter пользователей.</span><span class="sxs-lookup"><span data-stu-id="e015b-162">`AcquireTokenAsync(...)` first attempts tooreturn a token for hello requested resource (hello Graph API in this case) without prompting users tooenter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="e015b-163">При необходимости он показывает пользователей hello Azure AD на странице входа перед установкой hello запрошенного токена.</span><span class="sxs-lookup"><span data-stu-id="e015b-163">As necessary, it shows users hello Azure AD sign-in page before acquiring hello requested token.</span></span>
4. <span data-ttu-id="e015b-164">Присоединение hello запрос Graph API toohello токена доступа в hello **авторизации** заголовка:</span><span class="sxs-lookup"><span data-stu-id="e015b-164">Attach hello access token toohello Graph API request in hello **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="e015b-165">Вот и все для hello `DirectorySearcher` PCL и hello код приложения связанные с идентификаторами.</span><span class="sxs-lookup"><span data-stu-id="e015b-165">That's all for hello `DirectorySearcher` PCL and hello app's identity-related code.</span></span> <span data-ttu-id="e015b-166">Осталось toocall hello `SearchByAlias(...)` метод в представлениях для каждой платформы и, при необходимости, tooadd кода для правильной обработки hello жизненного цикла пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e015b-166">All that remains is toocall hello `SearchByAlias(...)` method in each platform's views and, where necessary, tooadd code for correctly handling hello UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="e015b-167">Android</span><span class="sxs-lookup"><span data-stu-id="e015b-167">Android</span></span>
1. <span data-ttu-id="e015b-168">В MainActivity.cs, добавьте вызов слишком`SearchByAlias(...)` обработчика щелчка кнопки hello:</span><span class="sxs-lookup"><span data-stu-id="e015b-168">In MainActivity.cs, add a call too`SearchByAlias(...)` in hello button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="e015b-169">Переопределить hello `OnActivityResult` tooforward жизненного цикла метод проверки подлинности перенаправляет задней toohello соответствующий метод.</span><span class="sxs-lookup"><span data-stu-id="e015b-169">Override hello `OnActivityResult` lifecycle method tooforward any authentication redirects back toohello appropriate method.</span></span> <span data-ttu-id="e015b-170">Для этого ADAL предоставляет вспомогательный метод в Android:</span><span class="sxs-lookup"><span data-stu-id="e015b-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="e015b-171">Классические приложения</span><span class="sxs-lookup"><span data-stu-id="e015b-171">Windows Desktop</span></span>
<span data-ttu-id="e015b-172">В MainWindow.xaml.cs звонок слишком`SearchByAlias(...)` , передав `WindowInteropHelper` в hello desktop `PlatformParameters` объекта:</span><span class="sxs-lookup"><span data-stu-id="e015b-172">In MainWindow.xaml.cs, make a call too`SearchByAlias(...)` by passing a `WindowInteropHelper` in hello desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="e015b-173">iOS</span><span class="sxs-lookup"><span data-stu-id="e015b-173">iOS</span></span>
<span data-ttu-id="e015b-174">Здравствуйте, операций ввода-вывода в DirSearchClient_iOSViewController.cs, `PlatformParameters` объект принимает ссылку toohello View Controller:</span><span class="sxs-lookup"><span data-stu-id="e015b-174">In DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` object takes a reference toohello View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="e015b-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="e015b-175">Windows Universal</span></span>
<span data-ttu-id="e015b-176">В универсальное приложение для Windows, откройте файл MainPage.xaml.cs, а затем реализуйте hello `Search` метод.</span><span class="sxs-lookup"><span data-stu-id="e015b-176">In Windows Universal, open MainPage.xaml.cs, and then implement hello `Search` method.</span></span> <span data-ttu-id="e015b-177">Этот метод использует вспомогательный метод в общий проект tooupdate пользовательского интерфейса, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="e015b-177">This method uses a helper method in a shared project tooupdate UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="e015b-178">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="e015b-178">What's next</span></span>
<span data-ttu-id="e015b-179">Теперь у нас есть рабочее приложение Xamarin, которое позволяет проверять подлинность пользователей и безопасным образом вызывать веб-интерфейсы API с помощью OAuth 2.0 на пяти различных платформах.</span><span class="sxs-lookup"><span data-stu-id="e015b-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="e015b-180">Если уже еще не заполнены вашего клиента с пользователями, пришло время toodo hello таким образом.</span><span class="sxs-lookup"><span data-stu-id="e015b-180">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>

1. <span data-ttu-id="e015b-181">Запуск приложения DirectorySearcher и затем войдите с помощью одного из пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="e015b-181">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="e015b-182">Осуществите поиск других пользователей по их имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="e015b-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="e015b-183">ADAL упрощает легко tooincorporate общие функции управления удостоверениями в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="e015b-183">ADAL makes it easy tooincorporate common identity features into hello app.</span></span> <span data-ttu-id="e015b-184">Он отвечает за всю работу dirty hello, например для управления кэшем, поддержка протокола OAuth, предоставляя hello пользователя с именем входа пользовательского интерфейса, и обновление истек срок действия маркеров.</span><span class="sxs-lookup"><span data-stu-id="e015b-184">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="e015b-185">Необходим вызов tooknow только один API-Интерфейс `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="e015b-185">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="e015b-186">Для справки, загрузить hello [полного примера](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (без настройки).</span><span class="sxs-lookup"><span data-stu-id="e015b-186">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="e015b-187">Теперь можно переходить на сценариях tooadditional удостоверений.</span><span class="sxs-lookup"><span data-stu-id="e015b-187">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="e015b-188">Например, попробуйте использовать [защиту веб-API для .NET с помощью Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e015b-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
