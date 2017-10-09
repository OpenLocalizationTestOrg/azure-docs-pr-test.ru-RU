---
title: "aaaGet работы с концентраторами уведомлений для приложений Xamarin.Android | Документы Microsoft"
description: "В этом учебнике вы узнаете, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa приложения Xamarin Android."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a>Приступая к работе с Центрами уведомлений для приложений Xamarin в Android
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Обзор
Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa Xamarin.Android приложения.
Вы создаете пустое приложение Xamarin.Android, которое получает push-уведомления с помощью Google Cloud Messaging (GCM). После завершения вы будете иметь доступ toouse вашей toobroadcast концентратора уведомлений push-уведомления tooall hello устройств под управлением приложения. Hello готовой код находится в hello [приложения NotificationHubs] [ GitHub] образца.

В этом учебнике показано простой сценарий широковещательных hello в с использованием концентраторов уведомлений.

## <a name="before-you-begin"></a>Перед началом работы
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

код завершения Hello в этом учебнике можно найти на GitHub [здесь](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).

## <a name="prerequisites"></a>Предварительные требования
Этот учебник требует hello следующее:

* Visual Studio с расширением Xamarin для Windows или Xamarin Studio для Mac OS X. Инструкции по установке см. в [руководстве по установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* Активная учетная запись Google
* [Компонент обмена сообщениями в Azure]
* [Компонент клиента Google Cloud Messaging]

Для прохождения других учебников, посвященных Центрам уведомлений для приложений Xamarin.Android, необходимо сначала выполнить действия, описанные в этом учебнике.

> [!IMPORTANT]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).
> 
> 

## <a name="enable-google-cloud-messaging"></a>Включение Google Cloud Messaging
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a>Настройка концентратора уведомлений
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p>Нажмите кнопку hello <b>Настройка</b> вверху hello, введите hello <b>ключ API</b> значение, полученное в предыдущем разделе hello, а затем нажмите кнопку <b>Сохранить</b>.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)

Концентратор уведомлений теперь настроенных toowork с GCM, и у вас есть hello соединения строки tooboth зарегистрировать уведомления tooreceive приложения и toosend push-уведомлений.

## <a name="connect-your-app-toohello-notification-hub"></a>Подключение приложения toohello концентратор уведомлений
### <a name="create-a-new-project"></a>Создание нового проекта
1. В Xamarin Studio щелкните **New Solution** (Создать решение), **Android App** (Приложение Android) и нажмите кнопку **Next** (Далее).
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. Введите значения в поля **App Name** (Имя приложения) и **Identifier** (Идентификатор). Нажмите кнопку hello **целевых платформ это** toosupport и нажмите кнопку **Далее** и **создать**.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    Будет создан проект Android.

1. Откройте свойства проекта hello, щелкнув правой кнопкой мыши новый проект в hello представление решений и выбрав **параметры**. Выберите hello **приложения Android** элемента в hello **построения** раздела.
   
    Убедитесь, что hello первую букву вашей **имя пакета** производится в нижнем регистре.
   
   > [!IMPORTANT]
   > Hello первой буквы имени пакета hello должны быть строчными. В противном случае возникнут ошибки манифеста приложения при регистрации **BroadcastReceiver** и **IntentFilter** для push-уведомлений ниже.
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. При необходимости набор hello **Android Минимальная версия** tooanother уровень API.
3. При необходимости набор hello **Android целевой версии** toohello другая версия API, которые должны tootarget (должен быть уровень API 8 или более поздней).

Нажмите кнопку **ОК** и диалогового окна параметров проекта закрыть hello.

### <a name="add-hello-required-components-tooyour-project"></a>Добавление проекта tooyour hello необходимые компоненты
Hello облака обмена сообщениями клиент Google на hello хранилище компонентов Xamarin упрощает процесс hello поддержки push-уведомлений в Xamarin.Android.

1. Щелкните правой кнопкой мыши папку hello компоненты в приложении Xamarin.Android и выберите **получить более компонентов**.
2. Поиск hello **обмена сообщениями Azure** компонента и добавьте его в проект toohello.
3. Поиск hello **клиент обмена сообщениями Google облака** компонента и добавьте его в проект toohello.

### <a name="set-up-notification-hubs-in-your-project"></a>Настройка центров уведомлений в проекте
1. Соберите следующую информацию для вашей Android приложения и концентратор уведомлений hello.
   
   * **GoogleProjectNumber**: это значение номер проекта можно получить из сводки hello приложения на портал разработчиков Google hello. Был записан на более ранних версий этого значения при создании приложения hello на портале hello.
   * **Прослушивание строка подключения**: hello в hello мониторинга [классический портал Azure], нажмите кнопку **Просмотр строк подключения**. Копировать hello *DefaultListenSharedAccessSignature* строку подключения для этого значения.
   * **Имя концентратора**: hello имя концентратора, из hello [классический портал Azure]. Например, *mynotificationhub2*.
     
     Создание **Constants.cs** класса для проекта Xamarin и определите следующие константы в классе hello hello. Замените значения заполнителей hello.
     
       public static class Constants   {
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       }
2. Добавьте hello следующие операторы using слишком**MainActivity.cs**:
   
        using Android.Util;
        using Gcm.Client;
