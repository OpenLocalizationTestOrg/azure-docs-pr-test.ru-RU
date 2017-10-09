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
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a>Добавление приложения Apache Cordova tooyour уведомлений push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Обзор
В этом учебнике добавлении проекта toohello [Apache Cordova краткого] принудительной уведомления, чтобы каждый раз при вставке записи push-уведомление отправляется toohello устройства.

Если вы не используете hello загружен быстрый запуск сервера проекта, требуется hello пакета расширения уведомлений push. Дополнительные сведения см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure][1].

## <a name="prerequisites"></a>Предварительные требования
В этом учебнике приложению Apache Cordova, разработанных с помощью Visual Studio 2015, который выполняется на hello эмулятор Android Google, устройство Android, устройства Windows и устройства iOS.

toocomplete этого учебника, необходимо:

* ПК с [Visual Studio Community 2015][2] или более поздней версии;
* [набор средств Visual Studio для Apache Cordova][4];
* [активная учетная запись Azure][3];
* завершенный [ознакомительный проект Apache Cordova][5];
* для Android: [учетная запись Google][6] с подтвержденным адресом электронной почты;
* для iOS: [участие в программе разработки решений для Apple][7] и устройство iOS (симулятор iOS не поддерживает push-уведомления);
* для Windows: [учетная запись разработчика приложений для Магазина Windows][8] и устройство Windows 10.

## <a name="configure-hub"></a>Настройка концентратора уведомлений
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

[Просмотрите видео, в котором показаны действия, описанные в этом разделе.][9]

## <a name="update-hello-server-project"></a>Обновление проекта в project server hello
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="add-push-to-app"></a>Изменение приложения Cordova
Убедитесь, что готовы toohandle push-уведомлений по установке подключаемого модуля Cordova принудительной hello, а также любые службы, специфический для платформы push проекта приложения Apache Cordova.

#### <a name="update-hello-cordova-version-in-your-project"></a>Обновите версию Cordova hello в своем проекте.
Если проект использует версию Apache Cordova более ранних, чем v6.1.1, обновите hello клиентский проект. проект hello tooupdate:

* Щелкните правой кнопкой мыши `config.xml` конструктор конфигурации tooopen hello.
* Перейдите на вкладку платформы hello.
* Выберите 6.1.1 в hello **Cordova CLI** текстовое поле.
* Выберите **построения**, затем **построить решение** tooupdate hello проекта.

#### <a name="install-hello-push-plugin"></a>Установите подключаемый модуль принудительной hello
Приложения Apache Cordova не обрабатывают возможностей устройства или сети изначально.  Эти возможности обеспечиваются подключаемыми модулями, которые публикуются в [npm][10] или на портале GitHub.  Hello `phonegap-plugin-push` подключаемый модуль — push-уведомлений используется toohandle сети.

Подключаемый модуль принудительной hello можно установить одним из следующих способов:

**Из hello командной строки:**

Выполните следующую команду hello:

    cordova plugin add phonegap-plugin-push

**в Visual Studio:**

1. В обозревателе решений откройте hello `config.xml` файла щелкните **подключаемые модули** > **настраиваемый**выберите **Git** в качестве источника установки, затем введите `https://github.com/phonegap/phonegap-plugin-push`как источник hello.

   ![][img1]

2. Выберите источник установки Далее toohello hello стрелка.
3. В **SENDER_ID**, если уже имеется код числовых проекта для проекта Google Developer Console hello, можно добавить его здесь. В противном случае введите значение заполнителя, например 777777.  Если планируется использовать устройство Android, это значение можно позже обновить в файле config.xml.
4. Щелкните **Добавить**.

установлен подключаемый модуль принудительной Hello.

#### <a name="install-hello-device-plugin"></a>Установите подключаемый модуль hello устройства
Выполните hello же процедуру, используемую hello tooinstall push-подключаемого модуля.  Добавить подключаемый модуль hello устройство из списка подключаемых модулей hello Core (щелкните **подключаемые модули** > **Core** toofind его). Необходимо, чтобы это имя платформы hello tooobtain подключаемого модуля.

#### <a name="register-your-device-on-application-start-up"></a>Регистрация устройства при запуске приложения
Сначала мы добавим минимальный требуемый код для Android. Более поздней версии измените toorun приложения hello, iOS или Windows 10.

1. Добавьте вызов слишком**registerForPushNotifications** во время обратного вызова hello для процесса входа в систему hello или внизу hello hello **onDeviceReady** метод:

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

    В этом примере показан вызов метода **registerForPushNotifications** после успешной проверки подлинности.  Метод `registerForPushNotifications()` можно вызывать каждый раз при необходимости.

2. Добавить новый hello **registerForPushNotifications** метод следующим образом:

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
3. (Android) В предыдущих кода hello, замените `Your_Project_ID` с числового hello project ID для приложения из [Google Developer Console][18].

## <a name="optional-configure-and-run-hello-app-on-android"></a>(Необязательно) Настройка и запуск приложения hello в Android
Выполните этот раздел tooenable push-уведомления для Android.

