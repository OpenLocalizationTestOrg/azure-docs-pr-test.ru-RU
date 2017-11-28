---
title: "Добавление push-уведомлений в приложение Apache Cordova с помощью мобильных приложений Azure | Документация Майкрософт"
description: "Узнайте, как использовать мобильные приложения Azure для отправки push-уведомлений в приложение Apache Cordova."
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
ms.openlocfilehash: dc3cab0a6a8b4a56ab0fba1a02e5bba9d0ed1b1f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-apache-cordova-app"></a><span data-ttu-id="f039f-103">Добавление push-уведомлений в приложение Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="f039f-103">Add push notifications to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="f039f-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f039f-104">Overview</span></span>
<span data-ttu-id="f039f-105">В этом руководстве описывается добавление push-уведомлений в [ознакомительный проект Apache Cordova], чтобы при вставке каждой новой записи отправлялось push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="f039f-105">In this tutorial, you add push notifications to the [Apache Cordova quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="f039f-106">Если вы не используете скачанный проект сервера, необходимо добавить пакет расширений для push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f039f-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="f039f-107">Дополнительные сведения см. в статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure][1].</span><span class="sxs-lookup"><span data-stu-id="f039f-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="f039f-108"><a name="prerequisites"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f039f-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="f039f-109">В этом руководстве используется приложение Apache Cordova, разработанное в Visual Studio 2015 и выполняемое в эмуляторе Google Android, а также устройства Android, Windows и iOS.</span><span class="sxs-lookup"><span data-stu-id="f039f-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on the Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="f039f-110">Для работы с этим учебником необходимы указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="f039f-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="f039f-111">ПК с [Visual Studio Community 2015][2] или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="f039f-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="f039f-112">[набор средств Visual Studio для Apache Cordova][4];</span><span class="sxs-lookup"><span data-stu-id="f039f-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="f039f-113">[активная учетная запись Azure][3];</span><span class="sxs-lookup"><span data-stu-id="f039f-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="f039f-114">завершенный [ознакомительный проект Apache Cordova][5];</span><span class="sxs-lookup"><span data-stu-id="f039f-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="f039f-115">для Android: [учетная запись Google][6] с подтвержденным адресом электронной почты;</span><span class="sxs-lookup"><span data-stu-id="f039f-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="f039f-116">для iOS: [участие в программе разработки решений для Apple][7] и устройство iOS (симулятор iOS не поддерживает push-уведомления);</span><span class="sxs-lookup"><span data-stu-id="f039f-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="f039f-117">для Windows: [учетная запись разработчика приложений для Магазина Windows][8] и устройство Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f039f-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="f039f-118"><a name="configure-hub"></a>Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="f039f-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="f039f-119">[Просмотрите видео, в котором показаны действия, описанные в этом разделе.][9]</span><span class="sxs-lookup"><span data-stu-id="f039f-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-the-server-project"></a><span data-ttu-id="f039f-120">Обновление серверного проекта</span><span class="sxs-lookup"><span data-stu-id="f039f-120">Update the server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="f039f-121"><a name="add-push-to-app"></a>Изменение приложения Cordova</span><span class="sxs-lookup"><span data-stu-id="f039f-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="f039f-122">Убедитесь, что проект приложения Apache Cordova готов для обработки push-уведомлений. Для этого установите подключаемый модуль push-уведомлений Cordova, а также все службы push-уведомлений для конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="f039f-122">Ensure your Apache Cordova app project is ready to handle push notifications by installing the Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-the-cordova-version-in-your-project"></a><span data-ttu-id="f039f-123">Обновление версии Cordova в проекте</span><span class="sxs-lookup"><span data-stu-id="f039f-123">Update the Cordova version in your project.</span></span>
<span data-ttu-id="f039f-124">Если в проекте используется более ранняя версия Apache Cordova, чем 6.1.1, обновите клиентский проект.</span><span class="sxs-lookup"><span data-stu-id="f039f-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update the client project.</span></span> <span data-ttu-id="f039f-125">Чтобы обновить проект, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f039f-125">To update the project:</span></span>

