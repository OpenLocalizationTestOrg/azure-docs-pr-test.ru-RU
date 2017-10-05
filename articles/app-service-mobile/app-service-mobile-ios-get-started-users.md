---
title: "Добавление проверки подлинности на iOS с помощью мобильных приложений Azure"
description: "Узнайте, как использовать мобильные приложения для проверки подлинности пользователей приложения iOS с помощью разных поставщиков удостоверений, включая AAD, Google, Facebook, Twitter и Майкрософт."
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
ms.openlocfilehash: 21a2cc6c1eaf4b34cbe8c2d7c4dbb69c8730cf32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-ios-app"></a><span data-ttu-id="69776-103">Добавление проверки подлинности в приложение iOS</span><span class="sxs-lookup"><span data-stu-id="69776-103">Add authentication to your iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="69776-104">В этом учебнике описывается добавление проверки подлинности в проект учебника по [быстрому запуску iOS] с помощью поддерживаемого поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="69776-104">In this tutorial, you add authentication to the [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="69776-105">Этот учебник использует материал учебника по [быстрому запуску iOS] , который необходимо пройти в первую очередь.</span><span class="sxs-lookup"><span data-stu-id="69776-105">This tutorial is based on the [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="69776-106"><a name="register"></a>Регистрация приложения для проверки подлинности и настройка службы приложений</span><span class="sxs-lookup"><span data-stu-id="69776-106"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="69776-107"><a name="redirecturl"></a>Добавление приложения в список разрешенных URL-адресов внешнего перенаправления</span><span class="sxs-lookup"><span data-stu-id="69776-107"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="69776-108">Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="69776-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="69776-109">Это позволяет системе аутентификации выполнять перенаправление обратно в приложение после завершения процесса аутентификации.</span><span class="sxs-lookup"><span data-stu-id="69776-109">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span>  <span data-ttu-id="69776-110">В этом руководстве мы повсеместно используем схему URL-адресов _appname_.</span><span class="sxs-lookup"><span data-stu-id="69776-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="69776-111">Тем не менее можно использовать любую схему URL-адресов на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="69776-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="69776-112">Она должна быть уникальной для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="69776-112">It should be unique to your mobile application.</span></span>  <span data-ttu-id="69776-113">Вот как можно включить перенаправление на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="69776-113">To enable the redirection on th server side:</span></span>

1. <span data-ttu-id="69776-114">На [портале Azure] выберите свою службу приложений.</span><span class="sxs-lookup"><span data-stu-id="69776-114">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="69776-115">Выберите пункт меню **Аутентификация или авторизация**.</span><span class="sxs-lookup"><span data-stu-id="69776-115">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="69776-116">В разделе **Поставщики проверки подлинности** щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="69776-116">Click **Azure Active Directory** under the **Authentication Providers** section.</span></span>

4. <span data-ttu-id="69776-117">Для параметра **Режим управления** задайте значение **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="69776-117">Set the **Management mode** to **Advanced**.</span></span>

5. <span data-ttu-id="69776-118">В поле **Разрешенные URL-адреса внешнего перенаправления** введите `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="69776-118">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="69776-119">_appname_ в этой строке — это схема URL-адресов для вашего мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="69776-119">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="69776-120">Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).</span><span class="sxs-lookup"><span data-stu-id="69776-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="69776-121">Необходимо записать выбранную строку, так как потребуется в нескольких местах настроить код мобильного приложения с использованием схемы URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="69776-121">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

6. <span data-ttu-id="69776-122">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="69776-122">Click **OK**.</span></span>

7. <span data-ttu-id="69776-123">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="69776-123">Click **Save**.</span></span>

## <span data-ttu-id="69776-124"><a name="permissions"></a>Предоставление разрешений только пользователям, прошедшим проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="69776-124"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="69776-125">В Xcode нажмите кнопку **Выполнить** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="69776-125">In Xcode, press **Run** to start the app.</span></span> <span data-ttu-id="69776-126">Будет порождено исключение, так как приложение попытается получить доступ к серверной части как пользователь, не прошедший аутентификацию, а для таблицы *TodoItem* теперь требуется аутентификация.</span><span class="sxs-lookup"><span data-stu-id="69776-126">An exception is raised because the app attempts to access the backend as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="69776-127"><a name="add-authentication"></a>Добавление проверки подлинности в приложение</span><span class="sxs-lookup"><span data-stu-id="69776-127"><a name="add-authentication"></a>Add authentication to app</span></span>
<span data-ttu-id="69776-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="69776-128">**Objective-C**:</span></span>

1. <span data-ttu-id="69776-129">На компьютере Mac откройте файл *QSTodoListViewController.m* в Xcode и добавьте следующий метод.</span><span class="sxs-lookup"><span data-stu-id="69776-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add the following method:</span></span>

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

    <span data-ttu-id="69776-130">Измените *google* на *microsoftaccount*, *twitter*, *facebook* или *windowsazureactivedirectory*, если Google не используется как поставщик удостоверений.</span><span class="sxs-lookup"><span data-stu-id="69776-130">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="69776-131">Если используется Facebook, то [требуется добавить домены Facebook в список разрешений][1] в приложении.</span><span class="sxs-lookup"><span data-stu-id="69776-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="69776-132">Замените **urlScheme** уникальным именем своего приложения.</span><span class="sxs-lookup"><span data-stu-id="69776-132">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="69776-133">Значение urlScheme должно быть таким же, как и для протокола схемы URL-адресов, указанного в поле **Разрешенные URL-адреса внешнего перенаправления** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="69776-133">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="69776-134">urlScheme используется при обратном вызове аутентификации для переключения на приложение после завершения запроса аутентификации.</span><span class="sxs-lookup"><span data-stu-id="69776-134">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="69776-135">Замените `[self refresh]` в `viewDidLoad` в файле *QSTodoListViewController.m* следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="69776-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with the following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="69776-136">Откройте файл `QSAppDelegate.h` и добавьте в него следующий код.</span><span class="sxs-lookup"><span data-stu-id="69776-136">Open the `QSAppDelegate.h` file and add the following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="69776-137">Откройте файл `QSAppDelegate.m` и добавьте в него следующий код.</span><span class="sxs-lookup"><span data-stu-id="69776-137">Open the `QSAppDelegate.m` file and add the following code:</span></span>

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

   <span data-ttu-id="69776-138">Добавьте этот код непосредственно перед строкой `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="69776-138">Add this code directly before the line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="69776-139">Замените _appname_ значением urlScheme, указанным на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="69776-139">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="69776-140">Откройте файл `AppName-Info.plist` (замените AppName именем своего приложения) и добавьте в него следующий код.</span><span class="sxs-lookup"><span data-stu-id="69776-140">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

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

    <span data-ttu-id="69776-141">Этот код должен быть помещен в элемент `<dict>`.</span><span class="sxs-lookup"><span data-stu-id="69776-141">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="69776-142">Замените строку _appname_ (в массиве для **CFBundleURLSchemes**) именем приложения, выбранным на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="69776-142">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="69776-143">Внести эти изменения можно также в редакторе PList. Щелкните файл `AppName-Info.plist` в XCode, чтобы открыть редактор PList.</span><span class="sxs-lookup"><span data-stu-id="69776-143">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="69776-144">Замените строку `com.microsoft.azure.zumo` для **CFBundleURLName** идентификатором своего пакета Apple.</span><span class="sxs-lookup"><span data-stu-id="69776-144">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="69776-145">Нажмите кнопку *Выполнить*, чтобы запустить приложение, и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="69776-145">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="69776-146">После входа вы должны увидеть список Todo и сможете вносить изменения.</span><span class="sxs-lookup"><span data-stu-id="69776-146">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="69776-147">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="69776-147">**Swift**:</span></span>