3. Добавьте экземпляр переменной toohello `MainActivity` класс, который будет использоваться tooshow диалогового окна предупреждения при запуске приложение hello:
   
        public static MainActivity instance;
4. Создайте следующий метод в hello hello **MainActivity** класса:
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. В hello `OnCreate` метод **MainActivity.cs**, инициализировать hello `instance` переменной и добавить вызов слишком`RegisterWithGCM`:
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. Создайте класс **MyBroadcastReceiver**.
   
   > [!NOTE]
   > Здесь мы рассмотрим создание класса **BroadcastReceiver** с нуля. Тем не менее Создание быстрого альтернативных toomanually **MyBroadcastReceiver.cs** — toorefer toohello **GcmService.cs** файл найден в проекте Xamarin.Android образец hello, входящий в состав hello [Образцы NotificationHubs][GitHub]. Дублирование **GcmService.cs** и изменение имен класса может быть также toostart отличное место.
   > 
   > 
7. Добавьте следующее hello с помощью инструкций слишком**MyBroadcastReceiver.cs** (ссылается компонент toohello и сборки, который был добавлен ранее):
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. В **MyBroadcastReceiver.cs**, добавить следующие запросы разрешений между hello hello **с помощью** инструкций и hello **имен** объявление:
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. В **MyBroadcastReceiver.cs**, измените hello **MyBroadcastReceiver** класса toomatch hello следующее:
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. Добавьте в файл **MyBroadcastReceiver.cs** еще один класс с именем **PushHandlerService**, сделав его производным от **GcmServiceBase**. Убедитесь, что hello tooapply **службы** toohello класс атрибута:
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. **GcmServiceBase** реализует методы **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** и **OnError()**. Наш **PushHandlerService** реализации класса необходимо переопределить эти методы, и эти методы будут срабатывать в ответ toointeracting с концентратором уведомлений hello.
12. Переопределить hello **OnRegistered()** метод в **PushHandlerService** с помощью hello, следующий код:
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > В hello **OnRegistered()** кода выше, следует иметь в виду tooregister hello возможность toospecify тегов для определенных каналов обмена сообщениями.
    > 
    > 