* <span data-ttu-id="f039f-126">Щелкните правой кнопкой мыши файл `config.xml`, чтобы открыть конструктор конфигураций.</span><span class="sxs-lookup"><span data-stu-id="f039f-126">Right-click `config.xml` to open the configuration designer.</span></span>
* <span data-ttu-id="f039f-127">Перейдите на вкладку "Платформы".</span><span class="sxs-lookup"><span data-stu-id="f039f-127">Select the Platforms tab.</span></span>
* <span data-ttu-id="f039f-128">В текстовом поле **Cordova CLI** выберите 6.1.1.</span><span class="sxs-lookup"><span data-stu-id="f039f-128">Choose 6.1.1 in the **Cordova CLI** text box.</span></span>
* <span data-ttu-id="f039f-129">Чтобы обновить проект, выберите **Сборка**, а затем — **Собрать решение**.</span><span class="sxs-lookup"><span data-stu-id="f039f-129">Choose **Build**, then **Build Solution** to update the project.</span></span>

#### <a name="install-the-push-plugin"></a><span data-ttu-id="f039f-130">Установка подключаемого модуля push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="f039f-130">Install the push plugin</span></span>
<span data-ttu-id="f039f-131">Приложения Apache Cordova не обрабатывают возможностей устройства или сети изначально.</span><span class="sxs-lookup"><span data-stu-id="f039f-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="f039f-132">Эти возможности обеспечиваются подключаемыми модулями, которые публикуются в [npm][10] или на портале GitHub.</span><span class="sxs-lookup"><span data-stu-id="f039f-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="f039f-133">Подключаемый модуль `phonegap-plugin-push` используется для обработки push-уведомлений сети.</span><span class="sxs-lookup"><span data-stu-id="f039f-133">The `phonegap-plugin-push` plugin is used to handle network push notifications.</span></span>

<span data-ttu-id="f039f-134">Подключаемый модуль push-уведомлений можно установить одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="f039f-134">You can install the push plugin in one of these ways:</span></span>

<span data-ttu-id="f039f-135">**из командной строки:**</span><span class="sxs-lookup"><span data-stu-id="f039f-135">**From the command-prompt:**</span></span>

