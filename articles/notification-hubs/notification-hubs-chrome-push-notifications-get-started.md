---
title: "Отправка push-уведомлений в приложения Chrome с помощью Центров уведомлений Azure | Документация Майкрософт"
description: "Узнайте, как использовать Центры уведомлений Azure для отправки push-уведомлений в приложение Chrome."
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
ms.openlocfilehash: 600b1b7e5f3987c9a0acc33b7049f7118442b931
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="send-push-notifications-to-chrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="a848c-104">Отправка push-уведомлений в приложения Chrome с помощью Центров уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="a848c-104">Send push notifications to Chrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="a848c-105">В этом разделе показано, как использовать Центры уведомлений Azure для отправки push-уведомлений в приложение Chrome, которое будет запущено в браузере Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="a848c-105">This topic shows you how to use Azure Notification Hubs to send push notifications to a Chrome App, which will be displayed within the context of the Google Chrome browser.</span></span> <span data-ttu-id="a848c-106">В этом руководстве мы создадим приложение Chrome, которое получает push-уведомления с помощью [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="a848c-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="a848c-107">Для работы с этим учебником необходима активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a848c-107">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a848c-108">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a848c-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a848c-109">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="a848c-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="a848c-110">В этом учебнике рассматриваются следующие основные шаги для включения push-уведомлений:</span><span class="sxs-lookup"><span data-stu-id="a848c-110">The tutorial walks you through these basic steps to enable push notifications:</span></span>

