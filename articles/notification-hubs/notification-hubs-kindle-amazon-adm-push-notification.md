---
title: "Приступая к работе с Центрами уведомлений Azure для приложений Kindle | Документация Майкрософт"
description: "Из этого учебника вы узнаете, как использовать Центры уведомлений Azure для отправки push-уведомлений в приложение Kindle."
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
ms.openlocfilehash: 7206f152ed7270abc62536a9ee164f7227833bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="a677c-103">Приступая к работе с Центрами уведомлений для приложений Kindle</span><span class="sxs-lookup"><span data-stu-id="a677c-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="a677c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a677c-104">Overview</span></span>
<span data-ttu-id="a677c-105">В этом учебнике показано, как использовать Центры уведомлений Azure для отправки push-уведомлений в приложение Kindle.</span><span class="sxs-lookup"><span data-stu-id="a677c-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Kindle application.</span></span>
<span data-ttu-id="a677c-106">Вы создаете пустое приложение Kindle, которое получает push-уведомления с помощью Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="a677c-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a677c-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a677c-107">Prerequisites</span></span>
<span data-ttu-id="a677c-108">Для работы с данным учебником требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="a677c-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="a677c-109">Скачайте пакет SDK Android (предполагается, что вы будете использовать Eclipse) с <a href="http://go.microsoft.com/fwlink/?LinkId=389797">сайта Android</a>.</span><span class="sxs-lookup"><span data-stu-id="a677c-109">Get the Android SDK (we assume that you will use Eclipse) from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="a677c-110">Следуйте указаниям, приведенным в статье <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Настройка среды разработки</a>, для настройки среды разработки для Kindle.</span><span class="sxs-lookup"><span data-stu-id="a677c-110">Follow the steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> to set up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-to-the-developer-portal"></a><span data-ttu-id="a677c-111">Добавление нового приложения на портал разработчика</span><span class="sxs-lookup"><span data-stu-id="a677c-111">Add a new app to the developer portal</span></span>
1. <span data-ttu-id="a677c-112">Для начала создайте приложение на [портале разработчика Amazon].</span><span class="sxs-lookup"><span data-stu-id="a677c-112">First, create an app in the [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="a677c-113">Скопируйте **ключ приложения**.</span><span class="sxs-lookup"><span data-stu-id="a677c-113">Copy the **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="a677c-114">На портале щелкните название вашего приложения, затем перейдите на вкладку **Device Messaging** .</span><span class="sxs-lookup"><span data-stu-id="a677c-114">In the portal, click the name of your app, and then click the **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="a677c-115">Щелкните **Создать новый профиль безопасности**, затем создайте профиль безопасности (например, **Профиль безопасности TestAdm**).</span><span class="sxs-lookup"><span data-stu-id="a677c-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="a677c-116">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a677c-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="a677c-117">Щелкните **Профили безопасности** для просмотра только что созданного профиля.</span><span class="sxs-lookup"><span data-stu-id="a677c-117">Click **Security Profiles** to view the security profile that you just created.</span></span> <span data-ttu-id="a677c-118">Скопируйте значения **Код клиента** и **Секрет клиента** для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="a677c-118">Copy the **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="a677c-119">Создание ключа API</span><span class="sxs-lookup"><span data-stu-id="a677c-119">Create an API key</span></span>
1. <span data-ttu-id="a677c-120">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a677c-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="a677c-121">Перейдите в папку пакета Android SDK.</span><span class="sxs-lookup"><span data-stu-id="a677c-121">Navigate to the Android SDK folder.</span></span>
3. <span data-ttu-id="a677c-122">Введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a677c-122">Enter the following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="a677c-123">Для пароля **keystore** введите **android**.</span><span class="sxs-lookup"><span data-stu-id="a677c-123">For the **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="a677c-124">Скопируйте отпечаток **MD5** .</span><span class="sxs-lookup"><span data-stu-id="a677c-124">Copy the **MD5** fingerprint.</span></span>
6. <span data-ttu-id="a677c-125">Вернувшись на портал разработчика, на вкладке **Обмен сообщениями** щелкните **Android/Kindle**, введите имя пакета для вашего приложения (например, **com.sample.notificationhubtest**) и значение **MD5**, а затем щелкните **Создать ключ API**.</span><span class="sxs-lookup"><span data-stu-id="a677c-125">Back in the developer portal, on the **Messaging** tab, click **Android/Kindle** and enter the name of the package for your app (for example, **com.sample.notificationhubtest**) and the **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-to-the-hub"></a><span data-ttu-id="a677c-126">Добавление учетных данных для центра</span><span class="sxs-lookup"><span data-stu-id="a677c-126">Add credentials to the hub</span></span>
<span data-ttu-id="a677c-127">На портале добавьте секрет клиента и код клиента на вкладку **Настройка** центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a677c-127">In the portal, add the client secret and client ID to the **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="a677c-128">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="a677c-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="a677c-129">При создании приложения используйте API уровня не ниже 17.</span><span class="sxs-lookup"><span data-stu-id="a677c-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="a677c-130">Добавьте библиотеки ADM в проект Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a677c-130">Add the ADM libraries to your Eclipse project:</span></span>

1. <span data-ttu-id="a677c-131">Чтобы получить библиотеку ADM, [загрузите пакет SDK].</span><span class="sxs-lookup"><span data-stu-id="a677c-131">To obtain the ADM library, [download the SDK].</span></span> <span data-ttu-id="a677c-132">Распакуйте ZIP-файл пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="a677c-132">Extract the SDK zip file.</span></span>
2. <span data-ttu-id="a677c-133">В Eclipse щелкните правой кнопкой мыши по проекту и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="a677c-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="a677c-134">Выберите **путь построения Java** в левой части экрана и выберите ** библиотеки ** вверху вкладку.</span><span class="sxs-lookup"><span data-stu-id="a677c-134">Select **Java Build Path** on the left, and then select the **Libraries **tab at the top.</span></span> <span data-ttu-id="a677c-135">Щелкните **Add External Jar** (Добавить внешний JAR-файл) и выберите файл `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` из каталога, в который вы распаковали пакет SDK Amazon.</span><span class="sxs-lookup"><span data-stu-id="a677c-135">Click **Add External Jar**, and select the file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from the directory in which you extracted the Amazon SDK.</span></span>
3. <span data-ttu-id="a677c-136">Загрузите пакет NotificationHubs Android SDK (ссылка).</span><span class="sxs-lookup"><span data-stu-id="a677c-136">Download the NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="a677c-137">Извлеките содержимое пакета, а затем перетащите файл `notification-hubs-sdk.jar` в папку `libs` в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a677c-137">Unzip the package, and then drag the file `notification-hubs-sdk.jar` into the `libs` folder in Eclipse.</span></span>

<span data-ttu-id="a677c-138">Изменение манифеста приложения для поддержки ADM</span><span class="sxs-lookup"><span data-stu-id="a677c-138">Edit your app manifest to support ADM:</span></span>

1. <span data-ttu-id="a677c-139">Добавьте пространство имен Amazon в корневом элементе манифеста.</span><span class="sxs-lookup"><span data-stu-id="a677c-139">Add the Amazon namespace in the root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="a677c-140">Добавьте разрешения в качестве первого элемента в элементе манифеста.</span><span class="sxs-lookup"><span data-stu-id="a677c-140">Add permissions as the first element under the manifest element.</span></span> <span data-ttu-id="a677c-141">Вместо **[YOUR PACKAGE NAME]** укажите пакет, который вы используете для создания приложения.</span><span class="sxs-lookup"><span data-stu-id="a677c-141">Substitute **[YOUR PACKAGE NAME]** with the package that you used to create your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access to receive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK to keep the processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="a677c-142">Вставьте приведенный ниже элемент в качестве первого потомка элемента приложения.</span><span class="sxs-lookup"><span data-stu-id="a677c-142">Insert the following element as the first child of the application element.</span></span> <span data-ttu-id="a677c-143">Не забудьте заменить **[YOUR SERVICE NAME]** именем обработчика сообщений ADM, который будет создан в следующем разделе (включая пакет), а **[YOUR PACKAGE NAME]** именем пакета, с помощью которого создается приложение.</span><span class="sxs-lookup"><span data-stu-id="a677c-143">Remember to substitute **[YOUR SERVICE NAME]** with the name of your ADM message handler that you create in the next section (including the package), and replace **[YOUR PACKAGE NAME]** with the package name with which you created your app.</span></span>
   
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
   
            <!-- To interact with ADM, your app must listen for the following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace the name in the category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="a677c-144">Создание обработчика сообщений ADM</span><span class="sxs-lookup"><span data-stu-id="a677c-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="a677c-145">Создайте новый класс с наследованием от `com.amazon.device.messaging.ADMMessageHandlerBase` и назовите его `MyADMMessageHandler`, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="a677c-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in the following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="a677c-146">Добавьте следующие операторы `import` :</span><span class="sxs-lookup"><span data-stu-id="a677c-146">Add the following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="a677c-147">Добавьте в созданный класс приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="a677c-147">Add the following code in the class that you created.</span></span> <span data-ttu-id="a677c-148">Не забудьте подставить имя центра и строку подключения (listen).</span><span class="sxs-lookup"><span data-stu-id="a677c-148">Remember to substitute the hub name and connection string (listen):</span></span>
   
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
4. <span data-ttu-id="a677c-149">Добавьте в метод `OnMessage()` следующий код:</span><span class="sxs-lookup"><span data-stu-id="a677c-149">Add the following code to the `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="a677c-150">Добавьте в метод `OnRegistered` следующий код:</span><span class="sxs-lookup"><span data-stu-id="a677c-150">Add the following code to the `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="a677c-151">Добавьте в метод `OnUnregistered` следующий код:</span><span class="sxs-lookup"><span data-stu-id="a677c-151">Add the following code to the `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="a677c-152">Затем в методе `MainActivity` добавьте следующую инструкцию import:</span><span class="sxs-lookup"><span data-stu-id="a677c-152">In the `MainActivity` method, add the following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="a677c-153">В конец метода `OnCreate` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="a677c-153">Add the following code at the end of the `OnCreate` method:</span></span>
   
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

## <a name="add-your-api-key-to-your-app"></a><span data-ttu-id="a677c-154">Добавление ключа API в приложение</span><span class="sxs-lookup"><span data-stu-id="a677c-154">Add your API key to your app</span></span>
1. <span data-ttu-id="a677c-155">В Eclipse создайте новый файл с именем **api_key.txt** в активах каталога проекта.</span><span class="sxs-lookup"><span data-stu-id="a677c-155">In Eclipse, create a new file named **api_key.txt** in the directory assets of your project.</span></span>
2. <span data-ttu-id="a677c-156">Откройте файл и скопируйте ключ API, созданный на портале разработчика Amazon.</span><span class="sxs-lookup"><span data-stu-id="a677c-156">Open the file and copy the API key that you generated in the Amazon developer portal.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="a677c-157">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="a677c-157">Run the app</span></span>
1. <span data-ttu-id="a677c-158">Запустите эмулятор.</span><span class="sxs-lookup"><span data-stu-id="a677c-158">Start the emulator.</span></span>
2. <span data-ttu-id="a677c-159">В эмуляторе сверху щелкните **Параметры**, затем **Моя учетная запись** и зарегистрируйтесь с использованием действующей учетной записи Amazon.</span><span class="sxs-lookup"><span data-stu-id="a677c-159">In the emulator, swipe from the top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="a677c-160">В Eclipse запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="a677c-160">In Eclipse, run the app.</span></span>

> [!NOTE]
> <span data-ttu-id="a677c-161">Если возникает проблема, проверьте время эмулятора (или устройства).</span><span class="sxs-lookup"><span data-stu-id="a677c-161">If a problem occurs, check the time of the emulator (or device).</span></span> <span data-ttu-id="a677c-162">Значение времени должно быть точным.</span><span class="sxs-lookup"><span data-stu-id="a677c-162">The time value must be accurate.</span></span> <span data-ttu-id="a677c-163">Для изменения времени эмулятора Kindle выполните следующую команду из каталога средств для платформы Android SDK:</span><span class="sxs-lookup"><span data-stu-id="a677c-163">To change the time of the Kindle emulator, you can run the following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="a677c-164">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="a677c-164">Send a message</span></span>
<span data-ttu-id="a677c-165">Чтобы отправить сообщение с помощью .NET, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="a677c-165">To send a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
<span data-ttu-id="a677c-166">[портале разработчика Amazon]: https://developer.amazon.com/home.html</span><span class="sxs-lookup"><span data-stu-id="a677c-166">[Amazon developer portal]: https://developer.amazon.com/home.html</span></span>
<span data-ttu-id="a677c-167">[загрузите пакет SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span><span class="sxs-lookup"><span data-stu-id="a677c-167">[download the SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span></span>

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
