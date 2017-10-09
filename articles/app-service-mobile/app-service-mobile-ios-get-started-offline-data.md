---
title: "aaaEnable автономной синхронизации с помощью мобильных приложений iOS | Документы Microsoft"
description: "Узнайте, как toouse службе приложений Azure мобильных приложений toocache и синхронизации автономные данные в приложения iOS."
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="db2aa-103">Включение автономной синхронизации с помощью мобильных приложений iOS</span><span class="sxs-lookup"><span data-stu-id="db2aa-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="db2aa-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="db2aa-104">Overview</span></span>
<span data-ttu-id="db2aa-105">В этом учебнике автономной синхронизации с hello функция службы приложений Azure мобильные приложения для iOS.</span><span class="sxs-lookup"><span data-stu-id="db2aa-105">This tutorial covers offline syncing with hello Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="db2aa-106">С автономной синхронизации конечные пользователи могут взаимодействовать с tooview мобильного приложения и добавлять изменения данных, даже в том случае, если они не имеют сетевых подключений.</span><span class="sxs-lookup"><span data-stu-id="db2aa-106">With offline syncing end-users can interact with a mobile app tooview, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="db2aa-107">Изменения сохраняются в локальной базе данных.</span><span class="sxs-lookup"><span data-stu-id="db2aa-107">Changes are stored in a local database.</span></span> <span data-ttu-id="db2aa-108">После hello устройство вернется в оперативный режим, hello изменения синхронизируются с hello удаленного серверной части.</span><span class="sxs-lookup"><span data-stu-id="db2aa-108">After hello device is back online, hello changes are synced with hello remote back end.</span></span>

