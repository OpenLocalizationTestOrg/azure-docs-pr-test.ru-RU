---
title: "Пакет SDK для Служб мобильного взаимодействия Azure (iOS) | Документация Майкрософт"
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
ms.openlocfilehash: 6acd343782a3ee07750e27ec3022ff81cedfadee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="1f8b0-103">Пакет SDK для Служб мобильного взаимодействия Azure (iOS)</span><span class="sxs-lookup"><span data-stu-id="1f8b0-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="1f8b0-104">Начните с этой статьи, чтобы получить подробную информацию об интеграции Служб мобильного взаимодействия Azure в приложения iOS.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-104">Start here to get all the details on how to integrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="1f8b0-105">Если вы хотите потренироваться, обязательно пройдите наш [15-минутный учебник](mobile-engagement-ios-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1f8b0-105">If you'd like to give it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="1f8b0-106">Щелкните, чтобы просмотреть [содержимое пакета SDK](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="1f8b0-106">Click to see the [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="1f8b0-107">Процедуры по интеграции</span><span class="sxs-lookup"><span data-stu-id="1f8b0-107">Integration procedures</span></span>
1. <span data-ttu-id="1f8b0-108">Начните с этого раздела: [Как интегрировать Службы мобильного взаимодействия в приложения iOS](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="1f8b0-108">Start here: [How to integrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="1f8b0-109">Сведения об уведомлениях: [Как интегрировать Reach (Notifications) в приложение iOS](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="1f8b0-109">For Notifications: [How to integrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="1f8b0-110">Реализация плана добавления тегов: [Как использовать API для расширенного добавления тегов Служб мобильного взаимодействия в приложении iOS](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="1f8b0-110">Tag plan implementation: [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="1f8b0-111">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="1f8b0-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="1f8b0-112">4.1.0 (17.07.2017)</span><span class="sxs-lookup"><span data-stu-id="1f8b0-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="1f8b0-113">Исправлена проблема с исчезающими на заднем фоне эмблемами.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="1f8b0-114">Исправлена проблема с предупреждениями в XCode 9 о невызванных в основной очереди API-интерфейсах.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="1f8b0-115">Исправлена утечка памяти при опросах охвата.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="1f8b0-116">Прекращена поддержка iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="1f8b0-117">Начиная с этой версии целевое устройство для развертывания приложения должно быть с версией не ниже iOS 7.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-117">Starting from this version the deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="1f8b0-118">Сведения о предыдущих версиях см. в [полных заметках о выпуске](mobile-engagement-ios-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="1f8b0-118">For earlier version please see the [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="1f8b0-119">Процедуры обновления</span><span class="sxs-lookup"><span data-stu-id="1f8b0-119">Upgrade procedures</span></span>
<span data-ttu-id="1f8b0-120">Если вы уже интегрировали в приложение старую версию службы Engagement, при обновлении пакета SDK необходимо учитывать следующее.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-120">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="1f8b0-121">Если вы пропустили несколько версий пакета SDK, вам понадобится выполнить ряд процедур. См. полную версию статьи [Процедуры обновления](mobile-engagement-ios-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="1f8b0-121">You may have to follow several procedures if you missed several versions of the SDK see the complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="1f8b0-122">Для каждой новой версии пакета SDK необходимо сначала заменить (удалить и повторно импортировать в проект Хcode) папки EngagementSDK и EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-122">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-to-400"></a><span data-ttu-id="1f8b0-123">С версии 3.0.0 до версии 4.0.0</span><span class="sxs-lookup"><span data-stu-id="1f8b0-123">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="1f8b0-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="1f8b0-124">XCode 8</span></span>
<span data-ttu-id="1f8b0-125">Версия XCode 8 является обязательной, начиная с пакета SDK версии 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-125">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="1f8b0-126">Если вам крайне важно оставить версию XCode 7, то можете воспользоваться [пакетом SDK Служб взаимодействия для iOS версии 3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="1f8b0-126">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="1f8b0-127">В предыдущей версии на устройствах iOS 10 выявлена ошибка в модуле обработки рекламных кампаний: не приводятся в действие системные уведомления.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-127">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="1f8b0-128">Для исправления этой ошибки понадобится реализовать в делегате приложения устаревшую версию API `application:didReceiveRemoteNotification:` :</span><span class="sxs-lookup"><span data-stu-id="1f8b0-128">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="1f8b0-129">**Данный способ не является рекомендуемым** , так как это поведение может измениться с любым последующим (даже незначительным) обновлением версии iOS из-за того, что этот интерфейс API для iOS устарел.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="1f8b0-130">Рекомендуется перейти на XCode 8 как можно скорее.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-130">You should switch to XCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="1f8b0-131">Платформа UserNotifications</span><span class="sxs-lookup"><span data-stu-id="1f8b0-131">UserNotifications framework</span></span>
<span data-ttu-id="1f8b0-132">В этапы сборки необходимо добавить платформу `UserNotifications` .</span><span class="sxs-lookup"><span data-stu-id="1f8b0-132">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="1f8b0-133">В обозревателе проектов откройте область проектов и выберите правильную цель.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-133">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="1f8b0-134">Затем откройте вкладку **Build phases** (Этапы сборки) и в меню **Link Binary With Libraries** (Связать двоичные объекты с библиотеками) добавьте платформу `UserNotifications.framework`, задав значение ссылки `Optional`.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-134">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="1f8b0-135">Функция push-уведомлений приложения</span><span class="sxs-lookup"><span data-stu-id="1f8b0-135">Application push capability</span></span>
<span data-ttu-id="1f8b0-136">XCode 8 может выполнить сброс настроек push-уведомлений приложения. Проверьте настройки этой функции на вкладке `capability` выбранной цели.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-136">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

#### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="1f8b0-137">Добавление нового кода регистрации уведомления в iOS 10</span><span class="sxs-lookup"><span data-stu-id="1f8b0-137">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="1f8b0-138">Старый фрагмент кода для регистрации приложения для получения уведомлений по-прежнему функционирует, но он использует устаревшие интерфейсы API при работе в iOS 10.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-138">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="1f8b0-139">Импортируйте платформу `User Notification` :</span><span class="sxs-lookup"><span data-stu-id="1f8b0-139">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="1f8b0-140">В методе `application:didFinishLaunchingWithOptions` делегата приложения замените:</span><span class="sxs-lookup"><span data-stu-id="1f8b0-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="1f8b0-141">на:</span><span class="sxs-lookup"><span data-stu-id="1f8b0-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="1f8b0-142">Разрешение конфликтов делегата UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="1f8b0-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="1f8b0-143">*Если приложения или библиотеки сторонних производителей не реализуют `UNUserNotificationCenterDelegate`, то эту часть можно пропустить.*</span><span class="sxs-lookup"><span data-stu-id="1f8b0-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="1f8b0-144">Делегат `UNUserNotificationCenter` используется пакетом SDK для отслеживания жизненного цикла уведомлений служб Engagement на устройствах, работающих под управлением iOS 10 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-144">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="1f8b0-145">Пакет SDK содержит собственную реализацию протокола `UNUserNotificationCenterDelegate`, однако в приложении может быть только один делегат `UNUserNotificationCenter`.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-145">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="1f8b0-146">Любой другой делегат, добавляемый в объект `UNUserNotificationCenter`, будет конфликтовать со службой Engagement.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-146">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="1f8b0-147">Если пакет SDK обнаружит ваш или другой делегат, он не будет применять собственную реализацию, чтобы дать вам возможность самому разрешить конфликт.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-147">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="1f8b0-148">Для разрешения конфликтов вам потребуется добавить приложение логики Engagement в собственный делегат.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-148">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="1f8b0-149">Это достигается двумя способами.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-149">There are two ways to achieve this.</span></span>

<span data-ttu-id="1f8b0-150">Первый способ. Просто переадресуйте вызовы делегата в пакет SDK:</span><span class="sxs-lookup"><span data-stu-id="1f8b0-150">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="1f8b0-151">Второй способ. Воспользуйтесь наследованием из класса `AEUserNotificationHandler`:</span><span class="sxs-lookup"><span data-stu-id="1f8b0-151">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="1f8b0-152">Можно определить, поступают ли уведомления из Служб взаимодействия, передав словарь `userInfo` в метод класса `isEngagementPushPayload:` агента.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="1f8b0-153">Убедитесь, что в делегате приложения делегат объекта `UNUserNotificationCenter` имеет значение вашего делегата в методе `application:willFinishLaunchingWithOptions:` или `application:didFinishLaunchingWithOptions:`.</span><span class="sxs-lookup"><span data-stu-id="1f8b0-153">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="1f8b0-154">Например, если вы воспользовались первым способом:</span><span class="sxs-lookup"><span data-stu-id="1f8b0-154">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
