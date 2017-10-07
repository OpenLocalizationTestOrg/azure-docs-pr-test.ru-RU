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
# <a name="add-authentication-tooyour-ios-app"></a>Добавление приложения iOS tooyour проверки подлинности
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

В этом учебнике добавления проверки подлинности toohello [iOS быстрый запуск] проекта с помощью поставщика удостоверений, поддерживаемых. Этот учебник основывается на hello [iOS быстрый запуск] руководство, в котором необходимо выполнять первой.

## <a name="register"></a>Регистрация приложения для проверки подлинности и настройка hello службы приложений
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Добавить ваш URL-адреса внешнего перенаправления разрешено toohello для приложений

Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения.  Это позволяет приложение hello проверки подлинности системы tooredirect задней tooyour после завершения процесса проверки подлинности hello.  В этом руководстве мы повсеместно используем схему URL-адресов _appname_.  Тем не менее можно использовать любую схему URL-адресов на свой выбор.  Он должен быть уникальным tooyour мобильного приложения.  tooenable hello перенаправления на стороне сервера th:

1. В hello [портал Azure], выделите службу приложения.

2. Нажмите кнопку hello **проверки подлинности и авторизации** пункт меню.

3. Нажмите кнопку **Azure Active Directory** под hello **поставщики проверки подлинности** раздела.

4. Набор hello **режим управления** слишком**Дополнительно**.

5. В hello **допускается внешний URL-адреса перенаправления**, введите `appname://easyauth.callback`.  Hello _appname_ в данной строке — hello схема URL-адресов для мобильного приложения.  Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).  Необходимо записать строку hello, выбранный как он потребуется tooadjust кода приложений для мобильных устройств с hello схема URL-адресов в нескольких местах.

6. Нажмите кнопку **ОК**.

7. Щелкните **Сохранить**.

## <a name="permissions"></a>Ограничить разрешения пользователей tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

В Xcode, нажмите клавишу **запуска** toostart приложение hello. Вызывает исключение, так как приложение hello пытается tooaccess серверной части, не прошедшие проверку подлинности пользователя, но hello *TodoItem* таблица теперь требует проверки подлинности.

## <a name="add-authentication"></a>Добавление проверки подлинности tooapp
**Objective-C**:

1. На компьютере Mac откройте *QSTodoListViewController.m* в Xcode и добавьте следующий метод hello:

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

    Изменение *google* слишком*microsoftaccount*, *twitter*, *facebook*, или *windowsazureactivedirectory* Если вы не используете как поставщика удостоверений Google. Если используется Facebook, то [требуется добавить домены Facebook в список разрешений][1] в приложении.

    Замените hello **urlScheme** уникальное имя для вашего приложения.  Hello urlScheme должен быть hello таким же как hello протокола схема URL-адрес, указанный в hello **допускается внешний URL-адреса перенаправления** в hello портал Azure. Hello urlScheme используется приложением hello проверки подлинности обратного вызова tooswitch задней tooyour после завершения проверки подлинности запроса.

2. Замените `[self refresh]` в `viewDidLoad` в *QSTodoListViewController.m* с hello, следующий код:

    ```Objective-C
    [self loginAndGetData];
    ```

3. Откройте hello `QSAppDelegate.h` и добавьте следующий код hello файла:

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. Откройте hello `QSAppDelegate.m` и добавьте следующий код hello файла:

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

   Добавьте следующий код непосредственно перед чтением строку hello `#pragma mark - Core Data stack`.  Замените _appname_ wih hello urlScheme значение, выбранное на шаге 1.

5. Откройте hello `AppName-Info.plist` (вместо AppName с именем hello приложения) и добавьте hello, следующий код:

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

    Этот код следует разместить внутри hello `<dict>` элемента.  Замените hello _appname_ строки (в массиве, **CFBundleURLSchemes**) с именем приложения hello, выбранное на шаге 1.  Также внести эти изменения в hello plist редактор - щелкните hello `AppName-Info.plist` файл в редакторе plist hello tooopen XCode.

    Замените hello `com.microsoft.azure.zumo` строка для **CFBundleURLName** с вашей Apple объединить идентификатор.

6. Нажмите клавишу *запуска* toostart приложения hello и войдите в систему. При входе необходимо будет tooview hello Todo list и обновления.

**Swift**:

1. На компьютере Mac откройте *ToDoTableViewController.swift* в Xcode и добавьте следующий метод hello:

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

    Изменение *google* слишком*microsoftaccount*, *twitter*, *facebook*, или *windowsazureactivedirectory* Если вы не используете как поставщика удостоверений Google. Если используется Facebook, то [требуется добавить домены Facebook в список разрешений][1] в приложении.

    Замените hello **urlScheme** уникальное имя для вашего приложения.  Hello urlScheme должен быть hello таким же как hello протокола схема URL-адрес, указанный в hello **допускается внешний URL-адреса перенаправления** в hello портал Azure. Hello urlScheme используется приложением hello проверки подлинности обратного вызова tooswitch задней tooyour после завершения проверки подлинности запроса.

2. Удалить строки hello `self.refreshControl?.beginRefreshing()` и `self.onRefresh(self.refreshControl)` в конце `viewDidLoad()` в *ToDoTableViewController.swift*. Добавьте вызов слишком`loginAndGetData()` вместо них:

    ```swift
    loginAndGetData()
    ```

3. Откройте hello `AppDelegate.swift` и добавьте следующие строки toohello hello `AppDelegate` класса:

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

    Замените hello _appname_ wih hello urlScheme значение, выбранное на шаге 1.

4. Откройте hello `AppName-Info.plist` (вместо AppName с именем hello приложения) и добавьте hello, следующий код:

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

    Этот код следует разместить внутри hello `<dict>` элемента.  Замените hello _appname_ строки (в массиве, **CFBundleURLSchemes**) с именем приложения hello, выбранное на шаге 1.  Также внести эти изменения в hello plist редактор - щелкните hello `AppName-Info.plist` файл в редакторе plist hello tooopen XCode.

    Замените hello `com.microsoft.azure.zumo` строка для **CFBundleURLName** с вашей Apple объединить идентификатор.

5. Нажмите клавишу *запуска* toostart приложения hello и войдите в систему. При входе необходимо будет tooview hello Todo list и обновления.

Для аутентификации службы приложений используется технология взаимодействия приложений Apple.  Дополнительные сведения по этому вопросу см. в разделе toohello [документации Apple][2]
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[портал Azure]: https://portal.azure.com

[iOS быстрый запуск]: app-service-mobile-ios-get-started.md