#### <a name="enable-gcm"></a>Включение Firebase Cloud Messaging
Поскольку изначально мы ожидаем hello Google Android платформы, необходимо включить Firebase Cloud Messaging.

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <a name="configure-backend"></a>Настройка hello мобильное приложение серверной toosend принудительной запросы с помощью FCM
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a>Настройка приложения Cordova для Android
В приложении Cordova откройте файл config.xml и замените `Your_Project_ID` с числового hello project ID для приложения hello [Google Developer Console][18].

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

Откройте index.js и обновите toouse кода hello свой идентификатор числовых проекта.

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <a name="configure-device"></a>Настройка устройства Android для отладочного режима USB
Перед развертыванием вашего приложения tooyour устройства Android необходимо tooenable отладка по USB.  На телефоне Android выполните следующие действия:

1. Go слишком**параметры** > **о телефоне**, затем коснитесь hello **номер построения** режим разработчика включен (около семь раз).
2. В **параметры** > **параметров разработчика** включить **отладка по USB**, телефоне Android tooyour Компьютере разработки, подключитесь с помощью кабеля USB.

Мы проверили этот способ, используя устройство Google Nexus 5X с Android 6.0 (Marshmallow).  Однако hello методы являются общими для любой современной версии Android.

#### <a name="install-google-play-services"></a>Установка служб Google Play
Подключаемый модуль принудительной Hello зависит от Android службы Google Play для push-уведомлений.

1. В Visual Studio щелкните **средства** > **Android** > **диспетчер Android SDK Manager**, разверните hello **дополнения** папки и проверьте hello поле toomake каждого hello следующие пакеты SDK установлен.

   * Android 2.3 или более поздней версии.
   * Репозиторий Google версии 27 или более поздней.
   * Службы Google Play 9.0.2 или более поздней.

2. Нажмите кнопку **установки пакетов** и дождитесь toocomplete установки hello.

Hello текущего необходимых библиотек, перечислены в hello [phonegap-plugin принудительной установки документации][19].

#### <a name="test-push-notifications-in-hello-app-on-android"></a>Тест push-уведомлений в приложения hello на Android
Теперь можно hello тестового push-уведомлений, запустив приложение и вставки элементов в таблице TodoItem hello. Вы можете проверить hello одного устройства или из второго устройства, при условии, что вы используете hello же серверной части. Проверка приложения Cordova на платформе Android hello в одном из следующих способов hello:

* **На физическом устройстве:** присоединить компьютер разработки tooyour устройства Android с помощью кабеля USB.  Вместо **Эмулятор Google Android** выберите **Устройство**. Visual Studio развертывает устройства toohello приложения hello и затем запускает приложение hello.  Затем вы можете взаимодействовать с hello приложения на устройстве hello.

  Усовершенствуйте интерфейс разработки.  В разработке приложения Android вам помогут приложения для демонстрации экрана, например [Mobizen][20].  Mobizen проектов веб-браузере tooa Android экрана на ПК.

* **На эмуляторе Android.** Для запуска в эмуляторе необходимо выполнить дополнительную настройку.

    Убедитесь, что вы развертываете tooa виртуального устройства, имеющий интерфейсы API Google задать в качестве цели hello, как показано в диспетчере hello виртуального устройства Android (AVD).

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    Если требуется более быстрое x86 toouse эмулятор, вы [Установка драйвера HAXM hello] [ 11] и настроить эмулятор toouse hello его.

    Добавить устройство Android toohello учетной записи Google, щелкнув **приложения** > **параметры** > **добавьте учетную запись**, следуйте указаниям hello.

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    Запустите приложение hello todolist как перед и вставить новый элемент todo. На этот раз значок уведомления отображается в области уведомлений hello. Вы можете открыть hello уведомления лоток tooview hello полный текст hello уведомления.

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a>Настройка и запуск проекта в iOS (необязательно)
Этот раздел предназначен для запуска проекта Cordova hello на устройствах iOS. Пропустите этот раздел, если вы не работаете с устройствами iOS.

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a>Установки и выполнения hello iOS удаленный агент сборки Mac или облачные службы
Перед запуском приложения Cordova в iOS с помощью Visual Studio перейдите hello шагов hello [руководстве по установке iOS] [ 12] tooinstall и выполнения hello удаленный агент сборки.

Убедитесь в том, что можно построить приложение hello для операций ввода-вывода. Hello действия, описанные в руководстве по установке hello, требуется toobuild для iOS из Visual Studio. Если у вас компьютер Mac, вы можете создать для iOS с помощью hello удаленный агент сборки на службы, например MacInCloud. Дополнительные сведения см. в разделе [запуск приложения iOS в облаке hello][21].

> [!NOTE]
> XCode 7 или более поздней — необходимые toouse подключаемого модуля принудительной hello в iOS.

#### <a name="find-hello-id-toouse-as-your-app-id"></a>Найти идентификатор toouse hello как ваш код приложения
Прежде чем регистрировать приложение для push-уведомлений, откройте файл config.xml в приложения Cordova, найти hello `id` атрибута значение в элементе hello мини-приложения и скопируйте его для последующего использования. В следующий XML-код hello, является Идентификатором hello `io.cordova.myapp7777777`.

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

