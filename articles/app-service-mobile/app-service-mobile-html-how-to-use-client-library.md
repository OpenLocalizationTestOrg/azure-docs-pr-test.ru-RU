---
title: "hello tooUse aaaHow JavaScript SDK для мобильных приложений Azure"
description: "Как v tooUse для мобильных приложений Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a>Как tooUse hello клиентская библиотека JavaScript для мобильных приложений Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Это руководство поможет tooperform распространенные сценарии, с помощью hello последней [JavaScript SDK для мобильных приложений Azure]. Если новый tooAzure мобильные приложения, сначала завершите [быстрого запуска Azure мобильных приложений] toocreate серверной части и создайте таблицу. В этом руководстве мы сосредоточиться на использование мобильной серверной части hello в HTML/JavaScript веб-приложений.

## <a name="supported-platforms"></a>Поддерживаемые платформы
Мы ограничить текущего toohello поддержки браузера и последние версии hello основные обозреватели: Google Chrome, Microsoft Edge, Microsoft Internet Explorer и Mozilla Firefox.  Ожидается, что toofunction hello SDK с любого относительно современного браузера.

Hello пакета распространяется в виде универсального модуля JavaScript, поэтому он поддерживает globals, AMD, CommonJS формат и.

## <a name="Setup"></a>Настройка и необходимые компоненты
В данном руководстве предполагается, что вы уже создали серверную часть с таблицей. В этом руководстве предполагается, что таблица hello имеет hello одной схеме с таблицами hello в этих учебниках.

Установка hello JavaScript SDK Azure Mobile приложения можно сделать с помощью hello `npm` команды:

```
npm install azure-mobile-apps-client --save
```

Библиотека Hello также может использоваться в качестве ES2015 модуля, в средах CommonJS, например Browserify и Webpack и как библиотека AMD.  Например:

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

Также можно использовать предварительно построенного версию пакета SDK для hello, загружая непосредственно из наших CDN:

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Практическое руководство. Проверка подлинности пользователей
Служба приложений Azure поддерживает аутентификацию и авторизацию пользователей с помощью различных внешних поставщиков удостоверений: Facebook, Google, учетная запись Майкрософт и Twitter. Можно задать разрешения для таблицы toorestrict доступ для определенных операций tooonly проверку подлинности пользователей. Hello идентификаторов правил авторизации tooimplement прошедших проверку подлинности пользователей также можно использовать в серверных скриптах. Дополнительные сведения см. в разделе hello [приступить к работе с проверкой подлинности] учебника.

Поддерживается два потока аутентификации: серверный и клиентский.  поток Hello server обеспечивает hello простой проверки подлинности, как зависит от поставщика hello веб-интерфейс проверки подлинности. Hello потока клиента обеспечивает более глубокую интеграцию с возможности определенных устройств, таких как-единого входа, зависит от конкретного поставщика SDK.

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Практическое руководство. Настройка службы мобильных приложений для внешних URL-адресов перенаправления
Несколько типов приложений JavaScript используйте toohandle возможность замыкания на себя, потоков пользовательского интерфейса OAuth.  К этим возможностям относятся следующие:

* выполнение службы в локальной среде;
* С помощью Live перезагрузить с hello платформы Ionic
* Перенаправление tooApp службы для проверки подлинности.

Локальное выполнение может вызвать проблемы, поскольку по умолчанию приложение службы проверки подлинности только в том случае tooallow доступ из мобильного приложения серверной части. Используйте следующие hello toochange действия проверки подлинности tooenable параметров приложения службы при запуске сервера hello локально hello.

1. Войдите в toohello [портал Azure]
2. Перейдите в серверной части tooyour мобильного приложения.
3. Выберите **обозреватель ресурсов** в hello **средства разработки** меню.
4. Нажмите кнопку **Go** обозреватель ресурсов hello tooopen для серверной части мобильных приложений в новой вкладке или окне.
5. Разверните hello **config** > **authsettings** узла приложения.
6. Нажмите кнопку hello **изменить** кнопку tooenable редактирование ресурсов hello.
7. Найти hello **allowedExternalRedirectUrls** элемент, который должен иметь значение null. Добавьте URL-адреса в массив.

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Замените URL-адреса hello в массиве hello hello URL-адреса службы, который в данном примере — `http://localhost:3000` для образца службы локального Node.js hello. Можно также использовать `http://localhost:4400` для службы Ripple hello или некоторые другие URL-адрес, в зависимости от настроек приложения.
8. В начале hello страницы приветствия, нажмите кнопку **чтения и записи**, нажмите кнопку **ПОМЕСТИТЬ** toosave обновления.

Необходимо также tooadd hello же замыкания на себя URL-адреса toohello CORS белый список параметров:

1. Перейдите назад toohello [портал Azure].
2. Перейдите в серверной части tooyour мобильного приложения.
3. Нажмите кнопку **CORS** в hello **API** меню.
4. Введите каждый URL-адрес в пустой hello **источники, которые разрешено** текстовое поле.  Будет создано новое текстовое поле.
5. Щелкните **Сохранить**

После обновления серверной hello, можно будет toouse hello новые замыкания на себя URL-адреса в вашем приложении.

<!-- URLs. -->
[быстрого запуска Azure мобильных приложений]: app-service-mobile-cordova-get-started.md
[приступить к работе с проверкой подлинности]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[портал Azure]: https://portal.azure.com/
[JavaScript SDK для мобильных приложений Azure]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
