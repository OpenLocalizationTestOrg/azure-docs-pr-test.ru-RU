1. <span data-ttu-id="1fd2a-101">В вашей **приложения** проекта, откройте hello файл `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-101">In your **app** project, open hello file `AndroidManifest.xml`.</span></span> <span data-ttu-id="1fd2a-102">В коде hello в следующих двух шагах hello замените  *`**my_app_package**`*  с именем hello hello пакета приложения для проекта.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-102">In hello code in hello next two steps, replace *`**my_app_package**`* with hello name of hello app package for your project.</span></span> <span data-ttu-id="1fd2a-103">Это значение hello hello `package` атрибут hello `manifest` тег.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-103">This is hello value of hello `package` attribute of hello `manifest` tag.</span></span>
2. <span data-ttu-id="1fd2a-104">Добавьте следующие новые разрешения после существующих hello hello `uses-permission` элемента:</span><span class="sxs-lookup"><span data-stu-id="1fd2a-104">Add hello following new permissions after hello existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="1fd2a-105">Добавьте следующий код после hello hello `application` открывающий тег:</span><span class="sxs-lookup"><span data-stu-id="1fd2a-105">Add hello following code after hello `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="1fd2a-106">Привет открыть файл *ToDoActivity.java*и добавьте следующие инструкции import hello:</span><span class="sxs-lookup"><span data-stu-id="1fd2a-106">Open hello file *ToDoActivity.java*, and add hello following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="1fd2a-107">Добавьте следующий класс частной переменной toohello hello.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-107">Add hello following private variable toohello class.</span></span> <span data-ttu-id="1fd2a-108">Замените  *`<PROJECT_NUMBER>`*  с номером проекта hello, присвоенный Google tooyour приложения в предшествующий процедура hello.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-108">Replace *`<PROJECT_NUMBER>`* with hello project number assigned by Google tooyour app in hello preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="1fd2a-109">Изменить определение hello *MobileServiceClient* из **закрытый** слишком**открытые статические**, поэтому теперь выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1fd2a-109">Change hello definition of *MobileServiceClient* from **private** too**public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="1fd2a-110">Добавление новых уведомлений toohandle класса.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-110">Add a new class toohandle notifications.</span></span> <span data-ttu-id="1fd2a-111">В обозревателе проектов откройте hello **src** > **основной** > **java** узлов и щелкните правой кнопкой мыши hello пакета имя узла.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-111">In Project Explorer, open hello **src** > **main** > **java** nodes, and right-click hello package name node.</span></span> <span data-ttu-id="1fd2a-112">Выберите **Создать** и **Java Class** (Класс Java).</span><span class="sxs-lookup"><span data-stu-id="1fd2a-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="1fd2a-113">В поле **Имя** введите `MyHandler` и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="1fd2a-114">В файле MyHandler hello замените объявление класса hello с:</span><span class="sxs-lookup"><span data-stu-id="1fd2a-114">In hello MyHandler file, replace hello class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="1fd2a-115">Добавьте следующие инструкции импорта для hello hello `MyHandler` класса:</span><span class="sxs-lookup"><span data-stu-id="1fd2a-115">Add hello following import statements for hello `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="1fd2a-116">После этого добавьте этот элемент toohello `MyHandler` класса:</span><span class="sxs-lookup"><span data-stu-id="1fd2a-116">Next add this member toohello `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="1fd2a-117">В hello `MyHandler` добавьте следующий код toooverride hello hello **onRegistered** метод, который регистрирует устройство с концентратором уведомлений hello мобильной службы.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-117">In hello `MyHandler` class, add hello following code toooverride hello **onRegistered** method, which registers your device with hello mobile service notification hub.</span></span>

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
       <span data-ttu-id="1fd2a-118">}</span><span class="sxs-lookup"><span data-stu-id="1fd2a-118">}</span></span>
13. <span data-ttu-id="1fd2a-119">В hello `MyHandler` добавьте следующий код toooverride hello hello **onReceive** метод, который вызывает toodisplay hello уведомление при получении.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-119">In hello `MyHandler` class, add hello following code toooverride hello **onReceive** method, which causes hello notification toodisplay when it is received.</span></span>

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
       <span data-ttu-id="1fd2a-120">}</span><span class="sxs-lookup"><span data-stu-id="1fd2a-120">}</span></span>
14. <span data-ttu-id="1fd2a-121">Обратно в файл TodoActivity.java hello, обновите hello **onCreate** метод hello *ToDoActivity* класса класса обработчика уведомлений tooregister hello.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-121">Back in hello TodoActivity.java file, update hello **onCreate** method of hello *ToDoActivity* class tooregister hello notification handler class.</span></span> <span data-ttu-id="1fd2a-122">Убедитесь, что tooadd этот код после hello *MobileServiceClient* создается.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-122">Make sure tooadd this code after hello *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="1fd2a-123">Приложение сейчас обновленные toosupport push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="1fd2a-123">Your app is now updated toosupport push notifications.</span></span>
