1. В вашей **приложения** проекта, откройте hello файл `AndroidManifest.xml`. В коде hello в следующих двух шагах hello замените  *`**my_app_package**`*  с именем hello hello пакета приложения для проекта. Это значение hello hello `package` атрибут hello `manifest` тег.
2. Добавьте следующие новые разрешения после существующих hello hello `uses-permission` элемента:

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. Добавьте следующий код после hello hello `application` открывающий тег:

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. Привет открыть файл *ToDoActivity.java*и добавьте следующие инструкции import hello:

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. Добавьте следующий класс частной переменной toohello hello. Замените  *`<PROJECT_NUMBER>`*  с номером проекта hello, присвоенный Google tooyour приложения в предшествующий процедура hello.

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. Изменить определение hello *MobileServiceClient* из **закрытый** слишком**открытые статические**, поэтому теперь выглядит следующим образом:

        public static MobileServiceClient mClient;
7. Добавление новых уведомлений toohandle класса. В обозревателе проектов откройте hello **src** > **основной** > **java** узлов и щелкните правой кнопкой мыши hello пакета имя узла. Выберите **Создать** и **Java Class** (Класс Java).
8. В поле **Имя** введите `MyHandler` и нажмите кнопку **ОК**.

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. В файле MyHandler hello замените объявление класса hello с:

        public class MyHandler extends NotificationsHandler {
10. Добавьте следующие инструкции импорта для hello hello `MyHandler` класса:

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. После этого добавьте этот элемент toohello `MyHandler` класса:

        public static final int NOTIFICATION_ID = 1;
12. В hello `MyHandler` добавьте следующий код toooverride hello hello **onRegistered** метод, который регистрирует устройство с концентратором уведомлений hello мобильной службы.

        @Override
        public void onRegistered(Context context,  final String gcmRegistrationId) {
           super.onRegistered(context, gcmRegistrationId);

           new AsyncTask<Void, Void, Void>() {

               protected Void doInBackground(Void... params) {
                   try {
                       ToDoActivity.mClient.getPush().register(gcmRegistrationId);
                       return null;
                   }
                   catch(Exception e) {
                       // handle error                
                   }
                   return null;              
               }
           }.execute();
       }
13. В hello `MyHandler` добавьте следующий код toooverride hello hello **onReceive** метод, который вызывает toodisplay hello уведомление при получении.

        @Override
        public void onReceive(Context context, Bundle bundle) {
               String msg = bundle.getString("message");

               PendingIntent contentIntent = PendingIntent.getActivity(context,
                       0, // requestCode
                       new Intent(context, ToDoActivity.class),
                       0); // flags

               Notification notification = new NotificationCompat.Builder(context)
                       .setSmallIcon(R.drawable.ic_launcher)
                       .setContentTitle("Notification Hub Demo")
                       .setStyle(new NotificationCompat.BigTextStyle().bigText(msg))
                       .setContentText(msg)
                       .setContentIntent(contentIntent)
                       .build();

               NotificationManager notificationManager = (NotificationManager)
                       context.getSystemService(Context.NOTIFICATION_SERVICE);
               notificationManager.notify(NOTIFICATION_ID, notification);
       }
14. Обратно в файл TodoActivity.java hello, обновите hello **onCreate** метод hello *ToDoActivity* класса класса обработчика уведомлений tooregister hello. Убедитесь, что tooadd этот код после hello *MobileServiceClient* создается.

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    Приложение сейчас обновленные toosupport push-уведомлений.
