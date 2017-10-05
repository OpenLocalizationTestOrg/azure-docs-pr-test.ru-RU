---
title: "Отправка push-уведомлений в приложения Xamarin на устройствах iOS с помощью центров уведомлений | Документация Майкрософт"
description: "Из этого учебника вы узнаете, как использовать Центры уведомлений Azure для отправки push-уведомлений в приложение Xamarin.iOS."
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
ms.openlocfilehash: 72a81fa0deb34ace77b8fb9b1a4e6b24ee164b35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="4de05-104">Отправка push-уведомлений в приложения Xamarin на устройствах iOS с помощью центров уведомлений</span><span class="sxs-lookup"><span data-stu-id="4de05-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="4de05-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="4de05-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4de05-106">Для работы с этим учебником необходима активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="4de05-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="4de05-107">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4de05-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4de05-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="4de05-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="4de05-109">В этом учебнике показано, как использовать Центры уведомлений Azure для отправки push-уведомлений в приложение на платформе iOS.</span><span class="sxs-lookup"><span data-stu-id="4de05-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span>
<span data-ttu-id="4de05-110">Вам предстоит создать пустое приложение Xamarin.iOS, получающее push-уведомления с помощью [службы push-уведомлений Apple (APNS)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="4de05-110">You'll create a blank Xamarin.iOS app that receives push notifications by using the [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="4de05-111">По завершении вы сможете рассылать push-уведомления на все устройства, где запущено ваше приложение, с помощью центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4de05-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="4de05-112">Готовый код доступен в примере [приложения NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="4de05-112">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="4de05-113">В этом руководстве описывается простой сценарий рассылки push-сообщений с использованием центров уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4de05-113">This tutorial demonstrates the simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4de05-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4de05-114">Prerequisites</span></span>
<span data-ttu-id="4de05-115">Для работы с данным учебником требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="4de05-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="4de05-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="4de05-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="4de05-117">устройство под управлением iOS 7.0 (или более поздней версии);</span><span class="sxs-lookup"><span data-stu-id="4de05-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="4de05-118">Участие в программе для разработчиков на платформе iOS</span><span class="sxs-lookup"><span data-stu-id="4de05-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="4de05-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="4de05-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="4de05-120">Из-за требований к конфигурации push-уведомлений для устройств iOS развертывание и тестирование примера приложения необходимо выполнять на физическом устройстве iOS (iPhone или iPad), а не в симуляторе.</span><span class="sxs-lookup"><span data-stu-id="4de05-120">Because of configuration requirements for iOS push notifications, you must deploy and test the sample application on a physical iOS device (iPhone or iPad) instead of in the simulator.</span></span>
  > 
  > 

<span data-ttu-id="4de05-121">Изучение этого руководства важно для понимания всех других руководств, посвященных Центрам уведомлений для приложений Xamarin на устройствах iOS.</span><span class="sxs-lookup"><span data-stu-id="4de05-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="4de05-122">Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="4de05-122">Configure your notification hub</span></span>
<span data-ttu-id="4de05-123">В этом разделе приведены пошаговые инструкции по созданию нового центра уведомлений и настройке проверки подлинности с помощью службы APNS, использующей раннее созданный вами сертификат push-уведомлений (файл с расширением **P12** ).</span><span class="sxs-lookup"><span data-stu-id="4de05-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="4de05-124">Если вы хотите использовать уже созданный центр уведомлений, перейдите к шагу 5.</span><span class="sxs-lookup"><span data-stu-id="4de05-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="4de05-125">Так как нам нужно настроить подключение к службе APNS, на портале Azure откройте параметры центра уведомлений, щелкните <b>Службы уведомлений</b> и в списке выберите пункт <b>Apple (APN)</b>.</span><span class="sxs-lookup"><span data-stu-id="4de05-125">As we want to configure the APNS connection, in the Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click the <b>Apple (APNS)</b> item in the list.</span></span> <span data-ttu-id="4de05-126">После этого щелкните <b>Загрузить сертификат</b>, выберите ранее экспортированный сертификат <b>.p12</b> и укажите пароль для него.</span><span class="sxs-lookup"><span data-stu-id="4de05-126">Once done, click on <b>Upload Certificate</b> and select the <b>.p12</b> certificate that you exported earlier, as well as the password for the certificate.</span></span></p>

<p><span data-ttu-id="4de05-127">Не забудьте выбрать режим <b>Песочница</b>, так как push-уведомления вы будете отправлять в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="4de05-127">Make sure to select <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="4de05-128">Вариант <b>Рабочая среда</b> используется, только если push-уведомления отправляются пользователям, которые уже приобрели приложение в магазине.</span><span class="sxs-lookup"><span data-stu-id="4de05-128">Only use the <b>Production</b> setting if you want to send push notifications to users who already purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="4de05-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="4de05-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="4de05-130">Центр уведомлений теперь подключен к службе APNS, и у вас есть строки подключения, с помощью которых вы сможете зарегистрировать свое приложение и отправлять push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="4de05-130">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="4de05-131">Подключение приложения к центру уведомлений</span><span class="sxs-lookup"><span data-stu-id="4de05-131">Connect your app to the notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="4de05-132">Создание нового проекта</span><span class="sxs-lookup"><span data-stu-id="4de05-132">Create a new project</span></span>
1. <span data-ttu-id="4de05-133">В Xamarin Studio создайте новый проект iOS и выберите шаблон **Unified API** > **Single View Application** (Единый API > Приложение с одним представлением).</span><span class="sxs-lookup"><span data-stu-id="4de05-133">In Xamarin Studio, create a new iOS project and select the **Unified API** > **Single View Application** template.</span></span>
   
     ![Выбор типа приложения в Xamarin Studio][31]
2. <span data-ttu-id="4de05-135">Добавьте ссылку на компонент обмена сообщениями Azure.</span><span class="sxs-lookup"><span data-stu-id="4de05-135">Add a reference to the Azure Messaging component.</span></span> <span data-ttu-id="4de05-136">В представлении решения щелкните правой кнопкой мыши папку **Components** (Компоненты) для вашего проекта и выберите пункт **Get More Components** (Получить дополнительные компоненты).</span><span class="sxs-lookup"><span data-stu-id="4de05-136">In the Solution view, right-click the **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="4de05-137">Найдите компонент **Мобильные службы Azure** и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="4de05-137">Search for the **Azure Messaging** component and add the component to your project.</span></span>
3. <span data-ttu-id="4de05-138">В файле **AppDelegate.cs**добавьте следующий оператор using:</span><span class="sxs-lookup"><span data-stu-id="4de05-138">In **AppDelegate.cs**, add the following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="4de05-139">Объявите экземпляр **SBNotificationHub**:</span><span class="sxs-lookup"><span data-stu-id="4de05-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="4de05-140">Создайте класс **Constants.cs** со следующими переменными:</span><span class="sxs-lookup"><span data-stu-id="4de05-140">Create a **Constants.cs** class with the following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="4de05-141">В файле **AppDelegate.cs** обновите метод **FinishedLaunching()**, как указано ниже.</span><span class="sxs-lookup"><span data-stu-id="4de05-141">In **AppDelegate.cs**, update **FinishedLaunching()** to match the following:</span></span>
   
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
7. <span data-ttu-id="4de05-142">Переопределите метод **RegisteredForRemoteNotifications()** в файле **AppDelegate.cs**.</span><span class="sxs-lookup"><span data-stu-id="4de05-142">Override the **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
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
8. <span data-ttu-id="4de05-143">Переопределите метод **ReceivedRemoteNotification()** в файле **AppDelegate.cs**.</span><span class="sxs-lookup"><span data-stu-id="4de05-143">Override the **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="4de05-144">Создайте следующий метод **ProcessNotification()** в файле **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="4de05-144">Create the following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check to see if the dictionary has the aps key.  This is the notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get the aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract the alert text
                // NOTE: If you're using the simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from the aps dictionary will be another NSDictionary.
                // Basically the JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from the ReceivedRemoteNotification while the app was running,
                // we of course need to manually process things like the sound, badge, and alert.
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
   > <span data-ttu-id="4de05-145">Вы можете переопределить метод **FailedToRegisterForRemoteNotifications()** для обработки различных ситуаций, таких как отсутствие сетевого подключения.</span><span class="sxs-lookup"><span data-stu-id="4de05-145">You can choose to override **FailedToRegisterForRemoteNotifications()** to handle situations such as no network connection.</span></span> <span data-ttu-id="4de05-146">Это особенно важно в тех случаях, когда пользователь может запустить приложение в автономном режиме (например, режим "В самолете") и вам нужно обрабатывать отправку push-сообщений так, как нужно для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="4de05-146">This is especially important where the user might start your application in offline mode (e.g. Airplane) and you want to handle push messaging scenarios specific to your app.</span></span>
   > 
   > 
10. <span data-ttu-id="4de05-147">Запустите приложение на устройстве.</span><span class="sxs-lookup"><span data-stu-id="4de05-147">Run the app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="4de05-148">Отправка push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="4de05-148">Sending Push Notifications</span></span>
<span data-ttu-id="4de05-149">Чтобы проверить получение push-уведомлений, отправьте в приложение тестовое уведомление. Это можно сделать на [портале Azure] с помощью функции **Тестовая отправка**. Она находится в наборе инструментов **Устранение неполадок** на странице центра уведомлений, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="4de05-149">You can test receiving push notifications in your app by sending notifications in the [Azure Portal] via the **Test Send** capability in the **Troubleshooting** toolset, right in the notification hub page, as shown in the screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="4de05-150">Push-уведомления обычно отправляются через серверную службу, например мобильные службы или ASP.NET, с помощью совместимой библиотеки.</span><span class="sxs-lookup"><span data-stu-id="4de05-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="4de05-151">Если библиотека недоступна, push-сообщения можно отправлять непосредственно с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="4de05-151">You can also use the REST API directly to send push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="4de05-152">В этом учебнике мы пойдем по простому пути и продемонстрируем тестирование клиентского приложения, отправляя уведомления с помощью пакета SDK для .NET для центров уведомлений не в серверную службу, а в консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="4de05-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="4de05-153">В качестве следующего шага по отправке уведомлений с сервера ASP.NET рекомендуем ознакомиться с руководством [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="4de05-153">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="4de05-154">Можно использовать следующие способы отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4de05-154">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="4de05-155">**Интерфейс REST**. [Интерфейс REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx) поддерживает работу с push-уведомлениями на любой серверной платформе.</span><span class="sxs-lookup"><span data-stu-id="4de05-155">**REST Interface**:  You can support push notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="4de05-156">**Пакет SDK .NET для Центров уведомлений Microsoft Azure**. В диспетчере пакетов NuGet для Visual Studio выполните команду [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="4de05-156">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="4de05-157">**Node.js**. [Использование центров уведомлений из Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="4de05-157">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="4de05-158">**Мобильные приложения**. Пример отправки уведомлений с сервера мобильных приложений службы приложений Azure, интегрированного с центрами уведомлений, см. в статье [Добавление push-уведомлений в приложение iOS](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="4de05-158">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="4de05-159">**Java или PHP**. Примеры отправки push-уведомлений с помощью REST API см. в статьях об использовании центров уведомлений из [Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="4de05-159">**Java / PHP**: For an example of how to send push notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="4de05-160">Отправка push-уведомлений из консольного приложения .NET(необязательный этап)</span><span class="sxs-lookup"><span data-stu-id="4de05-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="4de05-161">В этом разделе мы будем отправлять push-уведомления с помощью простого консольного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="4de05-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="4de05-162">Для целей этого примера мы перейдем в среду разработки Windows, где уже установлена программа Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4de05-162">For the purposes of this example, we will switch to a Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="4de05-163">Создайте в Visual Studio новое консольное приложение Visual C#.</span><span class="sxs-lookup"><span data-stu-id="4de05-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="4de05-164">В Visual Studio последовательно выберите элементы **Сервис**, **Диспетчер пакетов NuGet** и **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="4de05-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="4de05-165">Консоль диспетчера пакетов должна появиться в нижней части рабочей области Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4de05-165">The package manager console should appear docked to the bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="4de05-166">В окне консоли диспетчера пакетов задайте свойство **Проект по умолчанию** для нового проекта консольного приложения, а затем в окне консоли выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4de05-166">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="4de05-167">После этого будет добавлена ссылка на пакет SDK для Центров уведомлений Azure с помощью <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакета NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="4de05-167">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="4de05-168">Откройте файл `Program.cs` и добавьте следующую инструкцию `using`. Она позволит использовать классы и функции Azure в пределах основного класса.</span><span class="sxs-lookup"><span data-stu-id="4de05-168">Open the `Program.cs` file and add the following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="4de05-169">В классе `Program` добавьте следующий метод (не забудьте заменить **строку подключения** и **имя центра**).</span><span class="sxs-lookup"><span data-stu-id="4de05-169">In your `Program` class, add the following method (don't forget to replace the **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="4de05-170">Затем добавьте в метод `Main` следующие строки:</span><span class="sxs-lookup"><span data-stu-id="4de05-170">Add the following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="4de05-171">Нажмите клавишу F5, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="4de05-171">Press the F5 key to run the app.</span></span> <span data-ttu-id="4de05-172">Через несколько секунд на ваше устройство должно прийти push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="4de05-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="4de05-173">Убедитесь, что ваше устройство подключено к Интернету. Это может быть подключение через Wi-Fi или сотовую сеть.</span><span class="sxs-lookup"><span data-stu-id="4de05-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on the device.</span></span>

<span data-ttu-id="4de05-174">Все возможные виды полезных нагрузок можно найти в [руководстве по программированию локальных и push-уведомлений]Apple.</span><span class="sxs-lookup"><span data-stu-id="4de05-174">You can find all the possible payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="4de05-175">Отправка уведомлений с помощью мобильной службы (необязательный этап)</span><span class="sxs-lookup"><span data-stu-id="4de05-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="4de05-176">В этом разделе мы будем отправлять push-уведомления с помощью мобильной службы, используя скрипт узла.</span><span class="sxs-lookup"><span data-stu-id="4de05-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="4de05-177">Чтобы отправить уведомление с помощью мобильной службы, следуйте инструкциям из статьи [Приступая к работе с мобильными службами], а затем выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4de05-177">To send a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="4de05-178">Войдите на [классический портал Azure]и выберите мобильную службу.</span><span class="sxs-lookup"><span data-stu-id="4de05-178">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="4de05-179">Перейдите на расположенную вверху вкладку **Планировщик** .</span><span class="sxs-lookup"><span data-stu-id="4de05-179">Select the **Scheduler** tab on the top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="4de05-180">Создайте новое запланированное задание, вставьте имя и выберите **По запросу**.</span><span class="sxs-lookup"><span data-stu-id="4de05-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="4de05-181">Создав задание, щелкните его имя.</span><span class="sxs-lookup"><span data-stu-id="4de05-181">When the job is created, click the job name.</span></span> <span data-ttu-id="4de05-182">Откройте вкладку **Скрипт** в верхней панели.</span><span class="sxs-lookup"><span data-stu-id="4de05-182">Then click the **Script** tab on the top bar.</span></span>
5. <span data-ttu-id="4de05-183">Вставьте следующий скрипт внутрь функции планировщика.</span><span class="sxs-lookup"><span data-stu-id="4de05-183">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="4de05-184">Обязательно замените заполнители именем концентратора уведомлений и строкой подключения для элемента *DefaultFullSharedAccessSignature* , полученными ранее.</span><span class="sxs-lookup"><span data-stu-id="4de05-184">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="4de05-185">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4de05-185">Click **Save**.</span></span>
   
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
6. <span data-ttu-id="4de05-186">Нажмите кнопку **Запустить один раз** на нижней панели.</span><span class="sxs-lookup"><span data-stu-id="4de05-186">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="4de05-187">На устройстве должно отобразиться оповещение.</span><span class="sxs-lookup"><span data-stu-id="4de05-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4de05-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4de05-188">Next steps</span></span>
<span data-ttu-id="4de05-189">В этом простом примере мы отправили push-уведомления на все устройства iOS.</span><span class="sxs-lookup"><span data-stu-id="4de05-189">In this simple example, you broadcasted push notifications to all your iOS devices.</span></span> <span data-ttu-id="4de05-190">Инструкции по их отправке определенным целевым пользователям, см. в руководстве [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET].</span><span class="sxs-lookup"><span data-stu-id="4de05-190">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="4de05-191">Если необходимо разделить пользователей по группам интересов, см. раздел [Использование концентраторов уведомлений для передачи экстренных новостей].</span><span class="sxs-lookup"><span data-stu-id="4de05-191">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="4de05-192">Дополнительные сведения об использовании центров уведомлений см. в статьях [Общие сведения о концентраторах уведомлений] и [Notification Hubs How-To for iOS] (Инструкции по использованию центров уведомлений для iOS).</span><span class="sxs-lookup"><span data-stu-id="4de05-192">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for iOS].</span></span>

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

<span data-ttu-id="4de05-193">[Приступая к работе с мобильными службами]: /develop/mobile/tutorials/get-started-xamarin-ios</span><span class="sxs-lookup"><span data-stu-id="4de05-193">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios</span></span>
<span data-ttu-id="4de05-194">[классический портал Azure]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="4de05-194">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="4de05-195">[Общие сведения о концентраторах уведомлений]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="4de05-195">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="4de05-196">[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span><span class="sxs-lookup"><span data-stu-id="4de05-196">[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span></span>
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

<span data-ttu-id="4de05-197">[Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="4de05-197">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="4de05-198">[Использование концентраторов уведомлений для передачи экстренных новостей]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="4de05-198">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

<span data-ttu-id="4de05-199">[руководстве по программированию локальных и push-уведомлений]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span><span class="sxs-lookup"><span data-stu-id="4de05-199">[Local and Push Notification Programming Guide]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span></span>
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="4de05-200">[Xamarin Studio]: http://xamarin.com/download</span><span class="sxs-lookup"><span data-stu-id="4de05-200">[Xamarin Studio]: http://xamarin.com/download</span></span>
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
<span data-ttu-id="4de05-201">[портале Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="4de05-201">[Azure Portal]: https://portal.azure.com</span></span>
