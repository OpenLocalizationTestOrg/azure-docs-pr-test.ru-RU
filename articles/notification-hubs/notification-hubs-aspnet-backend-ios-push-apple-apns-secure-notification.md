---
title: "Безопасные push-уведомления посредством центров уведомлений Azure"
description: "Узнайте, как отправлять безопасные push-уведомления в приложение iOS из Azure. Примеры кода написаны на Objective-C и C#."
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
ms.openlocfilehash: e5f09fb3716303bb21fe7442aa6fa8832174838e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="23038-104">Безопасные push-уведомления посредством центров уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="23038-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23038-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="23038-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="23038-106">iOS</span><span class="sxs-lookup"><span data-stu-id="23038-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="23038-107">Android</span><span class="sxs-lookup"><span data-stu-id="23038-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="23038-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="23038-108">Overview</span></span>
<span data-ttu-id="23038-109">Поддержка push-уведомлений в Microsoft Azure позволяет получить доступ к простой в использовании, многоплатформенной и масштабируемой инфраструктуре для отправки push-уведомлений, которая значительно упрощает реализацию push-уведомлений как для индивидуальных пользователей, так и для корпоративных приложений для мобильных платформ.</span><span class="sxs-lookup"><span data-stu-id="23038-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="23038-110">Из-за ограничений, связанных с правовыми нормами или обеспечением безопасности, иногда в уведомлении могут присутствовать данные, которые нельзя передать через стандартную инфраструктуру push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="23038-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="23038-111">В этом учебнике рассказывается о том, как реализовать этот принцип при отправке важной информации через защищенное соединение с проверкой подлинности, установленное между устройством клиента и серверной частью приложения.</span><span class="sxs-lookup"><span data-stu-id="23038-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="23038-112">На высоком уровне поток можно представить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="23038-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="23038-113">Серверная часть приложения:</span><span class="sxs-lookup"><span data-stu-id="23038-113">The app back-end:</span></span>
   * <span data-ttu-id="23038-114">Сохраняет полезную нагрузку в базе данных серверной части.</span><span class="sxs-lookup"><span data-stu-id="23038-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="23038-115">Отправляет идентификатор этого уведомления устройству (защищаемые сведения не передаются).</span><span class="sxs-lookup"><span data-stu-id="23038-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="23038-116">Приложение на устройстве при получении уведомления:</span><span class="sxs-lookup"><span data-stu-id="23038-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="23038-117">Устройство связывается с серверной частью и запрашивает полезную нагрузку.</span><span class="sxs-lookup"><span data-stu-id="23038-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="23038-118">Приложение может показывать полезную нагрузку в виде уведомления на устройстве.</span><span class="sxs-lookup"><span data-stu-id="23038-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="23038-119">Стоит отметить: в предыдущем потоке (и в этом учебнике) мы предположили, что устройство сохраняет маркер проверки подлинности в локальном хранилище после входа пользователя.</span><span class="sxs-lookup"><span data-stu-id="23038-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="23038-120">Таким образом обеспечивается удобство работы, так как с помощью этого маркера устройство способно получать безопасные полезные данные уведомлений.</span><span class="sxs-lookup"><span data-stu-id="23038-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="23038-121">Если приложение не сохраняет маркеры проверки подлинности на устройстве, или если истек срок действия маркеров, приложение устройства, после получения уведомления, должно отобразить общее уведомление, предлагая пользователю запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="23038-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="23038-122">Затем приложение выполняет проверку подлинности пользователя и отображает полезную нагрузку уведомления.</span><span class="sxs-lookup"><span data-stu-id="23038-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="23038-123">В этом учебнике по безопасности push-уведомлений показано, как безопасно отправлять push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="23038-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="23038-124">Данное руководство является продолжением другого учебника под названием [Уведомление пользователей](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) , поэтому необходимо сначала выполнить шаги в указанном учебнике.</span><span class="sxs-lookup"><span data-stu-id="23038-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="23038-125">В этом учебнике подразумевается, что вы создали и настроили центр уведомлений, как описано в руководстве [Приступая к работе с центрами уведомлений (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="23038-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-ios-project"></a><span data-ttu-id="23038-126">Внесение изменений в проект iOS</span><span class="sxs-lookup"><span data-stu-id="23038-126">Modify the iOS project</span></span>
<span data-ttu-id="23038-127">После того, как вы изменили серверную часть приложения для отправки только *идентификатора* уведомления, необходимо внести изменения в приложение iOS для обработки этого уведомления и осуществления обратного вызова к серверной части для извлечения конфиденциального сообщения, которое должно быть отображено.</span><span class="sxs-lookup"><span data-stu-id="23038-127">Now that you modified your app back-end to send just the *id* of a notification, you have to change your iOS app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>

