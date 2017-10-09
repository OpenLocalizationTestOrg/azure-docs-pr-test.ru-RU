---
title: "aaaNotification концентраторов локализованные критические новостей учебника для iOS"
description: "Узнайте, как концентраторы уведомлений Azure Service Bus toosend toouse локализованные уведомлений с последними новостями (iOS)."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9fe88c0440e93b72d349574160ddcd85a7ba0be0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a>Использование концентраторов уведомлений критические toosend локализованные новостей tooiOS устройств
> [!div class="op_single_selector"]
> * [C# в Магазине Windows](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Обзор
В этом разделе показано, как toouse hello [шаблоны](notification-hubs-templates-cross-platform-push-messages.md) функции концентраторов уведомлений Azure toobroadcast критические уведомления новостей, локализованные языка и устройства. В этом учебнике, начинаться с приложение hello iOS, созданные в [toosend использования концентраторов уведомлений, новости]. После завершения можно будет tooregister для категорий, которые вас интересуют, указать язык в уведомления, которое tooreceive hello и получать только push-уведомлений для hello выбранных категорий на этом языке.

Существует два сценария toothis частей:

* приложение iOS позволяет клиентским устройств toospecify язык и toodifferent toosubscribe критические категории новостей;
* Hello внутренней осуществляет широковещательную рассылку уведомлений hello, с использованием hello **тега** и **шаблона** поддержки концентраторов уведомлений Azure.

## <a name="prerequisites"></a>Предварительные требования
Вы должны уже выполнили hello [toosend использования концентраторов уведомлений, новости] учебника и иметь hello кода, так как этот учебник построен непосредственно на этот код.

Наличие Visual Studio 2012 или более поздней версии не обязательно.

## <a name="template-concepts"></a>Основные сведения о шаблонах
В [toosend использования концентраторов уведомлений, новости] построении приложения, которое используется **теги** toonotifications toosubscribe новостей разных категорий.
Однако многие приложения ориентированы на несколько рынков и требуют локализации. Таким образом, содержимое hello hello уведомлений, сами имеют toobe локализованные доставленный toohello правильным набором устройств.
В этом разделе будет показано, как toouse hello **шаблона** функции концентраторов уведомлений tooeasily доставки локализованное уведомлений с последними новостями.

Примечание: один из способов toosend локализованные уведомления является toocreate нескольких версий каждого тега. Для экземпляра toosupport английском, французском и мандаринский, пришлось бы иметь три разные теги Мировые: «world_en», «world_fr» и «world_ch». Мы будет иметь toosend локализованной версии tooeach новостей hello world эти теги. В этом разделе используются шаблоны tooavoid hello увеличением числа теги и требование hello отправка нескольких сообщений.

На высоком уровне шаблоны являются toospecify способом как конкретного устройства следует получать такие уведомления. шаблон Hello указывает формат hello точное полезных данных с помощью ссылки tooproperties, которые являются частью приветственное сообщение, отправленное приложение в серверной части. В нашем случае мы отправим независимое от языка сообщение, которое содержит все поддерживаемые языки:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Затем мы гарантируем, что устройства регистрацию с шаблоном, который ссылается свойство правильный toohello. Для экземпляра приложения iOS, если оно tooregister для французского языка новостей зарегистрирует hello следующее:

    {
        aps:{
            alert: "$(News_French)"
        }
    }

Шаблоны — это очень мощная функция, о них можно узнать больше в нашей статье [Шаблоны](notification-hubs-templates-cross-platform-push-messages.md) .

## <a name="hello-app-user-interface"></a>пользовательский интерфейс приложения Hello
Теперь мы изменит приложение hello последние новости, созданный в разделе hello [toosend использования концентраторов уведомлений, новости] toosend локализованные новости, с помощью шаблонов.

В вашей MainStoryboard_iPhone.storyboard добавьте сегментированных управления с тремя hello языков, которые поддерживаются: английский, французский и китайский.

![][13]

Убедитесь в том tooadd IBOutlet в ваш ViewController.h как показано ниже:

![][14]

## <a name="building-hello-ios-app"></a>Построение приложения iOS hello
1. Добавьте в ваш Notification.h hello *retrieveLocale* метода и изменение хранилища hello и подписываться методы, как показано ниже:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    В вашей Notification.m измените hello *storeCategoriesAndSubscribe* метода, добавив параметр языкового стандарта hello и сохранить их в значения по умолчанию hello пользователя:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    Затем измените hello *подписаться* метод tooinclude hello языка:
   
        - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];
   
            NSString* localeString;
            switch (locale) {
                case 0:
                    localeString = @"English";
                    break;
                case 1:
                    localeString = @"French";
                    break;
                case 2:
                    localeString = @"Mandarin";
                    break;
            }
   
            NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];
   
            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
        }
   
    Обратите внимание на то, как мы теперь используют метод hello *registerTemplateWithDeviceToken*, а не *registerNativeWithDeviceToken*. При регистрации для шаблона у нас есть tooprovide hello json шаблона, а также имя шаблона hello (как в нашем приложении может возникнуть различные шаблоны tooregister). Внесите убедиться, что tooregister категорий, как теги, мы хотим toomake убедиться, что tooreceive hello notifciations для этих новостей.
   
    Добавьте метод tooretrieve hello языкового из пользовательских параметров по умолчанию hello:
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. Теперь, когда мы внесли изменения в наших класса уведомления, у нас есть toomake убедиться, что наши ViewController делает использование hello новый UISegmentControl. Добавьте следующие строки в hello hello *viewDidLoad* метод toomake убедиться, что tooshow hello языкового стандарта, выбранного в настоящее время:
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    Затем в вашей *подписаться* метод, изменить ваш вызов toohello *storeCategoriesAndSubscribe* toohello следующее:
   
        [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
            if (!error) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                      @"Subscribed!" delegate:nil cancelButtonTitle:
                                      @"OK" otherButtonTitles:nil, nil];
                [alert show];
            } else {
                NSLog(@"Error subscribing: %@", error);
            }
        }];
3. Наконец, у вас есть tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* метод в вашей AppDelegate.m, чтобы правильно, можно обновить регистрацию при запуске приложения. Изменить ваш вызов toohello *подписаться* метод уведомлений hello следующее:
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a>(Необязательно.) Отправьте локализованные шаблонные уведомления из консольного приложения .NET.
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a>(необязательно) Отправлять уведомления локализованный шаблон с устройства hello
Если не имеют доступа к tooVisual Studio или toojust теста, отправка уведомлений шаблона hello локализованные непосредственно из приложения hello на устройстве hello.  Вы можете простого добавления toohello параметры шаблона hello локализованные `SendNotificationRESTAPI` метод, определенный в предыдущем учебнике hello.

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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
                    \"News_English\":\"Breaking %@ News in English : %@\","
                    \"News_French\":\"Breaking %@ News in French : %@\","
                    \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
                    categoryTag, self.notificationMessage.text,
                    categoryTag, self.notificationMessage.text,  // insert English localized news here
                    categoryTag, self.notificationMessage.text,  // insert French localized news here
                    categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

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




## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об использовании шаблонов см. по следующим ссылкам:

* [Уведомление пользователей с помощью центров уведомлений: ASP.NET]
* [Уведомление пользователей с помощью центров уведомлений: мобильные службы]

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[toosend использования концентраторов уведомлений, новости]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[Уведомление пользователей с помощью центров уведомлений: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Уведомление пользователей с помощью центров уведомлений: мобильные службы]: /manage/services/notification-hubs/notify-users
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
