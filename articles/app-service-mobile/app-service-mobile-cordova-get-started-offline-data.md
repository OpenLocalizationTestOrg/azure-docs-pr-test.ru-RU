---
title: "aaaEnable автономной синхронизации для мобильного приложения Azure (Cordova) | Документы Microsoft"
description: "Узнайте, как toouse приложение службы мобильных приложений toocache и синхронизации автономные данные в приложении Cordova"
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a>Включение автономной синхронизации для мобильного приложения Cordova
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

В этом учебнике рассказывается функции hello автономной синхронизации мобильных приложений Azure для Cordova. Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением&mdash;Просмотр, добавление или изменение данных&mdash;даже в том случае, если нет сетевого соединения. Изменения сохраняются в локальной базе данных.  Как только устройство hello вернется в оперативный режим, эти изменения синхронизируются с hello удаленной службы.

Этот учебник основывается на hello решение Cordova краткое руководство для мобильных приложений, созданные после завершения hello учебника [краткое руководство по Apache Cordova]. В этом учебнике обновить hello решения краткое руководство tooadd автономного возможности мобильных приложений Azure.  Мы также выделяет hello автономного код в приложение hello.

toolearn Дополнительные сведения о функции hello автономной синхронизации, см. разделе hello [автономной синхронизации данных в мобильных приложениях Azure]. Дополнительные сведения об использовании API см. в разделе hello [документации по API](https://azure.github.io/azure-mobile-apps-js-client).

## <a name="add-offline-sync-toohello-quickstart-solution"></a>Добавить решение краткое руководство toohello автономной синхронизации
Hello автономной синхронизации кода необходимо добавить toohello приложения. Автономная синхронизация требуется хранилище для sqlite cordova hello подключаемый модуль, который автоматически добавляется приложения tooyour если подключаемый модуль мобильных приложений Azure hello включен в проект hello. проект Hello краткое руководство включает в себя эти подключаемых модулей.

1. В обозревателе решений Visual Studio откройте index.js и замените после кода hello

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    следующим:

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. Затем замените hello, следующий код:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    следующим:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    Hello выше дополнения кода инициализации локального хранилища hello и определить локальной таблицы, которая соответствует hello столбца значения, используемые в Azure серверной части. (Необязательно tooinclude значения всех столбцов в этом коде.)  Hello `version` поле обслуживается мобильной серверной части hello и используется для разрешения конфликтов.

    Контекст синхронизации toohello ссылка возвращается путем вызова **getSyncContext**. Hello контекста синхронизации помогает сохранить связи между таблицами, отслеживания и опубликуйте изменения во всех таблицах в клиентском приложении был изменен при `.push()` вызывается.

3. Обновление hello приложения URL-адрес tooyour мобильного приложения URL-адрес приложения.

4. Теперь замените код

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    следующим:

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    Hello предыдущий код инициализирует контекст синхронизации hello и затем вызывает tooget getSyncTable (вместо getTable) локального toohello ссылочной таблице.

    Этот код использует hello локальной базы данных для всех создания, чтения, обновления и удаления (CRUD) табличные операции.

    В этом примере выполняется простая обработка ошибок, связанных с конфликтами синхронизации. Будет обрабатываться в реальном приложении hello различных ошибок как условия в сети, сервер конфликтов и другие. Примеры кода см. в разделе hello [автономной синхронизации образца].

5. Добавьте этот tooperform функции hello фактическое синхронизации.

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    Принято изменения внутреннего сервера мобильного приложения toohello путем вызова toopush **syncContext.push()**. Например, можно вызвать **syncBackend** в кнопке синхронизации равноценных tooa обработчика событий кнопки.

## <a name="offline-sync-considerations"></a>Рекомендации по автономной синхронизации

В образце hello hello **принудительной** метод **syncContext** вызывается только при запуске приложения в функции обратного вызова hello для входа.  В реальном приложении также может разместить эту функцию синхронизации вручную или при изменении состояния сетевого hello.

При выполнении запросу к таблице, имеющей ожидающие локального обновления отслеживаются контекстом hello, извлечь операции автоматически триггеры push. При обновлении, добавление и завершение работы элементов в этом примере, можно опустить hello явные **принудительной** вызвать, поскольку он может быть избыточным.

В коде указано hello запрашиваются все записи в таблицы удаленного todoItem hello, но это также возможно toofilter записей, передавая идентификатор запроса и запрос слишком**принудительной**. Дополнительные сведения см в разделе hello *добавочной синхронизации* в [автономной синхронизации данных в мобильных приложениях Azure].

## <a name="optional-disable-authentication"></a>Отключение проверки подлинности (необязательно)

Если не требуется tooset проверку подлинности перед тестированием автономной синхронизации, закомментируйте hello функции обратного вызова для имени входа, но оставить hello код внутри функции обратного вызова hello убрать комментарии.  Преобразовав в комментарий hello строки имени входа, hello кода выглядит следующим образом:

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

Теперь hello приложения синхронизации с hello Azure серверной, при запуске приложение hello.

## <a name="run-hello-client-app"></a>Запустить клиентское приложение hello
С помощью автономного теперь включена синхронизация приложение можно запустить hello клиента хотя бы один раз для каждой платформы, для заполнения базы данных локального хранилища hello. Позже имитировать автономный режим и изменить hello данные в локальном хранилище hello, когда приложение hello отключен от сети.

## <a name="optional-test-hello-sync-behavior"></a>(Необязательно) Проверить поведение синхронизации hello
В этом разделе изменения toosimulate проекта клиента hello в случае автономной работы с помощью URL-адрес приложения, недопустимый для серверной части. При добавлении или изменении элементов данных, эти изменения хранятся в локальном хранилище, но не являются синхронизированных toohello источник данных, пока hello подключение будет восстановлено.

1. В hello обозревателе решений откройте файл проекта index.js hello и измените toopoint URL-адрес приложения hello на недопустимый URL-адрес, например hello, следующий код:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. В файле index.html обновить hello CSP `<meta>` элемент с hello же недопустимый URL-адрес.

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. Построить и запустить клиентское приложение hello и обратите внимание, что исключение заносится в консоли hello, когда приложение hello пытается синхронизировать с сервером hello после входа в систему. Все новые элементы, добавляемые существуют только в локальном хранилище hello, пока они помещаются в стек toohello мобильной серверной части. клиентское приложение Hello, ведет себя как toohello подключенной базы данных.

4. Закройте приложение hello и перезапустите его tooverify, hello новые элементы, созданные сохраненного toohello локального хранилища.

5. (Необязательно) С помощью Visual Studio tooview вашей toosee таблицы базы данных SQL Azure, hello данные в базе данных серверной части hello не изменились.

    В Visual Studio в откройте **обозреватель сервера**. Перейдите tooyour базы данных в **Azure**->**баз данных SQL**. Щелкните правой кнопкой мыши базу данных и выберите пункт **Открыть в обозревателе объектов SQL Server**. Теперь можно просмотреть tooyour таблицы базы данных SQL и ее содержимое.

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a>(Необязательно) Тест hello переподключения tooyour мобильной серверной части

В этом разделе переподключение hello toohello мобильного внутреннего сервера приложения, которое имитирует приложение hello, приходящие обратно в оперативном состоянии. При входе в данных является синхронной tooyour мобильной серверной части.

1. Снова откройте index.js и восстановления URL-адрес приложения hello.
2. Снова откройте файл index.html и исправьте URL-адрес приложения hello в hello CSP `<meta>` элемента.
3. Повторное построение и запуск клиентского приложения hello. приложение Hello попыток toosync с внутреннего сервера мобильного приложения hello после входа в систему. Проверьте регистрацию ни одного исключения в консоли отладки hello.
4. (Необязательно) Представление hello обновленных данных, с помощью обозревателя объектов SQL Server или средством REST, например Fiddler. Обратите внимание hello данные синхронизированы между hello серверной базой данных и hello локального хранилища.

    Обратите внимание, данные hello синхронизации между базой данных hello и локальное хранилище hello и содержит элементы hello, добавленного в автономном приложении.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [автономной синхронизации данных в мобильных приложениях Azure]
* [Инструменты Visual Studio для Apache Cordova]

## <a name="next-steps"></a>Дальнейшие действия
* Просмотрите дополнительные возможности автономной синхронизации, такие как разрешение конфликтов в hello [автономной синхронизации образца]
* Просмотрите hello автономной синхронизации Справочник по API в hello [документации по API](https://azure.github.io/azure-mobile-apps-js-client).

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[краткое руководство по Apache Cordova]: app-service-mobile-cordova-get-started.md
[автономной синхронизации образца]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[автономной синхронизации данных в мобильных приложениях Azure]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Инструменты Visual Studio для Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
