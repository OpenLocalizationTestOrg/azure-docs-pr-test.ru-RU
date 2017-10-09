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
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="c8e24-104">Безопасные push-уведомления посредством центров уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="c8e24-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8e24-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="c8e24-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="c8e24-106">iOS</span><span class="sxs-lookup"><span data-stu-id="c8e24-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="c8e24-107">Android</span><span class="sxs-lookup"><span data-stu-id="c8e24-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c8e24-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="c8e24-108">Overview</span></span>
<span data-ttu-id="c8e24-109">Поддержка уведомлений Push в Microsoft Azure позволяет tooaccess к использованию, несколькими платформами, масштабируемых push-инфраструктуру, которая значительно упрощает реализацию hello push-уведомлений для индивидуальных пользователей и корпоративных приложений для мобильных устройств платформы.</span><span class="sxs-lookup"><span data-stu-id="c8e24-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="c8e24-110">Иногда из-за ограничений tooregulatory или безопасности, приложение может возникнуть tooinclude что-нибудь в hello уведомление, которое не может передаваться через инфраструктуру hello Стандартная push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="c8e24-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="c8e24-111">В данном учебнике как tooachieve hello такие же возможности, отправляя конфиденциальных данных через проверку подлинности безопасное соединение между hello клиентского устройства и внутреннего сервера приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c8e24-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="c8e24-112">На высоком уровне hello поток выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c8e24-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="c8e24-113">Hello приложения внутреннего интерфейса:</span><span class="sxs-lookup"><span data-stu-id="c8e24-113">hello app back-end:</span></span>
   * <span data-ttu-id="c8e24-114">Сохраняет полезную нагрузку в базе данных серверной части.</span><span class="sxs-lookup"><span data-stu-id="c8e24-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="c8e24-115">Отправляет идентификатор hello toohello устройства создания уведомления (отправляются без защиты данных).</span><span class="sxs-lookup"><span data-stu-id="c8e24-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="c8e24-116">приложение Hello на устройстве hello, при получении уведомления hello:</span><span class="sxs-lookup"><span data-stu-id="c8e24-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="c8e24-117">устройство Hello обращается hello серверной части запроса hello безопасного полезных данных.</span><span class="sxs-lookup"><span data-stu-id="c8e24-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="c8e24-118">приложение Hello можно показать hello полезных данных в виде уведомлений на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="c8e24-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="c8e24-119">Очень важно, toonote, что предшествующий потока hello (и в этом учебнике) предполагается устройства hello склада маркер проверки подлинности в локальном хранилище после hello пользователь вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="c8e24-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="c8e24-120">Это гарантирует полностью эффективной работы, как hello устройства можно получить полезные данные безопасного hello уведомления, с помощью этого токена.</span><span class="sxs-lookup"><span data-stu-id="c8e24-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="c8e24-121">Если приложение не хранить токены проверки подлинности на устройстве hello или может быть просрочен эти токены, hello приложения для устройств, при получении уведомления hello отображать универсального уведомление запроса приложение hello toolaunch hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="c8e24-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="c8e24-122">Затем приложение Hello проверяет подлинность пользователя hello и приводятся полезные данные уведомления hello.</span><span class="sxs-lookup"><span data-stu-id="c8e24-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="c8e24-123">В этом учебнике принудительной защиты как toosend push-уведомление безопасно.</span><span class="sxs-lookup"><span data-stu-id="c8e24-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="c8e24-124">Hello учебник построен на hello [уведомить пользователей](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) учебник, поэтому hello шаги в этом учебнике должна выполнять первой.</span><span class="sxs-lookup"><span data-stu-id="c8e24-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="c8e24-125">В этом учебнике подразумевается, что вы создали и настроили центр уведомлений, как описано в руководстве [Приступая к работе с центрами уведомлений (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c8e24-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a><span data-ttu-id="c8e24-126">Изменение проекта iOS hello</span><span class="sxs-lookup"><span data-stu-id="c8e24-126">Modify hello iOS project</span></span>
<span data-ttu-id="c8e24-127">Теперь, когда вы изменили вашей hello просто toosend серверной части приложения *идентификатор* уведомления, у вас есть toochange вашей toohandle приложения iOS, уведомления и обратный вызов к серверной части tooretrieve hello защитить toobe сообщений отображается.</span><span class="sxs-lookup"><span data-stu-id="c8e24-127">Now that you modified your app back-end toosend just hello *id* of a notification, you have toochange your iOS app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>

<span data-ttu-id="c8e24-128">tooachieve этой цели, у нас есть toowrite hello логику tooretrieve hello защищенное содержимое из hello серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="c8e24-128">tooachieve this goal, we have toowrite hello logic tooretrieve hello secure content from hello app back-end.</span></span>

