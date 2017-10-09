---
title: "tooApache aaaAdd Push-уведомлений приложения Cordova с помощью мобильных приложений Azure | Документы Microsoft"
description: "Узнайте, как toosend toouse мобильных приложений Azure push приложения Apache Cordova tooyour уведомления."
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a><span data-ttu-id="7765c-103">Добавление приложения Apache Cordova tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="7765c-103">Add push notifications tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="7765c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="7765c-104">Overview</span></span>
<span data-ttu-id="7765c-105">В этом учебнике добавлении проекта toohello [Apache Cordova краткого] принудительной уведомления, чтобы каждый раз при вставке записи push-уведомление отправляется toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="7765c-105">In this tutorial, you add push notifications toohello [Apache Cordova quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="7765c-106">Если вы не используете hello загружен быстрый запуск сервера проекта, требуется hello пакета расширения уведомлений push.</span><span class="sxs-lookup"><span data-stu-id="7765c-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="7765c-107">Дополнительные сведения см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure][1].</span><span class="sxs-lookup"><span data-stu-id="7765c-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="7765c-108"><a name="prerequisites"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7765c-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="7765c-109">В этом учебнике приложению Apache Cordova, разработанных с помощью Visual Studio 2015, который выполняется на hello эмулятор Android Google, устройство Android, устройства Windows и устройства iOS.</span><span class="sxs-lookup"><span data-stu-id="7765c-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on hello Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="7765c-110">toocomplete этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="7765c-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="7765c-111">ПК с [Visual Studio Community 2015][2] или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="7765c-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="7765c-112">[набор средств Visual Studio для Apache Cordova][4];</span><span class="sxs-lookup"><span data-stu-id="7765c-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="7765c-113">[активная учетная запись Azure][3];</span><span class="sxs-lookup"><span data-stu-id="7765c-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="7765c-114">завершенный [ознакомительный проект Apache Cordova][5];</span><span class="sxs-lookup"><span data-stu-id="7765c-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="7765c-115">для Android: [учетная запись Google][6] с подтвержденным адресом электронной почты;</span><span class="sxs-lookup"><span data-stu-id="7765c-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="7765c-116">для iOS: [участие в программе разработки решений для Apple][7] и устройство iOS (симулятор iOS не поддерживает push-уведомления);</span><span class="sxs-lookup"><span data-stu-id="7765c-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="7765c-117">для Windows: [учетная запись разработчика приложений для Магазина Windows][8] и устройство Windows 10.</span><span class="sxs-lookup"><span data-stu-id="7765c-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="7765c-118"><a name="configure-hub"></a>Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="7765c-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="7765c-119">[Просмотрите видео, в котором показаны действия, описанные в этом разделе.][9]</span><span class="sxs-lookup"><span data-stu-id="7765c-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-hello-server-project"></a><span data-ttu-id="7765c-120">Обновление проекта в project server hello</span><span class="sxs-lookup"><span data-stu-id="7765c-120">Update hello server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="7765c-121"><a name="add-push-to-app"></a>Изменение приложения Cordova</span><span class="sxs-lookup"><span data-stu-id="7765c-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="7765c-122">Убедитесь, что готовы toohandle push-уведомлений по установке подключаемого модуля Cordova принудительной hello, а также любые службы, специфический для платформы push проекта приложения Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="7765c-122">Ensure your Apache Cordova app project is ready toohandle push notifications by installing hello Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-hello-cordova-version-in-your-project"></a><span data-ttu-id="7765c-123">Обновите версию Cordova hello в своем проекте.</span><span class="sxs-lookup"><span data-stu-id="7765c-123">Update hello Cordova version in your project.</span></span>
<span data-ttu-id="7765c-124">Если проект использует версию Apache Cordova более ранних, чем v6.1.1, обновите hello клиентский проект.</span><span class="sxs-lookup"><span data-stu-id="7765c-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update hello client project.</span></span> <span data-ttu-id="7765c-125">проект hello tooupdate:</span><span class="sxs-lookup"><span data-stu-id="7765c-125">tooupdate hello project:</span></span>

* <span data-ttu-id="7765c-126">Щелкните правой кнопкой мыши `config.xml` конструктор конфигурации tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-126">Right-click `config.xml` tooopen hello configuration designer.</span></span>
* <span data-ttu-id="7765c-127">Перейдите на вкладку платформы hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-127">Select hello Platforms tab.</span></span>
* <span data-ttu-id="7765c-128">Выберите 6.1.1 в hello **Cordova CLI** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="7765c-128">Choose 6.1.1 in hello **Cordova CLI** text box.</span></span>
* <span data-ttu-id="7765c-129">Выберите **построения**, затем **построить решение** tooupdate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="7765c-129">Choose **Build**, then **Build Solution** tooupdate hello project.</span></span>

#### <a name="install-hello-push-plugin"></a><span data-ttu-id="7765c-130">Установите подключаемый модуль принудительной hello</span><span class="sxs-lookup"><span data-stu-id="7765c-130">Install hello push plugin</span></span>
<span data-ttu-id="7765c-131">Приложения Apache Cordova не обрабатывают возможностей устройства или сети изначально.</span><span class="sxs-lookup"><span data-stu-id="7765c-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="7765c-132">Эти возможности обеспечиваются подключаемыми модулями, которые публикуются в [npm][10] или на портале GitHub.</span><span class="sxs-lookup"><span data-stu-id="7765c-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="7765c-133">Hello `phonegap-plugin-push` подключаемый модуль — push-уведомлений используется toohandle сети.</span><span class="sxs-lookup"><span data-stu-id="7765c-133">hello `phonegap-plugin-push` plugin is used toohandle network push notifications.</span></span>

<span data-ttu-id="7765c-134">Подключаемый модуль принудительной hello можно установить одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="7765c-134">You can install hello push plugin in one of these ways:</span></span>

<span data-ttu-id="7765c-135">**Из hello командной строки:**</span><span class="sxs-lookup"><span data-stu-id="7765c-135">**From hello command-prompt:**</span></span>

<span data-ttu-id="7765c-136">Выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="7765c-136">Execute hello following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="7765c-137">**в Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="7765c-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="7765c-138">В обозревателе решений откройте hello `config.xml` файла щелкните **подключаемые модули** > **настраиваемый**выберите **Git** в качестве источника установки, затем введите `https://github.com/phonegap/phonegap-plugin-push`как источник hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-138">In Solution Explorer, open hello `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as hello source.</span></span>

   ![][img1]

2. <span data-ttu-id="7765c-139">Выберите источник установки Далее toohello hello стрелка.</span><span class="sxs-lookup"><span data-stu-id="7765c-139">Click hello arrow next toohello installation source.</span></span>
3. <span data-ttu-id="7765c-140">В **SENDER_ID**, если уже имеется код числовых проекта для проекта Google Developer Console hello, можно добавить его здесь.</span><span class="sxs-lookup"><span data-stu-id="7765c-140">In **SENDER_ID**, if you already have a numeric project ID for hello Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="7765c-141">В противном случае введите значение заполнителя, например 777777.</span><span class="sxs-lookup"><span data-stu-id="7765c-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="7765c-142">Если планируется использовать устройство Android, это значение можно позже обновить в файле config.xml.</span><span class="sxs-lookup"><span data-stu-id="7765c-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="7765c-143">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7765c-143">Click **Add**.</span></span>

<span data-ttu-id="7765c-144">установлен подключаемый модуль принудительной Hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-144">hello push plugin is now installed.</span></span>

#### <a name="install-hello-device-plugin"></a><span data-ttu-id="7765c-145">Установите подключаемый модуль hello устройства</span><span class="sxs-lookup"><span data-stu-id="7765c-145">Install hello device plugin</span></span>
<span data-ttu-id="7765c-146">Выполните hello же процедуру, используемую hello tooinstall push-подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="7765c-146">Follow hello same procedure you used tooinstall hello push plugin.</span></span>  <span data-ttu-id="7765c-147">Добавить подключаемый модуль hello устройство из списка подключаемых модулей hello Core (щелкните **подключаемые модули** > **Core** toofind его).</span><span class="sxs-lookup"><span data-stu-id="7765c-147">Add hello Device plugin from hello Core plugins list (click **Plugins** > **Core** toofind it).</span></span> <span data-ttu-id="7765c-148">Необходимо, чтобы это имя платформы hello tooobtain подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="7765c-148">You need this plugin tooobtain hello platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="7765c-149">Регистрация устройства при запуске приложения</span><span class="sxs-lookup"><span data-stu-id="7765c-149">Register your device on application start-up</span></span>
<span data-ttu-id="7765c-150">Сначала мы добавим минимальный требуемый код для Android.</span><span class="sxs-lookup"><span data-stu-id="7765c-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="7765c-151">Более поздней версии измените toorun приложения hello, iOS или Windows 10.</span><span class="sxs-lookup"><span data-stu-id="7765c-151">Later, modify hello app toorun on iOS or Windows 10.</span></span>

1. <span data-ttu-id="7765c-152">Добавьте вызов слишком**registerForPushNotifications** во время обратного вызова hello для процесса входа в систему hello или внизу hello hello **onDeviceReady** метод:</span><span class="sxs-lookup"><span data-stu-id="7765c-152">Add a call too**registerForPushNotifications** during hello callback for hello login process, or at hello bottom of  hello **onDeviceReady** method:</span></span>

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="7765c-153">В этом примере показан вызов метода **registerForPushNotifications** после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7765c-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="7765c-154">Метод `registerForPushNotifications()` можно вызывать каждый раз при необходимости.</span><span class="sxs-lookup"><span data-stu-id="7765c-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="7765c-155">Добавить новый hello **registerForPushNotifications** метод следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7765c-155">Add hello new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. <span data-ttu-id="7765c-156">(Android) В предыдущих кода hello, замените `Your_Project_ID` с числового hello project ID для приложения из [Google Developer Console][18].</span><span class="sxs-lookup"><span data-stu-id="7765c-156">(Android) In hello preceding code, replace `Your_Project_ID` with hello numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-hello-app-on-android"></a><span data-ttu-id="7765c-157">(Необязательно) Настройка и запуск приложения hello в Android</span><span class="sxs-lookup"><span data-stu-id="7765c-157">(Optional) Configure and run hello app on Android</span></span>
<span data-ttu-id="7765c-158">Выполните этот раздел tooenable push-уведомления для Android.</span><span class="sxs-lookup"><span data-stu-id="7765c-158">Complete this section tooenable push notifications for Android.</span></span>

#### <span data-ttu-id="7765c-159"><a name="enable-gcm"></a>Включение Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="7765c-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="7765c-160">Поскольку изначально мы ожидаем hello Google Android платформы, необходимо включить Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="7765c-160">Since we are targeting hello Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="7765c-161"><a name="configure-backend"></a>Настройка hello мобильное приложение серверной toosend принудительной запросы с помощью FCM</span><span class="sxs-lookup"><span data-stu-id="7765c-161"><a name="configure-backend"></a>Configure hello Mobile App backend toosend push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="7765c-162">Настройка приложения Cordova для Android</span><span class="sxs-lookup"><span data-stu-id="7765c-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="7765c-163">В приложении Cordova откройте файл config.xml и замените `Your_Project_ID` с числового hello project ID для приложения hello [Google Developer Console][18].</span><span class="sxs-lookup"><span data-stu-id="7765c-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with hello numeric project ID for your app from hello [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="7765c-164">Откройте index.js и обновите toouse кода hello свой идентификатор числовых проекта.</span><span class="sxs-lookup"><span data-stu-id="7765c-164">Open index.js and update hello code toouse your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="7765c-165"><a name="configure-device"></a>Настройка устройства Android для отладочного режима USB</span><span class="sxs-lookup"><span data-stu-id="7765c-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="7765c-166">Перед развертыванием вашего приложения tooyour устройства Android необходимо tooenable отладка по USB.</span><span class="sxs-lookup"><span data-stu-id="7765c-166">Before you can deploy your application tooyour Android Device, you need tooenable USB Debugging.</span></span>  <span data-ttu-id="7765c-167">На телефоне Android выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7765c-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="7765c-168">Go слишком**параметры** > **о телефоне**, затем коснитесь hello **номер построения** режим разработчика включен (около семь раз).</span><span class="sxs-lookup"><span data-stu-id="7765c-168">Go too**Settings** > **About phone**, then tap hello **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="7765c-169">В **параметры** > **параметров разработчика** включить **отладка по USB**, телефоне Android tooyour Компьютере разработки, подключитесь с помощью кабеля USB.</span><span class="sxs-lookup"><span data-stu-id="7765c-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  tooyour development PC with a USB Cable.</span></span>

<span data-ttu-id="7765c-170">Мы проверили этот способ, используя устройство Google Nexus 5X с Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="7765c-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="7765c-171">Однако hello методы являются общими для любой современной версии Android.</span><span class="sxs-lookup"><span data-stu-id="7765c-171">However, hello techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="7765c-172">Установка служб Google Play</span><span class="sxs-lookup"><span data-stu-id="7765c-172">Install Google Play Services</span></span>
<span data-ttu-id="7765c-173">Подключаемый модуль принудительной Hello зависит от Android службы Google Play для push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7765c-173">hello push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="7765c-174">В Visual Studio щелкните **средства** > **Android** > **диспетчер Android SDK Manager**, разверните hello **дополнения** папки и проверьте hello поле toomake каждого hello следующие пакеты SDK установлен.</span><span class="sxs-lookup"><span data-stu-id="7765c-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand hello **Extras** folder and  check hello box toomake sure that each of hello following SDKs is installed.</span></span>

   * <span data-ttu-id="7765c-175">Android 2.3 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7765c-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="7765c-176">Репозиторий Google версии 27 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="7765c-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="7765c-177">Службы Google Play 9.0.2 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="7765c-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="7765c-178">Нажмите кнопку **установки пакетов** и дождитесь toocomplete установки hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-178">Click **Install Packages** and wait for hello installation toocomplete.</span></span>

<span data-ttu-id="7765c-179">Hello текущего необходимых библиотек, перечислены в hello [phonegap-plugin принудительной установки документации][19].</span><span class="sxs-lookup"><span data-stu-id="7765c-179">hello current required libraries are listed in hello [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-hello-app-on-android"></a><span data-ttu-id="7765c-180">Тест push-уведомлений в приложения hello на Android</span><span class="sxs-lookup"><span data-stu-id="7765c-180">Test push notifications in hello app on Android</span></span>
<span data-ttu-id="7765c-181">Теперь можно hello тестового push-уведомлений, запустив приложение и вставки элементов в таблице TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-181">You can now test push notifications by running hello app and inserting items in hello TodoItem table.</span></span> <span data-ttu-id="7765c-182">Вы можете проверить hello одного устройства или из второго устройства, при условии, что вы используете hello же серверной части.</span><span class="sxs-lookup"><span data-stu-id="7765c-182">You can test from hello same device or from a second device, as long as you are using hello same backend.</span></span> <span data-ttu-id="7765c-183">Проверка приложения Cordova на платформе Android hello в одном из следующих способов hello:</span><span class="sxs-lookup"><span data-stu-id="7765c-183">Test your Cordova app on hello Android platform in one of hello following ways:</span></span>

* <span data-ttu-id="7765c-184">**На физическом устройстве:** присоединить компьютер разработки tooyour устройства Android с помощью кабеля USB.</span><span class="sxs-lookup"><span data-stu-id="7765c-184">**On a physical device:** Attach your Android device tooyour development computer with a USB cable.</span></span>  <span data-ttu-id="7765c-185">Вместо **Эмулятор Google Android** выберите **Устройство**.</span><span class="sxs-lookup"><span data-stu-id="7765c-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="7765c-186">Visual Studio развертывает устройства toohello приложения hello и затем запускает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-186">Visual Studio deploys hello application toohello device and then runs hello application.</span></span>  <span data-ttu-id="7765c-187">Затем вы можете взаимодействовать с hello приложения на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-187">You can then interact with hello application on hello device.</span></span>

  <span data-ttu-id="7765c-188">Усовершенствуйте интерфейс разработки.</span><span class="sxs-lookup"><span data-stu-id="7765c-188">Improve your development experience.</span></span>  <span data-ttu-id="7765c-189">В разработке приложения Android вам помогут приложения для демонстрации экрана, например [Mobizen][20].</span><span class="sxs-lookup"><span data-stu-id="7765c-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="7765c-190">Mobizen проектов веб-браузере tooa Android экрана на ПК.</span><span class="sxs-lookup"><span data-stu-id="7765c-190">Mobizen projects your Android screen tooa web browser on your PC.</span></span>

* <span data-ttu-id="7765c-191">**На эмуляторе Android.** Для запуска в эмуляторе необходимо выполнить дополнительную настройку.</span><span class="sxs-lookup"><span data-stu-id="7765c-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="7765c-192">Убедитесь, что вы развертываете tooa виртуального устройства, имеющий интерфейсы API Google задать в качестве цели hello, как показано в диспетчере hello виртуального устройства Android (AVD).</span><span class="sxs-lookup"><span data-stu-id="7765c-192">Make sure you are deploying tooa virtual device that has Google APIs set as hello target, as shown in hello Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="7765c-193">Если требуется более быстрое x86 toouse эмулятор, вы [Установка драйвера HAXM hello] [ 11] и настроить эмулятор toouse hello его.</span><span class="sxs-lookup"><span data-stu-id="7765c-193">If you want toouse a faster x86 emulator, you [install hello HAXM driver][11] and configure hello emulator toouse it.</span></span>

    <span data-ttu-id="7765c-194">Добавить устройство Android toohello учетной записи Google, щелкнув **приложения** > **параметры** > **добавьте учетную запись**, следуйте указаниям hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-194">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="7765c-195">Запустите приложение hello todolist как перед и вставить новый элемент todo.</span><span class="sxs-lookup"><span data-stu-id="7765c-195">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="7765c-196">На этот раз значок уведомления отображается в области уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-196">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="7765c-197">Вы можете открыть hello уведомления лоток tooview hello полный текст hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="7765c-197">You can open hello notification drawer tooview hello full text of hello notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="7765c-198">Настройка и запуск проекта в iOS (необязательно)</span><span class="sxs-lookup"><span data-stu-id="7765c-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="7765c-199">Этот раздел предназначен для запуска проекта Cordova hello на устройствах iOS.</span><span class="sxs-lookup"><span data-stu-id="7765c-199">This section is for running hello Cordova project on iOS devices.</span></span> <span data-ttu-id="7765c-200">Пропустите этот раздел, если вы не работаете с устройствами iOS.</span><span class="sxs-lookup"><span data-stu-id="7765c-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="7765c-201">Установки и выполнения hello iOS удаленный агент сборки Mac или облачные службы</span><span class="sxs-lookup"><span data-stu-id="7765c-201">Install and run hello iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="7765c-202">Перед запуском приложения Cordova в iOS с помощью Visual Studio перейдите hello шагов hello [руководстве по установке iOS] [ 12] tooinstall и выполнения hello удаленный агент сборки.</span><span class="sxs-lookup"><span data-stu-id="7765c-202">Before you can run a Cordova app on iOS using Visual Studio, go through hello steps in hello [iOS Setup Guide][12] tooinstall and run hello remote build agent.</span></span>

<span data-ttu-id="7765c-203">Убедитесь в том, что можно построить приложение hello для операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="7765c-203">Make sure you can build hello app for iOS.</span></span> <span data-ttu-id="7765c-204">Hello действия, описанные в руководстве по установке hello, требуется toobuild для iOS из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7765c-204">hello steps in hello setup guide are required toobuild for iOS from Visual Studio.</span></span> <span data-ttu-id="7765c-205">Если у вас компьютер Mac, вы можете создать для iOS с помощью hello удаленный агент сборки на службы, например MacInCloud.</span><span class="sxs-lookup"><span data-stu-id="7765c-205">If you do not have a Mac, you can build for iOS using hello remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="7765c-206">Дополнительные сведения см. в разделе [запуск приложения iOS в облаке hello][21].</span><span class="sxs-lookup"><span data-stu-id="7765c-206">For more info, see [Run your iOS app in hello cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="7765c-207">XCode 7 или более поздней — необходимые toouse подключаемого модуля принудительной hello в iOS.</span><span class="sxs-lookup"><span data-stu-id="7765c-207">XCode 7 or greater is required toouse hello push plugin on iOS.</span></span>

#### <a name="find-hello-id-toouse-as-your-app-id"></a><span data-ttu-id="7765c-208">Найти идентификатор toouse hello как ваш код приложения</span><span class="sxs-lookup"><span data-stu-id="7765c-208">Find hello ID toouse as your App ID</span></span>
<span data-ttu-id="7765c-209">Прежде чем регистрировать приложение для push-уведомлений, откройте файл config.xml в приложения Cordova, найти hello `id` атрибута значение в элементе hello мини-приложения и скопируйте его для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="7765c-209">Before you register your app for push notifications, open config.xml in your Cordova app, find hello `id` attribute value in hello widget element, and copy it for later use.</span></span> <span data-ttu-id="7765c-210">В следующий XML-код hello, является Идентификатором hello `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="7765c-210">In hello following XML, hello ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="7765c-211">Вам потребуется использовать этот идентификатор при создании идентификатора приложения на портале разработчика Apple.</span><span class="sxs-lookup"><span data-stu-id="7765c-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="7765c-212">При создании другой идентификатор приложения на портале для разработчиков hello далее в этом учебнике необходимо выполнить выполнить ряд дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="7765c-212">If you create a different App ID on hello developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="7765c-213">Идентификатор Hello в элементе мини-приложение, должен соответствовать hello идентификатор приложения на портале разработчика hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-213">hello ID in the widget element must match hello App ID on hello developer portal.</span></span>

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="7765c-214">Регистрация приложения hello push-уведомления на портале для разработчиков Apple</span><span class="sxs-lookup"><span data-stu-id="7765c-214">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="7765c-215">Видео, демонстрирующее аналогичные действия</span><span class="sxs-lookup"><span data-stu-id="7765c-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="7765c-216">Настройка Azure toosend push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="7765c-216">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="7765c-217">Проверка, соответствует ли идентификатор приложения указанному в приложении Cordova</span><span class="sxs-lookup"><span data-stu-id="7765c-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="7765c-218">Если вы уже создали в учетной записи разработчика Apple идентификатор приложения hello совпадает с Идентификатором hello hello элемента мини-приложения в файле config.xml, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="7765c-218">If hello App ID you created in your Apple Developer Account already matches hello ID of hello widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="7765c-219">Однако если идентификаторы hello не совпадают, потребоваться hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7765c-219">However, if hello IDs don't match, take hello following steps:</span></span>

1. <span data-ttu-id="7765c-220">Удалите папку hello платформы из проекта.</span><span class="sxs-lookup"><span data-stu-id="7765c-220">Delete hello platforms folder from your project.</span></span>
2. <span data-ttu-id="7765c-221">Удалите папку hello подключаемые модули из проекта.</span><span class="sxs-lookup"><span data-stu-id="7765c-221">Delete hello plugins folder from your project.</span></span>
3. <span data-ttu-id="7765c-222">Удалите папки node_modules hello из проекта.</span><span class="sxs-lookup"><span data-stu-id="7765c-222">Delete hello node_modules folder from your project.</span></span>
4. <span data-ttu-id="7765c-223">Обновите hello атрибута id элемента мини-приложение hello в файл config.xml toouse hello идентификатор приложения, который был создан в вашей учетной записи разработчика Apple.</span><span class="sxs-lookup"><span data-stu-id="7765c-223">Update hello id attribute of hello widget element in config.xml toouse hello App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="7765c-224">Перестройте свой проект.</span><span class="sxs-lookup"><span data-stu-id="7765c-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="7765c-225">Тестирование push-уведомлений в приложении iOS</span><span class="sxs-lookup"><span data-stu-id="7765c-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="7765c-226">Убедитесь, что в Visual Studio **iOS** выбран в качестве цели развертывания hello, а затем выберите **устройства** toorun на iOS, подключенном устройстве.</span><span class="sxs-lookup"><span data-stu-id="7765c-226">In Visual Studio, make sure that **iOS** is selected as hello deployment target, and then choose **Device** toorun on your connected iOS device.</span></span>

    <span data-ttu-id="7765c-227">Можно запускать на tooyour подключенное устройство iOS ПК с помощью iTunes.</span><span class="sxs-lookup"><span data-stu-id="7765c-227">You can run on an iOS device connected tooyour PC using iTunes.</span></span> <span data-ttu-id="7765c-228">Симулятор iOS Hello не поддерживает push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7765c-228">hello iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="7765c-229">Нажмите клавишу hello **запуска** кнопку или **F5** в Visual Studio toobuild проекта hello начала hello приложение на устройстве iOS, а затем нажмите **ОК** tooaccept push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7765c-229">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS  device, then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7765c-230">приложение Hello запрашивает подтверждение push-уведомления во время первого запуска hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-230">hello app requests confirmation for push notifications during hello first run.</span></span>

3. <span data-ttu-id="7765c-231">В приложение hello введите задачу и нажмите кнопку hello плюс (+) значок.</span><span class="sxs-lookup"><span data-stu-id="7765c-231">In hello app, type a task, and then click hello plus (+) icon.</span></span>
4. <span data-ttu-id="7765c-232">Убедитесь, что принимается уведомления, затем нажмите кнопку ОК toodismiss hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="7765c-232">Verify that a notification is received, then click OK toodismiss hello notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="7765c-233">Настройка и запуск проекта в Windows (необязательно)</span><span class="sxs-lookup"><span data-stu-id="7765c-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="7765c-234">Этот раздел предназначен для запуска проекта приложения Apache Cordova hello на устройствах Windows 10 (подключаемый модуль принудительной PhoneGap hello поддерживается в Windows 10).</span><span class="sxs-lookup"><span data-stu-id="7765c-234">This section is for running hello Apache Cordova app project on Windows 10 devices (hello PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="7765c-235">Пропустите этот раздел, если вы не работаете с устройствами Windows.</span><span class="sxs-lookup"><span data-stu-id="7765c-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="7765c-236">Регистрация приложения Windows для получения push-уведомлений с помощью WNS</span><span class="sxs-lookup"><span data-stu-id="7765c-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="7765c-237">Параметры хранилища toouse hello в Visual Studio выберите цель Windows из списка платформ решения hello, как **Windows x64** или **Windows x86** (избежать **Windows AnyCPU** push-уведомления).</span><span class="sxs-lookup"><span data-stu-id="7765c-237">toouse hello Store options in Visual Studio, select a Windows target from hello Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="7765c-238">[Просмотрите видео, демонстрирующее аналогичные действия][13]</span><span class="sxs-lookup"><span data-stu-id="7765c-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="7765c-239">Настройка концентратора уведомления hello для WNS</span><span class="sxs-lookup"><span data-stu-id="7765c-239">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a><span data-ttu-id="7765c-240">Настройка вашего Cordova приложения toosupport push-уведомления Windows</span><span class="sxs-lookup"><span data-stu-id="7765c-240">Configure your Cordova app toosupport Windows push notifications</span></span>
<span data-ttu-id="7765c-241">Привет открыть конструктор конфигурации (правой кнопкой мыши файл config.xml и выберите **конструктор представлений**) выберите hello **Windows** и кнопку **Windows 10** под **Windows целевой версии**.</span><span class="sxs-lookup"><span data-stu-id="7765c-241">Open hello configuration designer (right-click on config.xml and select **View Designer**), select hello **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="7765c-242">Строит toosupport push-уведомлений в используемом по умолчанию (Отладка), откройте build.json файл.</span><span class="sxs-lookup"><span data-stu-id="7765c-242">toosupport push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="7765c-243">Скопируйте конфигурацию «выпуск» tooyour конфигурации отладки.</span><span class="sxs-lookup"><span data-stu-id="7765c-243">Copy the "release" configuration tooyour debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="7765c-244">После обновления hello hello build.json должна содержать hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="7765c-244">After hello update, hello build.json should contain hello following code:</span></span>

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="7765c-245">Постройте приложение hello и проверьте наличие ошибок.</span><span class="sxs-lookup"><span data-stu-id="7765c-245">Build hello app and verify that you have no errors.</span></span> <span data-ttu-id="7765c-246">Клиентское приложение теперь необходимо зарегистрировать для получения уведомлений hello из внутреннего сервера мобильного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-246">Your client app should now register for hello notifications from hello Mobile App backend.</span></span> <span data-ttu-id="7765c-247">Повторите действия из этого раздела для каждого проекта Windows, входящего в ваше решение.</span><span class="sxs-lookup"><span data-stu-id="7765c-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="7765c-248">Тестирование push-уведомлений в приложении Windows</span><span class="sxs-lookup"><span data-stu-id="7765c-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="7765c-249">В Visual Studio, убедитесь, что платформа Windows выбран в качестве целевого объекта развертывания hello, таких как **Windows x64** или **Windows x86**.</span><span class="sxs-lookup"><span data-stu-id="7765c-249">In Visual Studio, make sure that a Windows platform is selected as hello deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="7765c-250">Выберите приложение hello toorun на ПК Windows 10, размещения Visual Studio **локального компьютера**.</span><span class="sxs-lookup"><span data-stu-id="7765c-250">toorun hello app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="7765c-251">Нажмите клавишу hello запустите кнопка toobuild hello проект и запустить приложение hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-251">Press hello Run button toobuild hello project and start hello app.</span></span>

<span data-ttu-id="7765c-252">В приложение hello, введите имя для нового todoitem и нажмите кнопку hello плюс (+) значок tooadd его.</span><span class="sxs-lookup"><span data-stu-id="7765c-252">In hello app, type a name for a new todoitem, and then click hello plus (+) icon tooadd it.</span></span>

<span data-ttu-id="7765c-253">Проверка получения уведомления при добавлении элемента hello.</span><span class="sxs-lookup"><span data-stu-id="7765c-253">Verify that a notification is received when hello item is added.</span></span>

## <span data-ttu-id="7765c-254"><a name="next-steps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7765c-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="7765c-255">Узнайте, как [концентраторы уведомлений] [ 17] toolearn о push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7765c-255">Read about [Notification Hubs][17] toolearn about push notifications.</span></span>
* <span data-ttu-id="7765c-256">Если вы еще не сделали продолжить работу с учебником hello, [Добавление Authentication] [ 14] tooyour приложения Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="7765c-256">If you have not already done so, continue hello tutorial by [Adding Authentication][14] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="7765c-257">Узнайте, как toouse hello пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="7765c-257">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="7765c-258">[Использование клиентской библиотеки Apache Cordova для мобильных приложений Azure][15]</span><span class="sxs-lookup"><span data-stu-id="7765c-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="7765c-259">[Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure][1]</span><span class="sxs-lookup"><span data-stu-id="7765c-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="7765c-260">[Использование пакета SDK Node.js для мобильных приложений Azure][16]</span><span class="sxs-lookup"><span data-stu-id="7765c-260">[Node.js Server SDK][16]</span></span>

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
