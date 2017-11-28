---
title: "Приступая к работе магазина AD Windows aaaAzure | Документы Microsoft"
description: "Создание приложений Магазина Windows, которые интегрируются с Azure AD для входа в систему и вызывают интерфейсы API, защищенные Azure AD, с помощью OAuth."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="36dc6-103">Интеграция Azure AD с приложениями Магазина Windows</span><span class="sxs-lookup"><span data-stu-id="36dc6-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="36dc6-104">Проекты для Магазина Windows 8.1 и более ранних версий не поддерживаются в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="36dc6-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="36dc6-105">Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="36dc6-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="36dc6-106">При разработке приложений для магазина Windows hello, Azure Active Directory (Azure AD) упрощает простыми и понятными tooauthenticate пользователей с их учетными записями Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36dc6-106">If you're developing apps for hello Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward tooauthenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="36dc6-107">Путем интеграции с Azure AD, приложения могут безопасно использовать любой веб-API, который защищен службой Azure AD, например hello API Office 365 или hello Azure API.</span><span class="sxs-lookup"><span data-stu-id="36dc6-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="36dc6-108">Для классических приложений для магазина Windows, требующих tooaccess защищенные ресурсы Azure AD предоставляет hello библиотеку проверки подлинности Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="36dc6-108">For Windows Store desktop apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="36dc6-109">Цель Hello ADAL — toomake легко и маркеры доступа tooget приложения hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-109">hello sole purpose of ADAL is toomake it easy for hello app tooget access tokens.</span></span> <span data-ttu-id="36dc6-110">примеры, в этой статье показано, как toobuild DirectorySearcher Windows хранения toodemonstrate приложения:</span><span class="sxs-lookup"><span data-stu-id="36dc6-110">toodemonstrate how easy it is, this article shows how toobuild a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="36dc6-111">Получает маркеры для вызова API Azure AD Graph hello с помощью hello доступа [протокол проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="36dc6-111">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="36dc6-112">осуществляет поиск пользователей в каталоге с помощью заданного имени участника-пользователя (UPN);</span><span class="sxs-lookup"><span data-stu-id="36dc6-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="36dc6-113">Обеспечивает функцию выхода пользователя из приложения.</span><span class="sxs-lookup"><span data-stu-id="36dc6-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="36dc6-114">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="36dc6-114">Before you get started</span></span>
* <span data-ttu-id="36dc6-115">Загрузите hello [проект](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), или загрузить hello [полного примера](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="36dc6-115">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="36dc6-116">Каждая из этих загрузок является решением Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="36dc6-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="36dc6-117">Необходимо также клиент Azure AD в toocreate пользователей и зарегистрировать приложение hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-117">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="36dc6-118">Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="36dc6-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="36dc6-119">Когда будете готовы, выполните процедуры hello в hello следующих трех разделах.</span><span class="sxs-lookup"><span data-stu-id="36dc6-119">When you are ready, follow hello procedures in hello next three sections.</span></span>

## <a name="step-1-register-hello-directorysearcher-app"></a><span data-ttu-id="36dc6-120">Шаг 1: Регистрация приложения hello DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="36dc6-120">Step 1: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="36dc6-121">токены tooget приложения hello tooenable, необходимо сначала tooregister его в Azure AD для клиента и предоставить ему разрешение tooaccess hello API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="36dc6-121">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="36dc6-122">Этот процесс описывается далее.</span><span class="sxs-lookup"><span data-stu-id="36dc6-122">Here's how:</span></span>

1. <span data-ttu-id="36dc6-123">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36dc6-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="36dc6-124">На верхней панели hello выберите свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="36dc6-124">On hello top bar, click your account.</span></span> <span data-ttu-id="36dc6-125">После этого в разделе hello **каталога** список, клиент Active Directory hello выберите нужное приложение hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="36dc6-125">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="36dc6-126">Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36dc6-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="36dc6-127">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="36dc6-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="36dc6-128">Выполните запросы toocreate hello **собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="36dc6-128">Follow hello prompts toocreate a **Native Client Application**.</span></span>
  * <span data-ttu-id="36dc6-129">**Имя** описывает toousers приложения hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-129">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="36dc6-130">**URI перенаправления** представляет собой комбинацию схему и строки, Azure AD использует tooreturn маркера ответов.</span><span class="sxs-lookup"><span data-stu-id="36dc6-130">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="36dc6-131">Введите значение заполнителя (например, **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="36dc6-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="36dc6-132">Позже вы замените значение hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-132">You'll replace hello value later.</span></span>
6. <span data-ttu-id="36dc6-133">После завершения регистрации hello Azure AD присваивает приложение hello уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="36dc6-133">After you’ve completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="36dc6-134">Скопируйте значение hello на hello **приложения** вкладки, так как он потребуется позже.</span><span class="sxs-lookup"><span data-stu-id="36dc6-134">Copy hello value on hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="36dc6-135">На hello **параметры** выберите **требуемые разрешения**, а затем выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="36dc6-135">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="36dc6-136">Для hello **Azure Active Directory** приложения, выберите **Microsoft Graph** как hello API.</span><span class="sxs-lookup"><span data-stu-id="36dc6-136">For hello **Azure Active Directory** app, select **Microsoft Graph** as hello API.</span></span>
9. <span data-ttu-id="36dc6-137">В разделе **делегированные разрешения**, добавить hello **доступ к каталогу hello как пользователя, выполнившего вход hello** разрешение.</span><span class="sxs-lookup"><span data-stu-id="36dc6-137">Under **Delegated Permissions**, add hello **Access hello directory as hello signed-in user** permission.</span></span> <span data-ttu-id="36dc6-138">Таким образом приложение hello tooquery hello Graph API для пользователей.</span><span class="sxs-lookup"><span data-stu-id="36dc6-138">Doing so enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="36dc6-139">Шаг 2. Установка и настройка ADAL</span><span class="sxs-lookup"><span data-stu-id="36dc6-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="36dc6-140">Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="36dc6-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="36dc6-141">ADAL toocommunicate tooenable с Azure AD, ей следует присвоить некоторые сведения о регистрации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-141">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="36dc6-142">Добавьте проект DirectorySearcher ADAL toohello с помощью консоли диспетчера пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-142">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="36dc6-143">В проекте DirectorySearcher hello откройте файл MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="36dc6-143">In hello DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="36dc6-144">Замените значения hello hello **значения конфигурации** область со значениями hello, введенным в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="36dc6-144">Replace hello values in hello **Config Values** region with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="36dc6-145">Ваш код ссылается toothese значений при каждом использовании ADAL.</span><span class="sxs-lookup"><span data-stu-id="36dc6-145">Your code refers toothese values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="36dc6-146">Hello *клиента* hello домен вашего клиента Azure AD (например, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="36dc6-146">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="36dc6-147">Hello *clientId* — hello идентификатор клиента приложения hello, который копируется из портала hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-147">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
4. <span data-ttu-id="36dc6-148">Теперь необходимо toodiscover hello URI обратного вызова для приложения магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="36dc6-148">You now need toodiscover hello callback URI for your Windows Store app.</span></span> <span data-ttu-id="36dc6-149">Установите точку останова в этой строке в hello `MainPage` метод:</span><span class="sxs-lookup"><span data-stu-id="36dc6-149">Set a breakpoint on this line in hello `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="36dc6-150">Выполните сборку решения hello, убедившись, что будут восстановлены все ссылки на пакет.</span><span class="sxs-lookup"><span data-stu-id="36dc6-150">Build hello solution, making sure that all package references are restored.</span></span> <span data-ttu-id="36dc6-151">Если отсутствуют любых пакетов, откройте диспетчер пакетов NuGet hello и восстановить их.</span><span class="sxs-lookup"><span data-stu-id="36dc6-151">If any packages are missing, open hello NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="36dc6-152">Выполните приложение hello и скопируйте значение hello `redirectUri` при попадании в точку останова hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-152">Run hello app, and copy hello value of `redirectUri` when hello breakpoint is hit.</span></span> <span data-ttu-id="36dc6-153">значение Hello должен выглядеть примерно hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36dc6-153">hello value should look something like hello following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="36dc6-154">Включите hello **параметры** приложения hello в hello портал Azure, добавьте **RedirectUri** с предшествующей значение hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-154">Back on hello **Settings** tab of hello app in hello Azure portal, add a **RedirectUri** with hello preceding value.</span></span>  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="36dc6-155">Шаг 3: Используйте ADAL tooget токены из Azure AD</span><span class="sxs-lookup"><span data-stu-id="36dc6-155">Step 3: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="36dc6-156">Hello базовый принцип ADAL —, когда приложение hello требуется маркер доступа, он просто вызывает `authContext.AcquireToken(…)`, и ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="36dc6-156">hello basic principle behind ADAL is that whenever hello app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="36dc6-157">Инициализировать приложение hello `AuthenticationContext`, который является основной класс hello объекта ADAL.</span><span class="sxs-lookup"><span data-stu-id="36dc6-157">Initialize hello app’s `AuthenticationContext`, which is hello primary class of ADAL.</span></span> <span data-ttu-id="36dc6-158">Это действие передает ADAL hello координаты требуются toocommunicate с Azure AD и о том, как toocache маркеры.</span><span class="sxs-lookup"><span data-stu-id="36dc6-158">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="36dc6-159">Найдите hello `Search(...)` метод, который вызывается, когда пользователь щелкает hello **поиска** кнопку в пользовательском Интерфейсе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-159">Locate hello `Search(...)` method, which is invoked when users click hello **Search** button on hello app's UI.</span></span> <span data-ttu-id="36dc6-160">Этот метод делает tooquery toohello API Azure AD Graph запрос get для пользователей, имя участника-пользователя начинается с заданного условия поиска hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-160">This method makes a get request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span> <span data-ttu-id="36dc6-161">hello tooquery Graph API включают маркер доступа в запросе hello **авторизации** заголовок.</span><span class="sxs-lookup"><span data-stu-id="36dc6-161">tooquery hello Graph API, include an access token in hello request's **Authorization** header.</span></span> <span data-ttu-id="36dc6-162">Вот где может пригодиться ADAL.</span><span class="sxs-lookup"><span data-stu-id="36dc6-162">This is where ADAL comes in.</span></span>

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="36dc6-163">Когда приложение hello запрашивает маркер путем вызова `AcquireTokenAsync(...)`, ADAL пытается tooreturn маркер без запроса учетных данных пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-163">When hello app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span> <span data-ttu-id="36dc6-164">Если ADAL определит, что данный пользователь hello должен toosign в tooget маркера, отображает окно входа в диалоговом окне, собирает учетные данные пользователя hello и возвращает токен после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="36dc6-164">If ADAL determines that hello user needs toosign in tooget a token, it displays a sign-in dialog box, collects hello user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="36dc6-165">Если не удается tooreturn токен ADAL для какой-либо причине, hello *AuthenticationResult* находится в состоянии ошибки.</span><span class="sxs-lookup"><span data-stu-id="36dc6-165">If ADAL is unable tooreturn a token for any reason, hello *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="36dc6-166">Теперь это маркер доступа hello toouse времени, вы приобрели.</span><span class="sxs-lookup"><span data-stu-id="36dc6-166">Now it's time toouse hello access token you just acquired.</span></span> <span data-ttu-id="36dc6-167">Также в hello `Search(...)` метода присоединения hello маркера toohello запроса получения Graph API в hello **авторизации** заголовка:</span><span class="sxs-lookup"><span data-stu-id="36dc6-167">Also in hello `Search(...)` method, attach hello token toohello Graph API get request in hello **Authorization** header:</span></span>

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="36dc6-168">Можно использовать hello `AuthenticationResult` toodisplay сведения о пользователе hello в приложение hello, например идентификатор пользователя hello объекта:</span><span class="sxs-lookup"><span data-stu-id="36dc6-168">You can use hello `AuthenticationResult` object toodisplay information about hello user in hello app, such as hello user's ID:</span></span>

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="36dc6-169">Также можно использовать ADAL toosign пользователей вне приложения hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-169">You can also use ADAL toosign users out of hello app.</span></span> <span data-ttu-id="36dc6-170">Когда пользователь hello выбирает hello **выйти** кнопку, убедитесь, что hello следующего вызова слишком`AcquireTokenAsync(...)` показано представление «вход».</span><span class="sxs-lookup"><span data-stu-id="36dc6-170">When hello user clicks hello **Sign Out** button, ensure that hello next call too`AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="36dc6-171">С ADAL это действие можно так же легко, как очистка кэша маркера hello:</span><span class="sxs-lookup"><span data-stu-id="36dc6-171">With ADAL, this action is as easy as clearing hello token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="36dc6-172">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="36dc6-172">What's next</span></span>
<span data-ttu-id="36dc6-173">Теперь у вас есть рабочее приложение для магазина Windows, можно проверять подлинность пользователей, безопасно вызывать веб-API, с помощью OAuth 2.0 и получить основные сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about hello user.</span></span>

<span data-ttu-id="36dc6-174">Если уже еще не заполнены вашего клиента с пользователями, пришло время toodo hello таким образом.</span><span class="sxs-lookup"><span data-stu-id="36dc6-174">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>
1. <span data-ttu-id="36dc6-175">Запуск приложения DirectorySearcher и затем войдите с помощью одного из пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-175">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="36dc6-176">Осуществите поиск других пользователей по их имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="36dc6-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="36dc6-177">Закройте приложение hello и перезапустить ее.</span><span class="sxs-lookup"><span data-stu-id="36dc6-177">Close hello app, and rerun it.</span></span> <span data-ttu-id="36dc6-178">Обратите внимание на то, как hello пользовательского сеанса остается без изменений.</span><span class="sxs-lookup"><span data-stu-id="36dc6-178">Notice how hello user’s session remains intact.</span></span>
4. <span data-ttu-id="36dc6-179">Выйдите из системы, щелкнув правой кнопкой мыши горизонтальную полосу toodisplay hello и затем войдите как другой пользователь.</span><span class="sxs-lookup"><span data-stu-id="36dc6-179">Sign out by right-clicking toodisplay hello bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="36dc6-180">ADAL упрощает легко tooincorporate всех этих общих идентификаторов функций в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="36dc6-180">ADAL makes it easy tooincorporate all these common identity features into hello app.</span></span> <span data-ttu-id="36dc6-181">Он отвечает за всю работу dirty hello, например для управления кэшем, поддержка протокола OAuth, предоставляя hello пользователя с именем входа пользовательского интерфейса, и обновление истек срок действия маркеров.</span><span class="sxs-lookup"><span data-stu-id="36dc6-181">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="36dc6-182">Необходим вызов tooknow только один API-Интерфейс `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="36dc6-182">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="36dc6-183">Для справки, загрузить hello [полного примера](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (без настройки).</span><span class="sxs-lookup"><span data-stu-id="36dc6-183">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="36dc6-184">Теперь можно переходить на сценариях tooadditional удостоверений.</span><span class="sxs-lookup"><span data-stu-id="36dc6-184">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="36dc6-185">Например, попробуйте использовать [защиту веб-API для .NET с помощью Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="36dc6-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
