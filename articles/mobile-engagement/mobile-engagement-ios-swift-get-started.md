---
title: "aaaGet работы с Azure Mobile Engagement для операций ввода-вывода в Swift | Документы Microsoft"
description: "Узнайте, как toouse Azure Mobile Engagement Analytics и Push-уведомления для приложений iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="23d50-103">Начало работы со Службами мобильного взаимодействия Azure для приложений iOS в Swift</span><span class="sxs-lookup"><span data-stu-id="23d50-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="23d50-104">В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использования приложений и отправлять push-уведомления toosegmented пользователей tooan операций ввода-вывода приложения.</span><span class="sxs-lookup"><span data-stu-id="23d50-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="23d50-105">В этом учебнике вы создадите пустое приложение iOS, которое собирает основные данные и получает push-уведомления с помощью Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="23d50-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="23d50-106">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="23d50-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="23d50-107">XCode 8, который можно установить из MAC App Store;</span><span class="sxs-lookup"><span data-stu-id="23d50-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="23d50-108">Hello [iOS Mobile Engagement SDK]</span><span class="sxs-lookup"><span data-stu-id="23d50-108">hello [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="23d50-109">Сертификат push-уведомлений (P12), который можно получить в центре разработки для Apple</span><span class="sxs-lookup"><span data-stu-id="23d50-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="23d50-110">В этом учебнике используется Swift версии 3.0.</span><span class="sxs-lookup"><span data-stu-id="23d50-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="23d50-111">Завершение изучения этого руководства является необходимым условием для работы со всеми другими руководствами, посвященными Службам мобильного взаимодействия для приложений iOS.</span><span class="sxs-lookup"><span data-stu-id="23d50-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="23d50-112">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="23d50-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="23d50-113">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="23d50-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="23d50-114">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span><span class="sxs-lookup"><span data-stu-id="23d50-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="23d50-115"><a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для вашего приложения iOS</span><span class="sxs-lookup"><span data-stu-id="23d50-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="23d50-116"><a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="23d50-116"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="23d50-117">В этом руководстве содержатся «базовой интеграции», который hello минимальный набор данных требуется toocollect и отправить push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="23d50-117">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="23d50-118">Hello полной интеграции документацию можно найти в hello [iOS Mobile Engagement SDK-интеграция](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="23d50-118">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="23d50-119">Мы создадим простое приложение с помощью XCode toodemonstrate hello интеграции:</span><span class="sxs-lookup"><span data-stu-id="23d50-119">We will create a basic app with XCode toodemonstrate hello integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="23d50-120">Создание проекта iOS</span><span class="sxs-lookup"><span data-stu-id="23d50-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="23d50-121">Подключение Engagement tooMobile внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="23d50-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="23d50-122">Загрузите hello [iOS Mobile Engagement SDK]</span><span class="sxs-lookup"><span data-stu-id="23d50-122">Download hello [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="23d50-123">Извлеките hello. tar.gz файл tooa папку на компьютере</span><span class="sxs-lookup"><span data-stu-id="23d50-123">Extract hello .tar.gz file tooa folder in your computer</span></span>
3. <span data-ttu-id="23d50-124">Щелкните правой кнопкой мыши проект hello и выберите пункт «Добавить файлы слишком...»</span><span class="sxs-lookup"><span data-stu-id="23d50-124">Right click hello project and select "Add files too..."</span></span>
   
    ![][1]
4. <span data-ttu-id="23d50-125">Перейдите в папку toohello, будут извлечены hello SDK и выберите hello `EngagementSDK` папки, а затем нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="23d50-125">Navigate toohello folder where you extracted hello SDK and select hello `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="23d50-126">Откройте hello `Build Phases` вкладке и в hello `Link Binary With Libraries` меню добавьте hello платформы, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="23d50-126">Open hello `Build Phases` tab and in hello `Link Binary With Libraries` menu add hello frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="23d50-127">Создайте мост заголовок toobe может toouse hello API пакета SDK для элемента цель C, выбрав Файл > Создать > Файл > iOS > источника > файла заголовка.</span><span class="sxs-lookup"><span data-stu-id="23d50-127">Create a Bridging header toobe able toouse hello SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="23d50-128">Измените hello мост заголовок файла tooexpose Mobile Engagement Objective-C tooyour Swift кода, добавьте следующие импорты hello:</span><span class="sxs-lookup"><span data-stu-id="23d50-128">Edit hello bridging header file tooexpose Mobile Engagement Objective-C code tooyour Swift code, add hello following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="23d50-129">В разделе Параметры построения убедитесь, что hello параметр в списке Swift компилятора - формирования кода сборки заголовка мост Objective-C имеет заголовок toothis пути.</span><span class="sxs-lookup"><span data-stu-id="23d50-129">Under Build Settings, make sure hello Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path toothis header.</span></span> <span data-ttu-id="23d50-130">Ниже приведен пример пути: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (в зависимости от пути hello)**</span><span class="sxs-lookup"><span data-stu-id="23d50-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on hello path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="23d50-131">Вернитесь к предыдущему окну toohello портал Azure в вашем приложении *сведений о соединении* страницы и скопируйте hello строки подключения</span><span class="sxs-lookup"><span data-stu-id="23d50-131">Go back toohello Azure portal in your app's *Connection Info* page and copy hello Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="23d50-132">Теперь вставьте строку подключения hello в hello `didFinishLaunchingWithOptions` делегата</span><span class="sxs-lookup"><span data-stu-id="23d50-132">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="23d50-133"><a id="monitor"></a>Включение мониторинга в реальном времени</span><span class="sxs-lookup"><span data-stu-id="23d50-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="23d50-134">В toostart порядок отправки данных и убедитесь, что пользователи hello active необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана (действие).</span><span class="sxs-lookup"><span data-stu-id="23d50-134">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="23d50-135">Откройте hello **ViewController.swift** и замените hello базовый класс **ViewController** toobe **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="23d50-135">Open hello **ViewController.swift** file and replace hello base class of **ViewController** toobe **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="23d50-136"><a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="23d50-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="23d50-137"><a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="23d50-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="23d50-138">Mobile Engagement позволяет toointeract и получить доступ с пользователями с Push-уведомления и обмен сообщениями в приложении в контексте hello кампаний.</span><span class="sxs-lookup"><span data-stu-id="23d50-138">Mobile Engagement allows you toointeract and REACH with your users with Push Notifications and In-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="23d50-139">Этот модуль вызывается REACH на портале мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="23d50-139">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="23d50-140">Hello ниже настроит вашего приложения tooreceive их.</span><span class="sxs-lookup"><span data-stu-id="23d50-140">hello following sections will setup your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="23d50-141">Включить вашего приложения tooreceive автоматической Push-уведомления</span><span class="sxs-lookup"><span data-stu-id="23d50-141">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="23d50-142">Добавьте проект tooyour библиотеки Reach hello</span><span class="sxs-lookup"><span data-stu-id="23d50-142">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="23d50-143">Щелкните правой кнопкой мыши проект</span><span class="sxs-lookup"><span data-stu-id="23d50-143">Right click your project</span></span>
2. <span data-ttu-id="23d50-144">Выберите `Add file too...`</span><span class="sxs-lookup"><span data-stu-id="23d50-144">Select `Add file too...`</span></span>
3. <span data-ttu-id="23d50-145">Перейдите в папку toohello, будут извлечены hello SDK</span><span class="sxs-lookup"><span data-stu-id="23d50-145">Navigate toohello folder where you extracted hello SDK</span></span>
4. <span data-ttu-id="23d50-146">Выберите hello `EngagementReach` папки</span><span class="sxs-lookup"><span data-stu-id="23d50-146">Select hello `EngagementReach` folder</span></span>
5. <span data-ttu-id="23d50-147">Нажмите "Добавить"</span><span class="sxs-lookup"><span data-stu-id="23d50-147">Click Add</span></span>
6. <span data-ttu-id="23d50-148">Измените hello мост заголовков Objective-C Mobile Engagement Reach tooexpose заголовок файла и добавьте следующие импорты hello:</span><span class="sxs-lookup"><span data-stu-id="23d50-148">Edit hello bridging header file tooexpose Mobile Engagement Objective-C Reach headers and add hello following imports :</span></span>
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a><span data-ttu-id="23d50-149">Изменение делегата приложения</span><span class="sxs-lookup"><span data-stu-id="23d50-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="23d50-150">Внутри hello `didFinishLaunchingWithOptions` — создать модуль reach и передать его tooyour существующую строку инициализации участия:</span><span class="sxs-lookup"><span data-stu-id="23d50-150">Inside  hello `didFinishLaunchingWithOptions` -  create a reach module and pass it tooyour existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="23d50-151">Включить вашего приложения tooreceive Push-уведомления APNS</span><span class="sxs-lookup"><span data-stu-id="23d50-151">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="23d50-152">Добавьте следующие строки toohello hello `didFinishLaunchingWithOptions` метод:</span><span class="sxs-lookup"><span data-stu-id="23d50-152">Add hello following line toohello `didFinishLaunchingWithOptions` method:</span></span>
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. <span data-ttu-id="23d50-153">Добавить hello `didRegisterForRemoteNotificationsWithDeviceToken` метод следующим образом:</span><span class="sxs-lookup"><span data-stu-id="23d50-153">Add hello `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="23d50-154">Добавить hello `didReceiveRemoteNotification:fetchCompletionHandler:` метод следующим образом:</span><span class="sxs-lookup"><span data-stu-id="23d50-154">Add hello `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[iOS Mobile Engagement SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
