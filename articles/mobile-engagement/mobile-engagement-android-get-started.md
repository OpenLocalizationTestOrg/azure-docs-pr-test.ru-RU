---
title: "Приступая к работе со Службой мобильного взаимодействия Azure для приложений Android"
description: "Узнайте, как использовать Службы мобильного взаимодействия Azure с аналитическими функциями и push-уведомлениями для приложений Android."
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
ms.openlocfilehash: dc255a930bf71e6ef6d964bc5e3472a38ce4e467
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="8b00e-103">Приступая к работе со Службами мобильного взаимодействия Azure для приложений Android</span><span class="sxs-lookup"><span data-stu-id="8b00e-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="8b00e-104">В этой статье показано, как применять Службы мобильного взаимодействия Azure для анализа использования приложения и как отправлять push-уведомления сегментированным пользователям приложения Android.</span><span class="sxs-lookup"><span data-stu-id="8b00e-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of an Android application.</span></span>
<span data-ttu-id="8b00e-105">В этом учебнике описывается простой сценарий вещания с использованием Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="8b00e-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="8b00e-106">В рассматриваемом сценарии создается пустое приложение Android, которое собирает основные данные и получает push-уведомления с помощью службы Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="8b00e-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b00e-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8b00e-107">Prerequisites</span></span>
<span data-ttu-id="8b00e-108">Для прохождения этого учебника требуются [Средства разработчика Android](https://developer.android.com/sdk/index.html), которые включают в себя интегрированную среду разработки Android Studio и новейшую платформу Android.</span><span class="sxs-lookup"><span data-stu-id="8b00e-108">Completing this tutorial requires the [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>

<span data-ttu-id="8b00e-109">Вам также понадобится [пакет SDK Android для Служб мобильного взаимодействия](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="8b00e-109">It also requires the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b00e-110">Для работы с этим руководством требуется активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="8b00e-110">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="8b00e-111">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="8b00e-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8b00e-112">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="8b00e-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="8b00e-113">Настройка Служб мобильного взаимодействия для вашего приложения Android</span><span class="sxs-lookup"><span data-stu-id="8b00e-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="8b00e-114">Подключение приложения к серверной части Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="8b00e-114">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="8b00e-115">В этом руководстве описаны действия по базовой интеграции, т. е. минимум, необходимый для сбора данных и отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="8b00e-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="8b00e-116">Вы создадите основное приложение с помощью Android Studio, чтобы продемонстрировать интеграцию.</span><span class="sxs-lookup"><span data-stu-id="8b00e-116">You create a basic app with Android Studio to demonstrate the integration.</span></span>

<span data-ttu-id="8b00e-117">Документацию о полной интеграции можно найти в статье [Интеграция пакета Android SDK со Службами мобильного взаимодействия Azure](mobile-engagement-android-sdk-overview.md)в разделе об интеграции.</span><span class="sxs-lookup"><span data-stu-id="8b00e-117">The complete integration documentation can be found in the [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="8b00e-118">Создание проекта Android</span><span class="sxs-lookup"><span data-stu-id="8b00e-118">Create an Android project</span></span>
1. <span data-ttu-id="8b00e-119">Запустите **Android Studio** и во всплывающем окне выберите элемент **Start a new Android Studio project** (Создать новый проект Android Studio).</span><span class="sxs-lookup"><span data-stu-id="8b00e-119">Start **Android Studio**, and in the pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="8b00e-120">Укажите имя приложения и домен компании.</span><span class="sxs-lookup"><span data-stu-id="8b00e-120">Provide an app name and company domain.</span></span> <span data-ttu-id="8b00e-121">Запишите указанные данные, они понадобятся вам в будущем.</span><span class="sxs-lookup"><span data-stu-id="8b00e-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="8b00e-122">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8b00e-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="8b00e-123">Выберите целевой форм-фактор и уровень API, а затем нажмите кнопку **Next**(Далее).</span><span class="sxs-lookup"><span data-stu-id="8b00e-123">Select the target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8b00e-124">Для Служб мобильного взаимодействия необходим уровень API минимум 10 (Android 2.3.3).</span><span class="sxs-lookup"><span data-stu-id="8b00e-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="8b00e-125">Выберите экран **Blank Activity** (Пустое действие), который является единственным в этом приложении, и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="8b00e-125">Select **Blank Activity** here, which is the only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="8b00e-126">В конце оставьте настройки по умолчанию и нажмите кнопку **Finish**(Готово).</span><span class="sxs-lookup"><span data-stu-id="8b00e-126">Finally, leave the defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="8b00e-127">Android Studio создаст демонстрационное приложение, в которое мы интегрируем Службы мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="8b00e-127">Android Studio now creates the demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-the-sdk-library-in-your-project"></a><span data-ttu-id="8b00e-128">Включение библиотеки пакета SDK в проект</span><span class="sxs-lookup"><span data-stu-id="8b00e-128">Include the SDK library in your project</span></span>
1. <span data-ttu-id="8b00e-129">Скачайте [пакет SDK Android для Служб мобильного взаимодействия](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="8b00e-129">Download the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="8b00e-130">Извлеките файл архива в папку на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8b00e-130">Extract the archive file to a folder in your computer.</span></span>
3. <span data-ttu-id="8b00e-131">Определите библиотеку JAR-файлов для текущей версии этого пакета SDK и скопируйте ее в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="8b00e-131">Identify the .jar library for the current version of this SDK and copy it to the Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="8b00e-132">Перейдите к разделу **Project** (Проект), обозначенному на рисунке цифрой 1, и вставьте JAR-файл в папку с библиотеками (обозначена цифрой 2).</span><span class="sxs-lookup"><span data-stu-id="8b00e-132">Navigate to the **Project** section (1) and paste the .jar in the libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="8b00e-133">Чтобы скачать библиотеку, синхронизируйте проект.</span><span class="sxs-lookup"><span data-stu-id="8b00e-133">To load the library, sync the project .</span></span>

      ![][8]

### <a name="connect-your-app-to-mobile-engagement-backend-with-the-connection-string"></a><span data-ttu-id="8b00e-134">Подключение приложения к серверной части Служб мобильного взаимодействия с помощью строки подключения</span><span class="sxs-lookup"><span data-stu-id="8b00e-134">Connect your app to Mobile Engagement backend with the Connection String</span></span>
1. <span data-ttu-id="8b00e-135">Скопируйте следующие строки кода в раздел создания действия (эта операция должна выполняться только в одном месте приложения, обычно в разделе основных действий).</span><span class="sxs-lookup"><span data-stu-id="8b00e-135">Copy the following lines of code into the activity creation (must be done only in one place of your application, usually the main activity).</span></span> <span data-ttu-id="8b00e-136">Для этого примера приложения откройте файл MainActivity в папке src > main -> java и добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="8b00e-136">For this sample app, open up the MainActivity under src -> main -> java folder and add the following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="8b00e-137">Добавьте ссылки, нажав сочетание клавиш ALT+ВВОД или добавив следующие операторы импорта.</span><span class="sxs-lookup"><span data-stu-id="8b00e-137">Resolve the references by pressing Alt + Enter or adding the following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="8b00e-138">Вернитесь на страницу **Сведения о подключении** классического портала Azure для вашего приложения и скопируйте **строку подключения**.</span><span class="sxs-lookup"><span data-stu-id="8b00e-138">Go back to the Azure Classic Portal in your app's **Connection Info** page and copy the **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="8b00e-139">Вставьте его в параметр `setConnectionString` (при этом нужно полностью заменить строку, показанную в следующем коде):</span><span class="sxs-lookup"><span data-stu-id="8b00e-139">Paste it into the `setConnectionString` parameter, replacing the entire string shown in the following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="8b00e-140">Добавление разрешений и объявления службы</span><span class="sxs-lookup"><span data-stu-id="8b00e-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="8b00e-141">Добавьте эти разрешения в Manifest.xml проекта непосредственно перед тегом `<application>` или после него:</span><span class="sxs-lookup"><span data-stu-id="8b00e-141">Add these permissions to the Manifest.xml of your project immediately before or after the `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="8b00e-142">Чтобы объявить службу агента, добавьте следующий код между тегами `<application>` и `</application>`:</span><span class="sxs-lookup"><span data-stu-id="8b00e-142">To declare the agent service, add this code between the `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="8b00e-143">Во вставленном вами коде замените `"<Your application name>"` в метке, отображаемой в меню **Параметры** , в котором отображаются службы, запущенные на устройстве.</span><span class="sxs-lookup"><span data-stu-id="8b00e-143">In the code you pasted, replace `"<Your application name>"` in the label, which is displayed in the **Settings** menu where you can see services running on the device.</span></span> <span data-ttu-id="8b00e-144">Вы можете добавить в метку слово, например Service (служба).</span><span class="sxs-lookup"><span data-stu-id="8b00e-144">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="8b00e-145">Отправка экрана в Службы мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="8b00e-145">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="8b00e-146">Чтобы начать отправку данных и убедиться, что пользователи активны, отправьте по крайней мере один экран (действие) в серверную часть Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="8b00e-146">To start sending data and ensure that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

<span data-ttu-id="8b00e-147">Откройте файл **MainActivity.java** и добавьте следующий код, чтобы заменить класс **MainActivity** классом **EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="8b00e-147">Go to **MainActivity.java** and add the following to replace the base class of **MainActivity** to **EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="8b00e-148">Если базовый класс не является классом *Activity*, см. описание наследования из разных классов в разделе, посвященном [расширенной отчетности в Android](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="8b00e-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how to inherit from different classes.</span></span>
>
>

<span data-ttu-id="8b00e-149">Закомментируйте следующую строку этого простого примера сценария:</span><span class="sxs-lookup"><span data-stu-id="8b00e-149">Comment out the following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="8b00e-150">Если хотите сохранить `ActionBar` в приложении, см. раздел [Изменение классов Activity](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="8b00e-150">If you want to keep the `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="8b00e-151">Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="8b00e-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="8b00e-152">Включение push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="8b00e-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="8b00e-153">Во время кампаний Службы мобильного взаимодействия позволяют взаимодействовать с пользователями и ОХВАТЫВАТЬ АУДИТОРИЮ с помощью push-уведомлений и сообщений в приложении.</span><span class="sxs-lookup"><span data-stu-id="8b00e-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="8b00e-154">На портале Служб мобильного взаимодействия этот модуль называется МОДУЛЕМ ОБРАБОТКИ РЕКЛАМНЫХ КАМПАНИЙ.</span><span class="sxs-lookup"><span data-stu-id="8b00e-154">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="8b00e-155">В следующем разделе показано, как настроить приложение для приема уведомлений и сообщений.</span><span class="sxs-lookup"><span data-stu-id="8b00e-155">The following section sets up your app to receive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="8b00e-156">Копирование ресурсов SDK в проект</span><span class="sxs-lookup"><span data-stu-id="8b00e-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="8b00e-157">Вернитесь к содержимому скачанного пакета SDK и скопируйте папку **res** .</span><span class="sxs-lookup"><span data-stu-id="8b00e-157">Navigate back to your SDK download content and copy the **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="8b00e-158">Вернитесь в Android Studio, выберите каталог **main** в файлах проекта и вставьте его, чтобы добавить ресурсы в проект.</span><span class="sxs-lookup"><span data-stu-id="8b00e-158">Go back to Android Studio, select the **main** directory of your project files, and then paste it to add the resources to your project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="8b00e-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b00e-159">Next steps</span></span>
<span data-ttu-id="8b00e-160">Подробные сведения об интеграции пакета SDK см. в статье [Интеграция пакета Android SDK с Azure Mobile Engagement](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8b00e-160">Go to [Android SDK](mobile-engagement-android-sdk-overview.md) to get detailed knowledge about the SDK integration.</span></span>

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
