---
title: "aaaAzure Active Directory B2C | Документы Microsoft"
description: "Как toobuild настольных приложений Windows, содержит вход, регистрации и профиль управления с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="13883-103">Azure AD B2C: создание классического приложения Windows</span><span class="sxs-lookup"><span data-stu-id="13883-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="13883-104">С помощью B2C Azure Active Directory (Azure AD), можно добавить классического приложения функции управления tooyour мощные самообслуживания идентификаторов в несколько простых шагов.</span><span class="sxs-lookup"><span data-stu-id="13883-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features tooyour desktop app in a few short steps.</span></span> <span data-ttu-id="13883-105">В этой статье будет показано, как toocreate приложение .NET Windows Presentation Foundation (WPF) «список дел», которое включает в себя пользователя регистрации, вход и управление профилями пользователей.</span><span class="sxs-lookup"><span data-stu-id="13883-105">This article will show you how toocreate a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="13883-106">приложение Hello будет включать поддержку для регистрации и входа с помощью электронной почты или имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="13883-106">hello app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="13883-107">Приложение будет поддерживать регистрацию и вход в систему по имени пользователя или адресу электронной почты, а также по учетной записи в социальной сети, такой как Facebook или Google.</span><span class="sxs-lookup"><span data-stu-id="13883-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="13883-108">Создание каталога Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="13883-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="13883-109">Перед использованием Azure AD B2C необходимо создать каталог или клиент.</span><span class="sxs-lookup"><span data-stu-id="13883-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="13883-110">Каталог — это контейнер для данных всех ваших пользователей, приложений, групп и т. д.</span><span class="sxs-lookup"><span data-stu-id="13883-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="13883-111">Прежде чем продолжать работу с руководством, [создайте каталог B2C](active-directory-b2c-get-started.md), если вы его еще не создали.</span><span class="sxs-lookup"><span data-stu-id="13883-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="13883-112">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="13883-112">Create an application</span></span>
<span data-ttu-id="13883-113">Далее необходимо toocreate приложения в каталоге B2C.</span><span class="sxs-lookup"><span data-stu-id="13883-113">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="13883-114">Это дает сведения о Azure AD, что его нуждается toosecurely взаимодействовать с приложением.</span><span class="sxs-lookup"><span data-stu-id="13883-114">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="13883-115">toocreate приложения, выполните [эти инструкции](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="13883-115">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="13883-116">Не забудьте сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="13883-116">Be sure to:</span></span>

* <span data-ttu-id="13883-117">Включить **собственного клиента** в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="13883-117">Include a **native client** in hello application.</span></span>
* <span data-ttu-id="13883-118">Копировать hello **URI перенаправления** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="13883-118">Copy hello **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="13883-119">Это URL-адрес по умолчанию hello для этого примера кода.</span><span class="sxs-lookup"><span data-stu-id="13883-119">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="13883-120">Копировать hello **идентификатор приложения** , назначенный tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="13883-120">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="13883-121">Оно понадобится вам позднее.</span><span class="sxs-lookup"><span data-stu-id="13883-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="13883-122">Создание политик</span><span class="sxs-lookup"><span data-stu-id="13883-122">Create your policies</span></span>
<span data-ttu-id="13883-123">В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="13883-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="13883-124">Этот пример кода включает три способа идентификации: регистрацию, вход в систему и изменение профиля.</span><span class="sxs-lookup"><span data-stu-id="13883-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="13883-125">Необходимо toocreate политики для каждого типа, как описано в [статье политики](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="13883-125">You need toocreate a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="13883-126">При создании hello три политики, нужно убедиться, что:</span><span class="sxs-lookup"><span data-stu-id="13883-126">When you create hello three policies, be sure to:</span></span>

* <span data-ttu-id="13883-127">Выберите либо **регистрации идентификатора пользователя** или **электронной почты регистрации** в колонке Поставщики удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="13883-127">Choose either **User ID sign-up** or **Email sign-up** in hello identity providers blade.</span></span>
* <span data-ttu-id="13883-128">В политике регистрации укажите **отображаемое имя** и другие атрибуты регистрации.</span><span class="sxs-lookup"><span data-stu-id="13883-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="13883-129">В каждой политике в качестве утверждения приложения выберите утверждения **Отображаемое имя** и **Идентификатор объекта**.</span><span class="sxs-lookup"><span data-stu-id="13883-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="13883-130">Можно также выбрать другие утверждения.</span><span class="sxs-lookup"><span data-stu-id="13883-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="13883-131">Копировать hello **имя** каждой политики, после его создания.</span><span class="sxs-lookup"><span data-stu-id="13883-131">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="13883-132">Он должен иметь префикс hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="13883-132">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="13883-133">Эти имена политик понадобятся вам через некоторое время.</span><span class="sxs-lookup"><span data-stu-id="13883-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="13883-134">После успешного создания hello три политики, вы будете готовы toobuild приложения.</span><span class="sxs-lookup"><span data-stu-id="13883-134">After you have successfully created hello three policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="13883-135">Загрузка кода hello</span><span class="sxs-lookup"><span data-stu-id="13883-135">Download hello code</span></span>
<span data-ttu-id="13883-136">Здравствуйте, код для этого учебника [сохраняется на сайте GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="13883-136">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="13883-137">Образец hello toobuild как можно перейти, вы можете [загрузить каркас проект как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="13883-137">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="13883-138">Также можно клонировать основу hello:</span><span class="sxs-lookup"><span data-stu-id="13883-138">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="13883-139">также является приложение Hello завершения [доступны как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) или на hello `complete` ветви hello одного репозитория.</span><span class="sxs-lookup"><span data-stu-id="13883-139">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

<span data-ttu-id="13883-140">После загрузки кода образца hello запущен tooget файл .sln Visual Studio откройте hello.</span><span class="sxs-lookup"><span data-stu-id="13883-140">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="13883-141">Hello `TaskClient` проект является hello классическое приложение WPF, hello пользователь взаимодействует с.</span><span class="sxs-lookup"><span data-stu-id="13883-141">hello `TaskClient` project is hello WPF desktop application that hello user interacts with.</span></span> <span data-ttu-id="13883-142">Для целей этого учебника hello он вызывает задачу серверной части веб-API, размещенных в Azure, который хранит список дел каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="13883-142">For hello purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="13883-143">Нет необходимости toobuild hello веб-API, у нас уже есть она запущена.</span><span class="sxs-lookup"><span data-stu-id="13883-143">You do not need toobuild hello web API, we already have it running for you.</span></span>

<span data-ttu-id="13883-144">toolearn как веб-API безопасно проверка подлинности запросов с помощью Azure AD B2C извлечь [веб-API Приступая к работе статьи](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="13883-144">toolearn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="13883-145">Выполнение политик</span><span class="sxs-lookup"><span data-stu-id="13883-145">Execute policies</span></span>
<span data-ttu-id="13883-146">Приложение взаимодействует с Azure AD B2C, отправляя сообщения проверки подлинности, укажите политику hello требуемый tooexecute hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="13883-146">Your app communicates with Azure AD B2C by sending authentication messages that specify hello policy they want tooexecute as part of hello HTTP request.</span></span> <span data-ttu-id="13883-147">Для классических приложений .NET, можно использовать hello Предварительный просмотр сообщения проверки подлинности OAuth 2.0 toosend библиотеки проверки подлинности Microsoft (MSAL), выполнение политик и получения маркеров, которые вызывают веб-API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="13883-147">For .NET desktop applications, you can use hello preview Microsoft Authentication Library (MSAL) toosend OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="13883-148">Установка MSAL</span><span class="sxs-lookup"><span data-stu-id="13883-148">Install MSAL</span></span>
<span data-ttu-id="13883-149">Добавить MSAL toohello `TaskClient` проекта с помощью консоли диспетчера пакетов Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="13883-149">Add MSAL toohello `TaskClient` project by using hello Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="13883-150">Ввод данных B2C</span><span class="sxs-lookup"><span data-stu-id="13883-150">Enter your B2C details</span></span>
<span data-ttu-id="13883-151">Привет открыть файл `Globals.cs` и замените все значения свойств hello свои собственные.</span><span class="sxs-lookup"><span data-stu-id="13883-151">Open hello file `Globals.cs` and replace each of hello property values with your own.</span></span> <span data-ttu-id="13883-152">Этот класс используется во всех `TaskClient` tooreference часто используемых значений.</span><span class="sxs-lookup"><span data-stu-id="13883-152">This class is used throughout `TaskClient` tooreference commonly used values.</span></span>

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-hello-publicclientapplication"></a><span data-ttu-id="13883-153">Создать hello PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="13883-153">Create hello PublicClientApplication</span></span>
<span data-ttu-id="13883-154">основной класс Hello MSAL: `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="13883-154">hello primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="13883-155">Этот класс представляет приложение в системе hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="13883-155">This class represents your application in hello Azure AD B2C system.</span></span> <span data-ttu-id="13883-156">Когда hello Инициализирует приложение, создайте экземпляр класса `PublicClientApplication` в `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="13883-156">When hello app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="13883-157">Это можно использовать в окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="13883-157">This can be used throughout hello window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="13883-158">Запуск потока регистрации</span><span class="sxs-lookup"><span data-stu-id="13883-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="13883-159">Когда пользователь соглашается toosigns вверх, нужно tooinitiate регистрации потока, в котором применяется созданной вами политикой регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="13883-159">When a user opts toosigns up, you want tooinitiate a sign-up flow that uses hello sign-up policy you created.</span></span> <span data-ttu-id="13883-160">Для этого требуется только вызов метода `pca.AcquireTokenAsync(...)`с помощью MSAL.</span><span class="sxs-lookup"><span data-stu-id="13883-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="13883-161">Здравствуйте, параметры, можно передать слишком`AcquireTokenAsync(...)` определить, какой токен появляется, hello политику, используемую в запрос проверки подлинности hello и многое другое.</span><span class="sxs-lookup"><span data-stu-id="13883-161">hello parameters you pass too`AcquireTokenAsync(...)` determine which token you receive, hello policy used in hello authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="13883-162">Инициация потока входа</span><span class="sxs-lookup"><span data-stu-id="13883-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="13883-163">Можно выполнить вход в потоке hello так же, как запустить регистрации потока.</span><span class="sxs-lookup"><span data-stu-id="13883-163">You can initiate a sign-in flow in hello same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="13883-164">При входе в систему пользователя сделать hello же вызвать tooMSAL, с использованием политики входа:</span><span class="sxs-lookup"><span data-stu-id="13883-164">When a user signs in, make hello same call tooMSAL, this time by using your sign-in policy:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="13883-165">Инициирование потока изменения профиля</span><span class="sxs-lookup"><span data-stu-id="13883-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="13883-166">Еще раз, можно выполнить политику изменения профиля в hello аналогичным способом:</span><span class="sxs-lookup"><span data-stu-id="13883-166">Again, you can execute an edit-profile policy in hello same fashion:</span></span>

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

<span data-ttu-id="13883-167">Во всех этих случаях MSAL либо возвращает маркер в `AuthenticationResult` , либо выдает исключение.</span><span class="sxs-lookup"><span data-stu-id="13883-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="13883-168">Каждый раз, получить маркер из MSAL, можно использовать hello `AuthenticationResult.User` объекта tooupdate hello пользовательских данных в приложение hello, например hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="13883-168">Each time you get a token from MSAL, you can use hello `AuthenticationResult.User` object tooupdate hello user data in hello app, such as hello UI.</span></span> <span data-ttu-id="13883-169">ADAL также кэшей hello маркер для использования в других частях приложения hello.</span><span class="sxs-lookup"><span data-stu-id="13883-169">ADAL also caches hello token for use in other parts of hello application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="13883-170">Проверка наличия маркеров при запуске приложения</span><span class="sxs-lookup"><span data-stu-id="13883-170">Check for tokens on app start</span></span>
<span data-ttu-id="13883-171">Также можно отслеживать состояние входа пользователя hello tookeep MSAL.</span><span class="sxs-lookup"><span data-stu-id="13883-171">You can also use MSAL tookeep track of hello user's sign-in state.</span></span>  <span data-ttu-id="13883-172">В этом приложении мы хотим tooremain пользователя hello, даже после их закрыть приложение hello и повторно открыть его в системе.</span><span class="sxs-lookup"><span data-stu-id="13883-172">In this app, we want hello user tooremain signed in even after they close hello app & re-open it.</span></span>  <span data-ttu-id="13883-173">Назад внутри hello `OnInitialized` переопределить, используйте его MSAL `AcquireTokenSilent` toocheck метод для кэшированных маркеров:</span><span class="sxs-lookup"><span data-stu-id="13883-173">Back inside hello `OnInitialized` override, use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
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
```

## <a name="call-hello-task-api"></a><span data-ttu-id="13883-174">Вызвать API задачи hello</span><span class="sxs-lookup"><span data-stu-id="13883-174">Call hello task API</span></span>
<span data-ttu-id="13883-175">Использовали MSAL tooexecute политик и получения токенов.</span><span class="sxs-lookup"><span data-stu-id="13883-175">You have now used MSAL tooexecute policies and get tokens.</span></span>  <span data-ttu-id="13883-176">При необходимости toouse один эти токены toocall hello задач API вы снова сможете использовать его MSAL `AcquireTokenSilent` toocheck метод для кэшированных маркеров:</span><span class="sxs-lookup"><span data-stu-id="13883-176">When you want toouse one these tokens toocall hello task API, you can again use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
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
    ...
```

<span data-ttu-id="13883-177">При слишком hello вызовов`AcquireTokenSilentAsync(...)` завершается успешно и будет найден маркер в кэш hello, можно добавить hello маркера toohello `Authorization` заголовок hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="13883-177">When hello call too`AcquireTokenSilentAsync(...)` succeeds and a token is found in hello cache, you can add hello token toohello `Authorization` header of hello HTTP request.</span></span> <span data-ttu-id="13883-178">Список дел заголовок tooauthenticate hello запроса tooread hello в учетной записи пользователя будет использоваться веб-задачи Hello API:</span><span class="sxs-lookup"><span data-stu-id="13883-178">hello task web API will use this header tooauthenticate hello request tooread hello user's to-do list:</span></span>

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a><span data-ttu-id="13883-179">Пользователь hello Sign out</span><span class="sxs-lookup"><span data-stu-id="13883-179">Sign hello user out</span></span>
<span data-ttu-id="13883-180">Наконец, можно использовать MSAL tooend сеанс пользователя с приложение hello при выборе пользователем hello **Выход**.  При использовании MSAL, эти действия выполняются, сняв все маркеры hello из кэша маркеров hello.</span><span class="sxs-lookup"><span data-stu-id="13883-180">Finally, you can use MSAL tooend a user's session with hello app when hello user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of hello tokens from hello token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="13883-181">Запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="13883-181">Run hello sample app</span></span>
<span data-ttu-id="13883-182">Наконец построение и запуск образца hello.</span><span class="sxs-lookup"><span data-stu-id="13883-182">Finally, build and run hello sample.</span></span>  <span data-ttu-id="13883-183">После регистрации приложения hello с помощью электронной почты адрес или имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="13883-183">Sign up for hello app by using an email address or user name.</span></span> <span data-ttu-id="13883-184">Выйдите из системы и войти снова как hello же пользователя.</span><span class="sxs-lookup"><span data-stu-id="13883-184">Sign out and sign back in as hello same user.</span></span> <span data-ttu-id="13883-185">Измените профиль пользователя.</span><span class="sxs-lookup"><span data-stu-id="13883-185">Edit that user's profile.</span></span> <span data-ttu-id="13883-186">Выйдите и зарегистрируйтесь от имени другого пользователя.</span><span class="sxs-lookup"><span data-stu-id="13883-186">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="13883-187">Добавление поставщиков удостоверений социальных сетей</span><span class="sxs-lookup"><span data-stu-id="13883-187">Add social IDPs</span></span>
<span data-ttu-id="13883-188">В настоящее время приложение hello поддерживает только регистрации пользователя и войти, использовать **локальные учетные записи**.</span><span class="sxs-lookup"><span data-stu-id="13883-188">Currently, hello app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="13883-189">Учетные записи хранятся в каталоге B2C, где применяется имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="13883-189">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="13883-190">С помощью Azure AD B2C можно добавить поддержку для других поставщиков удостоверений (IDP), не изменяя код.</span><span class="sxs-lookup"><span data-stu-id="13883-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="13883-191">tooadd социальных IDPs tooyour приложение, начните с выполнения следующего hello подробные инструкции в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="13883-191">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="13883-192">Для каждого поставщика Удостоверений требуется toosupport, нужно tooregister приложения в этой системе и получение идентификатора клиента.</span><span class="sxs-lookup"><span data-stu-id="13883-192">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="13883-193">Настройка Facebook как поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="13883-193">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="13883-194">Настройка Google как поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="13883-194">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="13883-195">Настройка Amazon как поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="13883-195">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="13883-196">Настройка LinkedIn как поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="13883-196">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="13883-197">После добавления каталог tooyour B2C Поставщики удостоверений hello, необходимо каждый из трех политик tooinclude hello новый IDPs как описано в hello tooedit [статье политики](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="13883-197">After you add hello identity providers tooyour B2C directory, you need tooedit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="13883-198">После сохранения политик, снова запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="13883-198">After you save your policies, run hello app again.</span></span> <span data-ttu-id="13883-199">Вы увидите hello, добавления новых IDPs входа и регистрации в качестве параметров каждой своими впечатлениями удостоверения.</span><span class="sxs-lookup"><span data-stu-id="13883-199">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="13883-200">Можно поэкспериментировать с политиками и наблюдать за hello влияние на примере приложения.</span><span class="sxs-lookup"><span data-stu-id="13883-200">You can experiment with your policies and observe hello effects on your sample app.</span></span> <span data-ttu-id="13883-201">например: добавлять или удалять поставщиков удостоверений, управлять утверждениями приложений или изменять атрибуты регистрации, а также наблюдать эффект в примере приложения.</span><span class="sxs-lookup"><span data-stu-id="13883-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="13883-202">Эксперименты помогают увидеть связь между политиками, запросами на проверку подлинности и библиотекой MSAL.</span><span class="sxs-lookup"><span data-stu-id="13883-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="13883-203">Справочник по hello выполнить образец [предоставляется как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="13883-203">For reference, hello completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="13883-204">Кроме того, его можно клонировать из GitHub:</span><span class="sxs-lookup"><span data-stu-id="13883-204">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
