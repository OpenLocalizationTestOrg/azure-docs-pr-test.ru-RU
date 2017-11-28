---
title: "aaaAzure Rich Push концентраторы уведомлений"
description: "Узнайте, как toosend rich Push-уведомлений приложения iOS tooan уведомления из Azure. Примеры кода написаны на Objective-C и C#."
documentationcenter: ios
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: 590304df-c0a4-46c5-8ef5-6a6486bb3340
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 5432d8bf47777371bea3521a0c0176ade75fbd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="89970-104">Форматированные push-уведомления на основе концентраторов уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="89970-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="89970-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="89970-105">Overview</span></span>
<span data-ttu-id="89970-106">В порядке tooengage пользователей с мгновенными полноценное содержимое приложение может возникнуть toopush за пределы обычного текста.</span><span class="sxs-lookup"><span data-stu-id="89970-106">In order tooengage users with instant rich contents, an application might want toopush beyond plain text.</span></span> <span data-ttu-id="89970-107">Эти уведомления улучшают уровень взаимодействия с пользователем и позволяют отображать URL-адреса, изображения, купоны, воспроизводить звуки и т. д.</span><span class="sxs-lookup"><span data-stu-id="89970-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="89970-108">Этот учебник построен на hello [уведомить пользователей](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) раздела и показано, как toosend push-уведомления, включающие полезных данных (например, изображения).</span><span class="sxs-lookup"><span data-stu-id="89970-108">This tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how toosend push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="89970-109">Этот учебник совместим с iOS 7 и 8.</span><span class="sxs-lookup"><span data-stu-id="89970-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="89970-110">На высоком уровне:</span><span class="sxs-lookup"><span data-stu-id="89970-110">At a high level:</span></span>

1. <span data-ttu-id="89970-111">Серверная часть приложения Hello:</span><span class="sxs-lookup"><span data-stu-id="89970-111">hello app backend:</span></span>
   * <span data-ttu-id="89970-112">Магазины hello форматированного полезных данных (в этом случае изображения) в хранилище базы данных или локальной серверной hello</span><span class="sxs-lookup"><span data-stu-id="89970-112">Stores hello rich payload (in this case, image) in hello backend database/local storage</span></span>
   * <span data-ttu-id="89970-113">Отправляет идентификатор этого устройства toohello уведомлений с широкими возможностями</span><span class="sxs-lookup"><span data-stu-id="89970-113">Sends ID of this rich notification toohello device</span></span>
2. <span data-ttu-id="89970-114">Приложения на устройстве hello:</span><span class="sxs-lookup"><span data-stu-id="89970-114">App on hello device:</span></span>
   * <span data-ttu-id="89970-115">Внутренний запрос hello форматированного полезных данных с Идентификатором hello, он получает hello контактов</span><span class="sxs-lookup"><span data-stu-id="89970-115">Contacts hello backend requesting hello rich payload with hello ID it receives</span></span>
   * <span data-ttu-id="89970-116">Отправляет уведомления пользователей на устройстве hello, после завершения извлечения данных и показывает hello полезных данных немедленно в том случае, когда пользователь нажимает кнопку toolearn Дополнительные</span><span class="sxs-lookup"><span data-stu-id="89970-116">Sends users notifications on hello device when data retrieval is complete, and shows hello payload immediately when users tap toolearn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="89970-117">Проект веб-интерфейса API</span><span class="sxs-lookup"><span data-stu-id="89970-117">WebAPI Project</span></span>
