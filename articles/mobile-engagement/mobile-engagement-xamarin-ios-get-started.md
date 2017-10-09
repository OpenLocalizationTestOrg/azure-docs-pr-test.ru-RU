---
title: "aaaGet работы с Azure Mobile Engagement для Xamarin.iOS"
description: "Узнайте, как toouse Azure Mobile Engagement с аналитики и Push-уведомления для Xamarin.iOS приложений."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="e81cc-103">Начало работы со Службами мобильного взаимодействия Azure для приложений Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="e81cc-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e81cc-104">В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использования приложений и отправить push-уведомления toosegmented пользователей в приложении Xamarin.iOS.</span><span class="sxs-lookup"><span data-stu-id="e81cc-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="e81cc-105">В этом руководстве вы создадите пустое приложение Xamarin.iOS, которое собирает основные данные и получает push-уведомления с помощью службы push-уведомлений Apple (APNs).</span><span class="sxs-lookup"><span data-stu-id="e81cc-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="e81cc-106">Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов.</span><span class="sxs-lookup"><span data-stu-id="e81cc-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="e81cc-107">Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="e81cc-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="e81cc-108">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="e81cc-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="e81cc-109">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="e81cc-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="e81cc-110">Вы также можете использовать Visual Studio с расширением Xamarin, но в этом руководстве используется Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="e81cc-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="e81cc-111">Инструкции см. в руководстве по [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="e81cc-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="e81cc-112">пакет Xamarin SDK для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="e81cc-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="e81cc-113">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e81cc-113">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e81cc-114">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e81cc-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e81cc-115">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="e81cc-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="e81cc-116"><a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для вашего приложения iOS</span><span class="sxs-lookup"><span data-stu-id="e81cc-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e81cc-117"><a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="e81cc-117"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="e81cc-118">В этом руководстве содержатся «базовой интеграции» hello минимальный набор данных требуется toocollect и отправить push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="e81cc-118">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span>

<span data-ttu-id="e81cc-119">Мы создадим простое приложение с помощью Xamarin toodemonstrate hello интеграции:</span><span class="sxs-lookup"><span data-stu-id="e81cc-119">We will create a basic app with Xamarin toodemonstrate hello integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="e81cc-120">Создание нового проекта Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="e81cc-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="e81cc-121">Запустите Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="e81cc-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="e81cc-122">Go слишком**файл** -> **New** -> **решения**</span><span class="sxs-lookup"><span data-stu-id="e81cc-122">Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="e81cc-123">Выберите **одного представления приложения**, убедитесь, что выбран hello языка **C#** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e81cc-123">Select **Single View App**, make sure hello selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="e81cc-124">Заполните hello **имя приложения** и hello **идентификатор организации** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e81cc-124">Fill in hello **App Name** and hello **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="e81cc-125">Убедитесь, что hello, в конце концов используется toodeploy приложение iOS использует идентификатор приложения, которое соответствует точно совпадает с hello идентификатор пакета, здесь у профиль публикации.</span><span class="sxs-lookup"><span data-stu-id="e81cc-125">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using an App ID which matches exactly with hello Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="e81cc-126">Обновление hello **имя проекта**, **имя решения** и **расположение** , если требуется и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="e81cc-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="e81cc-127">Xamarin Studio создаст hello нашего примера приложения, в котором будет интегрировать мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="e81cc-127">Xamarin Studio will create hello demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="e81cc-128">Подключение Engagement tooMobile внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="e81cc-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="e81cc-129">Щелкните правой кнопкой мыши hello **пакетов** папки в windows hello решений и выберите **Добавление пакетов...**</span><span class="sxs-lookup"><span data-stu-id="e81cc-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="e81cc-130">Поиск hello **Microsoft Azure Mobile Engagement Xamarin SDK** и добавьте его tooyour решения.</span><span class="sxs-lookup"><span data-stu-id="e81cc-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="e81cc-131">Откройте **AppDelegate.cs** и добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="e81cc-131">Open **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="e81cc-132">В hello **FinishedLaunching** метод, добавить следующие tooinitialize hello соединения с внутреннего сервера мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="e81cc-132">In hello **FinishedLaunching** method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="e81cc-133">Убедитесь, что tooadd вашей **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="e81cc-133">Make sure tooadd your **ConnectionString**.</span></span> <span data-ttu-id="e81cc-134">Этот код также использует фиктивное **NotificationIcon** добавляемым hello Mobile Engagement SDK, который можно привести tooreplace.</span><span class="sxs-lookup"><span data-stu-id="e81cc-134">This code also uses a dummy **NotificationIcon** which is added by hello Mobile Engagement SDK which you may want tooreplace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="e81cc-135"><a id="monitor"></a>Включение мониторинга в реальном времени</span><span class="sxs-lookup"><span data-stu-id="e81cc-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="e81cc-136">В toostart порядок отправки данных и убедитесь, что пользователи hello активны необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана.</span><span class="sxs-lookup"><span data-stu-id="e81cc-136">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="e81cc-137">Откройте **ViewController.cs** и добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="e81cc-137">Open **ViewController.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="e81cc-138">Замените hello класс, от которого `ViewController` наследует от `UIViewController` слишком`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="e81cc-138">Replace hello class from which `ViewController` inherits from `UIViewController` too`EngagementViewController`.</span></span> 

