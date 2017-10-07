---
title: "aaaAdd tooan входа iOS приложения с помощью hello конечная точка Azure AD v2.0 | Документы Microsoft"
description: "Как toobuild приложения iOS, входит в рабочую или учебную учетных записей пользователей с обоих личную учетную запись Майкрософт и с помощью сторонних библиотек."
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="6c3d0-103">Добавление приложения iOS tooan входа с помощью библиотеки сторонних разработчиков с API Graph с помощью конечной точки v2.0 hello</span><span class="sxs-lookup"><span data-stu-id="6c3d0-103">Add sign-in tooan iOS app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="6c3d0-104">Hello платформы удостоверений использует открытых стандартов, такие как OAuth2 и OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="6c3d0-105">Разработчики могут использовать любую библиотеку, они должны toointegrate с наших служб.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="6c3d0-106">toohelp разработчики используют нашей платформы с другими библиотеками, мы написали несколько пошаговых руководств, как это один toodemonstrate как tooconfigure сторонних библиотек tooconnect toohello платформы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="6c3d0-107">Большинство библиотек, которые реализуют [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) могут подключаться toohello платформы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="6c3d0-108">Приложения hello, создает в этом пошаговом руководстве пользователям можно войти в организации tootheir и выполните поиск другим пользователям в организации с помощью Graph API hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for others in their organization by using hello Graph API.</span></span>

