---
title: "Добавление push-уведомлений в приложение Xamarin.iOS с помощью службы приложений Azure"
description: "Использование службы приложений Azure для отправки push-уведомлений в приложение Xamarin.iOS"
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
ms.openlocfilehash: bf922e49c4c92d0065817a5dd6c7d10a04737304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinios-app"></a><span data-ttu-id="f648a-103">Добавление push-уведомлений в приложение Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="f648a-103">Add push notifications to your Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="f648a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f648a-104">Overview</span></span>
<span data-ttu-id="f648a-105">В этом руководстве мы добавим push-уведомления в [проект быстрого запуска Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md), чтобы при каждом добавлении новой записи на устройство отправлялось push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="f648a-105">In this tutorial, you add push notifications to the [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="f648a-106">Если вы не используете скачанный проект сервера, вам потребуется добавить пакет расширений для push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f648a-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="f648a-107">Дополнительные сведения о пакетах расширений для сервера см. в статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="f648a-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f648a-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f648a-108">Prerequisites</span></span>
* <span data-ttu-id="f648a-109">Ознакомьтесь с [кратким руководством по Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="f648a-109">Complete the [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="f648a-110">Физическое устройство iOS.</span><span class="sxs-lookup"><span data-stu-id="f648a-110">A physical iOS device.</span></span> <span data-ttu-id="f648a-111">Push-уведомления не поддерживаются в симуляторе iOS.</span><span class="sxs-lookup"><span data-stu-id="f648a-111">Push notifications are not supported by the iOS simulator.</span></span>

## <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="f648a-112">Зарегистрируйте приложение для push-уведомлений на портале разработчика Apple.</span><span class="sxs-lookup"><span data-stu-id="f648a-112">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-to-send-push-notifications"></a><span data-ttu-id="f648a-113">Настройка мобильного приложения для отправки push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="f648a-113">Configure your Mobile App to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="f648a-114">Обновление серверного проекта для отправки push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="f648a-114">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="f648a-115">Настройка проекта Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="f648a-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="f648a-116">Добавление push-уведомлений в приложение</span><span class="sxs-lookup"><span data-stu-id="f648a-116">Add push notifications to your app</span></span>
1. <span data-ttu-id="f648a-117">В **QSTodoService** добавьте приведенное ниже свойство, чтобы **AppDelegate** мог получить мобильный клиент.</span><span class="sxs-lookup"><span data-stu-id="f648a-117">In **QSTodoService**, add the following property so that **AppDelegate** can acquire the mobile client:</span></span>
   
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
2. <span data-ttu-id="f648a-118">Добавьте следующий оператор `using` в верхнюю часть файла **AppDelegate.cs** .</span><span class="sxs-lookup"><span data-stu-id="f648a-118">Add the following `using` statement to the top of the **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="f648a-119">В **AppDelegate** переопределите событие **FinishedLaunching**.</span><span class="sxs-lookup"><span data-stu-id="f648a-119">In **AppDelegate**, override the **FinishedLaunching** event:</span></span>
   
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
4. <span data-ttu-id="f648a-120">В том же файле переопределите событие **RegisteredForRemoteNotifications** .</span><span class="sxs-lookup"><span data-stu-id="f648a-120">In the same file, override the **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="f648a-121">В этом коде регистрируется простое шаблонное уведомление, которое будет рассылаться сервером по всем поддерживаемым платформам.</span><span class="sxs-lookup"><span data-stu-id="f648a-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by the server.</span></span>
   
    <span data-ttu-id="f648a-122">Дополнительные сведения о шаблонах центров уведомлений см. в статье [Шаблоны](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="f648a-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

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


1. <span data-ttu-id="f648a-123">Затем переопределите событие **DidReceivedRemoteNotification** :</span><span class="sxs-lookup"><span data-stu-id="f648a-123">Then, override the **DidReceivedRemoteNotification** event:</span></span>
   
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

<span data-ttu-id="f648a-124">Ваше приложение теперь обновлено для поддержки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f648a-124">Your app is now updated to support push notifications.</span></span>

## <span data-ttu-id="f648a-125"><a name="test"></a>Тестирование push-уведомлений в приложении</span><span class="sxs-lookup"><span data-stu-id="f648a-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="f648a-126">Нажмите кнопку **Выполнить**, чтобы выполнить сборку проекта и запустить приложение на устройстве iOS, а затем нажмите кнопку **ОК**, чтобы разрешить прием push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f648a-126">Press the **Run** button to build the project and start the app in an iOS capable device, then click **OK** to accept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f648a-127">Необходимо явно разрешить прием push-уведомлений от вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f648a-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="f648a-128">Этот запрос отображается только при первом запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="f648a-128">This request only occurs the first time that the app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="f648a-129">В приложении введите задачу, а затем щелкните значок плюса (**+**).</span><span class="sxs-lookup"><span data-stu-id="f648a-129">In the app, type a task, and then click the plus (**+**) icon.</span></span>
3. <span data-ttu-id="f648a-130">Убедитесь, что уведомление получено, а затем нажмите кнопку **ОК** , чтобы закрыть его.</span><span class="sxs-lookup"><span data-stu-id="f648a-130">Verify that a notification is received, then click **OK** to dismiss the notification.</span></span>
4. <span data-ttu-id="f648a-131">Повторите шаг 2 и сразу закройте приложение, затем убедитесь, что уведомление отображается.</span><span class="sxs-lookup"><span data-stu-id="f648a-131">Repeat step 2 and immediately close the app, then verify that a notification is shown.</span></span>

<span data-ttu-id="f648a-132">Вы успешно завершили ознакомление с данным учебником.</span><span class="sxs-lookup"><span data-stu-id="f648a-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



