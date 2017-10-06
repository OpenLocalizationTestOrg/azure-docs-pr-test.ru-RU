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
# <a name="add-push-notifications-tooyour-xamarinios-app"></a>Добавление push уведомления tooyour приложения Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Обзор
В этом учебнике добавить push уведомления toohello [Xamarin.iOS краткого](app-service-mobile-xamarin-ios-get-started.md) проекта, чтобы каждый раз при вставке записи push-уведомление отправляется toohello устройства.

Если вы не используете hello загружен проект быстрый запуск сервера, будет необходимо hello пакета расширения уведомлений push. В разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) для получения дополнительной информации.

## <a name="prerequisites"></a>Предварительные требования
* Полный hello [Xamarin.iOS краткое руководство](app-service-mobile-xamarin-ios-get-started.md) учебника.
* Физическое устройство iOS. Push-уведомления не поддерживаются симулятор iOS hello.

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Регистрация приложения hello push-уведомления на портале для разработчиков Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a>Настройка push-уведомлений toosend вашего мобильного приложения
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Обновить hello server проекта toosend push-уведомлений
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a>Настройка проекта Xamarin.iOS
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a>Добавить приложение tooyour уведомлений push
1. В **QSTodoService**, добавьте следующие свойства hello, чтобы **AppDelegate** можно получить hello мобильного клиента:
   
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
2. Добавьте следующее hello `using` инструкции toohello вверху hello **AppDelegate.cs** файла.
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. В **AppDelegate**, переопределите hello **FinishedLaunching** событий:
   
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
4. В hello того же файла, переопределите hello **RegisteredForRemoteNotifications** событий. В этом коде вы регистрируете для простой шаблон уведомление, отправляемое на всех поддерживаемых платформах сервером hello.
   
    Дополнительные сведения о шаблонах центров уведомлений см. в статье [Шаблоны](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).

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


1. Затем переопределите hello **DidReceivedRemoteNotification** событий:
   
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

Приложение сейчас обновленные toosupport push-уведомлений.

## <a name="test"></a>Тестирование push-уведомлений в приложении
1. Нажмите клавишу hello **запуска** toobuild hello проекта и запустите приложение hello в поддерживает устройства iOS, а затем нажмите кнопку **ОК** tooaccept push-уведомлений.
   
   > [!NOTE]
   > Необходимо явно разрешить прием push-уведомлений от вашего приложения. Этот запрос возникает только hello при первом hello приложение выполняется.
   > 
   > 
2. В приложение hello введите задачу и нажмите кнопку hello плюс (**+**) значок.
3. Убедитесь, что уведомление о получении, затем щелкните **ОК** toodismiss hello уведомления.
4. Повторите шаг 2 и немедленно закрыть hello приложения, а затем убедитесь, что отображается уведомление.

Вы успешно завершили ознакомление с данным учебником.

<!-- Images. -->

<!-- URLs. -->



