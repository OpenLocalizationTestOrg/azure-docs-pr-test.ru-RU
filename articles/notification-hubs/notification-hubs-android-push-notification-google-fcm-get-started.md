---
title: "tooAndroid уведомления aaaSending принудительной с концентраторами уведомлений Azure и Firebase Cloud Messaging | Документы Microsoft"
description: "В этом учебнике вы узнаете, как toouse концентраторов уведомлений Azure и Firebase Cloud Messaging toopush уведомления tooAndroid устройств."
services: notification-hubs
documentationcenter: android
keywords: "push-уведомления, push-уведомление, push-уведомление android, FCM, Firebase Cloud Messaging"
author: ysxu
manager: erikre
editor: 
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/14/2016
ms.author: yuaxu
ms.openlocfilehash: d2e57437ac7b0ef77abf048f991043620621e58d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a>Отправка push tooAndroid уведомлений с концентраторами уведомлений Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Обзор
> [!IMPORTANT]
> В этой статье описывается отправка push-уведомлений с помощью Google Firebase Cloud Messaging (FCM). Если вы все еще используете Google Cloud Messaging (GCM), см. раздел [tooAndroid уведомления Принудительная отправка с концентраторами уведомлений Azure и GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

Этот учебник показывает, как toouse концентраторов уведомлений Azure и toosend Firebase Cloud Messaging push-уведомления tooan Android приложения.
Вы создадите пустое приложение Android, которое получает push-уведомления с помощью Firebase Cloud Messaging.

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Hello завершения кода в этом учебнике можно загрузить с сайта GitHub [здесь](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).

## <a name="prerequisites"></a>Предварительные требования
> [!IMPORTANT]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).
> 
> 

* Кроме учетной записи Azure active tooan упоминалось выше, упражнений этого учебника требуется hello последнюю версию [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).
* Android версии 2.3 или более поздней.
* Репозиторий Google версии 27 или более поздней.
* Службы Google Play версии 9.0.2 или более поздней.
* Завершение изучения этого учебника является необходимым условием для работы со всеми другими учебниками, посвященными Центрам уведомлений для приложений Android.

