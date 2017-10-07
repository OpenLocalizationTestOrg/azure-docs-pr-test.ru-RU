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
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a>Отправка push-уведомлений в приложения Xamarin на устройствах iOS с помощью центров уведомлений
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Обзор
> [!IMPORTANT]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомлений приложения iOS tooan.
Вы создадите пустого приложения Xamarin.iOS, получающий push-уведомления с помощью hello [службы уведомлений Apple Push (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html). После завершения вы будете иметь доступ toouse вашей toobroadcast концентратора уведомлений push-уведомления tooall hello устройств под управлением приложения. Hello готовой код находится в hello [приложения NotificationHubs] [ GitHub] образца.

В этом учебнике показано широковещательных сценарий hello принудительной простого сообщения с концентраторами уведомлений.

## <a name="prerequisites"></a>Предварительные требования
Этот учебник требует hello следующее:

* [Xcode 6.0][Install Xcode]
* устройство под управлением iOS 7.0 (или более поздней версии);
* Участие в программе для разработчиков на платформе iOS
* [Xamarin Studio]
  
  > [!NOTE]
  > Из-за требования к конфигурации для iOS push-уведомлений необходимо развернуть и протестировать пример приложения hello на устройстве физических операций ввода-вывода (iPhone и iPad) вместо в симуляторе hello.
  > 
  > 

Изучение этого руководства важно для понимания всех других руководств, посвященных Центрам уведомлений для приложений Xamarin на устройствах iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a>Настройка концентратора уведомлений
В этом подразделе содержатся описано создание нового концентратора уведомлений и настройка проверки подлинности с помощью hello APNS **.p12** созданный сертификат push. Если вы хотите toouse концентратор уведомлений, который уже создан, можно пропустить toostep 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p>Изменить соединение APNS hello tooconfigure в hello портала Azure открыть параметры концентратор уведомлений, щелкните ande на <b>служб Notification Services</b>и нажмите кнопку hello <b>Apple (APN)</b> элемента в списке hello. После этого щелкните <b>передать сертификат</b> и выберите hello <b>.p12</b> сертификат, экспортированный ранее, а также пароль hello hello сертификата.</p>

<p>Убедитесь, что tooselect <b>"песочницы"</b> режиме, так как отправка push-сообщений в среде разработки. Использовать только hello <b>рабочей</b> параметр, toousers toosend принудительной уведомления, кто уже приобрели приложение в магазине hello.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

Концентратор уведомлений теперь настроенные toowork в APNS, и вы tooregister строки подключения hello приложения и отправки push-уведомлений.

## <a name="connect-your-app-toohello-notification-hub"></a>Подключение приложения toohello концентратор уведомлений
#### <a name="create-a-new-project"></a>Создание нового проекта
1. В Xamarin Studio, создайте новый проект iOS и выберите hello **единой API** > **одним приложением представление** шаблона.
   
     ![Выбор типа приложения в Xamarin Studio][31]
2. Добавление компонента обмена сообщениями Azure toohello ссылки. Hello представление решения, щелкните правой кнопкой мыши hello **компоненты** папку проекта и выберите **получить более компонентов**. Поиск hello **обмена сообщениями Azure** компонента и добавьте проект tooyour hello компонента.
3. В **AppDelegate.cs**, добавьте следующее hello с помощью инструкции:
   
        using WindowsAzure.Messaging;
4. Объявите экземпляр **SBNotificationHub**:
   
        private SBNotificationHub Hub { get; set; }
5. Создание **Constants.cs** класса hello следующие переменные:
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. В **AppDelegate.cs**, обновить **FinishedLaunching()** toomatch hello следующее:
   
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
7. Переопределить hello **RegisteredForRemoteNotifications()** метод в **AppDelegate.cs**:
   
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
8. Переопределить hello **ReceivedRemoteNotification()** метод в **AppDelegate.cs**:
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. Создайте ниже hello **ProcessNotification()** метод в **AppDelegate.cs**:
   
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
   > Вы можете toooverride **FailedToRegisterForRemoteNotifications()** toohandle ситуациях, например, отсутствует сетевое подключение. Это особенно важно в тех случаях, где hello пользователь может запустить приложение в автономном режиме (например "в самолете") и требуется принудительной toohandle сценариев tooyour конкретного приложения обмена сообщениями.
   > 
   > 
10. Запустите приложение hello на устройстве.

## <a name="sending-push-notifications"></a>Отправка push-уведомлений
Вы можете протестировать получения push-уведомлений в приложение путем отправки уведомления в hello [портала Azure] через hello **Тестовая отправка** возможность hello **Устранение неполадок** набор инструментов, непосредственно в страницу концентратора hello уведомления, как показано ниже экрана приветствия.

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

Push-уведомления обычно отправляются через серверную службу, например мобильные службы или ASP.NET, с помощью совместимой библиотеки. Также можно использовать hello REST API напрямую принудительной toosend сообщений, если библиотека недоступна в сценарий. 

В этом учебнике мы должен быть простым и просто демонстрации тестирование приложения клиента путем отправки уведомлений с использованием hello .NET SDK для концентраторов уведомлений в консольном приложении, а не серверной службы. Мы рекомендуем hello [toousers уведомления toopush использования концентраторов уведомлений](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) учебника hello на следующем шаге для отправки уведомлений из серверной части ASP.NET. Тем не менее можно использовать следующие подходы hello для отправки уведомлений:

* **Интерфейс REST**: push-уведомление может поддерживать на любой платформе серверной части, с помощью hello [интерфейс REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Пакета SDK .NET концентраторы уведомлений Microsoft Azure**: В hello диспетчера пакетов Nuget для Visual Studio, запустите [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [как концентраторы уведомлений из Node.js toouse](notification-hubs-nodejs-push-notification-tutorial.md).

**Мобильные приложения**: пример того, как toosend уведомления от мобильные приложения службы приложений Azure серверную платформу, которая интегрируется с концентраторами уведомлений в разделе [добавить push tooyour уведомления мобильного приложения](../app-service-mobile/app-service-mobile-ios-get-started-push.md).

* **Java / PHP**: пример как toosend push-уведомления с помощью hello API-интерфейс REST, в разделе «как toouse концентраторы уведомлений из Java и PHP» ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a>Отправка push-уведомлений из консольного приложения .NET(необязательный этап)
В этом разделе мы будем отправлять push-уведомления с помощью простого консольного приложения .NET. Для целей этого примера hello переключается среда разработки Microsoft tooa с уже установленной среды Visual Studio.

1. Создайте в Visual Studio новое консольное приложение Visual C#.
   
       ![Visual Studio - Create a new console application][213]
2. В Visual Studio последовательно выберите элементы **Сервис**, **Диспетчер пакетов NuGet** и **Консоль диспетчера пакетов**.
   
    консоль диспетчера пакетов Hello должна появиться закрепленной toohello нижней части рабочей области Visual Studio.
3. В hello в окне консоли диспетчера пакетов, задайте hello **проекта по умолчанию** tooyour нового консольного приложения проекта, а затем в окне консоли hello, выполните hello следующую команду:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    При этом добавляется ссылка toohello концентраторов уведомлений Azure SDK с помощью hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакет NuGet концентраторов Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Откройте hello `Program.cs` файл и добавьте следующее hello `using` инструкции, гарантируя, что мы используем Azure классы и функции внутри основного класса:
   
        using Microsoft.Azure.NotificationHubs;
5. В вашей `Program` добавьте следующий метод hello (не забудьте tooreplace hello **строка подключения** и **имя концентратора**):
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. Добавьте следующие строки в hello вашей `Main` метод:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Нажмите клавишу приложение hello ключа toorun F5 hello. Через несколько секунд на ваше устройство должно прийти push-уведомление. При использовании Wi-Fi или сети мобильной связи данных, убедитесь, что имеется активное подключение к Интернету на устройстве hello.

Можно найти все возможные полезных данных hello hello Apple [локальный и Push-уведомлений руководство по программированию на].

#### <a name="optional-send-notifications-from-a-mobile-service"></a>Отправка уведомлений с помощью мобильной службы (необязательный этап)
В этом разделе мы будем отправлять push-уведомления с помощью мобильной службы, используя скрипт узла.

toosend уведомления с помощью мобильной службы, следуйте [приступить к работе с мобильными службами], а затем:

1. Войдите в toohello [классический портал Azure]и выберите мобильной службы.
2. Выберите hello **планировщика** вкладки в верхней части hello.
   
       ![Azure Classic Portal - Scheduler][215]
3. Создайте новое запланированное задание, вставьте имя и выберите **По запросу**.
   
       ![Azure Classic Portal - Create new job][216]
4. При создании задания hello, щелкните имя задания hello. Нажмите кнопку hello **сценарий** вкладку на верхней панели hello.
5. Вставьте следующий сценарий внутри функции планировщика hello. Убедитесь, что tooreplace hello местозаполнителей уведомления имя и hello строку подключения к концентратору для *DefaultFullSharedAccessSignature* , полученный ранее. Щелкните **Сохранить**.
   
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
6. Нажмите кнопку **выполнить один раз** на нижней панели hello. На устройстве должно отобразиться оповещение.

## <a name="next-steps"></a>Дальнейшие действия
В этом простом примере вы широковещательной рассылки уведомлений tooall принудительной устройствах iOS. В заказ tootarget определенным пользователям, см. Учебник toohello [toousers уведомления toopush использования концентраторов уведомлений]. Следует ли toosegment пользователям по группы интересов, можно прочитать [toosend использования концентраторов уведомлений, новости]. Дополнительные сведения о toouse концентраторов уведомлений в [руководство концентраторы уведомлений] и в hello [iOS концентраторы уведомлений как toofor].

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
