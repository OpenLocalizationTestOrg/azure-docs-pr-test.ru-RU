---
title: "aaaAdd принудительной уведомления tooyour Xamarin.Forms приложения | Документы Microsoft"
description: "Узнайте, как toouse Azure служб toosend несколькими платформами принудительной уведомления tooyour Xamarin.Forms приложений."
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 9133a0b6dd99c01def525607c20ce5a9c19b9502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a><span data-ttu-id="433b0-103">Добавить приложение Xamarin.Forms tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="433b0-103">Add push notifications tooyour Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="433b0-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="433b0-104">Overview</span></span>
<span data-ttu-id="433b0-105">В этом учебнике добавить push tooall уведомления hello проекты, полученные из hello [Xamarin.Forms краткого](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="433b0-105">In this tutorial, you add push notifications tooall hello projects that resulted from hello [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="433b0-106">Это означает, что push-уведомление отправляется tooall кросс платформенных клиентов, каждый раз при вставке записи.</span><span class="sxs-lookup"><span data-stu-id="433b0-106">This means that a push notification is sent tooall cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="433b0-107">Если вы не используете hello загружен проект быстрый запуск сервера, будет необходимо hello пакета расширения уведомлений push.</span><span class="sxs-lookup"><span data-stu-id="433b0-107">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="433b0-108">Дополнительные сведения см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="433b0-108">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="433b0-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="433b0-109">Prerequisites</span></span>
<span data-ttu-id="433b0-110">Для iOS потребуется [участие в программе для разработчиков на платформе Apple](https://developer.apple.com/programs/ios/) и физическое устройство iOS.</span><span class="sxs-lookup"><span data-stu-id="433b0-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="433b0-111">Hello [симулятор iOS не поддерживает push-уведомления](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="433b0-111">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="433b0-112"><a name="configure-hub"></a>Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="433b0-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="433b0-113">Обновить hello server проекта toosend push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="433b0-113">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a><span data-ttu-id="433b0-114">Настройка и выполнение проекта Android hello (необязательно)</span><span class="sxs-lookup"><span data-stu-id="433b0-114">Configure and run hello Android project (optional)</span></span>
<span data-ttu-id="433b0-115">Выполните этот раздел tooenable push-уведомления для hello Xamarin.Forms Droid проекта для Android.</span><span class="sxs-lookup"><span data-stu-id="433b0-115">Complete this section tooenable push notifications for hello Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="433b0-116">Включение Firebase Cloud Messaging (FCM)</span><span class="sxs-lookup"><span data-stu-id="433b0-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a><span data-ttu-id="433b0-117">Настройка hello мобильные приложения серверной части toosend принудительной запросы с помощью FCM</span><span class="sxs-lookup"><span data-stu-id="433b0-117">Configure hello Mobile Apps back end toosend push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a><span data-ttu-id="433b0-118">Добавление проекта Android toohello уведомления</span><span class="sxs-lookup"><span data-stu-id="433b0-118">Add push notifications toohello Android project</span></span>
<span data-ttu-id="433b0-119">Hello серверной настроены FCM можно добавить компоненты и коды tooregister toohello клиента с FCM.</span><span class="sxs-lookup"><span data-stu-id="433b0-119">With hello back end configured with FCM, you can add components and codes toohello client tooregister with FCM.</span></span> <span data-ttu-id="433b0-120">Можно также зарегистрировать push-уведомлений с концентраторами уведомлений Azure через hello заканчивается обратно мобильные приложения и получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="433b0-120">You can also register for push notifications with Azure Notification Hubs through hello Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="433b0-121">В hello **Droid** проекта, щелкните правой кнопкой мыши hello **компоненты** папку и нажмите кнопку **получить более компонентов...** . Выполните поиск hello **клиент обмена сообщениями Google облака** компонента и добавьте его в проект toohello.</span><span class="sxs-lookup"><span data-stu-id="433b0-121">In hello **Droid** project, right-click hello **Components** folder, and click **Get More Components...**. Then search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span> <span data-ttu-id="433b0-122">Этот компонент поддерживает push-уведомления для проекта Xamarin Android.</span><span class="sxs-lookup"><span data-stu-id="433b0-122">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="433b0-123">Откройте файл проекта MainActivity.cs hello и добавьте hello, следующем за инструкцией в начале hello hello файла:</span><span class="sxs-lookup"><span data-stu-id="433b0-123">Open hello MainActivity.cs project file, and add hello following statement at hello top of hello file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="433b0-124">Добавьте следующий код toohello hello **OnCreate** слишком вызов метода после hello**LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="433b0-124">Add hello following code toohello **OnCreate** method after hello call too**LoadApplication**:</span></span>

        try
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating hello client. Verify hello URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="433b0-125">Добавьте новый вспомогательный метод **CreateAndShowDialog** , как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="433b0-125">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="433b0-126">Добавьте следующий код toohello hello **MainActivity** класса:</span><span class="sxs-lookup"><span data-stu-id="433b0-126">Add hello following code toohello **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return hello current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="433b0-127">Это обеспечивает доступ к текущим hello **MainActivity** экземпляра, поэтому можно выполнить на hello основной поток пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="433b0-127">This exposes hello current **MainActivity** instance, so we can execute on hello main UI thread.</span></span>
6. <span data-ttu-id="433b0-128">Инициализировать hello `instance` переменных в начале hello hello **OnCreate** метода, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="433b0-128">Initialize hello `instance` variable at hello beginning of hello **OnCreate** method, as follows.</span></span>

        // Set hello current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="433b0-129">Добавить новый toohello файл класса **Droid** проект с именем `GcmService.cs`и убедитесь, что следующие hello **с помощью** операторы присутствуют в начале hello hello файла:</span><span class="sxs-lookup"><span data-stu-id="433b0-129">Add a new class file toohello **Droid** project named `GcmService.cs`, and make sure hello following **using** statements are present at hello top of hello file:</span></span>

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. <span data-ttu-id="433b0-130">Добавьте следующие запросы разрешений hello верхней части файла hello после hello hello **с помощью** инструкций и перед hello **имен** объявления.</span><span class="sxs-lookup"><span data-stu-id="433b0-130">Add hello following permission requests at hello top of hello file, after hello **using** statements and before hello **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="433b0-131">Добавьте следующие пространства имен toohello определения класса hello.</span><span class="sxs-lookup"><span data-stu-id="433b0-131">Add hello following class definition toohello namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="433b0-132">Замените **<PROJECT_NUMBER>** номером своего проекта, который вы записали ранее.</span><span class="sxs-lookup"><span data-stu-id="433b0-132">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="433b0-133">Замените hello пустой **GcmService** класса hello, следующий код, который использует новый приемник широковещательных hello:</span><span class="sxs-lookup"><span data-stu-id="433b0-133">Replace hello empty **GcmService** class with hello following code, which uses hello new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="433b0-134">Добавьте следующий код toohello hello **GcmService** класса.</span><span class="sxs-lookup"><span data-stu-id="433b0-134">Add hello following code toohello **GcmService** class.</span></span> <span data-ttu-id="433b0-135">Это значение переопределяет hello **OnRegistered** обработчик событий и реализует **зарегистрировать** метод.</span><span class="sxs-lookup"><span data-stu-id="433b0-135">This overrides hello **OnRegistered** event handler and implements a **Register** method.</span></span>

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    <span data-ttu-id="433b0-136">Обратите внимание, что этот код использует hello `messageParam` параметр в hello регистрацию шаблона.</span><span class="sxs-lookup"><span data-stu-id="433b0-136">Note that this code uses hello `messageParam` parameter in hello template registration.</span></span>
12. <span data-ttu-id="433b0-137">Добавьте следующий код, который реализует hello **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="433b0-137">Add hello following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store hello message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent tooshow ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create hello notification
            //we use hello pending intent, passing our ui intent over which will get called
            //when hello notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set hello notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove hello notification once hello user touches it
                    .SetAutoCancel(true).Build();

            //Show hello notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="433b0-138">Это обрабатывает входящие уведомления и отправляет их toohello уведомления диспетчера toobe отображается.</span><span class="sxs-lookup"><span data-stu-id="433b0-138">This handles incoming notifications and sends them toohello notification manager toobe displayed.</span></span>
13. <span data-ttu-id="433b0-139">**GcmServiceBase** также требует tooimplement hello **OnUnRegistered** и **OnError** методы обработчика, но это можно сделать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="433b0-139">**GcmServiceBase** also requires you tooimplement hello **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="433b0-140">Теперь вы проверки готовности push-уведомлений в приложение hello, работающее на устройстве с Android или hello эмулятора.</span><span class="sxs-lookup"><span data-stu-id="433b0-140">Now, you are ready test push notifications in hello app running on an Android device or hello emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="433b0-141">Тестирование push-уведомлений в приложении Android</span><span class="sxs-lookup"><span data-stu-id="433b0-141">Test push notifications in your Android app</span></span>
<span data-ttu-id="433b0-142">Первые два шага Hello необходимы только в том случае, если вы тестируете в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="433b0-142">hello first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="433b0-143">Убедитесь, что выполняется развертывание tooor отладку на виртуальное устройство с API-интерфейсы Google задать в качестве цели hello, как показано ниже в диспетчере hello виртуального устройства Android.</span><span class="sxs-lookup"><span data-stu-id="433b0-143">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device manager.</span></span>
2. <span data-ttu-id="433b0-144">Добавить устройство Android toohello учетной записи Google, щелкнув **приложения** > **параметры** > **добавьте учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="433b0-144">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="433b0-145">Затем выполните tooadd приглашения hello существующее устройство toohello учетной записи Google или toocreate новый.</span><span class="sxs-lookup"><span data-stu-id="433b0-145">Then follow hello prompts tooadd an existing Google account toohello device, or toocreate a new one.</span></span>
3. <span data-ttu-id="433b0-146">В Visual Studio и Xamarin Studio, щелкните правой кнопкой мыши hello **Droid** проекта и нажмите кнопку **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="433b0-146">In Visual Studio or Xamarin Studio, right-click hello **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="433b0-147">Нажмите кнопку **запуска** toobuild hello проект и запустить приложение hello на устройстве Android или в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="433b0-147">Click **Run** toobuild hello project and start hello app on your Android device or emulator.</span></span>
5. <span data-ttu-id="433b0-148">В приложение hello введите задачу и нажмите кнопку hello плюс (**+**) значок.</span><span class="sxs-lookup"><span data-stu-id="433b0-148">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
6. <span data-ttu-id="433b0-149">После добавления элемента должно отобразиться соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="433b0-149">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-hello-ios-project-optional"></a><span data-ttu-id="433b0-150">Настройка и выполнение проекта iOS hello (необязательно)</span><span class="sxs-lookup"><span data-stu-id="433b0-150">Configure and run hello iOS project (optional)</span></span>
<span data-ttu-id="433b0-151">Этот раздел предназначен для запуска проекта iOS hello Xamarin для устройств iOS.</span><span class="sxs-lookup"><span data-stu-id="433b0-151">This section is for running hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="433b0-152">Пропустите этот раздел, если вы не работаете с устройствами iOS.</span><span class="sxs-lookup"><span data-stu-id="433b0-152">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a><span data-ttu-id="433b0-153">Настройка концентратора уведомления hello для APNS</span><span class="sxs-lookup"><span data-stu-id="433b0-153">Configure hello notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="433b0-154">Далее вы настроите приветствия iOS проекта в Visual Studio или Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="433b0-154">Next, you will configure hello iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="433b0-155">Добавление приложения iOS tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="433b0-155">Add push notifications tooyour iOS app</span></span>
1. <span data-ttu-id="433b0-156">В hello **iOS** проекта откройте AppDelegate.cs и добавьте следующие инструкции toohello начало файла кода hello hello.</span><span class="sxs-lookup"><span data-stu-id="433b0-156">In hello **iOS** project, open AppDelegate.cs and add hello following statement toohello top of hello code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="433b0-157">В hello **AppDelegate** добавьте переопределение для hello **RegisteredForRemoteNotifications** tooregister событий для уведомлений:</span><span class="sxs-lookup"><span data-stu-id="433b0-157">In hello **AppDelegate** class, add an override for hello **RegisteredForRemoteNotifications** event tooregister for notifications:</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. <span data-ttu-id="433b0-158">В **AppDelegate**, также добавьте следующие переопределение для hello hello **DidReceiveRemoteNotification** обработчик событий:</span><span class="sxs-lookup"><span data-stu-id="433b0-158">In **AppDelegate**, also add hello following override for hello **DidReceiveRemoteNotification** event handler:</span></span>

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    <span data-ttu-id="433b0-159">Этот метод обрабатывает входящих уведомлений, пока работает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="433b0-159">This method handles incoming notifications while hello app is running.</span></span>
4. <span data-ttu-id="433b0-160">В hello **AppDelegate** добавьте следующий код toohello hello **FinishedLaunching** метод:</span><span class="sxs-lookup"><span data-stu-id="433b0-160">In hello **AppDelegate** class, add hello following code toohello **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="433b0-161">Он обеспечивает поддержку удаленных уведомлений и запрашивает регистрацию push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="433b0-161">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="433b0-162">Приложение сейчас обновленные toosupport push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="433b0-162">Your app is now updated toosupport push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="433b0-163">Тестирование push-уведомлений в приложении iOS</span><span class="sxs-lookup"><span data-stu-id="433b0-163">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="433b0-164">Щелкните правой кнопкой мыши проект iOS hello и нажмите кнопку **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="433b0-164">Right-click hello iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="433b0-165">Нажмите клавишу hello **запуска** кнопку или **F5** hello проекта toobuild Visual Studio и запустите приложение hello в устройстве iOS.</span><span class="sxs-lookup"><span data-stu-id="433b0-165">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS device.</span></span> <span data-ttu-id="433b0-166">Нажмите кнопку **ОК** tooaccept push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="433b0-166">Then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="433b0-167">Необходимо явно разрешить прием push-уведомлений от вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="433b0-167">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="433b0-168">Этот запрос возникает только hello при первом hello приложение выполняется.</span><span class="sxs-lookup"><span data-stu-id="433b0-168">This request only occurs hello first time that hello app runs.</span></span>
   >
   >
3. <span data-ttu-id="433b0-169">В приложение hello введите задачу и нажмите кнопку hello плюс (**+**) значок.</span><span class="sxs-lookup"><span data-stu-id="433b0-169">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
4. <span data-ttu-id="433b0-170">Убедитесь, что уведомление о получении и нажмите кнопку **ОК** toodismiss hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="433b0-170">Verify that a notification is received, and then click **OK** toodismiss hello notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="433b0-171">Настройка и запуск проектов для Windows (необязательно)</span><span class="sxs-lookup"><span data-stu-id="433b0-171">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="433b0-172">Этот раздел предназначен для запуска проектов Xamarin.Forms WinApp и WinPhone81 для устройств Windows hello.</span><span class="sxs-lookup"><span data-stu-id="433b0-172">This section is for running hello Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="433b0-173">Эти действия применимы для любых проектов универсальной платформы Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="433b0-173">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="433b0-174">Пропустите этот раздел, если вы не работаете с устройствами Windows.</span><span class="sxs-lookup"><span data-stu-id="433b0-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="433b0-175">Регистрация приложения для Windows для получения push-уведомлений через службу уведомлений Windows (WNS)</span><span class="sxs-lookup"><span data-stu-id="433b0-175">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="433b0-176">Настройка концентратора уведомления hello для WNS</span><span class="sxs-lookup"><span data-stu-id="433b0-176">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="433b0-177">Добавление приложения Windows tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="433b0-177">Add push notifications tooyour Windows app</span></span>
1. <span data-ttu-id="433b0-178">В Visual Studio откройте **App.xaml.cs** в Windows проекта и добавьте следующие инструкции hello.</span><span class="sxs-lookup"><span data-stu-id="433b0-178">In Visual Studio, open **App.xaml.cs** in a Windows project, and add hello following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="433b0-179">Замените `<your_TodoItemManager_portable_class_namespace>` с пространством имен hello для переносимого проекта, содержащего hello `TodoItemManager` класса.</span><span class="sxs-lookup"><span data-stu-id="433b0-179">Replace `<your_TodoItemManager_portable_class_namespace>` with hello namespace of your portable project that contains hello `TodoItemManager` class.</span></span>
2. <span data-ttu-id="433b0-180">В App.xaml.cs, добавьте следующее hello **InitNotificationsAsync** метод:</span><span class="sxs-lookup"><span data-stu-id="433b0-180">In App.xaml.cs, add hello following **InitNotificationsAsync** method:</span></span>

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    <span data-ttu-id="433b0-181">Этот метод возвращает hello канала push-уведомлений и регистрирует уведомления о шаблона шаблона tooreceive из центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="433b0-181">This method gets hello push notification channel, and registers a template tooreceive template notifications from your notification hub.</span></span> <span data-ttu-id="433b0-182">Шаблон уведомления, поддерживающий *messageParam* будет доставлена toothis клиента.</span><span class="sxs-lookup"><span data-stu-id="433b0-182">A template notification that supports *messageParam* will be delivered toothis client.</span></span>
3. <span data-ttu-id="433b0-183">В App.xaml.cs, обновите hello **OnLaunched** определения метода обработчика событий, добавив hello `async` модификатор.</span><span class="sxs-lookup"><span data-stu-id="433b0-183">In App.xaml.cs, update hello **OnLaunched** event handler method definition by adding hello `async` modifier.</span></span> <span data-ttu-id="433b0-184">Затем добавьте hello, следующей строкой кода в конце hello hello метод:</span><span class="sxs-lookup"><span data-stu-id="433b0-184">Then add hello following line of code at hello end of hello method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="433b0-185">Это гарантирует, что hello регистрации push-уведомлений создается или обновляется каждый раз при запуске приложения hello.</span><span class="sxs-lookup"><span data-stu-id="433b0-185">This ensures that hello push notification registration is created or refreshed every time hello app is launched.</span></span> <span data-ttu-id="433b0-186">Очень важно toodo этот tooguarantee, hello канала WNS push не всегда активно.</span><span class="sxs-lookup"><span data-stu-id="433b0-186">It's important toodo this tooguarantee that hello WNS push channel is always active.</span></span>  
4. <span data-ttu-id="433b0-187">В обозревателе решений Visual Studio, откройте hello **Package.appxmanifest** и задайте **поддержкой всплывающих** слишком**Да** под **уведомления**.</span><span class="sxs-lookup"><span data-stu-id="433b0-187">In Solution Explorer for Visual Studio, open hello **Package.appxmanifest** file, and set **Toast Capable** too**Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="433b0-188">Постройте приложение hello и убедитесь, что у вас нет ошибок.</span><span class="sxs-lookup"><span data-stu-id="433b0-188">Build hello app and verify you have no errors.</span></span> <span data-ttu-id="433b0-189">Клиентское приложение должно теперь зарегистрировать hello шаблон уведомления в hello что заканчивается обратно мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="433b0-189">Your client app should now register for hello template notifications from hello Mobile Apps back end.</span></span> <span data-ttu-id="433b0-190">Повторите действия из этого раздела для каждого проекта Windows, входящего в ваше решение.</span><span class="sxs-lookup"><span data-stu-id="433b0-190">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="433b0-191">Тестирование push-уведомлений в приложении Windows</span><span class="sxs-lookup"><span data-stu-id="433b0-191">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="433b0-192">В Visual Studio щелкните правой кнопкой мыши проект Windows и выберите **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="433b0-192">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="433b0-193">Нажмите клавишу hello **запуска** кнопку toobuild hello проект и запустить приложение hello.</span><span class="sxs-lookup"><span data-stu-id="433b0-193">Press hello **Run** button toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="433b0-194">В приложение hello, введите имя для нового todoitem и нажмите кнопку hello плюс (**+**) tooadd значок его.</span><span class="sxs-lookup"><span data-stu-id="433b0-194">In hello app, type a name for a new todoitem, and then click hello plus (**+**) icon tooadd it.</span></span>
4. <span data-ttu-id="433b0-195">Проверка получения уведомления при добавлении элемента hello.</span><span class="sxs-lookup"><span data-stu-id="433b0-195">Verify that a notification is received when hello item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="433b0-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="433b0-196">Next steps</span></span>
<span data-ttu-id="433b0-197">Вы можете узнать больше о push-уведомлениях.</span><span class="sxs-lookup"><span data-stu-id="433b0-197">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="433b0-198">Диагностика неполадок, связанных с push-уведомлениями</span><span class="sxs-lookup"><span data-stu-id="433b0-198">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="433b0-199">Существуют различные причины, по которым уведомления могут теряться или не доходить до устройств.</span><span class="sxs-lookup"><span data-stu-id="433b0-199">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="433b0-200">В этом разделе показано, как tooanalyze и выясните, hello корневой причиной сбоев уведомлений push.</span><span class="sxs-lookup"><span data-stu-id="433b0-200">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="433b0-201">Можно также перейти на tooone из hello следующие учебники:</span><span class="sxs-lookup"><span data-stu-id="433b0-201">You can also continue on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="433b0-202">Добавить приложение tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="433b0-202">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="433b0-203">Узнайте, как пользователи tooauthenticate приложения с поставщиком удостоверений.</span><span class="sxs-lookup"><span data-stu-id="433b0-203">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="433b0-204">Включение автономной синхронизации для приложения</span><span class="sxs-lookup"><span data-stu-id="433b0-204">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="433b0-205">Узнайте, как tooadd поддержке приложения с помощью мобильных приложений серверной части.</span><span class="sxs-lookup"><span data-stu-id="433b0-205">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="433b0-206">Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением (&mdash;просматривать, добавлять или изменять данные&mdash;) даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="433b0-206">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
