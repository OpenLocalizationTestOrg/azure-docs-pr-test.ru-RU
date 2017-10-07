---
title: "aaaAzure iOS Mobile Engagement Обзор пакета SDK | Документы Microsoft"
description: "Последние обновления и указания для пакета SDK для iOS для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 38f0da2f84df9c62f8fbca233bfda8b9936fdc0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="95df2-103">Пакет SDK для Служб мобильного взаимодействия Azure (iOS)</span><span class="sxs-lookup"><span data-stu-id="95df2-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="95df2-104">Начните здесь tooget все hello сведения о том, как toointegrate Azure Mobile Engagement в приложение iOS.</span><span class="sxs-lookup"><span data-stu-id="95df2-104">Start here tooget all hello details on how toointegrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="95df2-105">Если вы хотите toogive его try прежде всего убедитесь, вы нашей [15 минут учебника](mobile-engagement-ios-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="95df2-105">If you'd like toogive it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="95df2-106">Нажмите кнопку toosee hello [содержимого пакета SDK](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="95df2-106">Click toosee hello [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="95df2-107">Процедуры по интеграции</span><span class="sxs-lookup"><span data-stu-id="95df2-107">Integration procedures</span></span>
1. <span data-ttu-id="95df2-108">Начните здесь: [как toointegrate Mobile Engagement в приложения iOS](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="95df2-108">Start here: [How toointegrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="95df2-109">Для получения уведомлений: [как toointegrate Reach (уведомлений) в приложении iOS](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="95df2-109">For Notifications: [How toointegrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="95df2-110">Тег план реализации: [как toouse hello дополнительные теги API в приложении iOS Mobile Engagement](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="95df2-110">Tag plan implementation: [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="95df2-111">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="95df2-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="95df2-112">4.1.0 (17.07.2017)</span><span class="sxs-lookup"><span data-stu-id="95df2-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="95df2-113">Исправлена проблема с исчезающими на заднем фоне эмблемами.</span><span class="sxs-lookup"><span data-stu-id="95df2-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="95df2-114">Исправлена проблема с предупреждениями в XCode 9 о невызванных в основной очереди API-интерфейсах.</span><span class="sxs-lookup"><span data-stu-id="95df2-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="95df2-115">Исправлена утечка памяти при опросах охвата.</span><span class="sxs-lookup"><span data-stu-id="95df2-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="95df2-116">Прекращена поддержка iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="95df2-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="95df2-117">Начиная с этой версии цель развертывания hello приложения должен быть по крайней мере iOS 7.</span><span class="sxs-lookup"><span data-stu-id="95df2-117">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="95df2-118">Для более ранней версии см. в разделе hello [завершения заметки о выпуске](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="95df2-118">For earlier version please see hello [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="95df2-119">Процедуры обновления</span><span class="sxs-lookup"><span data-stu-id="95df2-119">Upgrade procedures</span></span>
<span data-ttu-id="95df2-120">Если уже имеется встроенный более старой версии участия в приложение, у вас есть hello tooconsider при обновлении hello SDK следующие точки.</span><span class="sxs-lookup"><span data-stu-id="95df2-120">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="95df2-121">Возможно, toofollow несколько процедур если пропущены несколько версий hello SDK см hello завершения [обновление процедуры](mobile-engagement-ios-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="95df2-121">You may have toofollow several procedures if you missed several versions of hello SDK see hello complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="95df2-122">Для каждой новой версии пакета SDK для hello сначала необходимо заменить (удалить и повторно импортировать в xcode) hello EngagementSDK и EngagementReach папки.</span><span class="sxs-lookup"><span data-stu-id="95df2-122">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-too400"></a><span data-ttu-id="95df2-123">Из 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="95df2-123">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="95df2-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="95df2-124">XCode 8</span></span>
<span data-ttu-id="95df2-125">XCode 8 является обязательным, начиная с версии 4.0.0 hello SDK.</span><span class="sxs-lookup"><span data-stu-id="95df2-125">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="95df2-126">Если действительно зависят XCode 7, то вы можете использовать hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="95df2-126">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="95df2-127">При работе на устройствах iOS 10 на hello модулем этой предыдущей версии имеется известная ошибка: не обработанных системных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="95df2-127">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="95df2-128">toofix будет иметь tooimplement hello нерекомендуемый API `application:didReceiveRemoteNotification:` в вашем приложении делегат следующим образом:</span><span class="sxs-lookup"><span data-stu-id="95df2-128">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="95df2-129">**Данный способ не является рекомендуемым** , так как это поведение может измениться с любым последующим (даже незначительным) обновлением версии iOS из-за того, что этот интерфейс API для iOS устарел.</span><span class="sxs-lookup"><span data-stu-id="95df2-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="95df2-130">Следует как можно быстрее перейти tooXCode 8.</span><span class="sxs-lookup"><span data-stu-id="95df2-130">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="95df2-131">Платформа UserNotifications</span><span class="sxs-lookup"><span data-stu-id="95df2-131">UserNotifications framework</span></span>
<span data-ttu-id="95df2-132">Требуется tooadd hello `UserNotifications` framework поэтапно сборки.</span><span class="sxs-lookup"><span data-stu-id="95df2-132">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="95df2-133">в обозревателе проектов hello откройте панель проекта и выберите правильный hello.</span><span class="sxs-lookup"><span data-stu-id="95df2-133">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="95df2-134">Откройте hello **«Этапы сборки»** вкладку и в hello **«Двоичный с библиотеками»** меню, добавление платформы `UserNotifications.framework` -задать связь hello как`Optional`</span><span class="sxs-lookup"><span data-stu-id="95df2-134">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="95df2-135">Функция push-уведомлений приложения</span><span class="sxs-lookup"><span data-stu-id="95df2-135">Application push capability</span></span>
<span data-ttu-id="95df2-136">Приложение может привести к сбросу XCode 8 принудительные возможность, проверьте его в hello `capability` вкладку выбранного целевого.</span><span class="sxs-lookup"><span data-stu-id="95df2-136">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

#### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="95df2-137">Добавление нового кода в регистрации iOS 10 уведомления hello</span><span class="sxs-lookup"><span data-stu-id="95df2-137">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="95df2-138">старые кода фрагмент tooregister hello приложение Hello toonotifications по-прежнему работает, но использует устаревшие интерфейсы API при выполнении с iOS 10.</span><span class="sxs-lookup"><span data-stu-id="95df2-138">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="95df2-139">Импорт hello `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="95df2-139">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="95df2-140">В методе `application:didFinishLaunchingWithOptions` делегата приложения замените:</span><span class="sxs-lookup"><span data-stu-id="95df2-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="95df2-141">на:</span><span class="sxs-lookup"><span data-stu-id="95df2-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="95df2-142">Разрешение конфликтов делегата UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="95df2-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="95df2-143">*Если приложения или библиотеки сторонних производителей не реализуют `UNUserNotificationCenterDelegate`, то эту часть можно пропустить.*</span><span class="sxs-lookup"><span data-stu-id="95df2-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="95df2-144">Объект `UNUserNotificationCenter` делегат используется hello SDK toomonitor hello жизненного цикла Engagement уведомлений на устройства под управлением IOS, 10 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="95df2-144">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="95df2-145">пакет SDK для Hello имеет собственную реализацию hello `UNUserNotificationCenterDelegate` протокола, но может быть только один `UNUserNotificationCenter` делегировать каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="95df2-145">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="95df2-146">Любого другого делегата добавлены toohello `UNUserNotificationCenter` объекта будут конфликтовать с hello Engagement один.</span><span class="sxs-lookup"><span data-stu-id="95df2-146">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="95df2-147">Если hello SDK обнаруживает делегата к или любые другие третьих лиц, то не будет использовать собственную реализацию toogive вы tooresolve вероятность hello конфликтов.</span><span class="sxs-lookup"><span data-stu-id="95df2-147">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="95df2-148">Вы должны будете tooadd hello Engagement логику tooyour владельцем делегата в порядке tooresolve hello конфликтов.</span><span class="sxs-lookup"><span data-stu-id="95df2-148">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="95df2-149">Существует два способа tooachieve это.</span><span class="sxs-lookup"><span data-stu-id="95df2-149">There are two ways tooachieve this.</span></span>

<span data-ttu-id="95df2-150">Предложение 1, просто переадресующей делегат вызывает toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="95df2-150">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="95df2-151">Или предложение 2, путем наследования от hello `AEUserNotificationHandler` класса</span><span class="sxs-lookup"><span data-stu-id="95df2-151">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="95df2-152">Можно определить, откуда уведомление на работе или не путем передачи его `userInfo` toohello словарь агента `isEngagementPushPayload:` методу класса.</span><span class="sxs-lookup"><span data-stu-id="95df2-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="95df2-153">Убедитесь в том, что hello `UNUserNotificationCenter` объекта делегата задается tooyour делегата в рамках либо hello `application:willFinishLaunchingWithOptions:` или hello `application:didFinishLaunchingWithOptions:` метод делегата вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="95df2-153">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="95df2-154">Например если реализовано hello выше предложение 1:</span><span class="sxs-lookup"><span data-stu-id="95df2-154">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