<span data-ttu-id="23038-128">Для достижения этой цели мы напишем логику извлечения безопасного содержимого из серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="23038-128">To achieve this goal, we have to write the logic to retrieve the secure content from the app back-end.</span></span>

1. <span data-ttu-id="23038-129">Убедитесь, что в **AppDelegate.m**приложение подписано на получение автоматических уведомлений и обрабатывает отправленный из серверной части идентификатор уведомлений.</span><span class="sxs-lookup"><span data-stu-id="23038-129">In **AppDelegate.m**, make sure the app registers for silent notifications so it processes the notification id sent from the backend.</span></span> <span data-ttu-id="23038-130">Добавьте параметр **UIRemoteNotificationTypeNewsstandContentAvailability** в didFinishLaunchingWithOptions:</span><span class="sxs-lookup"><span data-stu-id="23038-130">Add the **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="23038-131">В файле **AppDelegate.m** добавьте в начало файла реализационную часть со следующим объявлением:</span><span class="sxs-lookup"><span data-stu-id="23038-131">In your **AppDelegate.m** add an implementation section at the top with the following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="23038-132">Затем добавьте в реализационную часть следующий код, заменив заполнитель `{back-end endpoint}` на конечную точку серверной части, которая была получена ранее:</span><span class="sxs-lookup"><span data-stu-id="23038-132">Then add in the implementation section the following code, substituting the placeholder `{back-end endpoint}` with the endpoint for your back-end obtained previously:</span></span>

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

    This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences.

1. <span data-ttu-id="23038-133">Теперь мы обработаем входящее уведомление и используем вышеуказанный метод для извлечения содержимого и его отображения.</span><span class="sxs-lookup"><span data-stu-id="23038-133">Now we have to handle the incoming notification and use the method above to retrieve the content to display.</span></span> <span data-ttu-id="23038-134">Во-первых, мы должны создать для приложения iOS возможность работы в фоновом режиме при получении push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="23038-134">First, we have to enable your iOS app to run in the background when receiving a push notification.</span></span> <span data-ttu-id="23038-135">В **XCode** выберите проект приложения в панели слева, затем выберите основную платформу в разделе **Targets** (Целевые объекты) центральной панели.</span><span class="sxs-lookup"><span data-stu-id="23038-135">In **XCode**, select your app project on the left panel, then click your main app target in the **Targets** section from the central pane.</span></span>
2. <span data-ttu-id="23038-136">Затем щелкните вкладку **Capabilities** (Возможности) в верхней части центральной панели и установите флажок **Remote Notifications** (Удаленные уведомления).</span><span class="sxs-lookup"><span data-stu-id="23038-136">Then click your **Capabilities** tab at the top of your central pane, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="23038-137">В файле **AppDelegate.m** добавьте следующий метод для обработки push-уведомлений:</span><span class="sxs-lookup"><span data-stu-id="23038-137">In **AppDelegate.m** add the following method to handle push notifications:</span></span>
   
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
   
    <span data-ttu-id="23038-138">Обратите внимание, что случаи отсутствующего свойства заголовки проверки подлинности или отклонения предпочтительнее обрабатывать на серверной части.</span><span class="sxs-lookup"><span data-stu-id="23038-138">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="23038-139">Обработка в таких случаях в основном зависит от пользовательского опыта на целевой платформе.</span><span class="sxs-lookup"><span data-stu-id="23038-139">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="23038-140">Одним из вариантов является отображение уведомления с обычным предложением пользователю для проверки подлинности, чтобы получить текущее уведомление.</span><span class="sxs-lookup"><span data-stu-id="23038-140">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="23038-141">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="23038-141">Run the Application</span></span>
<span data-ttu-id="23038-142">Для запуска приложения выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="23038-142">To run the application, do the following:</span></span>

1. <span data-ttu-id="23038-143">В XCode запустите приложение на физическом устройстве под управлением iOS (push-уведомления не будут работать в симуляторе).</span><span class="sxs-lookup"><span data-stu-id="23038-143">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="23038-144">В пользовательском интерфейсе приложения iOS введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="23038-144">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="23038-145">Это могут быть любые совпадающие строки.</span><span class="sxs-lookup"><span data-stu-id="23038-145">These can be any string, but they must be the same value.</span></span>
3. <span data-ttu-id="23038-146">В пользовательском интерфейсе приложения iOS нажмите **Вход**.</span><span class="sxs-lookup"><span data-stu-id="23038-146">In the iOS app UI, click **Log in**.</span></span> <span data-ttu-id="23038-147">Затем нажмите **Отправить push-уведомление**.</span><span class="sxs-lookup"><span data-stu-id="23038-147">Then click **Send push**.</span></span> <span data-ttu-id="23038-148">Вы должны увидеть конфиденциальное уведомление, которое будет отображено в центре уведомлений.</span><span class="sxs-lookup"><span data-stu-id="23038-148">You should see the secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
