---
title: "tooAndroid уведомления aaaSending принудительной с концентраторами уведомлений Azure | Документы Microsoft"
description: "В этом учебнике вы узнаете, как toouse концентраторов уведомлений Azure toopush уведомления tooAndroid устройств."
services: notification-hubs
documentationcenter: android
keywords: "push-уведомления, push-уведомление, push-уведомление android"
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 6b15a477d86cf1e6efffb21c5bcef0de7761af79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="13651-104">Отправка push tooAndroid уведомлений с концентраторами уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="13651-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="13651-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="13651-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="13651-106">В этой статье описывается отправка push-уведомлений с помощью Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="13651-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="13651-107">Если вы используете Google обмена сообщениями облака Firebase (FCM), см. раздел [tooAndroid уведомления Принудительная отправка с концентраторами уведомлений Azure и FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="13651-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="13651-108">Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомления tooan Android приложения.</span><span class="sxs-lookup"><span data-stu-id="13651-108">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="13651-109">Вы создадите пустое приложение Android, которое получает push-уведомления с помощью Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="13651-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="13651-110">Hello завершения кода в этом учебнике можно загрузить с сайта GitHub [здесь](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="13651-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13651-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="13651-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="13651-112">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="13651-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="13651-113">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="13651-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="13651-114">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="13651-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="13651-115">Кроме учетной записи Azure active tooan упоминалось выше, этого учебника требуется только hello последнюю версию [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="13651-115">In addition tooan active Azure account mentioned above, this tutorial only requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="13651-116">Завершение изучения этого учебника является необходимым условием для работы со всеми другими учебниками, посвященными Центрам уведомлений для приложений Android.</span><span class="sxs-lookup"><span data-stu-id="13651-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="13651-117">Создание проекта с поддержкой Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="13651-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="13651-118">Настройка нового центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="13651-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="13651-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="13651-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="13651-120">В hello **параметры** колонке выберите **служб Notification Services** и затем **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="13651-120">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="13651-121">Введите ключ hello API и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="13651-121">Enter hello API key and click **Save**.</span></span>

&emsp;&emsp;![Центры уведомлений Azure — Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="13651-123">Концентратор уведомлений теперь настроенный toowork с GCM и у вас есть tooboth строки подключения hello регистрации вашего приложения tooreceive и отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="13651-123">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="13651-124"><a id="connecting-app"></a>Подключение приложения toohello концентратор уведомлений</span><span class="sxs-lookup"><span data-stu-id="13651-124"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="13651-125">Создание нового проекта Android</span><span class="sxs-lookup"><span data-stu-id="13651-125">Create a new Android project</span></span>
1. <span data-ttu-id="13651-126">В Android Studio создайте новый проект Android Studio.</span><span class="sxs-lookup"><span data-stu-id="13651-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio — новый проект][13]
2. <span data-ttu-id="13651-128">Выберите hello **телефонов и планшетных ПК** форме коэффициент и hello **SDK минимум** нужных toosupport.</span><span class="sxs-lookup"><span data-stu-id="13651-128">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="13651-129">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="13651-129">Then click **Next**.</span></span>
   
   ![Android Studio — рабочий процесс создания проекта][14]
3. <span data-ttu-id="13651-131">Выберите **пустое действие** hello основных действий, щелкните **Далее**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="13651-131">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="13651-132">Добавление проекта toohello служб Google Play</span><span class="sxs-lookup"><span data-stu-id="13651-132">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="13651-133">Добавление библиотек Центров уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="13651-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="13651-134">В hello `Build.Gradle` файл для hello **приложения**, добавить следующие строки в hello hello **зависимости** раздела.</span><span class="sxs-lookup"><span data-stu-id="13651-134">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="13651-135">Добавьте следующий репозиторий после hello hello **зависимости** раздела.</span><span class="sxs-lookup"><span data-stu-id="13651-135">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="13651-136">Обновление hello AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="13651-136">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="13651-137">toosupport GCM, мы должны реализовать службу прослушивателя идентификатор экземпляра в наш код, который используется слишком[получать маркеры регистрации](https://developers.google.com/cloud-messaging/android/client#sample-register) с помощью [API идентификатор экземпляра Google](https://developers.google.com/instance-id/).</span><span class="sxs-lookup"><span data-stu-id="13651-137">toosupport GCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="13651-138">В этом учебнике мы назвать класс hello `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="13651-138">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="13651-139">Добавьте следующий файл определения службы toohello AndroidManifest.xml, внутри hello hello `<application>` тег.</span><span class="sxs-lookup"><span data-stu-id="13651-139">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="13651-140">Замените hello `<your package>` заполнитель hello ваше имя самого пакета отображается вверху hello hello `AndroidManifest.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="13651-140">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="13651-141">После наших маркер регистрации GCM сотрудничают с hello API идентификатор экземпляра, мы будем использовать слишком[зарегистрироваться hello концентратор уведомлений Azure](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="13651-141">Once we have received our GCM registration token from hello Instance ID API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="13651-142">Поддерживаются регистрация с помощью фоновой hello `IntentService` с именем `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="13651-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="13651-143">Кроме того, эта служба будет отвечать за [обновление маркера регистрации в GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span><span class="sxs-lookup"><span data-stu-id="13651-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="13651-144">Добавьте следующий файл определения службы toohello AndroidManifest.xml, внутри hello hello `<application>` тег.</span><span class="sxs-lookup"><span data-stu-id="13651-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="13651-145">Замените hello `<your package>` заполнитель hello ваше имя самого пакета отображается вверху hello hello `AndroidManifest.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="13651-145">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="13651-146">Также мы определим tooreceive получателя уведомлений.</span><span class="sxs-lookup"><span data-stu-id="13651-146">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="13651-147">Добавьте следующие определения toohello AndroidManifest.xml файл приемника, внутри hello hello `<application>` тег.</span><span class="sxs-lookup"><span data-stu-id="13651-147">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="13651-148">Замените hello `<your package>` заполнитель hello ваше имя самого пакета отображается вверху hello hello `AndroidManifest.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="13651-148">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="13651-149">Добавьте следующие необходимые GCM hello, связанные с разрешениями ниже hello `</application>` тег.</span><span class="sxs-lookup"><span data-stu-id="13651-149">Add hello following necessary GCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="13651-150">Убедитесь, что tooreplace `<your package>` с именем пакета hello показано вверху hello hello `AndroidManifest.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="13651-150">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="13651-151">Дополнительные сведения об этих разрешениях см. в статье [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) (Настройка клиентского приложения GCM для Android).</span><span class="sxs-lookup"><span data-stu-id="13651-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="13651-152">Добавление кода</span><span class="sxs-lookup"><span data-stu-id="13651-152">Adding code</span></span>
1. <span data-ttu-id="13651-153">В hello представления проекта, разверните **приложения** > **src** > **основной** > **java**.</span><span class="sxs-lookup"><span data-stu-id="13651-153">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="13651-154">Щелкните правой кнопкой мыши папку пакета в **java**, щелкните **New** (Создать) и выберите **Java Class** (Класс Java).</span><span class="sxs-lookup"><span data-stu-id="13651-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="13651-155">Добавьте новый класс с именем `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="13651-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio — новый класс Java][6]
   
    <span data-ttu-id="13651-157">Убедитесь, что эти три заполнители в следующий код для hello hello hello tooupdate `NotificationSettings` класса:</span><span class="sxs-lookup"><span data-stu-id="13651-157">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="13651-158">**Идентификатор отправителя**: hello номер проекта, полученные ранее в hello [облачной консоли Google](http://cloud.google.com/console).</span><span class="sxs-lookup"><span data-stu-id="13651-158">**SenderId**: hello project number you obtained earlier in hello [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="13651-159">**HubListenConnectionString**: hello **DefaultListenAccessSignature** строку подключения для концентратор.</span><span class="sxs-lookup"><span data-stu-id="13651-159">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="13651-160">Можно скопировать этой строки подключения, нажав кнопку **политики доступа** на hello **параметры** колонке концентратора, на hello [портала Azure].</span><span class="sxs-lookup"><span data-stu-id="13651-160">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="13651-161">**HubName**: используйте имя hello центра уведомлений, появится в колонке концентратора hello в hello [портала Azure].</span><span class="sxs-lookup"><span data-stu-id="13651-161">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="13651-162">`NotificationSettings` :</span><span class="sxs-lookup"><span data-stu-id="13651-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="13651-163">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="13651-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="13651-164">}</span><span class="sxs-lookup"><span data-stu-id="13651-164">}</span></span>
2. <span data-ttu-id="13651-165">Используя описанные выше действия hello, добавьте новый класс с именем `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="13651-165">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="13651-166">Таким образом мы выполним реализацию службы прослушивания идентификаторов экземпляра.</span><span class="sxs-lookup"><span data-stu-id="13651-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="13651-167">Hello код для этого класса будут вызывать нашей `IntentService` слишком[GCM токен обновления hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="13651-167">hello code for this class will call our `IntentService` too[refresh hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="13651-168">Добавьте еще один новый класс tooyour проект с именем `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="13651-168">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="13651-169">Это будет hello реализацию для наших `IntentService` , обрабатывающий [обновление токен GCM hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) и [регистрации с концентратором уведомлений hello](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="13651-169">This will be hello implementation for our `IntentService` that will handle [refreshing hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="13651-170">Используйте следующий код для этого класса hello.</span><span class="sxs-lookup"><span data-stu-id="13651-170">Use hello following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
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
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting tooregister with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete token refresh", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="13651-171">В вашей `MainActivity` класса, добавьте следующее hello `import` приведенные выше hello инструкции объявления класса.</span><span class="sxs-lookup"><span data-stu-id="13651-171">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="13651-172">Добавьте следующие закрытые члены вверху hello класс hello hello.</span><span class="sxs-lookup"><span data-stu-id="13651-172">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="13651-173">Мы будем использовать эти [Проверьте доступность службы Google Play hello согласно рекомендациям Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="13651-173">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="13651-174">В вашей `MainActivity` добавьте следующий метод toohello доступность службы Google Play hello.</span><span class="sxs-lookup"><span data-stu-id="13651-174">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
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
5. <span data-ttu-id="13651-175">В вашей `MainActivity` добавьте следующий код, который будет искать службы Google Play перед вызовом hello вашей `IntentService` tooget ваш токен регистрации GCM и регистрации в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="13651-175">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="13651-176">В hello `OnCreate` метод hello `MainActivity` добавьте hello следующий процесс регистрации hello toostart кода при создании действия.</span><span class="sxs-lookup"><span data-stu-id="13651-176">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="13651-177">Добавить эти дополнительные методы toohello `MainActivity` tooverify состояния и отчетов состояния приложения в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="13651-177">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="13651-178">Hello `ToastNotify` метод использует hello *«Hello World»* `TextView` управления tooreport состояние и оповещения, сохраняемым в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="13651-178">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="13651-179">В макете activity_main.xml добавьте hello, код подписки для этого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="13651-179">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="13651-180">Далее мы добавим подкласс для наших приемника, определенный в hello AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="13651-180">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="13651-181">Добавьте еще один новый класс tooyour проект с именем `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="13651-181">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="13651-182">Добавьте следующие инструкции импорта вверху hello hello `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="13651-182">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="13651-183">Добавьте следующий код для hello hello `MyHandler` класс, сделав его подкласс `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="13651-183">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="13651-184">Этот код переопределяет hello `OnReceive` метод, поэтому обработчик hello сообщит уведомлений, полученных.</span><span class="sxs-lookup"><span data-stu-id="13651-184">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="13651-185">Обработчик Hello также отправляет диспетчер hello принудительной уведомлений toohello Android уведомление с помощью hello `sendNotification()` метод.</span><span class="sxs-lookup"><span data-stu-id="13651-185">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="13651-186">Hello `sendNotification()` следует выполнить метод, если приложение hello не выполняется и получает уведомление.</span><span class="sxs-lookup"><span data-stu-id="13651-186">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="13651-187">В Android Studio hello меню щелкните **построения** > **перестроить проект** toomake убедиться, что, присутствуют в коде нет ошибок.</span><span class="sxs-lookup"><span data-stu-id="13651-187">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="13651-188">Отправка push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="13651-188">Sending push notifications</span></span>
<span data-ttu-id="13651-189">Вы можете протестировать получения push-уведомлений в приложение, отправляя их через hello [портала Azure] -искать hello **Устранение неполадок** статьи в колонке концентратора hello, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="13651-189">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Центры уведомлений Azure — тестовая отправка](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="13651-191">(Необязательно) Отправлять push-уведомления прямо из приложения hello</span><span class="sxs-lookup"><span data-stu-id="13651-191">(Optional) Send push notifications directly from hello app</span></span>
<span data-ttu-id="13651-192">Обычно уведомления отправляются с сервера базы данных.</span><span class="sxs-lookup"><span data-stu-id="13651-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="13651-193">В некоторых случаях может потребоваться toobe push-уведомлений может toosend непосредственно из клиентского приложения hello.</span><span class="sxs-lookup"><span data-stu-id="13651-193">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="13651-194">В этом разделе описывается, как toosend уведомления с помощью клиента hello hello [API REST для концентратора уведомлений Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="13651-194">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="13651-195">В представлении проекта Android Studio разверните узел **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="13651-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="13651-196">Откройте hello `activity_main.xml` макета и выберите пункт hello **текст** вкладке tooupdate hello текстовое содержимое файла hello.</span><span class="sxs-lookup"><span data-stu-id="13651-196">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="13651-197">Обновите его с hello кода, который добавляет новые `Button` и `EditText` элементы управления для отправки push-концентратор уведомлений toohello сообщения уведомления.</span><span class="sxs-lookup"><span data-stu-id="13651-197">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="13651-198">Добавьте следующий код в нижней hello непосредственно перед `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="13651-198">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="13651-199">В представлении проекта Android Studio разверните узел **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="13651-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="13651-200">Откройте hello `strings.xml` и добавьте hello строковых значений, на которые ссылается hello нового файла `Button` и `EditText` элементов управления.</span><span class="sxs-lookup"><span data-stu-id="13651-200">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="13651-201">Добавьте следующие hello нижней части файла hello непосредственно перед `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="13651-201">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="13651-202">В вашей `NotificationSetting.java` файл, добавьте следующий параметр toohello hello `NotificationSettings` класса.</span><span class="sxs-lookup"><span data-stu-id="13651-202">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="13651-203">Обновление `HubFullAccess` с hello **DefaultFullSharedAccessSignature** строку подключения для концентратор.</span><span class="sxs-lookup"><span data-stu-id="13651-203">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="13651-204">В этой строке подключения можно скопировать из hello [портала Azure] , щелкнув **политики доступа** на hello **параметры** колонке концентратор уведомлений.</span><span class="sxs-lookup"><span data-stu-id="13651-204">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="13651-205">В вашей `MainActivity.java` файл, добавьте следующее hello `import` инструкции выше hello `MainActivity` класса.</span><span class="sxs-lookup"><span data-stu-id="13651-205">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="13651-206">В вашей `MainActivity.java` файл, добавить следующие члены вверху hello hello hello `MainActivity` класса.</span><span class="sxs-lookup"><span data-stu-id="13651-206">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="13651-207">Необходимо создать tooauthenticate токена программного обеспечения URL-адреса (SaS) концентратора уведомлений tooyour POST запроса toosend сообщений.</span><span class="sxs-lookup"><span data-stu-id="13651-207">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="13651-208">Это делается путем синтаксического анализа hello данные ключа из строки подключения hello и последующего создания hello маркер SaS, как упоминалось в hello [основные понятия](http://msdn.microsoft.com/library/azure/dn495627.aspx) Справочник по REST API.</span><span class="sxs-lookup"><span data-stu-id="13651-208">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="13651-209">Привет, следующий код представляет собой пример реализацию.</span><span class="sxs-lookup"><span data-stu-id="13651-209">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="13651-210">В `MainActivity.java`, добавьте следующий метод toohello hello `MainActivity` класса tooparse строки подключения.</span><span class="sxs-lookup"><span data-stu-id="13651-210">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
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
7. <span data-ttu-id="13651-211">В `MainActivity.java`, добавьте следующий метод toohello hello `MainActivity` класса toocreate маркер проверки подлинности SaS.</span><span class="sxs-lookup"><span data-stu-id="13651-211">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
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
8. <span data-ttu-id="13651-212">В `MainActivity.java`, добавьте следующий метод toohello hello `MainActivity` hello класс toohandle **отправить уведомление** нажмите кнопку и отправить push-уведомление hello концентратора toohello сообщения с помощью hello встроенных API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="13651-212">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
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

## <a name="testing-your-app"></a><span data-ttu-id="13651-213">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="13651-213">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="13651-214">Push-уведомлений в эмуляторе hello</span><span class="sxs-lookup"><span data-stu-id="13651-214">Push notifications in hello emulator</span></span>
<span data-ttu-id="13651-215">Следует tootest push-уведомлений в эмуляторе убедитесь, что образ эмулятора поддерживает уровень Google API hello, выбранное для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="13651-215">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="13651-216">Если изображение не поддерживает собственные интерфейсы API Google, вы получите hello **службы\_не\_ДОСТУПНО** исключение.</span><span class="sxs-lookup"><span data-stu-id="13651-216">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="13651-217">Кроме toohello выше, убедитесь, что вы добавили запуска эмулятора под учетной записью tooyour вашей Google система **параметры** > **учетные записи**.</span><span class="sxs-lookup"><span data-stu-id="13651-217">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="13651-218">В противном случае ваш tooregister попыток с GCM может привести к hello **проверки ПОДЛИННОСТИ\_сбой** исключение.</span><span class="sxs-lookup"><span data-stu-id="13651-218">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="13651-219">Запуск приложения hello</span><span class="sxs-lookup"><span data-stu-id="13651-219">Running hello application</span></span>
1. <span data-ttu-id="13651-220">Выполните приложение hello и обратите внимание, что идентификатор hello регистрации указывается для успешной регистрации.</span><span class="sxs-lookup"><span data-stu-id="13651-220">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
      ![Тестирование на устройстве Android — регистрация канала][18]
2. <span data-ttu-id="13651-222">Введите toobe сообщение уведомления, отправленные tooall устройств Android, которые зарегистрированы с концентратором hello.</span><span class="sxs-lookup"><span data-stu-id="13651-222">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
      ![Тестирование на устройстве Android — отправка сообщения][19]

3. <span data-ttu-id="13651-224">Нажмите кнопку **Send Notification**(Отправить уведомление).</span><span class="sxs-lookup"><span data-stu-id="13651-224">Press **Send Notification**.</span></span> <span data-ttu-id="13651-225">Будут показаны все устройства, работающие приложения hello `AlertDialog` экземпляр с hello push-сообщение уведомления.</span><span class="sxs-lookup"><span data-stu-id="13651-225">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="13651-226">Устройства, нет hello приложение работает, но ранее зарегистрированные push-уведомлений получит уведомление hello диспетчера уведомлений Android.</span><span class="sxs-lookup"><span data-stu-id="13651-226">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="13651-227">Их можно просмотреть путем считывания вниз от верхнего левого угла hello.</span><span class="sxs-lookup"><span data-stu-id="13651-227">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
      ![Тестирование на устройстве Android — уведомления][21]

## <a name="next-steps"></a><span data-ttu-id="13651-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="13651-229">Next steps</span></span>
<span data-ttu-id="13651-230">Мы рекомендуем hello [toousers уведомления toopush использования концентраторов уведомлений] учебника в качестве следующего шага hello.</span><span class="sxs-lookup"><span data-stu-id="13651-230">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="13651-231">Также будет показано, как уведомления о toosend из серверной части ASP.NET с помощью тегов tootarget конкретных пользователей.</span><span class="sxs-lookup"><span data-stu-id="13651-231">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="13651-232">Если требуется toosegment пользователи, группы интересов извлечь hello [toosend использования концентраторов уведомлений, новости] учебника.</span><span class="sxs-lookup"><span data-stu-id="13651-232">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="13651-233">toolearn Дополнительные общие сведения о концентраторах уведомлений см. наш [руководство концентраторы уведомлений].</span><span class="sxs-lookup"><span data-stu-id="13651-233">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[руководство концентраторы уведомлений]: http://msdn.microsoft.com/library/jj927170.aspx
[toousers уведомления toopush использования концентраторов уведомлений]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[toosend использования концентраторов уведомлений, новости]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[портала Azure]: https://portal.azure.com
