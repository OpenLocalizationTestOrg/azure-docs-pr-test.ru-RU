---
title: "aaaNotification концентраторов критические новостей учебника - операций ввода-вывода"
description: "Узнайте, как toosend концентраторы уведомлений Azure Service Bus toouse критические новостей уведомления tooiOS устройств."
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
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="b4451-103">Использование концентраторов уведомлений toosend новости</span><span class="sxs-lookup"><span data-stu-id="b4451-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="b4451-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b4451-104">Overview</span></span>
<span data-ttu-id="b4451-105">В этом разделе показано, как toouse концентраторов уведомлений Azure toobroadcast критические новостей уведомления tooan приложения iOS.</span><span class="sxs-lookup"><span data-stu-id="b4451-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan iOS app.</span></span> <span data-ttu-id="b4451-106">После завершения будет быть может tooregister переноса категории новостей нужных вам и получения только push-уведомлений для этих категорий.</span><span class="sxs-lookup"><span data-stu-id="b4451-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="b4451-107">Этот сценарий представлен общий шаблон для многих приложений, где уведомления состоят из отправленных toobe toogroups пользователей, которым был объявлен ранее интересующих их, например, средство чтения RSS, приложений для вентиляторов музыку и т. д.</span><span class="sxs-lookup"><span data-stu-id="b4451-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="b4451-108">Широковещательный сценарии реализуются путем включения одного или нескольких *теги* при создании регистрации в концентраторе уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="b4451-109">Отправке уведомлений tooa тегов, все устройства, которые зарегистрированы для тега hello получат уведомление hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="b4451-110">Так как теги являются просто строками, у которых нет toobe заранее подготовлены.</span><span class="sxs-lookup"><span data-stu-id="b4451-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="b4451-111">Дополнительные сведения о тегах см. в разделе слишком[маршрутизации концентраторов уведомлений и выражения с тегами](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="b4451-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4451-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b4451-112">Prerequisites</span></span>
<span data-ttu-id="b4451-113">В этом разделе основан на приложение hello, созданный в [приступить к работе с концентраторами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="b4451-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="b4451-114">Перед началом работы с данным руководством необходимо выполнить задания руководства по [началу работы с центрами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="b4451-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="b4451-115">Добавить приложение toohello Выбор категории</span><span class="sxs-lookup"><span data-stu-id="b4451-115">Add category selection toohello app</span></span>
<span data-ttu-id="b4451-116">Hello первым шагом является tooadd hello пользовательского интерфейса элементов tooyour существующей раскадровки, позволяющие tooregister категории tooselect пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-116">hello first step is tooadd hello UI elements tooyour existing storyboard that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="b4451-117">выбранные пользователем категории Hello хранятся на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="b4451-118">При запуске приложение hello регистрацию устройств создается в концентратор уведомлений с категориями hello выбран как теги.</span><span class="sxs-lookup"><span data-stu-id="b4451-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="b4451-119">Добавьте в ваш MainStoryboard_iPhone.storyboard hello следующие компоненты из библиотеки hello объекта.</span><span class="sxs-lookup"><span data-stu-id="b4451-119">In your MainStoryboard_iPhone.storyboard add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="b4451-120">метка с текстом "Экстренные новости";</span><span class="sxs-lookup"><span data-stu-id="b4451-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="b4451-121">метки с текстами категории "Мир", "Политика", "Бизнес", "Технология", "Наука", "Спорт";</span><span class="sxs-lookup"><span data-stu-id="b4451-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="b4451-122">Шесть переключателя, по одному на каждую категорию, задать для каждого ключа **состояние** toobe **Off** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b4451-122">Six switches, one per category, set each switch **State** toobe **Off** by default.</span></span>
   * <span data-ttu-id="b4451-123">Одна кнопка с надписью «Подписка».</span><span class="sxs-lookup"><span data-stu-id="b4451-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="b4451-124">Раскадровка должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b4451-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="b4451-125">В редакторе помощника hello создания выходов для всех коммутаторов hello и вызывать их «WorldSwitch», «PoliticsSwitch», «BusinessSwitch», «TechnologySwitch», «ScienceSwitch», «SportsSwitch»</span><span class="sxs-lookup"><span data-stu-id="b4451-125">In hello assistant editor, create outlets for all hello switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="b4451-126">Создайте действие для кнопки с названием "Подписка".</span><span class="sxs-lookup"><span data-stu-id="b4451-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="b4451-127">Ваш ViewController.h должна содержать hello следующее:</span><span class="sxs-lookup"><span data-stu-id="b4451-127">Your ViewController.h should contain hello following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="b4451-128">Создайте класс **Cocoa Touch Class** с именем `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="b4451-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="b4451-129">Скопируйте следующий код в разделе интерфейса hello hello файла Notifications.h hello:</span><span class="sxs-lookup"><span data-stu-id="b4451-129">Copy hello following code in hello interface section of hello file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="b4451-130">Добавьте следующие директивы tooNotifications.m импорта hello:</span><span class="sxs-lookup"><span data-stu-id="b4451-130">Add hello following import directive tooNotifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="b4451-131">Скопируйте следующий код в разделе реализации hello hello файла Notifications.m hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-131">Copy hello following code in hello implementation section of hello file Notifications.m.</span></span>
   
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



    <span data-ttu-id="b4451-132">Этот класс использует локальное хранилище toostore и получить hello категории новостей, который получит это устройство.</span><span class="sxs-lookup"><span data-stu-id="b4451-132">This class uses local storage toostore and retrieve hello categories of news that this device will receive.</span></span> <span data-ttu-id="b4451-133">Кроме того, он содержит метод tooregister для следующих категорий с помощью [шаблона](notification-hubs-templates-cross-platform-push-messages.md) регистрации.</span><span class="sxs-lookup"><span data-stu-id="b4451-133">Also, it contains a method tooregister for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="b4451-134">В файле AppDelegate.h hello добавьте инструкцию импорта для Notifications.h и добавьте свойство для экземпляра класса уведомлений hello:</span><span class="sxs-lookup"><span data-stu-id="b4451-134">In hello AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of hello Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="b4451-135">В hello **didFinishLaunchingWithOptions** метод в AppDelegate.m, добавить hello кода tooinitialize hello уведомления экземпляр в начале hello метод hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-135">In hello **didFinishLaunchingWithOptions** method in AppDelegate.m, add hello code tooinitialize hello notifications instance at hello beginning of hello method.</span></span>  
   
    <span data-ttu-id="b4451-136">`HUBNAME`и `HUBLISTENACCESS` (определенная в hubinfo.h) уже должна содержать hello `<hub name>` и `<connection string with listen access>` заменой заполнителей уведомления имя и hello строку подключения к концентратору для *DefaultListenSharedAccessSignature*, полученный ранее</span><span class="sxs-lookup"><span data-stu-id="b4451-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have hello `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="b4451-137">Так как учетные данные, которые распространяются с помощью клиентского приложения, обычно не безопасны, hello ключ для прослушивания доступа следует распространять только с помощью клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="b4451-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="b4451-138">Прослушивать доступа включает tooregister вашего приложения для уведомлений, но существующие регистрации нельзя изменить, и не может отправлять уведомления.</span><span class="sxs-lookup"><span data-stu-id="b4451-138">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="b4451-139">Полный доступ Hello используется в защищенной серверной службе для отправки уведомлений и изменять существующие регистрации.</span><span class="sxs-lookup"><span data-stu-id="b4451-139">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="b4451-140">В hello **didRegisterForRemoteNotificationsWithDeviceToken** метод в AppDelegate.m, замените hello код в метод hello hello после уведомления класс маркера toohello устройства кода toopass hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-140">In hello **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace hello code in hello method with hello following code toopass hello device token toohello notifications class.</span></span> <span data-ttu-id="b4451-141">класс уведомления Hello выполнит hello регистрации уведомлений с категориями hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-141">hello notifications class will perform hello registering for notifications with hello categories.</span></span> <span data-ttu-id="b4451-142">При изменении выбора категории hello пользователя мы называем hello `subscribeWithCategories` метода в ответ toohello **подписаться** кнопку tooupdate их.</span><span class="sxs-lookup"><span data-stu-id="b4451-142">If hello user changes category selections, we call hello `subscribeWithCategories` method in response toohello **subscribe** button tooupdate them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b4451-143">Так как в любое время можно вероятность hello токен устройства, назначаемые hello Apple Push Notification Service (APNS), необходимо зарегистрировать для уведомлений часто tooavoid сбоев уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b4451-143">Because hello device token assigned by hello Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="b4451-144">В этом примере регистрируется для уведомления каждый раз при запуске этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-144">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="b4451-145">Для приложений, которые часто выполняются более чем один раз в день, возможно, если можно пропустить пропускной способности toopreserve регистрации менее чем за день прошел с момента предыдущей регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-145">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="b4451-146">Обратите внимание, что на этом этапе следует никакой другой код в hello **didRegisterForRemoteNotificationsWithDeviceToken** метод.</span><span class="sxs-lookup"><span data-stu-id="b4451-146">Note that at this point there should be no other code in hello **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="b4451-147">Hello следующие методы должны уже присутствовать в AppDelegate.m завершению hello [приступить к работе с концентраторами уведомлений] [ get-started] учебника.</span><span class="sxs-lookup"><span data-stu-id="b4451-147">hello following methods should already be present in AppDelegate.m from completing hello [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="b4451-148">В противном случае добавьте их.</span><span class="sxs-lookup"><span data-stu-id="b4451-148">If not, add them.</span></span>
   
    <span data-ttu-id="b4451-149">-(void) {messageText:(NSString *) сообщение MessageBox:(NSString *) заголовка</span><span class="sxs-lookup"><span data-stu-id="b4451-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="b4451-150">}</span><span class="sxs-lookup"><span data-stu-id="b4451-150">}</span></span>
   
   * <span data-ttu-id="b4451-151">didReceiveRemoteNotification приложения:(UIApplication *) (void) приложения: (NSDictionary *) userInfo {NSLog (@"% @", сведений о пользователях);   [самостоятельной MessageBox:@"Notification» сообщение: [valueForKey:@"alert [userInfo objectForKey:@"aps»]»]]; }</span><span class="sxs-lookup"><span data-stu-id="b4451-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="b4451-152">Этот метод отвечает за уведомлений, полученных выполняющейся приложение hello, отображая простой **UIAlert**.</span><span class="sxs-lookup"><span data-stu-id="b4451-152">This method handles notifications received when hello app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="b4451-153">В ViewController.m, добавьте оператор импорта для hello AppDelegate.h и скопируйте следующий код в hello создан XCode **подписаться** метод.</span><span class="sxs-lookup"><span data-stu-id="b4451-153">In ViewController.m, add a import statement for AppDelegate.h and copy hello following code into hello XCode-generated **subscribe** method.</span></span> <span data-ttu-id="b4451-154">Этот код обновит hello уведомления регистрации toouse hello новой категории теги hello пользователь выбрал в пользовательском интерфейсе hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-154">This code will update hello notification registration toouse hello new category tags hello user has chosen in hello user interface.</span></span>
   
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
   
   <span data-ttu-id="b4451-155">Этот метод создает **NSMutableArray** из категории и использует hello **уведомления** список hello toostore классов в hello локального хранилища и регистры hello соответствующие теги в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b4451-155">This method creates an **NSMutableArray** of categories and uses hello **Notifications** class toostore hello list in hello local storage and registers hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="b4451-156">При изменении категории регистрации hello воссоздается при hello новые категории.</span><span class="sxs-lookup"><span data-stu-id="b4451-156">When categories are changed, hello registration is recreated with hello new categories.</span></span>
3. <span data-ttu-id="b4451-157">В ViewController.m, добавьте следующий код в hello hello **viewDidLoad** метод tooset hello пользовательский интерфейс на основе ранее сохраненные hello категорий.</span><span class="sxs-lookup"><span data-stu-id="b4451-157">In ViewController.m, add hello following code in hello **viewDidLoad** method tooset hello user interface based on hello previously saved categories.</span></span>

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="b4451-158">При запуске приложение hello приложение Hello можно хранить набор категорий в hello tooregister локального хранилища используется устройством с концентратором уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-158">hello app can now store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello app starts.</span></span>  <span data-ttu-id="b4451-159">Hello пользователя можно изменить выбор hello категорий во время выполнения и нажмите кнопку hello **подписаться** метод tooupdate hello регистрации для устройства hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-159">hello user can change hello selection of categories at runtime and click hello **subscribe** method tooupdate hello registration for hello device.</span></span> <span data-ttu-id="b4451-160">Далее потребуется обновить hello toosend приложения hello, критические уведомления новостей непосредственно в само приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-160">Next, you will update hello app toosend hello breaking news notifications directly in hello app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="b4451-161">(Необязательно.) Отправка уведомлений с тегами</span><span class="sxs-lookup"><span data-stu-id="b4451-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="b4451-162">Если у вас нет доступа к tooVisual Studio, можно пропустить следующий раздел toohello и отправки уведомления из самого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-162">If you don't have access tooVisual Studio, you can skip toohello next section and send notifications from hello app itself.</span></span> <span data-ttu-id="b4451-163">Также можно отправлять уведомление правильный шаблон hello из hello [классический портал Azure] используя вкладку hello отладки для центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b4451-163">You can also send hello proper template notification from hello [Azure Classic Portal] using hello debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a><span data-ttu-id="b4451-164">(необязательно) Отправлять уведомления с устройства hello</span><span class="sxs-lookup"><span data-stu-id="b4451-164">(optional) Send notifications from hello device</span></span>
<span data-ttu-id="b4451-165">Обычно уведомления будут отправляться с помощью серверной службы, но вы можете отправлять уведомлений с последними новостями непосредственно из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from hello app.</span></span> <span data-ttu-id="b4451-166">toodo это корпорация Майкрософт будет обновлять hello `SendNotificationRESTAPI` метод, определенный в hello [приступить к работе с концентраторами уведомлений] [ get-started] учебника.</span><span class="sxs-lookup"><span data-stu-id="b4451-166">toodo this we will update hello `SendNotificationRESTAPI` method that we defined in hello [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="b4451-167">В обновление hello ViewController.m `SendNotificationRESTAPI` как следует, что принимает в качестве параметра для тега категории hello и отправляет соответствующие hello [шаблона](notification-hubs-templates-cross-platform-push-messages.md) уведомления.</span><span class="sxs-lookup"><span data-stu-id="b4451-167">In ViewController.m update hello `SendNotificationRESTAPI` method as follows so that it accepts a parameter for hello category tag and sends hello proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
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
2. <span data-ttu-id="b4451-168">В обновление hello ViewController.m **отправить уведомление** действие, как показано в далее кода hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-168">In ViewController.m update hello **Send Notification** action as shown in hello code that follows.</span></span> <span data-ttu-id="b4451-169">Чтобы он будет отправлять уведомления hello по отдельности с помощью каждого тега и отправить toomultiple платформы.</span><span class="sxs-lookup"><span data-stu-id="b4451-169">So that it will send hello notifications using each tag individually and send toomultiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="b4451-170">Повторно создайте проект и убедитесь, что у вас не возникли ошибки сборки.</span><span class="sxs-lookup"><span data-stu-id="b4451-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="b4451-171">Запустите приложение hello и создавать уведомления</span><span class="sxs-lookup"><span data-stu-id="b4451-171">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="b4451-172">Нажмите клавишу hello запустите кнопка toobuild hello проект и запустить приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-172">Press hello Run button toobuild hello project and start hello app.</span></span> <span data-ttu-id="b4451-173">Выберите некоторые tooand toosubscribe критические параметры новостей, а затем клавишу hello **Subscribe** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b4451-173">Select some breaking news options toosubscribe tooand then press hello **Subscribe** button.</span></span> <span data-ttu-id="b4451-174">Вы увидите соответствующее диалоговое окно приветствия, которые были подписаны уведомления.</span><span class="sxs-lookup"><span data-stu-id="b4451-174">You should see a dialog indicating hello notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="b4451-175">При выборе **Subscribe**, hello hello выбранных категорий приложений преобразует в теги и запрашивает новую регистрацию устройств для hello выбранных тегов из концентратора уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="b4451-175">When you choose **Subscribe**, hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span>
2. <span data-ttu-id="b4451-176">Введите сообщение toobe, передаются как новости нажмите клавишу hello **отправить уведомление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b4451-176">Enter a message toobe sent as breaking news then press hello **Send Notification** button.</span></span> <span data-ttu-id="b4451-177">Также можно запустить hello .NET консольного приложения toogenerate уведомления.</span><span class="sxs-lookup"><span data-stu-id="b4451-177">Alternatively, run hello .NET console app toogenerate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="b4451-178">Новости toobreaking каждого устройства подписка получит hello уведомлений с последними новостями который только что отправлен.</span><span class="sxs-lookup"><span data-stu-id="b4451-178">Each device subscribed toobreaking news will receive hello breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4451-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b4451-179">Next steps</span></span>
<span data-ttu-id="b4451-180">В этом учебнике мы узнали, каким образом toobroadcast новости по категориям.</span><span class="sxs-lookup"><span data-stu-id="b4451-180">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="b4451-181">Рассмотрим, выполнив одну из hello следующие учебники, выделите других расширенных сценариях концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b4451-181">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="b4451-182">**[Использовать локализованные toobroadcast новости концентраторы уведомлений]**</span><span class="sxs-lookup"><span data-stu-id="b4451-182">**[Use Notification Hubs toobroadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="b4451-183">Узнайте, как критические отправки tooenable новостей приложения hello tooexpand локализованные уведомления.</span><span class="sxs-lookup"><span data-stu-id="b4451-183">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Использовать локализованные toobroadcast новости концентраторы уведомлений]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[классический портал Azure]: https://manage.windowsazure.com
