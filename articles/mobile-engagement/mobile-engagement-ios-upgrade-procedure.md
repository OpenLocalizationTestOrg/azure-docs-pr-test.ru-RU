---
title: "aaaAzure iOS Mobile Engagement процедура обновления пакета SDK | Документы Microsoft"
description: "Последние обновления и указания для пакета SDK для iOS для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>Процедуры обновления
Если уже имеется встроенный более старой версии участия в приложение, у вас есть hello tooconsider при обновлении hello SDK следующие точки.

Для каждой новой версии пакета SDK для hello сначала необходимо заменить (удалить и повторно импортировать в xcode) hello EngagementSDK и EngagementReach папки.

## <a name="from-300-too400"></a>Из 3.0.0 too4.0.0
### <a name="xcode-8"></a>XCode 8
XCode 8 является обязательным, начиная с версии 4.0.0 hello SDK.

> [!NOTE]
> Если действительно зависят XCode 7, то вы можете использовать hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). При работе на устройствах iOS 10 на hello модулем этой предыдущей версии имеется известная ошибка: не обработанных системных уведомлений. toofix будет иметь tooimplement hello нерекомендуемый API `application:didReceiveRemoteNotification:` в вашем приложении делегат следующим образом:
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Данный способ не является рекомендуемым** , так как это поведение может измениться с любым последующим (даже незначительным) обновлением версии iOS из-за того, что этот интерфейс API для iOS устарел. Следует как можно быстрее перейти tooXCode 8.
> 
> 

### <a name="usernotifications-framework"></a>Платформа UserNotifications
Требуется tooadd hello `UserNotifications` framework поэтапно сборки.

в обозревателе проектов hello откройте панель проекта и выберите правильный hello. Откройте hello **«Этапы сборки»** вкладку и в hello **«Двоичный с библиотеками»** меню, добавление платформы `UserNotifications.framework` -задать связь hello как`Optional`

### <a name="application-push-capability"></a>Функция push-уведомлений приложения
Приложение может привести к сбросу XCode 8 принудительные возможность, проверьте его в hello `capability` вкладку выбранного целевого.

### <a name="add-hello-new-ios-10-notification-registration-code"></a>Добавление нового кода в регистрации iOS 10 уведомления hello
старые кода фрагмент tooregister hello приложение Hello toonotifications по-прежнему работает, но использует устаревшие интерфейсы API при выполнении с iOS 10.

Импорт hello `User Notification` framework:

        #import <UserNotifications/UserNotifications.h> 

В методе `application:didFinishLaunchingWithOptions` делегата приложения замените:

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

на:

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Разрешение конфликтов делегата UNUserNotificationCenter

*Если приложения или библиотеки сторонних производителей не реализуют `UNUserNotificationCenterDelegate`, то эту часть можно пропустить.*

Объект `UNUserNotificationCenter` делегат используется hello SDK toomonitor hello жизненного цикла Engagement уведомлений на устройства под управлением IOS, 10 или более поздней. пакет SDK для Hello имеет собственную реализацию hello `UNUserNotificationCenterDelegate` протокола, но может быть только один `UNUserNotificationCenter` делегировать каждого приложения. Любого другого делегата добавлены toohello `UNUserNotificationCenter` объекта будут конфликтовать с hello Engagement один. Если hello SDK обнаруживает делегата к или любые другие третьих лиц, то не будет использовать собственную реализацию toogive вы tooresolve вероятность hello конфликтов. Вы должны будете tooadd hello Engagement логику tooyour владельцем делегата в порядке tooresolve hello конфликтов.

Существует два способа tooachieve это.

Предложение 1, просто переадресующей делегат вызывает toohello SDK:

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

Или предложение 2, путем наследования от hello `AEUserNotificationHandler` класса

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> Можно определить, откуда уведомление на работе или не путем передачи его `userInfo` toohello словарь агента `isEngagementPushPayload:` методу класса.

Убедитесь в том, что hello `UNUserNotificationCenter` объекта делегата задается tooyour делегата в рамках либо hello `application:willFinishLaunchingWithOptions:` или hello `application:didFinishLaunchingWithOptions:` метод делегата вашего приложения.
Например если реализовано hello выше предложение 1:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a>Из 2.0.0 too3.0.0
Прекращена поддержка iOS 4.X. Начиная с этой версии цель развертывания hello приложения должен быть по крайней мере iOS 6.

Если вы используете Reach в приложении, необходимо добавить `remote-notification` toohello значение `UIBackgroundModes` массива в файле Info.plist в порядке tooreceive удаленного уведомления.

Здравствуйте, метод `application:didReceiveRemoteNotification:` необходимо заменить toobe `application:didReceiveRemoteNotification:fetchCompletionHandler:` в делегате приложения.

«AEPushDelegate.h» является устаревшим интерфейс и вы должны tooremove все ссылки. Это включает в себя удаление `[[EngagementAgent shared] setPushDelegate:self]` и делегата методы из делегата приложения hello:

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a>Из 1.16.0 too2.0.0
Hello ниже описаны как toomigrate SDK-интеграция с hello обновления Capptain предлагаемых Capptain SAS в приложение на платформе Azure Mobile Engagement.
При переносе из более ранней версии, обратитесь к веб-сайт toomigrate hello Capptain too1.16 сначала затем применить hello после процедуры.

> [!IMPORTANT]
> Capptain и мобильного охвата не являются hello и теми же службами и только представленные ниже процедуры hello выделяет как toomigrate hello клиентского приложения. Миграция hello SDK в приложение hello не выполняют миграцию данных из hello Capptain toohello мобильного охвата серверов
> 
> 

### <a name="agent"></a>Агент
Здравствуйте, метод `registerApp:` будет заменен hello новый метод `init:`. Следует обновить делегат приложения соответствующим образом и использовать строку подключения:

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

Отслеживание SmartAd был удален из пакета SDK, достаточно лишь tooremove все экземпляры `AETrackModule` класса

### <a name="class-name-changes"></a>Изменение имени класса
В рамках ребрендинг hello существует несколько классов и файлов, имена которых требуется изменить toobe.

Во всех классах префикс CP нужно заменить префиксом AE.

Пример:

* `CPModule.h`переименовывается слишком`AEModule.h`.

Во всех классах префикс Capptain нужно заменить префиксом Engagement.

Примеры:

* Здравствуйте, класс `CapptainAgent` переименовывается слишком`EngagementAgent`.
* Здравствуйте, класс `CapptainTableViewController` переименовывается слишком`EngagementTableViewController`.
* Здравствуйте, класс `CapptainUtils` переименовывается слишком`EngagementUtils`.
* Здравствуйте, класс `CapptainViewController` переименовывается слишком`EngagementViewController`.

