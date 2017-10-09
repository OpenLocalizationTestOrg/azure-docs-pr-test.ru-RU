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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a>Начало работы со Службами мобильного взаимодействия Azure для приложений iOS в Swift
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использования приложений и отправлять push-уведомления toosegmented пользователей tooan операций ввода-вывода приложения.
В этом учебнике вы создадите пустое приложение iOS, которое собирает основные данные и получает push-уведомления с помощью Apple Push Notification System (APNS).

Этот учебник требует hello следующее:

* XCode 8, который можно установить из MAC App Store;
* Hello [iOS Mobile Engagement SDK]
* Сертификат push-уведомлений (P12), который можно получить в центре разработки для Apple

> [!NOTE]
> В этом учебнике используется Swift версии 3.0. 
> 
> 

Завершение изучения этого руководства является необходимым условием для работы со всеми другими руководствами, посвященными Службам мобильного взаимодействия для приложений iOS.

> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).
> 
> 

## <a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для вашего приложения iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений
В этом руководстве содержатся «базовой интеграции», который hello минимальный набор данных требуется toocollect и отправить push-уведомление. Hello полной интеграции документацию можно найти в hello [iOS Mobile Engagement SDK-интеграция](mobile-engagement-ios-sdk-overview.md)

Мы создадим простое приложение с помощью XCode toodemonstrate hello интеграции:

### <a name="create-a-new-ios-project"></a>Создание проекта iOS
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a>Подключение Engagement tooMobile внутренний сервер приложений
1. Загрузите hello [iOS Mobile Engagement SDK]
2. Извлеките hello. tar.gz файл tooa папку на компьютере
3. Щелкните правой кнопкой мыши проект hello и выберите пункт «Добавить файлы слишком...»
   
    ![][1]
4. Перейдите в папку toohello, будут извлечены hello SDK и выберите hello `EngagementSDK` папки, а затем нажмите кнопку ОК.
   
    ![][2]
5. Откройте hello `Build Phases` вкладке и в hello `Link Binary With Libraries` меню добавьте hello платформы, как показано ниже:
   
    ![][3]
6. Создайте мост заголовок toobe может toouse hello API пакета SDK для элемента цель C, выбрав Файл > Создать > Файл > iOS > источника > файла заголовка.
   
    ![][4]
7. Измените hello мост заголовок файла tooexpose Mobile Engagement Objective-C tooyour Swift кода, добавьте следующие импорты hello:
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. В разделе Параметры построения убедитесь, что hello параметр в списке Swift компилятора - формирования кода сборки заголовка мост Objective-C имеет заголовок toothis пути. Ниже приведен пример пути: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (в зависимости от пути hello)**
   
   ![][6]
9. Вернитесь к предыдущему окну toohello портал Azure в вашем приложении *сведений о соединении* страницы и скопируйте hello строки подключения
   
   ![][5]
10. Теперь вставьте строку подключения hello в hello `didFinishLaunchingWithOptions` делегата
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <a id="monitor"></a>Включение мониторинга в реальном времени
В toostart порядок отправки данных и убедитесь, что пользователи hello active необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана (действие).

1. Откройте hello **ViewController.swift** и замените hello базовый класс **ViewController** toobe **EngagementViewController**:
   
    `class ViewController : EngagementViewController {`

## <a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении
Mobile Engagement позволяет toointeract и получить доступ с пользователями с Push-уведомления и обмен сообщениями в приложении в контексте hello кампаний. Этот модуль вызывается REACH на портале мобильного охвата hello.
Hello ниже настроит вашего приложения tooreceive их.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Включить вашего приложения tooreceive автоматической Push-уведомления
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Добавьте проект tooyour библиотеки Reach hello
1. Щелкните правой кнопкой мыши проект
2. Выберите `Add file too...`
3. Перейдите в папку toohello, будут извлечены hello SDK
4. Выберите hello `EngagementReach` папки
5. Нажмите "Добавить"
6. Измените hello мост заголовков Objective-C Mobile Engagement Reach tooexpose заголовок файла и добавьте следующие импорты hello:
   
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

### <a name="modify-your-application-delegate"></a>Изменение делегата приложения
1. Внутри hello `didFinishLaunchingWithOptions` — создать модуль reach и передать его tooyour существующую строку инициализации участия:
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Включить вашего приложения tooreceive Push-уведомления APNS
1. Добавьте следующие строки toohello hello `didFinishLaunchingWithOptions` метод:
   
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
2. Добавить hello `didRegisterForRemoteNotificationsWithDeviceToken` метод следующим образом:
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. Добавить hello `didReceiveRemoteNotification:fetchCompletionHandler:` метод следующим образом:
   
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
