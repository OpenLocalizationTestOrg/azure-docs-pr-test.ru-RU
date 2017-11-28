---
title: "aaaiOS Push-уведомлений с концентраторами уведомлений для приложений Xamarin | Документы Microsoft"
description: "В этом учебнике вы узнаете, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa Xamarin iOS приложения."
services: notification-hubs
keywords: "push-уведомления для IOS, push-сообщения, push-уведомления, push-сообщение"
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="44e0a-104">Отправка push-уведомлений в приложения Xamarin на устройствах iOS с помощью центров уведомлений</span><span class="sxs-lookup"><span data-stu-id="44e0a-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="44e0a-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="44e0a-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="44e0a-106">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="44e0a-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="44e0a-107">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="44e0a-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="44e0a-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="44e0a-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="44e0a-109">Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомлений приложения iOS tooan.</span><span class="sxs-lookup"><span data-stu-id="44e0a-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span>
<span data-ttu-id="44e0a-110">Вы создадите пустого приложения Xamarin.iOS, получающий push-уведомления с помощью hello [службы уведомлений Apple Push (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="44e0a-110">You'll create a blank Xamarin.iOS app that receives push notifications by using hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="44e0a-111">После завершения вы будете иметь доступ toouse вашей toobroadcast концентратора уведомлений push-уведомления tooall hello устройств под управлением приложения.</span><span class="sxs-lookup"><span data-stu-id="44e0a-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="44e0a-112">Hello готовой код находится в hello [приложения NotificationHubs] [ GitHub] образца.</span><span class="sxs-lookup"><span data-stu-id="44e0a-112">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="44e0a-113">В этом учебнике показано широковещательных сценарий hello принудительной простого сообщения с концентраторами уведомлений.</span><span class="sxs-lookup"><span data-stu-id="44e0a-113">This tutorial demonstrates hello simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44e0a-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="44e0a-114">Prerequisites</span></span>
<span data-ttu-id="44e0a-115">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="44e0a-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="44e0a-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="44e0a-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="44e0a-117">устройство под управлением iOS 7.0 (или более поздней версии);</span><span class="sxs-lookup"><span data-stu-id="44e0a-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="44e0a-118">Участие в программе для разработчиков на платформе iOS</span><span class="sxs-lookup"><span data-stu-id="44e0a-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="44e0a-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="44e0a-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="44e0a-120">Из-за требования к конфигурации для iOS push-уведомлений необходимо развернуть и протестировать пример приложения hello на устройстве физических операций ввода-вывода (iPhone и iPad) вместо в симуляторе hello.</span><span class="sxs-lookup"><span data-stu-id="44e0a-120">Because of configuration requirements for iOS push notifications, you must deploy and test hello sample application on a physical iOS device (iPhone or iPad) instead of in hello simulator.</span></span>
  > 
  > 

<span data-ttu-id="44e0a-121">Изучение этого руководства важно для понимания всех других руководств, посвященных Центрам уведомлений для приложений Xamarin на устройствах iOS.</span><span class="sxs-lookup"><span data-stu-id="44e0a-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="44e0a-122">Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="44e0a-122">Configure your notification hub</span></span>
<span data-ttu-id="44e0a-123">В этом подразделе содержатся описано создание нового концентратора уведомлений и настройка проверки подлинности с помощью hello APNS **.p12** созданный сертификат push.</span><span class="sxs-lookup"><span data-stu-id="44e0a-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="44e0a-124">Если вы хотите toouse концентратор уведомлений, который уже создан, можно пропустить toostep 5.</span><span class="sxs-lookup"><span data-stu-id="44e0a-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="44e0a-125">Изменить соединение APNS hello tooconfigure в hello портала Azure открыть параметры концентратор уведомлений, щелкните ande на <b>служб Notification Services</b>и нажмите кнопку hello <b>Apple (APN)</b> элемента в списке hello.</span><span class="sxs-lookup"><span data-stu-id="44e0a-125">As we want tooconfigure hello APNS connection, in hello Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click hello <b>Apple (APNS)</b> item in hello list.</span></span> <span data-ttu-id="44e0a-126">После этого щелкните <b>передать сертификат</b> и выберите hello <b>.p12</b> сертификат, экспортированный ранее, а также пароль hello hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="44e0a-126">Once done, click on <b>Upload Certificate</b> and select hello <b>.p12</b> certificate that you exported earlier, as well as hello password for hello certificate.</span></span></p>

<p><span data-ttu-id="44e0a-127">Убедитесь, что tooselect <b>"песочницы"</b> режиме, так как отправка push-сообщений в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="44e0a-127">Make sure tooselect <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="44e0a-128">Использовать только hello <b>рабочей</b> параметр, toousers toosend принудительной уведомления, кто уже приобрели приложение в магазине hello.</span><span class="sxs-lookup"><span data-stu-id="44e0a-128">Only use hello <b>Production</b> setting if you want toosend push notifications toousers who already purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="44e0a-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="44e0a-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="44e0a-130">Концентратор уведомлений теперь настроенные toowork в APNS, и вы tooregister строки подключения hello приложения и отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="44e0a-130">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="44e0a-131">Подключение приложения toohello концентратор уведомлений</span><span class="sxs-lookup"><span data-stu-id="44e0a-131">Connect your app toohello notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="44e0a-132">Создание нового проекта</span><span class="sxs-lookup"><span data-stu-id="44e0a-132">Create a new project</span></span>
1. <span data-ttu-id="44e0a-133">В Xamarin Studio, создайте новый проект iOS и выберите hello **единой API** > **одним приложением представление** шаблона.</span><span class="sxs-lookup"><span data-stu-id="44e0a-133">In Xamarin Studio, create a new iOS project and select hello **Unified API** > **Single View Application** template.</span></span>
   
     ![Выбор типа приложения в Xamarin Studio][31]
2. <span data-ttu-id="44e0a-135">Добавление компонента обмена сообщениями Azure toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="44e0a-135">Add a reference toohello Azure Messaging component.</span></span> <span data-ttu-id="44e0a-136">Hello представление решения, щелкните правой кнопкой мыши hello **компоненты** папку проекта и выберите **получить более компонентов**.</span><span class="sxs-lookup"><span data-stu-id="44e0a-136">In hello Solution view, right-click hello **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="44e0a-137">Поиск hello **обмена сообщениями Azure** компонента и добавьте проект tooyour hello компонента.</span><span class="sxs-lookup"><span data-stu-id="44e0a-137">Search for hello **Azure Messaging** component and add hello component tooyour project.</span></span>
3. <span data-ttu-id="44e0a-138">В **AppDelegate.cs**, добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="44e0a-138">In **AppDelegate.cs**, add hello following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="44e0a-139">Объявите экземпляр **SBNotificationHub**:</span><span class="sxs-lookup"><span data-stu-id="44e0a-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="44e0a-140">Создание **Constants.cs** класса hello следующие переменные:</span><span class="sxs-lookup"><span data-stu-id="44e0a-140">Create a **Constants.cs** class with hello following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="44e0a-141">В **AppDelegate.cs**, обновить **FinishedLaunching()** toomatch hello следующее:</span><span class="sxs-lookup"><span data-stu-id="44e0a-141">In **AppDelegate.cs**, update **FinishedLaunching()** toomatch hello following:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. <span data-ttu-id="44e0a-142">Переопределить hello **RegisteredForRemoteNotifications()** метод в **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="44e0a-142">Override hello **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. <span data-ttu-id="44e0a-143">Переопределить hello **ReceivedRemoteNotification()** метод в **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="44e0a-143">Override hello **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="44e0a-144">Создайте ниже hello **ProcessNotification()** метод в **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="44e0a-144">Create hello following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="44e0a-145">Вы можете toooverride **FailedToRegisterForRemoteNotifications()** toohandle ситуациях, например, отсутствует сетевое подключение.</span><span class="sxs-lookup"><span data-stu-id="44e0a-145">You can choose toooverride **FailedToRegisterForRemoteNotifications()** toohandle situations such as no network connection.</span></span> <span data-ttu-id="44e0a-146">Это особенно важно в тех случаях, где hello пользователь может запустить приложение в автономном режиме (например "в самолете") и требуется принудительной toohandle сценариев tooyour конкретного приложения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="44e0a-146">This is especially important where hello user might start your application in offline mode (e.g. Airplane) and you want toohandle push messaging scenarios specific tooyour app.</span></span>
   > 
   > 
10. <span data-ttu-id="44e0a-147">Запустите приложение hello на устройстве.</span><span class="sxs-lookup"><span data-stu-id="44e0a-147">Run hello app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="44e0a-148">Отправка push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="44e0a-148">Sending Push Notifications</span></span>
<span data-ttu-id="44e0a-149">Вы можете протестировать получения push-уведомлений в приложение путем отправки уведомления в hello [портала Azure] через hello **Тестовая отправка** возможность hello **Устранение неполадок** набор инструментов, непосредственно в страницу концентратора hello уведомления, как показано ниже экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="44e0a-149">You can test receiving push notifications in your app by sending notifications in hello [Azure Portal] via hello **Test Send** capability in hello **Troubleshooting** toolset, right in hello notification hub page, as shown in hello screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="44e0a-150">Push-уведомления обычно отправляются через серверную службу, например мобильные службы или ASP.NET, с помощью совместимой библиотеки.</span><span class="sxs-lookup"><span data-stu-id="44e0a-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="44e0a-151">Также можно использовать hello REST API напрямую принудительной toosend сообщений, если библиотека недоступна в сценарий.</span><span class="sxs-lookup"><span data-stu-id="44e0a-151">You can also use hello REST API directly toosend push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="44e0a-152">В этом учебнике мы должен быть простым и просто демонстрации тестирование приложения клиента путем отправки уведомлений с использованием hello .NET SDK для концентраторов уведомлений в консольном приложении, а не серверной службы.</span><span class="sxs-lookup"><span data-stu-id="44e0a-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="44e0a-153">Мы рекомендуем hello [toousers уведомления toopush использования концентраторов уведомлений](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) учебника hello на следующем шаге для отправки уведомлений из серверной части ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="44e0a-153">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="44e0a-154">Тем не менее можно использовать следующие подходы hello для отправки уведомлений:</span><span class="sxs-lookup"><span data-stu-id="44e0a-154">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="44e0a-155">**Интерфейс REST**: push-уведомление может поддерживать на любой платформе серверной части, с помощью hello [интерфейс REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="44e0a-155">**REST Interface**:  You can support push notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="44e0a-156">**Пакета SDK .NET концентраторы уведомлений Microsoft Azure**: В hello диспетчера пакетов Nuget для Visual Studio, запустите [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="44e0a-156">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="44e0a-157">**Node.js** : [как концентраторы уведомлений из Node.js toouse](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="44e0a-157">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="44e0a-158">**Мобильные приложения**: пример того, как toosend уведомления от мобильные приложения службы приложений Azure серверную платформу, которая интегрируется с концентраторами уведомлений в разделе [добавить push tooyour уведомления мобильного приложения](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="44e0a-158">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="44e0a-159">**Java / PHP**: пример как toosend push-уведомления с помощью hello API-интерфейс REST, в разделе «как toouse концентраторы уведомлений из Java и PHP» ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="44e0a-159">**Java / PHP**: For an example of how toosend push notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="44e0a-160">Отправка push-уведомлений из консольного приложения .NET(необязательный этап)</span><span class="sxs-lookup"><span data-stu-id="44e0a-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="44e0a-161">В этом разделе мы будем отправлять push-уведомления с помощью простого консольного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="44e0a-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="44e0a-162">Для целей этого примера hello переключается среда разработки Microsoft tooa с уже установленной среды Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44e0a-162">For hello purposes of this example, we will switch tooa Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="44e0a-163">Создайте в Visual Studio новое консольное приложение Visual C#.</span><span class="sxs-lookup"><span data-stu-id="44e0a-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="44e0a-164">В Visual Studio последовательно выберите элементы **Сервис**, **Диспетчер пакетов NuGet** и **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="44e0a-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="44e0a-165">консоль диспетчера пакетов Hello должна появиться закрепленной toohello нижней части рабочей области Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44e0a-165">hello package manager console should appear docked toohello bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="44e0a-166">В hello в окне консоли диспетчера пакетов, задайте hello **проекта по умолчанию** tooyour нового консольного приложения проекта, а затем в окне консоли hello, выполните hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="44e0a-166">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="44e0a-167">При этом добавляется ссылка toohello концентраторов уведомлений Azure SDK с помощью hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакет NuGet концентраторов Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="44e0a-167">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="44e0a-168">Откройте hello `Program.cs` файл и добавьте следующее hello `using` инструкции, гарантируя, что мы используем Azure классы и функции внутри основного класса:</span><span class="sxs-lookup"><span data-stu-id="44e0a-168">Open hello `Program.cs` file and add hello following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="44e0a-169">В вашей `Program` добавьте следующий метод hello (не забудьте tooreplace hello **строка подключения** и **имя концентратора**):</span><span class="sxs-lookup"><span data-stu-id="44e0a-169">In your `Program` class, add hello following method (don't forget tooreplace hello **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="44e0a-170">Добавьте следующие строки в hello вашей `Main` метод:</span><span class="sxs-lookup"><span data-stu-id="44e0a-170">Add hello following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="44e0a-171">Нажмите клавишу приложение hello ключа toorun F5 hello.</span><span class="sxs-lookup"><span data-stu-id="44e0a-171">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="44e0a-172">Через несколько секунд на ваше устройство должно прийти push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="44e0a-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="44e0a-173">При использовании Wi-Fi или сети мобильной связи данных, убедитесь, что имеется активное подключение к Интернету на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="44e0a-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on hello device.</span></span>

<span data-ttu-id="44e0a-174">Можно найти все возможные полезных данных hello hello Apple [локальный и Push-уведомлений руководство по программированию на].</span><span class="sxs-lookup"><span data-stu-id="44e0a-174">You can find all hello possible payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="44e0a-175">Отправка уведомлений с помощью мобильной службы (необязательный этап)</span><span class="sxs-lookup"><span data-stu-id="44e0a-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="44e0a-176">В этом разделе мы будем отправлять push-уведомления с помощью мобильной службы, используя скрипт узла.</span><span class="sxs-lookup"><span data-stu-id="44e0a-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="44e0a-177">toosend уведомления с помощью мобильной службы, следуйте [приступить к работе с мобильными службами], а затем:</span><span class="sxs-lookup"><span data-stu-id="44e0a-177">toosend a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="44e0a-178">Войдите в toohello [классический портал Azure]и выберите мобильной службы.</span><span class="sxs-lookup"><span data-stu-id="44e0a-178">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="44e0a-179">Выберите hello **планировщика** вкладки в верхней части hello.</span><span class="sxs-lookup"><span data-stu-id="44e0a-179">Select hello **Scheduler** tab on hello top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="44e0a-180">Создайте новое запланированное задание, вставьте имя и выберите **По запросу**.</span><span class="sxs-lookup"><span data-stu-id="44e0a-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="44e0a-181">При создании задания hello, щелкните имя задания hello.</span><span class="sxs-lookup"><span data-stu-id="44e0a-181">When hello job is created, click hello job name.</span></span> <span data-ttu-id="44e0a-182">Нажмите кнопку hello **сценарий** вкладку на верхней панели hello.</span><span class="sxs-lookup"><span data-stu-id="44e0a-182">Then click hello **Script** tab on hello top bar.</span></span>
5. <span data-ttu-id="44e0a-183">Вставьте следующий сценарий внутри функции планировщика hello.</span><span class="sxs-lookup"><span data-stu-id="44e0a-183">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="44e0a-184">Убедитесь, что tooreplace hello местозаполнителей уведомления имя и hello строку подключения к концентратору для *DefaultFullSharedAccessSignature* , полученный ранее.</span><span class="sxs-lookup"><span data-stu-id="44e0a-184">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="44e0a-185">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="44e0a-185">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. <span data-ttu-id="44e0a-186">Нажмите кнопку **выполнить один раз** на нижней панели hello.</span><span class="sxs-lookup"><span data-stu-id="44e0a-186">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="44e0a-187">На устройстве должно отобразиться оповещение.</span><span class="sxs-lookup"><span data-stu-id="44e0a-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44e0a-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44e0a-188">Next steps</span></span>
<span data-ttu-id="44e0a-189">В этом простом примере вы широковещательной рассылки уведомлений tooall принудительной устройствах iOS.</span><span class="sxs-lookup"><span data-stu-id="44e0a-189">In this simple example, you broadcasted push notifications tooall your iOS devices.</span></span> <span data-ttu-id="44e0a-190">В заказ tootarget определенным пользователям, см. Учебник toohello [toousers уведомления toopush использования концентраторов уведомлений].</span><span class="sxs-lookup"><span data-stu-id="44e0a-190">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="44e0a-191">Следует ли toosegment пользователям по группы интересов, можно прочитать [toosend использования концентраторов уведомлений, новости].</span><span class="sxs-lookup"><span data-stu-id="44e0a-191">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="44e0a-192">Дополнительные сведения о toouse концентраторов уведомлений в [руководство концентраторы уведомлений] и в hello [iOS концентраторы уведомлений как toofor].</span><span class="sxs-lookup"><span data-stu-id="44e0a-192">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor iOS].</span></span>

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[приступить к работе с мобильными службами]: /develop/mobile/tutorials/get-started-xamarin-ios
[классический портал Azure]: https://manage.windowsazure.com/
[руководство концентраторы уведомлений]: http://msdn.microsoft.com/library/jj927170.aspx
[iOS концентраторы уведомлений как toofor]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[toousers уведомления toopush использования концентраторов уведомлений]: /manage/services/notification-hubs/notify-users-aspnet
[toosend использования концентраторов уведомлений, новости]: /manage/services/notification-hubs/breaking-news-dotnet

[локальный и Push-уведомлений руководство по программированию на]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[портала Azure]: https://portal.azure.com
