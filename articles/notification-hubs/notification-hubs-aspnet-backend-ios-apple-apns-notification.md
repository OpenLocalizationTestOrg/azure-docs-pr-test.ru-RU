---
title: "Уведомление пользователей iOS через центры уведомлений с помощью серверной части .NET"
description: "Узнайте, как отправлять push-уведомления пользователям в Azure. Примеры кода написаны на Objective-C с использованием API .NET для серверной части."
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
ms.openlocfilehash: 0fa7a886e1ecb0a90b6aebc1dbf9ef0c6ce1acf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="ea0e0-104">Уведомление пользователей iOS через центры уведомлений с помощью серверной части .NET</span><span class="sxs-lookup"><span data-stu-id="ea0e0-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="ea0e0-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="ea0e0-105">Overview</span></span>
<span data-ttu-id="ea0e0-106">Поддержка push-уведомлений в Azure позволяет получить доступ к простой в использовании, многоплатформенной и масштабируемой инфраструктуре для отправки push-уведомлений, которая значительно упрощает реализацию push-уведомлений как для индивидуальных пользователей, так и для корпоративных приложений для мобильных платформ.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="ea0e0-107">В этом учебнике показано, как использовать концентраторы уведомлений Azure для отправки push-уведомлений пользователю определенного приложения на конкретном устройстве.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="ea0e0-108">Серверная часть ASP.NET WebAPI используется для проверки подлинности клиентов и создания уведомлений, как показано в разделе руководства [Управление регистрацией из серверной части](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="ea0e0-108">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="ea0e0-109">В этом учебнике подразумевается, что вы создали и настроили центр уведомлений, как описано в руководстве [Приступая к работе с центрами уведомлений (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ea0e0-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="ea0e0-110">Это руководство также необходимо изучить перед переходом к руководству [Безопасные push-уведомления для концентраторов уведомлений Azure](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md).</span><span class="sxs-lookup"><span data-stu-id="ea0e0-110">This tutorial is also the prerequisite to the [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="ea0e0-111">Если вы хотите использовать мобильные приложения в качестве внутренней службы, см. статью [Добавление push-уведомлений в приложение iOS](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="ea0e0-111">If you want to use Mobile Apps as your backend service, see the [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="ea0e0-112">Изменение приложения iOS</span><span class="sxs-lookup"><span data-stu-id="ea0e0-112">Modify your iOS app</span></span>
1. <span data-ttu-id="ea0e0-113">Откройте в одностраничном режиме просмотра приложение, которое вы создали с помощью руководства [Приступая к работе с центрами уведомлений (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="ea0e0-113">Open the Single Page view app you created in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ea0e0-114">В этом разделе подразумевается, что вы настроили свой проект, указав пустое имя организации.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="ea0e0-115">Если вы этого не сделали, вам нужно будет добавлять имя своей организации перед всеми именами классов.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-115">If not, you will need to prepend your organization name to all class names.</span></span>
   > 
   > 
2. <span data-ttu-id="ea0e0-116">В своем Main.storyboard добавьте компоненты из библиотеки объектов, показанные на снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-116">In your Main.storyboard add the components shown in the screenshot below from the object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="ea0e0-117">**Имя пользователя**: текстовое поле UITextField с замещающим текстом *Enter Username*, расположенное под меткой отправки результатов, справа, слева и сверху ограниченное полями.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath the send results label and constrained to the left and right margins and beneath the send results label.</span></span>
   * <span data-ttu-id="ea0e0-118">**Пароль**: текстовое поле UITextField с замещающим текстом *Enter Password*, расположенное под текстовым полем имени пользователя, справа, слева и сверху ограниченное полями.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath the username text field and constrained to the left and right margins and beneath the username text field.</span></span> <span data-ttu-id="ea0e0-119">Отметьте параметр **Защищенный ввод текста** в инспекторе атрибутов в разделе *Символ вывода*.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-119">Check the **Secure Text Entry** option in the Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="ea0e0-120">**Вход**: кнопка UIButton с меткой, которая расположена под текстовым полем пароля. Снимите флажок **Включить** в инспекторе атрибутов в разделе *Управление содержимым*.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-120">**Log in**: A UIButton labeled immediately beneath the password text field and uncheck the **Enabled** option in the Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="ea0e0-121">**WNS**: метка и переключатель для включения отправки уведомлений службы уведомлений Windows, если она установлена на концентраторе.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-121">**WNS**: Label and switch to enable sending the notification Windows Notification Service if it has been setup on the hub.</span></span> <span data-ttu-id="ea0e0-122">См. руководство [Начало работы с центрами уведомлений для приложений универсальной платформы Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="ea0e0-122">See the [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="ea0e0-123">**GCM**: метка и переключатель для включения отправки уведомлений в службу Google Cloud Messaging, если она установлена в концентраторе.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-123">**GCM**: Label and switch to enable sending the notification to Google Cloud Messaging if it has been setup on the hub.</span></span> <span data-ttu-id="ea0e0-124">См. руководство [Отправка push-уведомлений в приложения Android с помощью центров уведомлений Azure](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ea0e0-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="ea0e0-125">**APNS**: метка и переключатель для включения отправки уведомлений в службу уведомлений платформы Apple Platform Notification Service.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-125">**APNS**: Label and switch to enable sending the notification to the Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="ea0e0-126">**Имя получателя**: текстовое поле UITextField с замещающим текстом *Введите имя получателя*, расположенное непосредственно под меткой GCM, справа, слева и сверху ограниченное полями.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath the GCM label and constrained to the left and right margins and beneath the GCM label.</span></span>

    <span data-ttu-id="ea0e0-127">Подробнее о добавлении некоторых компонентов см. в руководстве [Отправка push-уведомлений с помощью центров уведомлений Azure в iOS](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ea0e0-127">Some components were added in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="ea0e0-128">**Ctrl** , перетащите компоненты из представления в файл ViewController.h и добавьте эти новые элементы.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-128">**Ctrl** drag from the components in the view to ViewController.h and add these new outlets.</span></span>
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used to enable the buttons on the UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used to enabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. <span data-ttu-id="ea0e0-129">В ViewController.h добавьте `#define` после операторов импорта.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-129">In ViewController.h, add the following `#define` just below your import statements.</span></span> <span data-ttu-id="ea0e0-130">Замените заполнитель *<Enter Your Backend Endpoint>\>* URL-адресом назначения, который использовался для развертывания серверной части приложения в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-130">Substitute the *<Enter Your Backend Endpoint\>* placeholder with the Destination URL you used to deploy your app backend in the previous section.</span></span> <span data-ttu-id="ea0e0-131">Например, *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="ea0e0-132">В проекте создайте класс **Cocoa Touch class** с именем **RegisterClient** для взаимодействия с серверной частью ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** to interface with the ASP.NET back-end you created.</span></span> <span data-ttu-id="ea0e0-133">Создайте класс, наследующий `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-133">Create the class inheriting from `NSObject`.</span></span> <span data-ttu-id="ea0e0-134">Затем добавьте следующий код в раздел RegisterClient.h:</span><span class="sxs-lookup"><span data-stu-id="ea0e0-134">Then add the following code in the RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="ea0e0-135">В RegisterClient.m обновите раздел `@interface` .</span><span class="sxs-lookup"><span data-stu-id="ea0e0-135">In the RegisterClient.m update the `@interface` section:</span></span>
   
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
5. <span data-ttu-id="ea0e0-136">Замените раздел `@implementation` RegisterClient.m следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-136">Replace the `@implementation` section in the RegisterClient.m with the following code.</span></span>

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

    <span data-ttu-id="ea0e0-137">В коде, указанном выше, реализуется логика, описываемая в статье [Регистрация из серверной части приложения](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) , при этом используется NSURLSession для выполнения вызовов REST в серверную часть приложения, и NSUserDefaults для локального сохранения идентификатора registrationId, возвращаемого концентратором уведомлений.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-137">The code above implements the logic explained in the guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession to perform REST calls to your app backend, and NSUserDefaults to locally store the registrationId returned by the notification hub.</span></span>

    <span data-ttu-id="ea0e0-138">Обратите внимание, что для нормальной работы этого класса должно быть правильно задано свойство **authorizationHeader** .</span><span class="sxs-lookup"><span data-stu-id="ea0e0-138">Note that this class requires its property **authorizationHeader** to be set in order to work properly.</span></span> <span data-ttu-id="ea0e0-139">Это свойство может быть установлено классом **ViewController** после выполнения входа.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-139">This property is set by the **ViewController** class after the log in.</span></span>

1. <span data-ttu-id="ea0e0-140">В ViewController.h добавьте оператор `#import` для RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="ea0e0-141">Затем добавьте объявление для токена устройства и ссылку на экземпляр `RegisterClient` в разделе `@interface`.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-141">Then add a declaration for the device token and reference to a `RegisterClient` instance in the `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="ea0e0-142">Добавьте в ViewController.m объявление частного метода в разделе `@interface` .</span><span class="sxs-lookup"><span data-stu-id="ea0e0-142">In ViewController.m, add a private method declaration in the `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create the Authorization header to perform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="ea0e0-143">Этот фрагмент не является безопасной схемой проверки подлинности. Следует заменить реализацию **createAndSetAuthenticationHeaderWithUsername:AndPassword:** своим собственным механизмом проверки подлинности, формирующим маркер проверки подлинности, используемый классом клиента register, например OAuth, Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-143">The following snippet is not a secure authentication scheme, you should substitute the implementation of the **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token to be consumed by the register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="ea0e0-144">Затем в разделе `@implementation` ViewController.m добавьте приведенный ниже код, который задает токен и заголовок проверки подлинности устройства.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-144">Then in the `@implementation` section of ViewController.m add the following code which adds the implementation for setting the device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="ea0e0-145">Обратите внимание, как при задании токена устройства активируется кнопка входа.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-145">Note how setting the device token enables the log in button.</span></span> <span data-ttu-id="ea0e0-146">Это происходит по той причине, что контроллер представления, являясь частью действия входа, регистрирует push-уведомления в серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-146">This is becasue as a part of the login action, the view controller registers for push notifications with the app backend.</span></span> <span data-ttu-id="ea0e0-147">Таким образом, действие «Вход» должно быть недоступно, пока токен устройства не будет настроен должным образом.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-147">Hence, we do not want Log In action to be accessible till the device token has been properly set up.</span></span> <span data-ttu-id="ea0e0-148">Можно разъединить вход и push-регистрацию, если первая операция выполняется раньше второй.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-148">You can decouple the log in from the push registration as long as the former happens before the latter.</span></span>
2. <span data-ttu-id="ea0e0-149">Чтобы в ViewController.m реализовать метод действия для кнопки **Вход** и метод отправки сообщений уведомления с помощью серверной части ASP.NET, используйте следующие фрагменты кода.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-149">In ViewController.m, use the following snippets to implement the action method for your **Log In** button and a method to send the notification message using the ASP.NET backend.</span></span>
   
       - <span data-ttu-id="ea0e0-150">(IBAction) LogInAction: отправителя (id) {/ / создать заголовок проверки подлинности и установите его в клиент регистра NSString * имя пользователя = self. UsernameField.text;   Пароль NSString * = self. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="ea0e0-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="ea0e0-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="ea0e0-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="ea0e0-152">__weak ViewController * selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken теги: nil andCompletion:^(NSError* error) {Если (! ошибка) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success» message:@"Registered успешно! "];});}}];}</span><span class="sxs-lookup"><span data-stu-id="ea0e0-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="ea0e0-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="ea0e0-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="ea0e0-154">Передайте тег pns и имя пользователя в качестве параметров URL-адрес REST серверной части ASP.NET NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @», BACKEND_ENDPOINT pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="ea0e0-154">// Pass the pns and username tag as parameters with the REST URL to the ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="ea0e0-155">Запрос NSMutableURLRequest * = [NSMutableURLRequest requestWithURL:requestURL];    [запрос setHTTPMethod:@"POST»];</span><span class="sxs-lookup"><span data-stu-id="ea0e0-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="ea0e0-156">Получить макетов authenticationheader от клиента регистра NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @», self.registerClient.authenticationHeader];    [запрос setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization»];</span><span class="sxs-lookup"><span data-stu-id="ea0e0-156">// Get the mock authenticationheader from the register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="ea0e0-157">Добавьте текст сообщения уведомления [запрос setValue:@"application/json;charset=utf-8» forHTTPHeaderField:@"Content-Type»];    [запросить setHTTPBody: [сообщений dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="ea0e0-157">//Add the notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="ea0e0-158">Выполнить API-интерфейса REST отправить уведомление на dataTask NSURLSessionDataTask серверной части ASP.NET * = [сеанса dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *Ошибка) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) ответа;        Если (ошибка || httpResponse.statusCode! = 200) {NSString* состояние = [stringWithFormat:@"Error NSString состояние для % @: % d\nError: %@\n», pns, httpResponse.statusCode, ошибка];            dispatch_async(dispatch_get_main_queue(), ^ {/ / добавление текста, поскольку все вызовы 3 PNS также могут иметь информацию, представление [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="ea0e0-158">// Execute the send notification REST API on the ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information to view                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="ea0e0-159">}];    [dataTask resume]; }</span><span class="sxs-lookup"><span data-stu-id="ea0e0-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="ea0e0-160">Обновите действие для кнопки **Отправить уведомление** для использования серверной части ASP.NET и отправки любой PNS, разрешенной коммутатором.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-160">Update the action for the **Send Notification** button to use the ASP.NET backend and send to any PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="ea0e0-161">В функции **ViewDidLoad**введите следующий код, чтобы создать экземпляр RegisterClient и задать делегат для текстовых полей.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-161">In function **ViewDidLoad**, add the following to instantiate the RegisterClient instance and set the delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="ea0e0-162">Теперь удалите в **AppDelegate.m** все содержимое метода **application:didRegisterForPushNotificationWithDeviceToken:** и замените его следующим содержимым, чтобы контроллер представления содержал последний токен устройства, полученный из элементов APN:</span><span class="sxs-lookup"><span data-stu-id="ea0e0-162">Now in **AppDelegate.m**, remove all the content of the method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with the following to make sure that the view controller contains the latest device token retrieved from APNs:</span></span>
   
       // Add import to the top of the file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="ea0e0-163">Наконец, убедитесь, что в **AppDelegate.m**есть следующий метод:</span><span class="sxs-lookup"><span data-stu-id="ea0e0-163">Finally in **AppDelegate.m**, make sure you have the following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-the-application"></a><span data-ttu-id="ea0e0-164">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="ea0e0-164">Test the Application</span></span>
1. <span data-ttu-id="ea0e0-165">В XCode запустите приложение на физическом устройстве под управлением iOS (push-уведомления не будут работать в симуляторе).</span><span class="sxs-lookup"><span data-stu-id="ea0e0-165">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="ea0e0-166">В пользовательском интерфейсе приложения iOS введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-166">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="ea0e0-167">Это может быть любая строка, но имя и пароль должны быть одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-167">These can be any string, but they must both be the same string value.</span></span> <span data-ttu-id="ea0e0-168">Затем нажмите кнопку **Log In**(Войти).</span><span class="sxs-lookup"><span data-stu-id="ea0e0-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="ea0e0-169">Должно отобразиться всплывающее окно с сообщением об успешной регистрации.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="ea0e0-170">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="ea0e0-171">В текстовом поле*Тег имени получателя* введите тег имени получателя, используемый при регистрации с другого устройства.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-171">In the **Recipient username tag* text field, enter the user name tag used with the registration from another device.</span></span>
5. <span data-ttu-id="ea0e0-172">Введите сообщение уведомления и нажмите кнопку **Отправить уведомление**.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="ea0e0-173">Сообщения уведомления могут получать только устройства с зарегистрированным тегом имени получателя.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-173">Only the devices that have a registration with the recipient user name tag receive the notification message.</span></span>  <span data-ttu-id="ea0e0-174">Сообщения отправляются только таким пользователям.</span><span class="sxs-lookup"><span data-stu-id="ea0e0-174">It is only sent to those users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