<span data-ttu-id="f039f-136">Выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f039f-136">Execute the following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="f039f-137">**в Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="f039f-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="f039f-138">В обозревателе решений откройте файл `config.xml`, щелкните **Подключаемые модули** > **Настраиваемые**, выберите **Git** как источник установки, а затем в качестве источника введите `https://github.com/phonegap/phonegap-plugin-push`.</span><span class="sxs-lookup"><span data-stu-id="f039f-138">In Solution Explorer, open the `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as the source.</span></span>

   ![][img1]

2. <span data-ttu-id="f039f-139">Щелкните стрелку рядом с источником установки.</span><span class="sxs-lookup"><span data-stu-id="f039f-139">Click the arrow next to the installation source.</span></span>
3. <span data-ttu-id="f039f-140">В поле **SENDER_ID** добавьте числовой идентификатор проекта Google Developer Console, если он уже есть.</span><span class="sxs-lookup"><span data-stu-id="f039f-140">In **SENDER_ID**, if you already have a numeric project ID for the Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="f039f-141">В противном случае введите значение заполнителя, например 777777.</span><span class="sxs-lookup"><span data-stu-id="f039f-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="f039f-142">Если планируется использовать устройство Android, это значение можно позже обновить в файле config.xml.</span><span class="sxs-lookup"><span data-stu-id="f039f-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="f039f-143">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f039f-143">Click **Add**.</span></span>

<span data-ttu-id="f039f-144">Теперь подключаемый модуль push-уведомлений установлен.</span><span class="sxs-lookup"><span data-stu-id="f039f-144">The push plugin is now installed.</span></span>

#### <a name="install-the-device-plugin"></a><span data-ttu-id="f039f-145">Установка подключаемого модуля устройства</span><span class="sxs-lookup"><span data-stu-id="f039f-145">Install the device plugin</span></span>
<span data-ttu-id="f039f-146">Выполните те же действия, что и для установки подключаемого модуля push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f039f-146">Follow the same procedure you used to install the push plugin.</span></span>  <span data-ttu-id="f039f-147">Добавьте подключаемый модуль устройства из списка основных подключаемых модулей (чтобы найти его, выберите **Подключаемые модули** > **Основные**).</span><span class="sxs-lookup"><span data-stu-id="f039f-147">Add the Device plugin from the Core plugins list (click **Plugins** > **Core** to find it).</span></span> <span data-ttu-id="f039f-148">Этот подключаемый модуль требуется, чтобы получить имя платформы.</span><span class="sxs-lookup"><span data-stu-id="f039f-148">You need this plugin to obtain the platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="f039f-149">Регистрация устройства при запуске приложения</span><span class="sxs-lookup"><span data-stu-id="f039f-149">Register your device on application start-up</span></span>
<span data-ttu-id="f039f-150">Сначала мы добавим минимальный требуемый код для Android.</span><span class="sxs-lookup"><span data-stu-id="f039f-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="f039f-151">Позднее мы внесем изменения в приложение для запуска в iOS или Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f039f-151">Later, modify the app to run on iOS or Windows 10.</span></span>

1. <span data-ttu-id="f039f-152">Добавьте вызов метода **registerForPushNotifications** в обратный вызов при входе в систему или в конец метода **onDeviceReady**.</span><span class="sxs-lookup"><span data-stu-id="f039f-152">Add a call to **registerForPushNotifications** during the callback for the login process, or at the bottom of  the **onDeviceReady** method:</span></span>

        // Login to the service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added to register for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="f039f-153">В этом примере показан вызов метода **registerForPushNotifications** после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f039f-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="f039f-154">Метод `registerForPushNotifications()` можно вызывать каждый раз при необходимости.</span><span class="sxs-lookup"><span data-stu-id="f039f-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="f039f-155">Добавьте новый метод **registerForPushNotifications** , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f039f-155">Add the new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle the registration event.
        pushRegistration.on('registration', function (data) {
          // Get the native platform of the device.
          var platform = device.platform;
          // Get the handle returned during registration.
          var handle = data.registrationId;
          // Set the device-specific message template.
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
3. <span data-ttu-id="f039f-156">Для Android: в приведенном выше коде замените значение `Your_Project_ID` числовым идентификатором проекта своего приложения, полученным на сайте [Google Developer Console][18].</span><span class="sxs-lookup"><span data-stu-id="f039f-156">(Android) In the preceding code, replace `Your_Project_ID` with the numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-the-app-on-android"></a><span data-ttu-id="f039f-157">Настройка и запуск приложения в Android (необязательно)</span><span class="sxs-lookup"><span data-stu-id="f039f-157">(Optional) Configure and run the app on Android</span></span>
<span data-ttu-id="f039f-158">В этом разделе описано, как включить поддержку push-уведомлений для платформы Android.</span><span class="sxs-lookup"><span data-stu-id="f039f-158">Complete this section to enable push notifications for Android.</span></span>

#### <span data-ttu-id="f039f-159"><a name="enable-gcm"></a>Включение Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="f039f-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="f039f-160">Так как изначально проект предназначен для платформы Google Android, необходимо включить Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="f039f-160">Since we are targeting the Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="f039f-161"><a name="configure-backend"></a>Настройка серверной части мобильного приложения для отправки push-запросов с использованием FCM</span><span class="sxs-lookup"><span data-stu-id="f039f-161"><a name="configure-backend"></a>Configure the Mobile App backend to send push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="f039f-162">Настройка приложения Cordova для Android</span><span class="sxs-lookup"><span data-stu-id="f039f-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="f039f-163">В приложении Cordova откройте файл config.xml и замените значение `Your_Project_ID` числовым идентификатором проекта своего приложения, полученным на сайте [Google Developer Console][18].</span><span class="sxs-lookup"><span data-stu-id="f039f-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with the numeric project ID for your app from the [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="f039f-164">Откройте файл index.js и добавьте в код числовой идентификатор своего проекта.</span><span class="sxs-lookup"><span data-stu-id="f039f-164">Open index.js and update the code to use your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="f039f-165"><a name="configure-device"></a>Настройка устройства Android для отладочного режима USB</span><span class="sxs-lookup"><span data-stu-id="f039f-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="f039f-166">Перед развертыванием приложения на устройстве Android необходимо включить отладку USB.</span><span class="sxs-lookup"><span data-stu-id="f039f-166">Before you can deploy your application to your Android Device, you need to enable USB Debugging.</span></span>  <span data-ttu-id="f039f-167">На телефоне Android выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f039f-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="f039f-168">Выберите элементы **Settings** > **About phone** (Параметры > О телефоне), коснитесь пункта **Build number** (Номер сборки) и дождитесь включения режима разработчика (примерно 7 секунд).</span><span class="sxs-lookup"><span data-stu-id="f039f-168">Go to **Settings** > **About phone**, then tap the **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="f039f-169">Вернитесь в раздел **Settings** > **Developer Options** (Параметры > Параметры разработчика), включите **отладочный режим USB**, а затем подключите телефон Android к компьютеру разработки с помощью USB-кабеля.</span><span class="sxs-lookup"><span data-stu-id="f039f-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  to your development PC with a USB Cable.</span></span>

<span data-ttu-id="f039f-170">Мы проверили этот способ, используя устройство Google Nexus 5X с Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="f039f-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="f039f-171">Все описанные приемы подходят для любой современной версии платформы Android.</span><span class="sxs-lookup"><span data-stu-id="f039f-171">However, the techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="f039f-172">Установка служб Google Play</span><span class="sxs-lookup"><span data-stu-id="f039f-172">Install Google Play Services</span></span>
<span data-ttu-id="f039f-173">Подключаемый модуль push-уведомлений передает push-уведомления через службы Google Play Android.</span><span class="sxs-lookup"><span data-stu-id="f039f-173">The push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="f039f-174">В Visual Studio щелкните **Инструменты** > **Android** > **Диспетчер пакетов SDK для Android**, разверните папку **Дополнения** и установите соответствующие флажки, чтобы обеспечить установку всех следующих пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="f039f-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand the **Extras** folder and  check the box to make sure that each of the following SDKs is installed.</span></span>

   * <span data-ttu-id="f039f-175">Android 2.3 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f039f-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="f039f-176">Репозиторий Google версии 27 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="f039f-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="f039f-177">Службы Google Play 9.0.2 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="f039f-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="f039f-178">Щелкните **Install Packages** (Установить пакеты) и дождитесь завершения установки.</span><span class="sxs-lookup"><span data-stu-id="f039f-178">Click **Install Packages** and wait for the installation to complete.</span></span>

<span data-ttu-id="f039f-179">Необходимые на данный момент библиотеки перечислены в [документации по установке подключаемого модуля push-уведомлений PhoneGap][19].</span><span class="sxs-lookup"><span data-stu-id="f039f-179">The current required libraries are listed in the [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-the-app-on-android"></a><span data-ttu-id="f039f-180">Тестирование push-уведомлений в приложении для Android</span><span class="sxs-lookup"><span data-stu-id="f039f-180">Test push notifications in the app on Android</span></span>
<span data-ttu-id="f039f-181">Теперь вы можете проверить работу push-уведомлений путем запуска приложения и вставки элементов в таблицу TodoItem.</span><span class="sxs-lookup"><span data-stu-id="f039f-181">You can now test push notifications by running the app and inserting items in the TodoItem table.</span></span> <span data-ttu-id="f039f-182">Это делается на том же (или другом) устройстве при условии, что используется одна серверная часть.</span><span class="sxs-lookup"><span data-stu-id="f039f-182">You can test from the same device or from a second device, as long as you are using the same backend.</span></span> <span data-ttu-id="f039f-183">Проверьте работу приложения Cordova на платформе Android одним из следующих способов.</span><span class="sxs-lookup"><span data-stu-id="f039f-183">Test your Cordova app on the Android platform in one of the following ways:</span></span>

* <span data-ttu-id="f039f-184">**На физическом устройстве.** Подключите устройство Android к компьютеру разработчика с помощью USB-кабеля.</span><span class="sxs-lookup"><span data-stu-id="f039f-184">**On a physical device:** Attach your Android device to your development computer with a USB cable.</span></span>  <span data-ttu-id="f039f-185">Вместо **Эмулятор Google Android** выберите **Устройство**.</span><span class="sxs-lookup"><span data-stu-id="f039f-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="f039f-186">Visual Studio развернет приложение на устройстве и запустит приложение.</span><span class="sxs-lookup"><span data-stu-id="f039f-186">Visual Studio deploys the application to the device and then runs the application.</span></span>  <span data-ttu-id="f039f-187">После этого вы сможете работать с приложением на устройстве.</span><span class="sxs-lookup"><span data-stu-id="f039f-187">You can then interact with the application on the device.</span></span>

  <span data-ttu-id="f039f-188">Усовершенствуйте интерфейс разработки.</span><span class="sxs-lookup"><span data-stu-id="f039f-188">Improve your development experience.</span></span>  <span data-ttu-id="f039f-189">В разработке приложения Android вам помогут приложения для демонстрации экрана, например [Mobizen][20].</span><span class="sxs-lookup"><span data-stu-id="f039f-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="f039f-190">Приложение Mobizen транслирует экран Android в веб-браузер на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f039f-190">Mobizen projects your Android screen to a web browser on your PC.</span></span>

* <span data-ttu-id="f039f-191">**На эмуляторе Android.** Для запуска в эмуляторе необходимо выполнить дополнительную настройку.</span><span class="sxs-lookup"><span data-stu-id="f039f-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="f039f-192">Убедитесь, что для развертывания используется виртуальное устройство, на котором в качестве места назначения заданы интерфейсы Google API, как показано в диспетчере виртуальных устройств Android (AVD).</span><span class="sxs-lookup"><span data-stu-id="f039f-192">Make sure you are deploying to a virtual device that has Google APIs set as the target, as shown in the Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="f039f-193">Если вы хотите использовать более быстрый эмулятор x86, [установите драйвер HAXM][11] и настройте его использование в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="f039f-193">If you want to use a faster x86 emulator, you [install the HAXM driver][11] and configure the emulator to use it.</span></span>

    <span data-ttu-id="f039f-194">Добавить учетную запись Google на устройстве Android, поочередно щелкнув **Apps** (Приложения) > **Settings** (Параметры) > **Add account** (Добавить учетную запись). Затем следуйте указаниям на экране.</span><span class="sxs-lookup"><span data-stu-id="f039f-194">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="f039f-195">Запустите приложение todolist, как ранее, и вставьте новый элемент списка дел.</span><span class="sxs-lookup"><span data-stu-id="f039f-195">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="f039f-196">На этот раз в области уведомлений отображается значок уведомления.</span><span class="sxs-lookup"><span data-stu-id="f039f-196">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="f039f-197">Вы можете открыть панель уведомлений, чтобы просмотреть полный текст уведомления.</span><span class="sxs-lookup"><span data-stu-id="f039f-197">You can open the notification drawer to view the full text of the notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="f039f-198">Настройка и запуск проекта в iOS (необязательно)</span><span class="sxs-lookup"><span data-stu-id="f039f-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="f039f-199">В этом разделе описано, как запустить проект Cordova для устройств под управлением iOS.</span><span class="sxs-lookup"><span data-stu-id="f039f-199">This section is for running the Cordova project on iOS devices.</span></span> <span data-ttu-id="f039f-200">Пропустите этот раздел, если вы не работаете с устройствами iOS.</span><span class="sxs-lookup"><span data-stu-id="f039f-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-the-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="f039f-201">Установка и запуск агента удаленной сборки iOS на компьютере Mac или в облачной службе</span><span class="sxs-lookup"><span data-stu-id="f039f-201">Install and run the iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="f039f-202">Прежде чем запускать приложение Cordova в iOS с помощью Visual Studio, выполните действия из [руководства по установке iOS][12], чтобы установить и запустить агент удаленной сборки.</span><span class="sxs-lookup"><span data-stu-id="f039f-202">Before you can run a Cordova app on iOS using Visual Studio, go through the steps in the [iOS Setup Guide][12] to install and run the remote build agent.</span></span>

<span data-ttu-id="f039f-203">Убедитесь, что вы можете создать приложение для iOS.</span><span class="sxs-lookup"><span data-stu-id="f039f-203">Make sure you can build the app for iOS.</span></span> <span data-ttu-id="f039f-204">Приведенные в этом руководстве шаги по установке необходимы для сборки приложения для iOS в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f039f-204">The steps in the setup guide are required to build for iOS from Visual Studio.</span></span> <span data-ttu-id="f039f-205">Если у вас нет компьютера Mac, можно использовать агент удаленной сборки в такой службе, как MacInCloud.</span><span class="sxs-lookup"><span data-stu-id="f039f-205">If you do not have a Mac, you can build for iOS using the remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="f039f-206">Дополнительные сведения см. в статье [Build and simulate a Cordova iOS app in the cloud][21] (Сборка и симуляция приложения Cordova iOS в облаке).</span><span class="sxs-lookup"><span data-stu-id="f039f-206">For more info, see [Run your iOS app in the cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="f039f-207">XCode 7 или более поздней версии требуется для использования подключаемого модуля push-уведомлений в iOS.</span><span class="sxs-lookup"><span data-stu-id="f039f-207">XCode 7 or greater is required to use the push plugin on iOS.</span></span>

#### <a name="find-the-id-to-use-as-your-app-id"></a><span data-ttu-id="f039f-208">Поиск идентификатора, который будет использоваться как идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="f039f-208">Find the ID to use as your App ID</span></span>
<span data-ttu-id="f039f-209">Прежде чем зарегистрировать приложение для работы с push-уведомлениями, откройте файл config.xml в приложении Cordova, найдите значение атрибута `id` в элементе мини-приложения и скопируйте его для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="f039f-209">Before you register your app for push notifications, open config.xml in your Cordova app, find the `id` attribute value in the widget element, and copy it for later use.</span></span> <span data-ttu-id="f039f-210">В приведенном ниже коде XML идентификатором выступает `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="f039f-210">In the following XML, the ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="f039f-211">Вам потребуется использовать этот идентификатор при создании идентификатора приложения на портале разработчика Apple.</span><span class="sxs-lookup"><span data-stu-id="f039f-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="f039f-212">Если на портале разработчика вы создали другой идентификатор приложения, вам понадобится выполнить дополнительные действия, описанные далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="f039f-212">If you create a different App ID on the developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="f039f-213">Идентификатор элемента мини-приложения должен соответствовать идентификатору приложения на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="f039f-213">The ID in the widget element must match the App ID on the developer portal.</span></span>

