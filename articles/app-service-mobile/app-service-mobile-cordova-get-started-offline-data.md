---
title: "Включение автономной синхронизации для мобильного приложения Azure (Cordova) | Документация Майкрософт"
description: "Использование мобильного приложения службы приложений для кэширования и синхронизации автономных данных в приложении Cordova"
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
ms.openlocfilehash: 45e80ca672dfdb6defc6e5c1aac3d29f5479125c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="fcc7f-103">Включение автономной синхронизации для мобильного приложения Cordova</span><span class="sxs-lookup"><span data-stu-id="fcc7f-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="fcc7f-104">В этом руководстве рассматривается функция автономной синхронизации мобильных приложений Azure для Cordova.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-104">This tutorial introduces the offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="fcc7f-105">Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением &mdash;просматривать, добавлять или изменять данные &mdash; даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-105">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="fcc7f-106">Изменения сохраняются в локальной базе данных.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="fcc7f-107">Как только устройство возвращается в режим подключения к сети, эти изменения синхронизируются с удаленной службой.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-107">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="fcc7f-108">В этом руководстве используется решение быстрого запуска Cordova для мобильных приложений, которые вы создадите, завершив изучение руководства [Создание приложения Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="fcc7f-108">This tutorial is based on the Cordova quickstart solution for Mobile Apps that you create when you complete the tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="fcc7f-109">При работе с этим руководством вы обновите решение быстрого запуска для добавления автономных функций мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-109">In this tutorial, you update the quickstart solution to add offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="fcc7f-110">Мы также рассмотрим автономный код, применяемый в приложении.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-110">We also highlight the offline-specific code in the app.</span></span>

<span data-ttu-id="fcc7f-111">Дополнительные сведения о функции автономной синхронизации см. в статье [Автономная синхронизация данных в мобильных приложениях Azure].</span><span class="sxs-lookup"><span data-stu-id="fcc7f-111">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="fcc7f-112">Сведения об использовании API см. в [документации по API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="fcc7f-112">For details of API usage, see the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-to-the-quickstart-solution"></a><span data-ttu-id="fcc7f-113">Добавление функции автономной синхронизации в решение быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="fcc7f-113">Add offline sync to the quickstart solution</span></span>
<span data-ttu-id="fcc7f-114">В приложение необходимо добавить код автономной синхронизации.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-114">The offline sync code must be added to the app.</span></span> <span data-ttu-id="fcc7f-115">Для включения функции автономной синхронизации требуется подключаемый модуль cordova-sqlite-storage, который автоматически добавляется в приложение после включения подключаемого модуля мобильных приложений Azure в проект.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-115">Offline sync requires the cordova-sqlite-storage plugin, which automatically gets added to your app when the Azure Mobile Apps plugin is included in the project.</span></span> <span data-ttu-id="fcc7f-116">В проект быстрого запуска добавлены оба этих подключаемых модуля.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-116">The Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="fcc7f-117">В обозревателе решений Visual Studio откройте файл index.js и замените код</span><span class="sxs-lookup"><span data-stu-id="fcc7f-117">In Visual Studio's Solution Explorer, open index.js and replace the following code</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable;      // Reference to a table endpoint on backend

    <span data-ttu-id="fcc7f-118">следующим:</span><span class="sxs-lookup"><span data-stu-id="fcc7f-118">with this code:</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable,      // Reference to a table endpoint on backend
           syncContext;        // Reference to offline data sync context

2. <span data-ttu-id="fcc7f-119">Затем замените код</span><span class="sxs-lookup"><span data-stu-id="fcc7f-119">Next, replace the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="fcc7f-120">следующим:</span><span class="sxs-lookup"><span data-stu-id="fcc7f-120">with this code:</span></span>

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

        // Get the sync context from the client
        syncContext = client.getSyncContext();

    <span data-ttu-id="fcc7f-121">Предыдущие дополнения кода позволяют выполнить инициализацию локального хранилища и определить локальную таблицу, соответствующую значениям столбцов, используемых в серверной части Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-121">The preceding code additions initialize the local store and define a local table that matches the column values used in your Azure back end.</span></span> <span data-ttu-id="fcc7f-122">(В этот код не нужно включать все значения столбцов.)  Поле `version` обслуживается серверной частью мобильной службы и используется для разрешения конфликтов.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-122">(You don't need to include all column values in this code.)  The `version` field is maintained by the mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="fcc7f-123">Ссылку на контекст синхронизации можно получить, вызвав метод **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-123">You get a reference to the sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="fcc7f-124">Контекст синхронизации помогает сохранить связи между таблицами, отслеживая и отправляя изменения во всех таблицах, измененных клиентским приложением при вызове `.push()` .</span><span class="sxs-lookup"><span data-stu-id="fcc7f-124">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="fcc7f-125">Замените текущий URL-адрес приложения URL-адресом вашего мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-125">Update the application URL to your Mobile App application URL.</span></span>

4. <span data-ttu-id="fcc7f-126">Теперь замените код</span><span class="sxs-lookup"><span data-stu-id="fcc7f-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is the table name

    <span data-ttu-id="fcc7f-127">следующим:</span><span class="sxs-lookup"><span data-stu-id="fcc7f-127">with this code:</span></span>

        // Initialize the sync context with the store
        syncContext.initialize(store).then(function () {

        // Get the local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle the conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert to server's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle the error
                  // In the simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function to perform the actual sync
        syncBackend();

        // Refresh the todoItems
        refreshDisplay();

        // Wire up the UI Event Handler for the Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="fcc7f-128">Приведенный выше код инициализирует контекст синхронизации, а затем вызывает метод getSyncTable (вместо getTable), чтобы получить ссылку на локальную таблицу.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-128">The preceding code initializes the sync context and then calls getSyncTable (instead of getTable) to get a reference to the local table.</span></span>

    <span data-ttu-id="fcc7f-129">Этот код использует локальную базу данных для всех операций создания, чтения, обновления и удаления (CRUD), выполняемых с таблицей.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-129">This code uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="fcc7f-130">В этом примере выполняется простая обработка ошибок, связанных с конфликтами синхронизации.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="fcc7f-131">Реальное приложение будет обрабатывать различные ошибки, например ошибки состояния сети, конфликты серверов и другие.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-131">A real application would handle the various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="fcc7f-132">Примеры кода можно найти [этом примере].</span><span class="sxs-lookup"><span data-stu-id="fcc7f-132">For code examples, see the [offline sync sample].</span></span>

5. <span data-ttu-id="fcc7f-133">Теперь добавьте эту функцию, чтобы выполнить фактическую синхронизацию.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-133">Next, add this function to perform the actual sync.</span></span>

        function syncBackend() {

          // Sync local store to Azure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from the Azure table after syncing to Azure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="fcc7f-134">Изменения в серверную часть мобильного приложения можно отправить в любое время, вызвав **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-134">You decide when to push changes to the Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="fcc7f-135">Например, можно вызвать **syncBackend** в обработчике событий кнопки, привязанной к кнопке синхронизации.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-135">For example, you could call **syncBackend** in a button event handler tied to a sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="fcc7f-136">Рекомендации по автономной синхронизации</span><span class="sxs-lookup"><span data-stu-id="fcc7f-136">Offline sync considerations</span></span>

<span data-ttu-id="fcc7f-137">В этом примере вызов метода **push** объекта **syncContext** выполняется только при запуске приложения в функции обратного вызова для входа.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-137">In the sample, the **push** method of **syncContext** is only called on app startup in the callback function for login.</span></span>  <span data-ttu-id="fcc7f-138">В реальном приложении функцию синхронизации также можно активировать вручную или при изменении состояния сети.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-138">In a real-world application, you could also make this sync functionality triggered manually or when the network state changes.</span></span>

<span data-ttu-id="fcc7f-139">При извлечении из таблицы, для которой есть ожидающие локальные обновления, отслеживаемые по контексту, операция извлечения автоматически активирует отправку.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-139">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="fcc7f-140">При обновлении, добавлении и завершении элементов в данном примере можно опустить явный вызов **push**, так как он может быть избыточен.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-140">When refreshing, adding, and completing items in this sample, you can omit the explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="fcc7f-141">В представленном коде запрашиваются все записи из удаленной таблицы TodoItem, однако их можно также отфильтровать путем передачи идентификатора запроса и запроса в **push**.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-141">In the provided code, all records in the remote todoItem table are queried, but it is also possible to filter records by passing a query id and query to **push**.</span></span> <span data-ttu-id="fcc7f-142">Дополнительные сведения см. в разделе *Добавочная синхронизация* статьи [Автономная синхронизация данных в мобильных приложениях Azure].</span><span class="sxs-lookup"><span data-stu-id="fcc7f-142">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="fcc7f-143">Отключение проверки подлинности (необязательно)</span><span class="sxs-lookup"><span data-stu-id="fcc7f-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="fcc7f-144">Если вы не хотите настраивать аутентификацию перед тестированием функции автономной синхронизации, то закомментируйте функцию обратного вызова для входа, но код внутри этой функции оставьте раскомментированным.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-144">If you don't want to set up authentication before testing offline sync, comment out the callback function for login, but leave the code inside the callback function uncommented.</span></span>  <span data-ttu-id="fcc7f-145">После комментирования строк входа в систему код выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-145">After commenting out the login lines, the code follows:</span></span>

      // Login to the service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave the rest of the code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="fcc7f-146">Теперь при запуске приложение синхронизируется с серверной частью Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-146">Now, the app syncs with the Azure backend when you run the app.</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="fcc7f-147">Запуск клиентского приложения</span><span class="sxs-lookup"><span data-stu-id="fcc7f-147">Run the client app</span></span>
<span data-ttu-id="fcc7f-148">Теперь, когда автономная синхронизация включена, можно запустить клиентское приложение по крайней мере по одному разу на каждой платформе, чтобы заполнить базу данных локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-148">With offline sync now enabled, you can run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="fcc7f-149">Далее вы сымитируете сценарий автономного режима и измените данные в локальном хранилище, пока приложение будет находиться в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-149">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="optional-test-the-sync-behavior"></a><span data-ttu-id="fcc7f-150">Тестирование режима синхронизации (необязательно)</span><span class="sxs-lookup"><span data-stu-id="fcc7f-150">(Optional) Test the sync behavior</span></span>
<span data-ttu-id="fcc7f-151">В этом разделе вы измените клиентский проект, чтобы смоделировать сценарий автономного режима, используя недействительный URL-адрес приложения для серверной части.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-151">In this section, you modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="fcc7f-152">При добавлении или изменении элементов данных эти изменения будут сохраняться в локальном хранилище, но не будут синхронизироваться с серверным хранилищем данных, пока не будет восстановлено подключение.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-152">When you add or change data items, these changes are held in the local store, but are not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="fcc7f-153">В обозревателе решений откройте файл проекта index.js и измените значение URL-адреса приложения таким образом, чтобы оно указывало на недопустимый URL-адрес, например, как показано в коде ниже.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-153">In the Solution Explorer, open the index.js project file and change the application URL to point to  an invalid URL, like the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="fcc7f-154">В файле index.html замените элемент `<meta>` поставщика облачных решений тем же самым недопустимым URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-154">In index.html, update the CSP `<meta>` element with the same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="fcc7f-155">Создайте и запустите клиентское приложение. Обратите внимание, что исключение регистрируется в журнале консоли при каждой попытке приложения выполнить синхронизацию с серверной частью после входа.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-155">Build and run the client app and notice that an exception is logged in the console when the app attempts to sync with the backend after login.</span></span> <span data-ttu-id="fcc7f-156">Добавляемые новые элементы существуют только в локальном хранилище, пока не будут извлечены в серверную часть мобильной службы.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-156">Any new items you add exist only in the local store until they are pushed to the mobile backend.</span></span> <span data-ttu-id="fcc7f-157">Клиентское приложение ведет себя так, как если бы оно было подключено к серверной части.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-157">The client app behaves as if it is connected to the backend.</span></span>

4. <span data-ttu-id="fcc7f-158">Закройте приложение и перезапустите его, чтобы убедиться, что новые элементы сохранены в локальном хранилище.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-158">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>

5. <span data-ttu-id="fcc7f-159">(Необязательно.) С помощью Visual Studio просмотрите таблицу базы данных SQL Azure, чтобы увидеть, что данные в серверной базе данных не изменились.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-159">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="fcc7f-160">В Visual Studio в откройте **обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="fcc7f-161">Перейдите к своей базе данных в **Azure**->**Базы данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-161">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="fcc7f-162">Щелкните правой кнопкой мыши базу данных и выберите пункт **Открыть в обозревателе объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="fcc7f-163">Теперь можно перейти к таблице базы данных SQL и ее содержимому.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-163">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="optional-test-the-reconnection-to-your-mobile-backend"></a><span data-ttu-id="fcc7f-164">Тестирование повторного подключения к мобильной серверной части (необязательно)</span><span class="sxs-lookup"><span data-stu-id="fcc7f-164">(Optional) Test the reconnection to your mobile backend</span></span>

<span data-ttu-id="fcc7f-165">В этом разделе вы повторно подключите приложение к серверной части мобильной службы, имитирующей приложение, подключающееся к сети.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-165">In this section, you reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="fcc7f-166">При входе данные синхронизируются с серверной частью мобильной службы.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-166">When you log in, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="fcc7f-167">Снова откройте файл index.js и восстановите URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-167">Reopen index.js and restore the application URL.</span></span>
2. <span data-ttu-id="fcc7f-168">Снова откройте файл index.html и измените URL-адрес приложения в элементе `<meta>` поставщика облачных решений.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-168">Reopen index.html and correct the application URL in the CSP `<meta>` element.</span></span>
3. <span data-ttu-id="fcc7f-169">Повторно выполните сборку и запустите клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-169">Rebuild and run the client app.</span></span> <span data-ttu-id="fcc7f-170">После входа приложение пытается выполнить синхронизацию с серверной частью мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-170">The app attempts to sync with the mobile app backend after login.</span></span> <span data-ttu-id="fcc7f-171">Убедитесь, что в журнале консоли отладки нет исключений.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-171">Verify that no exceptions are logged in the debug console.</span></span>
4. <span data-ttu-id="fcc7f-172">(Необязательно.) Просмотрите обновленные данные, используя обозреватель объектов SQL Server или инструмент REST, например Fiddler.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-172">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="fcc7f-173">Обратите внимание, что данные синхронизированы между базой данных в серверной части и локальным хранилищем.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-173">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="fcc7f-174">Обратите внимание, данные синхронизированы между базой данных и локальным хранилищем, и они содержат элементы, которые вы добавили, пока ваше приложение было вне сети.</span><span class="sxs-lookup"><span data-stu-id="fcc7f-174">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fcc7f-175">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fcc7f-175">Additional resources</span></span>
* <span data-ttu-id="fcc7f-176">[Автономная синхронизация данных в мобильных приложениях Azure]</span><span class="sxs-lookup"><span data-stu-id="fcc7f-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="fcc7f-177">[Инструменты Visual Studio для Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="fcc7f-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcc7f-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fcc7f-178">Next steps</span></span>
* <span data-ttu-id="fcc7f-179">Ознакомьтесь с более сложными функциями автономной синхронизации, такими как устранение конфликтов, в [этом примере].</span><span class="sxs-lookup"><span data-stu-id="fcc7f-179">Review more advanced offline sync features such as conflict resolution in the [offline sync sample]</span></span>
* <span data-ttu-id="fcc7f-180">Ознакомьтесь со справочной информацией об API автономной синхронизации в [документации по API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="fcc7f-180">Review the offline sync API reference in the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
<span data-ttu-id="fcc7f-181">[Создание приложения Apache Cordova]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="fcc7f-181">[Apache Cordova quick start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="fcc7f-182">[этом примере]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span><span class="sxs-lookup"><span data-stu-id="fcc7f-182">[offline sync sample]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span></span>
<span data-ttu-id="fcc7f-183">[Автономная синхронизация данных в мобильных приложениях Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="fcc7f-183">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with the .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
<span data-ttu-id="fcc7f-184">[Инструменты Visual Studio для Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="fcc7f-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
