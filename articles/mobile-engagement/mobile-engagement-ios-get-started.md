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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="9b870-103">Начало работы со Службами мобильного взаимодействия Azure для приложений iOS в Objective C</span><span class="sxs-lookup"><span data-stu-id="9b870-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="9b870-104">В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использования приложений и отправлять push-уведомления toosegmented пользователей tooan операций ввода-вывода приложения.</span><span class="sxs-lookup"><span data-stu-id="9b870-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="9b870-105">В этом учебнике вы создадите пустое приложение iOS, которое собирает основные данные и получает push-уведомления с помощью Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="9b870-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="9b870-106">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="9b870-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="9b870-107">XCode 8, который можно установить из MAC App Store;</span><span class="sxs-lookup"><span data-stu-id="9b870-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="9b870-108">Hello [iOS Mobile Engagement SDK]</span><span class="sxs-lookup"><span data-stu-id="9b870-108">hello [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="9b870-109">Завершение изучения этого руководства является необходимым условием для работы со всеми другими руководствами, посвященными Службам мобильного взаимодействия для приложений iOS.</span><span class="sxs-lookup"><span data-stu-id="9b870-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="9b870-110">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="9b870-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="9b870-111">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="9b870-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9b870-112">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="9b870-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="9b870-113"><a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для вашего приложения iOS</span><span class="sxs-lookup"><span data-stu-id="9b870-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="9b870-114"><a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="9b870-114"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="9b870-115">В этом руководстве содержатся «базовой интеграции», который hello минимальный набор данных требуется toocollect и отправить push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="9b870-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="9b870-116">Hello полной интеграции документацию можно найти в hello [iOS Mobile Engagement SDK-интеграция](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9b870-116">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="9b870-117">Мы создадим простое приложение с интеграцией hello toodemonstrate XCode.</span><span class="sxs-lookup"><span data-stu-id="9b870-117">We will create a basic app with XCode toodemonstrate hello integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="9b870-118">Создание проекта iOS</span><span class="sxs-lookup"><span data-stu-id="9b870-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="9b870-119">Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="9b870-119">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="9b870-120">Загрузите hello [iOS Mobile Engagement SDK].</span><span class="sxs-lookup"><span data-stu-id="9b870-120">Download hello [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="9b870-121">Извлеките hello. tar.gz файл tooa папку на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="9b870-121">Extract hello .tar.gz file tooa folder in your computer.</span></span>
3. <span data-ttu-id="9b870-122">Щелкните правой кнопкой мыши проект hello, а затем выберите **добавьте файлы в**.</span><span class="sxs-lookup"><span data-stu-id="9b870-122">Right-click hello project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="9b870-123">Перейдите в папку toohello, будут извлечены hello SDK, выберите hello `EngagementSDK` папку, нажмите кнопку **параметры** на нижний левый угол hello и убедитесь в том, что флажок hello **копирование элементов при необходимости** и hello флажок на целевом объекте проверяются, а затем нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9b870-123">Navigate toohello folder where you extracted hello SDK, select hello `EngagementSDK` folder, click **Options** on hello bottom left corner and make sure that hello checkbox **Copy items if needed** and hello checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="9b870-124">Привет открыть **этапов построения** вкладке и в hello **ссылку двоичного файла с библиотеками** меню, добавить hello платформы, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="9b870-124">Open hello **Build Phases** tab, and in hello **Link Binary With Libraries** menu, add hello frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="9b870-125">Вернитесь к предыдущему окну toohello портал Azure в вашем приложении **сведений о соединении** страницы и скопируйте строку подключения hello.</span><span class="sxs-lookup"><span data-stu-id="9b870-125">Go back toohello Azure portal in your app's **Connection Info** page and copy hello connection string.</span></span>

    ![][4]
7. <span data-ttu-id="9b870-126">Добавить hello, следующей строкой кода в ваш **AppDelegate.m** файла.</span><span class="sxs-lookup"><span data-stu-id="9b870-126">Add hello following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="9b870-127">Теперь вставьте строку подключения hello в hello `didFinishLaunchingWithOptions` делегата.</span><span class="sxs-lookup"><span data-stu-id="9b870-127">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="9b870-128">`setTestLogEnabled`— необязательный оператор, который включает журналы SDK на tooidentify проблемы.</span><span class="sxs-lookup"><span data-stu-id="9b870-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you tooidentify issues.</span></span>

## <span data-ttu-id="9b870-129"><a id="monitor"></a>Включение мониторинга в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="9b870-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="9b870-130">В toostart порядок отправки данных и убедитесь, что пользователи hello active необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана (действие).</span><span class="sxs-lookup"><span data-stu-id="9b870-130">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="9b870-131">Откройте hello **ViewController.h** и импортируйте **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="9b870-131">Open hello **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="9b870-132">Теперь замените hello суперкласса hello **ViewController** интерфейс с `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="9b870-132">Now replace hello super class of hello **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="9b870-133"><a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="9b870-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="9b870-134"><a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="9b870-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="9b870-135">Mobile Engagement позволяет toointeract со своими пользователями и получить доступ с push-уведомления и сообщения в контексте hello кампаний в приложения.</span><span class="sxs-lookup"><span data-stu-id="9b870-135">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="9b870-136">Этот модуль вызывается REACH на портале мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="9b870-136">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="9b870-137">Hello следующих разделах Настройка вашего приложения tooreceive их.</span><span class="sxs-lookup"><span data-stu-id="9b870-137">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="9b870-138">Включить вашего приложения tooreceive автоматической Push-уведомления</span><span class="sxs-lookup"><span data-stu-id="9b870-138">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="9b870-139">Добавьте проект tooyour библиотеки Reach hello</span><span class="sxs-lookup"><span data-stu-id="9b870-139">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="9b870-140">Щелкните проект правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="9b870-140">Right-click your project.</span></span>
2. <span data-ttu-id="9b870-141">Выберите пункт **Добавить файл в**.</span><span class="sxs-lookup"><span data-stu-id="9b870-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="9b870-142">Перейдите в папку toohello, будут извлечены hello SDK.</span><span class="sxs-lookup"><span data-stu-id="9b870-142">Navigate toohello folder where you extracted hello SDK.</span></span>
4. <span data-ttu-id="9b870-143">Выберите hello `EngagementReach` папки.</span><span class="sxs-lookup"><span data-stu-id="9b870-143">Select hello `EngagementReach` folder.</span></span>
5. <span data-ttu-id="9b870-144">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9b870-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="9b870-145">Изменение делегата приложения</span><span class="sxs-lookup"><span data-stu-id="9b870-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="9b870-146">В **AppDeletegate.m** файл, импортируйте модуль Engagement Reach hello.</span><span class="sxs-lookup"><span data-stu-id="9b870-146">Back in **AppDeletegate.m** file, import hello Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="9b870-147">Внутри hello `application:didFinishLaunchingWithOptions` метод, создайте модулем и передайте его tooyour существующую строку инициализации участия:</span><span class="sxs-lookup"><span data-stu-id="9b870-147">Inside hello `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it tooyour existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="9b870-148">Включить вашего приложения tooreceive Push-уведомления APNS</span><span class="sxs-lookup"><span data-stu-id="9b870-148">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="9b870-149">Добавьте следующие строки toohello hello `application:didFinishLaunchingWithOptions` метод:</span><span class="sxs-lookup"><span data-stu-id="9b870-149">Add hello following line toohello `application:didFinishLaunchingWithOptions` method:</span></span>

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
2. <span data-ttu-id="9b870-150">Добавить hello `application:didRegisterForRemoteNotificationsWithDeviceToken` метод следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9b870-150">Add hello `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="9b870-151">Добавить hello `didFailToRegisterForRemoteNotificationsWithError` метод следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9b870-151">Add hello `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. <span data-ttu-id="9b870-152">Добавить hello `didReceiveRemoteNotification:fetchCompletionHandler` метод следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9b870-152">Add hello `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

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