#### <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="f039f-214">Зарегистрируйте приложение для push-уведомлений на портале разработчика Apple.</span><span class="sxs-lookup"><span data-stu-id="f039f-214">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="f039f-215">Видео, демонстрирующее аналогичные действия</span><span class="sxs-lookup"><span data-stu-id="f039f-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="f039f-216">Настройка Azure для отправки push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="f039f-216">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="f039f-217">Проверка, соответствует ли идентификатор приложения указанному в приложении Cordova</span><span class="sxs-lookup"><span data-stu-id="f039f-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="f039f-218">Если идентификатор приложения, созданный в вашей учетной записи разработчика Apple, совпадает с идентификатором элемента мини-приложения в файле config.xml, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="f039f-218">If the App ID you created in your Apple Developer Account already matches the ID of the widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="f039f-219">Однако если идентификаторы не совпадают, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="f039f-219">However, if the IDs don't match, take the following steps:</span></span>

1. <span data-ttu-id="f039f-220">Удалите папку platforms из проекта.</span><span class="sxs-lookup"><span data-stu-id="f039f-220">Delete the platforms folder from your project.</span></span>
2. <span data-ttu-id="f039f-221">Удалите папку plugins из проекта.</span><span class="sxs-lookup"><span data-stu-id="f039f-221">Delete the plugins folder from your project.</span></span>
3. <span data-ttu-id="f039f-222">Удалите папку node_modules из проекта.</span><span class="sxs-lookup"><span data-stu-id="f039f-222">Delete the node_modules folder from your project.</span></span>
4. <span data-ttu-id="f039f-223">В качестве значения атрибута идентификатора для элемента мини-приложения в файле config.xml укажите идентификатор приложения, созданный в вашей учетной записи разработчика Apple.</span><span class="sxs-lookup"><span data-stu-id="f039f-223">Update the id attribute of the widget element in config.xml to use the App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="f039f-224">Перестройте свой проект.</span><span class="sxs-lookup"><span data-stu-id="f039f-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="f039f-225">Тестирование push-уведомлений в приложении iOS</span><span class="sxs-lookup"><span data-stu-id="f039f-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="f039f-226">В Visual Studio выберите **iOS** в качестве целевого объекта развертывания, а затем выберите **устройство**, которое нужно запустить на подключенном устройстве iOS.</span><span class="sxs-lookup"><span data-stu-id="f039f-226">In Visual Studio, make sure that **iOS** is selected as the deployment target, and then choose **Device** to run on your connected iOS device.</span></span>

    <span data-ttu-id="f039f-227">Можно выполнить запуск на устройстве iOS, подключенном к компьютеру с помощью iTunes.</span><span class="sxs-lookup"><span data-stu-id="f039f-227">You can run on an iOS device connected to your PC using iTunes.</span></span> <span data-ttu-id="f039f-228">Симулятор iOS не поддерживает push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="f039f-228">The iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="f039f-229">Нажмите кнопку **Запустить** или клавишу **F5** в Visual Studio, чтобы выполнить сборку проекта и запустить приложение на устройстве iOS. Затем нажмите кнопку **ОК**, чтобы разрешить прием push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f039f-229">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS  device, then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f039f-230">При первом запуске приложение запросит подтверждение для приема push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f039f-230">The app requests confirmation for push notifications during the first run.</span></span>