## <a name="create-a-new-android-studio-project"></a>Создание проекта Android Studio
1. В Android Studio создайте новый проект Android Studio.
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. Выберите hello **телефонов и планшетных ПК** форме коэффициент и hello **SDK минимум** нужных toosupport. Нажмите кнопку **Далее**.
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. Выберите **пустое действие** hello основных действий, щелкните **Далее**, а затем нажмите кнопку **Готово**.

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Создание проекта с поддержкой Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>Настройка нового центра уведомлений
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6. В hello **параметры** колонке центра уведомлений, выберите **служб Notification Services** и затем **Google (GCM)**. Введите ключ сервера FCM hello, скопированное ранее из hello [консоли Firebase](https://firebase.google.com/console/) и нажмите кнопку **Сохранить**.

&emsp;&emsp;![Центры уведомлений Azure — Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

Концентратор уведомлений теперь настроенный toowork с Messagin Firebase облака и у вас есть tooboth строки подключения hello регистрации вашего приложения tooreceive и отправки push-уведомлений.

## <a id="connecting-app"></a>Подключение приложения toohello концентратор уведомлений
### <a name="add-google-play-services-toohello-project"></a>Добавление проекта toohello служб Google Play
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>Добавление библиотек Центров уведомлений Azure
1. В hello `Build.Gradle` файл для hello **приложения**, добавить следующие строки в hello hello **зависимости** раздела.
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. Добавьте следующий репозиторий после hello hello **зависимости** раздела.
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a>Обновление hello AndroidManifest.xml.
1. toosupport FCM, мы должны реализовать службу прослушивателя идентификатор экземпляра в наш код, который используется слишком[получать маркеры регистрации](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) с помощью [Google FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId). В этом учебнике мы назвать класс hello `MyInstanceIDService`. 
   
    Добавьте следующий файл определения службы toohello AndroidManifest.xml, внутри hello hello `<application>` тег. 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. После наших маркер регистрации FCM сотрудничают с hello FirebaseInstanceId API, мы будем использовать слишком[зарегистрироваться hello концентратор уведомлений Azure](notification-hubs-push-notification-registration-management.md). Поддерживаются регистрация с помощью фоновой hello `IntentService` с именем `RegistrationIntentService`. Кроме того, эта служба будет отвечать за обновление маркера регистрации в FCM.
   
    Добавьте следующий файл определения службы toohello AndroidManifest.xml, внутри hello hello `<application>` тег. 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. Также мы определим tooreceive получателя уведомлений. Добавьте следующие определения toohello AndroidManifest.xml файл приемника, внутри hello hello `<application>` тег. Замените hello `<your package>` заполнитель hello ваше имя самого пакета отображается вверху hello hello `AndroidManifest.xml` файла.
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. Добавьте следующие необходимые FCM hello, связанные с разрешениями ниже hello `</application>` тег. Убедитесь, что tooreplace `<your package>` с именем пакета hello показано вверху hello hello `AndroidManifest.xml` файла.
   
    Дополнительные сведения об этих разрешений см. в разделе [установки GCM клиентского приложения для Android](https://developers.google.com/cloud-messaging/android/client#manifest) и [перенести GCM клиентского приложения для Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a>Добавление кода
1. В hello представления проекта, разверните **приложения** > **src** > **основной** > **java**. Щелкните правой кнопкой мыши папку пакета в **java**, щелкните **New** (Создать) и выберите **Java Class** (Класс Java). Добавьте новый класс с именем `NotificationSettings`. 
   
    ![Android Studio — новый класс Java](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    Убедитесь, что эти три заполнители в следующий код для hello hello hello tooupdate `NotificationSettings` класса:
   
   * **Идентификатор отправителя**: hello идентификатор отправителя, полученные ранее в hello **Cloud Messaging** параметров проекта в hello [Firebase консоли](https://firebase.google.com/console/).
   * **HubListenConnectionString**: hello **DefaultListenAccessSignature** строку подключения для концентратор. Можно скопировать этой строки подключения, нажав кнопку **политики доступа** на hello **параметры** колонке концентратора, на hello [портала Azure].
   * **HubName**: используйте имя hello центра уведомлений, появится в колонке концентратора hello в hello [портала Azure].
     
     `NotificationSettings` :
     
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       }
2. Используя описанные выше действия hello, добавьте новый класс с именем `MyInstanceIDService`. Таким образом мы выполним реализацию службы прослушивания идентификаторов экземпляра.
   
    Hello код для этого класса будут вызывать нашей `IntentService` слишком[FCM токен обновления hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) в фоновом режиме hello.
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.firebase.iid.FirebaseInstanceIdService;

        public class MyInstanceIDService extends FirebaseInstanceIdService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.d(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. Добавьте еще один новый класс tooyour проект с именем `RegistrationIntentService`. Это будет hello реализацию для наших `IntentService` , обрабатывающий [обновление токен hello FCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) и [регистрации с концентратором уведомлений hello](notification-hubs-push-notification-registration-management.md).
   
    Используйте следующий код для этого класса hello.
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;        
        import com.google.firebase.iid.FirebaseInstanceId;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {
   
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
                String storedToken = null;
   
                try {
                    String FCM_token = FirebaseInstanceId.getInstance().getToken();
                    Log.d(TAG, "FCM Registration Token: " + FCM_token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if hello token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete registration", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. В вашей `MainActivity` класса, добавьте следующее hello `import` приведенные выше hello инструкции объявления класса.
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. Добавьте следующие закрытые члены вверху hello класс hello hello. Мы будем использовать эти [Проверьте доступность службы Google Play hello согласно рекомендациям Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. В вашей `MainActivity` добавьте следующий метод toohello доступность службы Google Play hello. 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. В вашей `MainActivity` добавьте следующий код, который будет искать службы Google Play перед вызовом hello вашей `IntentService` tooget ваш токен FCM регистрации и регистрации в концентраторе уведомлений.
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. В hello `OnCreate` метод hello `MainActivity` добавьте hello следующий процесс регистрации hello toostart кода при создании действия.
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. Добавить эти дополнительные методы toohello `MainActivity` tooverify состояния и отчетов состояния приложения в вашем приложении.
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. Hello `ToastNotify` метод использует hello *«Hello World»* `TextView` управления tooreport состояние и оповещения, сохраняемым в приложение hello. В макете activity_main.xml добавьте hello, код подписки для этого элемента управления.
   
       android:id="@+id/text_hello"
9. Далее мы добавим подкласс для наших приемника, определенный в hello AndroidManifest.xml. Добавьте еще один новый класс tooyour проект с именем `MyHandler`.
10. Добавьте следующие инструкции импорта вверху hello hello `MyHandler.java`:
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. Добавьте следующий код для hello hello `MyHandler` класс, сделав его подкласс `com.microsoft.windowsazure.notifications.NotificationsHandler`.
    
    Этот код переопределяет hello `OnReceive` метод, поэтому обработчик hello сообщит уведомлений, полученных. Обработчик Hello также отправляет диспетчер hello принудительной уведомлений toohello Android уведомление с помощью hello `sendNotification()` метод. Hello `sendNotification()` следует выполнить метод, если приложение hello не выполняется и получает уведомление.
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. В Android Studio hello меню щелкните **построения** > **перестроить проект** toomake убедиться, что, присутствуют в коде нет ошибок.
13. Запустите приложение hello на устройстве и убедитесь, что он успешно регистрируется с концентратором уведомлений hello. 
    
    > [!NOTE]
    > Регистрация может завершиться ошибкой при изначальном hello до hello `onTokenRefresh()` вызывается метод экземпляра идентификатора службы. Обновление Hello следует пакетам успешной регистрации с концентратором уведомлений hello.
    > 
    > 

## <a name="sending-push-notifications"></a>Отправка push-уведомлений
Вы можете протестировать получения push-уведомлений в приложение, отправляя их через hello [портала Azure] -искать hello **Устранение неполадок** статьи в колонке концентратора hello, как показано ниже.

![Центры уведомлений Azure — тестовая отправка](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a>(Необязательно) Отправлять push-уведомления прямо из приложения hello
> [!IMPORTANT]
> В этом примере отправки уведомлений из клиентского приложения hello предоставляется только в целях обучения. Так как для этого потребуется hello `DefaultFullSharedAccessSignature` toobe на клиентское приложение hello, он предоставляет, пользователь может получить уведомления toosend несанкционированный доступ клиентов tooyour риск toohello концентратора уведомлений.
> 
> 

Обычно уведомления отправляются с сервера базы данных. В некоторых случаях может потребоваться toobe push-уведомлений может toosend непосредственно из клиентского приложения hello. В этом разделе описывается, как toosend уведомления с помощью клиента hello hello [API REST для концентратора уведомлений Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).

1. В представлении проекта Android Studio разверните узел **App** > **src** > **main** > **res** > **layout**. Откройте hello `activity_main.xml` макета и выберите пункт hello **текст** вкладке tooupdate hello текстовое содержимое файла hello. Обновите его с hello кода, который добавляет новые `Button` и `EditText` элементы управления для отправки push-концентратор уведомлений toohello сообщения уведомления. Добавьте следующий код в нижней hello непосредственно перед `</RelativeLayout>`.
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. В представлении проекта Android Studio разверните узел **App** > **src** > **main** > **res** > **values**. Откройте hello `strings.xml` и добавьте hello строковых значений, на которые ссылается hello нового файла `Button` и `EditText` элементов управления. Добавьте следующие hello нижней части файла hello непосредственно перед `</resources>`.
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. В вашей `NotificationSetting.java` файл, добавьте следующий параметр toohello hello `NotificationSettings` класса.
   
    Обновление `HubFullAccess` с hello **DefaultFullSharedAccessSignature** строку подключения для концентратор. В этой строке подключения можно скопировать из hello [портала Azure] , щелкнув **политики доступа** на hello **параметры** колонке концентратор уведомлений.
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. В вашей `MainActivity.java` файл, добавьте следующее hello `import` инструкции выше hello `MainActivity` класса.
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. В вашей `MainActivity.java` файл, добавить следующие члены вверху hello hello hello `MainActivity` класса.    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. Необходимо создать tooauthenticate токена программного обеспечения URL-адреса (SaS) концентратора уведомлений tooyour POST запроса toosend сообщений. Это делается путем синтаксического анализа hello данные ключа из строки подключения hello и последующего создания hello маркер SaS, как упоминалось в hello [основные понятия](http://msdn.microsoft.com/library/azure/dn495627.aspx) Справочник по REST API. Привет, следующий код представляет собой пример реализацию.
   
    В `MainActivity.java`, добавьте следующий метод toohello hello `MainActivity` класса tooparse строки подключения.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. В `MainActivity.java`, добавьте следующий метод toohello hello `MainActivity` класса toocreate маркер проверки подлинности SaS.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. В `MainActivity.java`, добавьте следующий метод toohello hello `MainActivity` hello класс toohandle **отправить уведомление** нажмите кнопку и отправить push-уведомление hello концентратора toohello сообщения с помощью hello встроенных API-интерфейса REST.
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a>Тестирование приложения
#### <a name="push-notifications-in-hello-emulator"></a>Push-уведомлений в эмуляторе hello
Следует tootest push-уведомлений в эмуляторе убедитесь, что образ эмулятора поддерживает уровень Google API hello, выбранное для вашего приложения. Если изображение не поддерживает собственные интерфейсы API Google, вы получите hello **службы\_не\_ДОСТУПНО** исключение.

Кроме toohello выше, убедитесь, что вы добавили запуска эмулятора под учетной записью tooyour вашей Google система **параметры** > **учетные записи**. В противном случае ваш tooregister попыток с GCM может привести к hello **проверки ПОДЛИННОСТИ\_сбой** исключение.

#### <a name="running-hello-application"></a>Запуск приложения hello
1. Выполните приложение hello и обратите внимание, что идентификатор hello регистрации указывается для успешной регистрации.
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. Введите toobe сообщение уведомления, отправленные tooall устройств Android, которые зарегистрированы с концентратором hello.
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. Нажмите кнопку **Send Notification**(Отправить уведомление). Будут показаны все устройства, работающие приложения hello `AlertDialog` экземпляр с hello push-сообщение уведомления. Устройства, нет hello приложение работает, но ранее зарегистрированные push-уведомлений получит уведомление hello диспетчера уведомлений Android. Их можно просмотреть путем считывания вниз от верхнего левого угла hello.
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a>Дальнейшие действия
Мы рекомендуем hello [toousers уведомления toopush использования концентраторов уведомлений] учебника в качестве следующего шага hello. Также будет показано, как уведомления о toosend из серверной части ASP.NET с помощью тегов tootarget конкретных пользователей.

Если требуется toosegment пользователи, группы интересов извлечь hello [toosend использования концентраторов уведомлений, новости] учебника.

toolearn Дополнительные общие сведения о концентраторах уведомлений см. наш [руководство концентраторы уведомлений].

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[руководство концентраторы уведомлений]: notification-hubs-push-notification-overview.md
[toousers уведомления toopush использования концентраторов уведомлений]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[toosend использования концентраторов уведомлений, новости]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[портала Azure]: https://portal.azure.com
