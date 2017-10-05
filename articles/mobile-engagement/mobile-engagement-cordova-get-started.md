---
title: "Начало работы со Службами мобильного взаимодействия Azure для Cordova (Phonegap)"
description: "Узнайте, как использовать Служб мобильного взаимодействия Azure для аналитики и отправки push-уведомлений в приложения Cordova (Phonegap)."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d7a761310782faab1dda023785f93cf90742e2ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="6be06-103">Начало работы со Службами мобильного взаимодействия Azure для Cordova (Phonegap)</span><span class="sxs-lookup"><span data-stu-id="6be06-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="6be06-104">В этой статье показано, как использовать Службы мобильного взаимодействия Azure для анализа использования приложений и отправки push-уведомлений сегментированным пользователям мобильного приложения, разработанного на платформе Cordova.</span><span class="sxs-lookup"><span data-stu-id="6be06-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="6be06-105">В этом учебнике вы создадим пустое приложение Cordova на компьютере Mac и интегрируем пакет SDK для Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="6be06-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="6be06-106">Приложение будет собирать базовые данные аналитики и получать push-уведомления с помощью системы push-уведомлений Apple (APNS) для iOS и Google Cloud Messaging (GCM) для Android.</span><span class="sxs-lookup"><span data-stu-id="6be06-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="6be06-107">Для тестирования мы развернем его на устройствах под управлением iOS или Android.</span><span class="sxs-lookup"><span data-stu-id="6be06-107">We will deploy this to an iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="6be06-108">Для работы с этим учебником необходима активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6be06-108">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6be06-109">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6be06-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6be06-110">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span><span class="sxs-lookup"><span data-stu-id="6be06-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="6be06-111">Для работы с данным учебником требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="6be06-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="6be06-112">Xcode, который можно установить из Mac App Store (для развертывания на iOS)</span><span class="sxs-lookup"><span data-stu-id="6be06-112">XCode, which you can install from Mac App Store (for deploying to iOS)</span></span>
* <span data-ttu-id="6be06-113">[Android SDK и эмулятор](http://developer.android.com/sdk/installing/index.html) (для развертывания на Android).</span><span class="sxs-lookup"><span data-stu-id="6be06-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying to Android)</span></span>
* <span data-ttu-id="6be06-114">Сертификат push-уведомлений (P12), который можно получить в центре разработки Apple (для APNS)</span><span class="sxs-lookup"><span data-stu-id="6be06-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="6be06-115">Номер проекта GCM, который можно найти в консоли разработчиков Google (для GCM)</span><span class="sxs-lookup"><span data-stu-id="6be06-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="6be06-116">Подключаемый модуль Cordova для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="6be06-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="6be06-117">Исходный код и файл сведений о подключаемом модуле Cordova см. на сайте [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova).</span><span class="sxs-lookup"><span data-stu-id="6be06-117">You can find the source code and the ReadMe for the Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="6be06-118"><a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для приложения Cordova</span><span class="sxs-lookup"><span data-stu-id="6be06-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="6be06-119"><a id="connecting-app">
            </a>Подключение приложения к серверной части Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="6be06-119"><a id="connecting-app"></a>Connecting your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="6be06-120">В этом учебнике описаны действия по базовой интеграции, т. е. минимум, требуемый для сбора данных и отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6be06-120">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="6be06-121">Чтобы продемонстрировать интеграцию, мы создадим простое приложение при помощи Сordova.</span><span class="sxs-lookup"><span data-stu-id="6be06-121">We will create a basic app with Cordova to demonstrate the integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="6be06-122">Создание нового проекта Cordova</span><span class="sxs-lookup"><span data-stu-id="6be06-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="6be06-123">Чтобы создать проект Cordova на основе шаблона по умолчанию, откройте окно *терминала* на компьютере Mac и введите указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="6be06-123">Launch *Terminal* window on your Mac machine and type the following which will create a new Cordova project from the default template.</span></span> <span data-ttu-id="6be06-124">Убедитесь, что в профиле публикации, который вы впоследствии будете использовать для развертывания приложения iOS, используется идентификатор приложения "com.mycompany.myapp".</span><span class="sxs-lookup"><span data-stu-id="6be06-124">Make sure that the publishing profile you eventually use to deploy your iOS app is using 'com.mycompany.myapp' as the App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="6be06-125">Выполните указанные ниже команды, чтобы настроить проект для **iOS** и запустить его в iOS Simulator.</span><span class="sxs-lookup"><span data-stu-id="6be06-125">Execute the following to configure your project for **iOS** and run it in the iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="6be06-126">Выполните указанные ниже команды, чтобы настроить проект для **Android** и запустить его в эмуляторе Android.</span><span class="sxs-lookup"><span data-stu-id="6be06-126">Execute the following to configure your project for **Android** and run it in the Android emulator.</span></span> <span data-ttu-id="6be06-127">Убедитесь, что для параметров эмулятора Android SDK в качестве цели установлены API-интерфейсы Google (Google Inc.), а в качестве ЦП/ABI используется ARM API-интерфейсов Google.</span><span class="sxs-lookup"><span data-stu-id="6be06-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with the CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="6be06-128">Добавьте консольный подключаемый модуль Cordova.</span><span class="sxs-lookup"><span data-stu-id="6be06-128">Add the Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="6be06-129">Подключение приложения к серверной части Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="6be06-129">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="6be06-130">Установите подключаемый модуль Cordova для Служб мобильного взаимодействия Azure и укажите значения переменных для настройки подключаемого модуля:</span><span class="sxs-lookup"><span data-stu-id="6be06-130">Install the Azure Mobile Engagement Cordova plugin while providing the variable values to configure the plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers the app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="6be06-131">*Значок Android Reach* — это должно быть имя ресурса без расширения или префикса (например, mynotificationicon), а значок файла необходимо скопировать в приложение Android (platforms/android/res/drawable).</span><span class="sxs-lookup"><span data-stu-id="6be06-131">*Android Reach Icon* : must be the name of the resource without any extension, nor drawable prefix (ex: mynotificationicon), and the icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="6be06-132">*Значок iOS Reach* — это должно быть имя ресурса с расширением (например, mynotificationicon.png), а файл значка должен быть добавлен в проект iOS с XCode (с помощью меню "Добавить файлы").</span><span class="sxs-lookup"><span data-stu-id="6be06-132">*iOS Reach Icon*  : must be the name of the resource with its extension (ex:  mynotificationicon.png), and the icon file must be added into your iOS project with XCode (using the Add Files Menu)</span></span>

## <span data-ttu-id="6be06-133"><a id="monitor"></a>Включение мониторинга в реальном времени</span><span class="sxs-lookup"><span data-stu-id="6be06-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="6be06-134">В проекте Cordova добавьте в файл **www/js/index.js** вызов Служб мобильного взаимодействия, чтобы объявить новое действие после получения события *deviceReady*.</span><span class="sxs-lookup"><span data-stu-id="6be06-134">In the Cordova project - edit **www/js/index.js** to add the call to Mobile Engagement to declare a new activity once the *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="6be06-135">Запустите приложение:</span><span class="sxs-lookup"><span data-stu-id="6be06-135">Run the application:</span></span>
   
   * <span data-ttu-id="6be06-136">**Для iOS:**</span><span class="sxs-lookup"><span data-stu-id="6be06-136">**For iOS**</span></span>
     
       <span data-ttu-id="6be06-137">В окне `Terminal` запустите ваше приложение в новом экземпляре iOS Simulator, выполнив указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="6be06-137">In `Terminal` window launch your app in a new Simulator instance by executing the following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="6be06-138">**Для Android:**</span><span class="sxs-lookup"><span data-stu-id="6be06-138">**For Android**</span></span>
     
       <span data-ttu-id="6be06-139">В окне `Terminal` запустите ваше приложение в новом экземпляре эмулятора, выполнив указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="6be06-139">In `Terminal` window launch your app in a new emulator instance by executing the following:</span></span>
     
           cordova run android
3. <span data-ttu-id="6be06-140">В журнале консоли можно увидеть следующее:</span><span class="sxs-lookup"><span data-stu-id="6be06-140">You can see the following in the console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="6be06-141"><a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="6be06-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="6be06-142"><a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="6be06-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="6be06-143">Службы мобильного взаимодействия позволяют взаимодействовать с пользователями с помощью push-уведомлений и сообщений в приложении в контексте кампаний.</span><span class="sxs-lookup"><span data-stu-id="6be06-143">Mobile Engagement allows you to interact with your users using Push Notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="6be06-144">На портале Служб мобильного взаимодействия этот модуль называется МОДУЛЕМ ОБРАБОТКИ РЕКЛАМНЫХ КАМПАНИЙ.</span><span class="sxs-lookup"><span data-stu-id="6be06-144">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="6be06-145">В следующих разделах описаны действия по настройке приложения для приема уведомлений и сообщений.</span><span class="sxs-lookup"><span data-stu-id="6be06-145">The following sections will setup your app to receive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="6be06-146">Настройка учетных данных для отправки push-уведомлений из Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="6be06-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="6be06-147">Чтобы разрешить Службам мобильного взаимодействия отправлять push-уведомления от вашего имени, необходимо предоставить им доступ к сертификату Apple iOS или ключу API сервера GCM.</span><span class="sxs-lookup"><span data-stu-id="6be06-147">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="6be06-148">Перейдите на портал Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="6be06-148">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="6be06-149">Убедитесь, что у вас открыто приложение, используемое для этого проекта, и нажмите кнопку **Использовать** внизу.</span><span class="sxs-lookup"><span data-stu-id="6be06-149">Ensure you're in the app we're using for this project and then click on the **Engage** button at the bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="6be06-150">Вы перейдете на страницу "Параметры" на портале Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6be06-150">You will land in the settings page in your Engagement Portal.</span></span> <span data-ttu-id="6be06-151">Здесь выберите раздел **Собственные push-уведомления** .</span><span class="sxs-lookup"><span data-stu-id="6be06-151">From there click on the **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="6be06-152">Настройте сертификат Apple iOS или ключ API сервера GCM.</span><span class="sxs-lookup"><span data-stu-id="6be06-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="6be06-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="6be06-153">**[iOS]**</span></span>
   
    <span data-ttu-id="6be06-154">а.</span><span class="sxs-lookup"><span data-stu-id="6be06-154">a.</span></span> <span data-ttu-id="6be06-155">Выберите сертификат P12, загрузите его и введите пароль:</span><span class="sxs-lookup"><span data-stu-id="6be06-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="6be06-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="6be06-156">**[Android]**</span></span>
   
    <span data-ttu-id="6be06-157">а.</span><span class="sxs-lookup"><span data-stu-id="6be06-157">a.</span></span> <span data-ttu-id="6be06-158">Выберите значок редактирования перед **ключом API** в разделе параметров GCM, а затем в открывшемся всплывающем окне вставьте ключ сервера GCM и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6be06-158">Click the edit icon in front of **API Key** in the GCM Settings section and in the popup which shows up, paste the GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-the-cordova-app"></a><span data-ttu-id="6be06-159">Включение push-уведомлений в приложении Cordova</span><span class="sxs-lookup"><span data-stu-id="6be06-159">Enable push notifications in the Cordova app</span></span>
<span data-ttu-id="6be06-160">Добавьте в файл **www/js/index.js** вызов Служб мобильного взаимодействия для запроса push-уведомлений и объявления обработчика.</span><span class="sxs-lookup"><span data-stu-id="6be06-160">Edit **www/js/index.js** to add the call to Mobile Engagement to request push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-the-app"></a><span data-ttu-id="6be06-161">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="6be06-161">Run the app</span></span>
<span data-ttu-id="6be06-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="6be06-162">**[iOS]**</span></span>

1. <span data-ttu-id="6be06-163">При тестировании push-уведомлений для сборки и развертывания приложения на устройстве мы будем использовать XCode, поскольку iOS разрешает вывод push-уведомлений только на реальных устройствах.</span><span class="sxs-lookup"><span data-stu-id="6be06-163">We will use XCode to build and deploy the app on the device to test push notifications since iOS only allows push notifications to an actual device.</span></span> <span data-ttu-id="6be06-164">Перейдите в расположение, где создан проект Cordova, и откройте папку **...\platforms\ios**.</span><span class="sxs-lookup"><span data-stu-id="6be06-164">Go to the location where your Cordova project is created and navigate to **...\platforms\ios** location.</span></span> <span data-ttu-id="6be06-165">Откройте XCODEPROJ-файл в XCode.</span><span class="sxs-lookup"><span data-stu-id="6be06-165">Open up the native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="6be06-166">Скомпилируйте и разверните приложение Cordova на устройстве iOS, используя учетную запись с профилем подготовки, содержащим сертификат, который вы только что загрузили на портал Служб мобильного взаимодействия, и идентификатором приложения, введенным при создании приложения Cordova.</span><span class="sxs-lookup"><span data-stu-id="6be06-166">Build and deploy the Cordova app to the iOS device using the account which has the provisioning profile containing the certificate you just uploaded to the Mobile Engagement portal and the App Id which matches the one you provided while creating the Cordova app.</span></span> <span data-ttu-id="6be06-167">Вы можете проверить значение *идентификатора набора* в файле **Resources\*-info.plist** в XCode.</span><span class="sxs-lookup"><span data-stu-id="6be06-167">You can check out the *Bundle identifier* in your **Resources\*-info.plist** file in XCode to match it up.</span></span> 
3. <span data-ttu-id="6be06-168">На устройстве iOS появится стандартное всплывающее окно с уведомлением о том, что приложение запрашивает разрешение на отправку уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6be06-168">You will see the standard iOS popup on your device saying that the app requests permission to send notifications.</span></span> <span data-ttu-id="6be06-169">Предоставьте это разрешение.</span><span class="sxs-lookup"><span data-stu-id="6be06-169">Grant the permission.</span></span> 

<span data-ttu-id="6be06-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="6be06-170">**[Android]**</span></span>

<span data-ttu-id="6be06-171">Для запуска приложения на Android можно просто использовать эмулятор Android, так как он поддерживает уведомления GCM.</span><span class="sxs-lookup"><span data-stu-id="6be06-171">You can simply use the emulator to run the Android app as GCM notifications are supported on the Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="6be06-172"><a id="send"></a>Отправка уведомления в приложение</span><span class="sxs-lookup"><span data-stu-id="6be06-172"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="6be06-173">Теперь мы создадим простую кампанию push-уведомлений, которая будет отправлять push-уведомления в приложение, запущенное на устройстве.</span><span class="sxs-lookup"><span data-stu-id="6be06-173">We will now create a simple Push Notification campaign that will send a push to your app running on the device:</span></span>

1. <span data-ttu-id="6be06-174">Перейдите на вкладку **Reach** на портале Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="6be06-174">Navigate to the **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="6be06-175">Щелкните **Создать объявление** , чтобы создать кампанию push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6be06-175">Click **New Announcement** to create your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="6be06-176">Введите данные для новой кампании **[Android]**</span><span class="sxs-lookup"><span data-stu-id="6be06-176">Provide inputs to create your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="6be06-177">Задайте **имя** кампании.</span><span class="sxs-lookup"><span data-stu-id="6be06-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="6be06-178">Для параметра **Тип доставки** выберите значение *Системное уведомление* *Простое*.</span><span class="sxs-lookup"><span data-stu-id="6be06-178">Select the **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="6be06-179">Для параметра **Время доставки** выберите значение *Любое время*</span><span class="sxs-lookup"><span data-stu-id="6be06-179">Select the **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="6be06-180">Укажите **название** уведомления, которое будет отображаться в первой строке push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="6be06-180">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="6be06-181">Укажите **сообщение** для уведомления, которое будет использоваться в качестве текста сообщения.</span><span class="sxs-lookup"><span data-stu-id="6be06-181">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="6be06-182">Введите данные для новой кампании **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="6be06-182">Provide inputs to create your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="6be06-183">Задайте **имя** кампании.</span><span class="sxs-lookup"><span data-stu-id="6be06-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="6be06-184">Для параметра **Время доставки** выберите значение *Только вне приложения*</span><span class="sxs-lookup"><span data-stu-id="6be06-184">Select the **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="6be06-185">Укажите **название** уведомления, которое будет отображаться в первой строке push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="6be06-185">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="6be06-186">Укажите **сообщение** для уведомления, которое будет использоваться в качестве текста сообщения.</span><span class="sxs-lookup"><span data-stu-id="6be06-186">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="6be06-187">Прокрутите окно вниз и в разделе содержимого выберите пункт **Только уведомления**</span><span class="sxs-lookup"><span data-stu-id="6be06-187">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="6be06-188">[Необязательно] Можно также указать URL-адрес действия.</span><span class="sxs-lookup"><span data-stu-id="6be06-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="6be06-189">Нужно использовать ту же схему URL-адресов, что и для переменной **AZME\_REDIRECT\_URL** подключаемого модуля, например *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="6be06-189">Make sure that it uses a URL scheme provided while configuring the plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="6be06-190">Вы настроили простейшую базовую кампанию.</span><span class="sxs-lookup"><span data-stu-id="6be06-190">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="6be06-191">Еще раз прокрутите окно вниз и нажмите кнопку **Создать** , чтобы сохранить кампанию.</span><span class="sxs-lookup"><span data-stu-id="6be06-191">Now scroll down again and click the **Create** button to save your campaign.</span></span>
8. <span data-ttu-id="6be06-192">И, наконец, **активируйте** кампанию.</span><span class="sxs-lookup"><span data-stu-id="6be06-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="6be06-193">Теперь push-уведомления в рамках этой кампании будут отображаться на устройстве или в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="6be06-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="6be06-194"><a id="next-steps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6be06-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="6be06-195">Обзор методов, доступных в пакете Cordova SDK для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="6be06-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