3. <span data-ttu-id="f039f-231">В приложении введите задачу, затем щелкните знак "плюс" (+).</span><span class="sxs-lookup"><span data-stu-id="f039f-231">In the app, type a task, and then click the plus (+) icon.</span></span>
4. <span data-ttu-id="f039f-232">Убедитесь, что уведомление получено, а затем нажмите кнопку ОК, чтобы его закрыть.</span><span class="sxs-lookup"><span data-stu-id="f039f-232">Verify that a notification is received, then click OK to dismiss the notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="f039f-233">Настройка и запуск проекта в Windows (необязательно)</span><span class="sxs-lookup"><span data-stu-id="f039f-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="f039f-234">В этом разделе описывается запуск проекта приложения Apache Cordova на устройствах Windows 10 (в Windows 10 поддерживается подключаемый модуль push-уведомлений PhoneGap).</span><span class="sxs-lookup"><span data-stu-id="f039f-234">This section is for running the Apache Cordova app project on Windows 10 devices (the PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="f039f-235">Пропустите этот раздел, если вы не работаете с устройствами Windows.</span><span class="sxs-lookup"><span data-stu-id="f039f-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="f039f-236">Регистрация приложения Windows для получения push-уведомлений с помощью WNS</span><span class="sxs-lookup"><span data-stu-id="f039f-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="f039f-237">Чтобы использовать возможности Магазина в Visual Studio, выберите версию платформы Windows из списка платформ решения, например **Windows-x64** или **Windows-x86** (не используйте **Windows-AnyCPU** для push-уведомлений).</span><span class="sxs-lookup"><span data-stu-id="f039f-237">To use the Store options in Visual Studio, select a Windows target from the Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="f039f-238">[Просмотрите видео, демонстрирующее аналогичные действия][13]</span><span class="sxs-lookup"><span data-stu-id="f039f-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="f039f-239">Настройка концентратора уведомлений для WNS</span><span class="sxs-lookup"><span data-stu-id="f039f-239">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-to-support-windows-push-notifications"></a><span data-ttu-id="f039f-240">Настройка поддержки push-уведомлений Windows в приложении Cordova</span><span class="sxs-lookup"><span data-stu-id="f039f-240">Configure your Cordova app to support Windows push notifications</span></span>
<span data-ttu-id="f039f-241">Откройте конструктор конфигурации (щелкните файл config.xml правой кнопкой мыши и выберите **Конструктор представлений**), перейдите на вкладку **Windows** и выберите для параметра **Целевая версия Windows** значение **Windows 10**.</span><span class="sxs-lookup"><span data-stu-id="f039f-241">Open the configuration designer (right-click on config.xml and select **View Designer**), select the **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="f039f-242">Для поддержки push-уведомлений в сборках по умолчанию (отладка) откройте файл build.json.</span><span class="sxs-lookup"><span data-stu-id="f039f-242">To support push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="f039f-243">Скопируйте конфигурацию в разделе release в конфигурацию отладки.</span><span class="sxs-lookup"><span data-stu-id="f039f-243">Copy the "release" configuration to your debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="f039f-244">После обновления файл build.json должен содержать следующий код:</span><span class="sxs-lookup"><span data-stu-id="f039f-244">After the update, the build.json should contain the following code:</span></span>

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