1. <span data-ttu-id="69776-148">На компьютере Mac откройте файл *ToDoTableViewController.swift* в Xcode и добавьте следующий метод.</span><span class="sxs-lookup"><span data-stu-id="69776-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add the following method:</span></span>

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

    <span data-ttu-id="69776-149">Измените *google* на *microsoftaccount*, *twitter*, *facebook* или *windowsazureactivedirectory*, если Google не используется как поставщик удостоверений.</span><span class="sxs-lookup"><span data-stu-id="69776-149">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="69776-150">Если используется Facebook, то [требуется добавить домены Facebook в список разрешений][1] в приложении.</span><span class="sxs-lookup"><span data-stu-id="69776-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="69776-151">Замените **urlScheme** уникальным именем своего приложения.</span><span class="sxs-lookup"><span data-stu-id="69776-151">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="69776-152">Значение urlScheme должно быть таким же, как и для протокола схемы URL-адресов, указанного в поле **Разрешенные URL-адреса внешнего перенаправления** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="69776-152">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="69776-153">urlScheme используется при обратном вызове аутентификации для переключения на приложение после завершения запроса аутентификации.</span><span class="sxs-lookup"><span data-stu-id="69776-153">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="69776-154">Удалите строки `self.refreshControl?.beginRefreshing()` и `self.onRefresh(self.refreshControl)` в конце `viewDidLoad()` в файле *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="69776-154">Remove the lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="69776-155">Добавьте вызов `loginAndGetData()` вместо них:</span><span class="sxs-lookup"><span data-stu-id="69776-155">Add a call to `loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="69776-156">Откройте файл `AppDelegate.swift` и добавьте следующую строку в класс `AppDelegate`.</span><span class="sxs-lookup"><span data-stu-id="69776-156">Open the `AppDelegate.swift` file and add the following line to the `AppDelegate` class:</span></span>

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

    <span data-ttu-id="69776-157">Замените _appname_ значением urlScheme, указанным на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="69776-157">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="69776-158">Откройте файл `AppName-Info.plist` (замените AppName именем своего приложения) и добавьте в него следующий код.</span><span class="sxs-lookup"><span data-stu-id="69776-158">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

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

    <span data-ttu-id="69776-159">Этот код должен быть помещен в элемент `<dict>`.</span><span class="sxs-lookup"><span data-stu-id="69776-159">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="69776-160">Замените строку _appname_ (в массиве для **CFBundleURLSchemes**) именем приложения, выбранным на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="69776-160">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="69776-161">Внести эти изменения можно также в редакторе PList. Щелкните файл `AppName-Info.plist` в XCode, чтобы открыть редактор PList.</span><span class="sxs-lookup"><span data-stu-id="69776-161">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="69776-162">Замените строку `com.microsoft.azure.zumo` для **CFBundleURLName** идентификатором своего пакета Apple.</span><span class="sxs-lookup"><span data-stu-id="69776-162">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="69776-163">Нажмите кнопку *Выполнить*, чтобы запустить приложение, и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="69776-163">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="69776-164">После входа вы должны увидеть список Todo и сможете вносить изменения.</span><span class="sxs-lookup"><span data-stu-id="69776-164">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="69776-165">Для аутентификации службы приложений используется технология взаимодействия приложений Apple.</span><span class="sxs-lookup"><span data-stu-id="69776-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="69776-166">Дополнительные сведения по этой теме доступны в [документации Apple][2].</span><span class="sxs-lookup"><span data-stu-id="69776-166">For more details on this subject, refer to the [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
<span data-ttu-id="69776-167">[портале Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="69776-167">[Azure portal]: https://portal.azure.com</span></span>

<span data-ttu-id="69776-168">[быстрому запуску iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="69776-168">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>

