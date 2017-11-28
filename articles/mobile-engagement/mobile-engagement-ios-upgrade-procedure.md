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
# <a name="upgrade-procedures"></a><span data-ttu-id="2c518-103">Процедуры обновления</span><span class="sxs-lookup"><span data-stu-id="2c518-103">Upgrade procedures</span></span>
<span data-ttu-id="2c518-104">Если уже имеется встроенный более старой версии участия в приложение, у вас есть hello tooconsider при обновлении hello SDK следующие точки.</span><span class="sxs-lookup"><span data-stu-id="2c518-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="2c518-105">Для каждой новой версии пакета SDK для hello сначала необходимо заменить (удалить и повторно импортировать в xcode) hello EngagementSDK и EngagementReach папки.</span><span class="sxs-lookup"><span data-stu-id="2c518-105">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="2c518-106">Из 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="2c518-106">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="2c518-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="2c518-107">XCode 8</span></span>
<span data-ttu-id="2c518-108">XCode 8 является обязательным, начиная с версии 4.0.0 hello SDK.</span><span class="sxs-lookup"><span data-stu-id="2c518-108">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="2c518-109">Если действительно зависят XCode 7, то вы можете использовать hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="2c518-109">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="2c518-110">При работе на устройствах iOS 10 на hello модулем этой предыдущей версии имеется известная ошибка: не обработанных системных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="2c518-110">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="2c518-111">toofix будет иметь tooimplement hello нерекомендуемый API `application:didReceiveRemoteNotification:` в вашем приложении делегат следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2c518-111">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="2c518-112">**Данный способ не является рекомендуемым** , так как это поведение может измениться с любым последующим (даже незначительным) обновлением версии iOS из-за того, что этот интерфейс API для iOS устарел.</span><span class="sxs-lookup"><span data-stu-id="2c518-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="2c518-113">Следует как можно быстрее перейти tooXCode 8.</span><span class="sxs-lookup"><span data-stu-id="2c518-113">You should switch tooXCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="2c518-114">Платформа UserNotifications</span><span class="sxs-lookup"><span data-stu-id="2c518-114">UserNotifications framework</span></span>
<span data-ttu-id="2c518-115">Требуется tooadd hello `UserNotifications` framework поэтапно сборки.</span><span class="sxs-lookup"><span data-stu-id="2c518-115">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="2c518-116">в обозревателе проектов hello откройте панель проекта и выберите правильный hello.</span><span class="sxs-lookup"><span data-stu-id="2c518-116">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="2c518-117">Откройте hello **«Этапы сборки»** вкладку и в hello **«Двоичный с библиотеками»** меню, добавление платформы `UserNotifications.framework` -задать связь hello как`Optional`</span><span class="sxs-lookup"><span data-stu-id="2c518-117">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="2c518-118">Функция push-уведомлений приложения</span><span class="sxs-lookup"><span data-stu-id="2c518-118">Application push capability</span></span>
<span data-ttu-id="2c518-119">Приложение может привести к сбросу XCode 8 принудительные возможность, проверьте его в hello `capability` вкладку выбранного целевого.</span><span class="sxs-lookup"><span data-stu-id="2c518-119">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="2c518-120">Добавление нового кода в регистрации iOS 10 уведомления hello</span><span class="sxs-lookup"><span data-stu-id="2c518-120">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="2c518-121">старые кода фрагмент tooregister hello приложение Hello toonotifications по-прежнему работает, но использует устаревшие интерфейсы API при выполнении с iOS 10.</span><span class="sxs-lookup"><span data-stu-id="2c518-121">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="2c518-122">Импорт hello `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="2c518-122">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="2c518-123">В методе `application:didFinishLaunchingWithOptions` делегата приложения замените:</span><span class="sxs-lookup"><span data-stu-id="2c518-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="2c518-124">на:</span><span class="sxs-lookup"><span data-stu-id="2c518-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="2c518-125">Разрешение конфликтов делегата UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="2c518-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="2c518-126">*Если приложения или библиотеки сторонних производителей не реализуют `UNUserNotificationCenterDelegate`, то эту часть можно пропустить.*</span><span class="sxs-lookup"><span data-stu-id="2c518-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="2c518-127">Объект `UNUserNotificationCenter` делегат используется hello SDK toomonitor hello жизненного цикла Engagement уведомлений на устройства под управлением IOS, 10 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="2c518-127">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="2c518-128">пакет SDK для Hello имеет собственную реализацию hello `UNUserNotificationCenterDelegate` протокола, но может быть только один `UNUserNotificationCenter` делегировать каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="2c518-128">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="2c518-129">Любого другого делегата добавлены toohello `UNUserNotificationCenter` объекта будут конфликтовать с hello Engagement один.</span><span class="sxs-lookup"><span data-stu-id="2c518-129">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="2c518-130">Если hello SDK обнаруживает делегата к или любые другие третьих лиц, то не будет использовать собственную реализацию toogive вы tooresolve вероятность hello конфликтов.</span><span class="sxs-lookup"><span data-stu-id="2c518-130">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="2c518-131">Вы должны будете tooadd hello Engagement логику tooyour владельцем делегата в порядке tooresolve hello конфликтов.</span><span class="sxs-lookup"><span data-stu-id="2c518-131">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="2c518-132">Существует два способа tooachieve это.</span><span class="sxs-lookup"><span data-stu-id="2c518-132">There are two ways tooachieve this.</span></span>

<span data-ttu-id="2c518-133">Предложение 1, просто переадресующей делегат вызывает toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="2c518-133">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="2c518-134">Или предложение 2, путем наследования от hello `AEUserNotificationHandler` класса</span><span class="sxs-lookup"><span data-stu-id="2c518-134">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="2c518-135">Можно определить, откуда уведомление на работе или не путем передачи его `userInfo` toohello словарь агента `isEngagementPushPayload:` методу класса.</span><span class="sxs-lookup"><span data-stu-id="2c518-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="2c518-136">Убедитесь в том, что hello `UNUserNotificationCenter` объекта делегата задается tooyour делегата в рамках либо hello `application:willFinishLaunchingWithOptions:` или hello `application:didFinishLaunchingWithOptions:` метод делегата вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="2c518-136">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="2c518-137">Например если реализовано hello выше предложение 1:</span><span class="sxs-lookup"><span data-stu-id="2c518-137">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a><span data-ttu-id="2c518-138">Из 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="2c518-138">From 2.0.0 too3.0.0</span></span>
<span data-ttu-id="2c518-139">Прекращена поддержка iOS 4.X.</span><span class="sxs-lookup"><span data-stu-id="2c518-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="2c518-140">Начиная с этой версии цель развертывания hello приложения должен быть по крайней мере iOS 6.</span><span class="sxs-lookup"><span data-stu-id="2c518-140">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="2c518-141">Если вы используете Reach в приложении, необходимо добавить `remote-notification` toohello значение `UIBackgroundModes` массива в файле Info.plist в порядке tooreceive удаленного уведомления.</span><span class="sxs-lookup"><span data-stu-id="2c518-141">If you are using Reach in your application, you must add `remote-notification` value toohello `UIBackgroundModes` array in your Info.plist file in order tooreceive remote notifications.</span></span>

<span data-ttu-id="2c518-142">Здравствуйте, метод `application:didReceiveRemoteNotification:` необходимо заменить toobe `application:didReceiveRemoteNotification:fetchCompletionHandler:` в делегате приложения.</span><span class="sxs-lookup"><span data-stu-id="2c518-142">hello method `application:didReceiveRemoteNotification:` needs toobe replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="2c518-143">«AEPushDelegate.h» является устаревшим интерфейс и вы должны tooremove все ссылки.</span><span class="sxs-lookup"><span data-stu-id="2c518-143">"AEPushDelegate.h" is deprecated interface and you need tooremove all references.</span></span> <span data-ttu-id="2c518-144">Это включает в себя удаление `[[EngagementAgent shared] setPushDelegate:self]` и делегата методы из делегата приложения hello:</span><span class="sxs-lookup"><span data-stu-id="2c518-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and hello delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a><span data-ttu-id="2c518-145">Из 1.16.0 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="2c518-145">From 1.16.0 too2.0.0</span></span>
<span data-ttu-id="2c518-146">Hello ниже описаны как toomigrate SDK-интеграция с hello обновления Capptain предлагаемых Capptain SAS в приложение на платформе Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2c518-146">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="2c518-147">При переносе из более ранней версии, обратитесь к веб-сайт toomigrate hello Capptain too1.16 сначала затем применить hello после процедуры.</span><span class="sxs-lookup"><span data-stu-id="2c518-147">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.16 first then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c518-148">Capptain и мобильного охвата не являются hello и теми же службами и только представленные ниже процедуры hello выделяет как toomigrate hello клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="2c518-148">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="2c518-149">Миграция hello SDK в приложение hello не выполняют миграцию данных из hello Capptain toohello мобильного охвата серверов</span><span class="sxs-lookup"><span data-stu-id="2c518-149">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="2c518-150">Агент</span><span class="sxs-lookup"><span data-stu-id="2c518-150">Agent</span></span>
<span data-ttu-id="2c518-151">Здравствуйте, метод `registerApp:` будет заменен hello новый метод `init:`.</span><span class="sxs-lookup"><span data-stu-id="2c518-151">hello method `registerApp:` has been replaced by hello new method `init:`.</span></span> <span data-ttu-id="2c518-152">Следует обновить делегат приложения соответствующим образом и использовать строку подключения:</span><span class="sxs-lookup"><span data-stu-id="2c518-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="2c518-153">Отслеживание SmartAd был удален из пакета SDK, достаточно лишь tooremove все экземпляры `AETrackModule` класса</span><span class="sxs-lookup"><span data-stu-id="2c518-153">SmartAd tracking has been removed from SDK you just have tooremove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="2c518-154">Изменение имени класса</span><span class="sxs-lookup"><span data-stu-id="2c518-154">Class Name Changes</span></span>
<span data-ttu-id="2c518-155">В рамках ребрендинг hello существует несколько классов и файлов, имена которых требуется изменить toobe.</span><span class="sxs-lookup"><span data-stu-id="2c518-155">As part of hello rebranding, there are couple of class/file names that need toobe changed.</span></span>

<span data-ttu-id="2c518-156">Во всех классах префикс CP нужно заменить префиксом AE.</span><span class="sxs-lookup"><span data-stu-id="2c518-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="2c518-157">Пример:</span><span class="sxs-lookup"><span data-stu-id="2c518-157">Example:</span></span>

* <span data-ttu-id="2c518-158">`CPModule.h`переименовывается слишком`AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="2c518-158">`CPModule.h` is renamed too`AEModule.h`.</span></span>

<span data-ttu-id="2c518-159">Во всех классах префикс Capptain нужно заменить префиксом Engagement.</span><span class="sxs-lookup"><span data-stu-id="2c518-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="2c518-160">Примеры:</span><span class="sxs-lookup"><span data-stu-id="2c518-160">Examples:</span></span>

* <span data-ttu-id="2c518-161">Здравствуйте, класс `CapptainAgent` переименовывается слишком`EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="2c518-161">hello class `CapptainAgent` is renamed too`EngagementAgent`.</span></span>
* <span data-ttu-id="2c518-162">Здравствуйте, класс `CapptainTableViewController` переименовывается слишком`EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="2c518-162">hello class `CapptainTableViewController` is renamed too`EngagementTableViewController`.</span></span>
* <span data-ttu-id="2c518-163">Здравствуйте, класс `CapptainUtils` переименовывается слишком`EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="2c518-163">hello class `CapptainUtils` is renamed too`EngagementUtils`.</span></span>
* <span data-ttu-id="2c518-164">Здравствуйте, класс `CapptainViewController` переименовывается слишком`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="2c518-164">hello class `CapptainViewController` is renamed too`EngagementViewController`.</span></span>

