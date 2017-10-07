---
title: "aaaHow tooUse подключаемый модуль Cordova Apache для мобильных приложений Azure"
description: "Как tooUse подключаемый модуль Cordova Apache для мобильных приложений Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a>Как toouse Apache Cordova клиентскую библиотеку для мобильных приложений Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Это руководство поможет tooperform распространенные сценарии, с помощью hello последней [подключаемый модуль Cordova Apache для мобильных приложений Azure]. Если новый tooAzure мобильные приложения, сначала завершите [быстрого запуска Azure мобильных приложений] toocreate серверной части, создайте таблицу и загрузить предварительно построенного проекта Apache Cordova. В этом руководстве мы сосредоточиться на стороне клиента hello подключаемых модулей Apache Cordova.

## <a name="supported-platforms"></a>Поддерживаемые платформы
Этот пакет SDK поддерживает Apache Cordova 6.0.0 и более поздних версий на устройствах iOS, Android и устройствах с Windows.  Поддержка платформы Hello выглядит следующим образом:

* API Android 19–24 (от KitKat до Nougat);
* iOS 8.0 и более поздних версий;
* Windows Phone 8.1;
* универсальная платформа Windows.

## <a name="Setup"></a>Настройка и необходимые компоненты
В данном руководстве предполагается, что вы уже создали серверную часть с таблицей. В этом руководстве предполагается, что таблица hello имеет hello одной схеме с таблицами hello в этих учебниках. В этом руководстве также предполагается, были добавлены кода tooyour hello подключаемого модуля Cordova Apache.  Если этого не делали, можно добавить проект tooyour подключаемых модулей Apache Cordova hello hello в командной строке:

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

Дополнительные сведения о создании [первого приложения Apache Cordova] см. в соответствующей документации.

## <a name="ionic"></a>Настройка приложения Ionic v2

tooproperly настроить проект Ionic v2, сначала создайте простое приложение и добавьте hello подключаемого модуля Cordova:

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

Добавьте следующие строки слишком hello`app.component.ts` toocreate hello клиентского объекта:

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

Теперь, можно собрать и запустить проект hello в браузере hello:

```
ionic platform add browser
ionic run browser
```

Подключаемый модуль Cordova приложения Azure Mobile Hello поддерживает оба Ionic приложения v1 и v2.  Только для приложения hello Ionic v2 требуют дополнительных объявление для hello `WindowsAzure` объекта.

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Практическое руководство. Проверка подлинности пользователей
Служба приложений Azure поддерживает аутентификацию и авторизацию пользователей с помощью различных внешних поставщиков удостоверений: Facebook, Google, учетная запись Майкрософт и Twitter. Можно задать разрешения для таблицы toorestrict доступ для определенных операций tooonly проверку подлинности пользователей. Hello идентификаторов правил авторизации tooimplement прошедших проверку подлинности пользователей также можно использовать в серверных скриптах. Дополнительные сведения см. в разделе hello [приступить к работе с проверкой подлинности] учебника.

При использовании проверки подлинности в приложении Apache Cordova, должны быть доступны следующие подключаемые модули Cordova hello:

* [cordova-plugin-device]
* [cordova-plugin-inappbrowser]

Поддерживается два потока аутентификации: серверный и клиентский.  поток Hello server обеспечивает hello простой проверки подлинности, как зависит от поставщика hello веб-интерфейс проверки подлинности. Hello потока клиента обеспечивает более глубокую интеграцию с возможности определенных устройств, таких как-единого входа, зависит от поставщика SDK конкретного устройства.

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Практическое руководство. Настройка службы мобильных приложений для внешних URL-адресов перенаправления
Несколько типов приложений Apache Cordova используйте toohandle возможность замыкания на себя, потоков пользовательского интерфейса OAuth.  Потоки пользовательского интерфейса OAuth на localhost вызвать проблемы, поскольку служба проверки подлинности hello только известны как tooutilize службы по умолчанию.  Ниже перечислены примеры проблемных потоков пользовательского интерфейса OAuth:

* Эмулятор Ripple Hello.
* динамическая перезагрузка с Ionic.
* Локальное выполнение hello мобильной серверной части
* Под управлением серверной части мобильных hello в другой службе приложений Azure, чем проверка подлинности обеспечивает один hello.

Выполните эти инструкции tooadd toohello локальные параметры конфигурации.

1. Войдите в toohello [портал Azure]
2. Выберите **все ресурсы** или **службы приложений** щелкните имя мобильного приложения hello.
3. Щелкните **Инструменты**
4. Нажмите кнопку **обозреватель ресурсов** hello OBSERVE меню, а затем нажмите кнопку **Go**.  Откроется новое окно или вкладка.
5. Разверните hello **config**, **authsettings** узлов на сайте в левой навигационной hello.
6. Щелкните **Изменить**
7. Найдите элемент «allowedExternalRedirectUrls» hello.  Его можно задать toonull или массив значений.  Измените значение toohello hello, следующие значения:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Замените URL-адреса hello hello URL-адреса службы.  Примерами являются «http://localhost:3000» (для hello Node.js образца службы) или «http://localhost:4400» (для службы Ripple hello).  Тем не менее эти URL-адреса — это примеры — вашей ситуации, включая служб hello, упомянутые в примерах hello, может отличаться.
8. Нажмите кнопку hello **чтения и записи** кнопки в hello правом верхнем углу экрана приветствия.
9. Щелкните зеленый hello **ПОМЕСТИТЬ** кнопки.

на этом этапе сохраняются параметры Hello.  Не закрывайте окно браузера hello до завершения hello параметры сохранения.
Также можно добавьте эти параметры замыкания на себя URL-адреса toohello CORS для службы приложений:

1. Войдите в toohello [портал Azure]
2. Выберите **все ресурсы** или **службы приложений** щелкните имя мобильного приложения hello.
3. автоматически открывает колонку параметров Hello.  В противном случае щелкните **Все параметры**.
4. Нажмите кнопку **CORS** меню hello API.
5. Введите URL-адрес hello, на котором необходимо tooadd в hello поле и нажмите клавишу ВВОД.
6. При необходимости введите дополнительные URL-адреса.
7. Нажмите кнопку **Сохранить** toosave hello параметры.

Занимает около 10 – 15 секунд hello новые параметры tootake эффект.

## <a name="register-for-push"></a>Практическое руководство. Регистрация для получения push-уведомлений
Установка hello [phonegap-plugin-push] toohandle push-уведомлений.  Этот подключаемый модуль можно легко добавить с помощью `cordova plugin add` команду в командной строке приветствия или с помощью установщика подключаемого модуля Git hello в среде Visual Studio.  Следующий код в приложении Apache Cordova регистрирует устройство для получения push-уведомлений.

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

Используйте hello toosend SDK концентраторы уведомлений push-уведомления с сервера hello.  Никогда не следует отправлять push-уведомления непосредственно из клиентов. Поэтому это может быть используется tootrigger отказ в обслуживании, направленную на концентраторы уведомлений или hello PNS.  Hello PNS удалось ban трафика в результате таких атак.

## <a name="more-information"></a>Дополнительные сведения

Дополнительные сведения об API можно найти в нашей [документация по API](http://azure.github.io/azure-mobile-apps-js-client/).

<!-- URLs. -->
[портал Azure]: https://portal.azure.com
[быстрого запуска Azure мобильных приложений]: app-service-mobile-cordova-get-started.md
[приступить к работе с проверкой подлинности]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[подключаемый модуль Cordova Apache для мобильных приложений Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[первого приложения Apache Cordova]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
