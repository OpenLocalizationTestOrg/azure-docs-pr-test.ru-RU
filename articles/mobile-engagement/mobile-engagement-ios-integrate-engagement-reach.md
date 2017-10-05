---
title: "Службы мобильного взаимодействия Azure: интеграция пакета SDK Reach для iOS | Документация Майкрософт"
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
ms.openlocfilehash: ba74e0c442ac10f096d465f989e03d2ceae8cd88
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-integrate-engagement-reach-on-ios"></a><span data-ttu-id="defb4-103">Как интегрировать рекламные кампании Engagement в iOS</span><span class="sxs-lookup"><span data-stu-id="defb4-103">How to Integrate Engagement Reach on iOS</span></span>
<span data-ttu-id="defb4-104">Перед выполнением этого руководства вам следует выполнить процедуры по интеграции, описанные в статье [Интеграция службы Engagement в iOS](mobile-engagement-ios-integrate-engagement.md) .</span><span class="sxs-lookup"><span data-stu-id="defb4-104">You must follow the integration procedure described in the [How to Integrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="defb4-105">Также требуется установка XCode 8.</span><span class="sxs-lookup"><span data-stu-id="defb4-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="defb4-106">Если вам крайне важно оставить версию XCode 7, то можете воспользоваться [пакетом SDK Служб взаимодействия для iOS версии 3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="defb4-106">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="defb4-107">В предыдущей версии на устройствах iOS 10 выявлена ошибка: не приводятся в действие системные уведомления.</span><span class="sxs-lookup"><span data-stu-id="defb4-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="defb4-108">Для исправления этой ошибки понадобится реализовать в делегате приложения устаревшую версию API `application:didReceiveRemoteNotification:` :</span><span class="sxs-lookup"><span data-stu-id="defb4-108">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="defb4-109">**Данный способ не является рекомендуемым** , так как это поведение может измениться с любым последующим (даже незначительным) обновлением версии iOS из-за того, что этот интерфейс API для iOS устарел.</span><span class="sxs-lookup"><span data-stu-id="defb4-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="defb4-110">Рекомендуется перейти на XCode 8 как можно скорее.</span><span class="sxs-lookup"><span data-stu-id="defb4-110">You should switch to XCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="defb4-111">Включение приложения для получения автоматических push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="defb4-111">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="defb4-112">Этапы интеграции</span><span class="sxs-lookup"><span data-stu-id="defb4-112">Integration steps</span></span>
### <a name="embed-the-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="defb4-113">Внедрение пакета SDK для Engagement Reach в проект iOS</span><span class="sxs-lookup"><span data-stu-id="defb4-113">Embed the Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="defb4-114">Добавьте пакет SDK для рекламных кампаний в проект Xcode.</span><span class="sxs-lookup"><span data-stu-id="defb4-114">Add the Reach sdk in your Xcode project.</span></span> <span data-ttu-id="defb4-115">В Xcode щелкните **Проект \> Добавить в проект** и выберите папку `EngagementReach`.</span><span class="sxs-lookup"><span data-stu-id="defb4-115">In Xcode, go to **Project \> Add to project** and choose the `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="defb4-116">Изменение делегата приложения</span><span class="sxs-lookup"><span data-stu-id="defb4-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="defb4-117">Импортируйте модуль обработки рекламных кампаний службы Engagement в верхней части файла реализации:</span><span class="sxs-lookup"><span data-stu-id="defb4-117">At the top of your implementation file, import the Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="defb4-118">Создайте внутри метода `applicationDidFinishLaunching:` или `application:didFinishLaunchingWithOptions:` модуль обработки рекламных кампаний и передайте его в существующую строку инициализации службы Engagement:</span><span class="sxs-lookup"><span data-stu-id="defb4-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it to your existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="defb4-119">Измените строку **icon.png** на имя изображения, которое вы хотите использовать в качестве значка уведомления.</span><span class="sxs-lookup"><span data-stu-id="defb4-119">Modify **'icon.png'** string with the image name you want as your notification icon.</span></span>
* <span data-ttu-id="defb4-120">Если вы хотите использовать параметр *Обновить значение индикатора событий* в рекламных кампаниях или применять кампании системных push-уведомлений \</SaaS/Reach API/Campaign format/Native Push\>, следует разрешить модулю обработки рекламных кампаний управлять значком индикатора событий (он будет автоматически очищать индикатор событий приложения и сбрасывать значение, хранимое службой Engagement, при каждом запуске приложения или его переключении на передний план).</span><span class="sxs-lookup"><span data-stu-id="defb4-120">If you want to use the option *Update badge value* in Reach campaigns or if you want to use native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let the Reach module manage the badge icon itself (it will automatically clear the application badge and also reset the value stored by Engagement every time the application is started or foregrounded).</span></span> <span data-ttu-id="defb4-121">Для этого после инициализации модуля обработки рекламных кампаний необходимо добавить следующую строку:</span><span class="sxs-lookup"><span data-stu-id="defb4-121">This is done by adding the following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="defb4-122">Чтобы обрабатывать отправку данных рекламных кампаний, делегат приложения должен соответствовать протоколу `AEReachDataPushDelegate` .</span><span class="sxs-lookup"><span data-stu-id="defb4-122">If you want to handle Reach data push, you must let your Application delegate conform to the `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="defb4-123">После инициализации модуля обработки рекламных кампаний добавьте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="defb4-123">Add the following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="defb4-124">Затем можно реализовать методы `onDataPushStringReceived:` и `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` в делегате приложения:</span><span class="sxs-lookup"><span data-stu-id="defb4-124">Then you can implement the methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

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

### <a name="category"></a><span data-ttu-id="defb4-125">Категория</span><span class="sxs-lookup"><span data-stu-id="defb4-125">Category</span></span>
<span data-ttu-id="defb4-126">При создании кампании отправки данных параметр «Категория» является необязательным. Он позволяет фильтровать отправленные данные.</span><span class="sxs-lookup"><span data-stu-id="defb4-126">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="defb4-127">Это удобно, если вам нужно принудительно отправлять различные данные `Base64` и определять их тип перед анализом.</span><span class="sxs-lookup"><span data-stu-id="defb4-127">This is useful if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

<span data-ttu-id="defb4-128">**Теперь приложение готово к получению и отображению содержимого рекламных кампаний!**</span><span class="sxs-lookup"><span data-stu-id="defb4-128">**Your application is now ready to receive and display reach contents!**</span></span>

## <a name="how-to-receive-announcements-and-polls-at-any-time"></a><span data-ttu-id="defb4-129">Как получать объявления и опросы в любое время</span><span class="sxs-lookup"><span data-stu-id="defb4-129">How to receive announcements and polls at any time</span></span>
<span data-ttu-id="defb4-130">С помощью службы push-уведомлений Apple служба Engagement может в любое время отправлять уведомления рекламных кампаний конечным пользователям.</span><span class="sxs-lookup"><span data-stu-id="defb4-130">Engagement can send Reach notifications to your end users at any time by using the Apple Push Notification Service.</span></span>

<span data-ttu-id="defb4-131">Чтобы включить эту функциональную возможность, необходимо подготовить приложение для push-уведомлений Apple и изменить его делегат.</span><span class="sxs-lookup"><span data-stu-id="defb4-131">To enable this functionality, you'll have to prepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="defb4-132">Подготовка приложения для push-уведомлений Apple</span><span class="sxs-lookup"><span data-stu-id="defb4-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="defb4-133">Следуйте указаниям в руководстве [Как подготовить приложение для работы с push-уведомлениями Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="defb4-133">Please follow the guide : [How to Prepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-the-necessary-client-code"></a><span data-ttu-id="defb4-134">Добавление необходимого клиентского кода</span><span class="sxs-lookup"><span data-stu-id="defb4-134">Add the necessary client code</span></span>
<span data-ttu-id="defb4-135">*На этом этапе для приложения должен быть зарегистрирован сертификат push-уведомлений Apple в интерфейсной части Engagement.*</span><span class="sxs-lookup"><span data-stu-id="defb4-135">*At this point your application should have a registered Apple push certificate in the Engagement frontend.*</span></span>

<span data-ttu-id="defb4-136">Если он не зарегистрирован, необходимо зарегистрировать приложение для получения push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="defb4-136">If it's not done already, you need to register your application to receive push notifications.</span></span>

* <span data-ttu-id="defb4-137">Импортируйте платформу `User Notification` :</span><span class="sxs-lookup"><span data-stu-id="defb4-137">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="defb4-138">Добавьте следующую строку при запуске приложения (обычно в `application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="defb4-138">Add the following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="defb4-139">Затем необходимо предоставить службе Engagement маркер устройства, возвращенный серверами Apple.</span><span class="sxs-lookup"><span data-stu-id="defb4-139">Then, You need to provide to Engagement the device token returned by Apple servers.</span></span> <span data-ttu-id="defb4-140">Он указывается в делегате приложения в методе с именем `application:didRegisterForRemoteNotificationsWithDeviceToken:` :</span><span class="sxs-lookup"><span data-stu-id="defb4-140">This is done in the method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="defb4-141">Наконец необходимо уведомить пакет SDK для службы Engagement о получении приложением удаленного уведомления.</span><span class="sxs-lookup"><span data-stu-id="defb4-141">Finally, you have to inform the Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="defb4-142">Для этого вызовите метод `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` в делегате приложения:</span><span class="sxs-lookup"><span data-stu-id="defb4-142">To do that, call the method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="defb4-143">По умолчанию completionHandler управляется Engagement Reach.</span><span class="sxs-lookup"><span data-stu-id="defb4-143">By default, Engagement Reach controls the completionHandler.</span></span> <span data-ttu-id="defb4-144">Если вы хотите вручную отреагировать на блок `handler`в коде, можно передать nil для аргумента `handler` и управлять блоком завершения самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="defb4-144">If you want to manually respond to the `handler` block in your code, you can pass nil for the `handler` argument and control the completion block yourself.</span></span> <span data-ttu-id="defb4-145">Список возможных значений см. в описании типа `UIBackgroundFetchResult`.</span><span class="sxs-lookup"><span data-stu-id="defb4-145">See the `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="defb4-146">Полный пример</span><span class="sxs-lookup"><span data-stu-id="defb4-146">Full example</span></span>
<span data-ttu-id="defb4-147">Ниже приведен полный пример интеграции:</span><span class="sxs-lookup"><span data-stu-id="defb4-147">Here is a full example of integration:</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="defb4-148">Разрешение конфликтов делегата UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="defb4-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="defb4-149">*Если приложения или библиотеки сторонних производителей не реализуют `UNUserNotificationCenterDelegate`, то эту часть можно пропустить.*</span><span class="sxs-lookup"><span data-stu-id="defb4-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="defb4-150">Делегат `UNUserNotificationCenter` используется пакетом SDK для отслеживания жизненного цикла уведомлений служб Engagement на устройствах, работающих под управлением iOS 10 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="defb4-150">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="defb4-151">Пакет SDK содержит собственную реализацию протокола `UNUserNotificationCenterDelegate`, однако в приложении может быть только один делегат `UNUserNotificationCenter`.</span><span class="sxs-lookup"><span data-stu-id="defb4-151">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="defb4-152">Любой другой делегат, добавляемый в объект `UNUserNotificationCenter`, будет конфликтовать со службой Engagement.</span><span class="sxs-lookup"><span data-stu-id="defb4-152">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="defb4-153">Если пакет SDK обнаружит ваш или другой делегат, он не будет применять собственную реализацию, чтобы дать вам возможность самому разрешить конфликт.</span><span class="sxs-lookup"><span data-stu-id="defb4-153">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="defb4-154">Для разрешения конфликтов вам потребуется добавить приложение логики Engagement в собственный делегат.</span><span class="sxs-lookup"><span data-stu-id="defb4-154">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="defb4-155">Это достигается двумя способами.</span><span class="sxs-lookup"><span data-stu-id="defb4-155">There are two ways to achieve this.</span></span>

<span data-ttu-id="defb4-156">Первый способ. Просто переадресуйте вызовы делегата в пакет SDK:</span><span class="sxs-lookup"><span data-stu-id="defb4-156">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="defb4-157">Второй способ. Воспользуйтесь наследованием из класса `AEUserNotificationHandler`:</span><span class="sxs-lookup"><span data-stu-id="defb4-157">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="defb4-158">Можно определить, поступают ли уведомления из Служб взаимодействия, передав словарь `userInfo` в метод класса `isEngagementPushPayload:` агента.</span><span class="sxs-lookup"><span data-stu-id="defb4-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="defb4-159">Убедитесь, что в делегате приложения делегат объекта `UNUserNotificationCenter` имеет значение вашего делегата в методе `application:willFinishLaunchingWithOptions:` или `application:didFinishLaunchingWithOptions:`.</span><span class="sxs-lookup"><span data-stu-id="defb4-159">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="defb4-160">Например, если вы воспользовались первым способом:</span><span class="sxs-lookup"><span data-stu-id="defb4-160">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="defb4-161">Как настраивать кампании</span><span class="sxs-lookup"><span data-stu-id="defb4-161">How to customize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="defb4-162">Уведомления</span><span class="sxs-lookup"><span data-stu-id="defb4-162">Notifications</span></span>
<span data-ttu-id="defb4-163">Существует два типа уведомлений: системные уведомления и уведомления в приложении.</span><span class="sxs-lookup"><span data-stu-id="defb4-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="defb4-164">Системные уведомления обрабатываются iOS, и их невозможно настроить.</span><span class="sxs-lookup"><span data-stu-id="defb4-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="defb4-165">Уведомления в приложении состоят из представления, которое динамически добавляется в текущее окно приложения.</span><span class="sxs-lookup"><span data-stu-id="defb4-165">In-app notifications are made of a view that is dynamically added to the current application window.</span></span> <span data-ttu-id="defb4-166">Это называется наложением уведомлений.</span><span class="sxs-lookup"><span data-stu-id="defb4-166">This is called a notification overlay.</span></span> <span data-ttu-id="defb4-167">Наложения уведомления прекрасно подходят для быстрой интеграции, так как для них не требуется изменять представления в приложении.</span><span class="sxs-lookup"><span data-stu-id="defb4-167">Notification overlays are great for a fast integration because they does not require you to modify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="defb4-168">Макет</span><span class="sxs-lookup"><span data-stu-id="defb4-168">Layout</span></span>
<span data-ttu-id="defb4-169">Чтобы настроить внешний вид уведомлений в приложении, вы можете просто изменить файл `AENotificationView.xib` в соответствии со своими потребностями, но при этом следует сохранить значения тегов и типы существующих вложенных представлений.</span><span class="sxs-lookup"><span data-stu-id="defb4-169">To modify the look of your in-app notifications, you can simply modify the file `AENotificationView.xib` to your needs, as long as you keep the tag values and types of the existing subviews.</span></span>

<span data-ttu-id="defb4-170">По умолчанию уведомления в приложении представлены в нижней части экрана.</span><span class="sxs-lookup"><span data-stu-id="defb4-170">By default, in-app notifications are presented at the bottom of the screen.</span></span> <span data-ttu-id="defb4-171">Если нужно, чтобы они отображались в верхней части экрана, отредактируйте предоставляемый файл `AENotificationView.xib` и измените свойство `AutoSizing` главного представления, чтобы оно располагалось в верхней части суперпредставления.</span><span class="sxs-lookup"><span data-stu-id="defb4-171">If you prefer to display them at the top of screen, edit the provided `AENotificationView.xib` and change the `AutoSizing` property of the main view so it can be kept at the top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="defb4-172">Категории</span><span class="sxs-lookup"><span data-stu-id="defb4-172">Categories</span></span>
<span data-ttu-id="defb4-173">При изменении предоставляемого макета изменяется внешний вид всех уведомлений.</span><span class="sxs-lookup"><span data-stu-id="defb4-173">When you modify the provided layout, you modify the look of all your notifications.</span></span> <span data-ttu-id="defb4-174">С помощью категорий можно определять различные типы внешнего вида (возможно, виды поведения) для уведомлений.</span><span class="sxs-lookup"><span data-stu-id="defb4-174">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="defb4-175">Категорию можно указать при создании рекламной кампании.</span><span class="sxs-lookup"><span data-stu-id="defb4-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="defb4-176">Учтите, что категории также позволяют настраивать объявления и опросы. Это описано далее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="defb4-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="defb4-177">Чтобы зарегистрировать обработчик категорий для уведомлений, необходимо добавить вызов после инициализации модуля обработки рекламных кампаний.</span><span class="sxs-lookup"><span data-stu-id="defb4-177">To register a category handler for your notifications, you need to add a call once the reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="defb4-178">`myNotifier` должен быть экземпляром объекта, который соответствует протоколу `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="defb4-178">`myNotifier` must be an instance of an object that conforms to the protocol `AENotifier`.</span></span>

<span data-ttu-id="defb4-179">Вы можете самостоятельно реализовать методы протокола или повторно реализовать существующий класс `AEDefaultNotifier`, который уже выполняет большую часть работы.</span><span class="sxs-lookup"><span data-stu-id="defb4-179">You can implement the protocol methods by yourself or you can choose to reimplement the existing class `AEDefaultNotifier` which already performs most of the work.</span></span>

<span data-ttu-id="defb4-180">Например, если нужно переопределить представление уведомлений для определенной категории, можно использовать этот пример:</span><span class="sxs-lookup"><span data-stu-id="defb4-180">For example, if you want to redefine the notification view for a specific category, you can follow this example:</span></span>

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

<span data-ttu-id="defb4-181">В этом простом примере категории предполагается, что в основном наборе приложений есть файл с именем `MyNotificationView.xib` .</span><span class="sxs-lookup"><span data-stu-id="defb4-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="defb4-182">Если методу не удается найти соответствующий файл `.xib`, уведомление не будет отображаться и служба Engagement выведет сообщение н консоли.</span><span class="sxs-lookup"><span data-stu-id="defb4-182">If the method is not able to find a corresponding `.xib`, the notification will not be displayed and Engagement will output a message in the console.</span></span>

<span data-ttu-id="defb4-183">Предоставленный NIB-файл должен подчиняться следующим правилам:</span><span class="sxs-lookup"><span data-stu-id="defb4-183">The provided nib file should respect the following rules:</span></span>

* <span data-ttu-id="defb4-184">он должен содержать только одно представление;</span><span class="sxs-lookup"><span data-stu-id="defb4-184">It should only contain one view.</span></span>
* <span data-ttu-id="defb4-185">вложенные представления должны относиться к тому же типу, что и вложенные представления в предоставленном NIB-файле с именем `AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="defb4-185">Subviews should be of the same types as the ones inside the provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="defb4-186">вложенные представления должны содержать те же теги, что и вложенные представления в предоставленном NIB-файле с именем `AENotificationView.xib`.</span><span class="sxs-lookup"><span data-stu-id="defb4-186">Subviews should have the same tags as the ones inside the provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="defb4-187">Просто скопируйте предоставленный NIB-файл с именем `AENotificationView.xib` и начните работу.</span><span class="sxs-lookup"><span data-stu-id="defb4-187">Just copy the provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="defb4-188">Но будьте внимательны: представление в этом NIB-файле связано в классом `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="defb4-188">But be careful, the view inside this nib file is associated to the class `AENotificationView`.</span></span> <span data-ttu-id="defb4-189">Этот класс переопределяет метод `layoutSubViews` , чтобы перемещать и изменять размер вложенных представлений в зависимости от контекста.</span><span class="sxs-lookup"><span data-stu-id="defb4-189">This class redefined the method `layoutSubViews` to move and resize its subviews according to context.</span></span> <span data-ttu-id="defb4-190">Вы можете заменить его классом `UIView` или настраиваемым классом представления.</span><span class="sxs-lookup"><span data-stu-id="defb4-190">You may want to replace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="defb4-191">Если вам требуется расширенная настройка уведомлений (например, если вам нужно загружать представление непосредственно из кода), советуем просмотреть предоставленную документацию по исходному коду и классу для `Protocol ReferencesDefaultNotifier` и `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="defb4-191">If you need deeper customization of your notifications(if you want for instance to load your view directly from the code), it is recommended to take a look at the provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="defb4-192">Обратите внимание, что одно и то же средство уведомления можно использовать для нескольких категорий.</span><span class="sxs-lookup"><span data-stu-id="defb4-192">Note that you can use the same notifier for multiple categories.</span></span>

<span data-ttu-id="defb4-193">Кроме того, можно переопределить средство уведомления по умолчанию следующим образом:</span><span class="sxs-lookup"><span data-stu-id="defb4-193">You can also redefined the default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="defb4-194">Обработка уведомлений</span><span class="sxs-lookup"><span data-stu-id="defb4-194">Notification handling</span></span>
<span data-ttu-id="defb4-195">При использовании категории по умолчанию некоторые методы жизненного цикла вызываются для объекта `AEReachContent`, чтобы предоставить статистику и обновить состояние кампании:</span><span class="sxs-lookup"><span data-stu-id="defb4-195">When using the default category, some life cycle methods are called on the `AEReachContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="defb4-196">При отображении уведомления в приложении `AEReachModule` вызывает метод `displayNotification` (который предоставляет статистику), если `handleNotification:` возвращает `YES`.</span><span class="sxs-lookup"><span data-stu-id="defb4-196">When the notification is displayed in application, the `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="defb4-197">При закрытии уведомления вызывается метод `exitNotification` и предоставляется статистика, после чего можно обрабатывать следующие кампании.</span><span class="sxs-lookup"><span data-stu-id="defb4-197">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="defb4-198">По щелчку уведомления вызывается метод `actionNotification` , предоставляется статистика и выполняется соответствующее действие.</span><span class="sxs-lookup"><span data-stu-id="defb4-198">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated action is performed.</span></span>

<span data-ttu-id="defb4-199">Если ваша реализация `AENotifier` обходит поведение по умолчанию, необходимо вызывать эти методы жизненного цикла самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="defb4-199">If your implementation of `AENotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="defb4-200">В следующих примерах показаны некоторые случаи обхода поведения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="defb4-200">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="defb4-201">Вы не расширяли `AEDefaultNotifier`, например реализовали обработку категорий с нуля.</span><span class="sxs-lookup"><span data-stu-id="defb4-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="defb4-202">Вы переопределили `prepareNotificationView:forContent:`. Обязательно сопоставьте хотя бы `onNotificationActioned` или `onNotificationExited` с одним из элементов управления пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="defb4-202">You overrode `prepareNotificationView:forContent:`, be sure to map at least `onNotificationActioned` or `onNotificationExited` to one of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="defb4-203">Если `handleNotification:` вызывает исключение, содержимое удаляется и вызывается `drop`. Затем это поведение регистрируется в статистике, после чего можно обрабатывать следующие кампании.</span><span class="sxs-lookup"><span data-stu-id="defb4-203">If `handleNotification:` throws an exception, the content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="defb4-204">Включение уведомления в состав существующего представления</span><span class="sxs-lookup"><span data-stu-id="defb4-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="defb4-205">Наложения хорошо подходят для быстрой интеграции, но иногда могут быть неудобными или приводить к нежелательным побочным эффектам.</span><span class="sxs-lookup"><span data-stu-id="defb4-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="defb4-206">Если вы не удовлетворены системой наложения в некоторых представлениях, ее можно настроить.</span><span class="sxs-lookup"><span data-stu-id="defb4-206">If you're not satisfied with the overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="defb4-207">Вы можете включить наш макет уведомлений в существующие представления.</span><span class="sxs-lookup"><span data-stu-id="defb4-207">You can decide to include our notification layout in your existing views.</span></span> <span data-ttu-id="defb4-208">Это можно выполнить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="defb4-208">To do so, there is two implementation styles:</span></span>

1. <span data-ttu-id="defb4-209">Добавьте представление уведомлений с помощью конструктора интерфейса:</span><span class="sxs-lookup"><span data-stu-id="defb4-209">Add the notification view using interface builder</span></span>

   * <span data-ttu-id="defb4-210">Откройте *конструктор интерфейса*</span><span class="sxs-lookup"><span data-stu-id="defb4-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="defb4-211">Разместите `UIView` размером 320 x 60 (или 768 x6 0 для iPad) там, где следует отображать уведомление.</span><span class="sxs-lookup"><span data-stu-id="defb4-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want the notification to appear</span></span>
   * <span data-ttu-id="defb4-212">Задайте для параметра «Тег» значение **36822491**</span><span class="sxs-lookup"><span data-stu-id="defb4-212">Set the Tag value for this view to : **36822491**</span></span>
2. <span data-ttu-id="defb4-213">Добавьте представление уведомлений программно.</span><span class="sxs-lookup"><span data-stu-id="defb4-213">Add the notification view programmatically.</span></span> <span data-ttu-id="defb4-214">Просто добавьте следующий код после инициализации представления:</span><span class="sxs-lookup"><span data-stu-id="defb4-214">Just add the following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values to your needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="defb4-215">Макрос `NOTIFICATION_AREA_VIEW_TAG` можно найти в файле `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="defb4-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="defb4-216">Средство уведомлений по умолчанию автоматически обнаруживает включение макета уведомлений в это представление и не будет добавлять наложение для него.</span><span class="sxs-lookup"><span data-stu-id="defb4-216">The default notifier automatically detects that the notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="defb4-217">Объявления и опросы</span><span class="sxs-lookup"><span data-stu-id="defb4-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="defb4-218">Макеты</span><span class="sxs-lookup"><span data-stu-id="defb4-218">Layouts</span></span>
<span data-ttu-id="defb4-219">Вы можете изменить файлы `AEDefaultAnnouncementView.xib` и `AEDefaultPollView.xib`, сохранив при этом значения тегов и типы существующих вложенных представлений.</span><span class="sxs-lookup"><span data-stu-id="defb4-219">You can modify the files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep the tag values and types of the existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="defb4-220">Категории</span><span class="sxs-lookup"><span data-stu-id="defb4-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="defb4-221">Альтернативные макеты</span><span class="sxs-lookup"><span data-stu-id="defb4-221">Alternate layouts</span></span>
<span data-ttu-id="defb4-222">Так же, как и категорию уведомлений, категорию кампании можно использовать для получения альтернативных макетов для объявлений и опросов.</span><span class="sxs-lookup"><span data-stu-id="defb4-222">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="defb4-223">Чтобы создать категорию для объявления, необходимо расширить **AEAnnouncementViewController** и зарегистрировать его после инициализации модуля обработки рекламных кампаний:</span><span class="sxs-lookup"><span data-stu-id="defb4-223">To create a category for an announcement, you must extend **AEAnnouncementViewController** and register it once the reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="defb4-224">По каждому щелчку уведомления для объявления с категорией my\_category будет выполняться инициализация зарегистрированного контроллера представлений (в этом случае `MyCustomAnnouncementViewController`) путем вызова метода `initWithAnnouncement:`, а представление будет добавляться в текущее окно приложения.</span><span class="sxs-lookup"><span data-stu-id="defb4-224">Each time a user will click on a notification for an announcement with the category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling the method `initWithAnnouncement:` and the view will be added to the current application window.</span></span>
>
>

<span data-ttu-id="defb4-225">В своей реализации класса `AEAnnouncementViewController` для инициализации вложенных представлений вам потребуется считать свойство `announcement`.</span><span class="sxs-lookup"><span data-stu-id="defb4-225">In your implementation of the `AEAnnouncementViewController` class you will have to read the property `announcement` to initialize your subviews.</span></span> <span data-ttu-id="defb4-226">Рассмотрите следующий пример, в котором две метки инициализируются с помощью свойств `title` и `body` класса `AEReachAnnouncement`:</span><span class="sxs-lookup"><span data-stu-id="defb4-226">Consider the example below, where two labels are initialized using `title` and `body` properties of the `AEReachAnnouncement` class:</span></span>

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

<span data-ttu-id="defb4-227">Если вместо того, чтобы загружать представления самостоятельно, вы хотите повторно использовать стандартный макет представления объявления по умолчанию, можно просто расширить предоставленный класс `AEDefaultAnnouncementViewController`с помощью пользовательского контролера представлений.</span><span class="sxs-lookup"><span data-stu-id="defb4-227">If you don't want to load your views by yourself but you just want to reuse the default announcement view layout, you can simply make your custom view controller extends the provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="defb4-228">Для этого продублируйте NIB-файл `AEDefaultAnnouncementView.xib` и переименуйте его, чтобы пользовательский контролер представлений мог загрузить его (для контроллера с именем `CustomAnnouncementViewController` NIB-файл нужно назвать `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="defb4-228">In that case, duplicate the nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="defb4-229">Чтобы заменить категорию объявлений по умолчанию, просто зарегистрируйте пользовательский контролер представлений для категории, определенной в `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="defb4-229">To replace the default category of announcements, simply register your custom view controller for the category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="defb4-230">Опросы можно настроить так же:</span><span class="sxs-lookup"><span data-stu-id="defb4-230">Polls can be customized the same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="defb4-231">В этом случае предоставленный `MyCustomPollViewController` должен расширять `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="defb4-231">This time, the provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="defb4-232">Или же можно расширить его с помощью контроллера по умолчанию: `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="defb4-232">Or you can choose to extend from the default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="defb4-233">Прежде чем закрыть контролер представлений, обязательно вызовите метод `action` (`submitAnswers:` для пользовательских контроллеров представлений опросов) или `exit`.</span><span class="sxs-lookup"><span data-stu-id="defb4-233">Don't forget to call either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before the view controller is dismissed.</span></span> <span data-ttu-id="defb4-234">В противном случае статистика не будет отправлена (т. е. не будет получена аналитика по кампании) и, что важнее, следующие кампании не будут получать уведомления до перезапуска процесса приложения.</span><span class="sxs-lookup"><span data-stu-id="defb4-234">Otherwise, statistics won't be sent (i.e. no analytics on the campaign) and more importantly next campaigns will not be notified until the application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="defb4-235">Пример реализации</span><span class="sxs-lookup"><span data-stu-id="defb4-235">Implementation example</span></span>
<span data-ttu-id="defb4-236">В этой реализации пользовательское представление объявлений загружается из внешнего XIB-файла.</span><span class="sxs-lookup"><span data-stu-id="defb4-236">In this implementation the custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="defb4-237">Так же, как и для расширенной настройки уведомлений, мы советуем просмотреть исходный код в стандартной реализации.</span><span class="sxs-lookup"><span data-stu-id="defb4-237">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

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
