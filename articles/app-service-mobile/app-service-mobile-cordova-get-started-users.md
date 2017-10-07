---
title: "aaaAdd проверки подлинности на Apache Cordova с помощью мобильных приложений | Документы Microsoft"
description: "Узнайте, как toouse мобильные приложения в службе приложений Azure tooauthenticate пользователей приложения Apache Cordova с помощью различных поставщиков удостоверений, включая Google, Facebook, Twitter и Microsoft."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a>Добавление приложения Apache Cordova tooyour проверки подлинности
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Сводка
В этом учебнике добавьте проект краткое руководство todolist toohello проверки подлинности на Apache Cordova с помощью поставщика удостоверений, поддерживаемых. Этот учебник основывается на hello [начало работы с мобильным приложениям] руководство, в котором необходимо выполнять первой.

## <a name="register"></a>Регистрация приложения для проверки подлинности и настройка hello службы приложений
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[Видео, демонстрирующее аналогичные действия](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <a name="permissions"></a>Ограничить разрешения пользователей tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Теперь вы можете подтвердить этой серверной tooyour анонимный доступ отключен. В Visual Studio:

* Привет открыть проект, созданный после завершения учебника hello [начало работы с мобильным приложениям].
* Запустите приложение в hello **эмулятор Android Google**.
* Непредвиденный сбой соединения проверьте, отображается ли после запуска приложение hello.

Затем обновите пользователи tooauthenticate приложения hello, прежде чем запрашивать ресурсы из внутреннего сервера мобильного приложения hello.

## <a name="add-authentication"></a>Добавить приложение toohello проверки подлинности
1. Откройте проект в **Visual Studio**, затем откройте hello `www/index.html` файл для редактирования.
2. Найдите hello `Content-Security-Policy` метатег в раздел head hello.  Добавьте hello узла OAuth toohello список разрешенных источников.

   | Поставщик | Имя поставщика SDK | Узел OAuth |
   |:--- |:--- |:--- |
   | Azure Active Directory | aad | https://login.microsoftonline.com |
   | Facebook | Facebook | https://www.facebook.com |
   | Google | Google | https://accounts.google.com |
   | Microsoft | microsoftaccount | https://login.live.com |
   | Twitter | Twitter | https://api.twitter.com |

    Пример политики безопасности содержимого (для Azure Active Directory):

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    Замените `https://login.microsoftonline.com` с узлом OAuth hello из hello предшествующей таблице.  Дополнительные сведения о метатег политики безопасности содержимого hello. в разделе hello [документации политики безопасности содержимого].

    Некоторые поставщики аутентификации не требуют изменений в политике безопасности содержимого при использовании на соответствующих мобильных устройствах.  Например, изменения в политики безопасности содержимого не требуются, если на устройстве Android используется проверка подлинности Google.

3. Откройте hello `www/js/index.js` файл для редактирования, найдите hello `onDeviceReady()` метод, и создание клиента hello кода добавьте hello, следующий код:

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    Этот код заменяет hello существующий код, который создает ссылку на таблицу hello и обновляет hello пользовательского интерфейса.

    метод login() Hello запускает проверку подлинности с поставщиком hello. метод login() Hello является асинхронной функции, которая возвращает объект Promise в JavaScript.  Hello остальная часть инициализации hello помещается внутри hello promise ответа, чтобы он не выполняется до завершения метода login() hello.

4. В коде hello только что добавленную замените `SDK_Provider_Name` с именем hello поставщика входа. Например, для Azure Active Directory используйте `client.login('aad')`.
5. Запустите проект.  После завершения инициализации hello проекта приложения показана страница входа hello OAuth для hello выбранного поставщика проверки подлинности.

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте больше об [аутентификации] с использованием службы приложений Azure.
* Продолжить работу с учебником hello, добавив [Push-уведомления] tooyour приложения Apache Cordova.

Узнайте, как toouse hello пакетов SDK.

* [Пакет SDK для Apache Cordova]
* [Серверный пакет SDK для ASP.NET]
* [Серверный пакет SDK для Node.js]

<!-- URLs. -->
[начало работы с мобильным приложениям]: app-service-mobile-cordova-get-started.md
[документации политики безопасности содержимого]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[Push-уведомления]: app-service-mobile-cordova-get-started-push.md
[аутентификации]: app-service-mobile-auth.md
[Пакет SDK для Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[Серверный пакет SDK для ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Серверный пакет SDK для Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
