---
title: "приложения tooChrome aaaSend принудительной уведомлений с концентраторами уведомлений Azure | Документы Microsoft"
description: "Узнайте, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa Chrome приложения."
services: notification-hubs
keywords: "мобильные push-уведомления, push-уведомления, push-уведомление, push-уведомления Chrome"
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="91974-104">Отправка push приложений tooChrome уведомлений с концентраторами уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="91974-104">Send push notifications tooChrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="91974-105">В этом разделе показано, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa Chrome приложение, которое будет отображаться в контексте hello hello браузера Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="91974-105">This topic shows you how toouse Azure Notification Hubs toosend push notifications tooa Chrome App, which will be displayed within hello context of hello Google Chrome browser.</span></span> <span data-ttu-id="91974-106">В этом руководстве мы создадим приложение Chrome, которое получает push-уведомления с помощью [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="91974-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="91974-107">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="91974-107">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="91974-108">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="91974-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="91974-109">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="91974-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="91974-110">Hello учебник поможет выполнить следующие основные шаги tooenable push-уведомлений:</span><span class="sxs-lookup"><span data-stu-id="91974-110">hello tutorial walks you through these basic steps tooenable push notifications:</span></span>

* [<span data-ttu-id="91974-111">Включение Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="91974-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="91974-112">Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="91974-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="91974-113">Концентратор уведомлений приложение Chrome toohello подключения</span><span class="sxs-lookup"><span data-stu-id="91974-113">Connect your Chrome App toohello notification hub</span></span>](#connect-app)
* [<span data-ttu-id="91974-114">Отправка push уведомления tooyour Chrome приложения</span><span class="sxs-lookup"><span data-stu-id="91974-114">Send a push notification tooyour Chrome App</span></span>](#send)
* [<span data-ttu-id="91974-115">Дополнительные функции и возможности</span><span class="sxs-lookup"><span data-stu-id="91974-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="91974-116">Push-уведомлений приложения Chrome не универсальный уведомления в браузере — это модель расширяемости конкретных toohello браузера (см. [Обзор приложений Chrome] подробные сведения).</span><span class="sxs-lookup"><span data-stu-id="91974-116">Chrome app push notifications are not generic in-browser notifications - they are specific toohello browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="91974-117">В дополнение к этому toohello браузер для настольных компьютеров, Chrome приложения выполняются на мобильном устройстве (Android и iOS) через Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="91974-117">In addition toohello desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="91974-118">В разделе [Chrome приложений на мобильном устройстве] toolearn дополнительные.</span><span class="sxs-lookup"><span data-stu-id="91974-118">See [Chrome Apps on Mobile] toolearn more.</span></span>
> 
> 

<span data-ttu-id="91974-119">Настройка GCM и концентраторов уведомлений Azure — идентичные tooconfiguring для Android, так как [Google Cloud Messaging для Chrome] является устаревшим и hello же GCM теперь поддерживает устройства Android и хром экземпляров.</span><span class="sxs-lookup"><span data-stu-id="91974-119">Configuring GCM and Azure Notification Hubs is identical tooconfiguring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and hello same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="91974-120"><a id="register"></a>Включение Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="91974-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="91974-121">Перейдите toohello [облачной консоли Google] веб-сайта, войдите с помощью учетной записи Google и нажмите кнопку hello **Создание проекта** кнопки.</span><span class="sxs-lookup"><span data-stu-id="91974-121">Navigate toohello [Google Cloud Console] website, sign in with your Google account credentials, and then click hello **Create Project** button.</span></span> <span data-ttu-id="91974-122">Укажите соответствующий **имя проекта**и нажмите кнопку hello **создать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="91974-122">Provide an appropriate **Project Name**, and then click hello **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="91974-123">Запишите hello **номер проекта** на hello **проекты** страницы для hello проекта, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="91974-123">Make a note of hello **Project Number** on hello **Projects** page for hello project that you just created.</span></span> <span data-ttu-id="91974-124">Это будет использоваться в качестве hello **идентификатор отправителя GCM** в tooregister Chrome приложения hello с GCM.</span><span class="sxs-lookup"><span data-stu-id="91974-124">You will use this as hello **GCM Sender ID** in hello Chrome App tooregister with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="91974-125">Hello левой панели щелкните **API-интерфейсы & auth**, затем прокрутите вниз и нажмите кнопку переключателя tooenable hello **Google Cloud Messaging для Android**.</span><span class="sxs-lookup"><span data-stu-id="91974-125">In hello left pane, click **APIs & auth**, and then scroll down and click hello toggle tooenable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="91974-126">Нет tooenable **Google Cloud Messaging для Chrome**.</span><span class="sxs-lookup"><span data-stu-id="91974-126">You don't have tooenable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="91974-127">Hello левой панели щелкните **учетные данные** > **создать новый ключ** > **ключа сервера** > **создать**.</span><span class="sxs-lookup"><span data-stu-id="91974-127">In hello left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="91974-128">Запишите hello server **ключ API**.</span><span class="sxs-lookup"><span data-stu-id="91974-128">Make a note of hello server **API Key**.</span></span> <span data-ttu-id="91974-129">Вы настроите это ваш tooenable Далее, концентратор уведомлений его tooGCM уведомления toosend push.</span><span class="sxs-lookup"><span data-stu-id="91974-129">You will configure this in your notification hub next, tooenable it toosend push notifications tooGCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="91974-130"><a id="configure-hub"></a>Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="91974-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="91974-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="91974-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="91974-132">В hello **параметры** колонке выберите **служб Notification Services** и затем **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="91974-132">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="91974-133">Введите ключ API hello и сохранить.</span><span class="sxs-lookup"><span data-stu-id="91974-133">Enter hello API key and save.</span></span>

&emsp;&emsp;![Центры уведомлений Azure — Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="91974-135"><a id="connect-app"></a>Концентратор уведомлений приложение Chrome toohello подключения</span><span class="sxs-lookup"><span data-stu-id="91974-135"><a id="connect-app"></a>Connect your Chrome App toohello notification hub</span></span>
<span data-ttu-id="91974-136">Концентратор уведомлений теперь настроенных toowork с GCM, и у вас есть hello tooregister строки подключения вашего приложения tooboth получения и отправки извещающих уведомлений.</span><span class="sxs-lookup"><span data-stu-id="91974-136">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooregister your app tooboth receive and send push notifications.</span></span> <span data-ttu-id="91974-137">LK</span><span class="sxs-lookup"><span data-stu-id="91974-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="91974-138">Создание нового приложения Chrome</span><span class="sxs-lookup"><span data-stu-id="91974-138">Create a new Chrome App</span></span>
<span data-ttu-id="91974-139">Образец Hello ниже основан на hello [пример GCM приложения Chrome] и использует hello рекомендуется toocreate способом приложения Chrome.</span><span class="sxs-lookup"><span data-stu-id="91974-139">hello sample below is based on hello [Chrome App GCM Sample] and uses hello recommended way toocreate a Chrome App.</span></span> <span data-ttu-id="91974-140">TooAzure специально связанные действия hello концентраторы уведомлений будут выделены.</span><span class="sxs-lookup"><span data-stu-id="91974-140">We will highlight hello steps specifically related tooAzure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="91974-141">Мы рекомендуем загрузить hello источника для этого приложения Chrome из [пример концентратора уведомлений приложения Chrome].</span><span class="sxs-lookup"><span data-stu-id="91974-141">We recommend that you download hello source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="91974-142">Hello Chrome приложение создается с помощью JavaScript и любой из редакторов Ваш предпочитаемый word можно использовать для его создания.</span><span class="sxs-lookup"><span data-stu-id="91974-142">hello Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="91974-143">Приложение Chrome будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="91974-143">Below is what this Chrome App will look like.</span></span>

![Приложение Google Chrome][15]

1. <span data-ttu-id="91974-145">Создайте папку с именем `ChromePushApp`.</span><span class="sxs-lookup"><span data-stu-id="91974-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="91974-146">Конечно, произвольное имя hello - Если присвоить файлу имя, чем-то другим, убедитесь, что можно заменить путем hello в сегменты кода hello требуется.</span><span class="sxs-lookup"><span data-stu-id="91974-146">Of course, hello name is arbitrary - if you name it something different, make sure you substitute hello path in hello required code segments.</span></span>
2. <span data-ttu-id="91974-147">Загрузите hello [библиотеки шифрования js] в hello папку, созданную на втором шаге hello.</span><span class="sxs-lookup"><span data-stu-id="91974-147">Download hello [crypto-js library] in hello folder you created in hello second step.</span></span> <span data-ttu-id="91974-148">В этой папке библиотеки будут содержаться две вложенные папки: `components` и `rollups`.</span><span class="sxs-lookup"><span data-stu-id="91974-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="91974-149">Создайте файл `manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="91974-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="91974-150">Все приложения Chrome, поддерживаемых файл манифеста, содержащий метаданные приложения hello и большинство того, все разрешения, предоставленные toohello приложения при hello пользователь устанавливает его.</span><span class="sxs-lookup"><span data-stu-id="91974-150">All Chrome Apps are backed by a manifest file that contains hello app metadata and, most importantly, all permissions that are granted toohello app when hello user installs it.</span></span>
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    <span data-ttu-id="91974-151">Обратите внимание hello `permissions` элемент, который указывает, что это приложение Chrome будет может tooreceive push-уведомления в GCM.</span><span class="sxs-lookup"><span data-stu-id="91974-151">Notice hello `permissions` element, which specifies that this Chrome App will be able tooreceive push notifications from GCM.</span></span> <span data-ttu-id="91974-152">Также необходимо указать URI концентраторов уведомлений Azure, где hello Chrome приложение сделает вызов REST tooregister hello.</span><span class="sxs-lookup"><span data-stu-id="91974-152">It must also specify hello Azure Notification Hubs URI where hello Chrome App will make a REST call tooregister.</span></span>
    <span data-ttu-id="91974-153">Наш пример приложения также использует файл значка `gcm_128.png`, можно найти в источнике hello повторно из исходного GCM образца hello.</span><span class="sxs-lookup"><span data-stu-id="91974-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at hello source that's reused from hello original GCM sample.</span></span> <span data-ttu-id="91974-154">Его можно заменить на любое изображение, которое соответствует hello [критерии значок](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="91974-154">You can substitute it for any image that fits hello [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="91974-155">Создайте файл с именем `background.js` с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="91974-155">Create a file called `background.js` with hello following code:</span></span>
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="91974-156">Это файл hello, всплывает окно Chrome приложения hello HTML (**register.html**) и также определяет обработчик hello **messageReceived** toohandle hello входящих push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="91974-156">This is hello file that pops up hello Chrome App window HTML (**register.html**) and also defines hello handler **messageReceived** toohandle hello incoming push notification.</span></span>
5. <span data-ttu-id="91974-157">Создайте файл с именем `register.html` -это определяет пользовательский Интерфейс hello Chrome приложения hello.</span><span class="sxs-lookup"><span data-stu-id="91974-157">Create a file called `register.html` - this defines hello UI of hello Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="91974-158">В этом образце используется **CryptoJS 3.1.2**.</span><span class="sxs-lookup"><span data-stu-id="91974-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="91974-159">Если вы загрузили другую версию библиотеки hello, убедитесь, что вы правильно заменить версию hello в hello `src` пути.</span><span class="sxs-lookup"><span data-stu-id="91974-159">If you downloaded another version of hello library, make sure you properly substitute hello version in hello `src` path.</span></span>
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. <span data-ttu-id="91974-160">Создайте файл с именем `register.js` hello код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="91974-160">Create a file called `register.js` with hello code below.</span></span> <span data-ttu-id="91974-161">Этот файл содержит скрипт hello за `register.html`.</span><span class="sxs-lookup"><span data-stu-id="91974-161">This file specifies hello script behind `register.html`.</span></span> <span data-ttu-id="91974-162">Chrome приложения не допускают встроенного выполнения, их необходимо toocreate отдельные резервного скрипта для пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="91974-162">Chrome Apps do not allow inline execution, so you have toocreate a separate backing script for your UI.</span></span>
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update hello payload with hello registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    <span data-ttu-id="91974-163">Hello выше сценарий имеет следующие ключевые параметры hello.</span><span class="sxs-lookup"><span data-stu-id="91974-163">hello above script has hello following key parameters:</span></span>
   
   * <span data-ttu-id="91974-164">**Window.onload** определяет события нажатия кнопки hello hello двух кнопок на hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="91974-164">**window.onload** defines hello button-click events of hello two buttons on hello UI.</span></span> <span data-ttu-id="91974-165">Один регистрируется GCM и других hello использует идентификатор регистрации hello, возвращаемое после регистрации GCM tooregister с концентраторами уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="91974-165">One registers with GCM, and hello other uses hello registration ID that's returned after registration with GCM tooregister with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="91974-166">**updateLog** — hello функция, которая позволяет нам toohandle простой протоколирования.</span><span class="sxs-lookup"><span data-stu-id="91974-166">**updateLog** is hello function that allows us toohandle simple logging capabilities.</span></span>
   * <span data-ttu-id="91974-167">**registerWithGCM** первого нажатия кнопки обработчика hello, благодаря чему hello `chrome.gcm.register` tooGCM tooregister hello текущего приложения Chrome экземпляра вызова.</span><span class="sxs-lookup"><span data-stu-id="91974-167">**registerWithGCM** is hello first button-click handler, which makes hello `chrome.gcm.register` call tooGCM tooregister hello current Chrome App instance.</span></span>
   * <span data-ttu-id="91974-168">**registerCallback** — hello функция обратного вызова, который вызывается при возвращении вызова регистрации GCM hello.</span><span class="sxs-lookup"><span data-stu-id="91974-168">**registerCallback** is hello callback function that gets called when hello GCM registration call returns.</span></span>
   * <span data-ttu-id="91974-169">**registerWithNH** — hello второй обработчик щелчка кнопки, который регистрируется с помощью концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="91974-169">**registerWithNH** is hello second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="91974-170">Он возвращает `hubName` и `connectionString` (какие hello пользователь указал) и создается hello вызова интерфейса API REST регистрации концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="91974-170">It gets `hubName` and `connectionString` (which hello user has specified) and crafts hello Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="91974-171">**splitConnectionString** и **generateSaSToken** — это вспомогательные средства представляют реализация JavaScript hello процесса создания маркера SaS, который должен использоваться во всех вызовах API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="91974-171">**splitConnectionString** and **generateSaSToken** are helpers that represent hello JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="91974-172">Дополнительные сведения см. в статье [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx) (Основные понятия).</span><span class="sxs-lookup"><span data-stu-id="91974-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="91974-173">**sendNHRegistrationRequest** это вызов функции hello, который делает HTTP REST tooAzure концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="91974-173">**sendNHRegistrationRequest** is hello function that makes a HTTP REST call tooAzure Notification Hubs.</span></span>
   * <span data-ttu-id="91974-174">**registrationPayload** определяет полезные данные XML регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="91974-174">**registrationPayload** defines hello registration XML payload.</span></span> <span data-ttu-id="91974-175">Дополнительные сведения см. в статье [Create Registration NH REST API]. (Создание REST API Центра уведомлений для регистрации).</span><span class="sxs-lookup"><span data-stu-id="91974-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="91974-176">Мы дополнить код регистрации hello в нем был получен из GCM.</span><span class="sxs-lookup"><span data-stu-id="91974-176">We update hello registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="91974-177">**клиент** является экземпляром класса **XMLHttpRequest** , мы используем toomake hello HTTP-запроса POST.</span><span class="sxs-lookup"><span data-stu-id="91974-177">**client** is an instance of **XMLHttpRequest** that we use toomake hello HTTP POST request.</span></span> <span data-ttu-id="91974-178">Обратите внимание, что мы изменить hello `Authorization` заголовок с `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="91974-178">Note that we update hello `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="91974-179">Если этот вызов будет выполнен успешно, этот экземпляр приложения Chrome будет зарегистрирован в центре уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="91974-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="91974-180">Hello общую структуру папок для этого проекта должен выглядеть примерно следующим образом: ![приложение Google Chrome - структура папок][21]</span><span class="sxs-lookup"><span data-stu-id="91974-180">hello overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="91974-181">Настройка и тестирование приложения Chrome</span><span class="sxs-lookup"><span data-stu-id="91974-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="91974-182">Откройте браузер Chrome.</span><span class="sxs-lookup"><span data-stu-id="91974-182">Open your Chrome browser.</span></span> <span data-ttu-id="91974-183">Откройте окно **Расширения** и установите флажок **Режим разработчика**.</span><span class="sxs-lookup"><span data-stu-id="91974-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="91974-184">Нажмите кнопку **загрузить распаковано расширение** и перейдите в папку toohello, где были созданы файлы hello.</span><span class="sxs-lookup"><span data-stu-id="91974-184">Click **Load unpacked extension** and navigate toohello folder where you created hello files.</span></span> <span data-ttu-id="91974-185">Можно также использовать hello **Chrome приложений и средства разработчика расширения**.</span><span class="sxs-lookup"><span data-stu-id="91974-185">You can also optionally use hello **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="91974-186">Этот инструмент представляет собой приложение и хром само по себе (установлен hello Chrome веб-хранилище) и предоставляет расширенные возможности отладки для разработки приложений Chrome.</span><span class="sxs-lookup"><span data-stu-id="91974-186">This tool is a Chrome App in itself (installed from hello Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="91974-187">Если hello Chrome приложения создается без ошибок, вы увидите отображаться Chrome приложения.</span><span class="sxs-lookup"><span data-stu-id="91974-187">If hello Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="91974-188">Введите hello **номер проекта** , полученный ранее из hello **облачной консоли Google** идентификатор отправителя hello и нажмите кнопку **регистрации GCM**.</span><span class="sxs-lookup"><span data-stu-id="91974-188">Enter hello **Project Number** that you got earlier from hello **Google Cloud Console** as hello sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="91974-189">Должно появиться сообщение hello **регистрации GCM успешно выполнен.**</span><span class="sxs-lookup"><span data-stu-id="91974-189">You must see hello message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="91974-190">Введите ваш **имя концентратора уведомлений** и hello **DefaultListenSharedAccessSignature** , полученный из портала hello ранее и нажмите кнопку **регистрации в концентратор уведомлений Azure**.</span><span class="sxs-lookup"><span data-stu-id="91974-190">Enter your **Notification Hub Name** and hello **DefaultListenSharedAccessSignature** that you obtained from hello portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="91974-191">Должно появиться сообщение hello **регистрации концентратор уведомлений успешно!**</span><span class="sxs-lookup"><span data-stu-id="91974-191">You must see hello message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="91974-192">а hello подробные сведения о регистрации ответ hello, который содержит hello регистрации концентраторов уведомлений Azure по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="91974-192">and hello details of hello registration response, which contains hello Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="91974-193"><a name="send"></a>Отправлять уведомления tooyour Chrome приложения</span><span class="sxs-lookup"><span data-stu-id="91974-193"><a name="send"></a>Send a notification tooyour Chrome App</span></span>
<span data-ttu-id="91974-194">Для тестирования мы отправим push-уведомления Chrome с помощью консольного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="91974-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="91974-195">Push-уведомления можно отправлять с помощью Центров уведомлений с любого сервера через общедоступный <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">интерфейс REST</a>.</span><span class="sxs-lookup"><span data-stu-id="91974-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="91974-196">Больше примеров, включающих использование разных платформ, можно найти на [портале документации](https://azure.microsoft.com/documentation/services/notification-hubs/) .</span><span class="sxs-lookup"><span data-stu-id="91974-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="91974-197">В Visual Studio, из hello **файл** последовательно выберите пункты **New** и затем **проекта**.</span><span class="sxs-lookup"><span data-stu-id="91974-197">In Visual Studio, from hello **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="91974-198">В разделе **Visual C#** щелкните **Windows** и **Консольное приложение**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="91974-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="91974-199">Это создаст новый проект консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="91974-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="91974-200">Из hello **средства** меню, нажмите кнопку **диспетчер пакетов библиотеки** и затем **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="91974-200">From hello **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="91974-201">Откроется консоль диспетчера пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="91974-201">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="91974-202">В окне консоли hello выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="91974-202">In hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="91974-203">Откройте `Program.cs` и добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="91974-203">Open `Program.cs` and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="91974-204">В hello `Program` добавьте следующий метод hello:</span><span class="sxs-lookup"><span data-stu-id="91974-204">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="91974-205">Убедитесь, что используются hello строки подключения с **полного** доступ, не **прослушивания** доступа.</span><span class="sxs-lookup"><span data-stu-id="91974-205">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="91974-206">Hello **прослушивания** строку подключения доступа не предоставляет разрешений toosend push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="91974-206">hello **Listen** access connection string does not grant permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="91974-207">Добавьте следующие hello вызовы в hello `Main` метод:</span><span class="sxs-lookup"><span data-stu-id="91974-207">Add hello following calls in hello `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="91974-208">Убедитесь, что запущен Chrome и запустите консольное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="91974-208">Make sure that Chrome is running, and run hello console application.</span></span>
8. <span data-ttu-id="91974-209">Вы увидите следующее hello уведомления всплывающее окно на рабочем столе.</span><span class="sxs-lookup"><span data-stu-id="91974-209">You should see hello following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="91974-210">Можно также просмотреть все уведомления с помощью окно уведомления Chrome hello в панели задач hello (в Windows) при выполнении Chrome.</span><span class="sxs-lookup"><span data-stu-id="91974-210">You can also see all your notifications by using hello Chrome Notifications window in hello taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="91974-211">Не нужно toohave hello Chrome приложение работает или открыть в браузере hello (хотя должна быть запущена самим браузером hello Chrome).</span><span class="sxs-lookup"><span data-stu-id="91974-211">You don't need toohave hello Chrome App running or open in hello browser (though hello Chrome browser itself must be running).</span></span> <span data-ttu-id="91974-212">Можно также получить консолидированное представление всех уведомлений в окно приветствия Chrome уведомления.</span><span class="sxs-lookup"><span data-stu-id="91974-212">You also get a consolidated view of all your notifications in hello Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="91974-213"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="91974-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="91974-214">Дополнительные сведения о Центрах уведомлений см. в статье [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET].</span><span class="sxs-lookup"><span data-stu-id="91974-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="91974-215">tootarget конкретных пользователей, см. toohello [Azure концентраторы уведомлений уведомить пользователей] учебника.</span><span class="sxs-lookup"><span data-stu-id="91974-215">tootarget specific users, refer toohello [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="91974-216">Если требуется toosegment пользователи, группы интересов, можно выполнить hello [концентраторов уведомлений Azure, новости] учебника.</span><span class="sxs-lookup"><span data-stu-id="91974-216">If you want toosegment your users by interest groups, you can follow hello [Azure Notification Hubs breaking news] tutorial.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[пример концентратора уведомлений приложения Chrome]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[облачной консоли Google]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET]: notification-hubs-push-notification-overview.md
[Обзор приложений Chrome]: https://developer.chrome.com/apps/about_apps
[пример GCM приложения Chrome]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[Chrome приложений на мобильном устройстве]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[Create Registration NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[библиотеки шифрования js]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Google Cloud Messaging для Chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[Azure концентраторы уведомлений уведомить пользователей]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[концентраторов уведомлений Azure, новости]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
