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
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a>Отправка push приложений tooChrome уведомлений с концентраторами уведомлений Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

В этом разделе показано, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa Chrome приложение, которое будет отображаться в контексте hello hello браузера Google Chrome. В этом руководстве мы создадим приложение Chrome, которое получает push-уведомления с помощью [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/). 

> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).
> 
> 

Hello учебник поможет выполнить следующие основные шаги tooenable push-уведомлений:

* [Включение Google Cloud Messaging](#register)
* [Настройка концентратора уведомлений](#configure-hub)
* [Концентратор уведомлений приложение Chrome toohello подключения](#connect-app)
* [Отправка push уведомления tooyour Chrome приложения](#send)
* [Дополнительные функции и возможности](#next-steps)

> [!NOTE]
> Push-уведомлений приложения Chrome не универсальный уведомления в браузере — это модель расширяемости конкретных toohello браузера (см. [Обзор приложений Chrome] подробные сведения). В дополнение к этому toohello браузер для настольных компьютеров, Chrome приложения выполняются на мобильном устройстве (Android и iOS) через Apache Cordova. В разделе [Chrome приложений на мобильном устройстве] toolearn дополнительные.
> 
> 

Настройка GCM и концентраторов уведомлений Azure — идентичные tooconfiguring для Android, так как [Google Cloud Messaging для Chrome] является устаревшим и hello же GCM теперь поддерживает устройства Android и хром экземпляров.

## <a id="register"></a>Включение Google Cloud Messaging
1. Перейдите toohello [облачной консоли Google] веб-сайта, войдите с помощью учетной записи Google и нажмите кнопку hello **Создание проекта** кнопки. Укажите соответствующий **имя проекта**и нажмите кнопку hello **создать** кнопки.
   
       ![Google Cloud Console - Create Project][1]
2. Запишите hello **номер проекта** на hello **проекты** страницы для hello проекта, который вы только что создали. Это будет использоваться в качестве hello **идентификатор отправителя GCM** в tooregister Chrome приложения hello с GCM.
   
       ![Google Cloud Console - Project Number][2]
3. Hello левой панели щелкните **API-интерфейсы & auth**, затем прокрутите вниз и нажмите кнопку переключателя tooenable hello **Google Cloud Messaging для Android**. Нет tooenable **Google Cloud Messaging для Chrome**.
   
       ![Google Cloud Console - Server Key][3]
4. Hello левой панели щелкните **учетные данные** > **создать новый ключ** > **ключа сервера** > **создать**.
   
       ![Google Cloud Console - Credentials][4]
5. Запишите hello server **ключ API**. Вы настроите это ваш tooenable Далее, концентратор уведомлений его tooGCM уведомления toosend push.
   
       ![Google Cloud Console - API Key][5]

## <a id="configure-hub"></a>Настройка концентратора уведомлений
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   В hello **параметры** колонке выберите **служб Notification Services** и затем **Google (GCM)**. Введите ключ API hello и сохранить.

&emsp;&emsp;![Центры уведомлений Azure — Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <a id="connect-app"></a>Концентратор уведомлений приложение Chrome toohello подключения
Концентратор уведомлений теперь настроенных toowork с GCM, и у вас есть hello tooregister строки подключения вашего приложения tooboth получения и отправки извещающих уведомлений. LK

### <a name="create-a-new-chrome-app"></a>Создание нового приложения Chrome
Образец Hello ниже основан на hello [пример GCM приложения Chrome] и использует hello рекомендуется toocreate способом приложения Chrome. TooAzure специально связанные действия hello концентраторы уведомлений будут выделены. 

> [!NOTE]
> Мы рекомендуем загрузить hello источника для этого приложения Chrome из [пример концентратора уведомлений приложения Chrome].
> 
> 

Hello Chrome приложение создается с помощью JavaScript и любой из редакторов Ваш предпочитаемый word можно использовать для его создания. Приложение Chrome будет выглядеть следующим образом.

![Приложение Google Chrome][15]

1. Создайте папку с именем `ChromePushApp`. Конечно, произвольное имя hello - Если присвоить файлу имя, чем-то другим, убедитесь, что можно заменить путем hello в сегменты кода hello требуется.
2. Загрузите hello [библиотеки шифрования js] в hello папку, созданную на втором шаге hello. В этой папке библиотеки будут содержаться две вложенные папки: `components` и `rollups`.
3. Создайте файл `manifest.json` . Все приложения Chrome, поддерживаемых файл манифеста, содержащий метаданные приложения hello и большинство того, все разрешения, предоставленные toohello приложения при hello пользователь устанавливает его.
   
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
   
    Обратите внимание hello `permissions` элемент, который указывает, что это приложение Chrome будет может tooreceive push-уведомления в GCM. Также необходимо указать URI концентраторов уведомлений Azure, где hello Chrome приложение сделает вызов REST tooregister hello.
    Наш пример приложения также использует файл значка `gcm_128.png`, можно найти в источнике hello повторно из исходного GCM образца hello. Его можно заменить на любое изображение, которое соответствует hello [критерии значок](https://developer.chrome.com/apps/manifest/icons).
4. Создайте файл с именем `background.js` с hello, следующий код:
   
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
   
    Это файл hello, всплывает окно Chrome приложения hello HTML (**register.html**) и также определяет обработчик hello **messageReceived** toohandle hello входящих push-уведомлений.
5. Создайте файл с именем `register.html` -это определяет пользовательский Интерфейс hello Chrome приложения hello. 
   
   > [!NOTE]
   > В этом образце используется **CryptoJS 3.1.2**. Если вы загрузили другую версию библиотеки hello, убедитесь, что вы правильно заменить версию hello в hello `src` пути.
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
6. Создайте файл с именем `register.js` hello код, приведенный ниже. Этот файл содержит скрипт hello за `register.html`. Chrome приложения не допускают встроенного выполнения, их необходимо toocreate отдельные резервного скрипта для пользовательского интерфейса.
   
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
   
    Hello выше сценарий имеет следующие ключевые параметры hello.
   
   * **Window.onload** определяет события нажатия кнопки hello hello двух кнопок на hello пользовательского интерфейса. Один регистрируется GCM и других hello использует идентификатор регистрации hello, возвращаемое после регистрации GCM tooregister с концентраторами уведомлений Azure.
   * **updateLog** — hello функция, которая позволяет нам toohandle простой протоколирования.
   * **registerWithGCM** первого нажатия кнопки обработчика hello, благодаря чему hello `chrome.gcm.register` tooGCM tooregister hello текущего приложения Chrome экземпляра вызова.
   * **registerCallback** — hello функция обратного вызова, который вызывается при возвращении вызова регистрации GCM hello.
   * **registerWithNH** — hello второй обработчик щелчка кнопки, который регистрируется с помощью концентраторов уведомлений. Он возвращает `hubName` и `connectionString` (какие hello пользователь указал) и создается hello вызова интерфейса API REST регистрации концентраторов уведомлений.
   * **splitConnectionString** и **generateSaSToken** — это вспомогательные средства представляют реализация JavaScript hello процесса создания маркера SaS, который должен использоваться во всех вызовах API-интерфейса REST. Дополнительные сведения см. в статье [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx) (Основные понятия).
   * **sendNHRegistrationRequest** это вызов функции hello, который делает HTTP REST tooAzure концентраторов уведомлений.
   * **registrationPayload** определяет полезные данные XML регистрации hello. Дополнительные сведения см. в статье [Create Registration NH REST API]. (Создание REST API Центра уведомлений для регистрации). Мы дополнить код регистрации hello в нем был получен из GCM.
   * **клиент** является экземпляром класса **XMLHttpRequest** , мы используем toomake hello HTTP-запроса POST. Обратите внимание, что мы изменить hello `Authorization` заголовок с `sasToken`. Если этот вызов будет выполнен успешно, этот экземпляр приложения Chrome будет зарегистрирован в центре уведомлений Azure.

Hello общую структуру папок для этого проекта должен выглядеть примерно следующим образом: ![приложение Google Chrome - структура папок][21]

### <a name="set-up-and-test-your-chrome-app"></a>Настройка и тестирование приложения Chrome
1. Откройте браузер Chrome. Откройте окно **Расширения** и установите флажок **Режим разработчика**.
   
       ![Google Chrome - Enable Developer Mode][16]
2. Нажмите кнопку **загрузить распаковано расширение** и перейдите в папку toohello, где были созданы файлы hello. Можно также использовать hello **Chrome приложений и средства разработчика расширения**. Этот инструмент представляет собой приложение и хром само по себе (установлен hello Chrome веб-хранилище) и предоставляет расширенные возможности отладки для разработки приложений Chrome.
   
       ![Google Chrome - Load Unpacked Extension][17]
3. Если hello Chrome приложения создается без ошибок, вы увидите отображаться Chrome приложения.
   
       ![Google Chrome - Chrome App Display][18]
4. Введите hello **номер проекта** , полученный ранее из hello **облачной консоли Google** идентификатор отправителя hello и нажмите кнопку **регистрации GCM**. Должно появиться сообщение hello **регистрации GCM успешно выполнен.**
   
       ![Google Chrome - Chrome App Customization][19]
5. Введите ваш **имя концентратора уведомлений** и hello **DefaultListenSharedAccessSignature** , полученный из портала hello ранее и нажмите кнопку **регистрации в концентратор уведомлений Azure**. Должно появиться сообщение hello **регистрации концентратор уведомлений успешно!** а hello подробные сведения о регистрации ответ hello, который содержит hello регистрации концентраторов уведомлений Azure по идентификатору.
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <a name="send"></a>Отправлять уведомления tooyour Chrome приложения
Для тестирования мы отправим push-уведомления Chrome с помощью консольного приложения .NET. 

> [!NOTE]
> Push-уведомления можно отправлять с помощью Центров уведомлений с любого сервера через общедоступный <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">интерфейс REST</a>. Больше примеров, включающих использование разных платформ, можно найти на [портале документации](https://azure.microsoft.com/documentation/services/notification-hubs/) .
> 
> 

1. В Visual Studio, из hello **файл** последовательно выберите пункты **New** и затем **проекта**. В разделе **Visual C#** щелкните **Windows** и **Консольное приложение**, а затем нажмите кнопку **ОК**.  Это создаст новый проект консольного приложения.
2. Из hello **средства** меню, нажмите кнопку **диспетчер пакетов библиотеки** и затем **консоль диспетчера пакетов**. Откроется консоль диспетчера пакетов hello.
3. В окне консоли hello выполните следующую команду hello:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. Откройте `Program.cs` и добавьте следующее hello `using` инструкции:
   
        using Microsoft.Azure.NotificationHubs;
5. В hello `Program` добавьте следующий метод hello:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > Убедитесь, что используются hello строки подключения с **полного** доступ, не **прослушивания** доступа. Hello **прослушивания** строку подключения доступа не предоставляет разрешений toosend push-уведомлений.
   > 
   > 
6. Добавьте следующие hello вызовы в hello `Main` метод:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Убедитесь, что запущен Chrome и запустите консольное приложение hello.
8. Вы увидите следующее hello уведомления всплывающее окно на рабочем столе.
   
       ![Google Chrome - Notification][13]
9. Можно также просмотреть все уведомления с помощью окно уведомления Chrome hello в панели задач hello (в Windows) при выполнении Chrome.
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> Не нужно toohave hello Chrome приложение работает или открыть в браузере hello (хотя должна быть запущена самим браузером hello Chrome). Можно также получить консолидированное представление всех уведомлений в окно приветствия Chrome уведомления.
> 
> 

## <a name="next-steps"> </a>Дальнейшие действия
Дополнительные сведения о Центрах уведомлений см. в статье [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET].

tootarget конкретных пользователей, см. toohello [Azure концентраторы уведомлений уведомить пользователей] учебника. 

Если требуется toosegment пользователи, группы интересов, можно выполнить hello [концентраторов уведомлений Azure, новости] учебника.

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
