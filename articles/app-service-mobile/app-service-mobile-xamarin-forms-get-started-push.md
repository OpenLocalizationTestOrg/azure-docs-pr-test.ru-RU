---
title: "Добавление push-уведомлений в приложение Xamarin.Forms | Документация Майкрософт"
description: "Использование служб Azure для отправки кроссплатформенных push-уведомлений в приложения Xamarin.Forms."
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
ms.openlocfilehash: 912367636f1b26b3b07fbd5fe3fe8ed053218fd5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinforms-app"></a><span data-ttu-id="a7aac-103">Добавление push-уведомлений в приложение Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="a7aac-103">Add push notifications to your Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="a7aac-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a7aac-104">Overview</span></span>
<span data-ttu-id="a7aac-105">В этом руководстве вы добавите push-уведомления во все проекты, которые были созданы на основе [проекта быстрого запуска Xamarin.Forms](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a7aac-105">In this tutorial, you add push notifications to all the projects that resulted from the [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="a7aac-106">Это значит, что push-уведомление будет отправляться во все кроссплатформенные клиенты при каждой вставке записи.</span><span class="sxs-lookup"><span data-stu-id="a7aac-106">This means that a push notification is sent to all cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="a7aac-107">Если вы не используете скачанный проект сервера, необходимо добавить пакет расширений для push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a7aac-107">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="a7aac-108">Дополнительные сведения см. в статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a7aac-108">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7aac-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a7aac-109">Prerequisites</span></span>
<span data-ttu-id="a7aac-110">Для iOS потребуется [участие в программе для разработчиков на платформе Apple](https://developer.apple.com/programs/ios/) и физическое устройство iOS.</span><span class="sxs-lookup"><span data-stu-id="a7aac-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="a7aac-111">[Симулятор iOS не поддерживает push-уведомления](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="a7aac-111">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="a7aac-112"><a name="configure-hub"></a>Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="a7aac-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="a7aac-113">Обновление серверного проекта для отправки push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="a7aac-113">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-the-android-project-optional"></a><span data-ttu-id="a7aac-114">Настройка и запуск проекта Android (необязательно)</span><span class="sxs-lookup"><span data-stu-id="a7aac-114">Configure and run the Android project (optional)</span></span>
<span data-ttu-id="a7aac-115">Выполнив инструкции из этого раздела, вы добавите push-уведомления для проекта Xamarin.Forms Droid для платформы Android.</span><span class="sxs-lookup"><span data-stu-id="a7aac-115">Complete this section to enable push notifications for the Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="a7aac-116">Включение Firebase Cloud Messaging (FCM)</span><span class="sxs-lookup"><span data-stu-id="a7aac-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-the-mobile-apps-back-end-to-send-push-requests-by-using-fcm"></a><span data-ttu-id="a7aac-117">Настройка серверной части мобильных приложений для отправки push-запросов с использованием FCM</span><span class="sxs-lookup"><span data-stu-id="a7aac-117">Configure the Mobile Apps back end to send push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-to-the-android-project"></a><span data-ttu-id="a7aac-118">Добавление push-уведомлений в проект Android</span><span class="sxs-lookup"><span data-stu-id="a7aac-118">Add push notifications to the Android project</span></span>
<span data-ttu-id="a7aac-119">Настроив FCM для серверной части, в клиент можно добавить компоненты и код для регистрации в службе FCM.</span><span class="sxs-lookup"><span data-stu-id="a7aac-119">With the back end configured with FCM, you can add components and codes to the client to register with FCM.</span></span> <span data-ttu-id="a7aac-120">Можно также выполнить регистрацию в Центрах уведомлений Azure, чтобы отправлять push-уведомления через серверную часть мобильных приложений и получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="a7aac-120">You can also register for push notifications with Azure Notification Hubs through the Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="a7aac-121">В проекте **Droid** щелкните правой кнопкой мыши папку **Components** и выберите **Get More Components…** (Получить дополнительные компоненты).</span><span class="sxs-lookup"><span data-stu-id="a7aac-121">In the **Droid** project, right-click the **Components** folder, and click **Get More Components...**.</span></span> <span data-ttu-id="a7aac-122">Найдите компонент **Google Cloud Messaging Client** и добавьте его в проект.</span><span class="sxs-lookup"><span data-stu-id="a7aac-122">Then search for the **Google Cloud Messaging Client** component and add it to the project.</span></span> <span data-ttu-id="a7aac-123">Этот компонент поддерживает push-уведомления для проекта Xamarin Android.</span><span class="sxs-lookup"><span data-stu-id="a7aac-123">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="a7aac-124">Откройте файл проекта MainActivity.cs и добавьте приведенный ниже оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="a7aac-124">Open the MainActivity.cs project file, and add the following statement at the top of the file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="a7aac-125">Добавьте в метод **OnCreate** после строки вызова **LoadApplication** следующий код:</span><span class="sxs-lookup"><span data-stu-id="a7aac-125">Add the following code to the **OnCreate** method after the call to **LoadApplication**:</span></span>

        try
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating the client. Verify the URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="a7aac-126">Добавьте новый вспомогательный метод **CreateAndShowDialog** , как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="a7aac-126">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="a7aac-127">Добавьте следующий код в класс **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="a7aac-127">Add the following code to the **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return the current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="a7aac-128">Этот класс представляет текущий экземпляр **MainActivity** и позволяет выполнить действия в основном потоке пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a7aac-128">This exposes the current **MainActivity** instance, so we can execute on the main UI thread.</span></span>
6. <span data-ttu-id="a7aac-129">Инициализируйте переменную `instance` в начале метода **OnCreate**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a7aac-129">Initialize the `instance` variable at the beginning of the **OnCreate** method, as follows.</span></span>

        // Set the current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="a7aac-130">Добавьте в проект **Droid** новый файл класса с именем `GcmService.cs`. В начале файла этого класса обязательно должны присутствовать следующие операторы **using**:</span><span class="sxs-lookup"><span data-stu-id="a7aac-130">Add a new class file to the **Droid** project named `GcmService.cs`, and make sure the following **using** statements are present at the top of the file:</span></span>

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
8. <span data-ttu-id="a7aac-131">Добавьте в начало файла (после операторов **using**, но до объявления **namespace**) следующие запросы на разрешение.</span><span class="sxs-lookup"><span data-stu-id="a7aac-131">Add the following permission requests at the top of the file, after the **using** statements and before the **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="a7aac-132">Добавьте следующее определение класса в пространство имен.</span><span class="sxs-lookup"><span data-stu-id="a7aac-132">Add the following class definition to the namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="a7aac-133">Замените **<PROJECT_NUMBER>** номером своего проекта, который вы записали ранее.</span><span class="sxs-lookup"><span data-stu-id="a7aac-133">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="a7aac-134">Замените пустой класс **GcmService** следующим кодом, который использует новый получатель широковещательных сообщений:</span><span class="sxs-lookup"><span data-stu-id="a7aac-134">Replace the empty **GcmService** class with the following code, which uses the new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="a7aac-135">Добавьте в класс **GcmService** приведенный далее код.</span><span class="sxs-lookup"><span data-stu-id="a7aac-135">Add the following code to the **GcmService** class.</span></span> <span data-ttu-id="a7aac-136">Так вы переопределите обработчик событий **OnRegistered** и реализуете метод **Register**.</span><span class="sxs-lookup"><span data-stu-id="a7aac-136">This overrides the **OnRegistered** event handler and implements a **Register** method.</span></span>

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

    <span data-ttu-id="a7aac-137">Обратите внимание, что этот код использует параметр `messageParam` в регистрации шаблона.</span><span class="sxs-lookup"><span data-stu-id="a7aac-137">Note that this code uses the `messageParam` parameter in the template registration.</span></span>
12. <span data-ttu-id="a7aac-138">Добавьте следующий код, который реализует метод **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="a7aac-138">Add the following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store the message
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

            //Create an intent to show ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create the notification
            //we use the pending intent, passing our ui intent over which will get called
            //when the notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set the notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove the notification once the user touches it
                    .SetAutoCancel(true).Build();

            //Show the notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="a7aac-139">Он обрабатывает входящие уведомления и передает их для отображения в диспетчер уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a7aac-139">This handles incoming notifications and sends them to the notification manager to be displayed.</span></span>
13. <span data-ttu-id="a7aac-140">Для **GcmServiceBase** также потребуется реализовать методы обработчика **OnUnRegistered** и **OnError**, например так:</span><span class="sxs-lookup"><span data-stu-id="a7aac-140">**GcmServiceBase** also requires you to implement the **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="a7aac-141">Теперь все готово, и вы можете проверить отправку push-уведомлений с помощью приложения, работающего на устройстве Android или в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="a7aac-141">Now, you are ready test push notifications in the app running on an Android device or the emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="a7aac-142">Тестирование push-уведомлений в приложении Android</span><span class="sxs-lookup"><span data-stu-id="a7aac-142">Test push notifications in your Android app</span></span>
<span data-ttu-id="a7aac-143">Первые два шага нужны, только если тестирование выполняется в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="a7aac-143">The first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="a7aac-144">Убедитесь, что для развертывания или отладки используется виртуальное устройство, на котором в качестве назначения заданы интерфейсы Google API, как показано ниже в диспетчере виртуальных устройств Android.</span><span class="sxs-lookup"><span data-stu-id="a7aac-144">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device manager.</span></span>
2. <span data-ttu-id="a7aac-145">Добавить учетную запись Google на устройстве Android, поочередно щелкнув **Apps** (Приложения) > **Settings** (Параметры) > **Add account** (Добавить учетную запись).</span><span class="sxs-lookup"><span data-stu-id="a7aac-145">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="a7aac-146">Затем следуйте указаниям в отображаемых запросах, чтобы добавить на устройство имеющуюся учетную запись Google или создать новую.</span><span class="sxs-lookup"><span data-stu-id="a7aac-146">Then follow the prompts to add an existing Google account to the device, or to create a new one.</span></span>
3. <span data-ttu-id="a7aac-147">В Visual Studio или Xamarin Studio щелкните правой кнопкой мыши проект **Droid** и выберите **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="a7aac-147">In Visual Studio or Xamarin Studio, right-click the **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="a7aac-148">Нажмите кнопку **Запустить** , чтобы создать проект и запустить приложение на устройстве Android или в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="a7aac-148">Click **Run** to build the project and start the app on your Android device or emulator.</span></span>
5. <span data-ttu-id="a7aac-149">В приложении введите задачу, а затем щелкните значок плюса (**+**).</span><span class="sxs-lookup"><span data-stu-id="a7aac-149">In the app, type a task, and then click the plus (**+**) icon.</span></span>
6. <span data-ttu-id="a7aac-150">После добавления элемента должно отобразиться соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="a7aac-150">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-the-ios-project-optional"></a><span data-ttu-id="a7aac-151">Настройка и запуск проекта iOS (необязательно)</span><span class="sxs-lookup"><span data-stu-id="a7aac-151">Configure and run the iOS project (optional)</span></span>
<span data-ttu-id="a7aac-152">В этом разделе описано, как запустить проект Xamarin iOS для устройств под управлением iOS.</span><span class="sxs-lookup"><span data-stu-id="a7aac-152">This section is for running the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="a7aac-153">Пропустите этот раздел, если вы не работаете с устройствами iOS.</span><span class="sxs-lookup"><span data-stu-id="a7aac-153">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-the-notification-hub-for-apns"></a><span data-ttu-id="a7aac-154">Настройка концентратора уведомлений для APNs</span><span class="sxs-lookup"><span data-stu-id="a7aac-154">Configure the notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="a7aac-155">Далее следует настроить параметры проекта iOS в Xamarin Studio или Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a7aac-155">Next, you will configure the iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="a7aac-156">Добавление push-уведомлений в приложение iOS</span><span class="sxs-lookup"><span data-stu-id="a7aac-156">Add push notifications to your iOS app</span></span>
1. <span data-ttu-id="a7aac-157">В проекте **iOS** откройте файл AppDelegate.cs и добавьте в его начало приведенный ниже оператор.</span><span class="sxs-lookup"><span data-stu-id="a7aac-157">In the **iOS** project, open AppDelegate.cs and add the following statement to the top of the code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="a7aac-158">В класс **AppDelegate** добавьте переопределение для события **RegisteredForRemoteNotifications**, чтобы выполнить регистрацию для получения уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a7aac-158">In the **AppDelegate** class, add an override for the **RegisteredForRemoteNotifications** event to register for notifications:</span></span>

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
3. <span data-ttu-id="a7aac-159">Добавьте также в класс **AppDelegate** следующее переопределение для обработчика событий **DidReceiveRemoteNotification**.</span><span class="sxs-lookup"><span data-stu-id="a7aac-159">In **AppDelegate**, also add the following override for the **DidReceiveRemoteNotification** event handler:</span></span>

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

    <span data-ttu-id="a7aac-160">Этот метод обрабатывает входящие уведомления во время выполнения приложения.</span><span class="sxs-lookup"><span data-stu-id="a7aac-160">This method handles incoming notifications while the app is running.</span></span>
4. <span data-ttu-id="a7aac-161">В классе **AppDelegate** добавьте следующий код в метод **FinishedLaunching**.</span><span class="sxs-lookup"><span data-stu-id="a7aac-161">In the **AppDelegate** class, add the following code to the **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="a7aac-162">Он обеспечивает поддержку удаленных уведомлений и запрашивает регистрацию push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a7aac-162">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="a7aac-163">Ваше приложение теперь обновлено для поддержки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a7aac-163">Your app is now updated to support push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="a7aac-164">Тестирование push-уведомлений в приложении iOS</span><span class="sxs-lookup"><span data-stu-id="a7aac-164">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="a7aac-165">Щелкните проект iOS правой кнопкой мыши и выберите **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="a7aac-165">Right-click the iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="a7aac-166">Нажмите кнопку **Запустить** или клавишу **F5** в Visual Studio, чтобы выполнить сборку проекта и запустить приложение на устройстве iOS.</span><span class="sxs-lookup"><span data-stu-id="a7aac-166">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS device.</span></span> <span data-ttu-id="a7aac-167">Затем нажмите кнопку **ОК**, чтобы принять push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="a7aac-167">Then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a7aac-168">Необходимо явно разрешить прием push-уведомлений от вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a7aac-168">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="a7aac-169">Этот запрос отображается только при первом запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="a7aac-169">This request only occurs the first time that the app runs.</span></span>
   >
   >
3. <span data-ttu-id="a7aac-170">В приложении введите задачу, а затем щелкните значок плюса (**+**).</span><span class="sxs-lookup"><span data-stu-id="a7aac-170">In the app, type a task, and then click the plus (**+**) icon.</span></span>
4. <span data-ttu-id="a7aac-171">Убедитесь, что уведомление получено, а затем нажмите кнопку **ОК**, чтобы его закрыть.</span><span class="sxs-lookup"><span data-stu-id="a7aac-171">Verify that a notification is received, and then click **OK** to dismiss the notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="a7aac-172">Настройка и запуск проектов для Windows (необязательно)</span><span class="sxs-lookup"><span data-stu-id="a7aac-172">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="a7aac-173">В этом разделе описано, как запускать проекты Xamarin.Forms WinApp и WinPhone81 на устройствах под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="a7aac-173">This section is for running the Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="a7aac-174">Эти действия применимы для любых проектов универсальной платформы Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="a7aac-174">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="a7aac-175">Пропустите этот раздел, если вы не работаете с устройствами Windows.</span><span class="sxs-lookup"><span data-stu-id="a7aac-175">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="a7aac-176">Регистрация приложения для Windows для получения push-уведомлений через службу уведомлений Windows (WNS)</span><span class="sxs-lookup"><span data-stu-id="a7aac-176">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="a7aac-177">Настройка концентратора уведомлений для WNS</span><span class="sxs-lookup"><span data-stu-id="a7aac-177">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="a7aac-178">Добавление push-уведомлений в приложение Windows</span><span class="sxs-lookup"><span data-stu-id="a7aac-178">Add push notifications to your Windows app</span></span>
1. <span data-ttu-id="a7aac-179">В Visual Studio откройте файл проекта Windows **App.xaml.cs** и добавьте следующие операторы.</span><span class="sxs-lookup"><span data-stu-id="a7aac-179">In Visual Studio, open **App.xaml.cs** in a Windows project, and add the following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="a7aac-180">Вместо `<your_TodoItemManager_portable_class_namespace>` укажите пространство имен своего переносимого проекта, который содержит класс `TodoItemManager`.</span><span class="sxs-lookup"><span data-stu-id="a7aac-180">Replace `<your_TodoItemManager_portable_class_namespace>` with the namespace of your portable project that contains the `TodoItemManager` class.</span></span>
2. <span data-ttu-id="a7aac-181">В файл App.xaml.cs добавьте следующий метод **InitNotificationsAsync**.</span><span class="sxs-lookup"><span data-stu-id="a7aac-181">In App.xaml.cs, add the following **InitNotificationsAsync** method:</span></span>

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

    <span data-ttu-id="a7aac-182">Этот метод получает канал push-уведомлений и регистрирует шаблон для получения шаблонных уведомлений из центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a7aac-182">This method gets the push notification channel, and registers a template to receive template notifications from your notification hub.</span></span> <span data-ttu-id="a7aac-183">Клиенту будет доставлено шаблонное уведомление, поддерживающее параметр *messageParam* .</span><span class="sxs-lookup"><span data-stu-id="a7aac-183">A template notification that supports *messageParam* will be delivered to this client.</span></span>
3. <span data-ttu-id="a7aac-184">В файле App.xaml.cs измените определение метода обработчика событий **OnLaunched**, добавив в него модификатор `async`.</span><span class="sxs-lookup"><span data-stu-id="a7aac-184">In App.xaml.cs, update the **OnLaunched** event handler method definition by adding the `async` modifier.</span></span> <span data-ttu-id="a7aac-185">В конец метода добавьте следующую строку кода.</span><span class="sxs-lookup"><span data-stu-id="a7aac-185">Then add the following line of code at the end of the method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="a7aac-186">Теперь push-уведомления будут создаваться или обновляться при каждом запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="a7aac-186">This ensures that the push notification registration is created or refreshed every time the app is launched.</span></span> <span data-ttu-id="a7aac-187">Это нужно, чтобы push-канал WNS всегда оставался активным.</span><span class="sxs-lookup"><span data-stu-id="a7aac-187">It's important to do this to guarantee that the WNS push channel is always active.</span></span>  
4. <span data-ttu-id="a7aac-188">В обозревателе решений для Visual Studio откройте файл **Package.appxmanifest** и в разделе **Notifications** задайте для параметра **Toast Capable** значение **Yes**.</span><span class="sxs-lookup"><span data-stu-id="a7aac-188">In Solution Explorer for Visual Studio, open the **Package.appxmanifest** file, and set **Toast Capable** to **Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="a7aac-189">Выполните сборку приложения и убедитесь в отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="a7aac-189">Build the app and verify you have no errors.</span></span> <span data-ttu-id="a7aac-190">Теперь клиентское приложение должно зарегистрироваться для получения шаблонных уведомлений из серверной части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="a7aac-190">Your client app should now register for the template notifications from the Mobile Apps back end.</span></span> <span data-ttu-id="a7aac-191">Повторите действия из этого раздела для каждого проекта Windows, входящего в ваше решение.</span><span class="sxs-lookup"><span data-stu-id="a7aac-191">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="a7aac-192">Тестирование push-уведомлений в приложении Windows</span><span class="sxs-lookup"><span data-stu-id="a7aac-192">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="a7aac-193">В Visual Studio щелкните правой кнопкой мыши проект Windows и выберите **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="a7aac-193">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="a7aac-194">Нажмите кнопку **Запуск** , чтобы создать проект и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="a7aac-194">Press the **Run** button to build the project and start the app.</span></span>
3. <span data-ttu-id="a7aac-195">В приложении введите имя нового объекта todoitem и добавьте его, щелкнув знак "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="a7aac-195">In the app, type a name for a new todoitem, and then click the plus (**+**) icon to add it.</span></span>
4. <span data-ttu-id="a7aac-196">После добавления элемента должно отобразиться соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="a7aac-196">Verify that a notification is received when the item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7aac-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7aac-197">Next steps</span></span>
<span data-ttu-id="a7aac-198">Вы можете узнать больше о push-уведомлениях.</span><span class="sxs-lookup"><span data-stu-id="a7aac-198">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="a7aac-199">Диагностика неполадок, связанных с push-уведомлениями</span><span class="sxs-lookup"><span data-stu-id="a7aac-199">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="a7aac-200">Существуют различные причины, по которым уведомления могут теряться или не доходить до устройств.</span><span class="sxs-lookup"><span data-stu-id="a7aac-200">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="a7aac-201">В этой статье рассказывается, как проанализировать и определить основную причину сбоев push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a7aac-201">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="a7aac-202">Кроме того, вы можете изучить одно из следующих руководств:</span><span class="sxs-lookup"><span data-stu-id="a7aac-202">You can also continue on to one of the following tutorials:</span></span>

* [<span data-ttu-id="a7aac-203">Добавление проверки подлинности в приложение</span><span class="sxs-lookup"><span data-stu-id="a7aac-203">Add authentication to your app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="a7aac-204">Узнайте больше о проверке подлинности пользователей приложения с помощью поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="a7aac-204">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="a7aac-205">Включение автономной синхронизации для приложения</span><span class="sxs-lookup"><span data-stu-id="a7aac-205">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="a7aac-206">Узнайте, как добавить в приложение поддержку автономной работы с помощью серверной части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="a7aac-206">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="a7aac-207">Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением (&mdash;просматривать, добавлять или изменять данные&mdash;) даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="a7aac-207">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
