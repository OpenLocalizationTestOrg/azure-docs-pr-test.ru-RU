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
# <a name="azure-notification-hubs-rich-push"></a>Форматированные push-уведомления на основе концентраторов уведомлений Azure
## <a name="overview"></a>Обзор
В порядке tooengage пользователей с мгновенными полноценное содержимое приложение может возникнуть toopush за пределы обычного текста. Эти уведомления улучшают уровень взаимодействия с пользователем и позволяют отображать URL-адреса, изображения, купоны, воспроизводить звуки и т. д. Этот учебник построен на hello [уведомить пользователей](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) раздела и показано, как toosend push-уведомления, включающие полезных данных (например, изображения).

Этот учебник совместим с iOS 7 и 8.

  ![][IOS1]

На высоком уровне:

1. Серверная часть приложения Hello:
   * Магазины hello форматированного полезных данных (в этом случае изображения) в хранилище базы данных или локальной серверной hello
   * Отправляет идентификатор этого устройства toohello уведомлений с широкими возможностями
2. Приложения на устройстве hello:
   * Внутренний запрос hello форматированного полезных данных с Идентификатором hello, он получает hello контактов
   * Отправляет уведомления пользователей на устройстве hello, после завершения извлечения данных и показывает hello полезных данных немедленно в том случае, когда пользователь нажимает кнопку toolearn Дополнительные

## <a name="webapi-project"></a>Проект веб-интерфейса API
1. В Visual Studio откройте hello **AppBackend** проекта, созданного в hello [уведомить пользователей](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) учебника.
2. Получить изображение будет toonotify пользователей с и поместить его в **img** папки в каталоге проекта.
3. Нажмите кнопку **Показать все файлы** в hello в обозревателе решений и щелкните правой кнопкой папку hello слишком**включить в проект**.
4. Выбранный образ hello, изменить его действие при построении в окне свойств слишком**внедренный ресурс**.
   
    ![][IOS2]
5. В **Notifications.cs**, добавьте следующее hello с помощью инструкции:
   
        using System.Reflection;
6. Обновление hello всей **уведомления** класса hello, следующий код. Быть убедиться, что tooreplace местозаполнителей hello учетных данных концентратора уведомлений и имя файла изображения.
   
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
   > (необязательно) См. слишком[как tooembed и доступ к ресурсам с помощью Visual C#](http://support.microsoft.com/kb/319292) Дополнительные сведения о том, как tooadd и получения ресурсов проекта.
   > 
   > 
7. В **NotificationsController.cs**, переопределить **NotificationsController** с hello следующие фрагменты кода. Это отправляет toodevice идентификатор начального автоматической форматированного уведомления и разрешает получение клиентского образа:
   
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
8. Теперь мы будет повторное развертывание этого приложения tooan веб-сайта Azure, в порядке toomake доступ из всех устройств. Щелкните правой кнопкой мыши на hello **AppBackend** проект и выберите **публикации**.
9. Выберите в качестве цели публикации веб-сайт Azure. Войти с учетной записью Azure и выберите существующий или новый веб-сайт и запишите hello **URL-адрес назначения** свойство в hello **подключения** вкладки. Мы будем называть toothis URL-адрес, как ваш *конечную точку серверной части* далее в этом учебнике. Щелкните **Опубликовать**.

## <a name="modify-hello-ios-project"></a>Изменение проекта iOS hello
Теперь, когда вы изменили приложения серверной hello просто toosend *идентификатор* уведомления, будет изменить этот идентификатор вашей toohandle приложения iOS и получения форматированного сообщения hello из серверной части.

1. Откройте свой проект iOS и включить удаленный уведомления по переходом цели tooyour основным приложением в hello **цели** раздела.
2. Щелкните **возможности**, включите **фоновые режимы**и проверьте hello **удаленного уведомления** флажок.
   
    ![][IOS3]
3. Go слишком**Main.storyboard**и убедитесь, что у вас есть View Controller (tooas указанной Главная представление-контроллер в этом учебнике) из [уведомлять пользователя](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) учебника.
4. Добавить **навигации контроллера** tooyour раскадровки и перетаскивание его hello toomake View Controller tooHome **корневой представление** навигации. Убедитесь, что hello **— начальное представление контроллер** в атрибутах инспектора выбирается только hello навигации контроллера.
5. Добавить **View Controller** toostoryboard и добавьте **представление изображения**. Это страница приветствия, пользователи увидят, когда они выберут toolearn несколько, щелкнув hello notifiication. Раскадровка должна выглядеть следующим образом:
   
    ![][IOS4]
6. Щелкните hello **Главная View Controller** в раскадровки и убедитесь, что он содержит **homeViewController** как его **настраиваемый класс** и **идентификатор раскадровки**под hello удостоверение инспектора.
7. Здравствуйте же контроллера представление изображения как **imageViewController**.
8. Затем создайте новый класс View Controller под названием **imageViewController** toohandle hello пользовательского интерфейса вы только что создали.
9. В **imageViewController.h**, добавьте следующие объявления интерфейса контроллера toohello hello. Убедитесь, что toocontrol перетаскивания из hello раскадровки изображение представления toothese свойства toolink hello два:
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. В **imageViewController.m**, добавьте следующее hello в конце hello **viewDidload**:
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. В **AppDelegate.m**, созданный контроллер image hello импорта:
    
        #import "imageViewController.h"
12. Добавьте раздел интерфейса с помощью объявления hello:
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. В **AppDelegate** проверьте, регистрирует ли приложение автоматические уведомления в **application: didFinishLaunchingWithOptions**:
    
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

1. Замените в следующие реализации для hello **приложения: didRegisterForRemoteNotificationsWithDeviceToken** tootake hello раскадровки изменения интерфейса пользователя в учетную запись:
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. Затем добавьте следующие методы слишком hello**AppDelegate.m** tooretrieve hello изображения от конечной точки и отправить локального уведомление при завершении извлечения. Убедитесь, что заполнитель hello toosubstitute `{backend endpoint}` с серверной конечной точки:
   
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
3. Обрабатывать уведомления локальных hello выше, открыв hello контроллера представление изображения в **AppDelegate.m** с hello следующие методы:
   
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

## <a name="run-hello-application"></a>Запустите приложение hello
1. В XCode запустите приложение hello на устройстве физических операций ввода-вывода (push-уведомлений не будет работать в симуляторе hello).
2. В приложении iOS hello пользовательского интерфейса, введите имя пользователя и пароль hello же для проверки подлинности и нажмите кнопку **входа в**.
3. Щелкните **Отправить push-уведомление** , после чего в приложении появится предупреждение. Если щелкнуть **дополнительные**, можно подключить toohello изображения выбранного tooinclude в серверной части приложения.
4. Можно также щелкнуть **принудительной отправки** и сразу же нажмите кнопку домашней hello вашего устройства. Через несколько секунд вы получите push-уведомление. Если коснуться ее или выберите более будут введены tooyour приложения и hello широкие возможности графического содержимого.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
