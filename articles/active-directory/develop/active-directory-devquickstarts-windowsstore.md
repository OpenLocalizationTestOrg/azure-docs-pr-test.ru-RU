---
title: "Приступая к работе с Магазином Windows в Azure AD | Документация Майкрософт"
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
ms.openlocfilehash: 6b5189dc06d7f8b0ed4426944948b904feba847e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="4c7a1-103">Интеграция Azure AD с приложениями Магазина Windows</span><span class="sxs-lookup"><span data-stu-id="4c7a1-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="4c7a1-104">Проекты для Магазина Windows 8.1 и более ранних версий не поддерживаются в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="4c7a1-105">Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="4c7a1-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="4c7a1-106">При разработке приложений для Магазина Windows система Azure Active Directory (Azure AD) позволяет легко и просто осуществлять аутентификацию пользователей с помощью их учетных записей в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-106">If you're developing apps for the Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward to authenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="4c7a1-107">Благодаря интеграции с Azure AD приложение может безопасно использовать любые веб-API, защищаемые с помощью Azure AD, например интерфейсы API Office 365 или Azure.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="4c7a1-108">Классическим приложениям для Магазина Windows, которым необходим доступ к защищенным ресурсам, Azure AD предоставляет библиотеку аутентификации Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="4c7a1-108">For Windows Store desktop apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="4c7a1-109">Единственное предназначение ADAL — упростить процесс получения маркеров доступа.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-109">The sole purpose of ADAL is to make it easy for the app to get access tokens.</span></span> <span data-ttu-id="4c7a1-110">В этой статье показано, насколько это легко, на примере создания приложения DirectorySearcher для Магазина Windows, которое обладает следующими преимуществами:</span><span class="sxs-lookup"><span data-stu-id="4c7a1-110">To demonstrate how easy it is, this article shows how to build a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="4c7a1-111">получает маркеры доступа для вызова интерфейса API Graph Azure AD с помощью [протокола проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx);</span><span class="sxs-lookup"><span data-stu-id="4c7a1-111">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="4c7a1-112">осуществляет поиск пользователей в каталоге с помощью заданного имени участника-пользователя (UPN);</span><span class="sxs-lookup"><span data-stu-id="4c7a1-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="4c7a1-113">Обеспечивает функцию выхода пользователя из приложения.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="4c7a1-114">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="4c7a1-114">Before you get started</span></span>
* <span data-ttu-id="4c7a1-115">Скачайте [схему проекта](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip) или [готовый пример](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="4c7a1-115">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="4c7a1-116">Каждая из этих загрузок является решением Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="4c7a1-117">Вам также необходим клиент Azure AD для создания пользователей и регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-117">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="4c7a1-118">Если клиента нет, [узнайте, как его получить](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="4c7a1-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="4c7a1-119">Когда будете готовы, выполните процедуры, описанные в следующих трех разделах.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-119">When you are ready, follow the procedures in the next three sections.</span></span>

## <a name="step-1-register-the-directorysearcher-app"></a><span data-ttu-id="4c7a1-120">Шаг 1. Регистрация приложения DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="4c7a1-120">Step 1: Register the DirectorySearcher app</span></span>
<span data-ttu-id="4c7a1-121">Чтобы приложение могло получать маркеры, сначала необходимо его зарегистрировать в клиенте Azure AD и предоставить ему разрешение на доступ к интерфейсу API Graph для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-121">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="4c7a1-122">Этот процесс описывается далее.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-122">Here's how:</span></span>

1. <span data-ttu-id="4c7a1-123">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c7a1-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4c7a1-124">На верхней панели щелкните свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-124">On the top bar, click your account.</span></span> <span data-ttu-id="4c7a1-125">Затем в списке **Каталог** выберите клиент Active Directory для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-125">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="4c7a1-126">В области слева щелкните **Больше служб** и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="4c7a1-127">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="4c7a1-128">Следуя инструкциям, создайте **собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-128">Follow the prompts to create a **Native Client Application**.</span></span>
  * <span data-ttu-id="4c7a1-129">**Имя** — это описание приложения для пользователей.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-129">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="4c7a1-130">**URI перенаправления** представляет собой сочетание схемы и строки, используемое Azure AD для возвращения ответов маркеров.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-130">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="4c7a1-131">Введите значение заполнителя (например, **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="4c7a1-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="4c7a1-132">Вы замените это значение позже.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-132">You'll replace the value later.</span></span>
6. <span data-ttu-id="4c7a1-133">После завершения регистрации Azure AD присваивает приложению уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-133">After you’ve completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="4c7a1-134">Скопируйте значение на вкладке **Приложение**. Оно потребуется вам позже.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-134">Copy the value on the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="4c7a1-135">На странице **Параметры** выберите **Необходимые разрешения** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-135">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="4c7a1-136">Для приложения **Azure Active Directory** в качестве API выберите **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-136">For the **Azure Active Directory** app, select **Microsoft Graph** as the API.</span></span>
9. <span data-ttu-id="4c7a1-137">В разделе **Делегированные разрешения** добавьте разрешение **Access the directory as the signed-in user** (Доступ к каталогу от имени пользователя, выполнившего вход).</span><span class="sxs-lookup"><span data-stu-id="4c7a1-137">Under **Delegated Permissions**, add the **Access the directory as the signed-in user** permission.</span></span> <span data-ttu-id="4c7a1-138">Это действие позволяет приложению отправлять запросы в API Graph для пользователей.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-138">Doing so enables the app to query the Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="4c7a1-139">Шаг 2. Установка и настройка ADAL</span><span class="sxs-lookup"><span data-stu-id="4c7a1-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="4c7a1-140">Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="4c7a1-141">Чтобы обеспечить взаимодействие библиотеки ADAL с Azure AD, необходимо указать определенные сведения о регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-141">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="4c7a1-142">Добавьте ADAL в проект DirectorySearcher с помощью консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-142">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="4c7a1-143">В проекте DirectorySearcher откройте файл MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-143">In the DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="4c7a1-144">Замените значения в разделе **Config Values** (Значения конфигурации) значениями, введенными на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-144">Replace the values in the **Config Values** region with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="4c7a1-145">Ваш код будет ссылаться на эти значения при каждом использовании ADAL.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-145">Your code refers to these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="4c7a1-146">*tenant* — это домен вашего клиента Azure AD (например, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4c7a1-146">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="4c7a1-147">*clientId* — идентификатор клиента приложения, скопированный с портала.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-147">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
4. <span data-ttu-id="4c7a1-148">Теперь необходимо обнаружить URI обратного вызова для вашего приложения Магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-148">You now need to discover the callback URI for your Windows Store app.</span></span> <span data-ttu-id="4c7a1-149">Установите точку останова в этой строке в методе `MainPage` :</span><span class="sxs-lookup"><span data-stu-id="4c7a1-149">Set a breakpoint on this line in the `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="4c7a1-150">Выполните сборку решения, убедившись, что все ссылки на пакеты восстановлены.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-150">Build the solution, making sure that all package references are restored.</span></span> <span data-ttu-id="4c7a1-151">Если какие-то пакеты отсутствуют, то откройте диспетчер пакетов NuGet и восстановите их.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-151">If any packages are missing, open the NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="4c7a1-152">Запустите приложение и скопируйте значение `redirectUri` при попадании в точку останова.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-152">Run the app, and copy the value of `redirectUri` when the breakpoint is hit.</span></span> <span data-ttu-id="4c7a1-153">Это значение выглядит примерно так:</span><span class="sxs-lookup"><span data-stu-id="4c7a1-153">The value should look something like the following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="4c7a1-154">Вернитесь на вкладку **Параметры** приложения на портале Azure и добавьте вышеупомянутое значение **RedirectUri**.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-154">Back on the **Settings** tab of the app in the Azure portal, add a **RedirectUri** with the preceding value.</span></span>  

## <a name="step-3-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="4c7a1-155">Шаг 3. Использование ADAL для получения маркеров из Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c7a1-155">Step 3: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="4c7a1-156">Основной принцип ADAL состоит в следующем: каждый раз, когда приложению необходим маркер доступа, оно просто вызывает `authContext.AcquireToken(…)`, а ADAL делает все остальное.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-156">The basic principle behind ADAL is that whenever the app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="4c7a1-157">Инициализируйте класс `AuthenticationContext` приложения, который является основным классом ADAL.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-157">Initialize the app’s `AuthenticationContext`, which is the primary class of ADAL.</span></span> <span data-ttu-id="4c7a1-158">Это действие отправляет в библиотеку ADAL координаты, которые ей требуются для взаимодействия с Azure AD, и сообщает о способе кэширования маркеров.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-158">This action passes ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="4c7a1-159">Найдите метод `Search(...)`, который вызывается при нажатии кнопки **Поиск** в пользовательском интерфейсе приложения.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-159">Locate the `Search(...)` method, which is invoked when users click the **Search** button on the app's UI.</span></span> <span data-ttu-id="4c7a1-160">Этот метод выполняет запрос GET в интерфейс API Graph службы Azure AD для запроса списка пользователей, чьи имена участника-пользователя начинаются с данного слова поиска.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-160">This method makes a get request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span> <span data-ttu-id="4c7a1-161">Для отправки запросов в API Graph включите маркер доступа в заголовок **авторизации** запроса.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-161">To query the Graph API, include an access token in the request's **Authorization** header.</span></span> <span data-ttu-id="4c7a1-162">Вот где может пригодиться ADAL.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-162">This is where ADAL comes in.</span></span>

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
                ShowAuthError(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="4c7a1-163">Когда приложение запрашивает маркер путем вызова `AcquireTokenAsync(...)`, библиотека ADAL пытается вернуть маркер без запроса учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-163">When the app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span> <span data-ttu-id="4c7a1-164">Если библиотека ADAL решит, что пользователь должен войти в систему для получения маркера, то она отобразит диалоговое окно входа, соберет учетные данные пользователя и вернет маркер после успешной аутентификации.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-164">If ADAL determines that the user needs to sign in to get a token, it displays a sign-in dialog box, collects the user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="4c7a1-165">Если ADAL по какой-то причине не сможет вернуть маркер, то статус *AuthenticationResult* будет представлять собой ошибку.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-165">If ADAL is unable to return a token for any reason, the *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="4c7a1-166">Теперь настало время использовать только что полученный маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-166">Now it's time to use the access token you just acquired.</span></span> <span data-ttu-id="4c7a1-167">Также в методе `Search(...)` добавьте маркер в запрос GET API Graph в заголовке **авторизации**:</span><span class="sxs-lookup"><span data-stu-id="4c7a1-167">Also in the `Search(...)` method, attach the token to the Graph API get request in the **Authorization** header:</span></span>

    ```C#
    // Add the access token to the Authorization header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="4c7a1-168">Для отображения сведений о пользователе в вашем приложении, например идентификатора пользователя, можно использовать объект `AuthenticationResult`:</span><span class="sxs-lookup"><span data-stu-id="4c7a1-168">You can use the `AuthenticationResult` object to display information about the user in the app, such as the user's ID:</span></span>

    ```C#
    // Update the page UI to represent the signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="4c7a1-169">Также с помощью ADAL можно выполнить выход пользователей из приложения.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-169">You can also use ADAL to sign users out of the app.</span></span> <span data-ttu-id="4c7a1-170">Когда пользователь нажимает кнопку **Выход**, убедитесь, что при следующем вызове `AcquireTokenAsync(...)` отображается окно входа.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-170">When the user clicks the **Sign Out** button, ensure that the next call to `AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="4c7a1-171">С помощью ADAL это так же просто сделать, как и очистить кэш маркеров:</span><span class="sxs-lookup"><span data-stu-id="4c7a1-171">With ADAL, this action is as easy as clearing the token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from the token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="4c7a1-172">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="4c7a1-172">What's next</span></span>
<span data-ttu-id="4c7a1-173">Теперь у нас есть рабочее приложение для Магазина Windows, которое может выполнять аутентификацию пользователей, безопасно вызывать веб-API с помощью OAuth 2.0 и получать основные сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the user.</span></span>

<span data-ttu-id="4c7a1-174">Если в клиент еще не добавлены пользователи, то сейчас самое время это сделать.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-174">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>
1. <span data-ttu-id="4c7a1-175">Запустите приложение DirectorySearcher и войдите как один из пользователей.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-175">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="4c7a1-176">Осуществите поиск других пользователей по их имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="4c7a1-177">Закройте приложение и снова запустите его.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-177">Close the app, and rerun it.</span></span> <span data-ttu-id="4c7a1-178">Обратите внимание на то, что пользовательский сеанс не изменяется.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-178">Notice how the user’s session remains intact.</span></span>
4. <span data-ttu-id="4c7a1-179">Выйдите (щелкните правой кнопкой мыши, чтобы отобразить нижнюю панель) и снова войдите под именем другого пользователя.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-179">Sign out by right-clicking to display the bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="4c7a1-180">Библиотека ADAL упрощает процесс включения всех этих общих возможностей идентификации в приложение.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-180">ADAL makes it easy to incorporate all these common identity features into the app.</span></span> <span data-ttu-id="4c7a1-181">Она отвечает за всю "грязную работу": управление кэшем, поддержку протокола OAuth, предоставление пользователю пользовательского интерфейса для входа и обновление истекших маркеров.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-181">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="4c7a1-182">Вам нужно знать только один вызов API — `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-182">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="4c7a1-183">Скачайте для справки [готовый пример](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (без ваших значений конфигурации).</span><span class="sxs-lookup"><span data-stu-id="4c7a1-183">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="4c7a1-184">Теперь можно приступить к дополнительным сценариям идентификации.</span><span class="sxs-lookup"><span data-stu-id="4c7a1-184">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="4c7a1-185">Например, попробуйте использовать [защиту веб-API для .NET с помощью Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="4c7a1-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
