---
title: "aaaAzure iOS Mobile Engagement SDK-интеграция доступа | Документы Microsoft"
description: "Последние обновления и указания для пакета SDK для iOS для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a>Как tooIntegrate Engagement Reach на iOS
Необходимо выполнить процедуры интеграции hello, описанной в hello [как tooIntegrate Engagement документе iOS](mobile-engagement-ios-integrate-engagement.md) до следующего руководства.

Также требуется установка XCode 8. Если действительно зависят XCode 7, то вы можете использовать hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). В предыдущей версии на устройствах iOS 10 выявлена ошибка: не приводятся в действие системные уведомления. toofix будет иметь tooimplement hello нерекомендуемый API `application:didReceiveRemoteNotification:` в вашем приложении делегат следующим образом:

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Данный способ не является рекомендуемым** , так как это поведение может измениться с любым последующим (даже незначительным) обновлением версии iOS из-за того, что этот интерфейс API для iOS устарел. Следует как можно быстрее перейти tooXCode 8.
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Включить вашего приложения tooreceive автоматической Push-уведомления
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a>Этапы интеграции
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a>Внедрение hello Engagement Reach SDK в проект iOS
* Добавьте пакет sdk для Reach hello в своем проекте Xcode. В Xcode перейдите слишком**проекта \> добавить tooproject** и выберите hello `EngagementReach` папки.

### <a name="modify-your-application-delegate"></a>Изменение делегата приложения
* Вверху hello файл реализации импортируйте модуль Engagement Reach hello:

      [...]
      #import "AEReachModule.h"
* Внутри метода `applicationDidFinishLaunching:` или `application:didFinishLaunchingWithOptions:`, создайте модуль reach и передать его tooyour существующую строку инициализации участия:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* Изменить **«icon.png»** строка, в которой имя образа hello, необходимо в качестве значка уведомления.
* Если требуется, чтобы параметр hello toouse *обновление значения эмблемы* в кампании Reach и следует ли собственные Push-уведомления toouse \<SaaS или Reach API/кампании Push формат и машинным\> кампаний, предоставляется возможность управлять модулем hello Hello эмблемы сам значок (он будет автоматически сброшено эмблемы приложения hello и также сбросить значение hello охватом каждый раз приложения hello запущен» или «foregrounded). Это делается путем добавления следующей строкой после инициализации модуля Reach hello:

      [reach setAutoBadgeEnabled:YES];
* Принудительная отправка данных Reach toohandle следует должен дать вашему представителю приложения соответствует toohello `AEReachDataPushDelegate` протокола. Добавьте hello, следующей строкой после инициализации модуля Reach.

      [reach setDataPushDelegate:self];
* Затем можно реализовать методы hello `onDataPushStringReceived:` и `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` в делегате приложения:

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a>Категория
параметр категории Hello не является обязательным при создании кампании Push-данных и позволяет ваши данные toofilter помещает в стек. Это полезно, если требуется, чтобы различные типы toopush из `Base64` tooidentify данных и необходимо их типа перед синтаксическим анализом их.

**Приложение будет теперь готовы tooreceive и отображения достичь содержимое!**

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a>Как tooreceive объявлений и для опросов в любое время
Engagement можно отправлять уведомления Reach tooyour конечных пользователей в любое время с помощью hello Apple Push Notification Service.

tooenable эта функция будет иметь tooprepare приложения для push-уведомлений Apple и изменения приложения делегата.