## <span data-ttu-id="e81cc-139"><a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="e81cc-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="e81cc-140"><a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="e81cc-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="e81cc-141">Mobile Engagement позволяет toointeract со своими пользователями и получить доступ с push-уведомления и сообщения в контексте hello кампаний в приложения.</span><span class="sxs-lookup"><span data-stu-id="e81cc-141">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="e81cc-142">Этот модуль вызывается REACH на портале мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="e81cc-142">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="e81cc-143">Hello следующих разделах Настройка вашего приложения tooreceive их.</span><span class="sxs-lookup"><span data-stu-id="e81cc-143">hello following sections set up your app tooreceive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="e81cc-144">Изменение делегата приложения</span><span class="sxs-lookup"><span data-stu-id="e81cc-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="e81cc-145">Откройте hello **AppDelegate.cs** и добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="e81cc-145">Open hello **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="e81cc-146">Теперь внутри hello `FinishedLaunching` метод, добавить следующие tooregister для push-сообщений, после hello`EngagementAgent.init(...)`</span><span class="sxs-lookup"><span data-stu-id="e81cc-146">Now inside hello `FinishedLaunching` method, add hello following tooregister for push messages after `EngagementAgent.init(...)`</span></span>
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. <span data-ttu-id="e81cc-147">И наконец — обновить или добавить hello следующие методы:</span><span class="sxs-lookup"><span data-stu-id="e81cc-147">Finally - update or add hello following methods:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="e81cc-148">В вашей **Info.plist** файла в решении hello, убедитесь, что hello **идентификатор пакета** совпадает с hello **идентификатор приложения** имеется в профиле подготовки в hello разработчиков Apple По центру.</span><span class="sxs-lookup"><span data-stu-id="e81cc-148">In your **Info.plist** file in hello solution, confirm that hello **Bundle Identifier** matches with hello **App ID** you have in your provisioning profile in hello Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="e81cc-149">В hello же **Info.plist** файл, убедитесь в том, что возвращаются hello **Включение фоновых режимов** и **удаленного уведомления**.</span><span class="sxs-lookup"><span data-stu-id="e81cc-149">In hello same **Info.plist** file, make sure that you have checked hello **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="e81cc-150">Запустите приложение hello на устройстве hello, сопоставленную с данным профилем публикации.</span><span class="sxs-lookup"><span data-stu-id="e81cc-150">Run hello app on hello device you have associated with this publishing profile.</span></span> 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
