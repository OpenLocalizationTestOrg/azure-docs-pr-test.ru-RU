---
title: "Учебник по передаче экстренных новостей в центрах уведомлений: iOS"
description: "Узнайте, как использовать центры уведомлений Azure Service Bus для отправки уведомлений об экстренных новостях на устройства iOS."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: dc47250db6fb3a2853dae24e02bda236154d93fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="7cd9d-103">Использование концентраторов уведомлений для передачи экстренных новостей</span><span class="sxs-lookup"><span data-stu-id="7cd9d-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="7cd9d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="7cd9d-104">Overview</span></span>
<span data-ttu-id="7cd9d-105">В этом разделе показано, как использовать концентраторы уведомлений Azure для рассылки уведомлений об экстренных новостях в приложение iOS.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an iOS app.</span></span> <span data-ttu-id="7cd9d-106">По завершении вы сможете зарегистрироваться в интересующих вас категориях экстренных новостей и получать push-уведомления только для этих категорий.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="7cd9d-107">Данный сценарий является общеупотребимым шаблоном для многих приложений, где требуется отправлять уведомления группам пользователей, ранее проявивших к ним интерес, например, программы чтения RSS, приложений для музыкальных фанатов и т. д.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="7cd9d-108">Широковещательные сценарии реализуются путем включения одного или нескольких *тегов* при создании регистрации в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="7cd9d-109">Если уведомления отправляются на тег, их получают все устройства, зарегистрированные для данного тега.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="7cd9d-110">Поскольку теги представляют собой обычные строки, их не нужно подготавливать заранее.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="7cd9d-111">Дополнительные сведения о тегах см. в статье [Маршрутизация и выражения тегов](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="7cd9d-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cd9d-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7cd9d-112">Prerequisites</span></span>
<span data-ttu-id="7cd9d-113">Материал данной статьи основан на приложении, созданном в разделе по [началу работы с центрами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="7cd9d-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="7cd9d-114">Перед началом работы с данным руководством необходимо выполнить задания руководства по [началу работы с центрами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="7cd9d-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="7cd9d-115">Добавление возможности выбора категорий в приложение</span><span class="sxs-lookup"><span data-stu-id="7cd9d-115">Add category selection to the app</span></span>
<span data-ttu-id="7cd9d-116">Прежде всего, необходимо добавить элементы пользовательского интерфейса для имеющейся раскадровки, позволяющие пользователю выбирать категории для регистрации.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-116">The first step is to add the UI elements to your existing storyboard that enable the user to select categories to register.</span></span> <span data-ttu-id="7cd9d-117">Выбранные пользователем категории хранятся на устройстве.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="7cd9d-118">При запуске приложения в центре уведомлений создается регистрация устройства с выбранными категориями, представленными в форме тегов.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="7cd9d-119">В вашем MainStoryboard_iPhone.storyboard добавьте следующие компоненты из библиотеки объектов:</span><span class="sxs-lookup"><span data-stu-id="7cd9d-119">In your MainStoryboard_iPhone.storyboard add the following components from the object library:</span></span>
   
   * <span data-ttu-id="7cd9d-120">метка с текстом "Экстренные новости";</span><span class="sxs-lookup"><span data-stu-id="7cd9d-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="7cd9d-121">метки с текстами категории "Мир", "Политика", "Бизнес", "Технология", "Наука", "Спорт";</span><span class="sxs-lookup"><span data-stu-id="7cd9d-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="7cd9d-122">Шесть переключателей, по одному в каждой категории. Задайте для каждого переключателя **Состояние** по умолчанию **Off** (Откл.).</span><span class="sxs-lookup"><span data-stu-id="7cd9d-122">Six switches, one per category, set each switch **State** to be **Off** by default.</span></span>
   * <span data-ttu-id="7cd9d-123">Одна кнопка с надписью «Подписка».</span><span class="sxs-lookup"><span data-stu-id="7cd9d-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="7cd9d-124">Раскадровка должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7cd9d-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="7cd9d-125">В редакторе помощника создайте выходы для всех переключателей и назовите их WorldSwitch, PoliticsSwitch, BusinessSwitch, TechnologySwitch, ScienceSwitch, SportsSwitch.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-125">In the assistant editor, create outlets for all the switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="7cd9d-126">Создайте действие для кнопки с названием "Подписка".</span><span class="sxs-lookup"><span data-stu-id="7cd9d-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="7cd9d-127">Файл BreakingNewsViewController.h должен содержать следующее:</span><span class="sxs-lookup"><span data-stu-id="7cd9d-127">Your ViewController.h should contain the following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="7cd9d-128">Создайте класс **Cocoa Touch Class** с именем `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="7cd9d-129">Скопируйте следующий код в интерфейсную часть файла Notifications.h:</span><span class="sxs-lookup"><span data-stu-id="7cd9d-129">Copy the following code in the interface section of the file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="7cd9d-130">Добавьте следующую директиву импорта в Notifications.m:</span><span class="sxs-lookup"><span data-stu-id="7cd9d-130">Add the following import directive to Notifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="7cd9d-131">Скопируйте следующий код в раздел файла Notifications.m, в котором запрограммирована реализация.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-131">Copy the following code in the implementation section of the file Notifications.m.</span></span>
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    <span data-ttu-id="7cd9d-132">Этот класс использует локальное хранилище для хранения и извлечения категорий новостей, которые данное устройство должно получать.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-132">This class uses local storage to store and retrieve the categories of news that this device will receive.</span></span> <span data-ttu-id="7cd9d-133">Он также содержит метод регистрации этих категорий с помощью [шаблонной](notification-hubs-templates-cross-platform-push-messages.md) регистрации.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-133">Also, it contains a method to register for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="7cd9d-134">В файле AppDelegate.h добавьте оператор импорта для Notifications.h и добавьте свойство для экземпляра класса уведомлений:</span><span class="sxs-lookup"><span data-stu-id="7cd9d-134">In the AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of the Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="7cd9d-135">В методе **didFinishLaunchingWithOptions** в файле AppDelegate.m добавьте в начало метода код для инициализации экземпляра уведомления.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-135">In the **didFinishLaunchingWithOptions** method in AppDelegate.m, add the code to initialize the notifications instance at the beginning of the method.</span></span>  
   
    <span data-ttu-id="7cd9d-136">В `HUBNAME` и `HUBLISTENACCESS` (определены в hubinfo.h) заполнители `<hub name>` и `<connection string with listen access>` уже должны быть заменены именем центра уведомлений и строкой подключения для *DefaultListenSharedAccessSignature*, полученными ранее.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have the `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="7cd9d-137">Так как учетные данные, которые распространяются с помощью клиентского приложения, обычно небезопасны, с помощью вашего клиентского приложения следует распространять только ключ для доступа к прослушиванию.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="7cd9d-138">Доступ к прослушиванию позволяет приложению регистрироваться для использования уведомлений, однако при этом нельзя изменять имеющиеся регистрации и отправлять уведомления.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-138">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="7cd9d-139">Полный ключ доступа используется в защищенной серверной службе для отправки уведомлений и смены существующих регистраций.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-139">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="7cd9d-140">В методе **didRegisterForRemoteNotificationsWithDeviceToken** в файле AppDelegate.m замените код метода на указанный ниже код, чтобы переместить маркер устройства в класс уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-140">In the **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace the code in the method with the following code to pass the device token to the notifications class.</span></span> <span data-ttu-id="7cd9d-141">Класс уведомлений выполнит регистрацию получения уведомлений с категориями.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-141">The notifications class will perform the registering for notifications with the categories.</span></span> <span data-ttu-id="7cd9d-142">Если пользователь меняет выбранные категории, для их обновления будет вызван метод `subscribeWithCategories` в ответ на действие кнопки **подписка** .</span><span class="sxs-lookup"><span data-stu-id="7cd9d-142">If the user changes category selections, we call the `subscribeWithCategories` method in response to the **subscribe** button to update them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7cd9d-143">Поскольку маркер устройства, назначенный службой push-уведомлений Apple (APNS), может измениться в любое время, следует регулярно производить регистрацию для использования уведомлений, чтобы предотвратить сбои уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-143">Because the device token assigned by the Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="7cd9d-144">В этом примере регистрация для использования уведомлений осуществляется при каждом запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-144">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="7cd9d-145">Для тех приложений, которые запускаются часто, более одного раза в день, возможно, лучше пропустить регистрацию, чтобы сэкономить трафик, если с момента прошлой регистрации прошло меньше суток.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-145">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves the categories from local storage and requests a registration for these categories
        // each time the app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="7cd9d-146">Обратите внимание, что на данном этапе не должно быть никакого другого кода в методе **didRegisterForRemoteNotificationsWithDeviceToken** .</span><span class="sxs-lookup"><span data-stu-id="7cd9d-146">Note that at this point there should be no other code in the **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="7cd9d-147">Следующие методы должны уже присутствовать в AppDelegate.m завершению [приступить к работе с концентраторами уведомлений] [ get-started] учебника.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-147">The following methods should already be present in AppDelegate.m from completing the [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="7cd9d-148">В противном случае добавьте их.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-148">If not, add them.</span></span>
   
    <span data-ttu-id="7cd9d-149">-(void) {messageText:(NSString *) сообщение MessageBox:(NSString *) заголовка</span><span class="sxs-lookup"><span data-stu-id="7cd9d-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="7cd9d-150">}</span><span class="sxs-lookup"><span data-stu-id="7cd9d-150">}</span></span>
   
   * <span data-ttu-id="7cd9d-151">didReceiveRemoteNotification приложения:(UIApplication *) (void) приложения: (NSDictionary *) userInfo {NSLog (@"% @", сведений о пользователях);   [самостоятельной MessageBox:@"Notification» сообщение: [valueForKey:@"alert [userInfo objectForKey:@"aps»]»]]; }</span><span class="sxs-lookup"><span data-stu-id="7cd9d-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="7cd9d-152">Этот метод обрабатывает уведомления, полученные при запуске приложения, отображая простой **UIAlert**.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-152">This method handles notifications received when the app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="7cd9d-153">В файле ViewController.m добавьте оператор импорта для AppDelegate.h и скопируйте предложенный код в созданный с помощью XCode метод **подписки** .</span><span class="sxs-lookup"><span data-stu-id="7cd9d-153">In ViewController.m, add a import statement for AppDelegate.h and copy the following code into the XCode-generated **subscribe** method.</span></span> <span data-ttu-id="7cd9d-154">Этот код обновляет регистрацию уведомлений для использования тегов новой категории, которые пользователь выбрал в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-154">This code will update the notification registration to use the new category tags the user has chosen in the user interface.</span></span>
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   <span data-ttu-id="7cd9d-155">Этот метод создает список категорий **NSMutableArray** и использует класс **Notifications** для хранения списка в локальном хранилище и регистрации соответствующих тегов в центре уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-155">This method creates an **NSMutableArray** of categories and uses the **Notifications** class to store the list in the local storage and registers the corresponding tags with your notification hub.</span></span> <span data-ttu-id="7cd9d-156">При изменении категорий регистрация создается заново с новыми категориями.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-156">When categories are changed, the registration is recreated with the new categories.</span></span>
3. <span data-ttu-id="7cd9d-157">В файле ViewController.m в метод **viewDidLoad** добавьте предложенный код, чтобы задать пользовательский интерфейс на основе ранее сохраненных категорий.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-157">In ViewController.m, add the following code in the **viewDidLoad** method to set the user interface based on the previously saved categories.</span></span>

        // This updates the UI on startup based on the status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="7cd9d-158">Теперь приложение может сохранять набор категорий в локальном хранилище устройства и использовать его для регистрации в концентраторе уведомлений всякий раз при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-158">The app can now store a set of categories in the device local storage used to register with the notification hub whenever the app starts.</span></span>  <span data-ttu-id="7cd9d-159">Пользователь может изменить выбранные категории во время выполнения и щелкнуть метод **подписки** для обновления регистрации устройства.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-159">The user can change the selection of categories at runtime and click the **subscribe** method to update the registration for the device.</span></span> <span data-ttu-id="7cd9d-160">Далее вы сможете обновить приложение для отправки уведомлений об экстренных новостях непосредственно в состав самого приложения.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-160">Next, you will update the app to send the breaking news notifications directly in the app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="7cd9d-161">(Необязательно.) Отправка уведомлений с тегами</span><span class="sxs-lookup"><span data-stu-id="7cd9d-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="7cd9d-162">Если у вас нет доступа к Visual Studio, можно перейти к следующему разделу и отправлять уведомления из самого приложения.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-162">If you don't have access to Visual Studio, you can skip to the next section and send notifications from the app itself.</span></span> <span data-ttu-id="7cd9d-163">Вы также можете отправлять правильные шаблонные уведомления с [классического портала Azure] с помощью вкладки «Отладка» для центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-163">You can also send the proper template notification from the [Azure Classic Portal] using the debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-the-device"></a><span data-ttu-id="7cd9d-164">(Необязательно.) Отправка уведомлений с устройства</span><span class="sxs-lookup"><span data-stu-id="7cd9d-164">(optional) Send notifications from the device</span></span>
<span data-ttu-id="7cd9d-165">Как правило, уведомления отправляются серверной службой, но вы можете отправлять уведомления об экстренных новостях непосредственно из приложения.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from the app.</span></span> <span data-ttu-id="7cd9d-166">Для этого корпорация Майкрософт будет обновлять `SendNotificationRESTAPI` метод, определенный в [приступить к работе с концентраторами уведомлений] [ get-started] учебника.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-166">To do this we will update the `SendNotificationRESTAPI` method that we defined in the [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="7cd9d-167">В файле ViewController.m обновите метод `SendNotificationRESTAPI` , как показано ниже, чтобы он принимал параметр для тега категории и отправлял правильное [шаблонное](notification-hubs-templates-cross-platform-push-messages.md) уведомление.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-167">In ViewController.m update the `SendNotificationRESTAPI` method as follows so that it accepts a parameter for the category tag and sends the proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
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
2. <span data-ttu-id="7cd9d-168">В файле ViewController.m обновите действие **Отправить уведомление** , как показано в предложенном коде.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-168">In ViewController.m update the **Send Notification** action as shown in the code that follows.</span></span> <span data-ttu-id="7cd9d-169">Таким образом, он будет отправлять уведомления, используя отдельно каждый тег, и отправлять их на несколько платформ.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-169">So that it will send the notifications using each tag individually and send to multiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send the message as breaking news for each category to WNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="7cd9d-170">Повторно создайте проект и убедитесь, что у вас не возникли ошибки сборки.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="7cd9d-171">Запуск приложения и создание уведомлений</span><span class="sxs-lookup"><span data-stu-id="7cd9d-171">Run the app and generate notifications</span></span>
1. <span data-ttu-id="7cd9d-172">Нажмите кнопку Запуск для построения проекта, после чего запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-172">Press the Run button to build the project and start the app.</span></span> <span data-ttu-id="7cd9d-173">Чтобы подписаться на некоторые экстренные новости, нажмите кнопку **Подписаться** .</span><span class="sxs-lookup"><span data-stu-id="7cd9d-173">Select some breaking news options to subscribe to and then press the **Subscribe** button.</span></span> <span data-ttu-id="7cd9d-174">В появившемся диалоговом окне отобразятся те уведомления, на которые была настроена подписка.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-174">You should see a dialog indicating the notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="7cd9d-175">Если выбрано **Подписка**, приложение преобразует выбранные категории в теги и запрашивает у концентратора уведомлений новую регистрацию устройств для выбранных тегов.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-175">When you choose **Subscribe**, the app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span>
2. <span data-ttu-id="7cd9d-176">Введите сообщение, отправляемое в качестве экстренных новостей, и нажмите кнопку **Отправить уведомление** .</span><span class="sxs-lookup"><span data-stu-id="7cd9d-176">Enter a message to be sent as breaking news then press the **Send Notification** button.</span></span> <span data-ttu-id="7cd9d-177">Можно также запустить консольное приложение .NET для создания уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-177">Alternatively, run the .NET console app to generate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="7cd9d-178">Каждое устройство с подпиской на экстренные новости будет получать отправленные вами уведомления об экстренных новостях.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-178">Each device subscribed to breaking news will receive the breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cd9d-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7cd9d-179">Next steps</span></span>
<span data-ttu-id="7cd9d-180">В этом учебнике мы рассмотрели, как производить рассылку экстренных новостей по категориям.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-180">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="7cd9d-181">Далее вам рекомендуется изучить один из следующих учебников, в которых рассматриваются более сложные сценарии использования концентраторов уведомлений:</span><span class="sxs-lookup"><span data-stu-id="7cd9d-181">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="7cd9d-182">**[Использование Центров уведомлений для вещания локализованных экстренных новостей на устройства iOS]**</span><span class="sxs-lookup"><span data-stu-id="7cd9d-182">**[Use Notification Hubs to broadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="7cd9d-183">Как расширить возможности приложения экстренных новостей для отправки локализованных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7cd9d-183">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="7cd9d-184">[Использование Центров уведомлений для вещания локализованных экстренных новостей на устройства iOS]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="7cd9d-184">[Use Notification Hubs to broadcast localized breaking news]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
<span data-ttu-id="7cd9d-185">[классического портала Azure]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="7cd9d-185">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
