---
title: "aaaGet работы с концентраторами уведомлений Azure для Kindle приложений | Документы Microsoft"
description: "В этом учебнике вы узнаете, как концентраторы уведомлений Azure toosend toouse push-уведомления tooa электронная версия приложения."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a>Приступая к работе с Центрами уведомлений для приложений Kindle
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Обзор
Этот учебник показывает, как концентраторы уведомлений Azure toosend toouse push-уведомления tooa электронная версия приложения.
Вы создаете пустое приложение Kindle, которое получает push-уведомления с помощью Amazon Device Messaging (ADM).

## <a name="prerequisites"></a>Предварительные требования
Этот учебник требует hello следующее:

* Получение hello пакета SDK для Android (предполагается, что используется Eclipse) из hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android сайта</a>.
* Следуйте указаниям hello <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">параметр вверх разработки среды</a> tooset среды разработки для Kindle.

## <a name="add-a-new-app-toohello-developer-portal"></a>Добавить новый портал для разработчиков приложений toohello
1. Во-первых, создайте приложение в hello [портала для разработчиков Amazon].
   
    ![][0]
2. Копировать hello **ключ приложения**.
   
    ![][1]
3. На портале hello, щелкните имя приложения hello и нажмите кнопку hello **обмена сообщениями на устройстве** вкладки.
   
    ![][2]
4. Щелкните **Создать новый профиль безопасности**, затем создайте профиль безопасности (например, **Профиль безопасности TestAdm**). Нажмите кнопку **Сохранить**.
   
    ![][3]
5. Нажмите кнопку **профили безопасности** tooview hello безопасности профиль, который вы только что создали. Копировать hello **идентификатор клиента** и **секрет клиента** значения для последующего использования.
   
    ![][4]

## <a name="create-an-api-key"></a>Создание ключа API
1. Откройте окно командной строки с правами администратора.
2. Перейдите в папку toohello пакета SDK для Android.
3. Введите следующую команду hello:
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. Для hello **keystore** пароль, введите **android**.
5. Копировать hello **MD5** отпечатков пальцев.
6. Обратно на портале разработчика hello, hello **обмен сообщениями** щелкните **Android/Kindle** и введите имя hello hello пакета приложения (например, **com.sample.notificationhubtest**) и hello **MD5** значение, а затем нажмите кнопку **создать ключ API**.

## <a name="add-credentials-toohello-hub"></a>Добавить концентратор toohello учетные данные
В портал hello добавьте hello клиента секрета и клиент идентификатор toohello **Настройка** вкладку центра уведомлений.

## <a name="set-up-your-application"></a>Настройка приложения
> [!NOTE]
> При создании приложения используйте API уровня не ниже 17.
> 
> 

Добавьте проект библиотеки tooyour Eclipse для hello ADM.

1. Библиотека ADM hello tooobtain, [загрузить hello SDK]. Извлеките ZIP-файл пакета SDK для hello.
2. В Eclipse щелкните правой кнопкой мыши по проекту и выберите **Свойства**. Выберите **путь построения Java** hello слева и выберите hello ** библиотеки ** вкладку вверху hello. Нажмите кнопку **добавить внешний Jar**и выберите hello файл `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` из каталога hello извлечен hello Amazon SDK.
3. Загрузите hello NotificationHubs пакета SDK для Android (ссылка).
4. Распакуйте пакет hello, а затем перетащите файл hello `notification-hubs-sdk.jar` в hello `libs` папки в Eclipse.

Измените ADM манифеста toosupport вашего приложения.

1. Добавьте пространство имен Amazon hello в hello корневого манифеста элемента:

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. Добавьте разрешения в качестве hello первый элемент в элементе манифеста hello. Замена **[ПАКЕТА имя]** с hello пакета используется toocreate приложения.
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. Вставьте следующий элемент как первый дочерний элемент приложения hello hello hello. Помните, toosubstitute **[имя службы]** с именем hello ADM обработчика сообщений, которые создаются в следующем разделе hello (включая пакет hello) и замените **[ПАКЕТА имя]** с hello Имя пакета, в котором для создания приложения.
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a>Создание обработчика сообщений ADM
1. Создайте новый класс, наследующий от `com.amazon.device.messaging.ADMMessageHandlerBase` и назовите его `MyADMMessageHandler`, как показано в следующий рисунок hello:
   
    ![][6]
2. Добавьте следующее hello `import` инструкции:
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. Добавьте следующий код в созданный класс hello hello. Запомните toosubstitute hello концентратора имя и строку соединения (прослушивания):
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. Добавьте следующий код toohello hello `OnMessage()` метод:
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. Добавьте следующий код toohello hello `OnRegistered` метод:
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. Добавьте следующий код toohello hello `OnUnregistered` метод:
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. В hello `MainActivity` метод, добавьте следующие инструкции import hello:
   
        import com.amazon.device.messaging.ADM;
8. Добавьте следующий код в конце hello hello hello `OnCreate` метод:
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-tooyour-app"></a>Добавить приложение tooyour ключа API
1. В Eclipse, создайте новый файл с именем **api_key.txt** в ресурсах hello каталог проекта.
2. Привет открыть файл и скопируйте hello API ключ, который был создан в портале для разработчиков Amazon hello.

## <a name="run-hello-app"></a>Выполните приложение hello
1. Запустите эмулятор hello.
2. В эмуляторе hello проведите сверху hello и нажмите кнопку **параметры**, а затем нажмите кнопку **моей учетной записи** и зарегистрировать с помощью действительной учетной записи Amazon.
3. В Eclipse запустите приложение hello.

> [!NOTE]
> Если возникнут проблемы, проверьте время hello эмулятор hello (или устройства). значение времени Hello должно быть точным. время hello toochange hello электронная версия эмулятора, можно запустить следующую команду из каталога средства платформы Android SDK hello:
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a>Отправка сообщения
toosend сообщения с помощью .NET:

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[портала для разработчиков Amazon]: https://developer.amazon.com/home.html
[загрузить hello SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
