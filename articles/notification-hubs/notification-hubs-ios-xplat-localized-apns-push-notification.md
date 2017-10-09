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
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a><span data-ttu-id="b427a-103">Использование концентраторов уведомлений критические toosend локализованные новостей tooiOS устройств</span><span class="sxs-lookup"><span data-stu-id="b427a-103">Use Notification Hubs toosend localized breaking news tooiOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b427a-104">C# в Магазине Windows</span><span class="sxs-lookup"><span data-stu-id="b427a-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="b427a-105">iOS</span><span class="sxs-lookup"><span data-stu-id="b427a-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="b427a-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="b427a-106">Overview</span></span>
<span data-ttu-id="b427a-107">В этом разделе показано, как toouse hello [шаблоны](notification-hubs-templates-cross-platform-push-messages.md) функции концентраторов уведомлений Azure toobroadcast критические уведомления новостей, локализованные языка и устройства.</span><span class="sxs-lookup"><span data-stu-id="b427a-107">This topic shows you how toouse hello [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="b427a-108">В этом учебнике, начинаться с приложение hello iOS, созданные в [toosend использования концентраторов уведомлений, новости].</span><span class="sxs-lookup"><span data-stu-id="b427a-108">In this tutorial you start with hello iOS app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="b427a-109">После завершения можно будет tooregister для категорий, которые вас интересуют, указать язык в уведомления, которое tooreceive hello и получать только push-уведомлений для hello выбранных категорий на этом языке.</span><span class="sxs-lookup"><span data-stu-id="b427a-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="b427a-110">Существует два сценария toothis частей:</span><span class="sxs-lookup"><span data-stu-id="b427a-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="b427a-111">приложение iOS позволяет клиентским устройств toospecify язык и toodifferent toosubscribe критические категории новостей;</span><span class="sxs-lookup"><span data-stu-id="b427a-111">iOS app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="b427a-112">Hello внутренней осуществляет широковещательную рассылку уведомлений hello, с использованием hello **тега** и **шаблона** поддержки концентраторов уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="b427a-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b427a-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b427a-113">Prerequisites</span></span>
<span data-ttu-id="b427a-114">Вы должны уже выполнили hello [toosend использования концентраторов уведомлений, новости] учебника и иметь hello кода, так как этот учебник построен непосредственно на этот код.</span><span class="sxs-lookup"><span data-stu-id="b427a-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="b427a-115">Наличие Visual Studio 2012 или более поздней версии не обязательно.</span><span class="sxs-lookup"><span data-stu-id="b427a-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="b427a-116">Основные сведения о шаблонах</span><span class="sxs-lookup"><span data-stu-id="b427a-116">Template concepts</span></span>
<span data-ttu-id="b427a-117">В [toosend использования концентраторов уведомлений, новости] построении приложения, которое используется **теги** toonotifications toosubscribe новостей разных категорий.</span><span class="sxs-lookup"><span data-stu-id="b427a-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="b427a-118">Однако многие приложения ориентированы на несколько рынков и требуют локализации.</span><span class="sxs-lookup"><span data-stu-id="b427a-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="b427a-119">Таким образом, содержимое hello hello уведомлений, сами имеют toobe локализованные доставленный toohello правильным набором устройств.</span><span class="sxs-lookup"><span data-stu-id="b427a-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="b427a-120">В этом разделе будет показано, как toouse hello **шаблона** функции концентраторов уведомлений tooeasily доставки локализованное уведомлений с последними новостями.</span><span class="sxs-lookup"><span data-stu-id="b427a-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="b427a-121">Примечание: один из способов toosend локализованные уведомления является toocreate нескольких версий каждого тега.</span><span class="sxs-lookup"><span data-stu-id="b427a-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="b427a-122">Для экземпляра toosupport английском, французском и мандаринский, пришлось бы иметь три разные теги Мировые: «world_en», «world_fr» и «world_ch».</span><span class="sxs-lookup"><span data-stu-id="b427a-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="b427a-123">Мы будет иметь toosend локализованной версии tooeach новостей hello world эти теги.</span><span class="sxs-lookup"><span data-stu-id="b427a-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="b427a-124">В этом разделе используются шаблоны tooavoid hello увеличением числа теги и требование hello отправка нескольких сообщений.</span><span class="sxs-lookup"><span data-stu-id="b427a-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="b427a-125">На высоком уровне шаблоны являются toospecify способом как конкретного устройства следует получать такие уведомления.</span><span class="sxs-lookup"><span data-stu-id="b427a-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="b427a-126">шаблон Hello указывает формат hello точное полезных данных с помощью ссылки tooproperties, которые являются частью приветственное сообщение, отправленное приложение в серверной части.</span><span class="sxs-lookup"><span data-stu-id="b427a-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="b427a-127">В нашем случае мы отправим независимое от языка сообщение, которое содержит все поддерживаемые языки:</span><span class="sxs-lookup"><span data-stu-id="b427a-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="b427a-128">Затем мы гарантируем, что устройства регистрацию с шаблоном, который ссылается свойство правильный toohello.</span><span class="sxs-lookup"><span data-stu-id="b427a-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="b427a-129">Для экземпляра приложения iOS, если оно tooregister для французского языка новостей зарегистрирует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="b427a-129">For instance,  an iOS app that wants tooregister for French news will register hello following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="b427a-130">Шаблоны — это очень мощная функция, о них можно узнать больше в нашей статье [Шаблоны](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="b427a-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="hello-app-user-interface"></a><span data-ttu-id="b427a-131">пользовательский интерфейс приложения Hello</span><span class="sxs-lookup"><span data-stu-id="b427a-131">hello app user interface</span></span>
<span data-ttu-id="b427a-132">Теперь мы изменит приложение hello последние новости, созданный в разделе hello [toosend использования концентраторов уведомлений, новости] toosend локализованные новости, с помощью шаблонов.</span><span class="sxs-lookup"><span data-stu-id="b427a-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="b427a-133">В вашей MainStoryboard_iPhone.storyboard добавьте сегментированных управления с тремя hello языков, которые поддерживаются: английский, французский и китайский.</span><span class="sxs-lookup"><span data-stu-id="b427a-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with hello three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="b427a-134">Убедитесь в том tooadd IBOutlet в ваш ViewController.h как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="b427a-134">Then make sure tooadd an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-hello-ios-app"></a><span data-ttu-id="b427a-135">Построение приложения iOS hello</span><span class="sxs-lookup"><span data-stu-id="b427a-135">Building hello iOS app</span></span>
1. <span data-ttu-id="b427a-136">Добавьте в ваш Notification.h hello *retrieveLocale* метода и изменение хранилища hello и подписываться методы, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="b427a-136">In your Notification.h add hello *retrieveLocale* method, and modify hello store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="b427a-137">В вашей Notification.m измените hello *storeCategoriesAndSubscribe* метода, добавив параметр языкового стандарта hello и сохранить их в значения по умолчанию hello пользователя:</span><span class="sxs-lookup"><span data-stu-id="b427a-137">In your Notification.m, modify hello *storeCategoriesAndSubscribe* method, by adding hello locale parameter and storing it in hello user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="b427a-138">Затем измените hello *подписаться* метод tooinclude hello языка:</span><span class="sxs-lookup"><span data-stu-id="b427a-138">Then modify hello *subscribe* method tooinclude hello locale:</span></span>
   
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
   
    <span data-ttu-id="b427a-139">Обратите внимание на то, как мы теперь используют метод hello *registerTemplateWithDeviceToken*, а не *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="b427a-139">Note how we are now using hello method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="b427a-140">При регистрации для шаблона у нас есть tooprovide hello json шаблона, а также имя шаблона hello (как в нашем приложении может возникнуть различные шаблоны tooregister).</span><span class="sxs-lookup"><span data-stu-id="b427a-140">When we register for a template we have tooprovide hello json template and also a name for hello template (as our app might want tooregister different templates).</span></span> <span data-ttu-id="b427a-141">Внесите убедиться, что tooregister категорий, как теги, мы хотим toomake убедиться, что tooreceive hello notifciations для этих новостей.</span><span class="sxs-lookup"><span data-stu-id="b427a-141">Make sure tooregister your categories as tags, as we want toomake sure tooreceive hello notifciations for those news.</span></span>
   
    <span data-ttu-id="b427a-142">Добавьте метод tooretrieve hello языкового из пользовательских параметров по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="b427a-142">Add a method tooretrieve hello locale from hello user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="b427a-143">Теперь, когда мы внесли изменения в наших класса уведомления, у нас есть toomake убедиться, что наши ViewController делает использование hello новый UISegmentControl.</span><span class="sxs-lookup"><span data-stu-id="b427a-143">Now that we modified our Notifications class, we have toomake sure that our ViewController makes use of hello new UISegmentControl.</span></span> <span data-ttu-id="b427a-144">Добавьте следующие строки в hello hello *viewDidLoad* метод toomake убедиться, что tooshow hello языкового стандарта, выбранного в настоящее время:</span><span class="sxs-lookup"><span data-stu-id="b427a-144">Add hello following line in hello *viewDidLoad* method toomake sure tooshow hello locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="b427a-145">Затем в вашей *подписаться* метод, изменить ваш вызов toohello *storeCategoriesAndSubscribe* toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="b427a-145">Then, in your *subscribe* method, change your call toohello *storeCategoriesAndSubscribe* toohello following:</span></span>
   
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
3. <span data-ttu-id="b427a-146">Наконец, у вас есть tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* метод в вашей AppDelegate.m, чтобы правильно, можно обновить регистрацию при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="b427a-146">Finally, you have tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="b427a-147">Изменить ваш вызов toohello *подписаться* метод уведомлений hello следующее:</span><span class="sxs-lookup"><span data-stu-id="b427a-147">Change your call toohello *subscribe* method of notifications with hello following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="b427a-148">(Необязательно.) Отправьте локализованные шаблонные уведомления из консольного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="b427a-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a><span data-ttu-id="b427a-149">(необязательно) Отправлять уведомления локализованный шаблон с устройства hello</span><span class="sxs-lookup"><span data-stu-id="b427a-149">(optional) Send localized template notifications from hello device</span></span>
<span data-ttu-id="b427a-150">Если не имеют доступа к tooVisual Studio или toojust теста, отправка уведомлений шаблона hello локализованные непосредственно из приложения hello на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="b427a-150">If you don't have access tooVisual Studio, or want toojust test sending hello localized template notifications directly from hello app on hello device.</span></span>  <span data-ttu-id="b427a-151">Вы можете простого добавления toohello параметры шаблона hello локализованные `SendNotificationRESTAPI` метод, определенный в предыдущем учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="b427a-151">You can simple add hello localized template parameters toohello `SendNotificationRESTAPI` method you defined in hello previous tutorial.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="b427a-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b427a-152">Next Steps</span></span>
<span data-ttu-id="b427a-153">Дополнительные сведения об использовании шаблонов см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="b427a-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="b427a-154">[Уведомление пользователей с помощью центров уведомлений: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="b427a-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="b427a-155">[Уведомление пользователей с помощью центров уведомлений: мобильные службы]</span><span class="sxs-lookup"><span data-stu-id="b427a-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

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
