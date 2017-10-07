---
title: "aaaGet к работе с Android приложения Azure Mobile Engagement"
description: "Узнайте, как toouse Azure Mobile Engagement с analytics и отправка уведомлений для приложений Android."
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="8d9da-103">Приступая к работе со Службами мобильного взаимодействия Azure для приложений Android</span><span class="sxs-lookup"><span data-stu-id="8d9da-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="8d9da-104">В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использовании веб-приложения и как toosend push-уведомления toosegmented пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="8d9da-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of an Android application.</span></span>
<span data-ttu-id="8d9da-105">В этом учебнике показано hello простой широковещательных сценарий с помощью мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="8d9da-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="8d9da-106">В рассматриваемом сценарии создается пустое приложение Android, которое собирает основные данные и получает push-уведомления с помощью службы Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="8d9da-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d9da-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8d9da-107">Prerequisites</span></span>
<span data-ttu-id="8d9da-108">Изучения этого учебника требуется hello [Android Developer Tools](https://developer.android.com/sdk/index.html), включающее hello Android Studio интегрированной среды разработки, а также последнюю версию платформы Android hello.</span><span class="sxs-lookup"><span data-stu-id="8d9da-108">Completing this tutorial requires hello [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>

<span data-ttu-id="8d9da-109">Это также требует hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="8d9da-109">It also requires hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8d9da-110">toocomplete этого учебника требуется активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9da-110">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="8d9da-111">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="8d9da-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8d9da-112">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="8d9da-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="8d9da-113">Настройка Служб мобильного взаимодействия для вашего приложения Android</span><span class="sxs-lookup"><span data-stu-id="8d9da-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="8d9da-114">Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="8d9da-114">Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="8d9da-115">В этом руководстве содержатся «базовой интеграции», который hello минимальный набор данных требуется toocollect и отправить push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="8d9da-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="8d9da-116">Создать простое приложение с интеграцией hello toodemonstrate Android Studio.</span><span class="sxs-lookup"><span data-stu-id="8d9da-116">You create a basic app with Android Studio toodemonstrate hello integration.</span></span>

<span data-ttu-id="8d9da-117">Hello полной интеграции документацию можно найти в hello [Mobile Engagement Android SDK интеграции](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8d9da-117">hello complete integration documentation can be found in hello [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="8d9da-118">Создание проекта Android</span><span class="sxs-lookup"><span data-stu-id="8d9da-118">Create an Android project</span></span>
1. <span data-ttu-id="8d9da-119">Запуск **Android Studio**затем во всплывающем hello **Создание нового проекта Android Studio**.</span><span class="sxs-lookup"><span data-stu-id="8d9da-119">Start **Android Studio**, and in hello pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="8d9da-120">Укажите имя приложения и домен компании.</span><span class="sxs-lookup"><span data-stu-id="8d9da-120">Provide an app name and company domain.</span></span> <span data-ttu-id="8d9da-121">Запишите указанные данные, они понадобятся вам в будущем.</span><span class="sxs-lookup"><span data-stu-id="8d9da-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="8d9da-122">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8d9da-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="8d9da-123">Форм-фактор hello целевой уровень API и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8d9da-123">Select hello target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8d9da-124">Для Служб мобильного взаимодействия необходим уровень API минимум 10 (Android 2.3.3).</span><span class="sxs-lookup"><span data-stu-id="8d9da-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="8d9da-125">Выберите **пустое действие** здесь, который является только экрана приветствия для этого приложения и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8d9da-125">Select **Blank Activity** here, which is hello only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="8d9da-126">Наконец, оставьте значения по умолчанию hello и нажмите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="8d9da-126">Finally, leave hello defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="8d9da-127">Android Studio создаст hello нашего примера приложения, в который мы интегрировать мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="8d9da-127">Android Studio now creates hello demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-hello-sdk-library-in-your-project"></a><span data-ttu-id="8d9da-128">Включить в проект библиотеки пакета SDK для hello</span><span class="sxs-lookup"><span data-stu-id="8d9da-128">Include hello SDK library in your project</span></span>
1. <span data-ttu-id="8d9da-129">Загрузите hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="8d9da-129">Download hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="8d9da-130">Извлеките hello архивной папки tooa файл на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8d9da-130">Extract hello archive file tooa folder in your computer.</span></span>
3. <span data-ttu-id="8d9da-131">Определить библиотеку .jar hello hello текущей версией этого пакета SDK и скопировать его toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="8d9da-131">Identify hello .jar library for hello current version of this SDK and copy it toohello Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="8d9da-132">Перейдите toohello **проекта** статьи (1) и вставьте hello .jar в папке библиотеки hello (2).</span><span class="sxs-lookup"><span data-stu-id="8d9da-132">Navigate toohello **Project** section (1) and paste hello .jar in hello libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="8d9da-133">Библиотека tooload hello, проекта hello синхронизации.</span><span class="sxs-lookup"><span data-stu-id="8d9da-133">tooload hello library, sync hello project .</span></span>

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a><span data-ttu-id="8d9da-134">Подключение Engagement tooMobile внутренний сервер приложений с hello строки подключения</span><span class="sxs-lookup"><span data-stu-id="8d9da-134">Connect your app tooMobile Engagement backend with hello Connection String</span></span>
1. <span data-ttu-id="8d9da-135">Скопируйте следующие строки кода в создании действия hello (должно быть выполнено только в одном месте приложения, обычно hello основных действий) hello.</span><span class="sxs-lookup"><span data-stu-id="8d9da-135">Copy hello following lines of code into hello activity creation (must be done only in one place of your application, usually hello main activity).</span></span> <span data-ttu-id="8d9da-136">Для этого образца приложения откройте hello MainActivity под src -> main папку java "->" и добавьте следующее hello:</span><span class="sxs-lookup"><span data-stu-id="8d9da-136">For this sample app, open up hello MainActivity under src -> main -> java folder and add hello following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="8d9da-137">Разрешить ссылки hello, нажав клавиши Alt + Ввод или добавляя hello, следующие инструкции import:</span><span class="sxs-lookup"><span data-stu-id="8d9da-137">Resolve hello references by pressing Alt + Enter or adding hello following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="8d9da-138">Вернитесь к предыдущему окну классический портал Azure toohello в вашем приложении **сведений о соединении** страницы и скопируйте hello **строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="8d9da-138">Go back toohello Azure Classic Portal in your app's **Connection Info** page and copy hello **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="8d9da-139">Вставьте его в hello `setConnectionString` параметра, заменив всю строку hello показано hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="8d9da-139">Paste it into hello `setConnectionString` parameter, replacing hello entire string shown in hello following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="8d9da-140">Добавление разрешений и объявления службы</span><span class="sxs-lookup"><span data-stu-id="8d9da-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="8d9da-141">Добавьте эти разрешения toohello Manifest.xml проекта непосредственно перед или после hello `<application>` тег:</span><span class="sxs-lookup"><span data-stu-id="8d9da-141">Add these permissions toohello Manifest.xml of your project immediately before or after hello `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="8d9da-142">toodeclare Здравствуйте, служба агента, добавьте следующий код между hello `<application>` и `</application>` теги:</span><span class="sxs-lookup"><span data-stu-id="8d9da-142">toodeclare hello agent service, add this code between hello `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="8d9da-143">В коде hello вставленного замените `"<Your application name>"` в hello метки, которая отображается в hello **параметры** меню, где можно просматривать службы, работающие на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="8d9da-143">In hello code you pasted, replace `"<Your application name>"` in hello label, which is displayed in hello **Settings** menu where you can see services running on hello device.</span></span> <span data-ttu-id="8d9da-144">Можно добавить слово hello «Служба» в этой метке например.</span><span class="sxs-lookup"><span data-stu-id="8d9da-144">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="8d9da-145">Отправить экрана tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8d9da-145">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="8d9da-146">Отправка данных toostart и убедитесь, что пользователи hello активны, необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана (действие).</span><span class="sxs-lookup"><span data-stu-id="8d9da-146">toostart sending data and ensure that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

<span data-ttu-id="8d9da-147">Go слишком**MainActivity.java** и добавить следующие tooreplace hello базовый класс hello **MainActivity** слишком**EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="8d9da-147">Go too**MainActivity.java** and add hello following tooreplace hello base class of **MainActivity** too**EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="8d9da-148">Если базовый класс не *действия*, обратитесь к [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) как tooinherit из различных классов.</span><span class="sxs-lookup"><span data-stu-id="8d9da-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how tooinherit from different classes.</span></span>
>
>

<span data-ttu-id="8d9da-149">Закомментируйте hello, следующей строкой для этого простого примера сценария:</span><span class="sxs-lookup"><span data-stu-id="8d9da-149">Comment out hello following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="8d9da-150">Если требуется tookeep hello `ActionBar` в приложении, в разделе [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="8d9da-150">If you want tookeep hello `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="8d9da-151">Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="8d9da-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="8d9da-152">Включение push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="8d9da-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="8d9da-153">Во время кампаний Службы мобильного взаимодействия позволяют взаимодействовать с пользователями и ОХВАТЫВАТЬ АУДИТОРИЮ с помощью push-уведомлений и сообщений в приложении.</span><span class="sxs-lookup"><span data-stu-id="8d9da-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="8d9da-154">Этот модуль вызывается REACH на портале мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="8d9da-154">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="8d9da-155">Привет, в следующем разделе устанавливает вашего приложения tooreceive их.</span><span class="sxs-lookup"><span data-stu-id="8d9da-155">hello following section sets up your app tooreceive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="8d9da-156">Копирование ресурсов SDK в проект</span><span class="sxs-lookup"><span data-stu-id="8d9da-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="8d9da-157">Перейдите назад tooyour пакета SDK для загрузки содержимого и скопируйте hello **res** папки.</span><span class="sxs-lookup"><span data-stu-id="8d9da-157">Navigate back tooyour SDK download content and copy hello **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="8d9da-158">Вернитесь к предыдущему окну tooAndroid Studio, выберите hello **основной** каталог файлы проекта и вставьте его в проект tooyour ресурсы hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8d9da-158">Go back tooAndroid Studio, select hello **main** directory of your project files, and then paste it tooadd hello resources tooyour project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="8d9da-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d9da-159">Next steps</span></span>
<span data-ttu-id="8d9da-160">Go слишком[пакета SDK для Android](mobile-engagement-android-sdk-overview.md) tooget подробные сведения об интеграции пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="8d9da-160">Go too[Android SDK](mobile-engagement-android-sdk-overview.md) tooget detailed knowledge about hello SDK integration.</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
