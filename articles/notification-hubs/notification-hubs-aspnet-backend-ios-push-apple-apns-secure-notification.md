---
title: "aaaAzure Secure принудительной отправки уведомлений концентраторы"
description: "Узнайте, как безопасные toosend push приложения iOS tooan уведомления из Azure. Примеры кода написаны на Objective-C и C#."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 86dd8d7042e5b9e55d2d7ff41cb42f23831fc575
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Безопасные push-уведомления посредством центров уведомлений Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Обзор
Поддержка уведомлений Push в Microsoft Azure позволяет tooaccess к использованию, несколькими платформами, масштабируемых push-инфраструктуру, которая значительно упрощает реализацию hello push-уведомлений для индивидуальных пользователей и корпоративных приложений для мобильных устройств платформы.

Иногда из-за ограничений tooregulatory или безопасности, приложение может возникнуть tooinclude что-нибудь в hello уведомление, которое не может передаваться через инфраструктуру hello Стандартная push-уведомлений. В данном учебнике как tooachieve hello такие же возможности, отправляя конфиденциальных данных через проверку подлинности безопасное соединение между hello клиентского устройства и внутреннего сервера приложения hello.

На высоком уровне hello поток выглядит следующим образом:

1. Hello приложения внутреннего интерфейса:
   * Сохраняет полезную нагрузку в базе данных серверной части.
   * Отправляет идентификатор hello toohello устройства создания уведомления (отправляются без защиты данных).
2. приложение Hello на устройстве hello, при получении уведомления hello:
   * устройство Hello обращается hello серверной части запроса hello безопасного полезных данных.
   * приложение Hello можно показать hello полезных данных в виде уведомлений на устройстве hello.

Очень важно, toonote, что предшествующий потока hello (и в этом учебнике) предполагается устройства hello склада маркер проверки подлинности в локальном хранилище после hello пользователь вошел в систему. Это гарантирует полностью эффективной работы, как hello устройства можно получить полезные данные безопасного hello уведомления, с помощью этого токена. Если приложение не хранить токены проверки подлинности на устройстве hello или может быть просрочен эти токены, hello приложения для устройств, при получении уведомления hello отображать универсального уведомление запроса приложение hello toolaunch hello пользователя. Затем приложение Hello проверяет подлинность пользователя hello и приводятся полезные данные уведомления hello.

В этом учебнике принудительной защиты как toosend push-уведомление безопасно. Hello учебник построен на hello [уведомить пользователей](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) учебник, поэтому hello шаги в этом учебнике должна выполнять первой.

> [!NOTE]
> В этом учебнике подразумевается, что вы создали и настроили центр уведомлений, как описано в руководстве [Приступая к работе с центрами уведомлений (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a>Изменение проекта iOS hello
Теперь, когда вы изменили вашей hello просто toosend серверной части приложения *идентификатор* уведомления, у вас есть toochange вашей toohandle приложения iOS, уведомления и обратный вызов к серверной части tooretrieve hello защитить toobe сообщений отображается.

tooachieve этой цели, у нас есть toowrite hello логику tooretrieve hello защищенное содержимое из hello серверной части приложения.

1. В **AppDelegate.m**, сделайте убедиться, что регистры приложения hello для автоматической уведомления, чтобы он обрабатывает hello идентификатор уведомления, отправленные hello серверной части. Добавить hello **UIRemoteNotificationTypeNewsstandContentAvailability** параметр в didFinishLaunchingWithOptions:
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. В вашей **AppDelegate.m** к добавлению раздела реализации вверху hello с объявления hello:
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. Затем добавьте в hello реализации раздел hello после кода, заменив заполнитель hello `{back-end endpoint}` с конечной точкой hello для настройки сервера был получен:

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences.

1. Теперь мы toohandle hello входящие уведомления и использовать метод hello выше содержимого toodisplay tooretrieve hello. Во-первых у нас есть tooenable вашей toorun приложения iOS в фоновом режиме hello при получении push-уведомлений. В **XCode**, выберите проект приложения на левой панели hello, а затем выберите целевую основным приложением в hello **цели** раздел из центральной панели hello.
2. Нажмите кнопку вашей **возможности** вверху hello на центральной панели и проверьте hello **удаленного уведомления** флажок.
   
    ![][IOS1]
3. В **AppDelegate.m** добавьте следующий метод toohandle извещающих уведомлений hello:
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    Обратите внимание, что он является более предпочтительным, чем toohandle случаях hello отсутствующее свойство Заголовок проверки подлинности или отклонение с помощью серверной части hello. Hello конкретных обработки этих вариантов основном зависят от вам целевой. Один из вариантов — toodisplay уведомление с универсальным запрашивать hello tooauthenticate tooretrieve hello фактическое уведомление для пользователей.

## <a name="run-hello-application"></a>Запустите приложение hello
toorun Здравствуйте, приложения, hello следующие:

1. В XCode запустите приложение hello на устройстве физических операций ввода-вывода (push-уведомлений не будет работать в симуляторе hello).
2. В приложении iOS hello пользовательского интерфейса введите имя пользователя и пароль. Это может быть любой строкой, но они должны быть hello одинаковое значение.
3. В приложении iOS hello пользовательского интерфейса, нажмите кнопку **входа**. Затем нажмите **Отправить push-уведомление**. Вы увидите hello безопасных уведомлений, отображаемых в свой центр уведомлений.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
