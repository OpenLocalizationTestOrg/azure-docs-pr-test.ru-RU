---
title: "aaaAdd проверки подлинности в iOS с помощью мобильных приложений Azure"
description: "Узнайте, как toouse мобильных приложений Azure tooauthenticate пользователей приложения iOS с помощью различных поставщиков удостоверений, включая AAD, Google, Facebook, Twitter и Майкрософт."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a><span data-ttu-id="ffcdb-103">Добавление приложения iOS tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="ffcdb-103">Add authentication tooyour iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="ffcdb-104">В этом учебнике добавления проверки подлинности toohello [iOS быстрый запуск] проекта с помощью поставщика удостоверений, поддерживаемых.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-104">In this tutorial, you add authentication toohello [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="ffcdb-105">Этот учебник основывается на hello [iOS быстрый запуск] руководство, в котором необходимо выполнять первой.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-105">This tutorial is based on hello [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="ffcdb-106"><a name="register"></a>Регистрация приложения для проверки подлинности и настройка hello службы приложений</span><span class="sxs-lookup"><span data-stu-id="ffcdb-106"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="ffcdb-107"><a name="redirecturl"></a>Добавить ваш URL-адреса внешнего перенаправления разрешено toohello для приложений</span><span class="sxs-lookup"><span data-stu-id="ffcdb-107"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="ffcdb-108">Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="ffcdb-109">Это позволяет приложение hello проверки подлинности системы tooredirect задней tooyour после завершения процесса проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-109">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span>  <span data-ttu-id="ffcdb-110">В этом руководстве мы повсеместно используем схему URL-адресов _appname_.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="ffcdb-111">Тем не менее можно использовать любую схему URL-адресов на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="ffcdb-112">Он должен быть уникальным tooyour мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-112">It should be unique tooyour mobile application.</span></span>  <span data-ttu-id="ffcdb-113">tooenable hello перенаправления на стороне сервера th:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-113">tooenable hello redirection on th server side:</span></span>

1. <span data-ttu-id="ffcdb-114">В hello [портал Azure], выделите службу приложения.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-114">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="ffcdb-115">Нажмите кнопку hello **проверки подлинности и авторизации** пункт меню.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-115">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="ffcdb-116">Нажмите кнопку **Azure Active Directory** под hello **поставщики проверки подлинности** раздела.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-116">Click **Azure Active Directory** under hello **Authentication Providers** section.</span></span>

4. <span data-ttu-id="ffcdb-117">Набор hello **режим управления** слишком**Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-117">Set hello **Management mode** too**Advanced**.</span></span>

5. <span data-ttu-id="ffcdb-118">В hello **допускается внешний URL-адреса перенаправления**, введите `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-118">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="ffcdb-119">Hello _appname_ в данной строке — hello схема URL-адресов для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-119">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="ffcdb-120">Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).</span><span class="sxs-lookup"><span data-stu-id="ffcdb-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="ffcdb-121">Необходимо записать строку hello, выбранный как он потребуется tooadjust кода приложений для мобильных устройств с hello схема URL-адресов в нескольких местах.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-121">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

6. <span data-ttu-id="ffcdb-122">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-122">Click **OK**.</span></span>

7. <span data-ttu-id="ffcdb-123">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-123">Click **Save**.</span></span>

## <span data-ttu-id="ffcdb-124"><a name="permissions"></a>Ограничить разрешения пользователей tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="ffcdb-124"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="ffcdb-125">В Xcode, нажмите клавишу **запуска** toostart приложение hello.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-125">In Xcode, press **Run** toostart hello app.</span></span> <span data-ttu-id="ffcdb-126">Вызывает исключение, так как приложение hello пытается tooaccess серверной части, не прошедшие проверку подлинности пользователя, но hello *TodoItem* таблица теперь требует проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-126">An exception is raised because hello app attempts tooaccess the backend as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="ffcdb-127"><a name="add-authentication"></a>Добавление проверки подлинности tooapp</span><span class="sxs-lookup"><span data-stu-id="ffcdb-127"><a name="add-authentication"></a>Add authentication tooapp</span></span>
<span data-ttu-id="ffcdb-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-128">**Objective-C**:</span></span>

1. <span data-ttu-id="ffcdb-129">На компьютере Mac откройте *QSTodoListViewController.m* в Xcode и добавьте следующий метод hello:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add hello following method:</span></span>

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    <span data-ttu-id="ffcdb-130">Изменение *google* слишком*microsoftaccount*, *twitter*, *facebook*, или *windowsazureactivedirectory* Если вы не используете как поставщика удостоверений Google.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-130">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="ffcdb-131">Если используется Facebook, то [требуется добавить домены Facebook в список разрешений][1] в приложении.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="ffcdb-132">Замените hello **urlScheme** уникальное имя для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-132">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="ffcdb-133">Hello urlScheme должен быть hello таким же как hello протокола схема URL-адрес, указанный в hello **допускается внешний URL-адреса перенаправления** в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-133">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="ffcdb-134">Hello urlScheme используется приложением hello проверки подлинности обратного вызова tooswitch задней tooyour после завершения проверки подлинности запроса.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-134">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="ffcdb-135">Замените `[self refresh]` в `viewDidLoad` в *QSTodoListViewController.m* с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with hello following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="ffcdb-136">Откройте hello `QSAppDelegate.h` и добавьте следующий код hello файла:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-136">Open hello `QSAppDelegate.h` file and add hello following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="ffcdb-137">Откройте hello `QSAppDelegate.m` и добавьте следующий код hello файла:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-137">Open hello `QSAppDelegate.m` file and add hello following code:</span></span>

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   <span data-ttu-id="ffcdb-138">Добавьте следующий код непосредственно перед чтением строку hello `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-138">Add this code directly before hello line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="ffcdb-139">Замените _appname_ wih hello urlScheme значение, выбранное на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-139">Replace the _appname_ wih hello urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="ffcdb-140">Откройте hello `AppName-Info.plist` (вместо AppName с именем hello приложения) и добавьте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-140">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="ffcdb-141">Этот код следует разместить внутри hello `<dict>` элемента.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-141">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="ffcdb-142">Замените hello _appname_ строки (в массиве, **CFBundleURLSchemes**) с именем приложения hello, выбранное на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-142">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="ffcdb-143">Также внести эти изменения в hello plist редактор - щелкните hello `AppName-Info.plist` файл в редакторе plist hello tooopen XCode.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-143">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="ffcdb-144">Замените hello `com.microsoft.azure.zumo` строка для **CFBundleURLName** с вашей Apple объединить идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-144">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="ffcdb-145">Нажмите клавишу *запуска* toostart приложения hello и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-145">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="ffcdb-146">При входе необходимо будет tooview hello Todo list и обновления.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-146">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="ffcdb-147">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-147">**Swift**:</span></span>

1. <span data-ttu-id="ffcdb-148">На компьютере Mac откройте *ToDoTableViewController.swift* в Xcode и добавьте следующий метод hello:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add hello following method:</span></span>

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    <span data-ttu-id="ffcdb-149">Изменение *google* слишком*microsoftaccount*, *twitter*, *facebook*, или *windowsazureactivedirectory* Если вы не используете как поставщика удостоверений Google.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-149">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="ffcdb-150">Если используется Facebook, то [требуется добавить домены Facebook в список разрешений][1] в приложении.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="ffcdb-151">Замените hello **urlScheme** уникальное имя для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-151">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="ffcdb-152">Hello urlScheme должен быть hello таким же как hello протокола схема URL-адрес, указанный в hello **допускается внешний URL-адреса перенаправления** в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-152">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="ffcdb-153">Hello urlScheme используется приложением hello проверки подлинности обратного вызова tooswitch задней tooyour после завершения проверки подлинности запроса.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-153">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="ffcdb-154">Удалить строки hello `self.refreshControl?.beginRefreshing()` и `self.onRefresh(self.refreshControl)` в конце `viewDidLoad()` в *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-154">Remove hello lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="ffcdb-155">Добавьте вызов слишком`loginAndGetData()` вместо них:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-155">Add a call too`loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="ffcdb-156">Откройте hello `AppDelegate.swift` и добавьте следующие строки toohello hello `AppDelegate` класса:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-156">Open hello `AppDelegate.swift` file and add hello following line toohello `AppDelegate` class:</span></span>

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    <span data-ttu-id="ffcdb-157">Замените hello _appname_ wih hello urlScheme значение, выбранное на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-157">Replace hello _appname_ wih hello urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="ffcdb-158">Откройте hello `AppName-Info.plist` (вместо AppName с именем hello приложения) и добавьте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="ffcdb-158">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="ffcdb-159">Этот код следует разместить внутри hello `<dict>` элемента.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-159">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="ffcdb-160">Замените hello _appname_ строки (в массиве, **CFBundleURLSchemes**) с именем приложения hello, выбранное на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-160">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="ffcdb-161">Также внести эти изменения в hello plist редактор - щелкните hello `AppName-Info.plist` файл в редакторе plist hello tooopen XCode.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-161">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="ffcdb-162">Замените hello `com.microsoft.azure.zumo` строка для **CFBundleURLName** с вашей Apple объединить идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-162">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="ffcdb-163">Нажмите клавишу *запуска* toostart приложения hello и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-163">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="ffcdb-164">При входе необходимо будет tooview hello Todo list и обновления.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-164">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="ffcdb-165">Для аутентификации службы приложений используется технология взаимодействия приложений Apple.</span><span class="sxs-lookup"><span data-stu-id="ffcdb-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="ffcdb-166">Дополнительные сведения по этому вопросу см. в разделе toohello [документации Apple][2]</span><span class="sxs-lookup"><span data-stu-id="ffcdb-166">For more details on this subject, refer toohello [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[портал Azure]: https://portal.azure.com

[iOS быстрый запуск]: app-service-mobile-ios-get-started.md

