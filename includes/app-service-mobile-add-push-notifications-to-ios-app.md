
<span data-ttu-id="9e1a7-101">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="9e1a7-101">**Objective-C**:</span></span>

1. <span data-ttu-id="9e1a7-102">В **QSAppDelegate.m** импортируйте пакет SDK для iOS и **QSTodoService.h**:</span><span class="sxs-lookup"><span data-stu-id="9e1a7-102">In **QSAppDelegate.m**, import the iOS SDK and **QSTodoService.h**:</span></span>
   
        #import <MicrosoftAzureMobile/MicrosoftAzureMobile.h>
        #import "QSTodoService.h"
2. <span data-ttu-id="9e1a7-103">В коде `didFinishLaunchingWithOptions` в **QSAppDelegate.m** вставьте следующие строки прямо перед `return YES;`:</span><span class="sxs-lookup"><span data-stu-id="9e1a7-103">In `didFinishLaunchingWithOptions` in **QSAppDelegate.m**, insert the following lines right before `return YES;`:</span></span>
   
        UIUserNotificationSettings* notificationSettings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeAlert | UIUserNotificationTypeBadge | UIUserNotificationTypeSound categories:nil];
        [[UIApplication sharedApplication] registerUserNotificationSettings:notificationSettings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
3. <span data-ttu-id="9e1a7-104">В **QSAppDelegate.m**добавьте приведенные ниже методы обработчика.</span><span class="sxs-lookup"><span data-stu-id="9e1a7-104">In **QSAppDelegate.m**, add the following handler methods.</span></span> <span data-ttu-id="9e1a7-105">Ваше приложение теперь обновлено для поддержки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="9e1a7-105">Your app is now updated to support push notifications.</span></span> 
   
        // Registration with APNs is successful
        - (void)application:(UIApplication *)application
        didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
   
            QSTodoService *todoService = [QSTodoService defaultService];
            MSClient *client = todoService.client;
   
            [client.push registerDeviceToken:deviceToken completion:^(NSError *error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
            }];
        }
   
        // Handle any failure to register
        - (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:
        (NSError *)error {
            NSLog(@"Failed to register for remote notifications: %@", error);
        }
   
        // Use userInfo in the payload to display an alert.
        - (void)application:(UIApplication *)application
              didReceiveRemoteNotification:(NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
   
            NSDictionary *apsPayload = userInfo[@"aps"];
            NSString *alertString = apsPayload[@"alert"];
   
            // Create alert with notification content.
            UIAlertController *alertController = [UIAlertController
                                          alertControllerWithTitle:@"Notification"
                                          message:alertString
                                          preferredStyle:UIAlertControllerStyleAlert];
   
            UIAlertAction *cancelAction = [UIAlertAction
                                           actionWithTitle:NSLocalizedString(@"Cancel", @"Cancel")
                                           style:UIAlertActionStyleCancel
                                           handler:^(UIAlertAction *action)
                                           {
                                               NSLog(@"Cancel");
                                           }];
   
            UIAlertAction *okAction = [UIAlertAction
                                       actionWithTitle:NSLocalizedString(@"OK", @"OK")
                                       style:UIAlertActionStyleDefault
                                       handler:^(UIAlertAction *action)
                                       {
                                           NSLog(@"OK");
                                       }];
   
            [alertController addAction:cancelAction];
            [alertController addAction:okAction];
   
            // Get current view controller.
            UIViewController *currentViewController = [[[[UIApplication sharedApplication] delegate] window] rootViewController];
            while (currentViewController.presentedViewController)
            {
                currentViewController = currentViewController.presentedViewController;
            }
   
            // Display alert.
            [currentViewController presentViewController:alertController animated:YES completion:nil];
   
        }

<span data-ttu-id="9e1a7-106">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="9e1a7-106">**Swift**:</span></span>

1. <span data-ttu-id="9e1a7-107">Добавьте файл **ClientManager.swift** со следующим содержимым.</span><span class="sxs-lookup"><span data-stu-id="9e1a7-107">Add file **ClientManager.swift** with the following contents.</span></span> <span data-ttu-id="9e1a7-108">Замените *%AppUrl%* на URL-адрес внутреннего сервера мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="9e1a7-108">Replace *%AppUrl%* with the URL of the Azure Mobile App backend.</span></span>
   
        class ClientManager {
            static let sharedClient = MSClient(applicationURLString: "%AppUrl%")
        }
2. <span data-ttu-id="9e1a7-109">В **ToDoTableViewController.swift** замените строку `let client`, которая инициализирует `MSClient`, на следующую:</span><span class="sxs-lookup"><span data-stu-id="9e1a7-109">In **ToDoTableViewController.swift**, replace the `let client` line that initializes an `MSClient` with this line:</span></span>
   
        let client = ClientManager.sharedClient
3. <span data-ttu-id="9e1a7-110">В **AppDelegate.swift** замените текст `func application` на следующий:</span><span class="sxs-lookup"><span data-stu-id="9e1a7-110">In **AppDelegate.swift**, replace the body of `func application` as follows:</span></span>
   
        func application(application: UIApplication,
          didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
           application.registerUserNotificationSettings(
               UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound],
                   categories: nil))
           application.registerForRemoteNotifications()
           return true
        }
4. <span data-ttu-id="9e1a7-111">В **QSAppDelegate.m**добавьте приведенные ниже методы обработчика.</span><span class="sxs-lookup"><span data-stu-id="9e1a7-111">In **AppDelegate.swift**, add the following handler methods.</span></span> <span data-ttu-id="9e1a7-112">Ваше приложение теперь обновлено для поддержки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="9e1a7-112">Your app is now updated to support push notifications.</span></span>
   
        func application(application: UIApplication,
           didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
            ClientManager.sharedClient.push?.registerDeviceToken(deviceToken) { error in
                print("Error registering for notifications: ", error?.description)
            }
        }
   
        func application(application: UIApplication,
           didFailToRegisterForRemoteNotificationsWithError error: NSError) {
            print("Failed to register for remote notifications: ", error.description)
        }
   
        func application(application: UIApplication,
           didReceiveRemoteNotification userInfo: [NSObject: AnyObject]) {
   
            print(userInfo)
   
            let apsNotification = userInfo["aps"] as? NSDictionary
            let apsString       = apsNotification?["alert"] as? String
   
            let alert = UIAlertController(title: "Alert", message: apsString, preferredStyle: .Alert)
            let okAction = UIAlertAction(title: "OK", style: .Default) { _ in
                print("OK")
            }
            let cancelAction = UIAlertAction(title: "Cancel", style: .Default) { _ in
                print("Cancel")
            }
   
            alert.addAction(okAction)
            alert.addAction(cancelAction)
   
            var currentViewController = self.window?.rootViewController
            while currentViewController?.presentedViewController != nil {
                currentViewController = currentViewController?.presentedViewController
            }
   
            currentViewController?.presentViewController(alert, animated: true) {}
   
        }