Вам потребуется использовать этот идентификатор при создании идентификатора приложения на портале разработчика Apple. При создании другой идентификатор приложения на портале для разработчиков hello далее в этом учебнике необходимо выполнить выполнить ряд дополнительных действий. Идентификатор Hello в элементе мини-приложение, должен соответствовать hello идентификатор приложения на портале разработчика hello.

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Регистрация приложения hello push-уведомления на портале для разработчиков Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[Видео, демонстрирующее аналогичные действия](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a>Настройка Azure toosend push-уведомлений
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a>Проверка, соответствует ли идентификатор приложения указанному в приложении Cordova
Если вы уже создали в учетной записи разработчика Apple идентификатор приложения hello совпадает с Идентификатором hello hello элемента мини-приложения в файле config.xml, этот шаг можно пропустить. Однако если идентификаторы hello не совпадают, потребоваться hello следующие шаги:

1. Удалите папку hello платформы из проекта.
2. Удалите папку hello подключаемые модули из проекта.
3. Удалите папки node_modules hello из проекта.
4. Обновите hello атрибута id элемента мини-приложение hello в файл config.xml toouse hello идентификатор приложения, который был создан в вашей учетной записи разработчика Apple.
5. Перестройте свой проект.

##### <a name="test-push-notifications-in-your-ios-app"></a>Тестирование push-уведомлений в приложении iOS
1. Убедитесь, что в Visual Studio **iOS** выбран в качестве цели развертывания hello, а затем выберите **устройства** toorun на iOS, подключенном устройстве.

    Можно запускать на tooyour подключенное устройство iOS ПК с помощью iTunes. Симулятор iOS Hello не поддерживает push-уведомлений.

2. Нажмите клавишу hello **запуска** кнопку или **F5** в Visual Studio toobuild проекта hello начала hello приложение на устройстве iOS, а затем нажмите **ОК** tooaccept push-уведомлений.

   > [!NOTE]
   > приложение Hello запрашивает подтверждение push-уведомления во время первого запуска hello.

3. В приложение hello введите задачу и нажмите кнопку hello плюс (+) значок.
4. Убедитесь, что принимается уведомления, затем нажмите кнопку ОК toodismiss hello уведомления.

## <a name="optional-configure-and-run-on-windows"></a>Настройка и запуск проекта в Windows (необязательно)
Этот раздел предназначен для запуска проекта приложения Apache Cordova hello на устройствах Windows 10 (подключаемый модуль принудительной PhoneGap hello поддерживается в Windows 10). Пропустите этот раздел, если вы не работаете с устройствами Windows.

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a>Регистрация приложения Windows для получения push-уведомлений с помощью WNS
Параметры хранилища toouse hello в Visual Studio выберите цель Windows из списка платформ решения hello, как **Windows x64** или **Windows x86** (избежать **Windows AnyCPU** push-уведомления).

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

[Просмотрите видео, демонстрирующее аналогичные действия][13]

#### <a name="configure-hello-notification-hub-for-wns"></a>Настройка концентратора уведомления hello для WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a>Настройка вашего Cordova приложения toosupport push-уведомления Windows
Привет открыть конструктор конфигурации (правой кнопкой мыши файл config.xml и выберите **конструктор представлений**) выберите hello **Windows** и кнопку **Windows 10** под **Windows целевой версии**.

Строит toosupport push-уведомлений в используемом по умолчанию (Отладка), откройте build.json файл. Скопируйте конфигурацию «выпуск» tooyour конфигурации отладки.

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

После обновления hello hello build.json должна содержать hello, следующий код:

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

Постройте приложение hello и проверьте наличие ошибок. Клиентское приложение теперь необходимо зарегистрировать для получения уведомлений hello из внутреннего сервера мобильного приложения hello. Повторите действия из этого раздела для каждого проекта Windows, входящего в ваше решение.

#### <a name="test-push-notifications-in-your-windows-app"></a>Тестирование push-уведомлений в приложении Windows
В Visual Studio, убедитесь, что платформа Windows выбран в качестве целевого объекта развертывания hello, таких как **Windows x64** или **Windows x86**. Выберите приложение hello toorun на ПК Windows 10, размещения Visual Studio **локального компьютера**.

Нажмите клавишу hello запустите кнопка toobuild hello проект и запустить приложение hello.

В приложение hello, введите имя для нового todoitem и нажмите кнопку hello плюс (+) значок tooadd его.

Проверка получения уведомления при добавлении элемента hello.

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, как [концентраторы уведомлений] [ 17] toolearn о push-уведомлений.
* Если вы еще не сделали продолжить работу с учебником hello, [Добавление Authentication] [ 14] tooyour приложения Apache Cordova.

Узнайте, как toouse hello пакетов SDK.

* [Использование клиентской библиотеки Apache Cordova для мобильных приложений Azure][15]
* [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure][1]
* [Использование пакета SDK Node.js для мобильных приложений Azure][16]

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
