---
title: "приложения Xamarin.iOS tooyour уведомлений push aaaAdd службе приложений Azure"
description: "Узнайте, как toosend toouse службе приложений Azure push-уведомлений приложения Xamarin.iOS tooyour"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a><span data-ttu-id="ad9b3-103">Добавление push уведомления tooyour приложения Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="ad9b3-103">Add push notifications tooyour Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="ad9b3-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="ad9b3-104">Overview</span></span>
<span data-ttu-id="ad9b3-105">В этом учебнике добавить push уведомления toohello [Xamarin.iOS краткого](app-service-mobile-xamarin-ios-get-started.md) проекта, чтобы каждый раз при вставке записи push-уведомление отправляется toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-105">In this tutorial, you add push notifications toohello [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="ad9b3-106">Если вы не используете hello загружен проект быстрый запуск сервера, будет необходимо hello пакета расширения уведомлений push.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="ad9b3-107">В разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad9b3-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ad9b3-108">Prerequisites</span></span>
* <span data-ttu-id="ad9b3-109">Полный hello [Xamarin.iOS краткое руководство](app-service-mobile-xamarin-ios-get-started.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-109">Complete hello [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="ad9b3-110">Физическое устройство iOS.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-110">A physical iOS device.</span></span> <span data-ttu-id="ad9b3-111">Push-уведомления не поддерживаются симулятор iOS hello.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-111">Push notifications are not supported by hello iOS simulator.</span></span>

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="ad9b3-112">Регистрация приложения hello push-уведомления на портале для разработчиков Apple</span><span class="sxs-lookup"><span data-stu-id="ad9b3-112">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a><span data-ttu-id="ad9b3-113">Настройка push-уведомлений toosend вашего мобильного приложения</span><span class="sxs-lookup"><span data-stu-id="ad9b3-113">Configure your Mobile App toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="ad9b3-114">Обновить hello server проекта toosend push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="ad9b3-114">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="ad9b3-115">Настройка проекта Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="ad9b3-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="ad9b3-116">Добавить приложение tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="ad9b3-116">Add push notifications tooyour app</span></span>
1. <span data-ttu-id="ad9b3-117">В **QSTodoService**, добавьте следующие свойства hello, чтобы **AppDelegate** можно получить hello мобильного клиента:</span><span class="sxs-lookup"><span data-stu-id="ad9b3-117">In **QSTodoService**, add hello following property so that **AppDelegate** can acquire hello mobile client:</span></span>
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. <span data-ttu-id="ad9b3-118">Добавьте следующее hello `using` инструкции toohello вверху hello **AppDelegate.cs** файла.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-118">Add hello following `using` statement toohello top of hello **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="ad9b3-119">В **AppDelegate**, переопределите hello **FinishedLaunching** событий:</span><span class="sxs-lookup"><span data-stu-id="ad9b3-119">In **AppDelegate**, override hello **FinishedLaunching** event:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. <span data-ttu-id="ad9b3-120">В hello того же файла, переопределите hello **RegisteredForRemoteNotifications** событий.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-120">In hello same file, override hello **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="ad9b3-121">В этом коде вы регистрируете для простой шаблон уведомление, отправляемое на всех поддерживаемых платформах сервером hello.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by hello server.</span></span>
   
    <span data-ttu-id="ad9b3-122">Дополнительные сведения о шаблонах центров уведомлений см. в статье [Шаблоны](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="ad9b3-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. <span data-ttu-id="ad9b3-123">Затем переопределите hello **DidReceivedRemoteNotification** событий:</span><span class="sxs-lookup"><span data-stu-id="ad9b3-123">Then, override hello **DidReceivedRemoteNotification** event:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

<span data-ttu-id="ad9b3-124">Приложение сейчас обновленные toosupport push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-124">Your app is now updated toosupport push notifications.</span></span>

## <span data-ttu-id="ad9b3-125"><a name="test"></a>Тестирование push-уведомлений в приложении</span><span class="sxs-lookup"><span data-stu-id="ad9b3-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="ad9b3-126">Нажмите клавишу hello **запуска** toobuild hello проекта и запустите приложение hello в поддерживает устройства iOS, а затем нажмите кнопку **ОК** tooaccept push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-126">Press hello **Run** button toobuild hello project and start hello app in an iOS capable device, then click **OK** tooaccept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ad9b3-127">Необходимо явно разрешить прием push-уведомлений от вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="ad9b3-128">Этот запрос возникает только hello при первом hello приложение выполняется.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-128">This request only occurs hello first time that hello app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="ad9b3-129">В приложение hello введите задачу и нажмите кнопку hello плюс (**+**) значок.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-129">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
3. <span data-ttu-id="ad9b3-130">Убедитесь, что уведомление о получении, затем щелкните **ОК** toodismiss hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-130">Verify that a notification is received, then click **OK** toodismiss hello notification.</span></span>
4. <span data-ttu-id="ad9b3-131">Повторите шаг 2 и немедленно закрыть hello приложения, а затем убедитесь, что отображается уведомление.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-131">Repeat step 2 and immediately close hello app, then verify that a notification is shown.</span></span>

<span data-ttu-id="ad9b3-132">Вы успешно завершили ознакомление с данным учебником.</span><span class="sxs-lookup"><span data-stu-id="ad9b3-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