* [<span data-ttu-id="a848c-111">Включение Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="a848c-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="a848c-112">Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="a848c-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="a848c-113">Подключение приложения Chrome к концентратору уведомлений</span><span class="sxs-lookup"><span data-stu-id="a848c-113">Connect your Chrome App to the notification hub</span></span>](#connect-app)
* [<span data-ttu-id="a848c-114">Отправка push-уведомления в приложение Chrome</span><span class="sxs-lookup"><span data-stu-id="a848c-114">Send a push notification to your Chrome App</span></span>](#send)
* [<span data-ttu-id="a848c-115">Дополнительные функции и возможности</span><span class="sxs-lookup"><span data-stu-id="a848c-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="a848c-116">push-уведомления приложения Chrome не поддерживаются во всех браузерах. Они поддерживаются в браузерах с конкретной моделью расширения (дополнительные сведения см. в статье [Обзор приложений Chrome]).</span><span class="sxs-lookup"><span data-stu-id="a848c-116">Chrome app push notifications are not generic in-browser notifications - they are specific to the browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="a848c-117">Помимо классического браузера, приложения Chrome также могут работать на мобильных устройствах (с ОС Android и iOS) с помощью Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="a848c-117">In addition to the desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="a848c-118">Дополнительные сведения см. в статье [Приложения Chrome на мобильных устройствах].</span><span class="sxs-lookup"><span data-stu-id="a848c-118">See [Chrome Apps on Mobile] to learn more.</span></span>
> 
> 

<span data-ttu-id="a848c-119">Так как служба [Google Cloud Messaging для Chrome] устарела и одна версия GCM теперь поддерживает как устройства Android, так и экземпляры Chrome, настройка GCM и Центров уведомлений Azure аналогична их настройке для ОС Android.</span><span class="sxs-lookup"><span data-stu-id="a848c-119">Configuring GCM and Azure Notification Hubs is identical to configuring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and the same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="a848c-120"><a id="register"></a>Включение Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="a848c-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="a848c-121">Перейдите на веб-сайт [консоли Google Cloud] , войдите с помощью своих учетных данных Google и нажмите кнопку **Create Project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="a848c-121">Navigate to the [Google Cloud Console] website, sign in with your Google account credentials, and then click the **Create Project** button.</span></span> <span data-ttu-id="a848c-122">Введите соответствующее **имя проекта** и нажмите кнопку **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="a848c-122">Provide an appropriate **Project Name**, and then click the **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="a848c-123">Запишите номер только что созданного проекта из поля **Project Number** (Номер проекта) на странице **Projects** (Проекты).</span><span class="sxs-lookup"><span data-stu-id="a848c-123">Make a note of the **Project Number** on the **Projects** page for the project that you just created.</span></span> <span data-ttu-id="a848c-124">Этот номер следует использовать как **идентификатор отправителя GCM** в приложении Chrome для регистрации в GCM.</span><span class="sxs-lookup"><span data-stu-id="a848c-124">You will use this as the **GCM Sender ID** in the Chrome App to register with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="a848c-125">В области слева щелкните **APIs & auth** (API и проверка подлинности), прокрутите вниз и переведите переключатель **Google Cloud Messaging for Android** (Google Cloud Messaging для Android) в положение "Вкл.".</span><span class="sxs-lookup"><span data-stu-id="a848c-125">In the left pane, click **APIs & auth**, and then scroll down and click the toggle to enable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="a848c-126">**Google Cloud Messaging для Chrome**включать не нужно.</span><span class="sxs-lookup"><span data-stu-id="a848c-126">You don't have to enable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="a848c-127">В области слева щелкните **Credentials** (Учетные данные) > **Create New Key** (Создать ключ) > **Server Key** (Ключ сервера) > **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="a848c-127">In the left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="a848c-128">Запишите значение **API Key**(Ключ API) для сервера.</span><span class="sxs-lookup"><span data-stu-id="a848c-128">Make a note of the server **API Key**.</span></span> <span data-ttu-id="a848c-129">Далее мы выполним эти настройки в концентраторе уведомлений, чтобы активировать отправку push-уведомлений в GCM.</span><span class="sxs-lookup"><span data-stu-id="a848c-129">You will configure this in your notification hub next, to enable it to send push notifications to GCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="a848c-130"><a id="configure-hub"></a>Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="a848c-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="a848c-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="a848c-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="a848c-132">В колонке **Параметры** щелкните **Службы уведомлений**, а затем — **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="a848c-132">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="a848c-133">Введите ключ API и сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="a848c-133">Enter the API key and save.</span></span>

&emsp;&emsp;![Центры уведомлений Azure — Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="a848c-135"><a id="connect-app"></a>Подключение приложения Chrome к концентратору уведомлений</span><span class="sxs-lookup"><span data-stu-id="a848c-135"><a id="connect-app"></a>Connect your Chrome App to the notification hub</span></span>
<span data-ttu-id="a848c-136">Теперь центр уведомлений настроен для работы с GCM, а у вас есть строки подключения, с помощью которых вы можете зарегистрировать приложение для получения и отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a848c-136">Your notification hub is now configured to work with GCM, and you have the connection strings to register your app to both receive and send push notifications.</span></span> <span data-ttu-id="a848c-137">LK</span><span class="sxs-lookup"><span data-stu-id="a848c-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="a848c-138">Создание нового приложения Chrome</span><span class="sxs-lookup"><span data-stu-id="a848c-138">Create a new Chrome App</span></span>
<span data-ttu-id="a848c-139">Пример ниже основан на [образце использования службы GCM для приложения Chrome]. В нем приведен рекомендуемый способ создания приложения Chrome.</span><span class="sxs-lookup"><span data-stu-id="a848c-139">The sample below is based on the [Chrome App GCM Sample] and uses the recommended way to create a Chrome App.</span></span> <span data-ttu-id="a848c-140">В разделах ниже описаны действия, связанные с Центрами уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="a848c-140">We will highlight the steps specifically related to Azure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="a848c-141">Мы рекомендуем скачать источник для этого приложения Chrome со страницы [Образец использования концентратора уведомлений с приложением Chrome].</span><span class="sxs-lookup"><span data-stu-id="a848c-141">We recommend that you download the source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="a848c-142">Для создания приложения Chrome используется код JavaScript, который можно создать в любом текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="a848c-142">The Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="a848c-143">Приложение Chrome будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="a848c-143">Below is what this Chrome App will look like.</span></span>

![Приложение Google Chrome][15]

1. <span data-ttu-id="a848c-145">Создайте папку с именем `ChromePushApp`.</span><span class="sxs-lookup"><span data-stu-id="a848c-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="a848c-146">Вы можете присвоить ей другое имя, но в таком случае необходимо изменить путь в соответствующих сегментах кода.</span><span class="sxs-lookup"><span data-stu-id="a848c-146">Of course, the name is arbitrary - if you name it something different, make sure you substitute the path in the required code segments.</span></span>
2. <span data-ttu-id="a848c-147">Скачайте [библиотеку crypto-js] в папку, созданную на втором шаге.</span><span class="sxs-lookup"><span data-stu-id="a848c-147">Download the [crypto-js library] in the folder you created in the second step.</span></span> <span data-ttu-id="a848c-148">В этой папке библиотеки будут содержаться две вложенные папки: `components` и `rollups`.</span><span class="sxs-lookup"><span data-stu-id="a848c-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="a848c-149">Создайте файл `manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="a848c-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="a848c-150">Все приложения Chrome сохраняются с помощью файла манифеста, в котором содержатся метаданные приложения и, самое главное, все предоставленные для него разрешения при установке.</span><span class="sxs-lookup"><span data-stu-id="a848c-150">All Chrome Apps are backed by a manifest file that contains the app metadata and, most importantly, all permissions that are granted to the app when the user installs it.</span></span>
   
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
   
    <span data-ttu-id="a848c-151">Обратите внимание на элемент `permissions` , который указывает, что это приложение Chrome сможет получать push-уведомления от GCM.</span><span class="sxs-lookup"><span data-stu-id="a848c-151">Notice the `permissions` element, which specifies that this Chrome App will be able to receive push notifications from GCM.</span></span> <span data-ttu-id="a848c-152">Кроме того, он должен содержать универсальный код ресурса (URI) Центров уведомлений Azure, по которому приложение Chrome будет вызывать REST для регистрации.</span><span class="sxs-lookup"><span data-stu-id="a848c-152">It must also specify the Azure Notification Hubs URI where the Chrome App will make a REST call to register.</span></span>
    <span data-ttu-id="a848c-153">В нашем примере приложения также используется файл значка `gcm_128.png`, который можно найти в источнике, многократно используемом из исходного образца GCM.</span><span class="sxs-lookup"><span data-stu-id="a848c-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at the source that's reused from the original GCM sample.</span></span> <span data-ttu-id="a848c-154">Его можно заменить на любое другое изображение, которое соответствует [критериям значка](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="a848c-154">You can substitute it for any image that fits the [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="a848c-155">Создайте файл с именем `background.js` с помощью указанного ниже кода.</span><span class="sxs-lookup"><span data-stu-id="a848c-155">Create a file called `background.js` with the following code:</span></span>
   
        // Returns a new notification ID used in the notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs to form a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification to show the GCM message.
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
   
        // Set up listeners to trigger the first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="a848c-156">Это файл, в котором всплывает HTML-код окна приложения Chrome (**register.html**) и который определяет обработчик **messageReceived** для обработки входящего push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="a848c-156">This is the file that pops up the Chrome App window HTML (**register.html**) and also defines the handler **messageReceived** to handle the incoming push notification.</span></span>
5. <span data-ttu-id="a848c-157">Создайте файл с именем `register.html` , который определяет пользовательский интерфейс приложения Chrome.</span><span class="sxs-lookup"><span data-stu-id="a848c-157">Create a file called `register.html` - this defines the UI of the Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="a848c-158">В этом образце используется **CryptoJS 3.1.2**.</span><span class="sxs-lookup"><span data-stu-id="a848c-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="a848c-159">Если вы скачали другую версию библиотеки, измените версию в пути `src` .</span><span class="sxs-lookup"><span data-stu-id="a848c-159">If you downloaded another version of the library, make sure you properly substitute the version in the `src` path.</span></span>
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
6. <span data-ttu-id="a848c-160">Создайте файл `register.js` , используя указанный ниже код.</span><span class="sxs-lookup"><span data-stu-id="a848c-160">Create a file called `register.js` with the code below.</span></span> <span data-ttu-id="a848c-161">Этот файл определяет скрипт, лежащий в основе `register.html`.</span><span class="sxs-lookup"><span data-stu-id="a848c-161">This file specifies the script behind `register.html`.</span></span> <span data-ttu-id="a848c-162">Приложения Chrome не предусматривают встроенное выполнение, поэтому необходимо создать отдельный резервный сценарий для пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a848c-162">Chrome Apps do not allow inline execution, so you have to create a separate backing script for your UI.</span></span>
   
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
   
          // Prevent register button from being clicked again before the registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When the registration fails, handle the error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that the first-time registration is done.
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
   
          // Update the payload with the registration ID obtained earlier.
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
   
    <span data-ttu-id="a848c-163">В приведенном выше сценарии есть следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="a848c-163">The above script has the following key parameters:</span></span>
   
   * <span data-ttu-id="a848c-164">**window.onload** определяет события, которые происходят при нажатии каждой из двух кнопок в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="a848c-164">**window.onload** defines the button-click events of the two buttons on the UI.</span></span> <span data-ttu-id="a848c-165">Одна кнопка запускает регистрацию в GCM, а другая использует полученный после регистрации в GCM идентификатор для регистрации в центрах уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="a848c-165">One registers with GCM, and the other uses the registration ID that's returned after registration with GCM to register with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="a848c-166">**updateLog** — это функция, которая позволяет обрабатывать простые операции ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="a848c-166">**updateLog** is the function that allows us to handle simple logging capabilities.</span></span>
   * <span data-ttu-id="a848c-167">**registerWithGCM** — это обработчик нажатия первой кнопки, выполняющий вызов `chrome.gcm.register` в GCM, чтобы зарегистрировать текущий экземпляр приложения Chrome.</span><span class="sxs-lookup"><span data-stu-id="a848c-167">**registerWithGCM** is the first button-click handler, which makes the `chrome.gcm.register` call to GCM to register the current Chrome App instance.</span></span>
   * <span data-ttu-id="a848c-168">**registerCallback** — это функция обратного вызова, которая вызывается при возврате вызова регистрации в GCM.</span><span class="sxs-lookup"><span data-stu-id="a848c-168">**registerCallback** is the callback function that gets called when the GCM registration call returns.</span></span>
   * <span data-ttu-id="a848c-169">**registerWithNH** — это обработчик нажатия второй кнопки, который выполняет регистрацию в Центрах уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a848c-169">**registerWithNH** is the second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="a848c-170">Он получает значения `hubName` и `connectionString` (которые указал пользователь) и вызывает REST API для регистрации в Центре уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a848c-170">It gets `hubName` and `connectionString` (which the user has specified) and crafts the Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="a848c-171">**splitConnectionString** и **generateSaSToken** — это вспомогательные приложения для создания маркера SaS с помощью JavaScript. Этот маркер должен использоваться при каждом вызове REST API.</span><span class="sxs-lookup"><span data-stu-id="a848c-171">**splitConnectionString** and **generateSaSToken** are helpers that represent the JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="a848c-172">Дополнительные сведения см. в статье [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx) (Основные понятия).</span><span class="sxs-lookup"><span data-stu-id="a848c-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="a848c-173">**sendNHRegistrationRequest** — это функция, вызывающая HTTP REST в Центрах уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="a848c-173">**sendNHRegistrationRequest** is the function that makes a HTTP REST call to Azure Notification Hubs.</span></span>
   * <span data-ttu-id="a848c-174">**registrationPayload** определяет полезные XML-данные регистрации.</span><span class="sxs-lookup"><span data-stu-id="a848c-174">**registrationPayload** defines the registration XML payload.</span></span> <span data-ttu-id="a848c-175">Дополнительные сведения см. в статье [Create Registration NH REST API]. (Создание REST API Центра уведомлений для регистрации).</span><span class="sxs-lookup"><span data-stu-id="a848c-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="a848c-176">Здесь мы обновляем идентификатор регистрации, используя полученные из GCM данные.</span><span class="sxs-lookup"><span data-stu-id="a848c-176">We update the registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="a848c-177">**client** — это экземпляр **XMLHttpRequest**, используемый для выполнения запроса HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a848c-177">**client** is an instance of **XMLHttpRequest** that we use to make the HTTP POST request.</span></span> <span data-ttu-id="a848c-178">Обратите внимание, что мы обновляем заголовок `Authorization` с помощью `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="a848c-178">Note that we update the `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="a848c-179">Если этот вызов будет выполнен успешно, этот экземпляр приложения Chrome будет зарегистрирован в центре уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="a848c-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="a848c-180">Общая структура папок для этого проекта должна выглядеть следующим образом. ![Приложение Google Chrome — структура папок][21]</span><span class="sxs-lookup"><span data-stu-id="a848c-180">The overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="a848c-181">Настройка и тестирование приложения Chrome</span><span class="sxs-lookup"><span data-stu-id="a848c-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="a848c-182">Откройте браузер Chrome.</span><span class="sxs-lookup"><span data-stu-id="a848c-182">Open your Chrome browser.</span></span> <span data-ttu-id="a848c-183">Откройте окно **Расширения** и установите флажок **Режим разработчика**.</span><span class="sxs-lookup"><span data-stu-id="a848c-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="a848c-184">Нажмите кнопку **Load unpacked extension** (Скачать распакованное расширение) и перейдите к папке, в которой вы создали файлы.</span><span class="sxs-lookup"><span data-stu-id="a848c-184">Click **Load unpacked extension** and navigate to the folder where you created the files.</span></span> <span data-ttu-id="a848c-185">При необходимости можно также использовать средство **Chrome Apps & Extensions Developer Tool**.</span><span class="sxs-lookup"><span data-stu-id="a848c-185">You can also optionally use the **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="a848c-186">Это средство само по себе является приложением Chrome (оно устанавливается из веб-магазина Chrome), предоставляющим дополнительные возможности отладки для разработки приложений Chrome.</span><span class="sxs-lookup"><span data-stu-id="a848c-186">This tool is a Chrome App in itself (installed from the Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="a848c-187">Если ошибки создания отсутствуют, вы увидите свое приложение Chrome.</span><span class="sxs-lookup"><span data-stu-id="a848c-187">If the Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="a848c-188">Введите в поле Sender ID (Идентификатор отправителя) **номер проекта**, полученный ранее из **консоли Google Cloud**, а затем щелкните **Register with GCM** (Зарегистрировать в GCM).</span><span class="sxs-lookup"><span data-stu-id="a848c-188">Enter the **Project Number** that you got earlier from the **Google Cloud Console** as the sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="a848c-189">Должно появиться сообщение **Registration with GCM succeeded**</span><span class="sxs-lookup"><span data-stu-id="a848c-189">You must see the message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="a848c-190">Введите имя в поле **Notification Hub Name** (Имя Центра уведомлений) и значение **DefaultListenSharedAccessSignature**, полученное ранее на портале, а затем щелкните **Register with Azure Notification Hub** (Зарегистрировать в Центре уведомлений Azure).</span><span class="sxs-lookup"><span data-stu-id="a848c-190">Enter your **Notification Hub Name** and the **DefaultListenSharedAccessSignature** that you obtained from the portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="a848c-191">Должно появиться сообщение **Notification Hub Registration successful!**</span><span class="sxs-lookup"><span data-stu-id="a848c-191">You must see the message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="a848c-192">(Регистрация в концентраторе уведомлений выполнена успешно) и данные ответа о регистрации, в которых содержится идентификатор регистрации в Центрах уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="a848c-192">and the details of the registration response, which contains the Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="a848c-193"><a name="send"></a>Отправка уведомления в приложение Chrome</span><span class="sxs-lookup"><span data-stu-id="a848c-193"><a name="send"></a>Send a notification to your Chrome App</span></span>
<span data-ttu-id="a848c-194">Для тестирования мы отправим push-уведомления Chrome с помощью консольного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="a848c-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="a848c-195">Push-уведомления можно отправлять с помощью Центров уведомлений с любого сервера через общедоступный <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">интерфейс REST</a>.</span><span class="sxs-lookup"><span data-stu-id="a848c-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="a848c-196">Больше примеров, включающих использование разных платформ, можно найти на [портале документации](https://azure.microsoft.com/documentation/services/notification-hubs/) .</span><span class="sxs-lookup"><span data-stu-id="a848c-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="a848c-197">В Visual Studio откройте меню **Файл** и выберите **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="a848c-197">In Visual Studio, from the **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="a848c-198">В разделе **Visual C#** щелкните **Windows** и **Консольное приложение**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a848c-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="a848c-199">Это создаст новый проект консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="a848c-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="a848c-200">В меню **Инструменты** щелкните **Library Package Manager** (Диспетчер пакетов библиотеки) и **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="a848c-200">From the **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="a848c-201">Отобразится консоль диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="a848c-201">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="a848c-202">В окне консоли выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a848c-202">In the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference to the Azure Service Bus SDK with the <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="a848c-203">Откройте файл `Program.cs` и добавьте следующую инструкцию `using`:</span><span class="sxs-lookup"><span data-stu-id="a848c-203">Open `Program.cs` and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="a848c-204">Добавьте в класс `Program` следующий метод:</span><span class="sxs-lookup"><span data-stu-id="a848c-204">In the `Program` class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace the connection string placeholder with the connection string called `DefaultFullSharedAccessSignature` that you obtained in the notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="a848c-205">Обязательно используйте строку подключения с **полным** доступом, а не доступом к **прослушиванию**.</span><span class="sxs-lookup"><span data-stu-id="a848c-205">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="a848c-206">Строка подключения с доступом к **прослушиванию** не предоставляет разрешения для отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a848c-206">The **Listen** access connection string does not grant permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="a848c-207">Добавьте в метод `Main` следующие вызовы:</span><span class="sxs-lookup"><span data-stu-id="a848c-207">Add the following calls in the `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="a848c-208">Убедитесь, что браузер Chrome запущен, и запустите консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="a848c-208">Make sure that Chrome is running, and run the console application.</span></span>
8. <span data-ttu-id="a848c-209">На рабочем столе должно появиться следующее всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="a848c-209">You should see the following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="a848c-210">Кроме того, вы можете просмотреть все уведомления в окне уведомлений Chrome, которое можно открыть в запущенном браузере Chrome на панели задач (в ОС Windows).</span><span class="sxs-lookup"><span data-stu-id="a848c-210">You can also see all your notifications by using the Chrome Notifications window in the taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="a848c-211">При этом в нем не должно быть запущено или открыто приложение Chrome (хотя сам браузер Chrome должен быть запущен).</span><span class="sxs-lookup"><span data-stu-id="a848c-211">You don't need to have the Chrome App running or open in the browser (though the Chrome browser itself must be running).</span></span> <span data-ttu-id="a848c-212">В окне уведомлений Chrome можно увидеть обобщенное представление всех уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a848c-212">You also get a consolidated view of all your notifications in the Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="a848c-213"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a848c-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="a848c-214">Дополнительные сведения о Центрах уведомлений см. в статье [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET].</span><span class="sxs-lookup"><span data-stu-id="a848c-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="a848c-215">Дополнительные сведения о том, как ориентироваться на определенных пользователей, см. в статье [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET].</span><span class="sxs-lookup"><span data-stu-id="a848c-215">To target specific users, refer to the [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="a848c-216">Дополнительные сведения о том, как разделить пользователей по группам интересов, см. в статье [Использование Центров уведомлений Azure для передачи экстренных новостей].</span><span class="sxs-lookup"><span data-stu-id="a848c-216">If you want to segment your users by interest groups, you can follow the [Azure Notification Hubs breaking news] tutorial.</span></span>

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
<span data-ttu-id="a848c-217">[Образец использования концентратора уведомлений с приложением Chrome]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps</span><span class="sxs-lookup"><span data-stu-id="a848c-217">[Chrome App Notification Hub Sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps</span></span>
<span data-ttu-id="a848c-218">[консоли Google Cloud]: http://cloud.google.com/console</span><span class="sxs-lookup"><span data-stu-id="a848c-218">[Google Cloud Console]: http://cloud.google.com/console</span></span>
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="a848c-219">[Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="a848c-219">[Notification Hubs Overview]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="a848c-220">[Обзор приложений Chrome]: https://developer.chrome.com/apps/about_apps</span><span class="sxs-lookup"><span data-stu-id="a848c-220">[Chrome Apps Overview]: https://developer.chrome.com/apps/about_apps</span></span>
<span data-ttu-id="a848c-221">[образце использования службы GCM для приложения Chrome]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications</span><span class="sxs-lookup"><span data-stu-id="a848c-221">[Chrome App GCM Sample]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications</span></span>
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
<span data-ttu-id="a848c-222">[Приложения Chrome на мобильных устройствах]: https://developer.chrome.com/apps/chrome_apps_on_mobile</span><span class="sxs-lookup"><span data-stu-id="a848c-222">[Chrome Apps on Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile</span></span>
<span data-ttu-id="a848c-223">[Create Registration NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx</span><span class="sxs-lookup"><span data-stu-id="a848c-223">[Create Registration NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx</span></span>
<span data-ttu-id="a848c-224">[библиотеку crypto-js]: http://code.google.com/p/crypto-js/</span><span class="sxs-lookup"><span data-stu-id="a848c-224">[crypto-js library]: http://code.google.com/p/crypto-js/</span></span>
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
<span data-ttu-id="a848c-225">[Google Cloud Messaging для Chrome]: https://developer.chrome.com/apps/cloudMessagingV1</span><span class="sxs-lookup"><span data-stu-id="a848c-225">[Google Cloud Messaging for Chrome]: https://developer.chrome.com/apps/cloudMessagingV1</span></span>
<span data-ttu-id="a848c-226">[Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="a848c-226">[Azure Notification Hubs Notify Users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="a848c-227">[Использование Центров уведомлений Azure для передачи экстренных новостей]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="a848c-227">[Azure Notification Hubs breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
