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
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a>Начало работы со Службами мобильного взаимодействия Azure для приложений Xamarin.iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использования приложений и отправить push-уведомления toosegmented пользователей в приложении Xamarin.iOS.
В этом руководстве вы создадите пустое приложение Xamarin.iOS, которое собирает основные данные и получает push-уведомления с помощью службы push-уведомлений Apple (APNs).

> [!NOTE]
> Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов. Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Этот учебник требует hello следующее:

* [Xamarin Studio](http://xamarin.com/studio). Вы также можете использовать Visual Studio с расширением Xamarin, но в этом руководстве используется Xamarin Studio. Инструкции см. в руководстве по [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx). 
* [пакет Xamarin SDK для Служб мобильного взаимодействия](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).
> 
> 

## <a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для вашего приложения iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений
В этом руководстве содержатся «базовой интеграции» hello минимальный набор данных требуется toocollect и отправить push-уведомление.

Мы создадим простое приложение с помощью Xamarin toodemonstrate hello интеграции:

### <a name="create-a-new-xamarinios-project"></a>Создание нового проекта Xamarin.iOS
1. Запустите Xamarin Studio. Go слишком**файл** -> **New** -> **решения** 
   
    ![][1]
2. Выберите **одного представления приложения**, убедитесь, что выбран hello языка **C#** и нажмите кнопку **Далее**.
   
    ![][2]
3. Заполните hello **имя приложения** и hello **идентификатор организации** и нажмите кнопку **Далее**. 
   
    ![][3]
   
   > [!IMPORTANT]
   > Убедитесь, что hello, в конце концов используется toodeploy приложение iOS использует идентификатор приложения, которое соответствует точно совпадает с hello идентификатор пакета, здесь у профиль публикации. 
   > 
   > 
4. Обновление hello **имя проекта**, **имя решения** и **расположение** , если требуется и нажмите кнопку **создать**.
   
    ![][4]

Xamarin Studio создаст hello нашего примера приложения, в котором будет интегрировать мобильного охвата. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Подключение Engagement tooMobile внутренний сервер приложений
1. Щелкните правой кнопкой мыши hello **пакетов** папки в windows hello решений и выберите **Добавление пакетов...**
   
    ![][5]
2. Поиск hello **Microsoft Azure Mobile Engagement Xamarin SDK** и добавьте его tooyour решения.  
   
    ![][6]
3. Откройте **AppDelegate.cs** и добавьте следующее hello с помощью инструкции:
   
        using Microsoft.Azure.Engagement.Xamarin;
4. В hello **FinishedLaunching** метод, добавить следующие tooinitialize hello соединения с внутреннего сервера мобильного охвата hello. Убедитесь, что tooadd вашей **ConnectionString**. Этот код также использует фиктивное **NotificationIcon** добавляемым hello Mobile Engagement SDK, который можно привести tooreplace. 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <a id="monitor"></a>Включение мониторинга в реальном времени
В toostart порядок отправки данных и убедитесь, что пользователи hello активны необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана.

1. Откройте **ViewController.cs** и добавьте следующее hello с помощью инструкции:
   
        using Microsoft.Azure.Engagement.Xamarin;
2. Замените hello класс, от которого `ViewController` наследует от `UIViewController` слишком`EngagementViewController`. 

## <a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении
Mobile Engagement позволяет toointeract со своими пользователями и получить доступ с push-уведомления и сообщения в контексте hello кампаний в приложения. Этот модуль вызывается REACH на портале мобильного охвата hello.
Hello следующих разделах Настройка вашего приложения tooreceive их.

### <a name="modify-your-application-delegate"></a>Изменение делегата приложения
1. Откройте hello **AppDelegate.cs** и добавьте следующее hello с помощью инструкции:
   
        using System; 
2. Теперь внутри hello `FinishedLaunching` метод, добавить следующие tooregister для push-сообщений, после hello`EngagementAgent.init(...)`
   
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
3. И наконец — обновить или добавить hello следующие методы:
   
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
4. В вашей **Info.plist** файла в решении hello, убедитесь, что hello **идентификатор пакета** совпадает с hello **идентификатор приложения** имеется в профиле подготовки в hello разработчиков Apple По центру. 
   
    ![][7]
5. В hello же **Info.plist** файл, убедитесь в том, что возвращаются hello **Включение фоновых режимов** и **удаленного уведомления**. 
   
     ![][8]
6. Запустите приложение hello на устройстве hello, сопоставленную с данным профилем публикации. 

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