<span data-ttu-id="f039f-245">Выполните сборку приложения и убедитесь в отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="f039f-245">Build the app and verify that you have no errors.</span></span> <span data-ttu-id="f039f-246">Теперь клиентское приложение должно зарегистрироваться для получения уведомлений из серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="f039f-246">Your client app should now register for the notifications from the Mobile App backend.</span></span> <span data-ttu-id="f039f-247">Повторите действия из этого раздела для каждого проекта Windows, входящего в ваше решение.</span><span class="sxs-lookup"><span data-stu-id="f039f-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="f039f-248">Тестирование push-уведомлений в приложении Windows</span><span class="sxs-lookup"><span data-stu-id="f039f-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="f039f-249">В Visual Studio выберите платформу Windows, например **Windows-x64** или **Windows-x86**, в качестве целевого объекта развертывания.</span><span class="sxs-lookup"><span data-stu-id="f039f-249">In Visual Studio, make sure that a Windows platform is selected as the deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="f039f-250">Чтобы запустить приложение на компьютере Windows 10, где размещено приложение Visual Studio, выберите **Локальный компьютер**.</span><span class="sxs-lookup"><span data-stu-id="f039f-250">To run the app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="f039f-251">Нажмите кнопку Запуск для построения проекта, после чего запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="f039f-251">Press the Run button to build the project and start the app.</span></span>

