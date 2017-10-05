---
title: "Передача локализованных экстренных новостей на устройства iOS с помощью центров уведомлений"
description: "Узнайте, как использовать центры уведомлений Azure Service Bus для отправки уведомлений о локализованных экстренных новостях (iOS)."
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
ms.openlocfilehash: fd2b7d9dfd4f432bbcbaa3ed76f8bec0b9677e17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-localized-breaking-news-to-ios-devices"></a><span data-ttu-id="9fd7a-103">Использование концентраторов уведомлений для вещания локализованных экстренных новостей на устройства iOS</span><span class="sxs-lookup"><span data-stu-id="9fd7a-103">Use Notification Hubs to send localized breaking news to iOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9fd7a-104">C# в Магазине Windows</span><span class="sxs-lookup"><span data-stu-id="9fd7a-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="9fd7a-105">iOS</span><span class="sxs-lookup"><span data-stu-id="9fd7a-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9fd7a-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="9fd7a-106">Overview</span></span>
<span data-ttu-id="9fd7a-107">В этом разделе показано, как использовать функцию [шаблонов](notification-hubs-templates-cross-platform-push-messages.md) центров уведомлений Azure для рассылки уведомлений об экстренных новостях, локализованных для языка и устройства.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-107">This topic shows you how to use the [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="9fd7a-108">В этом учебнике вы начнете с приложения iOS, созданного в учебнике [Использование концентраторов уведомлений для передачи экстренных новостей].</span><span class="sxs-lookup"><span data-stu-id="9fd7a-108">In this tutorial you start with the iOS app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="9fd7a-109">По завершении вы сможете регистрировать для категорий, которые вас интересуют, указывать язык уведомлений, и получать push-уведомления только для выбранных категорий на этом языке.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="9fd7a-110">Этот сценарий состоит из двух частей:</span><span class="sxs-lookup"><span data-stu-id="9fd7a-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="9fd7a-111">приложение iOS позволяет клиентским устройствам указывать язык и подписываться на различные категории экстренных новостей;</span><span class="sxs-lookup"><span data-stu-id="9fd7a-111">iOS app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="9fd7a-112">сервер рассылает уведомления, используя функции **tag** и **template** Центров уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fd7a-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9fd7a-113">Prerequisites</span></span>
<span data-ttu-id="9fd7a-114">Вы должны предварительно выполнить учебник [Использование концентраторов уведомлений для передачи экстренных новостей] , чтобы у вас был нужный код, так как этот учебник построен непосредственно на этом коде.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="9fd7a-115">Наличие Visual Studio 2012 или более поздней версии не обязательно.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="9fd7a-116">Основные сведения о шаблонах</span><span class="sxs-lookup"><span data-stu-id="9fd7a-116">Template concepts</span></span>
<span data-ttu-id="9fd7a-117">В учебнике [Использование концентраторов уведомлений для передачи экстренных новостей] вы создали приложение, которое использовало **теги** для подписки на уведомления для различных категорий новостей.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="9fd7a-118">Однако многие приложения ориентированы на несколько рынков и требуют локализации.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="9fd7a-119">Это означает, что само содержимое уведомлений должно быть локализовано и доставлено в правильный набор устройств.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="9fd7a-120">В этом разделе будут продемонстрированы способы использования **шаблонов** центров уведомлений, которые позволяют легко доставлять уведомления о локализованных экстренных новостях.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="9fd7a-121">Примечание. Один из способов отправки локализованных уведомлений — создание нескольких версий каждого тега.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="9fd7a-122">Например, для поддержки английского, французского и китайского нам понадобится три разных тега для мировых новостей: "world_en", "world_fr" и "world_ch".</span><span class="sxs-lookup"><span data-stu-id="9fd7a-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="9fd7a-123">Затем необходимо отправить локализованную версию мировых новостей по каждому из этих тегов.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="9fd7a-124">В этом разделе мы используем шаблоны во избежание избыточного количества тегов и необходимости отправки нескольких сообщений.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="9fd7a-125">В общих чертах, шаблоны представляют собой способ указать, как конкретное устройство должно получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="9fd7a-126">Шаблон указывает точный формат полезных данных путем обращения к свойствам, которые являются частью сообщения, отправленного сервером вашего приложение.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="9fd7a-127">В нашем случае мы отправим независимое от языка сообщение, которое содержит все поддерживаемые языки:</span><span class="sxs-lookup"><span data-stu-id="9fd7a-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="9fd7a-128">Затем мы убедимся, что устройство зарегистрировано с шаблоном, который ссылается на нужное свойство.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="9fd7a-129">Например, приложение iOS, которое требуется зарегистрировать для французских новостей, зарегистрирует следующее:</span><span class="sxs-lookup"><span data-stu-id="9fd7a-129">For instance,  an iOS app that wants to register for French news will register the following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="9fd7a-130">Шаблоны — это очень мощная функция, о них можно узнать больше в нашей статье [Шаблоны](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="9fd7a-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="the-app-user-interface"></a><span data-ttu-id="9fd7a-131">Пользовательский интерфейс приложения</span><span class="sxs-lookup"><span data-stu-id="9fd7a-131">The app user interface</span></span>
<span data-ttu-id="9fd7a-132">Теперь изменим приложение "Экстренные новости", созданное в разделе [Использование концентраторов уведомлений для передачи экстренных новостей] для отправки локализованных экстренных новостей с помощью шаблонов.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="9fd7a-133">В файл MainStoryboard_iPhone.storyboard добавьте Segmented Control для трех поддерживаемых языков: английского, французского и китайского (мандаринский диалект).</span><span class="sxs-lookup"><span data-stu-id="9fd7a-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with the three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="9fd7a-134">Затем обязательно добавьте IBOutlet в свой файл ViewController.h, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="9fd7a-134">Then make sure to add an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-the-ios-app"></a><span data-ttu-id="9fd7a-135">Создание приложения iOS</span><span class="sxs-lookup"><span data-stu-id="9fd7a-135">Building the iOS app</span></span>
1. <span data-ttu-id="9fd7a-136">Добавьте в свой файл Notification.h метод *retrieveLocale* и измените методы хранения и подписки, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-136">In your Notification.h add the *retrieveLocale* method, and modify the store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="9fd7a-137">Измените в файле Notification.m метод *storeCategoriesAndSubscribe* , добавив параметр языка и сохранив его в пользовательских параметрах по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="9fd7a-137">In your Notification.m, modify the *storeCategoriesAndSubscribe* method, by adding the locale parameter and storing it in the user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="9fd7a-138">Затем измените метод *subscribe* , чтобы включить языковой стандарт:</span><span class="sxs-lookup"><span data-stu-id="9fd7a-138">Then modify the *subscribe* method to include the locale:</span></span>
   
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
   
    <span data-ttu-id="9fd7a-139">Обратите внимание на то, что мы теперь используем метод *registerTemplateWithDeviceToken*, а не *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-139">Note how we are now using the method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="9fd7a-140">При регистрации шаблона необходимо предоставить шаблон json, а также имя шаблона (поскольку для нашего приложения может возникнуть необходимость зарегистрировать различные шаблоны).</span><span class="sxs-lookup"><span data-stu-id="9fd7a-140">When we register for a template we have to provide the json template and also a name for the template (as our app might want to register different templates).</span></span> <span data-ttu-id="9fd7a-141">Убедитесь, что категории регистрируются как теги, поскольку мы хотим получать уведомления об этих новостях.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-141">Make sure to register your categories as tags, as we want to make sure to receive the notifciations for those news.</span></span>
   
    <span data-ttu-id="9fd7a-142">Добавьте метод для извлечения языкового стандарта из пользовательских параметров по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-142">Add a method to retrieve the locale from the user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="9fd7a-143">Теперь, когда мы внесли изменения в наш класс уведомлений, необходимо убедиться в том, что наш ViewController использует новый UISegmentControl.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-143">Now that we modified our Notifications class, we have to make sure that our ViewController makes use of the new UISegmentControl.</span></span> <span data-ttu-id="9fd7a-144">Добавьте следующую строку в метод *viewDidLoad* , чтобы убедиться в том, что отображается языковой стандарт, выбранный в данный момент:</span><span class="sxs-lookup"><span data-stu-id="9fd7a-144">Add the following line in the *viewDidLoad* method to make sure to show the locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="9fd7a-145">Затем в методе *subscribe* замените свой вызов *storeCategoriesAndSubscribe* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9fd7a-145">Then, in your *subscribe* method, change your call to the *storeCategoriesAndSubscribe* to the following:</span></span>
   
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
3. <span data-ttu-id="9fd7a-146">И наконец, необходимо обновить метод *didRegisterForRemoteNotificationsWithDeviceToken* в методе AppDelegate.m, чтобы правильно обновить регистрацию при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-146">Finally, you have to update the *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="9fd7a-147">Замените вызов метода уведомления *subscribe* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9fd7a-147">Change your call to the *subscribe* method of notifications with the following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="9fd7a-148">(Необязательно.) Отправьте локализованные шаблонные уведомления из консольного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-the-device"></a><span data-ttu-id="9fd7a-149">(Необязательно.) Отправка локализованных шаблонных уведомлений с устройства</span><span class="sxs-lookup"><span data-stu-id="9fd7a-149">(optional) Send localized template notifications from the device</span></span>
<span data-ttu-id="9fd7a-150">Предположим, у вас нет доступа к Visual Studio или вы просто хотите проверить отправку локализованных шаблонных уведомлений непосредственно из приложения на устройстве.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-150">If you don't have access to Visual Studio, or want to just test sending the localized template notifications directly from the app on the device.</span></span>  <span data-ttu-id="9fd7a-151">Вы можете просто добавить параметры локализованных шаблонов в метод `SendNotificationRESTAPI` , определенный в предыдущем учебнике.</span><span class="sxs-lookup"><span data-stu-id="9fd7a-151">You can simple add the localized template parameters to the `SendNotificationRESTAPI` method you defined in the previous tutorial.</span></span>

        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];

            NSString *json;

            // Construct the messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];

            // Generated the token to be used in the authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];

            //Create the request to add the template notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];

            // Add the category as a tag
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

            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];

            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];

            // Send the REST request
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




## <a name="next-steps"></a><span data-ttu-id="9fd7a-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9fd7a-152">Next Steps</span></span>
<span data-ttu-id="9fd7a-153">Дополнительные сведения об использовании шаблонов см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="9fd7a-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="9fd7a-154">[Уведомление пользователей с помощью центров уведомлений: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="9fd7a-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="9fd7a-155">[Уведомление пользователей с помощью центров уведомлений: мобильные службы]</span><span class="sxs-lookup"><span data-stu-id="9fd7a-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="9fd7a-156">[Использование концентраторов уведомлений для передачи экстренных новостей]: /manage/services/notification-hubs/breaking-news-ios</span><span class="sxs-lookup"><span data-stu-id="9fd7a-156">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-ios</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
<span data-ttu-id="9fd7a-157">[Уведомление пользователей с помощью центров уведомлений: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="9fd7a-157">[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="9fd7a-158">[Уведомление пользователей с помощью центров уведомлений: мобильные службы]: /manage/services/notification-hubs/notify-users</span><span class="sxs-lookup"><span data-stu-id="9fd7a-158">[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users</span></span>
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
