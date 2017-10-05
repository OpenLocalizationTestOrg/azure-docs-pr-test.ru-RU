---
title: "Добавление функции входа в приложение iOS с помощью конечной точки Azure AD версии 2.0 | Документация Майкрософт"
description: "Узнайте, как создать приложение iOS, которое поддерживает вход пользователей в систему с помощью личной, рабочей и учебной учетной записи Майкрософт, используя сторонние библиотеки."
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
ms.openlocfilehash: cf1455dc3d55ea3581195f7a315556d134c23a26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-ios-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="baed2-103">Добавление функции входа в приложение iOS, использующее стороннюю библиотеку и API Graph, с помощью конечной точки версии 2.0</span><span class="sxs-lookup"><span data-stu-id="baed2-103">Add sign-in to an iOS app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="baed2-104">Платформа Microsoft Identity использует открытые стандарты, такие как OAuth2 и OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="baed2-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="baed2-105">Разработчики могут использовать любую библиотеку на свой выбор для интеграции с нашими службами.</span><span class="sxs-lookup"><span data-stu-id="baed2-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="baed2-106">Чтобы помочь разработчикам с использованием нашей платформы с другими библиотеками, мы написали несколько подобных этому пошаговых руководств по настройке сторонних библиотеки для подключения к платформе Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="baed2-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="baed2-107">Большинство библиотек, в которых реализована [спецификация RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) , могут подключаться к платформе Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="baed2-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="baed2-108">Используя приложение, создаваемое в этом пошаговом руководстве, пользователи смогут войти в инфраструктуру своей организации и найти там других пользователей с помощью API Graph.</span><span class="sxs-lookup"><span data-stu-id="baed2-108">With the application that this walkthrough creates, users can sign in to their organization and then search for others in their organization by using the Graph API.</span></span>

