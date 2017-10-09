---
title: "aaaGet работы с Azure Mobile Engagement для Objective C iOS | Документы Microsoft"
description: "Узнайте, как toouse Azure Mobile Engagement с analytics и отправка уведомлений для приложений iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a>Начало работы со Службами мобильного взаимодействия Azure для приложений iOS в Objective C
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использования приложений и отправлять push-уведомления toosegmented пользователей tooan операций ввода-вывода приложения.
В этом учебнике вы создадите пустое приложение iOS, которое собирает основные данные и получает push-уведомления с помощью Apple Push Notification System (APNS).

Этот учебник требует hello следующее:

* XCode 8, который можно установить из MAC App Store;
* Hello [iOS Mobile Engagement SDK]

Завершение изучения этого руководства является необходимым условием для работы со всеми другими руководствами, посвященными Службам мобильного взаимодействия для приложений iOS.

> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).
>
>

## <a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для вашего приложения iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений
В этом руководстве содержатся «базовой интеграции», который hello минимальный набор данных требуется toocollect и отправить push-уведомление. Hello полной интеграции документацию можно найти в hello [iOS Mobile Engagement SDK-интеграция](mobile-engagement-ios-sdk-overview.md)

Мы создадим простое приложение с интеграцией hello toodemonstrate XCode.

### <a name="create-a-new-ios-project"></a>Создание проекта iOS
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Подключение мобильного охвата toohello внутренний сервер приложений
1. Загрузите hello [iOS Mobile Engagement SDK].
2. Извлеките hello. tar.gz файл tooa папку на своем компьютере.
3. Щелкните правой кнопкой мыши проект hello, а затем выберите **добавьте файлы в**.

    ![][1]
4. Перейдите в папку toohello, будут извлечены hello SDK, выберите hello `EngagementSDK` папку, нажмите кнопку **параметры** на нижний левый угол hello и убедитесь в том, что флажок hello **копирование элементов при необходимости** и hello флажок на целевом объекте проверяются, а затем нажмите **ОК**.

    ![][2]
5. Привет открыть **этапов построения** вкладке и в hello **ссылку двоичного файла с библиотеками** меню, добавить hello платформы, как показано ниже:

    ![][3]
6. Вернитесь к предыдущему окну toohello портал Azure в вашем приложении **сведений о соединении** страницы и скопируйте строку подключения hello.

    ![][4]
7. Добавить hello, следующей строкой кода в ваш **AppDelegate.m** файла.

        #import "EngagementAgent.h"
8. Теперь вставьте строку подключения hello в hello `didFinishLaunchingWithOptions` делегата.

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. `setTestLogEnabled`— необязательный оператор, который включает журналы SDK на tooidentify проблемы.

## <a id="monitor"></a>Включение мониторинга в режиме реального времени
В toostart порядок отправки данных и убедитесь, что пользователи hello active необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана (действие).

1. Откройте hello **ViewController.h** и импортируйте **EngagementViewController.h**:

    `#import "EngagementViewController.h"`
2. Теперь замените hello суперкласса hello **ViewController** интерфейс с `EngagementViewController`:

    `@interface ViewController : EngagementViewController`

## <a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении
Mobile Engagement позволяет toointeract со своими пользователями и получить доступ с push-уведомления и сообщения в контексте hello кампаний в приложения. Этот модуль вызывается REACH на портале мобильного охвата hello.
Hello следующих разделах Настройка вашего приложения tooreceive их.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Включить вашего приложения tooreceive автоматической Push-уведомления
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Добавьте проект tooyour библиотеки Reach hello
1. Щелкните проект правой кнопкой мыши.
2. Выберите пункт **Добавить файл в**.
3. Перейдите в папку toohello, будут извлечены hello SDK.
4. Выберите hello `EngagementReach` папки.
5. Щелкните **Добавить**.

### <a name="modify-your-application-delegate"></a>Изменение делегата приложения
1. В **AppDeletegate.m** файл, импортируйте модуль Engagement Reach hello.

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. Внутри hello `application:didFinishLaunchingWithOptions` метод, создайте модулем и передайте его tooyour существующую строку инициализации участия:

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Включить вашего приложения tooreceive Push-уведомления APNS
1. Добавьте следующие строки toohello hello `application:didFinishLaunchingWithOptions` метод:

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }
2. Добавить hello `application:didRegisterForRemoteNotificationsWithDeviceToken` метод следующим образом:

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. Добавить hello `didFailToRegisterForRemoteNotificationsWithError` метод следующим образом:

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. Добавить hello `didReceiveRemoteNotification:fetchCompletionHandler` метод следующим образом:

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[iOS Mobile Engagement SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