<span data-ttu-id="6c3d0-109">Если вы новый tooOAuth2 или OpenID Connect, большая часть конфигурации этого образца может оказаться tooyou смысле.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="6c3d0-110">Рекомендуем сначала ознакомиться со статьей [Протоколы версии 2.0 — поток кода авторизации OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="6c3d0-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="6c3d0-111">Некоторые возможности платформы, имеющие выражения в hello OAuth2 или OpenID Connect стандартами, например условный доступ и управление политикой Intune, требуется вы toouse нашей открытой библиотеки удостоверений Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="6c3d0-112">Конечная точка v2.0 Hello не поддерживает все сценарии Azure Active Directory и возможности.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="6c3d0-113">toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="6c3d0-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="6c3d0-114">Скачивание кода с сайта GitHub</span><span class="sxs-lookup"><span data-stu-id="6c3d0-114">Download code from GitHub</span></span>
<span data-ttu-id="6c3d0-115">поддерживается Hello кода для этого учебника [на GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="6c3d0-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="6c3d0-116">можно toofollow вдоль [загрузить приложение hello основу как .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) или основу hello клона:</span><span class="sxs-lookup"><span data-stu-id="6c3d0-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="6c3d0-117">Можно также просто загрузить образец hello и начать работу прямо сейчас.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-117">You can also just download hello sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="6c3d0-118">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="6c3d0-118">Register an app</span></span>
<span data-ttu-id="6c3d0-119">Создание нового приложения в hello [портала регистрации приложения](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), или выполните hello подробное описание действий по [как tooregister приложения с конечной точкой v2.0 hello](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="6c3d0-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at  [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="6c3d0-120">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="6c3d0-120">Make sure to:</span></span>

* <span data-ttu-id="6c3d0-121">Копировать hello **идентификатор приложения** это назначенные tooyour приложения, так как он понадобится скоро.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="6c3d0-122">Добавить hello **Mobile** платформы для приложения.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="6c3d0-123">Копировать hello **URI перенаправления** из портала hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="6c3d0-124">Необходимо использовать значение по умолчанию hello `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-124">You must use hello default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="6c3d0-125">Загрузить библиотеки NXOAuth2 стороннего hello и создание рабочей области</span><span class="sxs-lookup"><span data-stu-id="6c3d0-125">Download hello third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="6c3d0-126">В этом пошаговом руководстве будет использоваться hello OAuth2Client из GitHub, который является библиотекой OAuth2 для Mac OS X и iOS (Cocoa и Cocoa touch).</span><span class="sxs-lookup"><span data-stu-id="6c3d0-126">For this walkthrough, you will use hello OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="6c3d0-127">Эта библиотека основан на черновик 10 hello OAuth2 spec. Он реализует профиля собственное приложение hello и поддерживает конечную точку авторизации hello hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-127">This library is based on draft 10 of hello OAuth2 spec. It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="6c3d0-128">Это все, что hello потребуется toointegrate с платформой удостоверений Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-128">These are all hello things you'll need toointegrate with hello Microsoft identity platform.</span></span>

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a><span data-ttu-id="6c3d0-129">Добавьте проект tooyour hello библиотеки с помощью CocoaPods</span><span class="sxs-lookup"><span data-stu-id="6c3d0-129">Add hello library tooyour project by using CocoaPods</span></span>
<span data-ttu-id="6c3d0-130">CocoaPods — это диспетчер зависимостей для проектов Xcode.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-130">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="6c3d0-131">Автоматически управляет hello предыдущие шаги для установки.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-131">It manages hello previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="6c3d0-132">Добавьте следующие toothis podfile hello:</span><span class="sxs-lookup"><span data-stu-id="6c3d0-132">Add hello following toothis podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="6c3d0-133">Загрузка hello podfile с помощью CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-133">Load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="6c3d0-134">Будет создана новая рабочая область Xcode.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-134">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a><span data-ttu-id="6c3d0-135">Просмотр структуры hello hello проекта</span><span class="sxs-lookup"><span data-stu-id="6c3d0-135">Explore hello structure of hello project</span></span>
<span data-ttu-id="6c3d0-136">Следующая структура Hello, настройте для проектов в основу hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-136">hello following structure is set up for our project in hello skeleton:</span></span>

* <span data-ttu-id="6c3d0-137">Основное представление с поиском имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-137">A Master View with a UPN Search</span></span>
* <span data-ttu-id="6c3d0-138">Подробное представление hello данных о hello выбранного пользователя</span><span class="sxs-lookup"><span data-stu-id="6c3d0-138">A Detail View for hello data about hello selected user</span></span>
* <span data-ttu-id="6c3d0-139">Представление входа в систему, где пользователь сможет войти в graph hello tooquery приложения toohello</span><span class="sxs-lookup"><span data-stu-id="6c3d0-139">A Login View where a user can sign in toohello app tooquery hello graph</span></span>

<span data-ttu-id="6c3d0-140">Будут перенесены файлы toovarious в проверке подлинности каркас tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-140">We will move toovarious files in hello skeleton tooadd authentication.</span></span> <span data-ttu-id="6c3d0-141">Другие части кода hello, например visual код hello, не относящиеся tooidentity, но вам предоставляется.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-141">Other parts of hello code, such as hello visual code, do not pertain tooidentity but are provided for you.</span></span>

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a><span data-ttu-id="6c3d0-142">Настройка файла settings.plst hello в библиотеке hello</span><span class="sxs-lookup"><span data-stu-id="6c3d0-142">Set up hello settings.plst file in hello library</span></span>
* <span data-ttu-id="6c3d0-143">В проекте краткое руководство hello откройте hello `settings.plist` файла.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-143">In hello QuickStart project, open hello `settings.plist` file.</span></span> <span data-ttu-id="6c3d0-144">Замените hello значений элементов hello hello hello раздел tooreflect значений, используемых в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-144">Replace hello values of hello elements in hello section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="6c3d0-145">Код будет ссылаться на эти значения при каждом использовании hello библиотеку аутентификации Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-145">Your code will reference these values whenever it uses hello Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="6c3d0-146">Hello `clientId` hello идентификатор клиента приложения, скопированный из портала hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-146">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="6c3d0-147">Hello `redirectUri` является этот портал hello предоставленный URL-адрес перенаправления hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-147">hello `redirectUri` is hello redirect URL that hello portal provided.</span></span>

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="6c3d0-148">Настройка библиотеки NXOAuth2Client hello в вашей LoginViewController</span><span class="sxs-lookup"><span data-stu-id="6c3d0-148">Set up hello NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="6c3d0-149">Библиотека NXOAuth2Client Hello требует tooget некоторые значения, Настройка.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-149">hello NXOAuth2Client library requires some values tooget set up.</span></span> <span data-ttu-id="6c3d0-150">После завершения этой задачи можно использовать hello запрошенного токена toocall hello Graph API.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-150">After you complete that task, you can use hello acquired token toocall hello Graph API.</span></span> <span data-ttu-id="6c3d0-151">Поскольку `LoginView` будет вызывается каждый раз, нам нужно tooauthenticate, имеет смысл tooput значения конфигурации в файле toothat.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-151">Because `LoginView` will be called any time we need tooauthenticate, it makes sense tooput configuration values in toothat file.</span></span>

* <span data-ttu-id="6c3d0-152">Давайте добавим некоторые значения toohello `LoginViewController.m` файл tooset hello контекст для проверки подлинности и авторизации.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-152">Let's add some values toohello  `LoginViewController.m` file tooset hello context for authentication and authorization.</span></span> <span data-ttu-id="6c3d0-153">Сведения о значениях hello выполните кода hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-153">Details about hello values follow hello code.</span></span>
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

<span data-ttu-id="6c3d0-154">Давайте взглянем на подробные сведения о коде hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-154">Let's look at details about hello code.</span></span>

<span data-ttu-id="6c3d0-155">Первая строка Hello предназначена для `scopes`.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-155">hello first string is for `scopes`.</span></span>  <span data-ttu-id="6c3d0-156">Hello `User.Read` значение позволяет tooread hello базовый профиль hello вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-156">hello `User.Read` value allows you tooread hello basic profile of hello signed in user.</span></span>

<span data-ttu-id="6c3d0-157">Дополнительные сведения о всех доступных областей hello в [области разрешений Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="6c3d0-157">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="6c3d0-158">Для `authURL`, `loginURL`, `bhh`, и `tokenURL`, следует использовать значения hello, указанным ранее.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-158">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use hello values provided previously.</span></span> <span data-ttu-id="6c3d0-159">При использовании hello открытой библиотеки удостоверений Microsoft Azure, мы подтягивают эти данные можно с помощью конечной точки метаданных.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-159">If you use hello open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="6c3d0-160">Мы сделали hello непростая работа по извлечением эти значения.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-160">We've done hello hard work of extracting these values for you.</span></span>

<span data-ttu-id="6c3d0-161">Hello `keychain` значение — контейнер hello, hello NXOAuth2Client библиотеки будет использовать toocreate toostore цепочки ключей маркеры.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-161">hello `keychain` value is hello container that hello NXOAuth2Client library will use toocreate a keychain toostore your tokens.</span></span> <span data-ttu-id="6c3d0-162">Если вы хотите tooget единого входа (SSO) для различных приложений, можно указать же цепочке ключей в каждое приложение hello и запросить hello использование этой цепочке ключей в Xcode прав.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-162">If you'd like tooget single sign-on (SSO) across numerous apps, you can specify hello same keychain in each of your applications and request hello use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="6c3d0-163">Это описывается в документации Apple hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-163">This is explained in hello Apple documentation.</span></span>

<span data-ttu-id="6c3d0-164">остальные Hello эти значения требуется toouse hello библиотеку и создавать местах toocarry значения toohello контекста.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-164">hello rest of these values are required toouse hello library and create places for you toocarry values toohello context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="6c3d0-165">Создание кэша URL-адресов</span><span class="sxs-lookup"><span data-stu-id="6c3d0-165">Create a URL cache</span></span>
<span data-ttu-id="6c3d0-166">Внутри `(void)viewDidLoad()`, который всегда вызывается после загрузки представление hello, hello следующий код primes кэш для наших использования.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-166">Inside `(void)viewDidLoad()`, which is always called after hello view is loaded, hello following code primes a cache for our use.</span></span>

<span data-ttu-id="6c3d0-167">Добавьте следующий код hello:</span><span class="sxs-lookup"><span data-stu-id="6c3d0-167">Add hello following code:</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="6c3d0-168">Создание веб-представления для входа в систему</span><span class="sxs-lookup"><span data-stu-id="6c3d0-168">Create a WebView for sign-in</span></span>
<span data-ttu-id="6c3d0-169">WebView можно запрашивать пользователя hello дополнительные факторы, такие как SMS-сообщение (если настроено) или возвращать ошибки сообщения toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-169">A WebView can prompt hello user for additional factors like SMS text message (if configured) or return error messages toohello user.</span></span> <span data-ttu-id="6c3d0-170">Здесь будет настроить hello WebView и последующем hello записи обратные вызовы кода toohandle hello, которые будут происходить в hello WebView из службы удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-170">Here you'll set up hello WebView and then later write hello code toohandle hello callbacks that will happen in hello WebView from hello identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a><span data-ttu-id="6c3d0-171">Переопределите методы toohandle hello WebView аутентификации</span><span class="sxs-lookup"><span data-stu-id="6c3d0-171">Override hello WebView methods toohandle authentication</span></span>
<span data-ttu-id="6c3d0-172">hello tootell WebView, что происходит, когда пользователю требуется toosign в как отмечалось ранее, можно вставить после кода hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-172">tootell hello WebView what happens when a user needs toosign in as discussed previously, you can paste hello following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a><span data-ttu-id="6c3d0-173">Записи результата hello toohandle кода hello запрос OAuth2</span><span class="sxs-lookup"><span data-stu-id="6c3d0-173">Write code toohandle hello result of hello OAuth2 request</span></span>
<span data-ttu-id="6c3d0-174">Hello следующий код будет обрабатывать redirectURL hello, возвращенный hello WebView.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-174">hello following code will handle hello redirectURL that returns from hello WebView.</span></span> <span data-ttu-id="6c3d0-175">Если проверка подлинности не удалась, кода hello повторит попытку.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-175">If authentication wasn't successful, hello code will try again.</span></span> <span data-ttu-id="6c3d0-176">В свою очередь библиотека hello предоставит hello ошибки, можно просмотреть в консоли hello или асинхронная обработка.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-176">Meanwhile, hello library will provide hello error that you can see in hello console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a><span data-ttu-id="6c3d0-177">Настройка hello OAuth контекста (называемые хранилище учетных записей)</span><span class="sxs-lookup"><span data-stu-id="6c3d0-177">Set up hello OAuth Context (called account store)</span></span>
<span data-ttu-id="6c3d0-178">Здесь вы можете вызвать `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` hello общей учетной записи хранилища для каждой службы, которые должны tooaccess может toobe приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-178">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on hello shared account store for each service that you want hello application toobe able tooaccess.</span></span> <span data-ttu-id="6c3d0-179">Hello тип учетной записи — это строка, который используется в качестве идентификатора для определенной службе.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-179">hello account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="6c3d0-180">Так как вы обращаетесь hello Graph API, код hello ссылается tooit как `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-180">Because you are accessing hello Graph API, hello code refers tooit as `"myGraphService"`.</span></span> <span data-ttu-id="6c3d0-181">Затем устанавливается наблюдатель, сообщит, что-либо изменения с маркером hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-181">You then set up an observer that will tell you when anything changes with hello token.</span></span> <span data-ttu-id="6c3d0-182">После получения маркера hello вернетесь назад toohello hello пользователя `masterView`.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-182">After you get hello token, you return hello user back toohello `masterView`.</span></span>

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a><span data-ttu-id="6c3d0-183">Настройка toosearch образец hello и отображение hello пользователям hello Graph API</span><span class="sxs-lookup"><span data-stu-id="6c3d0-183">Set up hello Master View toosearch and display hello users from hello Graph API</span></span>
<span data-ttu-id="6c3d0-184">Приложение Master-View-Controller (MVC), которое отображает hello вернул данные в сетке hello выходит за рамки этого руководства hello и объясняются многие учебники по сети как один toobuild.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-184">A Master-View-Controller (MVC) app that displays hello returned data in hello grid is beyond hello scope of this walkthrough, and many online tutorials explain how toobuild one.</span></span> <span data-ttu-id="6c3d0-185">Этот код — в файле каркас hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-185">All this code is in hello skeleton file.</span></span> <span data-ttu-id="6c3d0-186">Однако следует соблюдать toodeal некоторые моменты в MVC-приложении:</span><span class="sxs-lookup"><span data-stu-id="6c3d0-186">However, you do need toodeal with a few things in this MVC application:</span></span>

* <span data-ttu-id="6c3d0-187">Отсекаемый отрезок, когда что-нибудь пользователем в поле поиска hello</span><span class="sxs-lookup"><span data-stu-id="6c3d0-187">Intercept when a user types something in hello search field</span></span>
* <span data-ttu-id="6c3d0-188">Обеспечивает объект данных назад toohello MasterView, поэтому он может отображать результаты hello в сетке hello</span><span class="sxs-lookup"><span data-stu-id="6c3d0-188">Provide an object of data back toohello MasterView so it can display hello results in hello grid</span></span>

<span data-ttu-id="6c3d0-189">Мы выполним это далее.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-189">We'll do those below.</span></span>

### <a name="add-a-check-toosee-if-youre-logged-in"></a><span data-ttu-id="6c3d0-190">Добавить toosee флажок, если вы выполнили вход</span><span class="sxs-lookup"><span data-stu-id="6c3d0-190">Add a check toosee if you're logged in</span></span>
<span data-ttu-id="6c3d0-191">приложение Hello мало Если не hello пользователь не выполнил вход, поэтому, смарт-toocheck еще маркера в кэше hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-191">hello application does little if hello user is not signed in, so it's smart toocheck if there is already a token in hello cache.</span></span> <span data-ttu-id="6c3d0-192">Если нет, выполняется перенаправление toohello LoginView для пользователя toosign hello в.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-192">If not, you redirect toohello LoginView for hello user toosign in.</span></span> <span data-ttu-id="6c3d0-193">Если вы вспомните hello лучшим способом toodo действий при загрузке представления — toouse hello `viewDidLoad()` метод, который предоставляет Apple.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-193">If you recall, hello best way toodo actions when a view loads is toouse hello `viewDidLoad()` method that Apple provides us.</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-hello-table-view-when-data-is-received"></a><span data-ttu-id="6c3d0-194">Обновление таблицы представления hello при получении данных</span><span class="sxs-lookup"><span data-stu-id="6c3d0-194">Update hello Table View when data is received</span></span>
<span data-ttu-id="6c3d0-195">Когда hello Graph API возвращает данные, вам нужно toodisplay hello данных.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-195">When hello Graph API returns data, you need toodisplay hello data.</span></span> <span data-ttu-id="6c3d0-196">Для простоты вот все hello кода tooupdate hello для таблицы.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-196">For simplicity, here is all hello code tooupdate hello table.</span></span> <span data-ttu-id="6c3d0-197">Можно просто вставить hello правильные значения в коде шаблона MVC.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-197">You can just paste hello right values in your MVC boilerplate code.</span></span>

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a><span data-ttu-id="6c3d0-198">Предоставляют способ toocall hello Graph API, когда пользователь вводит в поле поиска hello</span><span class="sxs-lookup"><span data-stu-id="6c3d0-198">Provide a way toocall hello Graph API when someone types in hello search field</span></span>
<span data-ttu-id="6c3d0-199">Когда пользователь вводит поиска в поле hello, вам нужно tooshove, через toohello Graph API.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-199">When a user types a search in hello box, you need tooshove that over toohello Graph API.</span></span> <span data-ttu-id="6c3d0-200">Hello `GraphAPICaller` класс, который будет делать в hello после кода, разделяющую функцию поиска hello hello презентации.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-200">hello `GraphAPICaller` class, which you will build in hello following code, separates hello lookup functionality from hello presentation.</span></span> <span data-ttu-id="6c3d0-201">Теперь напишем hello код, передающий любой поиска символов toohello Graph API.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-201">For now, let's write hello code that feeds any search characters toohello Graph API.</span></span> <span data-ttu-id="6c3d0-202">Это реализуется путем предоставления метода с названием `lookupInGraph`, который принимает строку hello, мы хотим toosearch для.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-202">We do this by providing a method called `lookupInGraph`, which takes hello string that we want toosearch for.</span></span>

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a><span data-ttu-id="6c3d0-203">Запись hello tooaccess класса поддержки Graph API</span><span class="sxs-lookup"><span data-stu-id="6c3d0-203">Write a Helper class tooaccess hello Graph API</span></span>
<span data-ttu-id="6c3d0-204">Это ядро hello нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-204">This is hello core of our application.</span></span> <span data-ttu-id="6c3d0-205">В то время как hello rest Вставка кода в шаблоне MVC по умолчанию hello из Apple, здесь вы записи граф hello tooquery кода hello пользователем и затем вернуть эти данные.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-205">Whereas hello rest was inserting code in hello default MVC pattern from Apple, here you write code tooquery hello graph as hello user types and then return that data.</span></span> <span data-ttu-id="6c3d0-206">Ниже приведен код hello и подробное описание следующим элементом.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-206">Here's hello code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="6c3d0-207">Создание нового файла заголовка Objective C</span><span class="sxs-lookup"><span data-stu-id="6c3d0-207">Create a new Objective C header file</span></span>
<span data-ttu-id="6c3d0-208">Имя файла hello `GraphAPICaller.h`и добавьте следующий код hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-208">Name hello file `GraphAPICaller.h`, and add hello following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="6c3d0-209">Как видно, указанный метод принимает строку и возвращает параметр completionBlock.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-209">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="6c3d0-210">Этот completionBlock как можно было предположить, будет обновить таблицы hello, предоставив объект заполненный данными в режиме реального времени как hello поиск пользователя.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-210">This completionBlock, as you may have guessed, will update hello table by providing an object with populated data in real time as hello user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="6c3d0-211">Создание нового файла Objective C</span><span class="sxs-lookup"><span data-stu-id="6c3d0-211">Create a new Objective C file</span></span>
<span data-ttu-id="6c3d0-212">Имя файла hello `GraphAPICaller.m`и добавьте следующий метод hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-212">Name hello file `GraphAPICaller.m`, and add hello following method.</span></span>

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

<span data-ttu-id="6c3d0-213">Разберем этот метод по-подробнее.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-213">Let's go through this method in detail.</span></span>

<span data-ttu-id="6c3d0-214">Hello этот код лежит в hello `NXOAuth2Request`, метод, который принимает параметры hello, который уже определен в файле settings.plist hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-214">hello core of this code is in hello `NXOAuth2Request`, method which takes hello parameters that you've already defined in hello settings.plist file.</span></span>

<span data-ttu-id="6c3d0-215">Hello первым шагом является вызов функции right Graph API tooconstruct hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-215">hello first step is tooconstruct hello right Graph API call.</span></span> <span data-ttu-id="6c3d0-216">Поскольку вы вызываете `/users`, укажите, добавляя ресурса Graph API toohello вместе с версией hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-216">Because you are calling `/users`, you specify that by appending it toohello Graph API resource along with hello version.</span></span> <span data-ttu-id="6c3d0-217">Таким образом смысле tooput их в файл параметров внешней так как их можно изменить по мере развития hello API.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-217">It makes sense tooput these in an external settings file because these can change as hello API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="6c3d0-218">Далее необходимо toospecify параметров также предоставит toohello вызова Graph API.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-218">Next, you need toospecify parameters that you will also provide toohello Graph API call.</span></span> <span data-ttu-id="6c3d0-219">Это *очень важным* , не размещать параметры hello в конечной точке hello ресурсов, поскольку, теряет для всех соответствующих символов не URI во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-219">It is *very important* that you do not put hello parameters in hello resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="6c3d0-220">Весь код запроса необходимо указать в параметрах hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-220">All query code must be provided in hello parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="6c3d0-221">Вы могли заметить, что этот код вызывает метод `convertParamsToDictionary` , который вы еще не написали.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-221">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="6c3d0-222">Давайте теперь выполните конце hello hello файла:</span><span class="sxs-lookup"><span data-stu-id="6c3d0-222">Let's do so now at hello end of hello file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="6c3d0-223">Далее используем hello `NXOAuth2Request` метод tooget данные обратно из hello API в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-223">Next, let's use hello `NXOAuth2Request` method tooget data back from hello API in JSON format.</span></span>

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="6c3d0-224">Наконец давайте взглянем на способы возврата данных hello toohello MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-224">Finally, let's look at how you return hello data toohello MasterViewController.</span></span> <span data-ttu-id="6c3d0-225">данных Hello возвращает, как сериализовать и десериализовать toobe должен и загружены в объект можно использовать, MainViewController hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-225">hello data returns as serialized and needs toobe deserialized and loaded in an object that hello MainViewController can consume.</span></span> <span data-ttu-id="6c3d0-226">Для этой цели имеет основу hello `User.m/h` файла при создании объекта-пользователя.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-226">For this purpose, hello skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="6c3d0-227">Необходимо заполнить данными из графа hello данного объекта-пользователя.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-227">You populate that User object with information from hello graph.</span></span>

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-hello-sample"></a><span data-ttu-id="6c3d0-228">Запуск образца hello</span><span class="sxs-lookup"><span data-stu-id="6c3d0-228">Run hello sample</span></span>
<span data-ttu-id="6c3d0-229">Если используется основу hello или за вместе с hello Пошаговое руководство приложения следует выполнять.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-229">If you've used hello skeleton or followed along with hello walkthrough your application should now run.</span></span> <span data-ttu-id="6c3d0-230">Запустить симулятор hello и нажмите кнопку **входа** toouse приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-230">Start hello simulator and click **Sign in** toouse hello application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="6c3d0-231">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="6c3d0-231">Get security updates for our product</span></span>
<span data-ttu-id="6c3d0-232">Мы рекомендуем вам уведомления при возникновении события безопасности, перейдя по адресу hello tooget [Технический центр безопасности](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.</span><span class="sxs-lookup"><span data-stu-id="6c3d0-232">We encourage you tooget notifications of when security incidents occur by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

