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
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="ceab4-103">Включение автономной синхронизации для мобильного приложения Cordova</span><span class="sxs-lookup"><span data-stu-id="ceab4-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="ceab4-104">В этом учебнике рассказывается функции hello автономной синхронизации мобильных приложений Azure для Cordova.</span><span class="sxs-lookup"><span data-stu-id="ceab4-104">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="ceab4-105">Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением&mdash;Просмотр, добавление или изменение данных&mdash;даже в том случае, если нет сетевого соединения.</span><span class="sxs-lookup"><span data-stu-id="ceab4-105">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="ceab4-106">Изменения сохраняются в локальной базе данных.</span><span class="sxs-lookup"><span data-stu-id="ceab4-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="ceab4-107">Как только устройство hello вернется в оперативный режим, эти изменения синхронизируются с hello удаленной службы.</span><span class="sxs-lookup"><span data-stu-id="ceab4-107">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="ceab4-108">Этот учебник основывается на hello решение Cordova краткое руководство для мобильных приложений, созданные после завершения hello учебника [краткое руководство по Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="ceab4-108">This tutorial is based on hello Cordova quickstart solution for Mobile Apps that you create when you complete hello tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="ceab4-109">В этом учебнике обновить hello решения краткое руководство tooadd автономного возможности мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="ceab4-109">In this tutorial, you update hello quickstart solution tooadd offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="ceab4-110">Мы также выделяет hello автономного код в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="ceab4-110">We also highlight hello offline-specific code in hello app.</span></span>

<span data-ttu-id="ceab4-111">toolearn Дополнительные сведения о функции hello автономной синхронизации, см. разделе hello [автономной синхронизации данных в мобильных приложениях Azure].</span><span class="sxs-lookup"><span data-stu-id="ceab4-111">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="ceab4-112">Дополнительные сведения об использовании API см. в разделе hello [документации по API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="ceab4-112">For details of API usage, see hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-toohello-quickstart-solution"></a><span data-ttu-id="ceab4-113">Добавить решение краткое руководство toohello автономной синхронизации</span><span class="sxs-lookup"><span data-stu-id="ceab4-113">Add offline sync toohello quickstart solution</span></span>
<span data-ttu-id="ceab4-114">Hello автономной синхронизации кода необходимо добавить toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="ceab4-114">hello offline sync code must be added toohello app.</span></span> <span data-ttu-id="ceab4-115">Автономная синхронизация требуется хранилище для sqlite cordova hello подключаемый модуль, который автоматически добавляется приложения tooyour если подключаемый модуль мобильных приложений Azure hello включен в проект hello.</span><span class="sxs-lookup"><span data-stu-id="ceab4-115">Offline sync requires hello cordova-sqlite-storage plugin, which automatically gets added tooyour app when hello Azure Mobile Apps plugin is included in hello project.</span></span> <span data-ttu-id="ceab4-116">проект Hello краткое руководство включает в себя эти подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="ceab4-116">hello Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="ceab4-117">В обозревателе решений Visual Studio откройте index.js и замените после кода hello</span><span class="sxs-lookup"><span data-stu-id="ceab4-117">In Visual Studio's Solution Explorer, open index.js and replace hello following code</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    <span data-ttu-id="ceab4-118">следующим:</span><span class="sxs-lookup"><span data-stu-id="ceab4-118">with this code:</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. <span data-ttu-id="ceab4-119">Затем замените hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="ceab4-119">Next, replace hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="ceab4-120">следующим:</span><span class="sxs-lookup"><span data-stu-id="ceab4-120">with this code:</span></span>

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

    <span data-ttu-id="ceab4-121">Hello выше дополнения кода инициализации локального хранилища hello и определить локальной таблицы, которая соответствует hello столбца значения, используемые в Azure серверной части.</span><span class="sxs-lookup"><span data-stu-id="ceab4-121">hello preceding code additions initialize hello local store and define a local table that matches hello column values used in your Azure back end.</span></span> <span data-ttu-id="ceab4-122">(Необязательно tooinclude значения всех столбцов в этом коде.)  Hello `version` поле обслуживается мобильной серверной части hello и используется для разрешения конфликтов.</span><span class="sxs-lookup"><span data-stu-id="ceab4-122">(You don't need tooinclude all column values in this code.)  hello `version` field is maintained by hello mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="ceab4-123">Контекст синхронизации toohello ссылка возвращается путем вызова **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="ceab4-123">You get a reference toohello sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="ceab4-124">Hello контекста синхронизации помогает сохранить связи между таблицами, отслеживания и опубликуйте изменения во всех таблицах в клиентском приложении был изменен при `.push()` вызывается.</span><span class="sxs-lookup"><span data-stu-id="ceab4-124">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="ceab4-125">Обновление hello приложения URL-адрес tooyour мобильного приложения URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="ceab4-125">Update hello application URL tooyour Mobile App application URL.</span></span>

4. <span data-ttu-id="ceab4-126">Теперь замените код</span><span class="sxs-lookup"><span data-stu-id="ceab4-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    <span data-ttu-id="ceab4-127">следующим:</span><span class="sxs-lookup"><span data-stu-id="ceab4-127">with this code:</span></span>

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

    <span data-ttu-id="ceab4-128">Hello предыдущий код инициализирует контекст синхронизации hello и затем вызывает tooget getSyncTable (вместо getTable) локального toohello ссылочной таблице.</span><span class="sxs-lookup"><span data-stu-id="ceab4-128">hello preceding code initializes hello sync context and then calls getSyncTable (instead of getTable) tooget a reference toohello local table.</span></span>

    <span data-ttu-id="ceab4-129">Этот код использует hello локальной базы данных для всех создания, чтения, обновления и удаления (CRUD) табличные операции.</span><span class="sxs-lookup"><span data-stu-id="ceab4-129">This code uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="ceab4-130">В этом примере выполняется простая обработка ошибок, связанных с конфликтами синхронизации.</span><span class="sxs-lookup"><span data-stu-id="ceab4-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="ceab4-131">Будет обрабатываться в реальном приложении hello различных ошибок как условия в сети, сервер конфликтов и другие.</span><span class="sxs-lookup"><span data-stu-id="ceab4-131">A real application would handle hello various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="ceab4-132">Примеры кода см. в разделе hello [автономной синхронизации образца].</span><span class="sxs-lookup"><span data-stu-id="ceab4-132">For code examples, see hello [offline sync sample].</span></span>

5. <span data-ttu-id="ceab4-133">Добавьте этот tooperform функции hello фактическое синхронизации.</span><span class="sxs-lookup"><span data-stu-id="ceab4-133">Next, add this function tooperform hello actual sync.</span></span>

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="ceab4-134">Принято изменения внутреннего сервера мобильного приложения toohello путем вызова toopush **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="ceab4-134">You decide when toopush changes toohello Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="ceab4-135">Например, можно вызвать **syncBackend** в кнопке синхронизации равноценных tooa обработчика событий кнопки.</span><span class="sxs-lookup"><span data-stu-id="ceab4-135">For example, you could call **syncBackend** in a button event handler tied tooa sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="ceab4-136">Рекомендации по автономной синхронизации</span><span class="sxs-lookup"><span data-stu-id="ceab4-136">Offline sync considerations</span></span>

<span data-ttu-id="ceab4-137">В образце hello hello **принудительной** метод **syncContext** вызывается только при запуске приложения в функции обратного вызова hello для входа.</span><span class="sxs-lookup"><span data-stu-id="ceab4-137">In hello sample, hello **push** method of **syncContext** is only called on app startup in hello callback function for login.</span></span>  <span data-ttu-id="ceab4-138">В реальном приложении также может разместить эту функцию синхронизации вручную или при изменении состояния сетевого hello.</span><span class="sxs-lookup"><span data-stu-id="ceab4-138">In a real-world application, you could also make this sync functionality triggered manually or when hello network state changes.</span></span>

<span data-ttu-id="ceab4-139">При выполнении запросу к таблице, имеющей ожидающие локального обновления отслеживаются контекстом hello, извлечь операции автоматически триггеры push.</span><span class="sxs-lookup"><span data-stu-id="ceab4-139">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="ceab4-140">При обновлении, добавление и завершение работы элементов в этом примере, можно опустить hello явные **принудительной** вызвать, поскольку он может быть избыточным.</span><span class="sxs-lookup"><span data-stu-id="ceab4-140">When refreshing, adding, and completing items in this sample, you can omit hello explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="ceab4-141">В коде указано hello запрашиваются все записи в таблицы удаленного todoItem hello, но это также возможно toofilter записей, передавая идентификатор запроса и запрос слишком**принудительной**.</span><span class="sxs-lookup"><span data-stu-id="ceab4-141">In hello provided code, all records in hello remote todoItem table are queried, but it is also possible toofilter records by passing a query id and query too**push**.</span></span> <span data-ttu-id="ceab4-142">Дополнительные сведения см в разделе hello *добавочной синхронизации* в [автономной синхронизации данных в мобильных приложениях Azure].</span><span class="sxs-lookup"><span data-stu-id="ceab4-142">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="ceab4-143">Отключение проверки подлинности (необязательно)</span><span class="sxs-lookup"><span data-stu-id="ceab4-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="ceab4-144">Если не требуется tooset проверку подлинности перед тестированием автономной синхронизации, закомментируйте hello функции обратного вызова для имени входа, но оставить hello код внутри функции обратного вызова hello убрать комментарии.</span><span class="sxs-lookup"><span data-stu-id="ceab4-144">If you don't want tooset up authentication before testing offline sync, comment out hello callback function for login, but leave hello code inside hello callback function uncommented.</span></span>  <span data-ttu-id="ceab4-145">Преобразовав в комментарий hello строки имени входа, hello кода выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ceab4-145">After commenting out hello login lines, hello code follows:</span></span>

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="ceab4-146">Теперь hello приложения синхронизации с hello Azure серверной, при запуске приложение hello.</span><span class="sxs-lookup"><span data-stu-id="ceab4-146">Now, hello app syncs with hello Azure backend when you run hello app.</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="ceab4-147">Запустить клиентское приложение hello</span><span class="sxs-lookup"><span data-stu-id="ceab4-147">Run hello client app</span></span>
<span data-ttu-id="ceab4-148">С помощью автономного теперь включена синхронизация приложение можно запустить hello клиента хотя бы один раз для каждой платформы, для заполнения базы данных локального хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="ceab4-148">With offline sync now enabled, you can run hello client application at least once on each platform to populate hello local store database.</span></span> <span data-ttu-id="ceab4-149">Позже имитировать автономный режим и изменить hello данные в локальном хранилище hello, когда приложение hello отключен от сети.</span><span class="sxs-lookup"><span data-stu-id="ceab4-149">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="optional-test-hello-sync-behavior"></a><span data-ttu-id="ceab4-150">(Необязательно) Проверить поведение синхронизации hello</span><span class="sxs-lookup"><span data-stu-id="ceab4-150">(Optional) Test hello sync behavior</span></span>
<span data-ttu-id="ceab4-151">В этом разделе изменения toosimulate проекта клиента hello в случае автономной работы с помощью URL-адрес приложения, недопустимый для серверной части.</span><span class="sxs-lookup"><span data-stu-id="ceab4-151">In this section, you modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="ceab4-152">При добавлении или изменении элементов данных, эти изменения хранятся в локальном хранилище, но не являются синхронизированных toohello источник данных, пока hello подключение будет восстановлено.</span><span class="sxs-lookup"><span data-stu-id="ceab4-152">When you add or change data items, these changes are held in the local store, but are not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="ceab4-153">В hello обозревателе решений откройте файл проекта index.js hello и измените toopoint URL-адрес приложения hello на недопустимый URL-адрес, например hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="ceab4-153">In hello Solution Explorer, open hello index.js project file and change hello application URL toopoint to  an invalid URL, like hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="ceab4-154">В файле index.html обновить hello CSP `<meta>` элемент с hello же недопустимый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="ceab4-154">In index.html, update hello CSP `<meta>` element with hello same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="ceab4-155">Построить и запустить клиентское приложение hello и обратите внимание, что исключение заносится в консоли hello, когда приложение hello пытается синхронизировать с сервером hello после входа в систему.</span><span class="sxs-lookup"><span data-stu-id="ceab4-155">Build and run hello client app and notice that an exception is logged in hello console when hello app attempts to sync with hello backend after login.</span></span> <span data-ttu-id="ceab4-156">Все новые элементы, добавляемые существуют только в локальном хранилище hello, пока они помещаются в стек toohello мобильной серверной части.</span><span class="sxs-lookup"><span data-stu-id="ceab4-156">Any new items you add exist only in hello local store until they are pushed toohello mobile backend.</span></span> <span data-ttu-id="ceab4-157">клиентское приложение Hello, ведет себя как toohello подключенной базы данных.</span><span class="sxs-lookup"><span data-stu-id="ceab4-157">hello client app behaves as if it is connected toohello backend.</span></span>

4. <span data-ttu-id="ceab4-158">Закройте приложение hello и перезапустите его tooverify, hello новые элементы, созданные сохраненного toohello локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="ceab4-158">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>

5. <span data-ttu-id="ceab4-159">(Необязательно) С помощью Visual Studio tooview вашей toosee таблицы базы данных SQL Azure, hello данные в базе данных серверной части hello не изменились.</span><span class="sxs-lookup"><span data-stu-id="ceab4-159">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="ceab4-160">В Visual Studio в откройте **обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="ceab4-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="ceab4-161">Перейдите tooyour базы данных в **Azure**->**баз данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="ceab4-161">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="ceab4-162">Щелкните правой кнопкой мыши базу данных и выберите пункт **Открыть в обозревателе объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ceab4-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="ceab4-163">Теперь можно просмотреть tooyour таблицы базы данных SQL и ее содержимое.</span><span class="sxs-lookup"><span data-stu-id="ceab4-163">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a><span data-ttu-id="ceab4-164">(Необязательно) Тест hello переподключения tooyour мобильной серверной части</span><span class="sxs-lookup"><span data-stu-id="ceab4-164">(Optional) Test hello reconnection tooyour mobile backend</span></span>

<span data-ttu-id="ceab4-165">В этом разделе переподключение hello toohello мобильного внутреннего сервера приложения, которое имитирует приложение hello, приходящие обратно в оперативном состоянии.</span><span class="sxs-lookup"><span data-stu-id="ceab4-165">In this section, you reconnect hello app toohello mobile backend, which simulates hello app coming back to an online state.</span></span> <span data-ttu-id="ceab4-166">При входе в данных является синхронной tooyour мобильной серверной части.</span><span class="sxs-lookup"><span data-stu-id="ceab4-166">When you log in, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="ceab4-167">Снова откройте index.js и восстановления URL-адрес приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ceab4-167">Reopen index.js and restore hello application URL.</span></span>
2. <span data-ttu-id="ceab4-168">Снова откройте файл index.html и исправьте URL-адрес приложения hello в hello CSP `<meta>` элемента.</span><span class="sxs-lookup"><span data-stu-id="ceab4-168">Reopen index.html and correct hello application URL in hello CSP `<meta>` element.</span></span>
3. <span data-ttu-id="ceab4-169">Повторное построение и запуск клиентского приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ceab4-169">Rebuild and run hello client app.</span></span> <span data-ttu-id="ceab4-170">приложение Hello попыток toosync с внутреннего сервера мобильного приложения hello после входа в систему.</span><span class="sxs-lookup"><span data-stu-id="ceab4-170">hello app attempts toosync with hello mobile app backend after login.</span></span> <span data-ttu-id="ceab4-171">Проверьте регистрацию ни одного исключения в консоли отладки hello.</span><span class="sxs-lookup"><span data-stu-id="ceab4-171">Verify that no exceptions are logged in hello debug console.</span></span>
4. <span data-ttu-id="ceab4-172">(Необязательно) Представление hello обновленных данных, с помощью обозревателя объектов SQL Server или средством REST, например Fiddler.</span><span class="sxs-lookup"><span data-stu-id="ceab4-172">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="ceab4-173">Обратите внимание hello данные синхронизированы между hello серверной базой данных и hello локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="ceab4-173">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="ceab4-174">Обратите внимание, данные hello синхронизации между базой данных hello и локальное хранилище hello и содержит элементы hello, добавленного в автономном приложении.</span><span class="sxs-lookup"><span data-stu-id="ceab4-174">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ceab4-175">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ceab4-175">Additional resources</span></span>
* <span data-ttu-id="ceab4-176">[автономной синхронизации данных в мобильных приложениях Azure]</span><span class="sxs-lookup"><span data-stu-id="ceab4-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="ceab4-177">[Инструменты Visual Studio для Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="ceab4-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="ceab4-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ceab4-178">Next steps</span></span>
* <span data-ttu-id="ceab4-179">Просмотрите дополнительные возможности автономной синхронизации, такие как разрешение конфликтов в hello [автономной синхронизации образца]</span><span class="sxs-lookup"><span data-stu-id="ceab4-179">Review more advanced offline sync features such as conflict resolution in hello [offline sync sample]</span></span>
* <span data-ttu-id="ceab4-180">Просмотрите hello автономной синхронизации Справочник по API в hello [документации по API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="ceab4-180">Review hello offline sync API reference in hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

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