### <a name="prepare-your-application-for-apple-push-notifications"></a>Подготовка приложения для push-уведомлений Apple
Следуйте инструкциям в руководстве hello: [как tooPrepare приложения для Push-уведомлений Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

### <a name="add-hello-necessary-client-code"></a>Добавьте необходимые клиентского кода hello
*На этом этапе приложение должно иметь зарегистрированный сертификат push Apple интерфейс Engagement hello.*

Если это не было сделано уже tooregister необходимо ваши приложения tooreceive push-уведомления.

* Импорт hello `User Notification` framework:

        #import <UserNotifications/UserNotifications.h>
* Добавьте следующие строки, при запуске приложения hello (обычно в `application:didFinishLaunchingWithOptions:`):

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

Затем необходимо устройство tooprovide tooEngagement hello токен, возвращенный серверами Apple. Это можно сделать в hello метод с именем `application:didRegisterForRemoteNotificationsWithDeviceToken:` в делегате приложения:

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

Наконец когда приложение получает уведомление об удаленном иметь hello tooinform Engagement SDK. Здравствуйте, toodo, вызовите метод `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` в делегате приложения:

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> По умолчанию Engagement Reach управляет hello completionHandler. Если требуется ответ toohello toomanually `handler` блока в коде, можно передать nil для hello `handler` блокировать завершение hello аргумента и управления самостоятельно. В разделе hello `UIBackgroundFetchResult` тип список возможных значений.
>
>

### <a name="full-example"></a>Полный пример
Ниже приведен полный пример интеграции:

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
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

## <a name="how-toocustomize-campaigns"></a>Как toocustomize кампании
### <a name="notifications"></a>Уведомления
Существует два типа уведомлений: системные уведомления и уведомления в приложении.

Системные уведомления обрабатываются iOS, и их невозможно настроить.

Уведомления в приложения состоят из представления, который динамически добавляется toohello текущего окна приложения. Это называется наложением уведомлений. Уведомления наложений прекрасно подходят для быстрого интеграции так как они не требуют вы toomodify любого представления в приложении.

#### <a name="layout"></a>Макет
toomodify вида hello уведомления в приложении, можно просто изменить файл hello `AENotificationView.xib` должен tooyour, при условии, что хранить значения тегов hello и типы hello существующих представлений.

По умолчанию hello нижней части экрана приветствия представлены уведомления в приложения. При желании toodisplay их hello верхней части экрана, изменить hello предоставленный `AENotificationView.xib` и измените hello `AutoSizing` hello в основном представлении, могут храниться вверху hello обзор его от свойства.

#### <a name="categories"></a>Категории
При изменении hello, предоставляемые макета, то изменить hello вида все уведомления. Категории позволяют вам toodefine, различные целевые ищет (возможно поведения) уведомления. Категорию можно указать при создании рекламной кампании. Учтите, что категории также позволяют настраивать объявления и опросы. Это описано далее в этом документе.

tooregister обработчик категории для уведомления требуется tooadd инициализации вызов после hello доступа модуля.

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

`myNotifier`должен быть экземпляр объекта, который соответствует протокол toohello `AENotifier`.

Для реализации методов протокола hello можно самостоятельно или выбрать существующий класс tooreimplement hello `AEDefaultNotifier` которого уже выполняет большую часть работы hello.

Например если вы хотите tooredefine hello уведомления представление для определенной категории, можно выполнить в этом примере.

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

В этом простом примере категории предполагается, что в основном наборе приложений есть файл с именем `MyNotificationView.xib` . Если метод hello не может toofind соответствующий `.xib`, не будет отображаться уведомление hello и Engagement будет выводить сообщение hello консоли.

Hello предоставленный файл nib должны учитывать hello следующие правила:

* он должен содержать только одно представление;
* Представлений должен быть таким же типы как hello областей внутри hello предоставленный nib файл с именем hello`AENotificationView.xib`
* Представлений должны иметь одинаково теги как hello областей внутри hello предоставленный nib файл с именем hello`AENotificationView.xib`

> [!TIP]
> Просто скопируйте hello предоставленный nib файл с именем `AENotificationView.xib`и начала работы оттуда. Но будьте внимательны, hello представление внутри этого файла nib имеет связанный класс toohello `AENotificationView`. Этот класс переопределен метод hello `layoutSubViews` toomove и изменить его представлений, в соответствии с toocontext. Вы можете tooreplace с `UIView` или пользовательское представление класса.
>
>

Если требуется более глубокого настройки уведомления (если для экземпляра tooload представление непосредственно из кода hello), рекомендуется tootake рассмотрим hello предоставленных исходного кода и класс документации `Protocol ReferencesDefaultNotifier` и `AENotifier`.

Обратите внимание, что можно использовать hello же средство уведомления для нескольких категорий.

Вы можете также переопределенное hello уведомляющий по умолчанию следующим образом:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a>Обработка уведомлений
При использовании категории по умолчанию hello, некоторые методы жизненного цикла вызываются на hello `AEReachContent` объекта tooreport статистики и обновление hello кампании состояния:

* Здравствуйте, когда в приложении отображается уведомление hello, `displayNotification` (который предоставляет статистические данные) вызывается метод по `AEReachModule` Если `handleNotification:` возвращает `YES`.
* При закрытии hello уведомления hello `exitNotification` вызывается метод, статистика выводится и далее кампаний теперь могут быть обработаны.
* Если щелкнуть уведомление hello `actionNotification` — вызывается, статистика выводится и hello связанное действие выполняется.

Если реализация `AENotifier` обходы hello поведение по умолчанию, вы получите toocall эти методы жизненного цикла по самостоятельно. Hello в следующих примерах показаны некоторые случаи, где пропускается hello поведение по умолчанию:

* Вы не расширяли `AEDefaultNotifier`, например реализовали обработку категорий с нуля.
* Вы используемое `prepareNotificationView:forContent:`, по крайней мере быть убедиться, что toomap `onNotificationActioned` или `onNotificationExited` tooone U.I элементов управления.

> [!WARNING]
> Если `handleNotification:` создает исключение, hello содержимого удаляется и `drop` — вызывается, это сообщение появляется в статистике и далее кампаний теперь могут быть обработаны.
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a>Включение уведомления в состав существующего представления
Наложения хорошо подходят для быстрой интеграции, но иногда могут быть неудобными или приводить к нежелательным побочным эффектам.

Если вы не удовлетворены системы наложения hello в некоторых представлений, можно настроить его для этих представлений.

Решите, tooinclude нашей макета уведомления в существующие представления. toodo таким образом, есть два стиля реализации:

1. Добавить представление hello уведомления, с помощью построителя интерфейса

   * Откройте *конструктор интерфейса*
   * Поместите 320 x 60 (или если вы находитесь на iPad 768 x 60) `UIView` место tooappear уведомления hello
   * Значение hello тег для этого представления слишком: **36822491**
2. Добавьте представление уведомления hello программным способом. Просто добавьте следующий код, при инициализации представления hello:

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

Макрос `NOTIFICATION_AREA_VIEW_TAG` можно найти в файле `AEDefaultNotifier.h`.

> [!NOTE]
> средство уведомления по умолчанию Hello автоматически обнаруживает макета hello уведомления включены в это представление и не будет добавлять наложение для него.
>
>

### <a name="announcements-and-polls"></a>Объявления и опросы
#### <a name="layouts"></a>Макеты
Можно изменить файлы hello `AEDefaultAnnouncementView.xib` и `AEDefaultPollView.xib` до тех пор, пока сохранять значения тегов hello и типы hello существующих представлений.

#### <a name="categories"></a>Категории
##### <a name="alternate-layouts"></a>Альтернативные макеты
Подобно уведомления категория кампании hello может быть используется toohave дополнительные раскладки для объявлений и опросов.

toocreate категория для объявления, необходимо расширить **AEAnnouncementViewController** и зарегистрируйте его после инициализации модулем hello:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> Каждый раз, пользователь нажимает кнопку на уведомления для объявления с категорией hello «my\_категории», контроллер зарегистрированных представление (в этом случае `MyCustomAnnouncementViewController`) инициализируются с помощью вызова метода hello `initWithAnnouncement:` и будет представление hello добавлены toohello текущего окна приложения.
>
>

В такой реализации hello `AEAnnouncementViewController` классе имеется свойство hello tooread `announcement` tooinitialize вашей представлений. Рассмотрим hello ниже пример, где два метки инициализируются с помощью `title` и `body` свойства hello `AEReachAnnouncement` класса:

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

Если вы не хотите tooload вашим представлениям в одиночку, но необходимо просто разметки представления объявления по умолчанию hello tooreuse, можно просто сделать контроллер пользовательское представление расширяет класс hello предоставленный `AEDefaultAnnouncementViewController`. В этом случае повторяющийся файл hello nib `AEDefaultAnnouncementView.xib` и переименуйте его, поэтому ее можно загрузить в контроллере пользовательское представление (для контроллера с именем `CustomAnnouncementViewController`, необходимо вызвать файла nib `CustomAnnouncementView.xib`).

категории по умолчанию hello tooreplace объявлений, просто регистрации контроллера настраиваемого представления для hello категории, определенной в `kAEReachDefaultCategory`:

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

Опрашивает может быть настроенный hello так же, как:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

Это время, предоставляемые hello `MyCustomPollViewController` необходимо расширить `AEPollViewController`. Или можно выбрать tooextend контроллера по умолчанию hello: `AEDefaultPollViewController`.

> [!IMPORTANT]
> Не забывайте toocall либо `action` (`submitAnswers:` для контроллеров представления пользовательских опроса) или `exit` метод до закрытия hello представление-контроллер. В противном случае статистические данные не могут быть переданы (т. е. не analytics hello кампании) и не будет уведомлен дополнительные кампаний, что важно далее до перезапуска процесса приложения hello.
>
>

##### <a name="implementation-example"></a>Пример реализации
В этой реализации представления пользовательских объявления hello загружается из файла внешних xib.

Как и для настройки дополнительных уведомлений рекомендуется toolook в исходный код hello hello стандартную реализацию.

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