<span data-ttu-id="baed2-109">Если вы еще не работали с OAuth2 или OpenID Connect, то вы не поймете большую часть примера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="baed2-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="baed2-110">Рекомендуем сначала ознакомиться со статьей [Протоколы версии 2.0 — поток кода авторизации OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="baed2-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="baed2-111">Чтобы использовать функции платформы, которые описаны в этих стандартах OAuth2 или OpenID Connect, такие как управление политиками условного доступа и управление политиками Intune, требуются библиотеки Microsoft Azure Identity с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="baed2-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="baed2-112">Не все сценарии и компоненты Azure Active Directory поддерживаются конечной точкой версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="baed2-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="baed2-113">Чтобы определить, следует ли вам использовать конечную точку версии 2.0, ознакомьтесь с [ограничениями версии 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="baed2-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="baed2-114">Скачивание кода с сайта GitHub</span><span class="sxs-lookup"><span data-stu-id="baed2-114">Download code from GitHub</span></span>
<span data-ttu-id="baed2-115">Код в этом учебнике размещен на портале [GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="baed2-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="baed2-116">Для понимания процесса можно [скачать основу приложения как ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) или клонировать ее:</span><span class="sxs-lookup"><span data-stu-id="baed2-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="baed2-117">Можно также просто скачать пример и немедленно приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="baed2-117">You can also just download the sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="baed2-118">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="baed2-118">Register an app</span></span>
<span data-ttu-id="baed2-119">Создайте новое приложение на [портале регистрации приложений](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните подробные инструкции по [регистрации приложения с использованием конечной точки версии 2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="baed2-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at  [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="baed2-120">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="baed2-120">Make sure to:</span></span>

* <span data-ttu-id="baed2-121">Скопируйте назначенный вашему приложению **идентификатор приложения**. Он вскоре вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="baed2-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="baed2-122">Добавьте для приложения **мобильную** платформу.</span><span class="sxs-lookup"><span data-stu-id="baed2-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="baed2-123">Скопируйте значение **URI перенаправления** с портала.</span><span class="sxs-lookup"><span data-stu-id="baed2-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="baed2-124">Необходимо использовать стандартное значение `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="baed2-124">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-the-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="baed2-125">Скачивание сторонней библиотеки NXOAuth2 и создание рабочей области</span><span class="sxs-lookup"><span data-stu-id="baed2-125">Download the third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="baed2-126">В этом пошаговом руководстве будет использоваться библиотека OAuth2Client с сайта GitHub. Это библиотека OAuth2 для Mac OS X и iOS (Cocoa и Cocoa Touch).</span><span class="sxs-lookup"><span data-stu-id="baed2-126">For this walkthrough, you will use the OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="baed2-127">В ее основе лежит черновая версия (10) спецификации OAuth2.</span><span class="sxs-lookup"><span data-stu-id="baed2-127">This library is based on draft 10 of the OAuth2 spec.</span></span> <span data-ttu-id="baed2-128">Она реализует профиль собственного приложения и поддерживает конечную точку авторизации пользователей.</span><span class="sxs-lookup"><span data-stu-id="baed2-128">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="baed2-129">Это все, что вам потребуется для интеграции с платформой Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="baed2-129">These are all the things you'll need to integrate with the Microsoft identity platform.</span></span>

### <a name="add-the-library-to-your-project-by-using-cocoapods"></a><span data-ttu-id="baed2-130">Добавление библиотеки в проект с помощью CocoaPods</span><span class="sxs-lookup"><span data-stu-id="baed2-130">Add the library to your project by using CocoaPods</span></span>
<span data-ttu-id="baed2-131">CocoaPods — это диспетчер зависимостей для проектов Xcode.</span><span class="sxs-lookup"><span data-stu-id="baed2-131">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="baed2-132">Он автоматически управляет приведенными выше шагами установки.</span><span class="sxs-lookup"><span data-stu-id="baed2-132">It manages the previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="baed2-133">Добавьте в файл Podfile следующий код:</span><span class="sxs-lookup"><span data-stu-id="baed2-133">Add the following to this podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="baed2-134">Скачайте файл Podfile с помощью CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="baed2-134">Load the podfile by using CocoaPods.</span></span> <span data-ttu-id="baed2-135">Будет создана новая рабочая область Xcode.</span><span class="sxs-lookup"><span data-stu-id="baed2-135">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-the-structure-of-the-project"></a><span data-ttu-id="baed2-136">Изучение структуры проекта</span><span class="sxs-lookup"><span data-stu-id="baed2-136">Explore the structure of the project</span></span>
<span data-ttu-id="baed2-137">В основе настроена следующая структура проекта.</span><span class="sxs-lookup"><span data-stu-id="baed2-137">The following structure is set up for our project in the skeleton:</span></span>

* <span data-ttu-id="baed2-138">Основное представление с поиском имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="baed2-138">A Master View with a UPN Search</span></span>
* <span data-ttu-id="baed2-139">Подробное представление с данными выбранного пользователя.</span><span class="sxs-lookup"><span data-stu-id="baed2-139">A Detail View for the data about the selected user</span></span>
* <span data-ttu-id="baed2-140">Представление входа, которое позволяет пользователю входить в приложение для запроса Graph.</span><span class="sxs-lookup"><span data-stu-id="baed2-140">A Login View where a user can sign in to the app to query the graph</span></span>

<span data-ttu-id="baed2-141">Мы будем использовать различные файлы, входящие в основу, для добавления аутентификации.</span><span class="sxs-lookup"><span data-stu-id="baed2-141">We will move to various files in the skeleton to add authentication.</span></span> <span data-ttu-id="baed2-142">Другие части кода, например код визуального элемента, не относятся к идентификации, но также предоставляются.</span><span class="sxs-lookup"><span data-stu-id="baed2-142">Other parts of the code, such as the visual code, do not pertain to identity but are provided for you.</span></span>

## <a name="set-up-the-settingsplst-file-in-the-library"></a><span data-ttu-id="baed2-143">Настройка файла settings.plst в библиотеке</span><span class="sxs-lookup"><span data-stu-id="baed2-143">Set up the settings.plst file in the library</span></span>
* <span data-ttu-id="baed2-144">В проекте QuickStart откройте файл `settings.plist` .</span><span class="sxs-lookup"><span data-stu-id="baed2-144">In the QuickStart project, open the `settings.plist` file.</span></span> <span data-ttu-id="baed2-145">Замените значения элементов в соответствующем разделе на значения, указанные на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="baed2-145">Replace the values of the elements in the section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="baed2-146">Код будет использовать эти значения при каждом использовании библиотеки аутентификации Active Directory.</span><span class="sxs-lookup"><span data-stu-id="baed2-146">Your code will reference these values whenever it uses the Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="baed2-147">Для `clientId` укажите скопированный на портале идентификатор клиента приложения.</span><span class="sxs-lookup"><span data-stu-id="baed2-147">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="baed2-148">Для `redirectUri` укажите URL-адрес перенаправления, предоставленный на портале.</span><span class="sxs-lookup"><span data-stu-id="baed2-148">The `redirectUri` is the redirect URL that the portal provided.</span></span>

## <a name="set-up-the-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="baed2-149">Настройка библиотеки NXOAuth2Client в LoginViewController</span><span class="sxs-lookup"><span data-stu-id="baed2-149">Set up the NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="baed2-150">Для библиотеки NXOAuth2Client необходимо задать некоторые значения.</span><span class="sxs-lookup"><span data-stu-id="baed2-150">The NXOAuth2Client library requires some values to get set up.</span></span> <span data-ttu-id="baed2-151">После выполнения этой задачи полученный токен можно будет использовать для вызова API Graph.</span><span class="sxs-lookup"><span data-stu-id="baed2-151">After you complete that task, you can use the acquired token to call the Graph API.</span></span> <span data-ttu-id="baed2-152">Так как `LoginView` вызывается в любое время, когда требуется аутентификация, то имеет смысл поместить в этот файл значения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="baed2-152">Because `LoginView` will be called any time we need to authenticate, it makes sense to put configuration values in to that file.</span></span>

* <span data-ttu-id="baed2-153">Добавим несколько значений в файл `LoginViewController.m` , чтобы задать контекст для аутентификации и авторизации.</span><span class="sxs-lookup"><span data-stu-id="baed2-153">Let's add some values to the  `LoginViewController.m` file to set the context for authentication and authorization.</span></span> <span data-ttu-id="baed2-154">Описание значений указано после кода.</span><span class="sxs-lookup"><span data-stu-id="baed2-154">Details about the values follow the code.</span></span>
  
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

<span data-ttu-id="baed2-155">Давайте взглянем на сведения о коде.</span><span class="sxs-lookup"><span data-stu-id="baed2-155">Let's look at details about the code.</span></span>

<span data-ttu-id="baed2-156">Первая строка — для `scopes`.</span><span class="sxs-lookup"><span data-stu-id="baed2-156">The first string is for `scopes`.</span></span>  <span data-ttu-id="baed2-157">Значение `User.Read` позволяет считывать базовый профиль вошедшего пользователя.</span><span class="sxs-lookup"><span data-stu-id="baed2-157">The `User.Read` value allows you to read the basic profile of the signed in user.</span></span>

<span data-ttu-id="baed2-158">Дополнительные сведения о всех доступных областях действия см. в разделе [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes) (Области действия разрешений Microsoft Graph).</span><span class="sxs-lookup"><span data-stu-id="baed2-158">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="baed2-159">Для `authURL`, `loginURL`, `bhh` и `tokenURL` следует использовать значения, заданные ранее.</span><span class="sxs-lookup"><span data-stu-id="baed2-159">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use the values provided previously.</span></span> <span data-ttu-id="baed2-160">При использовании библиотек Microsoft Azure Identity с открытым кодом эти данные можно получить с помощью конечной точки метаданных.</span><span class="sxs-lookup"><span data-stu-id="baed2-160">If you use the open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="baed2-161">Мы уже сделали все за вас и извлекли эти значения.</span><span class="sxs-lookup"><span data-stu-id="baed2-161">We've done the hard work of extracting these values for you.</span></span>

<span data-ttu-id="baed2-162">Значение `keychain` — это контейнер, который будет использовать библиотека NXOAuth2Client, чтобы создать цепочку ключей для хранения токенов.</span><span class="sxs-lookup"><span data-stu-id="baed2-162">The `keychain` value is the container that the NXOAuth2Client library will use to create a keychain to store your tokens.</span></span> <span data-ttu-id="baed2-163">Если вы хотите настроить единый вход для множества приложений, то можно указать одну и ту же цепочку ключей в каждом приложении и запросить ее использование в рамках объема обслуживания XCode.</span><span class="sxs-lookup"><span data-stu-id="baed2-163">If you'd like to get single sign-on (SSO) across numerous apps, you can specify the same keychain in each of your applications and request the use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="baed2-164">Это подробно описано в документации Apple.</span><span class="sxs-lookup"><span data-stu-id="baed2-164">This is explained in the Apple documentation.</span></span>

<span data-ttu-id="baed2-165">Остальные значения требуются для использования библиотеки. Они необходимы для передачи значений в контекст.</span><span class="sxs-lookup"><span data-stu-id="baed2-165">The rest of these values are required to use the library and create places for you to carry values to the context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="baed2-166">Создание кэша URL-адресов</span><span class="sxs-lookup"><span data-stu-id="baed2-166">Create a URL cache</span></span>
<span data-ttu-id="baed2-167">В функции `(void)viewDidLoad()`, которая всегда вызывается после загрузки представления, следующий код обеспечивает кэш для использования.</span><span class="sxs-lookup"><span data-stu-id="baed2-167">Inside `(void)viewDidLoad()`, which is always called after the view is loaded, the following code primes a cache for our use.</span></span>

<span data-ttu-id="baed2-168">Добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="baed2-168">Add the following code:</span></span>

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

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="baed2-169">Создание веб-представления для входа в систему</span><span class="sxs-lookup"><span data-stu-id="baed2-169">Create a WebView for sign-in</span></span>
<span data-ttu-id="baed2-170">Веб-представление может запрашивать у пользователя дополнительные факторы, например SMS-сообщение (если настроено), или возвращать ему сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="baed2-170">A WebView can prompt the user for additional factors like SMS text message (if configured) or return error messages to the user.</span></span> <span data-ttu-id="baed2-171">Вы настроите веб-представление, а затем запрограммируете обработку обратных вызовов, которые будут выполняться в этом представлении, из службы идентификации.</span><span class="sxs-lookup"><span data-stu-id="baed2-171">Here you'll set up the WebView and then later write the code to handle the callbacks that will happen in the WebView from the identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //to sign in to Microsoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate to the URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-the-webview-methods-to-handle-authentication"></a><span data-ttu-id="baed2-172">Переопределение методов веб-представления для обработки проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="baed2-172">Override the WebView methods to handle authentication</span></span>
<span data-ttu-id="baed2-173">Чтобы сообщить веб-представлению о том, что происходит, когда пользователю нужно выполнить вход, как обсуждалось ранее, можно вставить следующий код.</span><span class="sxs-lookup"><span data-stu-id="baed2-173">To tell the WebView what happens when a user needs to sign in as discussed previously, you can paste the following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get the auth token from a redirect so we need to handle that in the webview.

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

    // The webview is where all the communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if the UIWebView is showing our authorization URL or consent URL, show the UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read the Location from the UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by the redirect URL we chose to use from Microsoft APIs
        //continue the OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-to-handle-the-result-of-the-oauth2-request"></a><span data-ttu-id="baed2-174">Написание кода для обработки результатов запроса OAuth2</span><span class="sxs-lookup"><span data-stu-id="baed2-174">Write code to handle the result of the OAuth2 request</span></span>
<span data-ttu-id="baed2-175">Следующий код будет обрабатывать redirectURL, возвращаемый веб-представлением.</span><span class="sxs-lookup"><span data-stu-id="baed2-175">The following code will handle the redirectURL that returns from the WebView.</span></span> <span data-ttu-id="baed2-176">Если аутентификация не будет пройдена, код повторит попытку.</span><span class="sxs-lookup"><span data-stu-id="baed2-176">If authentication wasn't successful, the code will try again.</span></span> <span data-ttu-id="baed2-177">В то же время библиотека сообщит об этой ошибке, которую можно будет просмотреть в консоли или обработать асинхронно.</span><span class="sxs-lookup"><span data-stu-id="baed2-177">Meanwhile, the library will provide the error that you can see in the console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse the response for success or failure
     if (accessResult)
    //if success, complete the OAuth2 flow by handling the redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-the-oauth-context-called-account-store"></a><span data-ttu-id="baed2-178">Настройка контекста OAuth (вызываемого хранилища учетных записей)</span><span class="sxs-lookup"><span data-stu-id="baed2-178">Set up the OAuth Context (called account store)</span></span>
<span data-ttu-id="baed2-179">Вы можете вызвать `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` для общего хранилища учетных записей для каждой службы, к которой у вашего приложения должен быть доступ.</span><span class="sxs-lookup"><span data-stu-id="baed2-179">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on the shared account store for each service that you want the application to be able to access.</span></span> <span data-ttu-id="baed2-180">Учетная запись имеет тип "строка", который используется в качестве идентификатора для определенной службы.</span><span class="sxs-lookup"><span data-stu-id="baed2-180">The account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="baed2-181">Так как вы обращаетесь к API Graph, код ссылается на него как на `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="baed2-181">Because you are accessing the Graph API, the code refers to it as `"myGraphService"`.</span></span> <span data-ttu-id="baed2-182">Затем вы настроите наблюдатель, который будет сообщать об изменениях токена.</span><span class="sxs-lookup"><span data-stu-id="baed2-182">You then set up an observer that will tell you when anything changes with the token.</span></span> <span data-ttu-id="baed2-183">После получения токена пользователь вернется в `masterView`.</span><span class="sxs-lookup"><span data-stu-id="baed2-183">After you get the token, you return the user back to the `masterView`.</span></span>

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

## <a name="set-up-the-master-view-to-search-and-display-the-users-from-the-graph-api"></a><span data-ttu-id="baed2-184">Настройка основного представления для поиска и отображения пользователей из API Graph</span><span class="sxs-lookup"><span data-stu-id="baed2-184">Set up the Master View to search and display the users from the Graph API</span></span>
<span data-ttu-id="baed2-185">Приложение MVC, которое отображает возвращаемые данные в сетке, выходит за рамки этого пошагового руководства. В Интернете есть много руководств, в которых объясняется, как создать такое приложение.</span><span class="sxs-lookup"><span data-stu-id="baed2-185">A Master-View-Controller (MVC) app that displays the returned data in the grid is beyond the scope of this walkthrough, and many online tutorials explain how to build one.</span></span> <span data-ttu-id="baed2-186">Весь этот код находится в файле основы.</span><span class="sxs-lookup"><span data-stu-id="baed2-186">All this code is in the skeleton file.</span></span> <span data-ttu-id="baed2-187">Однако нужно внести некоторые изменения в это приложение MVC:</span><span class="sxs-lookup"><span data-stu-id="baed2-187">However, you do need to deal with a few things in this MVC application:</span></span>

* <span data-ttu-id="baed2-188">Настроить перехват текста, вводимого пользователем в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="baed2-188">Intercept when a user types something in the search field</span></span>
* <span data-ttu-id="baed2-189">Вернуть объект данных в основное представление, чтобы результаты могли отображаться в сетке.</span><span class="sxs-lookup"><span data-stu-id="baed2-189">Provide an object of data back to the MasterView so it can display the results in the grid</span></span>

<span data-ttu-id="baed2-190">Мы выполним это далее.</span><span class="sxs-lookup"><span data-stu-id="baed2-190">We'll do those below.</span></span>

### <a name="add-a-check-to-see-if-youre-logged-in"></a><span data-ttu-id="baed2-191">Добавление проверки выполнения входа</span><span class="sxs-lookup"><span data-stu-id="baed2-191">Add a check to see if you're logged in</span></span>
<span data-ttu-id="baed2-192">Возможности приложения ограничены, если пользователь не выполнил вход, поэтому целесообразно проверить, существует ли уже токен в кэше.</span><span class="sxs-lookup"><span data-stu-id="baed2-192">The application does little if the user is not signed in, so it's smart to check if there is already a token in the cache.</span></span> <span data-ttu-id="baed2-193">В противном случае осуществляется перенаправление в представление входа в систему, чтобы пользователь мог войти.</span><span class="sxs-lookup"><span data-stu-id="baed2-193">If not, you redirect to the LoginView for the user to sign in.</span></span> <span data-ttu-id="baed2-194">Если вы помните, для выполнения действий при загрузке представления рекомендуется использовать метод `viewDidLoad()` , предоставляемый Apple.</span><span class="sxs-lookup"><span data-stu-id="baed2-194">If you recall, the best way to do actions when a view loads is to use the `viewDidLoad()` method that Apple provides us.</span></span>

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

### <a name="update-the-table-view-when-data-is-received"></a><span data-ttu-id="baed2-195">Обновить представление таблицы при получении данных.</span><span class="sxs-lookup"><span data-stu-id="baed2-195">Update the Table View when data is received</span></span>
<span data-ttu-id="baed2-196">При возвращении данных из API Graph их необходимо отобразить.</span><span class="sxs-lookup"><span data-stu-id="baed2-196">When the Graph API returns data, you need to display the data.</span></span> <span data-ttu-id="baed2-197">Для простоты здесь приведен весь код, необходимый для обновления таблицы.</span><span class="sxs-lookup"><span data-stu-id="baed2-197">For simplicity, here is all the code to update the table.</span></span> <span data-ttu-id="baed2-198">Вы можете просто вставить правильные значения в стандартном коде MVC.</span><span class="sxs-lookup"><span data-stu-id="baed2-198">You can just paste the right values in your MVC boilerplate code.</span></span>

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


    // Configure the cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-to-call-the-graph-api-when-someone-types-in-the-search-field"></a><span data-ttu-id="baed2-199">Указать метод вызова API Graph, когда пользователь вводит текст в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="baed2-199">Provide a way to call the Graph API when someone types in the search field</span></span>
<span data-ttu-id="baed2-200">Когда пользователь вводит текст в поле поиска, необходимо передать его в API Graph.</span><span class="sxs-lookup"><span data-stu-id="baed2-200">When a user types a search in the box, you need to shove that over to the Graph API.</span></span> <span data-ttu-id="baed2-201">Класс `GraphAPICaller` , сборку которого вы выполните в следующем коде, разделяет функции поиска и представления.</span><span class="sxs-lookup"><span data-stu-id="baed2-201">The `GraphAPICaller` class, which you will build in the following code, separates the lookup functionality from the presentation.</span></span> <span data-ttu-id="baed2-202">А пока давайте напишем код, передающий знаки, вводимые при поиске, в API Graph.</span><span class="sxs-lookup"><span data-stu-id="baed2-202">For now, let's write the code that feeds any search characters to the Graph API.</span></span> <span data-ttu-id="baed2-203">Для этого мы укажем метод `lookupInGraph`, принимающий строку, которую нужно найти.</span><span class="sxs-lookup"><span data-stu-id="baed2-203">We do this by providing a method called `lookupInGraph`, which takes the string that we want to search for.</span></span>

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

## <a name="write-a-helper-class-to-access-the-graph-api"></a><span data-ttu-id="baed2-204">Написать вспомогательный класс для доступа к API Graph.</span><span class="sxs-lookup"><span data-stu-id="baed2-204">Write a Helper class to access the Graph API</span></span>
<span data-ttu-id="baed2-205">Это ядро нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="baed2-205">This is the core of our application.</span></span> <span data-ttu-id="baed2-206">Раньше мы вставляли код в шаблон MVC по умолчанию, предоставленный Apple, а теперь вы напишете код для запроса к Graph при вводе и возврата данных.</span><span class="sxs-lookup"><span data-stu-id="baed2-206">Whereas the rest was inserting code in the default MVC pattern from Apple, here you write code to query the graph as the user types and then return that data.</span></span> <span data-ttu-id="baed2-207">Ниже приведен код и пояснения к нему.</span><span class="sxs-lookup"><span data-stu-id="baed2-207">Here's the code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="baed2-208">Создание нового файла заголовка Objective C</span><span class="sxs-lookup"><span data-stu-id="baed2-208">Create a new Objective C header file</span></span>
<span data-ttu-id="baed2-209">Назовите файл `GraphAPICaller.h`и добавьте в него следующий код.</span><span class="sxs-lookup"><span data-stu-id="baed2-209">Name the file `GraphAPICaller.h`, and add the following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="baed2-210">Как видно, указанный метод принимает строку и возвращает параметр completionBlock.</span><span class="sxs-lookup"><span data-stu-id="baed2-210">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="baed2-211">Этот completionBlock, как можно догадаться, будет обновлять таблицу, предоставляя объект с заполненными данными в режиме реального времени во время выполнения поиска пользователем.</span><span class="sxs-lookup"><span data-stu-id="baed2-211">This completionBlock, as you may have guessed, will update the table by providing an object with populated data in real time as the user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="baed2-212">Создание нового файла Objective C</span><span class="sxs-lookup"><span data-stu-id="baed2-212">Create a new Objective C file</span></span>
<span data-ttu-id="baed2-213">Назовите файл `GraphAPICaller.m`и добавьте в него следующий метод.</span><span class="sxs-lookup"><span data-stu-id="baed2-213">Name the file `GraphAPICaller.m`, and add the following method.</span></span>

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
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
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

<span data-ttu-id="baed2-214">Разберем этот метод по-подробнее.</span><span class="sxs-lookup"><span data-stu-id="baed2-214">Let's go through this method in detail.</span></span>

<span data-ttu-id="baed2-215">Ядро этого кода находится в методе `NXOAuth2Request`, который принимает параметры, уже определенные вами в файле settings.plist.</span><span class="sxs-lookup"><span data-stu-id="baed2-215">The core of this code is in the `NXOAuth2Request`, method which takes the parameters that you've already defined in the settings.plist file.</span></span>

<span data-ttu-id="baed2-216">Сначала нужно создать правильный вызов API Graph.</span><span class="sxs-lookup"><span data-stu-id="baed2-216">The first step is to construct the right Graph API call.</span></span> <span data-ttu-id="baed2-217">Так как вызывается `/users`, необходимо указать это, добавив его в ресурс API Graph вместе с версией.</span><span class="sxs-lookup"><span data-stu-id="baed2-217">Because you are calling `/users`, you specify that by appending it to the Graph API resource along with the version.</span></span> <span data-ttu-id="baed2-218">Целесообразно поместить эти данные во внешний файл параметров, так как они могут меняться по мере развития API.</span><span class="sxs-lookup"><span data-stu-id="baed2-218">It makes sense to put these in an external settings file because these can change as the API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="baed2-219">Далее следует задать параметры, которые также указываются в вызове API Graph.</span><span class="sxs-lookup"><span data-stu-id="baed2-219">Next, you need to specify parameters that you will also provide to the Graph API call.</span></span> <span data-ttu-id="baed2-220">*Внимание!* Эти параметры не следует добавлять к конечной точке ресурсов, так как все знаки, не соответствующие формату универсального кода ресурса (URI), удаляются из нее во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="baed2-220">It is *very important* that you do not put the parameters in the resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="baed2-221">В параметрах необходимо указать весь код запроса.</span><span class="sxs-lookup"><span data-stu-id="baed2-221">All query code must be provided in the parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="baed2-222">Вы могли заметить, что этот код вызывает метод `convertParamsToDictionary` , который вы еще не написали.</span><span class="sxs-lookup"><span data-stu-id="baed2-222">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="baed2-223">Давайте добавим его в конце файла:</span><span class="sxs-lookup"><span data-stu-id="baed2-223">Let's do so now at the end of the file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="baed2-224">Теперь мы используем метод `NXOAuth2Request` для получения данных из API в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="baed2-224">Next, let's use the `NXOAuth2Request` method to get data back from the API in JSON format.</span></span>

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
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="baed2-225">Наконец, давайте рассмотрим метод возврата данных в MVC.</span><span class="sxs-lookup"><span data-stu-id="baed2-225">Finally, let's look at how you return the data to the MasterViewController.</span></span> <span data-ttu-id="baed2-226">Данные возвращаются в сериализированном виде. Их необходимо десериализировать и загрузить в объект, который может использовать MVC.</span><span class="sxs-lookup"><span data-stu-id="baed2-226">The data returns as serialized and needs to be deserialized and loaded in an object that the MainViewController can consume.</span></span> <span data-ttu-id="baed2-227">Для этого в основе предусмотрен файл `User.m/h`, который создает объект-пользователь.</span><span class="sxs-lookup"><span data-stu-id="baed2-227">For this purpose, the skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="baed2-228">Вы заполните этот объект-пользователь данными из Graph.</span><span class="sxs-lookup"><span data-stu-id="baed2-228">You populate that User object with information from the graph.</span></span>

```objc
                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
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


## <a name="run-the-sample"></a><span data-ttu-id="baed2-229">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="baed2-229">Run the sample</span></span>
<span data-ttu-id="baed2-230">Если вы использовали основу и выполнили все указания пошагового руководства, приложение должно работать.</span><span class="sxs-lookup"><span data-stu-id="baed2-230">If you've used the skeleton or followed along with the walkthrough your application should now run.</span></span> <span data-ttu-id="baed2-231">Запустите симулятор и нажмите кнопку **Sign in** (Войти), чтобы использовать приложение.</span><span class="sxs-lookup"><span data-stu-id="baed2-231">Start the simulator and click **Sign in** to use the application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="baed2-232">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="baed2-232">Get security updates for our product</span></span>
<span data-ttu-id="baed2-233">Рекомендуем получать уведомления о произошедших инцидентах безопасности. Для этого посетите [технический центр безопасности](https://technet.microsoft.com/security/dd252948) и подпишитесь на уведомления о советах безопасности.</span><span class="sxs-lookup"><span data-stu-id="baed2-233">We encourage you to get notifications of when security incidents occur by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

