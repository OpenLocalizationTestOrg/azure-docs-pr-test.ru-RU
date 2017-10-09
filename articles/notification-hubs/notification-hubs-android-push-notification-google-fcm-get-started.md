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
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="82ade-104">Отправка push tooAndroid уведомлений с концентраторами уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="82ade-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="82ade-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="82ade-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="82ade-106">В этой статье описывается отправка push-уведомлений с помощью Google Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="82ade-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="82ade-107">Если вы все еще используете Google Cloud Messaging (GCM), см. раздел [tooAndroid уведомления Принудительная отправка с концентраторами уведомлений Azure и GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="82ade-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="82ade-108">Этот учебник показывает, как toouse концентраторов уведомлений Azure и toosend Firebase Cloud Messaging push-уведомления tooan Android приложения.</span><span class="sxs-lookup"><span data-stu-id="82ade-108">This tutorial shows you how toouse Azure Notification Hubs and Firebase Cloud Messaging toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="82ade-109">Вы создадите пустое приложение Android, которое получает push-уведомления с помощью Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="82ade-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="82ade-110">Hello завершения кода в этом учебнике можно загрузить с сайта GitHub [здесь](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span><span class="sxs-lookup"><span data-stu-id="82ade-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82ade-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="82ade-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="82ade-112">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="82ade-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="82ade-113">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="82ade-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="82ade-114">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="82ade-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

* <span data-ttu-id="82ade-115">Кроме учетной записи Azure active tooan упоминалось выше, упражнений этого учебника требуется hello последнюю версию [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="82ade-115">In addition tooan active Azure account mentioned above, this tutorial requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="82ade-116">Android версии 2.3 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="82ade-116">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="82ade-117">Репозиторий Google версии 27 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="82ade-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="82ade-118">Службы Google Play версии 9.0.2 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="82ade-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="82ade-119">Завершение изучения этого учебника является необходимым условием для работы со всеми другими учебниками, посвященными Центрам уведомлений для приложений Android.</span><span class="sxs-lookup"><span data-stu-id="82ade-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-a-new-android-studio-project"></a><span data-ttu-id="82ade-120">Создание проекта Android Studio</span><span class="sxs-lookup"><span data-stu-id="82ade-120">Create a new Android Studio Project</span></span>
1. <span data-ttu-id="82ade-121">В Android Studio создайте новый проект Android Studio.</span><span class="sxs-lookup"><span data-stu-id="82ade-121">In Android Studio, start a new Android Studio project.</span></span>
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="82ade-122">Выберите hello **телефонов и планшетных ПК** форме коэффициент и hello **SDK минимум** нужных toosupport.</span><span class="sxs-lookup"><span data-stu-id="82ade-122">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="82ade-123">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="82ade-123">Then click **Next**.</span></span>
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="82ade-124">Выберите **пустое действие** hello основных действий, щелкните **Далее**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="82ade-124">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="82ade-125">Создание проекта с поддержкой Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="82ade-125">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="82ade-126">Настройка нового центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="82ade-126">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="82ade-127">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="82ade-127">&emsp;&emsp;6.</span></span> <span data-ttu-id="82ade-128">В hello **параметры** колонке центра уведомлений, выберите **служб Notification Services** и затем **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="82ade-128">In hello **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="82ade-129">Введите ключ сервера FCM hello, скопированное ранее из hello [консоли Firebase](https://firebase.google.com/console/) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="82ade-129">Enter hello FCM server key you copied earlier from hello [Firebase console](https://firebase.google.com/console/) and click **Save**.</span></span>

&emsp;&emsp;![Центры уведомлений Azure — Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="82ade-131">Концентратор уведомлений теперь настроенный toowork с Messagin Firebase облака и у вас есть tooboth строки подключения hello регистрации вашего приложения tooreceive и отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="82ade-131">Your notification hub is now configured toowork with Firebase Cloud Messagin, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="82ade-132"><a id="connecting-app"></a>Подключение приложения toohello концентратор уведомлений</span><span class="sxs-lookup"><span data-stu-id="82ade-132"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="82ade-133">Добавление проекта toohello служб Google Play</span><span class="sxs-lookup"><span data-stu-id="82ade-133">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="82ade-134">Добавление библиотек Центров уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="82ade-134">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="82ade-135">В hello `Build.Gradle` файл для hello **приложения**, добавить следующие строки в hello hello **зависимости** раздела.</span><span class="sxs-lookup"><span data-stu-id="82ade-135">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="82ade-136">Добавьте следующий репозиторий после hello hello **зависимости** раздела.</span><span class="sxs-lookup"><span data-stu-id="82ade-136">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="82ade-137">Обновление hello AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="82ade-137">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="82ade-138">toosupport FCM, мы должны реализовать службу прослушивателя идентификатор экземпляра в наш код, который используется слишком[получать маркеры регистрации](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) с помощью [Google FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span><span class="sxs-lookup"><span data-stu-id="82ade-138">toosupport FCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="82ade-139">В этом учебнике мы назвать класс hello `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="82ade-139">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="82ade-140">Добавьте следующий файл определения службы toohello AndroidManifest.xml, внутри hello hello `<application>` тег.</span><span class="sxs-lookup"><span data-stu-id="82ade-140">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="82ade-141">После наших маркер регистрации FCM сотрудничают с hello FirebaseInstanceId API, мы будем использовать слишком[зарегистрироваться hello концентратор уведомлений Azure](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="82ade-141">Once we have received our FCM registration token from hello FirebaseInstanceId API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="82ade-142">Поддерживаются регистрация с помощью фоновой hello `IntentService` с именем `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="82ade-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="82ade-143">Кроме того, эта служба будет отвечать за обновление маркера регистрации в FCM.</span><span class="sxs-lookup"><span data-stu-id="82ade-143">This service will also be responsible for refreshing our FCM registration token.</span></span>
   
    <span data-ttu-id="82ade-144">Добавьте следующий файл определения службы toohello AndroidManifest.xml, внутри hello hello `<application>` тег.</span><span class="sxs-lookup"><span data-stu-id="82ade-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="82ade-145">Также мы определим tooreceive получателя уведомлений.</span><span class="sxs-lookup"><span data-stu-id="82ade-145">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="82ade-146">Добавьте следующие определения toohello AndroidManifest.xml файл приемника, внутри hello hello `<application>` тег.</span><span class="sxs-lookup"><span data-stu-id="82ade-146">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="82ade-147">Замените hello `<your package>` заполнитель hello ваше имя самого пакета отображается вверху hello hello `AndroidManifest.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="82ade-147">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="82ade-148">Добавьте следующие необходимые FCM hello, связанные с разрешениями ниже hello `</application>` тег.</span><span class="sxs-lookup"><span data-stu-id="82ade-148">Add hello following necessary FCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="82ade-149">Убедитесь, что tooreplace `<your package>` с именем пакета hello показано вверху hello hello `AndroidManifest.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="82ade-149">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="82ade-150">Дополнительные сведения об этих разрешений см. в разделе [установки GCM клиентского приложения для Android](https://developers.google.com/cloud-messaging/android/client#manifest) и [перенести GCM клиентского приложения для Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span><span class="sxs-lookup"><span data-stu-id="82ade-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a><span data-ttu-id="82ade-151">Добавление кода</span><span class="sxs-lookup"><span data-stu-id="82ade-151">Adding code</span></span>
1. <span data-ttu-id="82ade-152">В hello представления проекта, разверните **приложения** > **src** > **основной** > **java**.</span><span class="sxs-lookup"><span data-stu-id="82ade-152">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="82ade-153">Щелкните правой кнопкой мыши папку пакета в **java**, щелкните **New** (Создать) и выберите **Java Class** (Класс Java).</span><span class="sxs-lookup"><span data-stu-id="82ade-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="82ade-154">Добавьте новый класс с именем `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="82ade-154">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio — новый класс Java](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="82ade-156">Убедитесь, что эти три заполнители в следующий код для hello hello hello tooupdate `NotificationSettings` класса:</span><span class="sxs-lookup"><span data-stu-id="82ade-156">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="82ade-157">**Идентификатор отправителя**: hello идентификатор отправителя, полученные ранее в hello **Cloud Messaging** параметров проекта в hello [Firebase консоли](https://firebase.google.com/console/).</span><span class="sxs-lookup"><span data-stu-id="82ade-157">**SenderId**: hello Sender Id you obtained earlier in hello **Cloud Messaging** tab of your project settings in hello [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="82ade-158">**HubListenConnectionString**: hello **DefaultListenAccessSignature** строку подключения для концентратор.</span><span class="sxs-lookup"><span data-stu-id="82ade-158">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="82ade-159">Можно скопировать этой строки подключения, нажав кнопку **политики доступа** на hello **параметры** колонке концентратора, на hello [портала Azure].</span><span class="sxs-lookup"><span data-stu-id="82ade-159">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="82ade-160">**HubName**: используйте имя hello центра уведомлений, появится в колонке концентратора hello в hello [портала Azure].</span><span class="sxs-lookup"><span data-stu-id="82ade-160">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="82ade-161">`NotificationSettings` :</span><span class="sxs-lookup"><span data-stu-id="82ade-161">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="82ade-162">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="82ade-162">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       <span data-ttu-id="82ade-163">}</span><span class="sxs-lookup"><span data-stu-id="82ade-163">}</span></span>
2. <span data-ttu-id="82ade-164">Используя описанные выше действия hello, добавьте новый класс с именем `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="82ade-164">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="82ade-165">Таким образом мы выполним реализацию службы прослушивания идентификаторов экземпляра.</span><span class="sxs-lookup"><span data-stu-id="82ade-165">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="82ade-166">Hello код для этого класса будут вызывать нашей `IntentService` слишком[FCM токен обновления hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="82ade-166">hello code for this class will call our `IntentService` too[refresh hello FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
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


1. <span data-ttu-id="82ade-167">Добавьте еще один новый класс tooyour проект с именем `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="82ade-167">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="82ade-168">Это будет hello реализацию для наших `IntentService` , обрабатывающий [обновление токен hello FCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) и [регистрации с концентратором уведомлений hello](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="82ade-168">This will be hello implementation for our `IntentService` that will handle [refreshing hello FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="82ade-169">Используйте следующий код для этого класса hello.</span><span class="sxs-lookup"><span data-stu-id="82ade-169">Use hello following code for this class.</span></span>
   
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
2. <span data-ttu-id="82ade-170">В вашей `MainActivity` класса, добавьте следующее hello `import` приведенные выше hello инструкции объявления класса.</span><span class="sxs-lookup"><span data-stu-id="82ade-170">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="82ade-171">Добавьте следующие закрытые члены вверху hello класс hello hello.</span><span class="sxs-lookup"><span data-stu-id="82ade-171">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="82ade-172">Мы будем использовать эти [Проверьте доступность службы Google Play hello согласно рекомендациям Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="82ade-172">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="82ade-173">В вашей `MainActivity` добавьте следующий метод toohello доступность службы Google Play hello.</span><span class="sxs-lookup"><span data-stu-id="82ade-173">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
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
5. <span data-ttu-id="82ade-174">В вашей `MainActivity` добавьте следующий код, который будет искать службы Google Play перед вызовом hello вашей `IntentService` tooget ваш токен FCM регистрации и регистрации в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="82ade-174">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your FCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="82ade-175">В hello `OnCreate` метод hello `MainActivity` добавьте hello следующий процесс регистрации hello toostart кода при создании действия.</span><span class="sxs-lookup"><span data-stu-id="82ade-175">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="82ade-176">Добавить эти дополнительные методы toohello `MainActivity` tooverify состояния и отчетов состояния приложения в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="82ade-176">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="82ade-177">Hello `ToastNotify` метод использует hello *«Hello World»* `TextView` управления tooreport состояние и оповещения, сохраняемым в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="82ade-177">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="82ade-178">В макете activity_main.xml добавьте hello, код подписки для этого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="82ade-178">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="82ade-179">Далее мы добавим подкласс для наших приемника, определенный в hello AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="82ade-179">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="82ade-180">Добавьте еще один новый класс tooyour проект с именем `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="82ade-180">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="82ade-181">Добавьте следующие инструкции импорта вверху hello hello `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="82ade-181">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="82ade-182">Добавьте следующий код для hello hello `MyHandler` класс, сделав его подкласс `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="82ade-182">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="82ade-183">Этот код переопределяет hello `OnReceive` метод, поэтому обработчик hello сообщит уведомлений, полученных.</span><span class="sxs-lookup"><span data-stu-id="82ade-183">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="82ade-184">Обработчик Hello также отправляет диспетчер hello принудительной уведомлений toohello Android уведомление с помощью hello `sendNotification()` метод.</span><span class="sxs-lookup"><span data-stu-id="82ade-184">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="82ade-185">Hello `sendNotification()` следует выполнить метод, если приложение hello не выполняется и получает уведомление.</span><span class="sxs-lookup"><span data-stu-id="82ade-185">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="82ade-186">В Android Studio hello меню щелкните **построения** > **перестроить проект** toomake убедиться, что, присутствуют в коде нет ошибок.</span><span class="sxs-lookup"><span data-stu-id="82ade-186">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="82ade-187">Запустите приложение hello на устройстве и убедитесь, что он успешно регистрируется с концентратором уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="82ade-187">Run hello app on your device and verify it registers successfully with hello notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="82ade-188">Регистрация может завершиться ошибкой при изначальном hello до hello `onTokenRefresh()` вызывается метод экземпляра идентификатора службы.</span><span class="sxs-lookup"><span data-stu-id="82ade-188">Registration may fail on hello initial launch until hello `onTokenRefresh()` method of instance Id service is called.</span></span> <span data-ttu-id="82ade-189">Обновление Hello следует пакетам успешной регистрации с концентратором уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="82ade-189">hello refresh should intiate a successful registration with hello notification hub.</span></span>
    > 
    > 

## <a name="sending-push-notifications"></a><span data-ttu-id="82ade-190">Отправка push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="82ade-190">Sending push notifications</span></span>
<span data-ttu-id="82ade-191">Вы можете протестировать получения push-уведомлений в приложение, отправляя их через hello [портала Azure] -искать hello **Устранение неполадок** статьи в колонке концентратора hello, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="82ade-191">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Центры уведомлений Azure — тестовая отправка](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="82ade-193">(Необязательно) Отправлять push-уведомления прямо из приложения hello</span><span class="sxs-lookup"><span data-stu-id="82ade-193">(Optional) Send push notifications directly from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="82ade-194">В этом примере отправки уведомлений из клиентского приложения hello предоставляется только в целях обучения.</span><span class="sxs-lookup"><span data-stu-id="82ade-194">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="82ade-195">Так как для этого потребуется hello `DefaultFullSharedAccessSignature` toobe на клиентское приложение hello, он предоставляет, пользователь может получить уведомления toosend несанкционированный доступ клиентов tooyour риск toohello концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="82ade-195">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="82ade-196">Обычно уведомления отправляются с сервера базы данных.</span><span class="sxs-lookup"><span data-stu-id="82ade-196">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="82ade-197">В некоторых случаях может потребоваться toobe push-уведомлений может toosend непосредственно из клиентского приложения hello.</span><span class="sxs-lookup"><span data-stu-id="82ade-197">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="82ade-198">В этом разделе описывается, как toosend уведомления с помощью клиента hello hello [API REST для концентратора уведомлений Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="82ade-198">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="82ade-199">В представлении проекта Android Studio разверните узел **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="82ade-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="82ade-200">Откройте hello `activity_main.xml` макета и выберите пункт hello **текст** вкладке tooupdate hello текстовое содержимое файла hello.</span><span class="sxs-lookup"><span data-stu-id="82ade-200">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="82ade-201">Обновите его с hello кода, который добавляет новые `Button` и `EditText` элементы управления для отправки push-концентратор уведомлений toohello сообщения уведомления.</span><span class="sxs-lookup"><span data-stu-id="82ade-201">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="82ade-202">Добавьте следующий код в нижней hello непосредственно перед `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="82ade-202">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="82ade-203">В представлении проекта Android Studio разверните узел **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="82ade-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="82ade-204">Откройте hello `strings.xml` и добавьте hello строковых значений, на которые ссылается hello нового файла `Button` и `EditText` элементов управления.</span><span class="sxs-lookup"><span data-stu-id="82ade-204">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="82ade-205">Добавьте следующие hello нижней части файла hello непосредственно перед `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="82ade-205">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="82ade-206">В вашей `NotificationSetting.java` файл, добавьте следующий параметр toohello hello `NotificationSettings` класса.</span><span class="sxs-lookup"><span data-stu-id="82ade-206">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="82ade-207">Обновление `HubFullAccess` с hello **DefaultFullSharedAccessSignature** строку подключения для концентратор.</span><span class="sxs-lookup"><span data-stu-id="82ade-207">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="82ade-208">В этой строке подключения можно скопировать из hello [портала Azure] , щелкнув **политики доступа** на hello **параметры** колонке концентратор уведомлений.</span><span class="sxs-lookup"><span data-stu-id="82ade-208">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. <span data-ttu-id="82ade-209">В вашей `MainActivity.java` файл, добавьте следующее hello `import` инструкции выше hello `MainActivity` класса.</span><span class="sxs-lookup"><span data-stu-id="82ade-209">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="82ade-210">В вашей `MainActivity.java` файл, добавить следующие члены вверху hello hello hello `MainActivity` класса.</span><span class="sxs-lookup"><span data-stu-id="82ade-210">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="82ade-211">Необходимо создать tooauthenticate токена программного обеспечения URL-адреса (SaS) концентратора уведомлений tooyour POST запроса toosend сообщений.</span><span class="sxs-lookup"><span data-stu-id="82ade-211">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="82ade-212">Это делается путем синтаксического анализа hello данные ключа из строки подключения hello и последующего создания hello маркер SaS, как упоминалось в hello [основные понятия](http://msdn.microsoft.com/library/azure/dn495627.aspx) Справочник по REST API.</span><span class="sxs-lookup"><span data-stu-id="82ade-212">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="82ade-213">Привет, следующий код представляет собой пример реализацию.</span><span class="sxs-lookup"><span data-stu-id="82ade-213">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="82ade-214">В `MainActivity.java`, добавьте следующий метод toohello hello `MainActivity` класса tooparse строки подключения.</span><span class="sxs-lookup"><span data-stu-id="82ade-214">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
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
7. <span data-ttu-id="82ade-215">В `MainActivity.java`, добавьте следующий метод toohello hello `MainActivity` класса toocreate маркер проверки подлинности SaS.</span><span class="sxs-lookup"><span data-stu-id="82ade-215">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
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
8. <span data-ttu-id="82ade-216">В `MainActivity.java`, добавьте следующий метод toohello hello `MainActivity` hello класс toohandle **отправить уведомление** нажмите кнопку и отправить push-уведомление hello концентратора toohello сообщения с помощью hello встроенных API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="82ade-216">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
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

## <a name="testing-your-app"></a><span data-ttu-id="82ade-217">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="82ade-217">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="82ade-218">Push-уведомлений в эмуляторе hello</span><span class="sxs-lookup"><span data-stu-id="82ade-218">Push notifications in hello emulator</span></span>
<span data-ttu-id="82ade-219">Следует tootest push-уведомлений в эмуляторе убедитесь, что образ эмулятора поддерживает уровень Google API hello, выбранное для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="82ade-219">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="82ade-220">Если изображение не поддерживает собственные интерфейсы API Google, вы получите hello **службы\_не\_ДОСТУПНО** исключение.</span><span class="sxs-lookup"><span data-stu-id="82ade-220">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="82ade-221">Кроме toohello выше, убедитесь, что вы добавили запуска эмулятора под учетной записью tooyour вашей Google система **параметры** > **учетные записи**.</span><span class="sxs-lookup"><span data-stu-id="82ade-221">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="82ade-222">В противном случае ваш tooregister попыток с GCM может привести к hello **проверки ПОДЛИННОСТИ\_сбой** исключение.</span><span class="sxs-lookup"><span data-stu-id="82ade-222">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="82ade-223">Запуск приложения hello</span><span class="sxs-lookup"><span data-stu-id="82ade-223">Running hello application</span></span>
1. <span data-ttu-id="82ade-224">Выполните приложение hello и обратите внимание, что идентификатор hello регистрации указывается для успешной регистрации.</span><span class="sxs-lookup"><span data-stu-id="82ade-224">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="82ade-225">Введите toobe сообщение уведомления, отправленные tooall устройств Android, которые зарегистрированы с концентратором hello.</span><span class="sxs-lookup"><span data-stu-id="82ade-225">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="82ade-226">Нажмите кнопку **Send Notification**(Отправить уведомление).</span><span class="sxs-lookup"><span data-stu-id="82ade-226">Press **Send Notification**.</span></span> <span data-ttu-id="82ade-227">Будут показаны все устройства, работающие приложения hello `AlertDialog` экземпляр с hello push-сообщение уведомления.</span><span class="sxs-lookup"><span data-stu-id="82ade-227">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="82ade-228">Устройства, нет hello приложение работает, но ранее зарегистрированные push-уведомлений получит уведомление hello диспетчера уведомлений Android.</span><span class="sxs-lookup"><span data-stu-id="82ade-228">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="82ade-229">Их можно просмотреть путем считывания вниз от верхнего левого угла hello.</span><span class="sxs-lookup"><span data-stu-id="82ade-229">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="82ade-230">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="82ade-230">Next steps</span></span>
<span data-ttu-id="82ade-231">Мы рекомендуем hello [toousers уведомления toopush использования концентраторов уведомлений] учебника в качестве следующего шага hello.</span><span class="sxs-lookup"><span data-stu-id="82ade-231">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="82ade-232">Также будет показано, как уведомления о toosend из серверной части ASP.NET с помощью тегов tootarget конкретных пользователей.</span><span class="sxs-lookup"><span data-stu-id="82ade-232">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="82ade-233">Если требуется toosegment пользователи, группы интересов извлечь hello [toosend использования концентраторов уведомлений, новости] учебника.</span><span class="sxs-lookup"><span data-stu-id="82ade-233">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="82ade-234">toolearn Дополнительные общие сведения о концентраторах уведомлений см. наш [руководство концентраторы уведомлений].</span><span class="sxs-lookup"><span data-stu-id="82ade-234">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

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