1. <span data-ttu-id="c8e24-129">В **AppDelegate.m**, сделайте убедиться, что регистры приложения hello для автоматической уведомления, чтобы он обрабатывает hello идентификатор уведомления, отправленные hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="c8e24-129">In **AppDelegate.m**, make sure hello app registers for silent notifications so it processes hello notification id sent from hello backend.</span></span> <span data-ttu-id="c8e24-130">Добавить hello **UIRemoteNotificationTypeNewsstandContentAvailability** параметр в didFinishLaunchingWithOptions:</span><span class="sxs-lookup"><span data-stu-id="c8e24-130">Add hello **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="c8e24-131">В вашей **AppDelegate.m** к добавлению раздела реализации вверху hello с объявления hello:</span><span class="sxs-lookup"><span data-stu-id="c8e24-131">In your **AppDelegate.m** add an implementation section at hello top with hello following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="c8e24-132">Затем добавьте в hello реализации раздел hello после кода, заменив заполнитель hello `{back-end endpoint}` с конечной точкой hello для настройки сервера был получен:</span><span class="sxs-lookup"><span data-stu-id="c8e24-132">Then add in hello implementation section hello following code, substituting hello placeholder `{back-end endpoint}` with hello endpoint for your back-end obtained previously:</span></span>

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

1. <span data-ttu-id="c8e24-133">Теперь мы toohandle hello входящие уведомления и использовать метод hello выше содержимого toodisplay tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="c8e24-133">Now we have toohandle hello incoming notification and use hello method above tooretrieve hello content toodisplay.</span></span> <span data-ttu-id="c8e24-134">Во-первых у нас есть tooenable вашей toorun приложения iOS в фоновом режиме hello при получении push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="c8e24-134">First, we have tooenable your iOS app toorun in hello background when receiving a push notification.</span></span> <span data-ttu-id="c8e24-135">В **XCode**, выберите проект приложения на левой панели hello, а затем выберите целевую основным приложением в hello **цели** раздел из центральной панели hello.</span><span class="sxs-lookup"><span data-stu-id="c8e24-135">In **XCode**, select your app project on hello left panel, then click your main app target in hello **Targets** section from hello central pane.</span></span>
2. <span data-ttu-id="c8e24-136">Нажмите кнопку вашей **возможности** вверху hello на центральной панели и проверьте hello **удаленного уведомления** флажок.</span><span class="sxs-lookup"><span data-stu-id="c8e24-136">Then click your **Capabilities** tab at hello top of your central pane, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="c8e24-137">В **AppDelegate.m** добавьте следующий метод toohandle извещающих уведомлений hello:</span><span class="sxs-lookup"><span data-stu-id="c8e24-137">In **AppDelegate.m** add hello following method toohandle push notifications:</span></span>
   
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
   
    <span data-ttu-id="c8e24-138">Обратите внимание, что он является более предпочтительным, чем toohandle случаях hello отсутствующее свойство Заголовок проверки подлинности или отклонение с помощью серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="c8e24-138">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="c8e24-139">Hello конкретных обработки этих вариантов основном зависят от вам целевой.</span><span class="sxs-lookup"><span data-stu-id="c8e24-139">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="c8e24-140">Один из вариантов — toodisplay уведомление с универсальным запрашивать hello tooauthenticate tooretrieve hello фактическое уведомление для пользователей.</span><span class="sxs-lookup"><span data-stu-id="c8e24-140">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="c8e24-141">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="c8e24-141">Run hello Application</span></span>
<span data-ttu-id="c8e24-142">toorun Здравствуйте, приложения, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="c8e24-142">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="c8e24-143">В XCode запустите приложение hello на устройстве физических операций ввода-вывода (push-уведомлений не будет работать в симуляторе hello).</span><span class="sxs-lookup"><span data-stu-id="c8e24-143">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="c8e24-144">В приложении iOS hello пользовательского интерфейса введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="c8e24-144">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="c8e24-145">Это может быть любой строкой, но они должны быть hello одинаковое значение.</span><span class="sxs-lookup"><span data-stu-id="c8e24-145">These can be any string, but they must be hello same value.</span></span>
3. <span data-ttu-id="c8e24-146">В приложении iOS hello пользовательского интерфейса, нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="c8e24-146">In hello iOS app UI, click **Log in**.</span></span> <span data-ttu-id="c8e24-147">Затем нажмите **Отправить push-уведомление**.</span><span class="sxs-lookup"><span data-stu-id="c8e24-147">Then click **Send push**.</span></span> <span data-ttu-id="c8e24-148">Вы увидите hello безопасных уведомлений, отображаемых в свой центр уведомлений.</span><span class="sxs-lookup"><span data-stu-id="c8e24-148">You should see hello secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
