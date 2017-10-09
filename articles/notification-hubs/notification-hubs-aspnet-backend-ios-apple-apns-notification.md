---
title: "aaaAzure пользователям уведомления концентраторов уведомлений для iOS с помощью серверного приложения .NET"
description: "Узнайте, как toosend push-уведомления toousers в Azure. Примеры кода, написанного на языке C цель и hello .NET API для внутреннего hello."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 1f7d1410-ef93-4c4b-813b-f075eed20082
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 56aed5b04d2d985b3f0e50c58991607f07b61248
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a>Уведомление пользователей iOS через центры уведомлений с помощью серверной части .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Обзор
Поддержка уведомлений Push в Azure позволяет tooaccess к использованию, многоплатформенных и масштабируемых push-инфраструктуру, которая значительно упрощает реализацию hello push-уведомлений для индивидуальных пользователей и корпоративных приложений для мобильных устройств платформы. Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa определенное приложение пользователя на конкретном устройстве. Серверной части ASP.NET WebAPI — используется tooauthenticate клиентов и уведомления toogenerate, как показано в раздел руководства hello [регистрации из серверной части приложения](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).

> [!NOTE]
> В этом учебнике подразумевается, что вы создали и настроили центр уведомлений, как описано в руководстве [Приступая к работе с центрами уведомлений (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md). Этот учебник содержит также hello готовности toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) учебника.
> Если toouse мобильные приложения как безопасности внутренней службы, см. hello [мобильных приложений Приступая к работе с Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a>Изменение приложения iOS
1. Просмотр приложения на одной странице Привет открыть созданный hello [Приступая к работе с концентраторами уведомлений (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) учебника.
   
   > [!NOTE]
   > В этом разделе подразумевается, что вы настроили свой проект, указав пустое имя организации. В противном случае вам потребуется tooprepend вашей организации tooall имя класса имена.
   > 
   > 
2. В вашей Main.storyboard добавьте hello компонентов показано на снимке экрана приветствия ниже из библиотеки hello объекта.
   
    ![][1]
   
   * **Имя пользователя**: UITextField с текст заполнителя *введите имя пользователя*, непосредственно под hello отправлять результаты метку и ограниченного toohello влево и правой границы и под hello отправить результаты метки.
   * **Пароль**: UITextField с текст заполнителя *ввод пароля*, немедленно ниже hello текстовое поле имени пользователя и ограниченного toohello слева и справа поля и под текстовое поле имени пользователя hello. Проверьте hello **Secure ввод текста** в диалоговом окне инспектора атрибут hello в разделе *возвращать ключ*.
   * **Войдите в**: UIButton с меткой сразу под hello пароль текстовое поле и снимите флажок hello **включено** в диалоговом окне инспектора атрибуты hello в разделе *содержимое элемента управления*
   * **WNS**: метка и отправка tooenable коммутатора hello уведомления службы уведомлений Windows, если он установлен и настроен на концентраторе hello. В разделе hello [Приступая к работе Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) учебника.
   * **GCM**: метки и отправка tooenable коммутатора hello Cloud Messaging tooGoogle уведомления, если он установлен и настроен на концентраторе hello. См. руководство [Отправка push-уведомлений в приложения Android с помощью центров уведомлений Azure](notification-hubs-android-push-notification-google-gcm-get-started.md).
   * **APNS**: Label и отправка tooenable коммутатора hello toohello уведомления службы уведомлений Apple платформы.
   * **Recipent Username**: UITextField с замещающий текст *получателя тег имени пользователя*, сразу под hello GCM метки и ограниченного toohello левого, правого поля и под hello GCM метки.

    Некоторые компоненты были добавлены в hello [Приступая к работе с концентраторами уведомлений (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) учебника.

1. **CTRL** перетащите из компонентов hello в представлении tooViewController.h hello и добавить эти новые выходы.
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used tooenable hello buttons on hello UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used tooenabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. В ViewController.h, добавьте следующее hello `#define` под инструкциях импорта. Замена hello *< Введите ваш конечную точку серверной части\>*  заполнитель hello использовать toodeploy внутренний сервер приложений в предыдущем разделе hello URL-адрес назначения. Например, *http://you_backend.azurewebsites.net*.
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. В проекте, создайте новый **Cocoa Touch класс** с именем **RegisterClient** toointerface с hello серверной части ASP.NET был создан. Создание hello класс, наследующий от `NSObject`. Затем добавьте следующий код в hello RegisterClient.h hello.
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. В hello RegisterClient.m обновления hello `@interface` раздела:
   
        @interface RegisterClient ()
   
        @property (strong, nonatomic) NSURLSession* session;
        @property (strong, nonatomic) NSURLSession* endpoint;
   
        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion;
        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion;
        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSString*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion;
   
        @end
5. Замените hello `@implementation` раздела hello RegisterClient.m с hello, следующий код.

        @implementation RegisterClient

        // Globals used by RegisterClient
        NSString *const RegistrationIdLocalStorageKey = @"RegistrationId";

        -(instancetype) initWithEndpoint:(NSString*)Endpoint
        {
            self = [super init];
            if (self) {
                NSURLSessionConfiguration* config = [NSURLSessionConfiguration defaultSessionConfiguration];
                _session = [NSURLSession sessionWithConfiguration:config delegate:nil delegateQueue:nil];
                _endpoint = Endpoint;
            }
            return self;
        }

        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
                    andCompletion:(void(^)(NSError*))completion
        {
            [self tryToRegisterWithDeviceToken:token tags:tags retry:YES andCompletion:completion];
        }

        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion
        {
            NSSet* tagsSet = tags?tags:[[NSSet alloc] init];

            NSString *deviceTokenString = [[token description]
                stringByTrimmingCharactersInSet:[NSCharacterSet characterSetWithCharactersInString:@"<>"]];
            deviceTokenString = [[deviceTokenString stringByReplacingOccurrencesOfString:@" " withString:@""]
                                    uppercaseString];

            [self retrieveOrRequestRegistrationIdWithDeviceToken: deviceTokenString
                completion:^(NSString* registrationId, NSError *error) {
                NSLog(@"regId: %@", registrationId);
                if (error) {
                    completion(error);
                    return;
                }

                [self upsertRegistrationWithRegistrationId:registrationId deviceToken:deviceTokenString
                    tags:tagsSet andCompletion:^(NSURLResponse * response, NSError *error) {
                    if (error) {
                        completion(error);
                        return;
                    }

                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if (httpResponse.statusCode == 200) {
                        completion(nil);
                    } else if (httpResponse.statusCode == 410 && retry) {
                        [self tryToRegisterWithDeviceToken:token tags:tags retry:NO andCompletion:completion];
                    } else {
                        NSLog(@"Registration error with response status: %ld", (long)httpResponse.statusCode);

                        completion([NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }

                }];
            }];
        }

        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSData*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion
        {
            NSDictionary* deviceRegistration = @{@"Platform" : @"apns", @"Handle": token,
                                                    @"Tags": [tags allObjects]};
            NSData* jsonData = [NSJSONSerialization dataWithJSONObject:deviceRegistration
                                options:NSJSONWritingPrettyPrinted error:nil];

            NSLog(@"JSON registration: %@", [[NSString alloc] initWithData:jsonData
                                                encoding:NSUTF8StringEncoding]);

            NSString* endpoint = [NSString stringWithFormat:@"%@/api/register/%@", _endpoint,
                                    registrationId];
            NSURL* requestURL = [NSURL URLWithString:endpoint];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"PUT"];
            [request setHTTPBody:jsonData];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
            [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                if (!error)
                {
                    completion(response, error);
                }
                else
                {
                    NSLog(@"Error request: %@", error);
                    completion(nil, error);
                }
            }];
            [dataTask resume];
        }

        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion
        {
            NSString* registrationId = [[NSUserDefaults standardUserDefaults]
                                        objectForKey:RegistrationIdLocalStorageKey];

            if (registrationId)
            {
                completion(registrationId, nil);
                return;
            }

            // request new one & save
            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/api/register?handle=%@",
                                    _endpoint, token]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"POST"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSString* registrationId = [[NSString alloc] initWithData:data
                        encoding:NSUTF8StringEncoding];

                    // remove quotes
                    registrationId = [registrationId substringWithRange:NSMakeRange(1,
                                        [registrationId length]-2)];

                    [[NSUserDefaults standardUserDefaults] setObject:registrationId
                        forKey:RegistrationIdLocalStorageKey];
                    [[NSUserDefaults standardUserDefaults] synchronize];

                    completion(registrationId, nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }

        @end

    Приведенный выше код Hello реализует логику hello и объясняются в руководстве по hello [регистрации из внутренний сервер приложений](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) с помощью NSURLSession tooperform REST вызывает tooyour внутреннего сервера приложения, а также NSUserDefaults toolocally хранилище hello registrationId возвращенных hello концентратора уведомлений.

    Обратите внимание, что для этого класса требуется его свойство **authorizationHeader** toobe правильно настроенной toowork заказа. Это свойство задается hello **ViewController** класса после входа hello.

1. В ViewController.h добавьте оператор `#import` для RegisterClient.h. Затем добавьте объявление для hello маркер устройства и ссылаться на tooa `RegisterClient` экземпляра в hello `@interface` раздела:
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. В ViewController.m, добавьте объявление закрытого метода в hello `@interface` раздела:
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> Hello следующий фрагмент не схему проверки подлинности, следует заменить hello реализация hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** с вашей механизм проверки подлинности При этом создается toobe токена проверки подлинности, занятая hello register класса клиента, например OAuth Active Directory.
> 
> 

1. Затем в hello `@implementation` раздел ViewController.m добавьте следующий код, который добавляет реализации hello параметр hello устройства маркера и проверки подлинности заголовка hello.
   
        -(void) setDeviceToken: (NSData*) deviceToken
        {
            _deviceToken = deviceToken;
            self.LogInButton.enabled = YES;
        }
   
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
        {
            NSString* headerValue = [NSString stringWithFormat:@"%@:%@", username, password];
   
            NSData* encodedData = [[headerValue dataUsingEncoding:NSUTF8StringEncoding] base64EncodedDataWithOptions:NSDataBase64EncodingEndLineWithCarriageReturn];
   
            self.registerClient.authenticationHeader = [[NSString alloc] initWithData:encodedData
                                                        encoding:NSUTF8StringEncoding];
        }
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
   
    Обратите внимание на то, как маркер устройства hello параметр делает hello кнопку входа. Это так, как в рамках действия входа hello регистрирует контроллер представление hello push-уведомления с внутреннего сервера приложения hello. Таким образом нам не нужно войти toobe действия доступны пока hello маркер устройства был правильно настроен. Чтобы отделить журнал hello в регистрации push hello до тех пор, пока бывшая hello производится перед выполнением последний hello.
2. В ViewController.m, используйте следующий метод действия hello tooimplement фрагменты для hello вашей **входа в** кнопки и метод toosend hello уведомлений сообщения с помощью hello серверной части ASP.NET.
   
       - (IBAction) LogInAction: отправителя (id) {/ / создать заголовок проверки подлинности и установите его в клиент регистра NSString * имя пользователя = self. UsernameField.text;   Пароль NSString * = self. PasswordField.text;
   
           [self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];
   
           __weak ViewController * selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken теги: nil andCompletion:^(NSError* error) {Если (! ошибка) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success» message:@"Registered успешно! "];});}}];}

        - (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];

            Передавать hello тег pns и имя пользователя в качестве параметров с toohello ASP.NET hello REST URL-адрес внутреннего NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @», BACKEND_ENDPOINT pns, usernameTag]];

            Запрос NSMutableURLRequest * = [NSMutableURLRequest requestWithURL:requestURL];    [запрос setHTTPMethod:@"POST»];

            Получать hello макетов authenticationheader от клиента регистра hello NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @», self.registerClient.authenticationHeader];    [запрос setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization»];

            Добавьте текст сообщения уведомления hello [запрос setValue:@"application/json;charset=utf-8» forHTTPHeaderField:@"Content-Type»];    [запросить setHTTPBody: [сообщений dataUsingEncoding:NSUTF8StringEncoding]];

            Выполнение hello отправка уведомлений API-интерфейса REST на hello ASP.NET серверной NSURLSessionDataTask * dataTask = [сеанса dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *Ошибка) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) ответа;        Если (ошибка || httpResponse.statusCode! = 200) {NSString* состояние = [stringWithFormat:@"Error NSString состояние для % @: % d\nError: %@\n», pns, httpResponse.statusCode, ошибка];            dispatch_async(dispatch_get_main_queue(), ^ {/ / добавление текста, так как все вызовы 3 PNS также могут быть tooview сведения [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            }];    [dataTask resume]; }


1. Обновить действие hello для hello **отправить уведомление** кнопку серверной части ASP.NET hello toouse и отправлять tooany PNS, включаемые к коммутатору.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            //[self SendNotificationRESTAPI];
            [self SendToEnabledPlatforms];
        }


        -(void)SendToEnabledPlatforms
        {
            NSString* json = [NSString stringWithFormat:@"\"%@\"",self.notificationMessage.text];

            [self.sendResults setText:@""];

            if ([self.WNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"wns" UsernameTag:self.RecipientField.text Message:json];

            if ([self.GCMSwitch isOn])
                [self SendNotificationASPNETBackend:@"gcm" UsernameTag:self.RecipientField.text Message:json];

            if ([self.APNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"apns" UsernameTag:self.RecipientField.text Message:json];
        }



1. В функции **ViewDidLoad**, добавьте следующий экземпляром RegisterClient tooinstantiate hello hello и задайте hello делегат для текстового поля.
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. Теперь в **AppDelegate.m**, удалите все содержимое hello hello метода **приложения: didRegisterForPushNotificationWithDeviceToken:** и заменить ее именем hello, убедитесь, что следующие toomake, Здравствуйте, представление контроллер содержит маркер устройства последнюю hello, полученные из APNs.
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. Finally в **AppDelegate.m**, убедитесь, что у вас есть hello следующий метод:
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a>Hello тестового приложения
1. В XCode запустите приложение hello на устройстве физических операций ввода-вывода (push-уведомлений не будет работать в симуляторе hello).
2. В приложении iOS hello пользовательского интерфейса введите имя пользователя и пароль. Это может быть любой строкой, но они оба должны быть hello же строковое значение. Затем нажмите кнопку **Log In**(Войти).
   
    ![][2]
3. Должно отобразиться всплывающее окно с сообщением об успешной регистрации. Нажмите кнопку **ОК**.
   
    ![][3]
4. В hello **тег username получателя* текста введите используется вместе с регистрацией hello с другого устройства тег имени пользователя hello.
5. Введите сообщение уведомления и нажмите кнопку **Отправить уведомление**.  Только устройства hello имеет регистрации с тегом имя получателя пользователя hello сообщение hello уведомления.  Он отправляется только toothose пользователей.
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
