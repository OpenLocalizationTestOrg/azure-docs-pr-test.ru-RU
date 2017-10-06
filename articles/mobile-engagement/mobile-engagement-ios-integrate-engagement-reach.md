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
# <a name="how-toointegrate-engagement-reach-on-ios"></a><span data-ttu-id="2b312-103">Как tooIntegrate Engagement Reach на iOS</span><span class="sxs-lookup"><span data-stu-id="2b312-103">How tooIntegrate Engagement Reach on iOS</span></span>
<span data-ttu-id="2b312-104">Необходимо выполнить процедуры интеграции hello, описанной в hello [как tooIntegrate Engagement документе iOS](mobile-engagement-ios-integrate-engagement.md) до следующего руководства.</span><span class="sxs-lookup"><span data-stu-id="2b312-104">You must follow hello integration procedure described in hello [How tooIntegrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="2b312-105">Также требуется установка XCode 8.</span><span class="sxs-lookup"><span data-stu-id="2b312-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="2b312-106">Если действительно зависят XCode 7, то вы можете использовать hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="2b312-106">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="2b312-107">В предыдущей версии на устройствах iOS 10 выявлена ошибка: не приводятся в действие системные уведомления.</span><span class="sxs-lookup"><span data-stu-id="2b312-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="2b312-108">toofix будет иметь tooimplement hello нерекомендуемый API `application:didReceiveRemoteNotification:` в вашем приложении делегат следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2b312-108">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="2b312-109">**Данный способ не является рекомендуемым** , так как это поведение может измениться с любым последующим (даже незначительным) обновлением версии iOS из-за того, что этот интерфейс API для iOS устарел.</span><span class="sxs-lookup"><span data-stu-id="2b312-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="2b312-110">Следует как можно быстрее перейти tooXCode 8.</span><span class="sxs-lookup"><span data-stu-id="2b312-110">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="2b312-111">Включить вашего приложения tooreceive автоматической Push-уведомления</span><span class="sxs-lookup"><span data-stu-id="2b312-111">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="2b312-112">Этапы интеграции</span><span class="sxs-lookup"><span data-stu-id="2b312-112">Integration steps</span></span>
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="2b312-113">Внедрение hello Engagement Reach SDK в проект iOS</span><span class="sxs-lookup"><span data-stu-id="2b312-113">Embed hello Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="2b312-114">Добавьте пакет sdk для Reach hello в своем проекте Xcode.</span><span class="sxs-lookup"><span data-stu-id="2b312-114">Add hello Reach sdk in your Xcode project.</span></span> <span data-ttu-id="2b312-115">В Xcode перейдите слишком**проекта \> добавить tooproject** и выберите hello `EngagementReach` папки.</span><span class="sxs-lookup"><span data-stu-id="2b312-115">In Xcode, go too**Project \> Add tooproject** and choose hello `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="2b312-116">Изменение делегата приложения</span><span class="sxs-lookup"><span data-stu-id="2b312-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="2b312-117">Вверху hello файл реализации импортируйте модуль Engagement Reach hello:</span><span class="sxs-lookup"><span data-stu-id="2b312-117">At hello top of your implementation file, import hello Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="2b312-118">Внутри метода `applicationDidFinishLaunching:` или `application:didFinishLaunchingWithOptions:`, создайте модуль reach и передать его tooyour существующую строку инициализации участия:</span><span class="sxs-lookup"><span data-stu-id="2b312-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it tooyour existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="2b312-119">Изменить **«icon.png»** строка, в которой имя образа hello, необходимо в качестве значка уведомления.</span><span class="sxs-lookup"><span data-stu-id="2b312-119">Modify **'icon.png'** string with hello image name you want as your notification icon.</span></span>
* <span data-ttu-id="2b312-120">Если требуется, чтобы параметр hello toouse *обновление значения эмблемы* в кампании Reach и следует ли собственные Push-уведомления toouse \<SaaS или Reach API/кампании Push формат и машинным\> кампаний, предоставляется возможность управлять модулем hello Hello эмблемы сам значок (он будет автоматически сброшено эмблемы приложения hello и также сбросить значение hello охватом каждый раз приложения hello запущен» или «foregrounded).</span><span class="sxs-lookup"><span data-stu-id="2b312-120">If you want toouse hello option *Update badge value* in Reach campaigns or if you want toouse native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let hello Reach module manage hello badge icon itself (it will automatically clear hello application badge and also reset hello value stored by Engagement every time hello application is started or foregrounded).</span></span> <span data-ttu-id="2b312-121">Это делается путем добавления следующей строкой после инициализации модуля Reach hello:</span><span class="sxs-lookup"><span data-stu-id="2b312-121">This is done by adding hello following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="2b312-122">Принудительная отправка данных Reach toohandle следует должен дать вашему представителю приложения соответствует toohello `AEReachDataPushDelegate` протокола.</span><span class="sxs-lookup"><span data-stu-id="2b312-122">If you want toohandle Reach data push, you must let your Application delegate conform toohello `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="2b312-123">Добавьте hello, следующей строкой после инициализации модуля Reach.</span><span class="sxs-lookup"><span data-stu-id="2b312-123">Add hello following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="2b312-124">Затем можно реализовать методы hello `onDataPushStringReceived:` и `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` в делегате приложения:</span><span class="sxs-lookup"><span data-stu-id="2b312-124">Then you can implement hello methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

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

### <a name="category"></a><span data-ttu-id="2b312-125">Категория</span><span class="sxs-lookup"><span data-stu-id="2b312-125">Category</span></span>
<span data-ttu-id="2b312-126">параметр категории Hello не является обязательным при создании кампании Push-данных и позволяет ваши данные toofilter помещает в стек.</span><span class="sxs-lookup"><span data-stu-id="2b312-126">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="2b312-127">Это полезно, если требуется, чтобы различные типы toopush из `Base64` tooidentify данных и необходимо их типа перед синтаксическим анализом их.</span><span class="sxs-lookup"><span data-stu-id="2b312-127">This is useful if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

<span data-ttu-id="2b312-128">**Приложение будет теперь готовы tooreceive и отображения достичь содержимое!**</span><span class="sxs-lookup"><span data-stu-id="2b312-128">**Your application is now ready tooreceive and display reach contents!**</span></span>

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a><span data-ttu-id="2b312-129">Как tooreceive объявлений и для опросов в любое время</span><span class="sxs-lookup"><span data-stu-id="2b312-129">How tooreceive announcements and polls at any time</span></span>
<span data-ttu-id="2b312-130">Engagement можно отправлять уведомления Reach tooyour конечных пользователей в любое время с помощью hello Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="2b312-130">Engagement can send Reach notifications tooyour end users at any time by using hello Apple Push Notification Service.</span></span>

<span data-ttu-id="2b312-131">tooenable эта функция будет иметь tooprepare приложения для push-уведомлений Apple и изменения приложения делегата.</span><span class="sxs-lookup"><span data-stu-id="2b312-131">tooenable this functionality, you'll have tooprepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="2b312-132">Подготовка приложения для push-уведомлений Apple</span><span class="sxs-lookup"><span data-stu-id="2b312-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="2b312-133">Следуйте инструкциям в руководстве hello: [как tooPrepare приложения для Push-уведомлений Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="2b312-133">Please follow hello guide : [How tooPrepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-hello-necessary-client-code"></a><span data-ttu-id="2b312-134">Добавьте необходимые клиентского кода hello</span><span class="sxs-lookup"><span data-stu-id="2b312-134">Add hello necessary client code</span></span>
<span data-ttu-id="2b312-135">*На этом этапе приложение должно иметь зарегистрированный сертификат push Apple интерфейс Engagement hello.*</span><span class="sxs-lookup"><span data-stu-id="2b312-135">*At this point your application should have a registered Apple push certificate in hello Engagement frontend.*</span></span>

<span data-ttu-id="2b312-136">Если это не было сделано уже tooregister необходимо ваши приложения tooreceive push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="2b312-136">If it's not done already, you need tooregister your application tooreceive push notifications.</span></span>

* <span data-ttu-id="2b312-137">Импорт hello `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="2b312-137">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="2b312-138">Добавьте следующие строки, при запуске приложения hello (обычно в `application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="2b312-138">Add hello following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="2b312-139">Затем необходимо устройство tooprovide tooEngagement hello токен, возвращенный серверами Apple.</span><span class="sxs-lookup"><span data-stu-id="2b312-139">Then, You need tooprovide tooEngagement hello device token returned by Apple servers.</span></span> <span data-ttu-id="2b312-140">Это можно сделать в hello метод с именем `application:didRegisterForRemoteNotificationsWithDeviceToken:` в делегате приложения:</span><span class="sxs-lookup"><span data-stu-id="2b312-140">This is done in hello method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="2b312-141">Наконец когда приложение получает уведомление об удаленном иметь hello tooinform Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="2b312-141">Finally, you have tooinform hello Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="2b312-142">Здравствуйте, toodo, вызовите метод `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` в делегате приложения:</span><span class="sxs-lookup"><span data-stu-id="2b312-142">toodo that, call hello method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="2b312-143">По умолчанию Engagement Reach управляет hello completionHandler.</span><span class="sxs-lookup"><span data-stu-id="2b312-143">By default, Engagement Reach controls hello completionHandler.</span></span> <span data-ttu-id="2b312-144">Если требуется ответ toohello toomanually `handler` блока в коде, можно передать nil для hello `handler` блокировать завершение hello аргумента и управления самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="2b312-144">If you want toomanually respond toohello `handler` block in your code, you can pass nil for hello `handler` argument and control hello completion block yourself.</span></span> <span data-ttu-id="2b312-145">В разделе hello `UIBackgroundFetchResult` тип список возможных значений.</span><span class="sxs-lookup"><span data-stu-id="2b312-145">See hello `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="2b312-146">Полный пример</span><span class="sxs-lookup"><span data-stu-id="2b312-146">Full example</span></span>
<span data-ttu-id="2b312-147">Ниже приведен полный пример интеграции:</span><span class="sxs-lookup"><span data-stu-id="2b312-147">Here is a full example of integration:</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="2b312-148">Разрешение конфликтов делегата UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="2b312-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="2b312-149">*Если приложения или библиотеки сторонних производителей не реализуют `UNUserNotificationCenterDelegate`, то эту часть можно пропустить.*</span><span class="sxs-lookup"><span data-stu-id="2b312-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="2b312-150">Объект `UNUserNotificationCenter` делегат используется hello SDK toomonitor hello жизненного цикла Engagement уведомлений на устройства под управлением IOS, 10 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="2b312-150">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="2b312-151">пакет SDK для Hello имеет собственную реализацию hello `UNUserNotificationCenterDelegate` протокола, но может быть только один `UNUserNotificationCenter` делегировать каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="2b312-151">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="2b312-152">Любого другого делегата добавлены toohello `UNUserNotificationCenter` объекта будут конфликтовать с hello Engagement один.</span><span class="sxs-lookup"><span data-stu-id="2b312-152">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="2b312-153">Если hello SDK обнаруживает делегата к или любые другие третьих лиц, то не будет использовать собственную реализацию toogive вы tooresolve вероятность hello конфликтов.</span><span class="sxs-lookup"><span data-stu-id="2b312-153">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="2b312-154">Вы должны будете tooadd hello Engagement логику tooyour владельцем делегата в порядке tooresolve hello конфликтов.</span><span class="sxs-lookup"><span data-stu-id="2b312-154">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="2b312-155">Существует два способа tooachieve это.</span><span class="sxs-lookup"><span data-stu-id="2b312-155">There are two ways tooachieve this.</span></span>

<span data-ttu-id="2b312-156">Предложение 1, просто переадресующей делегат вызывает toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="2b312-156">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="2b312-157">Или предложение 2, путем наследования от hello `AEUserNotificationHandler` класса</span><span class="sxs-lookup"><span data-stu-id="2b312-157">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="2b312-158">Можно определить, откуда уведомление на работе или не путем передачи его `userInfo` toohello словарь агента `isEngagementPushPayload:` методу класса.</span><span class="sxs-lookup"><span data-stu-id="2b312-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="2b312-159">Убедитесь в том, что hello `UNUserNotificationCenter` объекта делегата задается tooyour делегата в рамках либо hello `application:willFinishLaunchingWithOptions:` или hello `application:didFinishLaunchingWithOptions:` метод делегата вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="2b312-159">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="2b312-160">Например если реализовано hello выше предложение 1:</span><span class="sxs-lookup"><span data-stu-id="2b312-160">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="2b312-161">Как toocustomize кампании</span><span class="sxs-lookup"><span data-stu-id="2b312-161">How toocustomize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="2b312-162">Уведомления</span><span class="sxs-lookup"><span data-stu-id="2b312-162">Notifications</span></span>
<span data-ttu-id="2b312-163">Существует два типа уведомлений: системные уведомления и уведомления в приложении.</span><span class="sxs-lookup"><span data-stu-id="2b312-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="2b312-164">Системные уведомления обрабатываются iOS, и их невозможно настроить.</span><span class="sxs-lookup"><span data-stu-id="2b312-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="2b312-165">Уведомления в приложения состоят из представления, который динамически добавляется toohello текущего окна приложения.</span><span class="sxs-lookup"><span data-stu-id="2b312-165">In-app notifications are made of a view that is dynamically added toohello current application window.</span></span> <span data-ttu-id="2b312-166">Это называется наложением уведомлений.</span><span class="sxs-lookup"><span data-stu-id="2b312-166">This is called a notification overlay.</span></span> <span data-ttu-id="2b312-167">Уведомления наложений прекрасно подходят для быстрого интеграции так как они не требуют вы toomodify любого представления в приложении.</span><span class="sxs-lookup"><span data-stu-id="2b312-167">Notification overlays are great for a fast integration because they does not require you toomodify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="2b312-168">Макет</span><span class="sxs-lookup"><span data-stu-id="2b312-168">Layout</span></span>
<span data-ttu-id="2b312-169">toomodify вида hello уведомления в приложении, можно просто изменить файл hello `AENotificationView.xib` должен tooyour, при условии, что хранить значения тегов hello и типы hello существующих представлений.</span><span class="sxs-lookup"><span data-stu-id="2b312-169">toomodify hello look of your in-app notifications, you can simply modify hello file `AENotificationView.xib` tooyour needs, as long as you keep hello tag values and types of hello existing subviews.</span></span>

<span data-ttu-id="2b312-170">По умолчанию hello нижней части экрана приветствия представлены уведомления в приложения.</span><span class="sxs-lookup"><span data-stu-id="2b312-170">By default, in-app notifications are presented at hello bottom of hello screen.</span></span> <span data-ttu-id="2b312-171">При желании toodisplay их hello верхней части экрана, изменить hello предоставленный `AENotificationView.xib` и измените hello `AutoSizing` hello в основном представлении, могут храниться вверху hello обзор его от свойства.</span><span class="sxs-lookup"><span data-stu-id="2b312-171">If you prefer toodisplay them at hello top of screen, edit hello provided `AENotificationView.xib` and change hello `AutoSizing` property of hello main view so it can be kept at hello top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="2b312-172">Категории</span><span class="sxs-lookup"><span data-stu-id="2b312-172">Categories</span></span>
<span data-ttu-id="2b312-173">При изменении hello, предоставляемые макета, то изменить hello вида все уведомления.</span><span class="sxs-lookup"><span data-stu-id="2b312-173">When you modify hello provided layout, you modify hello look of all your notifications.</span></span> <span data-ttu-id="2b312-174">Категории позволяют вам toodefine, различные целевые ищет (возможно поведения) уведомления.</span><span class="sxs-lookup"><span data-stu-id="2b312-174">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="2b312-175">Категорию можно указать при создании рекламной кампании.</span><span class="sxs-lookup"><span data-stu-id="2b312-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="2b312-176">Учтите, что категории также позволяют настраивать объявления и опросы. Это описано далее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="2b312-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="2b312-177">tooregister обработчик категории для уведомления требуется tooadd инициализации вызов после hello доступа модуля.</span><span class="sxs-lookup"><span data-stu-id="2b312-177">tooregister a category handler for your notifications, you need tooadd a call once hello reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="2b312-178">`myNotifier`должен быть экземпляр объекта, который соответствует протокол toohello `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="2b312-178">`myNotifier` must be an instance of an object that conforms toohello protocol `AENotifier`.</span></span>

<span data-ttu-id="2b312-179">Для реализации методов протокола hello можно самостоятельно или выбрать существующий класс tooreimplement hello `AEDefaultNotifier` которого уже выполняет большую часть работы hello.</span><span class="sxs-lookup"><span data-stu-id="2b312-179">You can implement hello protocol methods by yourself or you can choose tooreimplement hello existing class `AEDefaultNotifier` which already performs most of hello work.</span></span>

<span data-ttu-id="2b312-180">Например если вы хотите tooredefine hello уведомления представление для определенной категории, можно выполнить в этом примере.</span><span class="sxs-lookup"><span data-stu-id="2b312-180">For example, if you want tooredefine hello notification view for a specific category, you can follow this example:</span></span>

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

<span data-ttu-id="2b312-181">В этом простом примере категории предполагается, что в основном наборе приложений есть файл с именем `MyNotificationView.xib` .</span><span class="sxs-lookup"><span data-stu-id="2b312-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="2b312-182">Если метод hello не может toofind соответствующий `.xib`, не будет отображаться уведомление hello и Engagement будет выводить сообщение hello консоли.</span><span class="sxs-lookup"><span data-stu-id="2b312-182">If hello method is not able toofind a corresponding `.xib`, hello notification will not be displayed and Engagement will output a message in hello console.</span></span>

<span data-ttu-id="2b312-183">Hello предоставленный файл nib должны учитывать hello следующие правила:</span><span class="sxs-lookup"><span data-stu-id="2b312-183">hello provided nib file should respect hello following rules:</span></span>

* <span data-ttu-id="2b312-184">он должен содержать только одно представление;</span><span class="sxs-lookup"><span data-stu-id="2b312-184">It should only contain one view.</span></span>
* <span data-ttu-id="2b312-185">Представлений должен быть таким же типы как hello областей внутри hello предоставленный nib файл с именем hello`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="2b312-185">Subviews should be of hello same types as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="2b312-186">Представлений должны иметь одинаково теги как hello областей внутри hello предоставленный nib файл с именем hello`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="2b312-186">Subviews should have hello same tags as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="2b312-187">Просто скопируйте hello предоставленный nib файл с именем `AENotificationView.xib`и начала работы оттуда.</span><span class="sxs-lookup"><span data-stu-id="2b312-187">Just copy hello provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="2b312-188">Но будьте внимательны, hello представление внутри этого файла nib имеет связанный класс toohello `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="2b312-188">But be careful, hello view inside this nib file is associated toohello class `AENotificationView`.</span></span> <span data-ttu-id="2b312-189">Этот класс переопределен метод hello `layoutSubViews` toomove и изменить его представлений, в соответствии с toocontext.</span><span class="sxs-lookup"><span data-stu-id="2b312-189">This class redefined hello method `layoutSubViews` toomove and resize its subviews according toocontext.</span></span> <span data-ttu-id="2b312-190">Вы можете tooreplace с `UIView` или пользовательское представление класса.</span><span class="sxs-lookup"><span data-stu-id="2b312-190">You may want tooreplace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="2b312-191">Если требуется более глубокого настройки уведомления (если для экземпляра tooload представление непосредственно из кода hello), рекомендуется tootake рассмотрим hello предоставленных исходного кода и класс документации `Protocol ReferencesDefaultNotifier` и `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="2b312-191">If you need deeper customization of your notifications(if you want for instance tooload your view directly from hello code), it is recommended tootake a look at hello provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="2b312-192">Обратите внимание, что можно использовать hello же средство уведомления для нескольких категорий.</span><span class="sxs-lookup"><span data-stu-id="2b312-192">Note that you can use hello same notifier for multiple categories.</span></span>

<span data-ttu-id="2b312-193">Вы можете также переопределенное hello уведомляющий по умолчанию следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2b312-193">You can also redefined hello default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="2b312-194">Обработка уведомлений</span><span class="sxs-lookup"><span data-stu-id="2b312-194">Notification handling</span></span>
<span data-ttu-id="2b312-195">При использовании категории по умолчанию hello, некоторые методы жизненного цикла вызываются на hello `AEReachContent` объекта tooreport статистики и обновление hello кампании состояния:</span><span class="sxs-lookup"><span data-stu-id="2b312-195">When using hello default category, some life cycle methods are called on hello `AEReachContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="2b312-196">Здравствуйте, когда в приложении отображается уведомление hello, `displayNotification` (который предоставляет статистические данные) вызывается метод по `AEReachModule` Если `handleNotification:` возвращает `YES`.</span><span class="sxs-lookup"><span data-stu-id="2b312-196">When hello notification is displayed in application, hello `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="2b312-197">При закрытии hello уведомления hello `exitNotification` вызывается метод, статистика выводится и далее кампаний теперь могут быть обработаны.</span><span class="sxs-lookup"><span data-stu-id="2b312-197">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="2b312-198">Если щелкнуть уведомление hello `actionNotification` — вызывается, статистика выводится и hello связанное действие выполняется.</span><span class="sxs-lookup"><span data-stu-id="2b312-198">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated action is performed.</span></span>

<span data-ttu-id="2b312-199">Если реализация `AENotifier` обходы hello поведение по умолчанию, вы получите toocall эти методы жизненного цикла по самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="2b312-199">If your implementation of `AENotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="2b312-200">Hello в следующих примерах показаны некоторые случаи, где пропускается hello поведение по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="2b312-200">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="2b312-201">Вы не расширяли `AEDefaultNotifier`, например реализовали обработку категорий с нуля.</span><span class="sxs-lookup"><span data-stu-id="2b312-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="2b312-202">Вы используемое `prepareNotificationView:forContent:`, по крайней мере быть убедиться, что toomap `onNotificationActioned` или `onNotificationExited` tooone U.I элементов управления.</span><span class="sxs-lookup"><span data-stu-id="2b312-202">You overrode `prepareNotificationView:forContent:`, be sure toomap at least `onNotificationActioned` or `onNotificationExited` tooone of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="2b312-203">Если `handleNotification:` создает исключение, hello содержимого удаляется и `drop` — вызывается, это сообщение появляется в статистике и далее кампаний теперь могут быть обработаны.</span><span class="sxs-lookup"><span data-stu-id="2b312-203">If `handleNotification:` throws an exception, hello content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="2b312-204">Включение уведомления в состав существующего представления</span><span class="sxs-lookup"><span data-stu-id="2b312-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="2b312-205">Наложения хорошо подходят для быстрой интеграции, но иногда могут быть неудобными или приводить к нежелательным побочным эффектам.</span><span class="sxs-lookup"><span data-stu-id="2b312-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="2b312-206">Если вы не удовлетворены системы наложения hello в некоторых представлений, можно настроить его для этих представлений.</span><span class="sxs-lookup"><span data-stu-id="2b312-206">If you're not satisfied with hello overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="2b312-207">Решите, tooinclude нашей макета уведомления в существующие представления.</span><span class="sxs-lookup"><span data-stu-id="2b312-207">You can decide tooinclude our notification layout in your existing views.</span></span> <span data-ttu-id="2b312-208">toodo таким образом, есть два стиля реализации:</span><span class="sxs-lookup"><span data-stu-id="2b312-208">toodo so, there is two implementation styles:</span></span>

1. <span data-ttu-id="2b312-209">Добавить представление hello уведомления, с помощью построителя интерфейса</span><span class="sxs-lookup"><span data-stu-id="2b312-209">Add hello notification view using interface builder</span></span>

   * <span data-ttu-id="2b312-210">Откройте *конструктор интерфейса*</span><span class="sxs-lookup"><span data-stu-id="2b312-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="2b312-211">Поместите 320 x 60 (или если вы находитесь на iPad 768 x 60) `UIView` место tooappear уведомления hello</span><span class="sxs-lookup"><span data-stu-id="2b312-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want hello notification tooappear</span></span>
   * <span data-ttu-id="2b312-212">Значение hello тег для этого представления слишком: **36822491**</span><span class="sxs-lookup"><span data-stu-id="2b312-212">Set hello Tag value for this view too: **36822491**</span></span>
2. <span data-ttu-id="2b312-213">Добавьте представление уведомления hello программным способом.</span><span class="sxs-lookup"><span data-stu-id="2b312-213">Add hello notification view programmatically.</span></span> <span data-ttu-id="2b312-214">Просто добавьте следующий код, при инициализации представления hello:</span><span class="sxs-lookup"><span data-stu-id="2b312-214">Just add hello following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="2b312-215">Макрос `NOTIFICATION_AREA_VIEW_TAG` можно найти в файле `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="2b312-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="2b312-216">средство уведомления по умолчанию Hello автоматически обнаруживает макета hello уведомления включены в это представление и не будет добавлять наложение для него.</span><span class="sxs-lookup"><span data-stu-id="2b312-216">hello default notifier automatically detects that hello notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="2b312-217">Объявления и опросы</span><span class="sxs-lookup"><span data-stu-id="2b312-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="2b312-218">Макеты</span><span class="sxs-lookup"><span data-stu-id="2b312-218">Layouts</span></span>
<span data-ttu-id="2b312-219">Можно изменить файлы hello `AEDefaultAnnouncementView.xib` и `AEDefaultPollView.xib` до тех пор, пока сохранять значения тегов hello и типы hello существующих представлений.</span><span class="sxs-lookup"><span data-stu-id="2b312-219">You can modify hello files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep hello tag values and types of hello existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="2b312-220">Категории</span><span class="sxs-lookup"><span data-stu-id="2b312-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="2b312-221">Альтернативные макеты</span><span class="sxs-lookup"><span data-stu-id="2b312-221">Alternate layouts</span></span>
<span data-ttu-id="2b312-222">Подобно уведомления категория кампании hello может быть используется toohave дополнительные раскладки для объявлений и опросов.</span><span class="sxs-lookup"><span data-stu-id="2b312-222">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="2b312-223">toocreate категория для объявления, необходимо расширить **AEAnnouncementViewController** и зарегистрируйте его после инициализации модулем hello:</span><span class="sxs-lookup"><span data-stu-id="2b312-223">toocreate a category for an announcement, you must extend **AEAnnouncementViewController** and register it once hello reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="2b312-224">Каждый раз, пользователь нажимает кнопку на уведомления для объявления с категорией hello «my\_категории», контроллер зарегистрированных представление (в этом случае `MyCustomAnnouncementViewController`) инициализируются с помощью вызова метода hello `initWithAnnouncement:` и будет представление hello добавлены toohello текущего окна приложения.</span><span class="sxs-lookup"><span data-stu-id="2b312-224">Each time a user will click on a notification for an announcement with hello category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling hello method `initWithAnnouncement:` and hello view will be added toohello current application window.</span></span>
>
>

<span data-ttu-id="2b312-225">В такой реализации hello `AEAnnouncementViewController` классе имеется свойство hello tooread `announcement` tooinitialize вашей представлений.</span><span class="sxs-lookup"><span data-stu-id="2b312-225">In your implementation of hello `AEAnnouncementViewController` class you will have tooread hello property `announcement` tooinitialize your subviews.</span></span> <span data-ttu-id="2b312-226">Рассмотрим hello ниже пример, где два метки инициализируются с помощью `title` и `body` свойства hello `AEReachAnnouncement` класса:</span><span class="sxs-lookup"><span data-stu-id="2b312-226">Consider hello example below, where two labels are initialized using `title` and `body` properties of hello `AEReachAnnouncement` class:</span></span>

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

<span data-ttu-id="2b312-227">Если вы не хотите tooload вашим представлениям в одиночку, но необходимо просто разметки представления объявления по умолчанию hello tooreuse, можно просто сделать контроллер пользовательское представление расширяет класс hello предоставленный `AEDefaultAnnouncementViewController`.</span><span class="sxs-lookup"><span data-stu-id="2b312-227">If you don't want tooload your views by yourself but you just want tooreuse hello default announcement view layout, you can simply make your custom view controller extends hello provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="2b312-228">В этом случае повторяющийся файл hello nib `AEDefaultAnnouncementView.xib` и переименуйте его, поэтому ее можно загрузить в контроллере пользовательское представление (для контроллера с именем `CustomAnnouncementViewController`, необходимо вызвать файла nib `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="2b312-228">In that case, duplicate hello nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="2b312-229">категории по умолчанию hello tooreplace объявлений, просто регистрации контроллера настраиваемого представления для hello категории, определенной в `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="2b312-229">tooreplace hello default category of announcements, simply register your custom view controller for hello category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="2b312-230">Опрашивает может быть настроенный hello так же, как:</span><span class="sxs-lookup"><span data-stu-id="2b312-230">Polls can be customized hello same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="2b312-231">Это время, предоставляемые hello `MyCustomPollViewController` необходимо расширить `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="2b312-231">This time, hello provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="2b312-232">Или можно выбрать tooextend контроллера по умолчанию hello: `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="2b312-232">Or you can choose tooextend from hello default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b312-233">Не забывайте toocall либо `action` (`submitAnswers:` для контроллеров представления пользовательских опроса) или `exit` метод до закрытия hello представление-контроллер.</span><span class="sxs-lookup"><span data-stu-id="2b312-233">Don't forget toocall either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before hello view controller is dismissed.</span></span> <span data-ttu-id="2b312-234">В противном случае статистические данные не могут быть переданы (т. е. не analytics hello кампании) и не будет уведомлен дополнительные кампаний, что важно далее до перезапуска процесса приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2b312-234">Otherwise, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly next campaigns will not be notified until hello application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="2b312-235">Пример реализации</span><span class="sxs-lookup"><span data-stu-id="2b312-235">Implementation example</span></span>
<span data-ttu-id="2b312-236">В этой реализации представления пользовательских объявления hello загружается из файла внешних xib.</span><span class="sxs-lookup"><span data-stu-id="2b312-236">In this implementation hello custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="2b312-237">Как и для настройки дополнительных уведомлений рекомендуется toolook в исходный код hello hello стандартную реализацию.</span><span class="sxs-lookup"><span data-stu-id="2b312-237">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

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