<span data-ttu-id="db2aa-109">Если это ваш первый опыт работы с мобильным приложениям, следует сначала выполнить учебника hello [создать приложение iOS].</span><span class="sxs-lookup"><span data-stu-id="db2aa-109">If this is your first experience with Mobile Apps, you should first complete hello tutorial [Create an iOS App].</span></span> <span data-ttu-id="db2aa-110">Если проект сервера краткое загружаются hello не используется, необходимо добавить проект tooyour пакеты расширения доступа к данным hello.</span><span class="sxs-lookup"><span data-stu-id="db2aa-110">If you do not use hello downloaded quick-start server project, you must add hello data-access extension packages tooyour project.</span></span> <span data-ttu-id="db2aa-111">Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="db2aa-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="db2aa-112">toolearn Дополнительные сведения о функции hello автономной синхронизации, в разделе [автономной синхронизации данных в мобильных приложениях].</span><span class="sxs-lookup"><span data-stu-id="db2aa-112">toolearn more about hello offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="db2aa-113"><a name="review-sync"></a>Просмотрите код синхронизации приветствия клиента</span><span class="sxs-lookup"><span data-stu-id="db2aa-113"><a name="review-sync"></a>Review hello client sync code</span></span>
<span data-ttu-id="db2aa-114">Hello клиентский проект, загруженный для hello [создать приложение iOS] учебник уже содержит код, который поддерживает синхронизацию в автономном режиме с помощью локальной базы данных на базе основных данных.</span><span class="sxs-lookup"><span data-stu-id="db2aa-114">hello client project that you downloaded for hello [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="db2aa-115">В этом разделе перечислены новые уже включен в учебник кода hello.</span><span class="sxs-lookup"><span data-stu-id="db2aa-115">This section summarizes what is already included in hello tutorial code.</span></span> <span data-ttu-id="db2aa-116">Концептуальный обзор функции hello. в разделе [автономной синхронизации данных в мобильных приложениях].</span><span class="sxs-lookup"><span data-stu-id="db2aa-116">For a conceptual overview of hello feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="db2aa-117">С помощью функции hello автономной синхронизации данных мобильных приложений конечные пользователи могут взаимодействовать с локальной базы данных даже в том случае, когда hello сеть недоступна.</span><span class="sxs-lookup"><span data-stu-id="db2aa-117">Using hello offline data-sync feature of Mobile Apps, end-users can interact with a local database even when hello network is inaccessible.</span></span> <span data-ttu-id="db2aa-118">toouse эти функции в вашем приложении инициализации контекста синхронизации hello `MSClient` и ссылаться на локальное хранилище.</span><span class="sxs-lookup"><span data-stu-id="db2aa-118">toouse these features in your app, you initialize hello sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="db2aa-119">Затем можно ссылаться на таблицы через hello **MSSyncTable** интерфейса.</span><span class="sxs-lookup"><span data-stu-id="db2aa-119">Then you reference your table through hello **MSSyncTable** interface.</span></span>

<span data-ttu-id="db2aa-120">В **QSTodoService.m** (Objective-C) или **ToDoTableViewController.swift** (Swift), обратите внимание, что тип члена hello hello **syncTable** —  **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="db2aa-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that hello type of hello member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="db2aa-121">Автономная синхронизация использует этот интерфейс таблицы синхронизации вместо **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="db2aa-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="db2aa-122">При использовании таблицы синхронизации, все операции перейдите toohello локальное хранилище и синхронизируются только с hello удаленного серверной части с явной передачи и операций по запросу.</span><span class="sxs-lookup"><span data-stu-id="db2aa-122">When a sync table is used, all operations go toohello local store and are synchronized only with hello remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="db2aa-123">tooget tooa синхронизации ссылочной таблицы, используйте hello **syncTableWithName** метод `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="db2aa-123">tooget a reference tooa sync table, use hello **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="db2aa-124">Автономная синхронизация функций tooremove, **tableWithName** вместо него.</span><span class="sxs-lookup"><span data-stu-id="db2aa-124">tooremove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="db2aa-125">Перед выполнением любых операций таблицы hello локального хранилища должен быть инициализирован.</span><span class="sxs-lookup"><span data-stu-id="db2aa-125">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="db2aa-126">Ниже приведен соответствующий код hello:</span><span class="sxs-lookup"><span data-stu-id="db2aa-126">Here is hello relevant code:</span></span>

* <span data-ttu-id="db2aa-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="db2aa-127">**Objective-C**.</span></span> <span data-ttu-id="db2aa-128">В hello **QSTodoService.init** метод:</span><span class="sxs-lookup"><span data-stu-id="db2aa-128">In hello **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="db2aa-129">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="db2aa-129">**Swift**.</span></span> <span data-ttu-id="db2aa-130">В hello **ToDoTableViewController.viewDidLoad** метод:</span><span class="sxs-lookup"><span data-stu-id="db2aa-130">In hello **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="db2aa-131">Этот метод создает локального хранилища с помощью hello `MSCoreDataStore` предоставляет интерфейс, который hello пакет SDK для мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="db2aa-131">This method creates a local store by using hello `MSCoreDataStore` interface, which hello Mobile Apps SDK provides.</span></span> <span data-ttu-id="db2aa-132">Кроме того, можно предоставить различные локальное хранилище путем реализации hello `MSSyncContextDataSource` протокола.</span><span class="sxs-lookup"><span data-stu-id="db2aa-132">Alternatively, you can provide a different local store by implementing hello `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="db2aa-133">Кроме того, hello первый параметр **MSSyncContext** является используется toospecify обработчика конфликтов.</span><span class="sxs-lookup"><span data-stu-id="db2aa-133">Also, hello first parameter of **MSSyncContext** is used toospecify a conflict handler.</span></span> <span data-ttu-id="db2aa-134">Так как мы прошли `nil`, мы получаем конфликтов по умолчанию hello обработчик, который не выполняется на любого конфликта.</span><span class="sxs-lookup"><span data-stu-id="db2aa-134">Because we have passed `nil`, we get hello default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="db2aa-135">Теперь давайте выполнения операции синхронизации фактическое hello и получение данных из удаленного серверной части hello:</span><span class="sxs-lookup"><span data-stu-id="db2aa-135">Now, let's perform hello actual sync operation, and get data from hello remote back end:</span></span>

* <span data-ttu-id="db2aa-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="db2aa-136">**Objective-C**.</span></span> <span data-ttu-id="db2aa-137">`syncData`Помещает сначала новые изменения, а затем вызывает **pullData** tooget данных из удаленного серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="db2aa-137">`syncData` first pushes new changes and then calls **pullData** tooget data from hello remote back end.</span></span> <span data-ttu-id="db2aa-138">Здравствуйте, в свою очередь, **pullData** метод получает новые данные, совпадает с запросом:</span><span class="sxs-lookup"><span data-stu-id="db2aa-138">In turn, hello **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="db2aa-139">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="db2aa-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="db2aa-140">В версии hello Objective-C в `syncData`, сначала вызовите **pushWithCompletion** в контексте синхронизации hello.</span><span class="sxs-lookup"><span data-stu-id="db2aa-140">In hello Objective-C version, in `syncData`, we first call **pushWithCompletion** on hello sync context.</span></span> <span data-ttu-id="db2aa-141">Этот метод является членом `MSSyncContext` (и не hello синхронизации сама таблица), так как он помещает изменения для всех таблиц.</span><span class="sxs-lookup"><span data-stu-id="db2aa-141">This method is a member of `MSSyncContext` (and not hello sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="db2aa-142">Только те записи, которые были изменены каким-либо образом локально (с помощью операции CUD) отправляются toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="db2aa-142">Only records that have been modified in some way locally (through CUD operations) are sent toohello server.</span></span> <span data-ttu-id="db2aa-143">Затем hello вспомогательный **pullData** вызове, который вызывает **MSSyncTable.pullWithQuery** tooretrieve удаленных данных и сохраняет его в локальной базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="db2aa-143">Then hello helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** tooretrieve remote data and store it in hello local database.</span></span>

<span data-ttu-id="db2aa-144">В версии Swift hello, так как операция отправки hello не является обязательным, отсутствует вызов слишком**pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="db2aa-144">In hello Swift version, because hello push operation was not strictly necessary, there is no call too**pushWithCompletion**.</span></span> <span data-ttu-id="db2aa-145">Если все ожидающие изменения в контексте hello синхронизации для таблицы hello, осуществляющего принудительной отправки, запросу всегда выдает push сначала.</span><span class="sxs-lookup"><span data-stu-id="db2aa-145">If there are any changes pending in hello sync context for hello table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="db2aa-146">Однако при наличии более одной таблицы синхронизации, это лучший tooensure принудительной вызова tooexplicitly, что все, что является согласованным для всех связанных таблиц.</span><span class="sxs-lookup"><span data-stu-id="db2aa-146">However, if you have more than one sync table, it is best tooexplicitly call push tooensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="db2aa-147">В hello Objective-C и Swift версий можно использовать hello **pullWithQuery** toospecify метод toofilter запроса hello tooretrieve записи.</span><span class="sxs-lookup"><span data-stu-id="db2aa-147">In both hello Objective-C and Swift versions, you can use hello **pullWithQuery** method toospecify a query toofilter hello records you want tooretrieve.</span></span> <span data-ttu-id="db2aa-148">В этом примере hello запрос получает все записи в удаленном hello `TodoItem` таблицы.</span><span class="sxs-lookup"><span data-stu-id="db2aa-148">In this example, hello query retrieves all records in hello remote `TodoItem` table.</span></span>

<span data-ttu-id="db2aa-149">Здравствуйте, второй параметр **pullWithQuery** является Идентификатором запроса, который используется для *добавочной синхронизации*. Добавочной синхронизации извлекает только те записи, которые были изменены с момента последней синхронизации hello, с помощью записи hello `UpdatedAt` отметка времени (называется `updatedAt` в hello локальное хранилище.) hello идентификатор запроса должен быть строку описания, которое является уникальным для каждого логического запроса в приложение.</span><span class="sxs-lookup"><span data-stu-id="db2aa-149">hello second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*. Incremental sync retrieves only records that were modified since hello last sync, using hello record's `UpdatedAt` time stamp (called `updatedAt` in hello local store.) hello query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="db2aa-150">tooopt за пределы добавочной синхронизации, передайте `nil` как hello ИД запроса.</span><span class="sxs-lookup"><span data-stu-id="db2aa-150">tooopt out of incremental sync, pass `nil` as hello query ID.</span></span> <span data-ttu-id="db2aa-151">Этот подход может привести к снижению производительности, так как при каждой операции извлечения будут извлекаться все записи.</span><span class="sxs-lookup"><span data-stu-id="db2aa-151">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="db2aa-152">приложение Hello Objective-C синхронизируется при изменении или добавлении данных, когда пользователь выполняет обновление жестов hello и при запуске.</span><span class="sxs-lookup"><span data-stu-id="db2aa-152">hello Objective-C app syncs when you modify or add data, when a user performs hello refresh gesture, and on launch.</span></span>

<span data-ttu-id="db2aa-153">Swift приложение Hello синхронизируется при пользователем hello жестов hello обновления и при запуске.</span><span class="sxs-lookup"><span data-stu-id="db2aa-153">hello Swift app syncs when hello user performs hello refresh gesture and on launch.</span></span>

<span data-ttu-id="db2aa-154">За hello синхронизации приложения всякий раз, когда данные изменения (Objective-C) или при запуске приложение hello (Objective-C и Swift), приложение hello предполагается, что этот пользователь hello находится в оперативном режиме.</span><span class="sxs-lookup"><span data-stu-id="db2aa-154">Because hello app syncs whenever data is modified (Objective-C) or whenever hello app starts (Objective-C and Swift), hello app assumes that hello user is online.</span></span> <span data-ttu-id="db2aa-155">В следующем разделе потребуется обновить приложение hello, чтобы пользователи могли изменять даже в том случае, если они находятся в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="db2aa-155">In a later section, you will update hello app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="db2aa-156"><a name="review-core-data"></a>Просмотрите hello основных данных модели</span><span class="sxs-lookup"><span data-stu-id="db2aa-156"><a name="review-core-data"></a>Review hello Core Data model</span></span>
<span data-ttu-id="db2aa-157">При использовании автономного хранилища hello основных данных, необходимо определить отдельные таблицы и поля в модели данных.</span><span class="sxs-lookup"><span data-stu-id="db2aa-157">When you use hello Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="db2aa-158">Пример приложения Hello уже есть модель данных с hello неправильный формат.</span><span class="sxs-lookup"><span data-stu-id="db2aa-158">hello sample app already includes a data model with hello right format.</span></span> <span data-ttu-id="db2aa-159">В этом разделе будут рассмотрены tooshow эти таблицы как они используются.</span><span class="sxs-lookup"><span data-stu-id="db2aa-159">In this section, we walk through these tables tooshow how they are used.</span></span>

<span data-ttu-id="db2aa-160">Откройте **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="db2aa-160">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="db2aa-161">Четыре таблицы будут определены - 3, используемым hello SDK и элементов, используемая для hello задачи:</span><span class="sxs-lookup"><span data-stu-id="db2aa-161">Four tables are defined--three that are used by hello SDK and one that's used for hello to-do items themselves:</span></span>
  * <span data-ttu-id="db2aa-162">MS_TableOperations: Отслеживает hello элементы, которые должны toobe синхронизируются с сервером hello.</span><span class="sxs-lookup"><span data-stu-id="db2aa-162">MS_TableOperations: Tracks hello items that need toobe synchronized with hello server.</span></span>
  * <span data-ttu-id="db2aa-163">MS_TableOperationErrors: отслеживает ошибки, возникающие во время автономной синхронизации.</span><span class="sxs-lookup"><span data-stu-id="db2aa-163">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="db2aa-164">MS_TableConfig: Отслеживает hello время последнего обновления hello последняя операция синхронизации для всех операций по запросу.</span><span class="sxs-lookup"><span data-stu-id="db2aa-164">MS_TableConfig: Tracks hello last updated time for hello last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="db2aa-165">TodoItem: Задача hello сохраняет сообщения.</span><span class="sxs-lookup"><span data-stu-id="db2aa-165">TodoItem: Stores hello to-do items.</span></span> <span data-ttu-id="db2aa-166">Здравствуйте, системные столбцы **createdAt**, **updatedAt**, и **версии** — это необязательные системные свойства.</span><span class="sxs-lookup"><span data-stu-id="db2aa-166">hello system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="db2aa-167">пакет SDK для мобильных приложений Hello резервирует имена столбцов, которые начинаются с «**``**».</span><span class="sxs-lookup"><span data-stu-id="db2aa-167">hello Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="db2aa-168">Не используйте этот префикс где-либо, кроме системных столбцов.</span><span class="sxs-lookup"><span data-stu-id="db2aa-168">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="db2aa-169">В противном случае в именах столбцов изменяются при использовании удаленного серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="db2aa-169">Otherwise, your column names are modified when you use hello remote back end.</span></span>
>
>

<span data-ttu-id="db2aa-170">При использовании функции автономных синхронизации hello определение hello три системные таблицы и таблицы данных hello.</span><span class="sxs-lookup"><span data-stu-id="db2aa-170">When you use hello offline sync feature, define hello three system tables and hello data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="db2aa-171">Системные таблицы</span><span class="sxs-lookup"><span data-stu-id="db2aa-171">System tables</span></span>

<span data-ttu-id="db2aa-172">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="db2aa-172">**MS_TableOperations**</span></span>  

![Атрибуты таблицы MS_TableOperations][defining-core-data-tableoperations-entity]

| <span data-ttu-id="db2aa-174">Атрибут</span><span class="sxs-lookup"><span data-stu-id="db2aa-174">Attribute</span></span> | <span data-ttu-id="db2aa-175">Тип</span><span class="sxs-lookup"><span data-stu-id="db2aa-175">Type</span></span> |
| --- | --- |
| <span data-ttu-id="db2aa-176">id</span><span class="sxs-lookup"><span data-stu-id="db2aa-176">id</span></span> | <span data-ttu-id="db2aa-177">Integer 64</span><span class="sxs-lookup"><span data-stu-id="db2aa-177">Integer 64</span></span> |
| <span data-ttu-id="db2aa-178">itemId</span><span class="sxs-lookup"><span data-stu-id="db2aa-178">itemId</span></span> | <span data-ttu-id="db2aa-179">Строка</span><span class="sxs-lookup"><span data-stu-id="db2aa-179">String</span></span> |
| <span data-ttu-id="db2aa-180">properties</span><span class="sxs-lookup"><span data-stu-id="db2aa-180">properties</span></span> | <span data-ttu-id="db2aa-181">Двоичные данные</span><span class="sxs-lookup"><span data-stu-id="db2aa-181">Binary Data</span></span> |
| <span data-ttu-id="db2aa-182">таблица</span><span class="sxs-lookup"><span data-stu-id="db2aa-182">table</span></span> | <span data-ttu-id="db2aa-183">Строка</span><span class="sxs-lookup"><span data-stu-id="db2aa-183">String</span></span> |
| <span data-ttu-id="db2aa-184">tableKind</span><span class="sxs-lookup"><span data-stu-id="db2aa-184">tableKind</span></span> | <span data-ttu-id="db2aa-185">Integer 16</span><span class="sxs-lookup"><span data-stu-id="db2aa-185">Integer 16</span></span> |


<span data-ttu-id="db2aa-186">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="db2aa-186">**MS_TableOperationErrors**</span></span>

 ![Атрибуты таблицы MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="db2aa-188">Атрибут</span><span class="sxs-lookup"><span data-stu-id="db2aa-188">Attribute</span></span> | <span data-ttu-id="db2aa-189">Тип</span><span class="sxs-lookup"><span data-stu-id="db2aa-189">Type</span></span> |
| --- | --- |
| <span data-ttu-id="db2aa-190">id</span><span class="sxs-lookup"><span data-stu-id="db2aa-190">id</span></span> |<span data-ttu-id="db2aa-191">Строка</span><span class="sxs-lookup"><span data-stu-id="db2aa-191">String</span></span> |
| <span data-ttu-id="db2aa-192">operationId</span><span class="sxs-lookup"><span data-stu-id="db2aa-192">operationId</span></span> |<span data-ttu-id="db2aa-193">Integer 64</span><span class="sxs-lookup"><span data-stu-id="db2aa-193">Integer 64</span></span> |
| <span data-ttu-id="db2aa-194">properties</span><span class="sxs-lookup"><span data-stu-id="db2aa-194">properties</span></span> |<span data-ttu-id="db2aa-195">Двоичные данные</span><span class="sxs-lookup"><span data-stu-id="db2aa-195">Binary Data</span></span> |
| <span data-ttu-id="db2aa-196">tableKind</span><span class="sxs-lookup"><span data-stu-id="db2aa-196">tableKind</span></span> |<span data-ttu-id="db2aa-197">Integer 16</span><span class="sxs-lookup"><span data-stu-id="db2aa-197">Integer 16</span></span> |

 <span data-ttu-id="db2aa-198">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="db2aa-198">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="db2aa-199">Атрибут</span><span class="sxs-lookup"><span data-stu-id="db2aa-199">Attribute</span></span> | <span data-ttu-id="db2aa-200">Тип</span><span class="sxs-lookup"><span data-stu-id="db2aa-200">Type</span></span> |
| --- | --- |
| <span data-ttu-id="db2aa-201">id</span><span class="sxs-lookup"><span data-stu-id="db2aa-201">id</span></span> |<span data-ttu-id="db2aa-202">Строка</span><span class="sxs-lookup"><span data-stu-id="db2aa-202">String</span></span> |
| <span data-ttu-id="db2aa-203">key</span><span class="sxs-lookup"><span data-stu-id="db2aa-203">key</span></span> |<span data-ttu-id="db2aa-204">Строка</span><span class="sxs-lookup"><span data-stu-id="db2aa-204">String</span></span> |
| <span data-ttu-id="db2aa-205">keyType</span><span class="sxs-lookup"><span data-stu-id="db2aa-205">keyType</span></span> |<span data-ttu-id="db2aa-206">Integer 64</span><span class="sxs-lookup"><span data-stu-id="db2aa-206">Integer 64</span></span> |
| <span data-ttu-id="db2aa-207">таблица</span><span class="sxs-lookup"><span data-stu-id="db2aa-207">table</span></span> |<span data-ttu-id="db2aa-208">Строка</span><span class="sxs-lookup"><span data-stu-id="db2aa-208">String</span></span> |
| <span data-ttu-id="db2aa-209">значение</span><span class="sxs-lookup"><span data-stu-id="db2aa-209">value</span></span> |<span data-ttu-id="db2aa-210">Строка</span><span class="sxs-lookup"><span data-stu-id="db2aa-210">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="db2aa-211">Таблица данных</span><span class="sxs-lookup"><span data-stu-id="db2aa-211">Data table</span></span>

<span data-ttu-id="db2aa-212">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="db2aa-212">**TodoItem**</span></span>

| <span data-ttu-id="db2aa-213">Атрибут</span><span class="sxs-lookup"><span data-stu-id="db2aa-213">Attribute</span></span> | <span data-ttu-id="db2aa-214">Тип</span><span class="sxs-lookup"><span data-stu-id="db2aa-214">Type</span></span> | <span data-ttu-id="db2aa-215">Примечание.</span><span class="sxs-lookup"><span data-stu-id="db2aa-215">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db2aa-216">id</span><span class="sxs-lookup"><span data-stu-id="db2aa-216">id</span></span> | <span data-ttu-id="db2aa-217">Строка, помеченная как обязательная</span><span class="sxs-lookup"><span data-stu-id="db2aa-217">String, marked required</span></span> |<span data-ttu-id="db2aa-218">Первичный ключ в удаленном хранилище</span><span class="sxs-lookup"><span data-stu-id="db2aa-218">Primary key in remote store</span></span> |
| <span data-ttu-id="db2aa-219">complete</span><span class="sxs-lookup"><span data-stu-id="db2aa-219">complete</span></span> | <span data-ttu-id="db2aa-220">Логический</span><span class="sxs-lookup"><span data-stu-id="db2aa-220">Boolean</span></span> | <span data-ttu-id="db2aa-221">Поле элемента списка дел</span><span class="sxs-lookup"><span data-stu-id="db2aa-221">To-do item field</span></span> |
| <span data-ttu-id="db2aa-222">text</span><span class="sxs-lookup"><span data-stu-id="db2aa-222">text</span></span> |<span data-ttu-id="db2aa-223">Строка</span><span class="sxs-lookup"><span data-stu-id="db2aa-223">String</span></span> |<span data-ttu-id="db2aa-224">Поле элемента списка дел</span><span class="sxs-lookup"><span data-stu-id="db2aa-224">To-do item field</span></span> |
| <span data-ttu-id="db2aa-225">дата создания</span><span class="sxs-lookup"><span data-stu-id="db2aa-225">createdAt</span></span> | <span data-ttu-id="db2aa-226">Дата</span><span class="sxs-lookup"><span data-stu-id="db2aa-226">Date</span></span> | <span data-ttu-id="db2aa-227">(необязательно) Сопоставляет слишком**createdAt** системного свойства</span><span class="sxs-lookup"><span data-stu-id="db2aa-227">(optional) Maps too**createdAt** system property</span></span> |
| <span data-ttu-id="db2aa-228">дата обновления</span><span class="sxs-lookup"><span data-stu-id="db2aa-228">updatedAt</span></span> | <span data-ttu-id="db2aa-229">Дата</span><span class="sxs-lookup"><span data-stu-id="db2aa-229">Date</span></span> | <span data-ttu-id="db2aa-230">(необязательно) Сопоставляет слишком**updatedAt** системного свойства</span><span class="sxs-lookup"><span data-stu-id="db2aa-230">(optional) Maps too**updatedAt** system property</span></span> |
| <span data-ttu-id="db2aa-231">версия</span><span class="sxs-lookup"><span data-stu-id="db2aa-231">version</span></span> | <span data-ttu-id="db2aa-232">Строка</span><span class="sxs-lookup"><span data-stu-id="db2aa-232">String</span></span> | <span data-ttu-id="db2aa-233">(необязательно) Используется toodetect конфликты, tooversion карты</span><span class="sxs-lookup"><span data-stu-id="db2aa-233">(optional) Used toodetect conflicts, maps tooversion</span></span> |

## <span data-ttu-id="db2aa-234"><a name="setup-sync"></a>Изменить поведение синхронизации hello приложение hello</span><span class="sxs-lookup"><span data-stu-id="db2aa-234"><a name="setup-sync"></a>Change hello sync behavior of hello app</span></span>
<span data-ttu-id="db2aa-235">В этом разделе можно изменить приложение hello, чтобы он не выполняется синхронизация на запуск приложения или при вставки и обновления элементов.</span><span class="sxs-lookup"><span data-stu-id="db2aa-235">In this section, you modify hello app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="db2aa-236">Она синхронизируется только в том случае, когда кнопка жестов hello обновления выполняется.</span><span class="sxs-lookup"><span data-stu-id="db2aa-236">It syncs only when hello refresh gesture button is performed.</span></span>

<span data-ttu-id="db2aa-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="db2aa-237">**Objective-C**:</span></span>

1. <span data-ttu-id="db2aa-238">В **QSTodoListViewController.m**, измените hello **viewDidLoad** tooremove метод hello вызовов слишком`[self refresh]` конце hello метод hello.</span><span class="sxs-lookup"><span data-stu-id="db2aa-238">In **QSTodoListViewController.m**, change hello **viewDidLoad** method tooremove hello call too`[self refresh]` at hello end of hello method.</span></span> <span data-ttu-id="db2aa-239">Теперь hello данных не синхронизированы с сервером hello на запуск приложения.</span><span class="sxs-lookup"><span data-stu-id="db2aa-239">Now hello data is not synced with hello server on app start.</span></span> <span data-ttu-id="db2aa-240">Она синхронизируется с содержимым hello hello локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="db2aa-240">Instead, it's synced with hello contents of hello local store.</span></span>
2. <span data-ttu-id="db2aa-241">В **QSTodoService.m**, изменять определение hello `addItem` , чтобы он не синхронизировать после вставки элемента hello.</span><span class="sxs-lookup"><span data-stu-id="db2aa-241">In **QSTodoService.m**, modify hello definition of `addItem` so that it doesn't sync after hello item is inserted.</span></span> <span data-ttu-id="db2aa-242">Удалите hello `self syncData` блокировку и замените hello следующее:</span><span class="sxs-lookup"><span data-stu-id="db2aa-242">Remove hello `self syncData` block and replace it with hello following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="db2aa-243">Изменить определение hello `completeItem` как было сказано ранее.</span><span class="sxs-lookup"><span data-stu-id="db2aa-243">Modify hello definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="db2aa-244">Удалите блок hello для `self syncData` и заменить ее именем hello следующее:</span><span class="sxs-lookup"><span data-stu-id="db2aa-244">Remove hello block for `self syncData` and replace it with hello following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="db2aa-245">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="db2aa-245">**Swift**:</span></span>

<span data-ttu-id="db2aa-246">В `viewDidLoad`в **ToDoTableViewController.swift**, закомментируйте hello две строки, показанный здесь, toostop синхронизации на запуск приложения.</span><span class="sxs-lookup"><span data-stu-id="db2aa-246">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out hello two lines shown here, toostop syncing on app start.</span></span> <span data-ttu-id="db2aa-247">На момент написания этой статьи hello приложение Swift Todo hello не обновить службу hello когда кто-то добавляет или завершения элемент.</span><span class="sxs-lookup"><span data-stu-id="db2aa-247">At hello time of this writing, hello Swift Todo app does not update hello service when someone adds or completes an item.</span></span> <span data-ttu-id="db2aa-248">Обновляет службу hello только на запуск приложения.</span><span class="sxs-lookup"><span data-stu-id="db2aa-248">It updates hello service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="db2aa-249"><a name="test-app"></a>Тестовое приложение hello</span><span class="sxs-lookup"><span data-stu-id="db2aa-249"><a name="test-app"></a>Test hello app</span></span>
<span data-ttu-id="db2aa-250">В этом разделе подключения tooan toosimulate недопустимый URL-адрес в случае автономной работы.</span><span class="sxs-lookup"><span data-stu-id="db2aa-250">In this section, you connect tooan invalid URL toosimulate an offline scenario.</span></span> <span data-ttu-id="db2aa-251">При добавлении элементов данных, все они удерживали в hello хранить локальные основные данные, но они все не синхронизированы с серверной части мобильное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="db2aa-251">When you add data items, they're held in hello local Core Data store, but they're not synced with hello mobile-app back end.</span></span>

1. <span data-ttu-id="db2aa-252">Изменить URL-адрес мобильного приложения hello в **QSTodoService.m** tooan недопустимый URL-адрес, а также выполнения hello приложение еще раз:</span><span class="sxs-lookup"><span data-stu-id="db2aa-252">Change hello mobile-app URL in **QSTodoService.m** tooan invalid URL, and run hello app again:</span></span>

   <span data-ttu-id="db2aa-253">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="db2aa-253">**Objective-C**.</span></span> <span data-ttu-id="db2aa-254">В файле QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="db2aa-254">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="db2aa-255">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="db2aa-255">**Swift**.</span></span> <span data-ttu-id="db2aa-256">В файле ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="db2aa-256">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="db2aa-257">Добавьте несколько элементов списка дел.</span><span class="sxs-lookup"><span data-stu-id="db2aa-257">Add some to-do items.</span></span> <span data-ttu-id="db2aa-258">Закройте имитатор hello (или приложение hello принудительно закрыть) и перезапустите ее.</span><span class="sxs-lookup"><span data-stu-id="db2aa-258">Quit hello simulator (or forcibly close hello app), and then restart it.</span></span> <span data-ttu-id="db2aa-259">Убедитесь, что изменения сохранились.</span><span class="sxs-lookup"><span data-stu-id="db2aa-259">Verify that your changes persist.</span></span>

3. <span data-ttu-id="db2aa-260">Просмотрите содержимое hello hello удаленного **TodoItem** таблицы:</span><span class="sxs-lookup"><span data-stu-id="db2aa-260">View hello contents of hello remote **TodoItem** table:</span></span>
   * <span data-ttu-id="db2aa-261">Для серверной Node.js, go toohello [портал Azure](https://portal.azure.com/) и в серверной части вашего мобильного приложения, выберите **простой таблицы** > **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="db2aa-261">For a Node.js back end, go toohello [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="db2aa-262">Для серверной части .NET используйте средства SQL, например SQL Server Management Studio, или клиент REST, например Fiddler или Postman.</span><span class="sxs-lookup"><span data-stu-id="db2aa-262">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="db2aa-263">Убедитесь, что новые элементы hello *не* был синхронизирован с сервером hello.</span><span class="sxs-lookup"><span data-stu-id="db2aa-263">Verify that hello new items have *not* been synced with hello server.</span></span>

5. <span data-ttu-id="db2aa-264">Изменение hello URL-адрес обратной toohello исправьте значение одного их в **QSTodoService.m**и приложение hello повторного запуска.</span><span class="sxs-lookup"><span data-stu-id="db2aa-264">Change hello URL back toohello correct one in **QSTodoService.m**, and rerun hello app.</span></span>

6. <span data-ttu-id="db2aa-265">Для выполнения обновления жестов hello перетащите вниз hello список элементов.</span><span class="sxs-lookup"><span data-stu-id="db2aa-265">Perform hello refresh gesture by pulling down hello list of items.</span></span>  
<span data-ttu-id="db2aa-266">Отобразится счетчик хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="db2aa-266">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="db2aa-267">Представление hello **TodoItem** данных еще раз.</span><span class="sxs-lookup"><span data-stu-id="db2aa-267">View hello **TodoItem** data again.</span></span> <span data-ttu-id="db2aa-268">Теперь должны отображаться Hello задача новых и измененных элементов.</span><span class="sxs-lookup"><span data-stu-id="db2aa-268">hello new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="db2aa-269">Сводка</span><span class="sxs-lookup"><span data-stu-id="db2aa-269">Summary</span></span>
<span data-ttu-id="db2aa-270">Функция автономного синхронизации toosupport hello, мы использовали hello `MSSyncTable` интерфейс и инициализируется `MSClient.syncContext` с локальным хранилищем.</span><span class="sxs-lookup"><span data-stu-id="db2aa-270">toosupport hello offline sync feature, we used hello `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="db2aa-271">В этом случае локальное хранилище hello был баз данных на основе основных данных.</span><span class="sxs-lookup"><span data-stu-id="db2aa-271">In this case, hello local store was a Core Data-based database.</span></span>

<span data-ttu-id="db2aa-272">При использовании локального хранилища основных данных, необходимо определить несколько таблиц с hello [исправить системные свойства](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="db2aa-272">When you use a Core Data local store, you must define several tables with hello [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="db2aa-273">Обычный Hello создание, чтение, обновление и удаление (CRUD) для мобильным приложениям применяются как в том случае, если приложение hello по-прежнему подключен, но все операции hello происходят запросы hello локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="db2aa-273">hello normal create, read, update, and delete (CRUD) operations for mobile apps work as if hello app is still connected, but all hello operations occur against hello local store.</span></span>

<span data-ttu-id="db2aa-274">При локальном хранилище hello мы синхронизируются с сервером hello, мы использовали hello **MSSyncTable.pullWithQuery** метод.</span><span class="sxs-lookup"><span data-stu-id="db2aa-274">When we synchronized hello local store with hello server, we used hello **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="db2aa-275">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="db2aa-275">Additional resources</span></span>
* <span data-ttu-id="db2aa-276">[автономной синхронизации данных в мобильных приложениях]</span><span class="sxs-lookup"><span data-stu-id="db2aa-276">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="db2aa-277">[Облака охватывает следующие темы. Автономная синхронизация в мобильных службах Azure] \(hello видео посвящена мобильных служб, но мобильные приложения в автономный режим синхронизации работает аналогичным образом.\)</span><span class="sxs-lookup"><span data-stu-id="db2aa-277">[Cloud Cover: Offline Sync in Azure Mobile Services] \(hello video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


[создать приложение iOS]: app-service-mobile-ios-get-started.md
[автономной синхронизации данных в мобильных приложениях]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Облака охватывает следующие темы. Автономная синхронизация в мобильных службах Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
