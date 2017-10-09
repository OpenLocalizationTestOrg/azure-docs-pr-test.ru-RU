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
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="73761-103">Приступая к работе с Центрами уведомлений для приложений Xamarin в Android</span><span class="sxs-lookup"><span data-stu-id="73761-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="73761-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="73761-104">Overview</span></span>
<span data-ttu-id="73761-105">Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa Xamarin.Android приложения.</span><span class="sxs-lookup"><span data-stu-id="73761-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Xamarin.Android application.</span></span>
<span data-ttu-id="73761-106">Вы создаете пустое приложение Xamarin.Android, которое получает push-уведомления с помощью Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="73761-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="73761-107">После завершения вы будете иметь доступ toouse вашей toobroadcast концентратора уведомлений push-уведомления tooall hello устройств под управлением приложения.</span><span class="sxs-lookup"><span data-stu-id="73761-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="73761-108">Hello готовой код находится в hello [приложения NotificationHubs] [ GitHub] образца.</span><span class="sxs-lookup"><span data-stu-id="73761-108">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="73761-109">В этом учебнике показано простой сценарий широковещательных hello в с использованием концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="73761-109">This tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="73761-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="73761-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="73761-111">код завершения Hello в этом учебнике можно найти на GitHub [здесь](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="73761-111">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73761-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="73761-112">Prerequisites</span></span>
<span data-ttu-id="73761-113">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="73761-113">This tutorial requires hello following:</span></span>

* <span data-ttu-id="73761-114">Visual Studio с расширением Xamarin для Windows или Xamarin Studio для Mac OS X. Инструкции по установке см. в [руководстве по установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="73761-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="73761-115">Активная учетная запись Google</span><span class="sxs-lookup"><span data-stu-id="73761-115">Active Google account</span></span>
* <span data-ttu-id="73761-116">[Компонент обмена сообщениями в Azure]</span><span class="sxs-lookup"><span data-stu-id="73761-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="73761-117">[Компонент клиента Google Cloud Messaging]</span><span class="sxs-lookup"><span data-stu-id="73761-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="73761-118">Для прохождения других учебников, посвященных Центрам уведомлений для приложений Xamarin.Android, необходимо сначала выполнить действия, описанные в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="73761-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73761-119">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="73761-119">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="73761-120">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="73761-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="73761-121">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="73761-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="73761-122">Включение Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="73761-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="73761-123">Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="73761-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="73761-124">Нажмите кнопку hello <b>Настройка</b> вверху hello, введите hello <b>ключ API</b> значение, полученное в предыдущем разделе hello, а затем нажмите кнопку <b>Сохранить</b>.</span><span class="sxs-lookup"><span data-stu-id="73761-124">Click hello <b>Configure</b> tab at hello top, enter hello <b>API Key</b> value you obtained in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="73761-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="73761-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="73761-126">Концентратор уведомлений теперь настроенных toowork с GCM, и у вас есть hello соединения строки tooboth зарегистрировать уведомления tooreceive приложения и toosend push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="73761-126">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive notifications and toosend push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="73761-127">Подключение приложения toohello концентратор уведомлений</span><span class="sxs-lookup"><span data-stu-id="73761-127">Connect your app toohello notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="73761-128">Создание нового проекта</span><span class="sxs-lookup"><span data-stu-id="73761-128">Create a new project</span></span>
1. <span data-ttu-id="73761-129">В Xamarin Studio щелкните **New Solution** (Создать решение), **Android App** (Приложение Android) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="73761-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="73761-130">Введите значения в поля **App Name** (Имя приложения) и **Identifier** (Идентификатор).</span><span class="sxs-lookup"><span data-stu-id="73761-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="73761-131">Нажмите кнопку hello **целевых платформ это** toosupport и нажмите кнопку **Далее** и **создать**.</span><span class="sxs-lookup"><span data-stu-id="73761-131">Click hello **Target Plaforms** you want toosupport and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="73761-132">Будет создан проект Android.</span><span class="sxs-lookup"><span data-stu-id="73761-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="73761-133">Откройте свойства проекта hello, щелкнув правой кнопкой мыши новый проект в hello представление решений и выбрав **параметры**.</span><span class="sxs-lookup"><span data-stu-id="73761-133">Open hello project properties by right-clicking your new project in hello Solution view and choosing **Options**.</span></span> <span data-ttu-id="73761-134">Выберите hello **приложения Android** элемента в hello **построения** раздела.</span><span class="sxs-lookup"><span data-stu-id="73761-134">Select hello **Android Application** item in hello **Build** section.</span></span>
   
    <span data-ttu-id="73761-135">Убедитесь, что hello первую букву вашей **имя пакета** производится в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="73761-135">Ensure that hello first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="73761-136">Hello первой буквы имени пакета hello должны быть строчными.</span><span class="sxs-lookup"><span data-stu-id="73761-136">hello first letter of hello package name must be lowercase.</span></span> <span data-ttu-id="73761-137">В противном случае возникнут ошибки манифеста приложения при регистрации **BroadcastReceiver** и **IntentFilter** для push-уведомлений ниже.</span><span class="sxs-lookup"><span data-stu-id="73761-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="73761-138">При необходимости набор hello **Android Минимальная версия** tooanother уровень API.</span><span class="sxs-lookup"><span data-stu-id="73761-138">Optionally, set hello **Minimum Android version** tooanother API Level.</span></span>
3. <span data-ttu-id="73761-139">При необходимости набор hello **Android целевой версии** toohello другая версия API, которые должны tootarget (должен быть уровень API 8 или более поздней).</span><span class="sxs-lookup"><span data-stu-id="73761-139">Optionally, set hello **Target Android version** toohello another API version that you want tootarget (must be API level 8 or higher).</span></span>

<span data-ttu-id="73761-140">Нажмите кнопку **ОК** и диалогового окна параметров проекта закрыть hello.</span><span class="sxs-lookup"><span data-stu-id="73761-140">Click **OK** and close hello Project Options dialog.</span></span>

### <a name="add-hello-required-components-tooyour-project"></a><span data-ttu-id="73761-141">Добавление проекта tooyour hello необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="73761-141">Add hello required components tooyour project</span></span>
<span data-ttu-id="73761-142">Hello облака обмена сообщениями клиент Google на hello хранилище компонентов Xamarin упрощает процесс hello поддержки push-уведомлений в Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="73761-142">hello Google Cloud Messaging Client available on hello Xamarin Component Store simplifies hello process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="73761-143">Щелкните правой кнопкой мыши папку hello компоненты в приложении Xamarin.Android и выберите **получить более компонентов**.</span><span class="sxs-lookup"><span data-stu-id="73761-143">Right-click hello Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="73761-144">Поиск hello **обмена сообщениями Azure** компонента и добавьте его в проект toohello.</span><span class="sxs-lookup"><span data-stu-id="73761-144">Search for hello **Azure Messaging** component and add it toohello project.</span></span>
3. <span data-ttu-id="73761-145">Поиск hello **клиент обмена сообщениями Google облака** компонента и добавьте его в проект toohello.</span><span class="sxs-lookup"><span data-stu-id="73761-145">Search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="73761-146">Настройка центров уведомлений в проекте</span><span class="sxs-lookup"><span data-stu-id="73761-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="73761-147">Соберите следующую информацию для вашей Android приложения и концентратор уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="73761-147">Gather hello following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="73761-148">**GoogleProjectNumber**: это значение номер проекта можно получить из сводки hello приложения на портал разработчиков Google hello.</span><span class="sxs-lookup"><span data-stu-id="73761-148">**GoogleProjectNumber**:  Get this Project Number value from hello overview of your app on hello Google Developer Portal.</span></span> <span data-ttu-id="73761-149">Был записан на более ранних версий этого значения при создании приложения hello на портале hello.</span><span class="sxs-lookup"><span data-stu-id="73761-149">You made a note of this value earlier when you created hello app on hello portal.</span></span>
   * <span data-ttu-id="73761-150">**Прослушивание строка подключения**: hello в hello мониторинга [классический портал Azure], нажмите кнопку **Просмотр строк подключения**.</span><span class="sxs-lookup"><span data-stu-id="73761-150">**Listen connection string**: On hello dashboard in hello [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="73761-151">Копировать hello *DefaultListenSharedAccessSignature* строку подключения для этого значения.</span><span class="sxs-lookup"><span data-stu-id="73761-151">Copy hello *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="73761-152">**Имя концентратора**: hello имя концентратора, из hello [классический портал Azure].</span><span class="sxs-lookup"><span data-stu-id="73761-152">**Hub name**: This is hello name of your hub from hello [Azure Classic Portal].</span></span> <span data-ttu-id="73761-153">Например, *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="73761-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="73761-154">Создание **Constants.cs** класса для проекта Xamarin и определите следующие константы в классе hello hello.</span><span class="sxs-lookup"><span data-stu-id="73761-154">Create a **Constants.cs** class for your Xamarin project and define hello following constant values in hello class.</span></span> <span data-ttu-id="73761-155">Замените значения заполнителей hello.</span><span class="sxs-lookup"><span data-stu-id="73761-155">Replace hello placeholders with your values.</span></span>
     
       <span data-ttu-id="73761-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="73761-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="73761-157">}</span><span class="sxs-lookup"><span data-stu-id="73761-157">}</span></span>
2. <span data-ttu-id="73761-158">Добавьте hello следующие операторы using слишком**MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="73761-158">Add hello following using statements too**MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="73761-159">Добавьте экземпляр переменной toohello `MainActivity` класс, который будет использоваться tooshow диалогового окна предупреждения при запуске приложение hello:</span><span class="sxs-lookup"><span data-stu-id="73761-159">Add an instance variable toohello `MainActivity` class that will be used tooshow an alert dialog when hello app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="73761-160">Создайте следующий метод в hello hello **MainActivity** класса:</span><span class="sxs-lookup"><span data-stu-id="73761-160">Create hello following method in hello **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="73761-161">В hello `OnCreate` метод **MainActivity.cs**, инициализировать hello `instance` переменной и добавить вызов слишком`RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="73761-161">In hello `OnCreate` method of **MainActivity.cs**, initialize hello `instance` variable and add a call too`RegisterWithGCM`:</span></span>
   
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
6. <span data-ttu-id="73761-162">Создайте класс **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="73761-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="73761-163">Здесь мы рассмотрим создание класса **BroadcastReceiver** с нуля.</span><span class="sxs-lookup"><span data-stu-id="73761-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="73761-164">Тем не менее Создание быстрого альтернативных toomanually **MyBroadcastReceiver.cs** — toorefer toohello **GcmService.cs** файл найден в проекте Xamarin.Android образец hello, входящий в состав hello [Образцы NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="73761-164">However, a quick alternative toomanually creating **MyBroadcastReceiver.cs** is toorefer toohello **GcmService.cs** file found in hello sample Xamarin.Android project included with hello [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="73761-165">Дублирование **GcmService.cs** и изменение имен класса может быть также toostart отличное место.</span><span class="sxs-lookup"><span data-stu-id="73761-165">Duplicating **GcmService.cs** and changing class names can be a great place toostart as well.</span></span>
   > 
   > 
7. <span data-ttu-id="73761-166">Добавьте следующее hello с помощью инструкций слишком**MyBroadcastReceiver.cs** (ссылается компонент toohello и сборки, который был добавлен ранее):</span><span class="sxs-lookup"><span data-stu-id="73761-166">Add hello following using statements too**MyBroadcastReceiver.cs** (referring toohello component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="73761-167">В **MyBroadcastReceiver.cs**, добавить следующие запросы разрешений между hello hello **с помощью** инструкций и hello **имен** объявление:</span><span class="sxs-lookup"><span data-stu-id="73761-167">In **MyBroadcastReceiver.cs**, add hello following permission requests between hello **using** statements and hello **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="73761-168">В **MyBroadcastReceiver.cs**, измените hello **MyBroadcastReceiver** класса toomatch hello следующее:</span><span class="sxs-lookup"><span data-stu-id="73761-168">In **MyBroadcastReceiver.cs**, change hello **MyBroadcastReceiver** class toomatch hello following:</span></span>
   
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
10. <span data-ttu-id="73761-169">Добавьте в файл **MyBroadcastReceiver.cs** еще один класс с именем **PushHandlerService**, сделав его производным от **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="73761-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="73761-170">Убедитесь, что hello tooapply **службы** toohello класс атрибута:</span><span class="sxs-lookup"><span data-stu-id="73761-170">Make sure tooapply hello **Service** attribute toohello class:</span></span>
    
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
11. <span data-ttu-id="73761-171">**GcmServiceBase** реализует методы **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** и **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="73761-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="73761-172">Наш **PushHandlerService** реализации класса необходимо переопределить эти методы, и эти методы будут срабатывать в ответ toointeracting с концентратором уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="73761-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response toointeracting with hello notification hub.</span></span>
12. <span data-ttu-id="73761-173">Переопределить hello **OnRegistered()** метод в **PushHandlerService** с помощью hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="73761-173">Override hello **OnRegistered()** method in **PushHandlerService** by using hello following code:</span></span>
    
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
    > <span data-ttu-id="73761-174">В hello **OnRegistered()** кода выше, следует иметь в виду tooregister hello возможность toospecify тегов для определенных каналов обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="73761-174">In hello **OnRegistered()** code above, you should note hello ability toospecify tags tooregister for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="73761-175">Переопределить hello **OnMessage** метод в **PushHandlerService** с помощью hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="73761-175">Override hello **OnMessage** method in **PushHandlerService** by using hello following code:</span></span>
    
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
14. <span data-ttu-id="73761-176">Добавьте следующее hello **createNotification** и **dialogNotify** методы слишком**PushHandlerService** для уведомления пользователей при получении уведомления.</span><span class="sxs-lookup"><span data-stu-id="73761-176">Add hello following **createNotification** and **dialogNotify** methods too**PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="73761-177">Структура уведомлений в версии платформы Android 5.0 и более поздних версиях существенно отличается от структуры в предыдущих версиях.</span><span class="sxs-lookup"><span data-stu-id="73761-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="73761-178">Если вы тестируете, Android 5.0 или более поздней версии, приложение hello потребуется toobe под управлением tooreceive hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="73761-178">If you test this on Android 5.0 or later, hello app will need toobe running tooreceive hello notification.</span></span> <span data-ttu-id="73761-179">Дополнительные сведения см. в статье об [уведомлениях Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="73761-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
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
15. <span data-ttu-id="73761-180">Переопределите абстрактные члены **OnUnRegistered()**, **OnRecoverableError()** и **OnError()** для компиляции кода:</span><span class="sxs-lookup"><span data-stu-id="73761-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
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

## <a name="run-your-app-in-hello-emulator"></a><span data-ttu-id="73761-181">Запуск приложения в эмуляторе hello</span><span class="sxs-lookup"><span data-stu-id="73761-181">Run your app in hello emulator</span></span>
<span data-ttu-id="73761-182">Если запустить это приложение в эмуляторе hello, убедитесь, что используется виртуального устройства Android (AVD), поддерживающий Google API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="73761-182">If you run this app in hello emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73761-183">В порядке tooreceive извещающих уведомлений необходимо настроить учетную запись Google на виртуального устройства Android.</span><span class="sxs-lookup"><span data-stu-id="73761-183">In order tooreceive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="73761-184">(В эмуляторе hello перейдите слишком**параметры** и нажмите кнопку **добавить учетную запись**.) Кроме того убедитесь, что эмулятор, hello — подключенных toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="73761-184">(In hello emulator, navigate too**Settings** and click **Add Account**.) Also, make sure that hello emulator is connected toohello Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="73761-185">Структура уведомлений в версии платформы Android 5.0 и более поздних версиях существенно отличается от структуры в предыдущих версиях.</span><span class="sxs-lookup"><span data-stu-id="73761-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="73761-186">Дополнительные сведения см. в статье об [уведомлениях Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="73761-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="73761-187">В меню **Tools** (Средства) щелкните **Open Android Emulator Manager** (Открыть диспетчер эмулятора Android), выберите свое устройство и нажмите кнопку **Edit** (Изменить).</span><span class="sxs-lookup"><span data-stu-id="73761-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="73761-188">В разделе **Target** (Цель) выберите **Google APIs** (API-интерфейсы Google), а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="73761-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="73761-189">На верхней панели инструментов hello, нажмите кнопку **запуска**, а затем выберите приложение.</span><span class="sxs-lookup"><span data-stu-id="73761-189">On hello top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="73761-190">Это запускает эмулятор hello и приложение hello.</span><span class="sxs-lookup"><span data-stu-id="73761-190">This starts hello emulator and runs hello app.</span></span>
   
   <span data-ttu-id="73761-191">приложение Hello извлекает hello *registrationId* из GCM и регистры с концентратором уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="73761-191">hello app retrieves hello *registrationId* from GCM and registers with hello notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="73761-192">Отправка уведомлений из серверной части</span><span class="sxs-lookup"><span data-stu-id="73761-192">Send notifications from your backend</span></span>
<span data-ttu-id="73761-193">Можно проверить получение уведомлений в приложение путем отправки уведомления в hello [классический портал Azure] через hello вкладки отладчика на концентраторе уведомлений hello, как показано ниже экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="73761-193">You can test receiving notifications in your app by sending notifications in hello [Azure Classic Portal] via hello debug tab on hello notification hub, as shown in hello screen below.</span></span>

![][30]

<span data-ttu-id="73761-194">Push-уведомления обычно отправляются в серверной службе, например мобильными службами или ASP.NET, с помощью совместимой библиотеки.</span><span class="sxs-lookup"><span data-stu-id="73761-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="73761-195">Также можно использовать hello REST API напрямую toosend уведомления сообщений, если библиотека недоступна для серверной части.</span><span class="sxs-lookup"><span data-stu-id="73761-195">You can also use hello REST API directly toosend notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="73761-196">Ниже приведен список некоторых учебников, которые можно tooreview для отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="73761-196">Here is a list of some other tutorials that you may want tooreview for sending notifications:</span></span>

* <span data-ttu-id="73761-197">ASP.NET: В разделе [toousers уведомления toopush использования концентраторов уведомлений].</span><span class="sxs-lookup"><span data-stu-id="73761-197">ASP.NET: See [Use Notification Hubs toopush notifications toousers].</span></span>
* <span data-ttu-id="73761-198">Azure Java концентраторы уведомлений SDK: в разделе [как toouse концентраторы уведомлений из Java](notification-hubs-java-push-notification-tutorial.md) для отправки уведомлений из Java.</span><span class="sxs-lookup"><span data-stu-id="73761-198">Azure Notification Hubs Java SDK: See [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="73761-199">Было протестировано в Eclipse для разработки для Android.</span><span class="sxs-lookup"><span data-stu-id="73761-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="73761-200">PHP: В разделе [как концентраторы уведомлений из PHP toouse](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="73761-200">PHP: See [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="73761-201">В подразделах следующего hello учебника hello отправлять уведомления с помощью консольного приложения .NET, а также с помощью мобильной службы через узел сценария.</span><span class="sxs-lookup"><span data-stu-id="73761-201">In hello next subsections of hello tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="73761-202">(Необязательно) Отправка уведомлений с помощью приложения .NET</span><span class="sxs-lookup"><span data-stu-id="73761-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="73761-203">В этом разделе мы будем отправлять уведомления с помощью консольного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="73761-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="73761-204">Создайте новое консольное приложение Visual C#.</span><span class="sxs-lookup"><span data-stu-id="73761-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="73761-205">В Visual Studio последовательно выберите элементы **Сервис**, **Диспетчер пакетов NuGet** и **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="73761-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="73761-206">Откроется консоль диспетчера пакетов hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73761-206">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="73761-207">В hello в окне консоли диспетчера пакетов, задайте hello **проекта по умолчанию** tooyour нового консольного приложения проекта, а затем в окне консоли hello, выполните hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="73761-207">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="73761-208">При этом добавляется ссылка toohello концентраторов уведомлений Azure SDK с помощью hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакет NuGet концентраторов Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="73761-208">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="73761-209">Откройте файл Program.cs hello и добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="73761-209">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="73761-210">В вашей `Program` добавьте следующий метод hello.</span><span class="sxs-lookup"><span data-stu-id="73761-210">In your `Program` class, add hello following method.</span></span> <span data-ttu-id="73761-211">Обновление текста заполнителя hello с вашей *DefaultFullSharedAccessSignature* имя концентратора и строку соединения из hello [классический портал Azure].</span><span class="sxs-lookup"><span data-stu-id="73761-211">Update hello placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from hello [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="73761-212">Добавьте следующие строки в hello вашей **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="73761-212">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="73761-213">Нажмите клавишу приложение hello ключа toorun F5 hello.</span><span class="sxs-lookup"><span data-stu-id="73761-213">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="73761-214">Вы должны получить уведомление в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="73761-214">You should receive a notification in hello app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="73761-215">(Необязательно) Отправка уведомлений с помощью мобильной службы</span><span class="sxs-lookup"><span data-stu-id="73761-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="73761-216">Выполните действия, описанные в статье [Приступая к работе с мобильными службами].</span><span class="sxs-lookup"><span data-stu-id="73761-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="73761-217">Войдите в toohello [классический портал Azure]и выберите мобильной службы.</span><span class="sxs-lookup"><span data-stu-id="73761-217">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="73761-218">Выберите hello **планировщика** вкладки в верхней части hello.</span><span class="sxs-lookup"><span data-stu-id="73761-218">Select hello **Scheduler** tab on hello top.</span></span>
   
      ![][22]
4. <span data-ttu-id="73761-219">Создайте новое запланированное задание, вставьте имя и выберите **По запросу**.</span><span class="sxs-lookup"><span data-stu-id="73761-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="73761-220">При создании задания hello, щелкните имя задания hello.</span><span class="sxs-lookup"><span data-stu-id="73761-220">When hello job is created, click hello job name.</span></span> <span data-ttu-id="73761-221">Нажмите кнопку hello **сценарий** вкладку на верхней панели hello.</span><span class="sxs-lookup"><span data-stu-id="73761-221">Then click hello **Script** tab on hello top bar.</span></span>
6. <span data-ttu-id="73761-222">Вставьте следующий сценарий внутри функции планировщика hello.</span><span class="sxs-lookup"><span data-stu-id="73761-222">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="73761-223">Убедитесь, что tooreplace hello местозаполнителей уведомления имя и hello строку подключения к концентратору для *DefaultFullSharedAccessSignature* , полученный ранее.</span><span class="sxs-lookup"><span data-stu-id="73761-223">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="73761-224">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="73761-224">Click **Save**.</span></span>
   
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
7. <span data-ttu-id="73761-225">Нажмите кнопку **выполнить один раз** на нижней панели hello.</span><span class="sxs-lookup"><span data-stu-id="73761-225">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="73761-226">Вы получите всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="73761-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73761-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="73761-227">Next steps</span></span>
<span data-ttu-id="73761-228">В этом простом примере вы широковещательной рассылки уведомлений tooall устройства Android.</span><span class="sxs-lookup"><span data-stu-id="73761-228">In this simple example, you broadcasted notifications tooall your Android devices.</span></span> <span data-ttu-id="73761-229">В заказ tootarget определенным пользователям, см. Учебник toohello [toousers уведомления toopush использования концентраторов уведомлений].</span><span class="sxs-lookup"><span data-stu-id="73761-229">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="73761-230">Следует ли toosegment пользователям по группы интересов, можно прочитать [toosend использования концентраторов уведомлений, новости].</span><span class="sxs-lookup"><span data-stu-id="73761-230">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="73761-231">Дополнительные сведения о toouse концентраторов уведомлений в [руководство концентраторы уведомлений] и в hello [Android toofor как концентраторы уведомлений].</span><span class="sxs-lookup"><span data-stu-id="73761-231">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor Android].</span></span>

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
