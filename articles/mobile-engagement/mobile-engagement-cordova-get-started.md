---
title: "aaaGet работы с Azure Mobile Engagement для Cordova/Phonegap"
description: "Узнайте, как toouse Azure Mobile Engagement Analytics и Push-уведомления для приложений Cordova/Phonegap."
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
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="3581f-103">Начало работы со Службами мобильного взаимодействия Azure для Cordova (Phonegap)</span><span class="sxs-lookup"><span data-stu-id="3581f-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="3581f-104">В этом разделе показано, как toounderstand toouse Azure Mobile Engagement, использования и отправить push уведомления toosegmented пользователям для мобильного приложения, разработанные с помощью Cordova.</span><span class="sxs-lookup"><span data-stu-id="3581f-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="3581f-105">В этом учебнике вы создадим пустое приложение Cordova на компьютере Mac и интегрируем пакет SDK для Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="3581f-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="3581f-106">Приложение будет собирать базовые данные аналитики и получать push-уведомления с помощью системы push-уведомлений Apple (APNS) для iOS и Google Cloud Messaging (GCM) для Android.</span><span class="sxs-lookup"><span data-stu-id="3581f-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="3581f-107">Мы Развернем этот tooan устройстве iOS или Android для тестирования.</span><span class="sxs-lookup"><span data-stu-id="3581f-107">We will deploy this tooan iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="3581f-108">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="3581f-108">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="3581f-109">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="3581f-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3581f-110">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span><span class="sxs-lookup"><span data-stu-id="3581f-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="3581f-111">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="3581f-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="3581f-112">XCode, которую можно установить в магазине приложений Mac (для развертывания tooiOS)</span><span class="sxs-lookup"><span data-stu-id="3581f-112">XCode, which you can install from Mac App Store (for deploying tooiOS)</span></span>
* <span data-ttu-id="3581f-113">[Android SDK & эмулятор](http://developer.android.com/sdk/installing/index.html) (для развертывания tooAndroid)</span><span class="sxs-lookup"><span data-stu-id="3581f-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying tooAndroid)</span></span>
* <span data-ttu-id="3581f-114">Сертификат push-уведомлений (P12), который можно получить в центре разработки Apple (для APNS)</span><span class="sxs-lookup"><span data-stu-id="3581f-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="3581f-115">Номер проекта GCM, который можно найти в консоли разработчиков Google (для GCM)</span><span class="sxs-lookup"><span data-stu-id="3581f-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="3581f-116">Подключаемый модуль Cordova для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="3581f-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="3581f-117">Можно найти исходного кода hello и hello ReadMe для подключаемого модуля Cordova hello на [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="3581f-117">You can find hello source code and hello ReadMe for hello Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="3581f-118"><a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для приложения Cordova</span><span class="sxs-lookup"><span data-stu-id="3581f-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="3581f-119"><a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="3581f-119"><a id="connecting-app"></a>Connecting your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="3581f-120">В этом руководстве содержатся «базовой интеграции» hello минимальный набор данных требуется toocollect и отправить push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="3581f-120">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="3581f-121">Мы создадим простое приложение с интеграцией hello toodemonstrate Cordova:</span><span class="sxs-lookup"><span data-stu-id="3581f-121">We will create a basic app with Cordova toodemonstrate hello integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="3581f-122">Создание нового проекта Cordova</span><span class="sxs-lookup"><span data-stu-id="3581f-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="3581f-123">Запустите *терминалов* окна на ваш Mac компьютера и типа hello после которого будет создан новый проект Cordova с помощью шаблона по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="3581f-123">Launch *Terminal* window on your Mac machine and type hello following which will create a new Cordova project from hello default template.</span></span> <span data-ttu-id="3581f-124">Убедитесь, что публикация hello профиля вы со временем toodeploy используйте приложение iOS использует «com.mycompany.myapp» как hello идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="3581f-124">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using 'com.mycompany.myapp' as hello App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="3581f-125">Выполните следующие tooconfigure hello проекта для **iOS** и запустите его в симуляторе iOS hello:</span><span class="sxs-lookup"><span data-stu-id="3581f-125">Execute hello following tooconfigure your project for **iOS** and run it in hello iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="3581f-126">Выполните следующие tooconfigure hello проекта для **Android** и запустите его в эмуляторе Android hello.</span><span class="sxs-lookup"><span data-stu-id="3581f-126">Execute hello following tooconfigure your project for **Android** and run it in hello Android emulator.</span></span> <span data-ttu-id="3581f-127">Убедитесь, что параметры эмулятора Android SDK своей цели как Google API-интерфейсы (Google Inc.) с ЦП hello / ABI как Google API-интерфейсы ARM.</span><span class="sxs-lookup"><span data-stu-id="3581f-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with hello CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="3581f-128">Добавьте подключаемый модуль Cordova Console hello.</span><span class="sxs-lookup"><span data-stu-id="3581f-128">Add hello Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="3581f-129">Подключение Engagement tooMobile внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="3581f-129">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="3581f-130">Установите подключаемый модуль Azure Mobile Engagement Cordova hello в то же время предоставляя значения переменных tooconfigure hello hello-подключаемого модуля:</span><span class="sxs-lookup"><span data-stu-id="3581f-130">Install hello Azure Mobile Engagement Cordova plugin while providing hello variable values tooconfigure hello plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="3581f-131">*Значок Android достичь* : должно быть именем hello hello ресурса не все расширения, а также drawable префикс (ex: mynotificationicon), и файл значка hello должны быть скопированы в проекте android (платформы/android/res/drawable)</span><span class="sxs-lookup"><span data-stu-id="3581f-131">*Android Reach Icon* : must be hello name of hello resource without any extension, nor drawable prefix (ex: mynotificationicon), and hello icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="3581f-132">*iOS достичь значок* : должно быть именем hello hello ресурсов без расширения (пример: mynotificationicon.png), и файл значка hello должен быть добавлен в проект iOS с XCode (с помощью меню Добавить файлы hello)</span><span class="sxs-lookup"><span data-stu-id="3581f-132">*iOS Reach Icon*  : must be hello name of hello resource with its extension (ex:  mynotificationicon.png), and hello icon file must be added into your iOS project with XCode (using hello Add Files Menu)</span></span>

## <span data-ttu-id="3581f-133"><a id="monitor"></a>Включение мониторинга в реальном времени</span><span class="sxs-lookup"><span data-stu-id="3581f-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="3581f-134">В проект Cordova hello — изменить **www/js/index.js** toodeclare Engagement tooMobile нового действия один раз hello вызовов hello tooadd *deviceReady* полученных событий.</span><span class="sxs-lookup"><span data-stu-id="3581f-134">In hello Cordova project - edit **www/js/index.js** tooadd hello call tooMobile Engagement toodeclare a new activity once hello *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="3581f-135">Запустите приложение hello:</span><span class="sxs-lookup"><span data-stu-id="3581f-135">Run hello application:</span></span>
   
   * <span data-ttu-id="3581f-136">**Для iOS:**</span><span class="sxs-lookup"><span data-stu-id="3581f-136">**For iOS**</span></span>
     
       <span data-ttu-id="3581f-137">В `Terminal` окна запуска приложения в новом экземпляре симулятора, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="3581f-137">In `Terminal` window launch your app in a new Simulator instance by executing hello following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="3581f-138">**Для Android:**</span><span class="sxs-lookup"><span data-stu-id="3581f-138">**For Android**</span></span>
     
       <span data-ttu-id="3581f-139">В `Terminal` окна запуска приложения в новом экземпляре эмулятора, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="3581f-139">In `Terminal` window launch your app in a new emulator instance by executing hello following:</span></span>
     
           cordova run android
3. <span data-ttu-id="3581f-140">Вы можете увидеть следующее hello в журналах hello консоли:</span><span class="sxs-lookup"><span data-stu-id="3581f-140">You can see hello following in hello console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="3581f-141"><a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="3581f-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="3581f-142"><a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="3581f-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="3581f-143">Mobile Engagement позволяет toointeract с пользователями с помощью Push-уведомления и сообщения в контексте hello кампаний в приложения.</span><span class="sxs-lookup"><span data-stu-id="3581f-143">Mobile Engagement allows you toointeract with your users using Push Notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="3581f-144">Этот модуль вызывается REACH на портале мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="3581f-144">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="3581f-145">Hello ниже настроит вашего приложения tooreceive их.</span><span class="sxs-lookup"><span data-stu-id="3581f-145">hello following sections will setup your app tooreceive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="3581f-146">Настройка учетных данных для отправки push-уведомлений из Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="3581f-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="3581f-147">tooallow мобильного охвата toosend Push-уведомления от вашего имени, необходимо его доступ к tooyour Apple iOS сертификат или ключ API GCM сервера toogrant.</span><span class="sxs-lookup"><span data-stu-id="3581f-147">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="3581f-148">Перейдите tooyour порталу мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="3581f-148">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="3581f-149">Убедитесь в приложение hello мы используем для этого проекта и выберите команду hello **Владейте** кнопку в нижней части hello:</span><span class="sxs-lookup"><span data-stu-id="3581f-149">Ensure you're in hello app we're using for this project and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="3581f-150">На странице параметров hello будут перемещаться в портал обязательств.</span><span class="sxs-lookup"><span data-stu-id="3581f-150">You will land in hello settings page in your Engagement Portal.</span></span> <span data-ttu-id="3581f-151">Из отсутствует щелкните hello **системные Push-уведомления** раздела:</span><span class="sxs-lookup"><span data-stu-id="3581f-151">From there click on hello **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="3581f-152">Настройте сертификат Apple iOS или ключ API сервера GCM.</span><span class="sxs-lookup"><span data-stu-id="3581f-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="3581f-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="3581f-153">**[iOS]**</span></span>
   
    <span data-ttu-id="3581f-154">а.</span><span class="sxs-lookup"><span data-stu-id="3581f-154">a.</span></span> <span data-ttu-id="3581f-155">Выберите сертификат P12, загрузите его и введите пароль:</span><span class="sxs-lookup"><span data-stu-id="3581f-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="3581f-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="3581f-156">**[Android]**</span></span>
   
    <span data-ttu-id="3581f-157">а.</span><span class="sxs-lookup"><span data-stu-id="3581f-157">a.</span></span> <span data-ttu-id="3581f-158">Щелкните значок редактирования hello перед **ключ API** в раздел параметров GCM hello во всплывающем hello, который отображается, hello GCM ключа сервера и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3581f-158">Click hello edit icon in front of **API Key** in hello GCM Settings section and in hello popup which shows up, paste hello GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a><span data-ttu-id="3581f-159">Включить push-уведомления в приложение Cordova hello</span><span class="sxs-lookup"><span data-stu-id="3581f-159">Enable push notifications in hello Cordova app</span></span>
<span data-ttu-id="3581f-160">Изменить **www/js/index.js** tooadd hello вызовов tooMobile Engagement toorequest push-уведомления и объявить обработчик:</span><span class="sxs-lookup"><span data-stu-id="3581f-160">Edit **www/js/index.js** tooadd hello call tooMobile Engagement toorequest push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a><span data-ttu-id="3581f-161">Выполните приложение hello</span><span class="sxs-lookup"><span data-stu-id="3581f-161">Run hello app</span></span>
<span data-ttu-id="3581f-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="3581f-162">**[iOS]**</span></span>

1. <span data-ttu-id="3581f-163">Мы будет использовать XCode toobuild и развернуть приложение hello на устройстве tootest hello push-уведомлений, поскольку iOS только позволяет принудительные уведомления tooan само устройство.</span><span class="sxs-lookup"><span data-stu-id="3581f-163">We will use XCode toobuild and deploy hello app on hello device tootest push notifications since iOS only allows push notifications tooan actual device.</span></span> <span data-ttu-id="3581f-164">Go toohello расположение, где создается проекта Cordova и перейдите в слишком**...\platforms\ios** расположение.</span><span class="sxs-lookup"><span data-stu-id="3581f-164">Go toohello location where your Cordova project is created and navigate too**...\platforms\ios** location.</span></span> <span data-ttu-id="3581f-165">Откройте hello собственного xcodeproj-файл в XCode.</span><span class="sxs-lookup"><span data-stu-id="3581f-165">Open up hello native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="3581f-166">Построение и развертывание hello Cordova приложения toohello устройствами iOS hello учетную запись, имеющую hello подготовительный профиль, содержащий только что переданный порталу мобильного охвата toohello и hello идентификатор приложения, который соответствует hello, который был предоставлен при создании сертификатов hello приложение Hello Cordova.</span><span class="sxs-lookup"><span data-stu-id="3581f-166">Build and deploy hello Cordova app toohello iOS device using hello account which has hello provisioning profile containing hello certificate you just uploaded toohello Mobile Engagement portal and hello App Id which matches hello one you provided while creating hello Cordova app.</span></span> <span data-ttu-id="3581f-167">Можно извлечь hello *идентификатор пакета* в ваш **ресурсов\*-info.plist** файл в XCode toomatch ее вверх.</span><span class="sxs-lookup"><span data-stu-id="3581f-167">You can check out hello *Bundle identifier* in your **Resources\*-info.plist** file in XCode toomatch it up.</span></span> 
3. <span data-ttu-id="3581f-168">Вы увидите всплывающее hello стандартных операций ввода-вывода на устройстве, о том, что приложение hello запросов на разрешение toosend уведомления.</span><span class="sxs-lookup"><span data-stu-id="3581f-168">You will see hello standard iOS popup on your device saying that hello app requests permission toosend notifications.</span></span> <span data-ttu-id="3581f-169">Разрешение "hello".</span><span class="sxs-lookup"><span data-stu-id="3581f-169">Grant hello permission.</span></span> 

<span data-ttu-id="3581f-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="3581f-170">**[Android]**</span></span>

<span data-ttu-id="3581f-171">Можно просто использовать Android приложение hello toorun hello эмулятора, как уведомления GCM, поддерживаются в эмуляторе Android hello.</span><span class="sxs-lookup"><span data-stu-id="3581f-171">You can simply use hello emulator toorun hello Android app as GCM notifications are supported on hello Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="3581f-172"><a id="send"></a>Отправить уведомление о tooyour приложение</span><span class="sxs-lookup"><span data-stu-id="3581f-172"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="3581f-173">Теперь мы создадим простой кампании Push-уведомлений, будет отправить приложение tooyour push, запущенного на устройстве hello:</span><span class="sxs-lookup"><span data-stu-id="3581f-173">We will now create a simple Push Notification campaign that will send a push tooyour app running on hello device:</span></span>

1. <span data-ttu-id="3581f-174">Перейдите toohello **достичь** вкладка на портале мобильного охвата</span><span class="sxs-lookup"><span data-stu-id="3581f-174">Navigate toohello **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="3581f-175">Нажмите кнопку **новое извещение** toocreate кампании push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="3581f-175">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="3581f-176">Предоставить входные данные toocreate кампанию **[Android]**</span><span class="sxs-lookup"><span data-stu-id="3581f-176">Provide inputs toocreate your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="3581f-177">Задайте **имя** кампании.</span><span class="sxs-lookup"><span data-stu-id="3581f-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="3581f-178">Выберите hello **тип доставки** как *Системное уведомление* *простой*</span><span class="sxs-lookup"><span data-stu-id="3581f-178">Select hello **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="3581f-179">Выберите hello **время доставки** как *«Any времени»*</span><span class="sxs-lookup"><span data-stu-id="3581f-179">Select hello **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="3581f-180">Укажите **заголовок** для уведомления будет первая строка hello в отправке hello.</span><span class="sxs-lookup"><span data-stu-id="3581f-180">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="3581f-181">Укажите **сообщение** для вашей уведомление, которое будет использоваться в качестве текста сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="3581f-181">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="3581f-182">Предоставить входные данные toocreate кампанию **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="3581f-182">Provide inputs toocreate your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="3581f-183">Задайте **имя** кампании.</span><span class="sxs-lookup"><span data-stu-id="3581f-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="3581f-184">Выберите hello **время доставки** как *«только вне приложения»*</span><span class="sxs-lookup"><span data-stu-id="3581f-184">Select hello **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="3581f-185">Укажите **заголовок** для уведомления будет первая строка hello в отправке hello.</span><span class="sxs-lookup"><span data-stu-id="3581f-185">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="3581f-186">Укажите **сообщение** для вашей уведомление, которое будет использоваться в качестве текста сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="3581f-186">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="3581f-187">Прокрутите вниз и выберите раздел содержимого hello **только уведомления**</span><span class="sxs-lookup"><span data-stu-id="3581f-187">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="3581f-188">[Необязательно] Можно также указать URL-адрес действия.</span><span class="sxs-lookup"><span data-stu-id="3581f-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="3581f-189">Убедитесь, что используется схема URL-адрес, указанный при настройке подключаемого модуля hello **AZME\_ПЕРЕНАПРАВЛЕНИЯ\_URL-адрес** переменной например *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="3581f-189">Make sure that it uses a URL scheme provided while configuring hello plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="3581f-190">Возможные основные кампании параметр hello, процедура завершена.</span><span class="sxs-lookup"><span data-stu-id="3581f-190">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="3581f-191">Теперь прокрутите список вниз и нажмите hello **создать** кнопку toosave кампанию.</span><span class="sxs-lookup"><span data-stu-id="3581f-191">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
8. <span data-ttu-id="3581f-192">И, наконец, **активируйте** кампанию.</span><span class="sxs-lookup"><span data-stu-id="3581f-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="3581f-193">Теперь push-уведомления в рамках этой кампании будут отображаться на устройстве или в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="3581f-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="3581f-194"><a id="next-steps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3581f-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="3581f-195">Обзор методов, доступных в пакете Cordova SDK для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="3581f-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

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

