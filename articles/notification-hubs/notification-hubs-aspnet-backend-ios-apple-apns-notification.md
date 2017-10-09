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
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="a8978-104">Уведомление пользователей iOS через центры уведомлений с помощью серверной части .NET</span><span class="sxs-lookup"><span data-stu-id="a8978-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="a8978-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="a8978-105">Overview</span></span>
<span data-ttu-id="a8978-106">Поддержка уведомлений Push в Azure позволяет tooaccess к использованию, многоплатформенных и масштабируемых push-инфраструктуру, которая значительно упрощает реализацию hello push-уведомлений для индивидуальных пользователей и корпоративных приложений для мобильных устройств платформы.</span><span class="sxs-lookup"><span data-stu-id="a8978-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="a8978-107">Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa определенное приложение пользователя на конкретном устройстве.</span><span class="sxs-lookup"><span data-stu-id="a8978-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="a8978-108">Серверной части ASP.NET WebAPI — используется tooauthenticate клиентов и уведомления toogenerate, как показано в раздел руководства hello [регистрации из серверной части приложения](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="a8978-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="a8978-109">В этом учебнике подразумевается, что вы создали и настроили центр уведомлений, как описано в руководстве [Приступая к работе с центрами уведомлений (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a8978-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="a8978-110">Этот учебник содержит также hello готовности toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="a8978-110">This tutorial is also hello prerequisite toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="a8978-111">Если toouse мобильные приложения как безопасности внутренней службы, см. hello [мобильных приложений Приступая к работе с Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="a8978-111">If you want toouse Mobile Apps as your backend service, see hello [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="a8978-112">Изменение приложения iOS</span><span class="sxs-lookup"><span data-stu-id="a8978-112">Modify your iOS app</span></span>
1. <span data-ttu-id="a8978-113">Просмотр приложения на одной странице Привет открыть созданный hello [Приступая к работе с концентраторами уведомлений (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="a8978-113">Open hello Single Page view app you created in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a8978-114">В этом разделе подразумевается, что вы настроили свой проект, указав пустое имя организации.</span><span class="sxs-lookup"><span data-stu-id="a8978-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="a8978-115">В противном случае вам потребуется tooprepend вашей организации tooall имя класса имена.</span><span class="sxs-lookup"><span data-stu-id="a8978-115">If not, you will need tooprepend your organization name tooall class names.</span></span>
   > 
   > 
2. <span data-ttu-id="a8978-116">В вашей Main.storyboard добавьте hello компонентов показано на снимке экрана приветствия ниже из библиотеки hello объекта.</span><span class="sxs-lookup"><span data-stu-id="a8978-116">In your Main.storyboard add hello components shown in hello screenshot below from hello object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="a8978-117">**Имя пользователя**: UITextField с текст заполнителя *введите имя пользователя*, непосредственно под hello отправлять результаты метку и ограниченного toohello влево и правой границы и под hello отправить результаты метки.</span><span class="sxs-lookup"><span data-stu-id="a8978-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath hello send results label and constrained toohello left and right margins and beneath hello send results label.</span></span>
   * <span data-ttu-id="a8978-118">**Пароль**: UITextField с текст заполнителя *ввод пароля*, немедленно ниже hello текстовое поле имени пользователя и ограниченного toohello слева и справа поля и под текстовое поле имени пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="a8978-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath hello username text field and constrained toohello left and right margins and beneath hello username text field.</span></span> <span data-ttu-id="a8978-119">Проверьте hello **Secure ввод текста** в диалоговом окне инспектора атрибут hello в разделе *возвращать ключ*.</span><span class="sxs-lookup"><span data-stu-id="a8978-119">Check hello **Secure Text Entry** option in hello Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="a8978-120">**Войдите в**: UIButton с меткой сразу под hello пароль текстовое поле и снимите флажок hello **включено** в диалоговом окне инспектора атрибуты hello в разделе *содержимое элемента управления*</span><span class="sxs-lookup"><span data-stu-id="a8978-120">**Log in**: A UIButton labeled immediately beneath hello password text field and uncheck hello **Enabled** option in hello Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="a8978-121">**WNS**: метка и отправка tooenable коммутатора hello уведомления службы уведомлений Windows, если он установлен и настроен на концентраторе hello.</span><span class="sxs-lookup"><span data-stu-id="a8978-121">**WNS**: Label and switch tooenable sending hello notification Windows Notification Service if it has been setup on hello hub.</span></span> <span data-ttu-id="a8978-122">В разделе hello [Приступая к работе Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="a8978-122">See hello [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="a8978-123">**GCM**: метки и отправка tooenable коммутатора hello Cloud Messaging tooGoogle уведомления, если он установлен и настроен на концентраторе hello.</span><span class="sxs-lookup"><span data-stu-id="a8978-123">**GCM**: Label and switch tooenable sending hello notification tooGoogle Cloud Messaging if it has been setup on hello hub.</span></span> <span data-ttu-id="a8978-124">См. руководство [Отправка push-уведомлений в приложения Android с помощью центров уведомлений Azure](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a8978-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="a8978-125">**APNS**: Label и отправка tooenable коммутатора hello toohello уведомления службы уведомлений Apple платформы.</span><span class="sxs-lookup"><span data-stu-id="a8978-125">**APNS**: Label and switch tooenable sending hello notification toohello Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="a8978-126">**Recipent Username**: UITextField с замещающий текст *получателя тег имени пользователя*, сразу под hello GCM метки и ограниченного toohello левого, правого поля и под hello GCM метки.</span><span class="sxs-lookup"><span data-stu-id="a8978-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath hello GCM label and constrained toohello left and right margins and beneath hello GCM label.</span></span>

    <span data-ttu-id="a8978-127">Некоторые компоненты были добавлены в hello [Приступая к работе с концентраторами уведомлений (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="a8978-127">Some components were added in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="a8978-128">**CTRL** перетащите из компонентов hello в представлении tooViewController.h hello и добавить эти новые выходы.</span><span class="sxs-lookup"><span data-stu-id="a8978-128">**Ctrl** drag from hello components in hello view tooViewController.h and add these new outlets.</span></span>
   
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
2. <span data-ttu-id="a8978-129">В ViewController.h, добавьте следующее hello `#define` под инструкциях импорта.</span><span class="sxs-lookup"><span data-stu-id="a8978-129">In ViewController.h, add hello following `#define` just below your import statements.</span></span> <span data-ttu-id="a8978-130">Замена hello *< Введите ваш конечную точку серверной части\>*  заполнитель hello использовать toodeploy внутренний сервер приложений в предыдущем разделе hello URL-адрес назначения.</span><span class="sxs-lookup"><span data-stu-id="a8978-130">Substitute hello *<Enter Your Backend Endpoint\>* placeholder with hello Destination URL you used toodeploy your app backend in hello previous section.</span></span> <span data-ttu-id="a8978-131">Например, *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="a8978-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="a8978-132">В проекте, создайте новый **Cocoa Touch класс** с именем **RegisterClient** toointerface с hello серверной части ASP.NET был создан.</span><span class="sxs-lookup"><span data-stu-id="a8978-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** toointerface with hello ASP.NET back-end you created.</span></span> <span data-ttu-id="a8978-133">Создание hello класс, наследующий от `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="a8978-133">Create hello class inheriting from `NSObject`.</span></span> <span data-ttu-id="a8978-134">Затем добавьте следующий код в hello RegisterClient.h hello.</span><span class="sxs-lookup"><span data-stu-id="a8978-134">Then add hello following code in hello RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="a8978-135">В hello RegisterClient.m обновления hello `@interface` раздела:</span><span class="sxs-lookup"><span data-stu-id="a8978-135">In hello RegisterClient.m update hello `@interface` section:</span></span>
   
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
5. <span data-ttu-id="a8978-136">Замените hello `@implementation` раздела hello RegisterClient.m с hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="a8978-136">Replace hello `@implementation` section in hello RegisterClient.m with hello following code.</span></span>

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

    <span data-ttu-id="a8978-137">Приведенный выше код Hello реализует логику hello и объясняются в руководстве по hello [регистрации из внутренний сервер приложений](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) с помощью NSURLSession tooperform REST вызывает tooyour внутреннего сервера приложения, а также NSUserDefaults toolocally хранилище hello registrationId возвращенных hello концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a8978-137">hello code above implements hello logic explained in hello guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession tooperform REST calls tooyour app backend, and NSUserDefaults toolocally store hello registrationId returned by hello notification hub.</span></span>

    <span data-ttu-id="a8978-138">Обратите внимание, что для этого класса требуется его свойство **authorizationHeader** toobe правильно настроенной toowork заказа.</span><span class="sxs-lookup"><span data-stu-id="a8978-138">Note that this class requires its property **authorizationHeader** toobe set in order toowork properly.</span></span> <span data-ttu-id="a8978-139">Это свойство задается hello **ViewController** класса после входа hello.</span><span class="sxs-lookup"><span data-stu-id="a8978-139">This property is set by hello **ViewController** class after hello log in.</span></span>

1. <span data-ttu-id="a8978-140">В ViewController.h добавьте оператор `#import` для RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="a8978-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="a8978-141">Затем добавьте объявление для hello маркер устройства и ссылаться на tooa `RegisterClient` экземпляра в hello `@interface` раздела:</span><span class="sxs-lookup"><span data-stu-id="a8978-141">Then add a declaration for hello device token and reference tooa `RegisterClient` instance in hello `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="a8978-142">В ViewController.m, добавьте объявление закрытого метода в hello `@interface` раздела:</span><span class="sxs-lookup"><span data-stu-id="a8978-142">In ViewController.m, add a private method declaration in hello `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="a8978-143">Hello следующий фрагмент не схему проверки подлинности, следует заменить hello реализация hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** с вашей механизм проверки подлинности При этом создается toobe токена проверки подлинности, занятая hello register класса клиента, например OAuth Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8978-143">hello following snippet is not a secure authentication scheme, you should substitute hello implementation of hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token toobe consumed by hello register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="a8978-144">Затем в hello `@implementation` раздел ViewController.m добавьте следующий код, который добавляет реализации hello параметр hello устройства маркера и проверки подлинности заголовка hello.</span><span class="sxs-lookup"><span data-stu-id="a8978-144">Then in hello `@implementation` section of ViewController.m add hello following code which adds hello implementation for setting hello device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="a8978-145">Обратите внимание на то, как маркер устройства hello параметр делает hello кнопку входа.</span><span class="sxs-lookup"><span data-stu-id="a8978-145">Note how setting hello device token enables hello log in button.</span></span> <span data-ttu-id="a8978-146">Это так, как в рамках действия входа hello регистрирует контроллер представление hello push-уведомления с внутреннего сервера приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a8978-146">This is becasue as a part of hello login action, hello view controller registers for push notifications with hello app backend.</span></span> <span data-ttu-id="a8978-147">Таким образом нам не нужно войти toobe действия доступны пока hello маркер устройства был правильно настроен.</span><span class="sxs-lookup"><span data-stu-id="a8978-147">Hence, we do not want Log In action toobe accessible till hello device token has been properly set up.</span></span> <span data-ttu-id="a8978-148">Чтобы отделить журнал hello в регистрации push hello до тех пор, пока бывшая hello производится перед выполнением последний hello.</span><span class="sxs-lookup"><span data-stu-id="a8978-148">You can decouple hello log in from hello push registration as long as hello former happens before hello latter.</span></span>
2. <span data-ttu-id="a8978-149">В ViewController.m, используйте следующий метод действия hello tooimplement фрагменты для hello вашей **входа в** кнопки и метод toosend hello уведомлений сообщения с помощью hello серверной части ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a8978-149">In ViewController.m, use hello following snippets tooimplement hello action method for your **Log In** button and a method toosend hello notification message using hello ASP.NET backend.</span></span>
   
       - <span data-ttu-id="a8978-150">(IBAction) LogInAction: отправителя (id) {/ / создать заголовок проверки подлинности и установите его в клиент регистра NSString * имя пользователя = self. UsernameField.text;   Пароль NSString * = self. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="a8978-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="a8978-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="a8978-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="a8978-152">__weak ViewController * selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken теги: nil andCompletion:^(NSError* error) {Если (! ошибка) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success» message:@"Registered успешно! "];});}}];}</span><span class="sxs-lookup"><span data-stu-id="a8978-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="a8978-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="a8978-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="a8978-154">Передавать hello тег pns и имя пользователя в качестве параметров с toohello ASP.NET hello REST URL-адрес внутреннего NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @», BACKEND_ENDPOINT pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="a8978-154">// Pass hello pns and username tag as parameters with hello REST URL toohello ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="a8978-155">Запрос NSMutableURLRequest * = [NSMutableURLRequest requestWithURL:requestURL];    [запрос setHTTPMethod:@"POST»];</span><span class="sxs-lookup"><span data-stu-id="a8978-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="a8978-156">Получать hello макетов authenticationheader от клиента регистра hello NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @», self.registerClient.authenticationHeader];    [запрос setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization»];</span><span class="sxs-lookup"><span data-stu-id="a8978-156">// Get hello mock authenticationheader from hello register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="a8978-157">Добавьте текст сообщения уведомления hello [запрос setValue:@"application/json;charset=utf-8» forHTTPHeaderField:@"Content-Type»];    [запросить setHTTPBody: [сообщений dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="a8978-157">//Add hello notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="a8978-158">Выполнение hello отправка уведомлений API-интерфейса REST на hello ASP.NET серверной NSURLSessionDataTask * dataTask = [сеанса dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *Ошибка) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) ответа;        Если (ошибка || httpResponse.statusCode! = 200) {NSString* состояние = [stringWithFormat:@"Error NSString состояние для % @: % d\nError: %@\n», pns, httpResponse.statusCode, ошибка];            dispatch_async(dispatch_get_main_queue(), ^ {/ / добавление текста, так как все вызовы 3 PNS также могут быть tooview сведения [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="a8978-158">// Execute hello send notification REST API on hello ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information tooview                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="a8978-159">}];    [dataTask resume]; }</span><span class="sxs-lookup"><span data-stu-id="a8978-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="a8978-160">Обновить действие hello для hello **отправить уведомление** кнопку серверной части ASP.NET hello toouse и отправлять tooany PNS, включаемые к коммутатору.</span><span class="sxs-lookup"><span data-stu-id="a8978-160">Update hello action for hello **Send Notification** button toouse hello ASP.NET backend and send tooany PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="a8978-161">В функции **ViewDidLoad**, добавьте следующий экземпляром RegisterClient tooinstantiate hello hello и задайте hello делегат для текстового поля.</span><span class="sxs-lookup"><span data-stu-id="a8978-161">In function **ViewDidLoad**, add hello following tooinstantiate hello RegisterClient instance and set hello delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="a8978-162">Теперь в **AppDelegate.m**, удалите все содержимое hello hello метода **приложения: didRegisterForPushNotificationWithDeviceToken:** и заменить ее именем hello, убедитесь, что следующие toomake, Здравствуйте, представление контроллер содержит маркер устройства последнюю hello, полученные из APNs.</span><span class="sxs-lookup"><span data-stu-id="a8978-162">Now in **AppDelegate.m**, remove all hello content of hello method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with hello following toomake sure that hello view controller contains hello latest device token retrieved from APNs:</span></span>
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="a8978-163">Finally в **AppDelegate.m**, убедитесь, что у вас есть hello следующий метод:</span><span class="sxs-lookup"><span data-stu-id="a8978-163">Finally in **AppDelegate.m**, make sure you have hello following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a><span data-ttu-id="a8978-164">Hello тестового приложения</span><span class="sxs-lookup"><span data-stu-id="a8978-164">Test hello Application</span></span>
1. <span data-ttu-id="a8978-165">В XCode запустите приложение hello на устройстве физических операций ввода-вывода (push-уведомлений не будет работать в симуляторе hello).</span><span class="sxs-lookup"><span data-stu-id="a8978-165">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="a8978-166">В приложении iOS hello пользовательского интерфейса введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="a8978-166">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="a8978-167">Это может быть любой строкой, но они оба должны быть hello же строковое значение.</span><span class="sxs-lookup"><span data-stu-id="a8978-167">These can be any string, but they must both be hello same string value.</span></span> <span data-ttu-id="a8978-168">Затем нажмите кнопку **Log In**(Войти).</span><span class="sxs-lookup"><span data-stu-id="a8978-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="a8978-169">Должно отобразиться всплывающее окно с сообщением об успешной регистрации.</span><span class="sxs-lookup"><span data-stu-id="a8978-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="a8978-170">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a8978-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="a8978-171">В hello **тег username получателя* текста введите используется вместе с регистрацией hello с другого устройства тег имени пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="a8978-171">In hello **Recipient username tag* text field, enter hello user name tag used with hello registration from another device.</span></span>
5. <span data-ttu-id="a8978-172">Введите сообщение уведомления и нажмите кнопку **Отправить уведомление**.</span><span class="sxs-lookup"><span data-stu-id="a8978-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="a8978-173">Только устройства hello имеет регистрации с тегом имя получателя пользователя hello сообщение hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="a8978-173">Only hello devices that have a registration with hello recipient user name tag receive hello notification message.</span></span>  <span data-ttu-id="a8978-174">Он отправляется только toothose пользователей.</span><span class="sxs-lookup"><span data-stu-id="a8978-174">It is only sent toothose users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
