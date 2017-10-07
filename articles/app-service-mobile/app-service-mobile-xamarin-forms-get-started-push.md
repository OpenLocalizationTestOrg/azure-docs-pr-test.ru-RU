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
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a>Добавить приложение Xamarin.Forms tooyour уведомлений push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Обзор
В этом учебнике добавить push tooall уведомления hello проекты, полученные из hello [Xamarin.Forms краткого](app-service-mobile-xamarin-forms-get-started.md). Это означает, что push-уведомление отправляется tooall кросс платформенных клиентов, каждый раз при вставке записи.

Если вы не используете hello загружен проект быстрый запуск сервера, будет необходимо hello пакета расширения уведомлений push. Дополнительные сведения см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Предварительные требования
Для iOS потребуется [участие в программе для разработчиков на платформе Apple](https://developer.apple.com/programs/ios/) и физическое устройство iOS. Hello [симулятор iOS не поддерживает push-уведомления](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).

## <a name="configure-hub"></a>Настройка концентратора уведомлений
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Обновить hello server проекта toosend push-уведомлений
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a>Настройка и выполнение проекта Android hello (необязательно)
Выполните этот раздел tooenable push-уведомления для hello Xamarin.Forms Droid проекта для Android.

### <a name="enable-firebase-cloud-messaging-fcm"></a>Включение Firebase Cloud Messaging (FCM)
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a>Настройка hello мобильные приложения серверной части toosend принудительной запросы с помощью FCM
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a>Добавление проекта Android toohello уведомления
Hello серверной настроены FCM можно добавить компоненты и коды tooregister toohello клиента с FCM. Можно также зарегистрировать push-уведомлений с концентраторами уведомлений Azure через hello заканчивается обратно мобильные приложения и получать уведомления.

1. В hello **Droid** проекта, щелкните правой кнопкой мыши hello **компоненты** папку и нажмите кнопку **получить более компонентов...** . Выполните поиск hello **клиент обмена сообщениями Google облака** компонента и добавьте его в проект toohello. Этот компонент поддерживает push-уведомления для проекта Xamarin Android.
2. Откройте файл проекта MainActivity.cs hello и добавьте hello, следующем за инструкцией в начале hello hello файла:

        using Gcm.Client;
3. Добавьте следующий код toohello hello **OnCreate** слишком вызов метода после hello**LoadApplication**:

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
4. Добавьте новый вспомогательный метод **CreateAndShowDialog** , как показано ниже:

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. Добавьте следующий код toohello hello **MainActivity** класса:

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

    Это обеспечивает доступ к текущим hello **MainActivity** экземпляра, поэтому можно выполнить на hello основной поток пользовательского интерфейса.
6. Инициализировать hello `instance` переменных в начале hello hello **OnCreate** метода, как показано ниже.

        // Set hello current instance of MainActivity.
        instance = this;
7. Добавить новый toohello файл класса **Droid** проект с именем `GcmService.cs`и убедитесь, что следующие hello **с помощью** операторы присутствуют в начале hello hello файла:

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
8. Добавьте следующие запросы разрешений hello верхней части файла hello после hello hello **с помощью** инструкций и перед hello **имен** объявления.

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. Добавьте следующие пространства имен toohello определения класса hello.

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > Замените **<PROJECT_NUMBER>** номером своего проекта, который вы записали ранее.    
   >
   >
10. Замените hello пустой **GcmService** класса hello, следующий код, который использует новый приемник широковещательных hello:

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. Добавьте следующий код toohello hello **GcmService** класса. Это значение переопределяет hello **OnRegistered** обработчик событий и реализует **зарегистрировать** метод.

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

    Обратите внимание, что этот код использует hello `messageParam` параметр в hello регистрацию шаблона.
12. Добавьте следующий код, который реализует hello **OnMessage**:

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

    Это обрабатывает входящие уведомления и отправляет их toohello уведомления диспетчера toobe отображается.
13. **GcmServiceBase** также требует tooimplement hello **OnUnRegistered** и **OnError** методы обработчика, но это можно сделать следующим образом:

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

Теперь вы проверки готовности push-уведомлений в приложение hello, работающее на устройстве с Android или hello эмулятора.

### <a name="test-push-notifications-in-your-android-app"></a>Тестирование push-уведомлений в приложении Android
Первые два шага Hello необходимы только в том случае, если вы тестируете в эмуляторе.

1. Убедитесь, что выполняется развертывание tooor отладку на виртуальное устройство с API-интерфейсы Google задать в качестве цели hello, как показано ниже в диспетчере hello виртуального устройства Android.
2. Добавить устройство Android toohello учетной записи Google, щелкнув **приложения** > **параметры** > **добавьте учетную запись**. Затем выполните tooadd приглашения hello существующее устройство toohello учетной записи Google или toocreate новый.
3. В Visual Studio и Xamarin Studio, щелкните правой кнопкой мыши hello **Droid** проекта и нажмите кнопку **Назначить запускаемым проектом**.
4. Нажмите кнопку **запуска** toobuild hello проект и запустить приложение hello на устройстве Android или в эмуляторе.
5. В приложение hello введите задачу и нажмите кнопку hello плюс (**+**) значок.
6. После добавления элемента должно отобразиться соответствующее уведомление.

## <a name="configure-and-run-hello-ios-project-optional"></a>Настройка и выполнение проекта iOS hello (необязательно)
Этот раздел предназначен для запуска проекта iOS hello Xamarin для устройств iOS. Пропустите этот раздел, если вы не работаете с устройствами iOS.

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a>Настройка концентратора уведомления hello для APNS
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

Далее вы настроите приветствия iOS проекта в Visual Studio или Xamarin Studio.

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a>Добавление приложения iOS tooyour уведомлений push
1. В hello **iOS** проекта откройте AppDelegate.cs и добавьте следующие инструкции toohello начало файла кода hello hello.

        using Newtonsoft.Json.Linq;
2. В hello **AppDelegate** добавьте переопределение для hello **RegisteredForRemoteNotifications** tooregister событий для уведомлений:

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
3. В **AppDelegate**, также добавьте следующие переопределение для hello hello **DidReceiveRemoteNotification** обработчик событий:

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

    Этот метод обрабатывает входящих уведомлений, пока работает приложение hello.
4. В hello **AppDelegate** добавьте следующий код toohello hello **FinishedLaunching** метод:

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    Он обеспечивает поддержку удаленных уведомлений и запрашивает регистрацию push-уведомлений.

Приложение сейчас обновленные toosupport push-уведомлений.

#### <a name="test-push-notifications-in-your-ios-app"></a>Тестирование push-уведомлений в приложении iOS
1. Щелкните правой кнопкой мыши проект iOS hello и нажмите кнопку **Назначить запускаемым проектом**.
2. Нажмите клавишу hello **запуска** кнопку или **F5** hello проекта toobuild Visual Studio и запустите приложение hello в устройстве iOS. Нажмите кнопку **ОК** tooaccept push-уведомлений.

   > [!NOTE]
   > Необходимо явно разрешить прием push-уведомлений от вашего приложения. Этот запрос возникает только hello при первом hello приложение выполняется.
   >
   >
3. В приложение hello введите задачу и нажмите кнопку hello плюс (**+**) значок.
4. Убедитесь, что уведомление о получении и нажмите кнопку **ОК** toodismiss hello уведомления.

## <a name="configure-and-run-windows-projects-optional"></a>Настройка и запуск проектов для Windows (необязательно)
Этот раздел предназначен для запуска проектов Xamarin.Forms WinApp и WinPhone81 для устройств Windows hello. Эти действия применимы для любых проектов универсальной платформы Windows (UWP). Пропустите этот раздел, если вы не работаете с устройствами Windows.

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a>Регистрация приложения для Windows для получения push-уведомлений через службу уведомлений Windows (WNS)
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a>Настройка концентратора уведомления hello для WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a>Добавление приложения Windows tooyour уведомлений push
1. В Visual Studio откройте **App.xaml.cs** в Windows проекта и добавьте следующие инструкции hello.

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    Замените `<your_TodoItemManager_portable_class_namespace>` с пространством имен hello для переносимого проекта, содержащего hello `TodoItemManager` класса.
2. В App.xaml.cs, добавьте следующее hello **InitNotificationsAsync** метод:

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

    Этот метод возвращает hello канала push-уведомлений и регистрирует уведомления о шаблона шаблона tooreceive из центра уведомлений. Шаблон уведомления, поддерживающий *messageParam* будет доставлена toothis клиента.
3. В App.xaml.cs, обновите hello **OnLaunched** определения метода обработчика событий, добавив hello `async` модификатор. Затем добавьте hello, следующей строкой кода в конце hello hello метод:

        await InitNotificationsAsync();

    Это гарантирует, что hello регистрации push-уведомлений создается или обновляется каждый раз при запуске приложения hello. Очень важно toodo этот tooguarantee, hello канала WNS push не всегда активно.  
4. В обозревателе решений Visual Studio, откройте hello **Package.appxmanifest** и задайте **поддержкой всплывающих** слишком**Да** под **уведомления**.
5. Постройте приложение hello и убедитесь, что у вас нет ошибок. Клиентское приложение должно теперь зарегистрировать hello шаблон уведомления в hello что заканчивается обратно мобильные приложения. Повторите действия из этого раздела для каждого проекта Windows, входящего в ваше решение.

#### <a name="test-push-notifications-in-your-windows-app"></a>Тестирование push-уведомлений в приложении Windows
1. В Visual Studio щелкните правой кнопкой мыши проект Windows и выберите **Назначить запускаемым проектом**.
2. Нажмите клавишу hello **запуска** кнопку toobuild hello проект и запустить приложение hello.
3. В приложение hello, введите имя для нового todoitem и нажмите кнопку hello плюс (**+**) tooadd значок его.
4. Проверка получения уведомления при добавлении элемента hello.

## <a name="next-steps"></a>Дальнейшие действия
Вы можете узнать больше о push-уведомлениях.

* [Диагностика неполадок, связанных с push-уведомлениями](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  Существуют различные причины, по которым уведомления могут теряться или не доходить до устройств. В этом разделе показано, как tooanalyze и выясните, hello корневой причиной сбоев уведомлений push.

Можно также перейти на tooone из hello следующие учебники:

* [Добавить приложение tooyour проверки подлинности](app-service-mobile-xamarin-forms-get-started-users.md)  
  Узнайте, как пользователи tooauthenticate приложения с поставщиком удостоверений.
* [Включение автономной синхронизации для приложения](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Узнайте, как tooadd поддержке приложения с помощью мобильных приложений серверной части. Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением (&mdash;просматривать, добавлять или изменять данные&mdash;) даже при отсутствии подключения к сети.

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
