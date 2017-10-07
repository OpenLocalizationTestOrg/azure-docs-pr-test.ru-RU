---
title: "текущий пользователь aaaRegister hello push-уведомления с помощью веб-API | Документы Microsoft"
description: "Узнайте, как toorequest зарегистрировать push-уведомлений в приложения iOS с концентраторами уведомлений Azure при регистрации выполняется с веб-API ASP.NET."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f859feb436093e703d7e1db38354dd356fff8efe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="a19be-103">Зарегистрируйте hello текущего пользователя для push-уведомлений с помощью ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a19be-103">Register hello current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a19be-104">iOS</span><span class="sxs-lookup"><span data-stu-id="a19be-104">iOS</span></span>](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a19be-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="a19be-105">Overview</span></span>
<span data-ttu-id="a19be-106">В этом разделе показано, как toorequest зарегистрировать push-уведомлений с концентраторами уведомлений Azure при выполнении в ASP.NET Web API регистрации.</span><span class="sxs-lookup"><span data-stu-id="a19be-106">This topic shows you how toorequest push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="a19be-107">В этом разделе расширяет hello учебника [уведомить пользователей с концентраторами уведомлений].</span><span class="sxs-lookup"><span data-stu-id="a19be-107">This topic extends hello tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="a19be-108">Вы должны уже выполнили hello необходимые действия, описанные в этой мобильной службы учебника toocreate hello с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="a19be-108">You must have already completed hello required steps in that tutorial toocreate hello authenticated mobile service.</span></span> <span data-ttu-id="a19be-109">Дополнительные сведения о hello уведомить пользователей сценарии, см. в разделе [уведомить пользователей с концентраторами уведомлений].</span><span class="sxs-lookup"><span data-stu-id="a19be-109">For more information on hello notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="a19be-110">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="a19be-110">Update your app</span></span>
1. <span data-ttu-id="a19be-111">Добавьте в ваш MainStoryboard_iPhone.storyboard hello следующие компоненты из библиотеки hello объекта.</span><span class="sxs-lookup"><span data-stu-id="a19be-111">In your MainStoryboard_iPhone.storyboard, add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="a19be-112">**Метка**: «Push-tooUser с концентраторами уведомлений»</span><span class="sxs-lookup"><span data-stu-id="a19be-112">**Label**: "Push tooUser with Notification Hubs"</span></span>
   * <span data-ttu-id="a19be-113">**Метка**: «InstallationId»</span><span class="sxs-lookup"><span data-stu-id="a19be-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="a19be-114">**Метка**: «Пользователь»</span><span class="sxs-lookup"><span data-stu-id="a19be-114">**Label**: "User"</span></span>
   * <span data-ttu-id="a19be-115">**Текстовое поле**: «Пользователь»</span><span class="sxs-lookup"><span data-stu-id="a19be-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="a19be-116">**Метка**: «Пароль»</span><span class="sxs-lookup"><span data-stu-id="a19be-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="a19be-117">**Текстовое поле**: «Пароль»</span><span class="sxs-lookup"><span data-stu-id="a19be-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="a19be-118">**Кнопка**: «Вход»</span><span class="sxs-lookup"><span data-stu-id="a19be-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="a19be-119">На этом этапе раскадровки выглядит hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a19be-119">At this point, your storyboard looks like hello following:</span></span>
     
      ![][0]
2. <span data-ttu-id="a19be-120">В редакторе помощника hello, создания выходов для всех элементов управления переключить hello и их вызова, соединение hello текстовые поля с hello View-Controller (делегат) и создайте **действия** для hello **входа** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a19be-120">In hello assistant editor, create outlets for all hello switched controls and call them, connect hello text fields with hello View Controller (delegate), and create an **Action** for hello **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="a19be-121">Создайте класс с именем **DeviceInfo**, и копировать hello после кода в раздел интерфейс hello hello файла DeviceInfo.h:</span><span class="sxs-lookup"><span data-stu-id="a19be-121">Create a class named **DeviceInfo**, and copy hello following code into hello interface section of hello file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="a19be-122">Скопируйте следующий код в разделе реализации hello файла DeviceInfo.m hello hello:</span><span class="sxs-lookup"><span data-stu-id="a19be-122">Copy hello following code in hello implementation section of hello DeviceInfo.m file:</span></span>
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store hello install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. <span data-ttu-id="a19be-123">В PushToUserAppDelegate.h добавьте следующие свойства одноэлементный hello.</span><span class="sxs-lookup"><span data-stu-id="a19be-123">In PushToUserAppDelegate.h, add hello following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="a19be-124">В hello **didFinishLaunchingWithOptions** метод в PushToUserAppDelegate.m, добавить hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="a19be-124">In hello **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add hello following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="a19be-125">Первая строка Hello инициализирует hello **DeviceInfo** singleton.</span><span class="sxs-lookup"><span data-stu-id="a19be-125">hello first line initializes hello **DeviceInfo** singleton.</span></span> <span data-ttu-id="a19be-126">Hello второй строки начинается hello регистрации для push-уведомления, которая уже присутствует — вы уже выполнили hello [начало работы с концентраторами уведомлений] учебника.</span><span class="sxs-lookup"><span data-stu-id="a19be-126">hello second line starts hello registration for push notifications, which is already present is you have already completed hello [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="a19be-127">В PushToUserAppDelegate.m, реализуйте метод hello **didRegisterForRemoteNotificationsWithDeviceToken** в ваш AppDelegate и добавить hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="a19be-127">In PushToUserAppDelegate.m, implement hello method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add hello following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="a19be-128">Таким образом задается hello маркер устройства для запроса hello.</span><span class="sxs-lookup"><span data-stu-id="a19be-128">This sets hello device token for hello request.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a19be-129">На этом этапе в методе не должно быть никакого другого кода.</span><span class="sxs-lookup"><span data-stu-id="a19be-129">At this point, there should not be any other code in this method.</span></span> <span data-ttu-id="a19be-130">Если у вас уже есть toohello вызов **registerNativeWithDeviceToken** метода, который был добавлен после завершения hello [начало работы с концентраторами уведомлений](/manage/services/notification-hubs/get-started-notification-hubs-ios/) учебника, необходимо масштабирование комментарий или удалить, вызов.</span><span class="sxs-lookup"><span data-stu-id="a19be-130">If you already have a call toohello **registerNativeWithDeviceToken** method that was added when you completed hello [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.</span></span>
   > 
   > 
8. <span data-ttu-id="a19be-131">Добавьте следующий метод обработчика hello hello PushToUserAppDelegate.m файла:</span><span class="sxs-lookup"><span data-stu-id="a19be-131">In hello PushToUserAppDelegate.m file, add hello following handler method:</span></span>
   
   * <span data-ttu-id="a19be-132">(void) приложения:(UIApplication *) приложения didReceiveRemoteNotification:(NSDictionary *) userInfo {NSLog (@"% @", сведений о пользователях);   UIAlertView * предупреждение = [[UIAlertView alloc] initWithTitle:@"Notification» сообщение: cancelButtonTitle делегата: nil [userInfo objectForKey:@"inAppMessage]»: @ otherButtonTitles:nil «ОК», nil];   [Показать предупреждения]; }</span><span class="sxs-lookup"><span data-stu-id="a19be-132">(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="a19be-133">Этот метод отображает предупреждение в hello пользовательского интерфейса, когда приложение получает уведомления при выполнении.</span><span class="sxs-lookup"><span data-stu-id="a19be-133">This method displays an alert in hello UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="a19be-134">Откройте файл PushToUserViewController.m hello и возврата hello клавиатуры в hello после реализации:</span><span class="sxs-lookup"><span data-stu-id="a19be-134">Open hello PushToUserViewController.m file, and return hello keyboard in hello following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="a19be-135">В hello **viewDidLoad** метод в файле PushToUserViewController.m hello, инициализировать hello installationId метку следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a19be-135">In hello **viewDidLoad** method in hello PushToUserViewController.m file, initialize hello installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="a19be-136">Добавьте следующие свойства в интерфейсе в PushToUserViewController.m hello:</span><span class="sxs-lookup"><span data-stu-id="a19be-136">Add hello following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="a19be-137">Затем добавьте следующие реализации hello:</span><span class="sxs-lookup"><span data-stu-id="a19be-137">Then, add hello following implementation:</span></span>
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. <span data-ttu-id="a19be-138">Копирования hello следующий код в hello **входа** метод обработчика, созданные XCode:</span><span class="sxs-lookup"><span data-stu-id="a19be-138">Copy hello following code into hello **login** handler method created by XCode:</span></span>
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    <span data-ttu-id="a19be-139">Этот метод возвращает идентификатор установки и каналов уведомлений и отправляет его, а также типа устройства hello, toohello проверку подлинности метод веб-API, который создает регистрацию в концентраторах уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a19be-139">This method gets both an installation ID and channel for push notifications and sends it, along with hello device type, toohello authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="a19be-140">Этот веб-API был определен в учебнике [уведомить пользователей с концентраторами уведомлений].</span><span class="sxs-lookup"><span data-stu-id="a19be-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="a19be-141">Теперь, когда hello клиентское приложение будет обновлен, возвращают toohello [уведомить пользователей с концентраторами уведомлений] и обновлять уведомления toosend hello мобильной службы с помощью концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a19be-141">Now that hello client app has been updated, return toohello [Notify users with Notification Hubs] and update hello mobile service toosend notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[уведомить пользователей с концентраторами уведомлений]: /manage/services/notification-hubs/notify-users-aspnet

[начало работы с концентраторами уведомлений]: /manage/services/notification-hubs/get-started-notification-hubs-ios
