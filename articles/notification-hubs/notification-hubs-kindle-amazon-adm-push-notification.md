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
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="6ef47-103">Приступая к работе с Центрами уведомлений для приложений Kindle</span><span class="sxs-lookup"><span data-stu-id="6ef47-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="6ef47-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="6ef47-104">Overview</span></span>
<span data-ttu-id="6ef47-105">Этот учебник показывает, как концентраторы уведомлений Azure toosend toouse push-уведомления tooa электронная версия приложения.</span><span class="sxs-lookup"><span data-stu-id="6ef47-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Kindle application.</span></span>
<span data-ttu-id="6ef47-106">Вы создаете пустое приложение Kindle, которое получает push-уведомления с помощью Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="6ef47-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ef47-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6ef47-107">Prerequisites</span></span>
<span data-ttu-id="6ef47-108">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="6ef47-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="6ef47-109">Получение hello пакета SDK для Android (предполагается, что используется Eclipse) из hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android сайта</a>.</span><span class="sxs-lookup"><span data-stu-id="6ef47-109">Get hello Android SDK (we assume that you will use Eclipse) from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="6ef47-110">Следуйте указаниям hello <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">параметр вверх разработки среды</a> tooset среды разработки для Kindle.</span><span class="sxs-lookup"><span data-stu-id="6ef47-110">Follow hello steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> tooset up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-toohello-developer-portal"></a><span data-ttu-id="6ef47-111">Добавить новый портал для разработчиков приложений toohello</span><span class="sxs-lookup"><span data-stu-id="6ef47-111">Add a new app toohello developer portal</span></span>
1. <span data-ttu-id="6ef47-112">Во-первых, создайте приложение в hello [портала для разработчиков Amazon].</span><span class="sxs-lookup"><span data-stu-id="6ef47-112">First, create an app in hello [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="6ef47-113">Копировать hello **ключ приложения**.</span><span class="sxs-lookup"><span data-stu-id="6ef47-113">Copy hello **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="6ef47-114">На портале hello, щелкните имя приложения hello и нажмите кнопку hello **обмена сообщениями на устройстве** вкладки.</span><span class="sxs-lookup"><span data-stu-id="6ef47-114">In hello portal, click hello name of your app, and then click hello **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="6ef47-115">Щелкните **Создать новый профиль безопасности**, затем создайте профиль безопасности (например, **Профиль безопасности TestAdm**).</span><span class="sxs-lookup"><span data-stu-id="6ef47-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="6ef47-116">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6ef47-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="6ef47-117">Нажмите кнопку **профили безопасности** tooview hello безопасности профиль, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="6ef47-117">Click **Security Profiles** tooview hello security profile that you just created.</span></span> <span data-ttu-id="6ef47-118">Копировать hello **идентификатор клиента** и **секрет клиента** значения для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="6ef47-118">Copy hello **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="6ef47-119">Создание ключа API</span><span class="sxs-lookup"><span data-stu-id="6ef47-119">Create an API key</span></span>
1. <span data-ttu-id="6ef47-120">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="6ef47-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="6ef47-121">Перейдите в папку toohello пакета SDK для Android.</span><span class="sxs-lookup"><span data-stu-id="6ef47-121">Navigate toohello Android SDK folder.</span></span>
3. <span data-ttu-id="6ef47-122">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="6ef47-122">Enter hello following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="6ef47-123">Для hello **keystore** пароль, введите **android**.</span><span class="sxs-lookup"><span data-stu-id="6ef47-123">For hello **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="6ef47-124">Копировать hello **MD5** отпечатков пальцев.</span><span class="sxs-lookup"><span data-stu-id="6ef47-124">Copy hello **MD5** fingerprint.</span></span>
6. <span data-ttu-id="6ef47-125">Обратно на портале разработчика hello, hello **обмен сообщениями** щелкните **Android/Kindle** и введите имя hello hello пакета приложения (например, **com.sample.notificationhubtest**) и hello **MD5** значение, а затем нажмите кнопку **создать ключ API**.</span><span class="sxs-lookup"><span data-stu-id="6ef47-125">Back in hello developer portal, on hello **Messaging** tab, click **Android/Kindle** and enter hello name of hello package for your app (for example, **com.sample.notificationhubtest**) and hello **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-toohello-hub"></a><span data-ttu-id="6ef47-126">Добавить концентратор toohello учетные данные</span><span class="sxs-lookup"><span data-stu-id="6ef47-126">Add credentials toohello hub</span></span>
<span data-ttu-id="6ef47-127">В портал hello добавьте hello клиента секрета и клиент идентификатор toohello **Настройка** вкладку центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6ef47-127">In hello portal, add hello client secret and client ID toohello **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="6ef47-128">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="6ef47-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="6ef47-129">При создании приложения используйте API уровня не ниже 17.</span><span class="sxs-lookup"><span data-stu-id="6ef47-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="6ef47-130">Добавьте проект библиотеки tooyour Eclipse для hello ADM.</span><span class="sxs-lookup"><span data-stu-id="6ef47-130">Add hello ADM libraries tooyour Eclipse project:</span></span>

1. <span data-ttu-id="6ef47-131">Библиотека ADM hello tooobtain, [загрузить hello SDK].</span><span class="sxs-lookup"><span data-stu-id="6ef47-131">tooobtain hello ADM library, [download hello SDK].</span></span> <span data-ttu-id="6ef47-132">Извлеките ZIP-файл пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="6ef47-132">Extract hello SDK zip file.</span></span>
2. <span data-ttu-id="6ef47-133">В Eclipse щелкните правой кнопкой мыши по проекту и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="6ef47-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="6ef47-134">Выберите **путь построения Java** hello слева и выберите hello ** библиотеки ** вкладку вверху hello.</span><span class="sxs-lookup"><span data-stu-id="6ef47-134">Select **Java Build Path** on hello left, and then select hello **Libraries **tab at hello top.</span></span> <span data-ttu-id="6ef47-135">Нажмите кнопку **добавить внешний Jar**и выберите hello файл `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` из каталога hello извлечен hello Amazon SDK.</span><span class="sxs-lookup"><span data-stu-id="6ef47-135">Click **Add External Jar**, and select hello file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from hello directory in which you extracted hello Amazon SDK.</span></span>
3. <span data-ttu-id="6ef47-136">Загрузите hello NotificationHubs пакета SDK для Android (ссылка).</span><span class="sxs-lookup"><span data-stu-id="6ef47-136">Download hello NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="6ef47-137">Распакуйте пакет hello, а затем перетащите файл hello `notification-hubs-sdk.jar` в hello `libs` папки в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="6ef47-137">Unzip hello package, and then drag hello file `notification-hubs-sdk.jar` into hello `libs` folder in Eclipse.</span></span>

<span data-ttu-id="6ef47-138">Измените ADM манифеста toosupport вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="6ef47-138">Edit your app manifest toosupport ADM:</span></span>

1. <span data-ttu-id="6ef47-139">Добавьте пространство имен Amazon hello в hello корневого манифеста элемента:</span><span class="sxs-lookup"><span data-stu-id="6ef47-139">Add hello Amazon namespace in hello root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="6ef47-140">Добавьте разрешения в качестве hello первый элемент в элементе манифеста hello.</span><span class="sxs-lookup"><span data-stu-id="6ef47-140">Add permissions as hello first element under hello manifest element.</span></span> <span data-ttu-id="6ef47-141">Замена **[ПАКЕТА имя]** с hello пакета используется toocreate приложения.</span><span class="sxs-lookup"><span data-stu-id="6ef47-141">Substitute **[YOUR PACKAGE NAME]** with hello package that you used toocreate your app.</span></span>
   
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
2. <span data-ttu-id="6ef47-142">Вставьте следующий элемент как первый дочерний элемент приложения hello hello hello.</span><span class="sxs-lookup"><span data-stu-id="6ef47-142">Insert hello following element as hello first child of hello application element.</span></span> <span data-ttu-id="6ef47-143">Помните, toosubstitute **[имя службы]** с именем hello ADM обработчика сообщений, которые создаются в следующем разделе hello (включая пакет hello) и замените **[ПАКЕТА имя]** с hello Имя пакета, в котором для создания приложения.</span><span class="sxs-lookup"><span data-stu-id="6ef47-143">Remember toosubstitute **[YOUR SERVICE NAME]** with hello name of your ADM message handler that you create in hello next section (including hello package), and replace **[YOUR PACKAGE NAME]** with hello package name with which you created your app.</span></span>
   
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

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="6ef47-144">Создание обработчика сообщений ADM</span><span class="sxs-lookup"><span data-stu-id="6ef47-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="6ef47-145">Создайте новый класс, наследующий от `com.amazon.device.messaging.ADMMessageHandlerBase` и назовите его `MyADMMessageHandler`, как показано в следующий рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="6ef47-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in hello following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="6ef47-146">Добавьте следующее hello `import` инструкции:</span><span class="sxs-lookup"><span data-stu-id="6ef47-146">Add hello following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="6ef47-147">Добавьте следующий код в созданный класс hello hello.</span><span class="sxs-lookup"><span data-stu-id="6ef47-147">Add hello following code in hello class that you created.</span></span> <span data-ttu-id="6ef47-148">Запомните toosubstitute hello концентратора имя и строку соединения (прослушивания):</span><span class="sxs-lookup"><span data-stu-id="6ef47-148">Remember toosubstitute hello hub name and connection string (listen):</span></span>
   
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
4. <span data-ttu-id="6ef47-149">Добавьте следующий код toohello hello `OnMessage()` метод:</span><span class="sxs-lookup"><span data-stu-id="6ef47-149">Add hello following code toohello `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="6ef47-150">Добавьте следующий код toohello hello `OnRegistered` метод:</span><span class="sxs-lookup"><span data-stu-id="6ef47-150">Add hello following code toohello `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="6ef47-151">Добавьте следующий код toohello hello `OnUnregistered` метод:</span><span class="sxs-lookup"><span data-stu-id="6ef47-151">Add hello following code toohello `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="6ef47-152">В hello `MainActivity` метод, добавьте следующие инструкции import hello:</span><span class="sxs-lookup"><span data-stu-id="6ef47-152">In hello `MainActivity` method, add hello following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="6ef47-153">Добавьте следующий код в конце hello hello hello `OnCreate` метод:</span><span class="sxs-lookup"><span data-stu-id="6ef47-153">Add hello following code at hello end of hello `OnCreate` method:</span></span>
   
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

## <a name="add-your-api-key-tooyour-app"></a><span data-ttu-id="6ef47-154">Добавить приложение tooyour ключа API</span><span class="sxs-lookup"><span data-stu-id="6ef47-154">Add your API key tooyour app</span></span>
1. <span data-ttu-id="6ef47-155">В Eclipse, создайте новый файл с именем **api_key.txt** в ресурсах hello каталог проекта.</span><span class="sxs-lookup"><span data-stu-id="6ef47-155">In Eclipse, create a new file named **api_key.txt** in hello directory assets of your project.</span></span>
2. <span data-ttu-id="6ef47-156">Привет открыть файл и скопируйте hello API ключ, который был создан в портале для разработчиков Amazon hello.</span><span class="sxs-lookup"><span data-stu-id="6ef47-156">Open hello file and copy hello API key that you generated in hello Amazon developer portal.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="6ef47-157">Выполните приложение hello</span><span class="sxs-lookup"><span data-stu-id="6ef47-157">Run hello app</span></span>
1. <span data-ttu-id="6ef47-158">Запустите эмулятор hello.</span><span class="sxs-lookup"><span data-stu-id="6ef47-158">Start hello emulator.</span></span>
2. <span data-ttu-id="6ef47-159">В эмуляторе hello проведите сверху hello и нажмите кнопку **параметры**, а затем нажмите кнопку **моей учетной записи** и зарегистрировать с помощью действительной учетной записи Amazon.</span><span class="sxs-lookup"><span data-stu-id="6ef47-159">In hello emulator, swipe from hello top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="6ef47-160">В Eclipse запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="6ef47-160">In Eclipse, run hello app.</span></span>

> [!NOTE]
> <span data-ttu-id="6ef47-161">Если возникнут проблемы, проверьте время hello эмулятор hello (или устройства).</span><span class="sxs-lookup"><span data-stu-id="6ef47-161">If a problem occurs, check hello time of hello emulator (or device).</span></span> <span data-ttu-id="6ef47-162">значение времени Hello должно быть точным.</span><span class="sxs-lookup"><span data-stu-id="6ef47-162">hello time value must be accurate.</span></span> <span data-ttu-id="6ef47-163">время hello toochange hello электронная версия эмулятора, можно запустить следующую команду из каталога средства платформы Android SDK hello:</span><span class="sxs-lookup"><span data-stu-id="6ef47-163">toochange hello time of hello Kindle emulator, you can run hello following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="6ef47-164">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="6ef47-164">Send a message</span></span>
<span data-ttu-id="6ef47-165">toosend сообщения с помощью .NET:</span><span class="sxs-lookup"><span data-stu-id="6ef47-165">toosend a message by using .NET:</span></span>

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
