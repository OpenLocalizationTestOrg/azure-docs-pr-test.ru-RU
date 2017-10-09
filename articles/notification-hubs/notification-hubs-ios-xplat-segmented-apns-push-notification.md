---
title: "aaaNotification концентраторов критические новостей учебника - операций ввода-вывода"
description: "Узнайте, как toosend концентраторы уведомлений Azure Service Bus toouse критические новостей уведомления tooiOS устройств."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Использование концентраторов уведомлений toosend новости
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Обзор
В этом разделе показано, как toouse концентраторов уведомлений Azure toobroadcast критические новостей уведомления tooan приложения iOS. После завершения будет быть может tooregister переноса категории новостей нужных вам и получения только push-уведомлений для этих категорий. Этот сценарий представлен общий шаблон для многих приложений, где уведомления состоят из отправленных toobe toogroups пользователей, которым был объявлен ранее интересующих их, например, средство чтения RSS, приложений для вентиляторов музыку и т. д.

Широковещательный сценарии реализуются путем включения одного или нескольких *теги* при создании регистрации в концентраторе уведомлений hello. Отправке уведомлений tooa тегов, все устройства, которые зарегистрированы для тега hello получат уведомление hello. Так как теги являются просто строками, у которых нет toobe заранее подготовлены. Дополнительные сведения о тегах см. в разделе слишком[маршрутизации концентраторов уведомлений и выражения с тегами](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Предварительные требования
В этом разделе основан на приложение hello, созданный в [приступить к работе с концентраторами уведомлений][get-started]. Перед началом работы с данным руководством необходимо выполнить задания руководства по [началу работы с центрами уведомлений][get-started].

## <a name="add-category-selection-toohello-app"></a>Добавить приложение toohello Выбор категории
Hello первым шагом является tooadd hello пользовательского интерфейса элементов tooyour существующей раскадровки, позволяющие tooregister категории tooselect пользователя hello. выбранные пользователем категории Hello хранятся на устройстве hello. При запуске приложение hello регистрацию устройств создается в концентратор уведомлений с категориями hello выбран как теги.

1. Добавьте в ваш MainStoryboard_iPhone.storyboard hello следующие компоненты из библиотеки hello объекта.
   
   * метка с текстом "Экстренные новости";
   * метки с текстами категории "Мир", "Политика", "Бизнес", "Технология", "Наука", "Спорт";
   * Шесть переключателя, по одному на каждую категорию, задать для каждого ключа **состояние** toobe **Off** по умолчанию.
   * Одна кнопка с надписью «Подписка».
     
     Раскадровка должна выглядеть следующим образом:
     
     ![][3]
2. В редакторе помощника hello создания выходов для всех коммутаторов hello и вызывать их «WorldSwitch», «PoliticsSwitch», «BusinessSwitch», «TechnologySwitch», «ScienceSwitch», «SportsSwitch»
3. Создайте действие для кнопки с названием "Подписка". Ваш ViewController.h должна содержать hello следующее:
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. Создайте класс **Cocoa Touch Class** с именем `Notifications`. Скопируйте следующий код в разделе интерфейса hello hello файла Notifications.h hello:
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. Добавьте следующие директивы tooNotifications.m импорта hello:
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. Скопируйте следующий код в разделе реализации hello hello файла Notifications.m hello.
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    Этот класс использует локальное хранилище toostore и получить hello категории новостей, который получит это устройство. Кроме того, он содержит метод tooregister для следующих категорий с помощью [шаблона](notification-hubs-templates-cross-platform-push-messages.md) регистрации.

1. В файле AppDelegate.h hello добавьте инструкцию импорта для Notifications.h и добавьте свойство для экземпляра класса уведомлений hello:
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. В hello **didFinishLaunchingWithOptions** метод в AppDelegate.m, добавить hello кода tooinitialize hello уведомления экземпляр в начале hello метод hello.  
   
    `HUBNAME`и `HUBLISTENACCESS` (определенная в hubinfo.h) уже должна содержать hello `<hub name>` и `<connection string with listen access>` заменой заполнителей уведомления имя и hello строку подключения к концентратору для *DefaultListenSharedAccessSignature*, полученный ранее
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > Так как учетные данные, которые распространяются с помощью клиентского приложения, обычно не безопасны, hello ключ для прослушивания доступа следует распространять только с помощью клиентского приложения. Прослушивать доступа включает tooregister вашего приложения для уведомлений, но существующие регистрации нельзя изменить, и не может отправлять уведомления. Полный доступ Hello используется в защищенной серверной службе для отправки уведомлений и изменять существующие регистрации.
   > 
   > 
3. В hello **didRegisterForRemoteNotificationsWithDeviceToken** метод в AppDelegate.m, замените hello код в метод hello hello после уведомления класс маркера toohello устройства кода toopass hello. класс уведомления Hello выполнит hello регистрации уведомлений с категориями hello. При изменении выбора категории hello пользователя мы называем hello `subscribeWithCategories` метода в ответ toohello **подписаться** кнопку tooupdate их.
   
   > [!NOTE]
   > Так как в любое время можно вероятность hello токен устройства, назначаемые hello Apple Push Notification Service (APNS), необходимо зарегистрировать для уведомлений часто tooavoid сбоев уведомлений. В этом примере регистрируется для уведомления каждый раз при запуске этого приложения hello. Для приложений, которые часто выполняются более чем один раз в день, возможно, если можно пропустить пропускной способности toopreserve регистрации менее чем за день прошел с момента предыдущей регистрации hello.
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    Обратите внимание, что на этом этапе следует никакой другой код в hello **didRegisterForRemoteNotificationsWithDeviceToken** метод.

1. Hello следующие методы должны уже присутствовать в AppDelegate.m завершению hello [приступить к работе с концентраторами уведомлений] [ get-started] учебника.  В противном случае добавьте их.
   
    -(void) {messageText:(NSString *) сообщение MessageBox:(NSString *) заголовка
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    }
   
   * didReceiveRemoteNotification приложения:(UIApplication *) (void) приложения: (NSDictionary *) userInfo {NSLog (@"% @", сведений о пользователях);   [самостоятельной MessageBox:@"Notification» сообщение: [valueForKey:@"alert [userInfo objectForKey:@"aps»]»]]; }
   
   Этот метод отвечает за уведомлений, полученных выполняющейся приложение hello, отображая простой **UIAlert**.
2. В ViewController.m, добавьте оператор импорта для hello AppDelegate.h и скопируйте следующий код в hello создан XCode **подписаться** метод. Этот код обновит hello уведомления регистрации toouse hello новой категории теги hello пользователь выбрал в пользовательском интерфейсе hello.
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   Этот метод создает **NSMutableArray** из категории и использует hello **уведомления** список hello toostore классов в hello локального хранилища и регистры hello соответствующие теги в концентраторе уведомлений. При изменении категории регистрации hello воссоздается при hello новые категории.
3. В ViewController.m, добавьте следующий код в hello hello **viewDidLoad** метод tooset hello пользовательский интерфейс на основе ранее сохраненные hello категорий.

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



При запуске приложение hello приложение Hello можно хранить набор категорий в hello tooregister локального хранилища используется устройством с концентратором уведомлений hello.  Hello пользователя можно изменить выбор hello категорий во время выполнения и нажмите кнопку hello **подписаться** метод tooupdate hello регистрации для устройства hello. Далее потребуется обновить hello toosend приложения hello, критические уведомления новостей непосредственно в само приложение hello.

## <a name="optional-sending-tagged-notifications"></a>(Необязательно.) Отправка уведомлений с тегами
Если у вас нет доступа к tooVisual Studio, можно пропустить следующий раздел toohello и отправки уведомления из самого приложения hello. Также можно отправлять уведомление правильный шаблон hello из hello [классический портал Azure] используя вкладку hello отладки для центра уведомлений. 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a>(необязательно) Отправлять уведомления с устройства hello
Обычно уведомления будут отправляться с помощью серверной службы, но вы можете отправлять уведомлений с последними новостями непосредственно из приложения hello. toodo это корпорация Майкрософт будет обновлять hello `SendNotificationRESTAPI` метод, определенный в hello [приступить к работе с концентраторами уведомлений] [ get-started] учебника.

1. В обновление hello ViewController.m `SendNotificationRESTAPI` как следует, что принимает в качестве параметра для тега категории hello и отправляет соответствующие hello [шаблона](notification-hubs-templates-cross-platform-push-messages.md) уведомления.
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add hello category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];
   
            [dataTask resume];
        }
2. В обновление hello ViewController.m **отправить уведомление** действие, как показано в далее кода hello. Чтобы он будет отправлять уведомления hello по отдельности с помощью каждого тега и отправить toomultiple платформы.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. Повторно создайте проект и убедитесь, что у вас не возникли ошибки сборки.

## <a name="run-hello-app-and-generate-notifications"></a>Запустите приложение hello и создавать уведомления
1. Нажмите клавишу hello запустите кнопка toobuild hello проект и запустить приложение hello. Выберите некоторые tooand toosubscribe критические параметры новостей, а затем клавишу hello **Subscribe** кнопки. Вы увидите соответствующее диалоговое окно приветствия, которые были подписаны уведомления.
   
    ![][1]
   
    При выборе **Subscribe**, hello hello выбранных категорий приложений преобразует в теги и запрашивает новую регистрацию устройств для hello выбранных тегов из концентратора уведомлений hello.
2. Введите сообщение toobe, передаются как новости нажмите клавишу hello **отправить уведомление** кнопки. Также можно запустить hello .NET консольного приложения toogenerate уведомления.
   
    ![][2]
3. Новости toobreaking каждого устройства подписка получит hello уведомлений с последними новостями который только что отправлен.

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике мы узнали, каким образом toobroadcast новости по категориям. Рассмотрим, выполнив одну из hello следующие учебники, выделите других расширенных сценариях концентраторов уведомлений.

* **[Использовать локализованные toobroadcast новости концентраторы уведомлений]**
  
    Узнайте, как критические отправки tooenable новостей приложения hello tooexpand локализованные уведомления.

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Использовать локализованные toobroadcast новости концентраторы уведомлений]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[классический портал Azure]: https://manage.windowsazure.com