<span data-ttu-id="f039f-252">В приложении введите имя нового объекта todoitem и добавьте его, щелкнув значок плюса (+).</span><span class="sxs-lookup"><span data-stu-id="f039f-252">In the app, type a name for a new todoitem, and then click the plus (+) icon to add it.</span></span>

<span data-ttu-id="f039f-253">После добавления элемента должно отобразиться соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="f039f-253">Verify that a notification is received when the item is added.</span></span>

## <span data-ttu-id="f039f-254"><a name="next-steps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f039f-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="f039f-255">Дополнительные сведения о push-уведомлениях см. в статье о [центрах уведомлений][17].</span><span class="sxs-lookup"><span data-stu-id="f039f-255">Read about [Notification Hubs][17] to learn about push notifications.</span></span>
* <span data-ttu-id="f039f-256">Продолжите работу с руководством и [добавьте проверку подлинности][14] в приложение Apache Cordova, если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="f039f-256">If you have not already done so, continue the tutorial by [Adding Authentication][14] to your Apache Cordova app.</span></span>

<span data-ttu-id="f039f-257">Подробнее об использовании пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="f039f-257">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="f039f-258">[Использование клиентской библиотеки Apache Cordova для мобильных приложений Azure][15]</span><span class="sxs-lookup"><span data-stu-id="f039f-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="f039f-259">[Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure][1]</span><span class="sxs-lookup"><span data-stu-id="f039f-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="f039f-260">[Использование пакета SDK Node.js для мобильных приложений Azure][16]</span><span class="sxs-lookup"><span data-stu-id="f039f-260">[Node.js Server SDK][16]</span></span>

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