13. Переопределить hello **OnMessage** метод в **PushHandlerService** с помощью hello, следующий код:
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. Добавьте следующее hello **createNotification** и **dialogNotify** методы слишком**PushHandlerService** для уведомления пользователей при получении уведомления.
    
    > [!NOTE]
    > Структура уведомлений в версии платформы Android 5.0 и более поздних версиях существенно отличается от структуры в предыдущих версиях. Если вы тестируете, Android 5.0 или более поздней версии, приложение hello потребуется toobe под управлением tooreceive hello уведомления. Дополнительные сведения см. в статье об [уведомлениях Android](http://go.microsoft.com/fwlink/?LinkId=615880).
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. Переопределите абстрактные члены **OnUnRegistered()**, **OnRecoverableError()** и **OnError()** для компиляции кода:
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a>Запуск приложения в эмуляторе hello
Если запустить это приложение в эмуляторе hello, убедитесь, что используется виртуального устройства Android (AVD), поддерживающий Google API-интерфейсы.

> [!IMPORTANT]
> В порядке tooreceive извещающих уведомлений необходимо настроить учетную запись Google на виртуального устройства Android. (В эмуляторе hello перейдите слишком**параметры** и нажмите кнопку **добавить учетную запись**.) Кроме того убедитесь, что эмулятор, hello — подключенных toohello Интернета.
> 
> [!NOTE]
> Структура уведомлений в версии платформы Android 5.0 и более поздних версиях существенно отличается от структуры в предыдущих версиях. Дополнительные сведения см. в статье об [уведомлениях Android](http://go.microsoft.com/fwlink/?LinkId=615880).
> 
> 

1. В меню **Tools** (Средства) щелкните **Open Android Emulator Manager** (Открыть диспетчер эмулятора Android), выберите свое устройство и нажмите кнопку **Edit** (Изменить).
   
      ![][18]
2. В разделе **Target** (Цель) выберите **Google APIs** (API-интерфейсы Google), а затем нажмите кнопку **ОК**.
   
      ![][19]
3. На верхней панели инструментов hello, нажмите кнопку **запуска**, а затем выберите приложение. Это запускает эмулятор hello и приложение hello.
   
   приложение Hello извлекает hello *registrationId* из GCM и регистры с концентратором уведомлений hello.

## <a name="send-notifications-from-your-backend"></a>Отправка уведомлений из серверной части
Можно проверить получение уведомлений в приложение путем отправки уведомления в hello [классический портал Azure] через hello вкладки отладчика на концентраторе уведомлений hello, как показано ниже экрана приветствия.

![][30]

Push-уведомления обычно отправляются в серверной службе, например мобильными службами или ASP.NET, с помощью совместимой библиотеки. Также можно использовать hello REST API напрямую toosend уведомления сообщений, если библиотека недоступна для серверной части.

Ниже приведен список некоторых учебников, которые можно tooreview для отправки уведомлений.

* ASP.NET: В разделе [toousers уведомления toopush использования концентраторов уведомлений].
* Azure Java концентраторы уведомлений SDK: в разделе [как toouse концентраторы уведомлений из Java](notification-hubs-java-push-notification-tutorial.md) для отправки уведомлений из Java. Было протестировано в Eclipse для разработки для Android.
* PHP: В разделе [как концентраторы уведомлений из PHP toouse](notification-hubs-php-push-notification-tutorial.md).

В подразделах следующего hello учебника hello отправлять уведомления с помощью консольного приложения .NET, а также с помощью мобильной службы через узел сценария.

#### <a name="optional-send-notifications-by-using-a-net-app"></a>(Необязательно) Отправка уведомлений с помощью приложения .NET
В этом разделе мы будем отправлять уведомления с помощью консольного приложения .NET.

1. Создайте новое консольное приложение Visual C#.
   
      ![][20]
2. В Visual Studio последовательно выберите элементы **Сервис**, **Диспетчер пакетов NuGet** и **Консоль диспетчера пакетов**.
   
    Откроется консоль диспетчера пакетов hello в Visual Studio.
3. В hello в окне консоли диспетчера пакетов, задайте hello **проекта по умолчанию** tooyour нового консольного приложения проекта, а затем в окне консоли hello, выполните hello следующую команду:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    При этом добавляется ссылка toohello концентраторов уведомлений Azure SDK с помощью hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакет NuGet концентраторов Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Откройте файл Program.cs hello и добавьте следующее hello `using` инструкции:
   
        using Microsoft.Azure.NotificationHubs;
5. В вашей `Program` добавьте следующий метод hello. Обновление текста заполнителя hello с вашей *DefaultFullSharedAccessSignature* имя концентратора и строку соединения из hello [классический портал Azure].
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. Добавьте следующие строки в hello вашей **Main** метод:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Нажмите клавишу приложение hello ключа toorun F5 hello. Вы должны получить уведомление в приложение hello.
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a>(Необязательно) Отправка уведомлений с помощью мобильной службы
1. Выполните действия, описанные в статье [Приступая к работе с мобильными службами].
2. Войдите в toohello [классический портал Azure]и выберите мобильной службы.
3. Выберите hello **планировщика** вкладки в верхней части hello.
   
      ![][22]
4. Создайте новое запланированное задание, вставьте имя и выберите **По запросу**.
   
      ![][23]
5. При создании задания hello, щелкните имя задания hello. Нажмите кнопку hello **сценарий** вкладку на верхней панели hello.
6. Вставьте следующий сценарий внутри функции планировщика hello. Убедитесь, что tooreplace hello местозаполнителей уведомления имя и hello строку подключения к концентратору для *DefaultFullSharedAccessSignature* , полученный ранее. Щелкните **Сохранить**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. Нажмите кнопку **выполнить один раз** на нижней панели hello. Вы получите всплывающее уведомление.

## <a name="next-steps"></a>Дальнейшие действия
В этом простом примере вы широковещательной рассылки уведомлений tooall устройства Android. В заказ tootarget определенным пользователям, см. Учебник toohello [toousers уведомления toopush использования концентраторов уведомлений]. Следует ли toosegment пользователям по группы интересов, можно прочитать [toosend использования концентраторов уведомлений, новости]. Дополнительные сведения о toouse концентраторов уведомлений в [руководство концентраторы уведомлений] и в hello [Android toofor как концентраторы уведомлений].

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Приступая к работе с мобильными службами]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[классический портал Azure]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[руководство концентраторы уведомлений]: http://msdn.microsoft.com/library/jj927170.aspx
[Android toofor как концентраторы уведомлений]: http://msdn.microsoft.com/library/dn282661.aspx

[toousers уведомления toopush использования концентраторов уведомлений]: /manage/services/notification-hubs/notify-users-aspnet
[toosend использования концентраторов уведомлений, новости]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Компонент клиента Google Cloud Messaging]: http://components.xamarin.com/view/GCMClient/
[Компонент обмена сообщениями в Azure]: http://components.xamarin.com/view/azure-messaging
