---
title: "tooiOS уведомления aaaSending принудительной с концентраторами уведомлений Azure | Документы Microsoft"
description: "В этом учебнике вы узнаете, как toosend toouse концентраторов уведомлений Azure push-уведомления tooan операций ввода-вывода приложения."
services: notification-hubs
documentationcenter: ios
keywords: "push-уведомление, push-уведомления, push-уведомления node.js, push-уведомления ios"
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a><span data-ttu-id="41a15-104">Отправка push tooiOS уведомлений с концентраторами уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="41a15-104">Sending push notifications tooiOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="41a15-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="41a15-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="41a15-106">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="41a15-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="41a15-107">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="41a15-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="41a15-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="41a15-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="41a15-109">Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомлений приложения iOS tooan.</span><span class="sxs-lookup"><span data-stu-id="41a15-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span> <span data-ttu-id="41a15-110">Вы создадите пустого приложения iOS, получающий push-уведомления с помощью hello [службы Push-уведомления Apple (APN)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="41a15-110">You'll create a blank iOS app that receives push notifications by using hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="41a15-111">После завершения вы будете иметь доступ toouse вашей toobroadcast концентратора уведомлений push-уведомления tooall hello устройств под управлением приложения.</span><span class="sxs-lookup"><span data-stu-id="41a15-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="41a15-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="41a15-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="41a15-113">код завершения Hello в этом учебнике можно найти [на GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="41a15-113">hello completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="41a15-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="41a15-114">Prerequisites</span></span>
<span data-ttu-id="41a15-115">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="41a15-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="41a15-116">[мобильных служб iOS SDK версии 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="41a15-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="41a15-117">последняя версия [Xcode]</span><span class="sxs-lookup"><span data-stu-id="41a15-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="41a15-118">устройство с iOS 8 (или более поздней версии);</span><span class="sxs-lookup"><span data-stu-id="41a15-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="41a15-119">[программе для разработчиков на платформе Apple](https://developer.apple.com/programs/) .</span><span class="sxs-lookup"><span data-stu-id="41a15-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="41a15-120">Из-за требования к конфигурации для push-уведомлений необходимо развернуть и проверить push-уведомления на устройстве физических операций ввода-вывода (iPhone и iPad) вместо симулятор iOS hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of hello iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="41a15-121">Изучение этого руководства является необходимым условием для работы со всеми другими руководствами, посвященными Центрам уведомлений для приложений iOS.</span><span class="sxs-lookup"><span data-stu-id="41a15-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="41a15-122">Настройка push-уведомлений iOS в центре уведомлений </span><span class="sxs-lookup"><span data-stu-id="41a15-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="41a15-123">В этом подразделе содержатся описано создание нового концентратора уведомлений и настройка проверки подлинности с помощью hello APNS **.p12** созданный сертификат push.</span><span class="sxs-lookup"><span data-stu-id="41a15-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="41a15-124">Если вы хотите toouse концентратор уведомлений, который уже создан, можно пропустить toostep 5.</span><span class="sxs-lookup"><span data-stu-id="41a15-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="41a15-125">Нажмите кнопку hello <b>служб Notification Services</b> кнопку в hello <b>параметры</b> колонке выберите <b>Apple (APN)</b>.</span><span class="sxs-lookup"><span data-stu-id="41a15-125">Click hello <b>Notification Services</b> button in hello <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="41a15-126">Щелкните <b>передать сертификат</b> и выберите hello <b>.p12</b> файл, экспортированный ранее.</span><span class="sxs-lookup"><span data-stu-id="41a15-126">Click on <b>Upload Certificate</b> and select hello <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="41a15-127">Убедитесь, что также указать правильный пароль hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-127">Make sure you also specify hello correct password.</span></span></p>

<p><span data-ttu-id="41a15-128">Убедитесь, что tooselect <b>"песочницы"</b> режиме, так как это для разработки приложений.</span><span class="sxs-lookup"><span data-stu-id="41a15-128">Make sure tooselect <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="41a15-129">Использовать только hello <b>рабочей</b> Если toosend принудительной уведомления toousers купившего приложения из магазина hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-129">Only use hello <b>Production</b> if you want toosend push notifications toousers who purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="41a15-130">&emsp;&emsp;&emsp;&emsp;![Настройка APNS на портале Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="41a15-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Настройка сертификации APNS на портале Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="41a15-132">Концентратор уведомлений теперь настроенные toowork в APNS, и вы tooregister строки подключения hello приложения и отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="41a15-132">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-toonotification-hubs"></a><span data-ttu-id="41a15-133">Подключение к tooNotification приложения iOS концентраторы</span><span class="sxs-lookup"><span data-stu-id="41a15-133">Connect your iOS app tooNotification Hubs</span></span>
1. <span data-ttu-id="41a15-134">В Xcode, создайте новый проект iOS и выберите hello **одним приложением представление** шаблона.</span><span class="sxs-lookup"><span data-stu-id="41a15-134">In Xcode, create a new iOS project and select hello **Single View Application** template.</span></span>
   
    ![Xcode — приложение с одним представлением][8]
    
2. <span data-ttu-id="41a15-136">При установке hello параметров для нового проекта, убедитесь, что toouse hello же **название продукта** и **идентификатор организации** , которые использовались при установленные ранее ИД набора hello hello разработчиков Apple портал.</span><span class="sxs-lookup"><span data-stu-id="41a15-136">When setting hello options for your new project, make sure toouse hello same **Product Name** and **Organization Identifier** that you used when you previously set hello bundle ID on hello Apple Developer portal.</span></span>
   
    ![Xcode — параметры проекта][11]
    
3. <span data-ttu-id="41a15-138">В разделе **цели**, щелкните имя проекта, hello **параметры построения** и разверните **удостоверения подписывания кода**и затем в разделе **отладки**, установить вашу личность подписи кода.</span><span class="sxs-lookup"><span data-stu-id="41a15-138">Under **Targets**, click your project name, click hello **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="41a15-139">Переключить **уровни** из **основные** слишком**все**и задайте **профиль подготовки** toohello подготовительного профиля, который вы создали ранее .</span><span class="sxs-lookup"><span data-stu-id="41a15-139">Toggle **Levels** from **Basic** too**All**, and set **Provisioning Profile** toohello provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="41a15-140">Если вы не видите hello новый профиль подготовки, вы создали в Xcode, обновите профили hello удостоверение подписывания.</span><span class="sxs-lookup"><span data-stu-id="41a15-140">If you don't see hello new provisioning profile that you created in Xcode, try refreshing hello profiles for your signing identity.</span></span> <span data-ttu-id="41a15-141">Нажмите кнопку **Xcode** hello меню, нажмите кнопку **предпочтения**, щелкните hello **учетной записи** щелкните hello **Просмотр сведений о** , выберите элемент к удостоверение подписывания, а затем нажмите кнопку обновления hello в нижнем правом углу hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-141">Click **Xcode** on hello menu bar, click **Preferences**, click hello **Account** tab, click hello **View Details** button, click your signing identity, and then click hello refresh button in hello bottom-right corner.</span></span>
   
    ![Xcode — профиль подготовки][9]
4. <span data-ttu-id="41a15-143">Загрузите hello [мобильных служб iOS SDK версии 1.2.4] и распакуйте файл hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-143">Download hello [Mobile Services iOS SDK version 1.2.4] and unzip hello file.</span></span> <span data-ttu-id="41a15-144">В Xcode, щелкните правой кнопкой мыши проект и нажмите кнопку hello **добавить файлы для** hello параметр tooadd **WindowsAzureMessaging.framework** проекту Xcode tooyour папки.</span><span class="sxs-lookup"><span data-stu-id="41a15-144">In Xcode, right-click your project and click hello **Add Files to** option tooadd hello **WindowsAzureMessaging.framework** folder tooyour Xcode project.</span></span> <span data-ttu-id="41a15-145">Выберите **Copy items if needed** (Копировать элементы при необходимости), а затем щелкните **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="41a15-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="41a15-146">концентраторы уведомлений Hello SDK не поддерживает bitcode в Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="41a15-146">hello notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="41a15-147">Необходимо задать **включить Bitcode** слишком**нет** в hello **параметры сборки** для проекта.</span><span class="sxs-lookup"><span data-stu-id="41a15-147">You must set **Enable Bitcode** too**No** in hello **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Распаковка пакета SDK Azure][10]
5. <span data-ttu-id="41a15-149">Добавить новый заголовок tooyour проект файл с именем `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="41a15-149">Add a new header file tooyour project named `HubInfo.h`.</span></span> <span data-ttu-id="41a15-150">Этот файл будет содержать hello константы для центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="41a15-150">This file will hold hello constants for your notification hub.</span></span>  <span data-ttu-id="41a15-151">Добавьте следующие определения hello и замените hello строка литерала местозаполнителей вашей *имя концентратора* и hello *DefaultListenSharedAccessSignature* записанные ранее.</span><span class="sxs-lookup"><span data-stu-id="41a15-151">Add hello following definitions and replace hello string literal placeholders with your *hub name* and hello *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="41a15-152">Откройте ваш `AppDelegate.h` файла добавьте следующие директивы импорта hello:</span><span class="sxs-lookup"><span data-stu-id="41a15-152">Open your `AppDelegate.h` file add hello following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="41a15-153">В вашей `AppDelegate.m file`, добавьте следующий код в hello hello `didFinishLaunchingWithOptions` метода, основанного на версии iOS.</span><span class="sxs-lookup"><span data-stu-id="41a15-153">In your `AppDelegate.m file`, add hello following code in hello `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="41a15-154">Этот код регистрирует маркер вашего устройства в APNs.</span><span class="sxs-lookup"><span data-stu-id="41a15-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="41a15-155">Для iOS 8:</span><span class="sxs-lookup"><span data-stu-id="41a15-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="41a15-156">Для too8 предыдущих версий iOS:</span><span class="sxs-lookup"><span data-stu-id="41a15-156">For iOS versions prior too8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="41a15-157">В hello того же файла, добавьте следующие методы hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-157">In hello same file, add hello following methods.</span></span> <span data-ttu-id="41a15-158">Он подключает toohello концентратор уведомлений, используя сведения о соединении hello, указанной в HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="41a15-158">This code connects toohello notification hub using hello connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="41a15-159">Затем он предоставляет концентратора уведомлений маркера toohello hello устройства, чтобы hello концентратора уведомлений можно отправлять уведомления:</span><span class="sxs-lookup"><span data-stu-id="41a15-159">It then gives hello device token toohello notification hub so that hello notification hub can send notifications:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. <span data-ttu-id="41a15-160">В hello того же файла, добавьте следующий метод toodisplay hello **UIAlert** Если hello уведомление получено во время активного приложение hello:</span><span class="sxs-lookup"><span data-stu-id="41a15-160">In hello same file, add hello following method toodisplay a **UIAlert** if hello notification is received while hello app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="41a15-161">Постройте и запустите приложение hello на tooverify вашего устройства, не сбоя.</span><span class="sxs-lookup"><span data-stu-id="41a15-161">Build and run hello app on your device tooverify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="41a15-162">Отправка тестовых push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="41a15-162">Send test push notifications</span></span>
<span data-ttu-id="41a15-163">Можно проверить получение уведомлений в приложение, отправляя push-уведомлений в hello [портала Azure] через hello **Устранение неполадок** раздел в колонке hello концентратора (использовать hello *Тестовая отправка* параметр).</span><span class="sxs-lookup"><span data-stu-id="41a15-163">You can test receiving notifications in your app by sending push notifications in hello [Azure Portal] via hello **Troubleshooting** section in hello hub blade (use hello *Test Send* option).</span></span>

![Портал Azure — тестовая отправка][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a><span data-ttu-id="41a15-165">(Необязательно) Отправлять push-уведомления из приложения hello</span><span class="sxs-lookup"><span data-stu-id="41a15-165">(Optional) Send push notifications from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="41a15-166">В этом примере отправки уведомлений из клиентского приложения hello предоставляется только в целях обучения.</span><span class="sxs-lookup"><span data-stu-id="41a15-166">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="41a15-167">Так как для этого потребуется hello `DefaultFullSharedAccessSignature` toobe на клиентское приложение hello, он предоставляет, пользователь может получить уведомления toosend несанкционированный доступ клиентов tooyour риск toohello концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="41a15-167">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="41a15-168">Следует toosend push-уведомления в приложения в этом разделе приведен пример того, как toodo это с помощью интерфейса REST "hello".</span><span class="sxs-lookup"><span data-stu-id="41a15-168">If you want toosend push notifications from within an app, this section provides an example of how toodo this using hello REST interface.</span></span>

1. <span data-ttu-id="41a15-169">Откройте в Xcode, `Main.storyboard` и добавьте следующие компоненты пользовательского интерфейса из hello объекта библиотеки tooallow hello пользователя toosend push-уведомлений в приложение hello hello:</span><span class="sxs-lookup"><span data-stu-id="41a15-169">In Xcode, open `Main.storyboard` and add hello following UI components from hello object library tooallow hello user toosend push notifications in hello app:</span></span>
   
   * <span data-ttu-id="41a15-170">Метка без текста.</span><span class="sxs-lookup"><span data-stu-id="41a15-170">A label with no label text.</span></span> <span data-ttu-id="41a15-171">Он будет иметь ошибки используется tooreport в отправке уведомлений.</span><span class="sxs-lookup"><span data-stu-id="41a15-171">It will be used tooreport errors in sending notifications.</span></span> <span data-ttu-id="41a15-172">Hello **строки** свойство должно быть установлено слишком**0** , будет автоматически подогнана право ограниченного toohello и левого полей и hello верхней части представления hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-172">hello **Lines** property should be set too**0** so that it will automatically size constrained toohello right and left margins and hello top of hello view.</span></span>
   * <span data-ttu-id="41a15-173">Текстовое поле с **заполнитель** текст задан слишком**введите сообщение уведомления**.</span><span class="sxs-lookup"><span data-stu-id="41a15-173">A text field with **Placeholder** text set too**Enter Notification Message**.</span></span> <span data-ttu-id="41a15-174">Ограничить hello поле непосредственно под hello метки, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="41a15-174">Constrain hello field just below hello label as shown below.</span></span> <span data-ttu-id="41a15-175">Установите в качестве делегата розетки hello hello View Controller.</span><span class="sxs-lookup"><span data-stu-id="41a15-175">Set hello View Controller as hello outlet delegate.</span></span>
   * <span data-ttu-id="41a15-176">Кнопка под названием **отправить уведомление** ограниченного под hello текстовое поле и в середине hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-176">A button titled **Send Notification** constrained just below hello text field and in hello horizontal center.</span></span>
     
     <span data-ttu-id="41a15-177">представление Hello должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="41a15-177">hello view should look as follows:</span></span>
     
     ![Конструктор Xcode][32]
2. <span data-ttu-id="41a15-179">[Добавить торговцам](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) hello подпись и текстовое поле с подключением просмотра и обновление вашей `interface` toosupport определения `UITextFieldDelegate` и `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="41a15-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for hello label and text field connected your view, and update your `interface` definition toosupport `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="41a15-180">Добавьте три свойства объявления hello показано ниже toohelp поддержки вызов API-интерфейса REST hello и анализе ответа hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-180">Add hello three property declarations shown below toohelp support calling hello REST API and parsing hello response.</span></span>
   
    <span data-ttu-id="41a15-181">Ваш файл ViewController.h должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="41a15-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="41a15-182">Откройте `HubInfo.h` и добавьте следующие константы, которые будут использоваться для отправки уведомлений tooyour концентратора hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-182">Open `HubInfo.h` and add hello following constants which will be used for sending notifications tooyour hub.</span></span> <span data-ttu-id="41a15-183">Замените hello заполнитель строковый литерал реальный *DefaultFullSharedAccessSignature* строку подключения.</span><span class="sxs-lookup"><span data-stu-id="41a15-183">Replace hello placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="41a15-184">Добавьте следующее hello `#import` tooyour инструкций `ViewController.h` файла.</span><span class="sxs-lookup"><span data-stu-id="41a15-184">Add hello following `#import` statements tooyour `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="41a15-185">В `ViewController.m` добавить после реализации интерфейса toohello кода hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-185">In `ViewController.m` add hello following code toohello interface implementation.</span></span> <span data-ttu-id="41a15-186">Этот код будет анализировать строку подключения *DefaultFullSharedAccessSignature*.</span><span class="sxs-lookup"><span data-stu-id="41a15-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="41a15-187">Как упоминалось в hello [Справочник по REST API](http://msdn.microsoft.com/library/azure/dn495627.aspx), этот проанализированный сведения будут использоваться toogenerate маркер SaS для hello **авторизации** заголовка запроса.</span><span class="sxs-lookup"><span data-stu-id="41a15-187">As mentioned in hello [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used toogenerate a SaS token for hello **Authorization** request header.</span></span>
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. <span data-ttu-id="41a15-188">В `ViewController.m`, обновление hello `viewDidLoad` строка подключения tooparse hello метод при загрузке представления hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-188">In `ViewController.m`, update hello `viewDidLoad` method tooparse hello connection string when hello view loads.</span></span> <span data-ttu-id="41a15-189">Также добавьте hello служебные методы, показанный ниже, toohello реализацию интерфейса.</span><span class="sxs-lookup"><span data-stu-id="41a15-189">Also add hello utility methods, shown below, toohello interface implementation.</span></span>  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. <span data-ttu-id="41a15-190">В `ViewController.m`, добавьте следующий код toohello интерфейса реализации toogenerate hello авторизации маркер SaS, предоставляемого hello hello **авторизации** заголовок, как упоминалось в hello [API-интерфейса REST Справочник по](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="41a15-190">In `ViewController.m`, add hello following code toohello interface implementation toogenerate hello SaS authorization token that will be provided in hello **Authorization** header, as mentioned in hello [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. <span data-ttu-id="41a15-191">Здравствуйте, клавишу CTRL при перетаскивании из **отправить уведомление** кнопку слишком`ViewController.m` tooadd действие с именем **SendNotificationMessage** для hello **Touch вниз** событий.</span><span class="sxs-lookup"><span data-stu-id="41a15-191">Ctrl+drag from hello **Send Notification** button too`ViewController.m` tooadd an action named **SendNotificationMessage** for hello **Touch Down** event.</span></span> <span data-ttu-id="41a15-192">Метод обновления с hello, следующий код toosend hello уведомления с помощью API-интерфейса REST hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-192">Update method with hello following code toosend hello notification using hello REST API.</span></span>
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. <span data-ttu-id="41a15-193">В `ViewController.m`, добавить следующие toosupport метод делегата, закрытие hello клавиатуры для текстового поля hello hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-193">In `ViewController.m`, add hello following delegate method toosupport closing hello keyboard for hello text field.</span></span> <span data-ttu-id="41a15-194">CTRL + перетащите значок hello текстовое поле toohello View Controller в hello интерфейса конструктора tooset hello Просмотр контроллера как hello выхода делегата.</span><span class="sxs-lookup"><span data-stu-id="41a15-194">Ctrl+drag from hello text field toohello View Controller icon in hello interface designer tooset hello view controller as hello outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="41a15-195">В `ViewController.m`, добавьте следующее hello делегировать методы toosupport анализа hello ответа с помощью `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="41a15-195">In `ViewController.m`, add hello following delegate methods toosupport parsing hello response by using `NSXMLParser`.</span></span>
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="41a15-196">Постройте проект hello и убедитесь, что отсутствуют ошибки.</span><span class="sxs-lookup"><span data-stu-id="41a15-196">Build hello project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="41a15-197">Если возникли ошибка сборки в Xcode7 о поддержке bitcode, следует изменить hello **параметры построения** > **включить Bitcode (ENABLE_BITCODE)** слишком**нет** в Xcode.</span><span class="sxs-lookup"><span data-stu-id="41a15-197">If you encounter a build error in Xcode7 about bitcode support, you should change hello **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** too**NO** in Xcode.</span></span> <span data-ttu-id="41a15-198">Hello SDK концентраторов уведомлений в настоящее время не поддерживает bitcode.</span><span class="sxs-lookup"><span data-stu-id="41a15-198">hello Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="41a15-199">Можно найти все полезные данные уведомления возможных hello hello Apple [локальный и Push-уведомлений руководство по программированию на].</span><span class="sxs-lookup"><span data-stu-id="41a15-199">You can find all hello possible notification payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="41a15-200">Проверка того, может ли ваше приложение получать push-уведомления</span><span class="sxs-lookup"><span data-stu-id="41a15-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="41a15-201">tootest push-уведомления на iOS, необходимо развернуть устройство физических операций ввода-вывода tooa приложения hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-201">tootest push notifications on iOS, you must deploy hello app tooa physical iOS device.</span></span> <span data-ttu-id="41a15-202">Не удается отправить push-уведомлений Apple с помощью симулятора iOS hello.</span><span class="sxs-lookup"><span data-stu-id="41a15-202">You cannot send Apple push notifications by using hello iOS Simulator.</span></span>

1. <span data-ttu-id="41a15-203">Запустите приложение hello и убедитесь, что регистрация выполняется успешно и нажмите клавишу **ОК**.</span><span class="sxs-lookup"><span data-stu-id="41a15-203">Run hello app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![Проверка регистрации push-уведомления приложения iOS][33]
2. <span data-ttu-id="41a15-205">Можно отправить тестовое push-уведомление от hello [портала Azure], как описано выше.</span><span class="sxs-lookup"><span data-stu-id="41a15-205">You can send a test push notification from hello [Azure Portal], as described above.</span></span> <span data-ttu-id="41a15-206">Если вы добавили код для отправки push-уведомлений в приложение hello, коснитесь внутри tooenter поле текст hello сообщение уведомления.</span><span class="sxs-lookup"><span data-stu-id="41a15-206">If you added code for sending push notifications in hello app, touch inside hello text field tooenter a notification message.</span></span> <span data-ttu-id="41a15-207">Нажмите клавишу hello **отправки** кнопку на клавиатуре hello или hello **отправить уведомление** кнопку в приветственное сообщение hello представление toosend уведомления.</span><span class="sxs-lookup"><span data-stu-id="41a15-207">Then press hello **Send** button on hello keyboard or hello **Send Notification** button in hello view toosend hello notification message.</span></span>
   
    ![Проверка отправки push-уведомления приложения iOS][34]
3. <span data-ttu-id="41a15-209">Hello push-уведомление отправляется tooall устройства, зарегистрированные tooreceive hello уведомления от hello конкретного концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="41a15-209">hello push notification is sent tooall devices that are registered tooreceive hello notifications from hello particular Notification Hub.</span></span>
   
    ![Проверка получения push-уведомления приложения iOS][35]

## <a name="next-steps"></a><span data-ttu-id="41a15-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="41a15-211">Next steps</span></span>
<span data-ttu-id="41a15-212">В этом простом примере вы широковещательной рассылки push уведомления tooall устройства iOS, зарегистрированных.</span><span class="sxs-lookup"><span data-stu-id="41a15-212">In this simple example, you broadcasted push notifications tooall your registered iOS devices.</span></span> <span data-ttu-id="41a15-213">Мы советуем использовать на следующем шаге в продолжении toohello обучением [уведомления концентраторы уведомления пользователей Azure для iOS с серверной части .NET] руководство, в котором будет пошаговое описание создания push toosend внутренних уведомлений с помощью тегов.</span><span class="sxs-lookup"><span data-stu-id="41a15-213">We suggest as a next step in your learning that you proceed toohello [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend toosend push notifications using tags.</span></span> 

<span data-ttu-id="41a15-214">Если требуется toosegment пользователи, группы интересов, можно дополнительно переместить на toohello [toosend использования концентраторов уведомлений, новости] учебника.</span><span class="sxs-lookup"><span data-stu-id="41a15-214">If you want toosegment your users by interest groups, you can additionally move on toohello [Use Notification Hubs toosend breaking news] tutorial.</span></span> 

<span data-ttu-id="41a15-215">Общие сведения о Центрах уведомлений см. [здесь].</span><span class="sxs-lookup"><span data-stu-id="41a15-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[мобильных служб iOS SDK версии 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[здесь]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[уведомления концентраторы уведомления пользователей Azure для iOS с серверной части .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[toosend использования концентраторов уведомлений, новости]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[локальный и Push-уведомлений руководство по программированию на]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[портала Azure]: https://portal.azure.com