1. <span data-ttu-id="89970-118">В Visual Studio откройте hello **AppBackend** проекта, созданного в hello [уведомить пользователей](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="89970-118">In Visual Studio, open hello **AppBackend** project that you created in hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="89970-119">Получить изображение будет toonotify пользователей с и поместить его в **img** папки в каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="89970-119">Obtain an image you would like toonotify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="89970-120">Нажмите кнопку **Показать все файлы** в hello в обозревателе решений и щелкните правой кнопкой папку hello слишком**включить в проект**.</span><span class="sxs-lookup"><span data-stu-id="89970-120">Click **Show All Files** in hello Solution Explorer, and right-click hello folder too**Include In Project**.</span></span>
4. <span data-ttu-id="89970-121">Выбранный образ hello, изменить его действие при построении в окне свойств слишком**внедренный ресурс**.</span><span class="sxs-lookup"><span data-stu-id="89970-121">With hello image selected, change its Build Action in Properties window too**Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="89970-122">В **Notifications.cs**, добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="89970-122">In **Notifications.cs**, add hello following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="89970-123">Обновление hello всей **уведомления** класса hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="89970-123">Update hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="89970-124">Быть убедиться, что tooreplace местозаполнителей hello учетных данных концентратора уведомлений и имя файла изображения.</span><span class="sxs-lookup"><span data-stu-id="89970-124">Be sure tooreplace hello placeholders with your notification hub credentials and image file name.</span></span>
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message toodisplay toousers
            public string Message { get; set; }
            // Type of rich payload (developer-defined)
            public string RichType { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }
   
        public class Notifications {
            public static Notifications Instance = new Notifications();
   
            private List<Notification> notifications = new List<Notification>();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                // Placeholders: replace with hello connection string (with full access) for your notification hub and hello hub name from hello Azure Classics Portal
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",  "{hub name}");
            }
   
            public Notification CreateNotification(string message, string richType, string payload) {
                var notification = new Notification() {
                    Id = notifications.Count,
                    Message = message,
                    RichType = richType,
                    Payload = payload,
                    Read = false
                };
   
                notifications.Add(notification);
   
                return notification;
            }
   
            public Stream ReadImage(int id) {
                var assembly = Assembly.GetExecutingAssembly();
                // Placeholder: image file name (for example, logo.png).
                return assembly.GetManifestResourceStream("AppBackend.img.{logo.png}");
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="89970-125">(необязательно) См. слишком[как tooembed и доступ к ресурсам с помощью Visual C#](http://support.microsoft.com/kb/319292) Дополнительные сведения о том, как tooadd и получения ресурсов проекта.</span><span class="sxs-lookup"><span data-stu-id="89970-125">(optional) Refer too[How tooembed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how tooadd and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="89970-126">В **NotificationsController.cs**, переопределить **NotificationsController** с hello следующие фрагменты кода.</span><span class="sxs-lookup"><span data-stu-id="89970-126">In **NotificationsController.cs**, redefine **NotificationsController**  with hello following snippets.</span></span> <span data-ttu-id="89970-127">Это отправляет toodevice идентификатор начального автоматической форматированного уведомления и разрешает получение клиентского образа:</span><span class="sxs-lookup"><span data-stu-id="89970-127">This sends an initial silent rich notification id toodevice and allows client-side retrieval of image:</span></span>
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) tooclient
        public async Task<HttpResponseMessage> Post() {
            // Replace hello placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification tooapns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. <span data-ttu-id="89970-128">Теперь мы будет повторное развертывание этого приложения tooan веб-сайта Azure, в порядке toomake доступ из всех устройств.</span><span class="sxs-lookup"><span data-stu-id="89970-128">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="89970-129">Щелкните правой кнопкой мыши на hello **AppBackend** проект и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="89970-129">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="89970-130">Выберите в качестве цели публикации веб-сайт Azure.</span><span class="sxs-lookup"><span data-stu-id="89970-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="89970-131">Войти с учетной записью Azure и выберите существующий или новый веб-сайт и запишите hello **URL-адрес назначения** свойство в hello **подключения** вкладки. Мы будем называть toothis URL-адрес, как ваш *конечную точку серверной части* далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="89970-131">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="89970-132">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="89970-132">Click **Publish**.</span></span>

## <a name="modify-hello-ios-project"></a><span data-ttu-id="89970-133">Изменение проекта iOS hello</span><span class="sxs-lookup"><span data-stu-id="89970-133">Modify hello iOS project</span></span>
<span data-ttu-id="89970-134">Теперь, когда вы изменили приложения серверной hello просто toosend *идентификатор* уведомления, будет изменить этот идентификатор вашей toohandle приложения iOS и получения форматированного сообщения hello из серверной части.</span><span class="sxs-lookup"><span data-stu-id="89970-134">Now that you have modified your app backend toosend just hello *id* of a notification, you will change your iOS app toohandle that id and retrieve hello rich message from your backend.</span></span>

1. <span data-ttu-id="89970-135">Откройте свой проект iOS и включить удаленный уведомления по переходом цели tooyour основным приложением в hello **цели** раздела.</span><span class="sxs-lookup"><span data-stu-id="89970-135">Open your iOS project, and enable remote notifications by going tooyour main app target in hello **Targets** section.</span></span>
2. <span data-ttu-id="89970-136">Щелкните **возможности**, включите **фоновые режимы**и проверьте hello **удаленного уведомления** флажок.</span><span class="sxs-lookup"><span data-stu-id="89970-136">Click on **Capabilities**, turn on **Background Modes**, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="89970-137">Go слишком**Main.storyboard**и убедитесь, что у вас есть View Controller (tooas указанной Главная представление-контроллер в этом учебнике) из [уведомлять пользователя](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="89970-137">Go too**Main.storyboard**, and make sure you have a View Controller (refered tooas Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="89970-138">Добавить **навигации контроллера** tooyour раскадровки и перетаскивание его hello toomake View Controller tooHome **корневой представление** навигации.</span><span class="sxs-lookup"><span data-stu-id="89970-138">Add a **Navigation Controller** tooyour storyboard, and control-drag tooHome View Controller toomake it hello **root view** of navigation.</span></span> <span data-ttu-id="89970-139">Убедитесь, что hello **— начальное представление контроллер** в атрибутах инспектора выбирается только hello навигации контроллера.</span><span class="sxs-lookup"><span data-stu-id="89970-139">Make sure hello **Is Initial View Controller** in Attributes inspector is selected for hello Navigation Controller only.</span></span>
5. <span data-ttu-id="89970-140">Добавить **View Controller** toostoryboard и добавьте **представление изображения**.</span><span class="sxs-lookup"><span data-stu-id="89970-140">Add a **View Controller** toostoryboard and add an **Image View**.</span></span> <span data-ttu-id="89970-141">Это страница приветствия, пользователи увидят, когда они выберут toolearn несколько, щелкнув hello notifiication.</span><span class="sxs-lookup"><span data-stu-id="89970-141">This is hello page users will see once they choose toolearn more by clicking on hello notifiication.</span></span> <span data-ttu-id="89970-142">Раскадровка должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89970-142">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="89970-143">Щелкните hello **Главная View Controller** в раскадровки и убедитесь, что он содержит **homeViewController** как его **настраиваемый класс** и **идентификатор раскадровки**под hello удостоверение инспектора.</span><span class="sxs-lookup"><span data-stu-id="89970-143">Click on hello **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under hello Identity inspector.</span></span>
7. <span data-ttu-id="89970-144">Здравствуйте же контроллера представление изображения как **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="89970-144">Do hello same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="89970-145">Затем создайте новый класс View Controller под названием **imageViewController** toohandle hello пользовательского интерфейса вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="89970-145">Then, create a new View Controller class titled **imageViewController** toohandle hello UI you just created.</span></span>
9. <span data-ttu-id="89970-146">В **imageViewController.h**, добавьте следующие объявления интерфейса контроллера toohello hello.</span><span class="sxs-lookup"><span data-stu-id="89970-146">In **imageViewController.h**, add hello following toohello controller's interface declarations.</span></span> <span data-ttu-id="89970-147">Убедитесь, что toocontrol перетаскивания из hello раскадровки изображение представления toothese свойства toolink hello два:</span><span class="sxs-lookup"><span data-stu-id="89970-147">Make sure toocontrol-drag from hello storyboard image view toothese properties toolink hello two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="89970-148">В **imageViewController.m**, добавьте следующее hello в конце hello **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="89970-148">In **imageViewController.m**, add hello following at hello end of **viewDidload**:</span></span>
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="89970-149">В **AppDelegate.m**, созданный контроллер image hello импорта:</span><span class="sxs-lookup"><span data-stu-id="89970-149">In **AppDelegate.m**, import hello image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="89970-150">Добавьте раздел интерфейса с помощью объявления hello:</span><span class="sxs-lookup"><span data-stu-id="89970-150">Add an interface section with hello following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="89970-151">В **AppDelegate** проверьте, регистрирует ли приложение автоматические уведомления в **application: didFinishLaunchingWithOptions**:</span><span class="sxs-lookup"><span data-stu-id="89970-151">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
        // Software version
        self.iOS8 = [[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)] && [[UIApplication sharedApplication] respondsToSelector:@selector(registerForRemoteNotifications)];
    
        // Register for remote notifications for iOS8 and previous versions
        if (self.iOS8) {
            NSLog(@"This device is running with iOS8.");
    
            // Action
            UIMutableUserNotificationAction *richPushAction = [[UIMutableUserNotificationAction alloc] init];
            richPushAction.identifier = @"richPushMore";
            richPushAction.activationMode = UIUserNotificationActivationModeForeground;
            richPushAction.authenticationRequired = NO;
            richPushAction.title = @"More";
    
            // Notification category
            UIMutableUserNotificationCategory* richPushCategory = [[UIMutableUserNotificationCategory alloc] init];
            richPushCategory.identifier = @"richPush";
            [richPushCategory setActions:@[richPushAction] forContext:UIUserNotificationActionContextDefault];
    
            // Notification categories
            NSSet* richPushCategories = [NSSet setWithObjects:richPushCategory, nil];

            UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                    UIUserNotificationTypeAlert |
                                                    UIUserNotificationTypeBadge
                                                                                     categories:richPushCategories];

            [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
            [[UIApplication sharedApplication] registerForRemoteNotifications];

        }
        else {
            // Previous iOS versions
            NSLog(@"This device is running with iOS7 or earlier versions.");

            [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
        }

        return YES;

1. <span data-ttu-id="89970-152">Замените в следующие реализации для hello **приложения: didRegisterForRemoteNotificationsWithDeviceToken** tootake hello раскадровки изменения интерфейса пользователя в учетную запись:</span><span class="sxs-lookup"><span data-stu-id="89970-152">Subsitute in hello following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** tootake hello storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="89970-153">Затем добавьте следующие методы слишком hello**AppDelegate.m** tooretrieve hello изображения от конечной точки и отправить локального уведомление при завершении извлечения.</span><span class="sxs-lookup"><span data-stu-id="89970-153">Then, add hello following methods too**AppDelegate.m** tooretrieve hello image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="89970-154">Убедитесь, что заполнитель hello toosubstitute `{backend endpoint}` с серверной конечной точки:</span><span class="sxs-lookup"><span data-stu-id="89970-154">Make sure toosubstitute hello placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
       NSString *const GetNotificationEndpoint = @"{backend endpoint}/api/notifications";
   
       // Helper: retrieve notification content from backend with rich notification id
       - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion {
           UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
           homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
           NSString* authenticationHeader = hvc.registerClient.authenticationHeader;
           // Check if authenticated
           if (!authenticationHeader) return;
   
           NSURLSession* session = [NSURLSession
                                    sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                    delegate:nil
                                    delegateQueue:nil];
   
           NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, richId]];
           NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
           [request setHTTPMethod:@"GET"];
           NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
           [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
   
           NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
   
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
               if (!error && httpResponse.statusCode == 200) {
                   // From NSData tooUIImage
                   self.imagePayload = [UIImage imageWithData:data];
   
                   completion(nil);
               }
               else {
                   NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                   if (error)
                       completion(error);
                   else {
                       completion([NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                   }
               }
           }];
           [dataTask resume];
       }
   
       // Handle silent push notifications when id is sent from backend
       - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler {
           self.userInfo = userInfo;
           int richId = [[self.userInfo objectForKey:@"richId"] intValue];
           NSString* richType = [self.userInfo objectForKey:@"richType"];
   
           // Retrieve image data
           if ([richType isEqualToString:@"img"]) {  
               [self retrieveRichImageWithId:richId completion:^(NSError* error) {
                   if (!error){
                       // Send local notification
                       UILocalNotification* localNotification = [[UILocalNotification alloc] init];
   
                       // "5" is arbitrary here toogive you enough time tooquit out of hello app and receive push notifications
                       localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:5];
                       localNotification.userInfo = self.userInfo;
                       localNotification.alertBody = [self.userInfo objectForKey:@"richMessage"];
                       localNotification.timeZone = [NSTimeZone defaultTimeZone];
   
                       // iOS8 categories
                       if (self.iOS8) {
                           localNotification.category = @"richPush";
                       }
   
                       [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                       handler(UIBackgroundFetchResultNewData);
                   }
                   else{
                       handler(UIBackgroundFetchResultFailed);
                   }
               }];
           }
           // Add "else if" here toohandle more types of rich content such as url, sound files, etc.
       }
3. <span data-ttu-id="89970-155">Обрабатывать уведомления локальных hello выше, открыв hello контроллера представление изображения в **AppDelegate.m** с hello следующие методы:</span><span class="sxs-lookup"><span data-stu-id="89970-155">Handle hello local notification above by opening up hello image view controller in **AppDelegate.m** with hello following methods:</span></span>
   
       // Helper: redirect users tooimage view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image tooimage view controller
           imgViewController.imagePayload = img;
   
           // Redirect
           [navigationController pushViewController:imgViewController animated:YES];
       }
   
       // Handle local notification sent above in didReceiveRemoteNotification
       - (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification {
           if (application.applicationState == UIApplicationStateActive) {
               // Show in-app alert with an extra "more" button
               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:notification.alertBody delegate:self cancelButtonTitle:@"OK" otherButtonTitles:@"More", nil];
   
               [alert show];
           }
           // App becomes active from user's tap on notification
           else {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
       }
   
       // Handle buttons in in-app alerts and redirect with data/image
       - (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex {
           // Handle "more" button
           if (buttonIndex == 1)
           {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           // Add "else if" here toohandle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-hello-application"></a><span data-ttu-id="89970-156">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="89970-156">Run hello Application</span></span>
1. <span data-ttu-id="89970-157">В XCode запустите приложение hello на устройстве физических операций ввода-вывода (push-уведомлений не будет работать в симуляторе hello).</span><span class="sxs-lookup"><span data-stu-id="89970-157">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="89970-158">В приложении iOS hello пользовательского интерфейса, введите имя пользователя и пароль hello же для проверки подлинности и нажмите кнопку **входа в**.</span><span class="sxs-lookup"><span data-stu-id="89970-158">In hello iOS app UI, enter a username and password of hello same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="89970-159">Щелкните **Отправить push-уведомление** , после чего в приложении появится предупреждение.</span><span class="sxs-lookup"><span data-stu-id="89970-159">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="89970-160">Если щелкнуть **дополнительные**, можно подключить toohello изображения выбранного tooinclude в серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="89970-160">If you click on **More**, you will be brought toohello image you chose tooinclude in your app backend.</span></span>
4. <span data-ttu-id="89970-161">Можно также щелкнуть **принудительной отправки** и сразу же нажмите кнопку домашней hello вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="89970-161">You can also click **Send push** and immediately press hello home button of your device.</span></span> <span data-ttu-id="89970-162">Через несколько секунд вы получите push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="89970-162">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="89970-163">Если коснуться ее или выберите более будут введены tooyour приложения и hello широкие возможности графического содержимого.</span><span class="sxs-lookup"><span data-stu-id="89970-163">If you tap on it or click More, you will be brought tooyour app and hello rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
