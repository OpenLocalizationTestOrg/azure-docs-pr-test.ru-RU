---
title: "aaaEnable автономную синхронизацию Azure мобильного приложения (Android)"
description: "Узнайте, как toouse мобильные приложения службы приложений toocache и синхронизировать данные в приложении Android"
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="182a9-103">Включение автономной синхронизации для мобильного приложения Android</span><span class="sxs-lookup"><span data-stu-id="182a9-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="182a9-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="182a9-104">Overview</span></span>
<span data-ttu-id="182a9-105">В этом учебнике приведены функции hello автономной синхронизации мобильных приложений Azure для Android.</span><span class="sxs-lookup"><span data-stu-id="182a9-105">This tutorial covers hello offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="182a9-106">Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением&mdash;Просмотр, добавление или изменение данных&mdash;даже в том случае, если нет сетевого соединения.</span><span class="sxs-lookup"><span data-stu-id="182a9-106">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="182a9-107">Изменения сохраняются в локальной базе данных.</span><span class="sxs-lookup"><span data-stu-id="182a9-107">Changes are stored in a local database.</span></span> <span data-ttu-id="182a9-108">Как только устройство hello вернется в оперативный режим, эти изменения синхронизируются с hello удаленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="182a9-108">Once hello device is back online, these changes are synced with hello remote backend.</span></span>

<span data-ttu-id="182a9-109">Если это ваш первый опыт работы с мобильных приложений Azure, сначала следует выполнить hello учебника [создать приложение Android].</span><span class="sxs-lookup"><span data-stu-id="182a9-109">If this is your first experience with Azure Mobile Apps, you should first complete hello tutorial [Create an Android App].</span></span> <span data-ttu-id="182a9-110">Если вы не используете hello загружен быстрый запуск сервера проекта, необходимо добавить проект tooyour пакеты расширения доступа hello данных.</span><span class="sxs-lookup"><span data-stu-id="182a9-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="182a9-111">Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="182a9-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="182a9-112">toolearn Дополнительные сведения о функции hello автономной синхронизации, см. разделе hello [автономной синхронизации данных в мобильных приложениях Azure].</span><span class="sxs-lookup"><span data-stu-id="182a9-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-app-toosupport-offline-sync"></a><span data-ttu-id="182a9-113">Обновление автономной синхронизации hello приложения toosupport</span><span class="sxs-lookup"><span data-stu-id="182a9-113">Update hello app toosupport offline sync</span></span>
<span data-ttu-id="182a9-114">С автономной синхронизации можно просматривать, записывать tooand из *синхронизации таблицы* (с помощью hello *IMobileServiceSyncTable* интерфейса), который является частью **SQLite** базы данных на устройстве.</span><span class="sxs-lookup"><span data-stu-id="182a9-114">With offline sync, you read tooand write from a *sync table* (using hello *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="182a9-115">toopush и запросу изменения между устройством hello и мобильных служб Azure, вы используете *контекст синхронизации* (*MobileServiceClient.SyncContext*), который инициализируется с помощью hello локальной базы данных toostore данные локально.</span><span class="sxs-lookup"><span data-stu-id="182a9-115">toopush and pull changes between hello device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with hello local database toostore data locally.</span></span>

1. <span data-ttu-id="182a9-116">В `TodoActivity.java`, закомментируйте hello существующим определением `mToDoTable` и раскомментируйте следующую версию таблицы hello синхронизации:</span><span class="sxs-lookup"><span data-stu-id="182a9-116">In `TodoActivity.java`, comment out hello existing definition of `mToDoTable` and uncomment hello sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="182a9-117">В hello `onCreate` метод закомментируйте hello существующей инициализации `mToDoTable` и раскомментируйте это определение:</span><span class="sxs-lookup"><span data-stu-id="182a9-117">In hello `onCreate` method, comment out hello existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="182a9-118">В `refreshItemsFromTable` закомментируйте определение hello `results` и раскомментируйте это определение:</span><span class="sxs-lookup"><span data-stu-id="182a9-118">In `refreshItemsFromTable` comment out hello definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="182a9-119">Закомментируйте определение hello `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="182a9-119">Comment out hello definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="182a9-120">Раскомментируйте hello определение `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="182a9-120">Uncomment hello definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="182a9-121">Раскомментируйте hello определение `sync`:</span><span class="sxs-lookup"><span data-stu-id="182a9-121">Uncomment hello definition of `sync`:</span></span>
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-hello-app"></a><span data-ttu-id="182a9-122">Тестовое приложение hello</span><span class="sxs-lookup"><span data-stu-id="182a9-122">Test hello app</span></span>
<span data-ttu-id="182a9-123">В этом разделе тестировать поведение hello Wi-Fi на и затем выключите toocreate Wi-Fi в случае автономной работы.</span><span class="sxs-lookup"><span data-stu-id="182a9-123">In this section, you test hello behavior with WiFi on, and then turn off WiFi toocreate an offline scenario.</span></span>

<span data-ttu-id="182a9-124">При добавлении элементов данных, они хранятся в локальное хранилище SQLite hello, но не синхронизирован toohello мобильной службы, до нажатия клавиши hello **обновление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="182a9-124">When you add data items, they are held in hello local SQLite store, but not synced toohello mobile service until you press hello **Refresh** button.</span></span> <span data-ttu-id="182a9-125">Другие приложения могут применяться другие требования относительно toobe синхронизирован, когда потребуется данных, но для демонстрационных целей этого учебника имеет явно запросить пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="182a9-125">Other apps may have different requirements regarding when data needs toobe synchronized, but for demo purposes this tutorial has hello user explicitly request it.</span></span>

<span data-ttu-id="182a9-126">При нажатии этой кнопки запускается новая фоновая задача.</span><span class="sxs-lookup"><span data-stu-id="182a9-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="182a9-127">Помещает сначала все изменения, внесенные toohello локального хранилища с помощью контекст синхронизации, а затем переносит все изменения данных из локальной таблицы Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="182a9-127">It first pushes all changes made toohello local store using synchronization context, then pulls all changed data from Azure toohello local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="182a9-128">Тестирование в автономном режиме</span><span class="sxs-lookup"><span data-stu-id="182a9-128">Offline testing</span></span>
1. <span data-ttu-id="182a9-129">Место hello устройство или симулятор в *режим "в самолете"*.</span><span class="sxs-lookup"><span data-stu-id="182a9-129">Place hello device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="182a9-130">Это позволит смоделировать автономный сценарий.</span><span class="sxs-lookup"><span data-stu-id="182a9-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="182a9-131">Добавьте несколько элементов *ToDo* или отметьте некоторые элементы как завершенные.</span><span class="sxs-lookup"><span data-stu-id="182a9-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="182a9-132">Закройте hello устройство или симулятор (или приложение hello принудительно закрыть) и перезапустите.</span><span class="sxs-lookup"><span data-stu-id="182a9-132">Quit hello device or simulator (or forcibly close hello app) and restart.</span></span> <span data-ttu-id="182a9-133">Убедитесь, что изменения были сохранены на устройстве hello, так как они хранятся в локальном хранилище SQLite hello.</span><span class="sxs-lookup"><span data-stu-id="182a9-133">Verify that your changes have been persisted on hello device because they are held in hello local SQLite store.</span></span>
3. <span data-ttu-id="182a9-134">Просмотрите содержимое hello hello Azure *TodoItem* таблицы с помощью средства SQL, таких как *SQL Server Management Studio*, или клиент REST, такие как *Fiddler* или  *Почтальон*.</span><span class="sxs-lookup"><span data-stu-id="182a9-134">View hello contents of hello Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="182a9-135">Убедитесь, что новые элементы hello *не* был синхронизирован toohello сервера</span><span class="sxs-lookup"><span data-stu-id="182a9-135">Verify that hello new items have *not* been synced toohello server</span></span>
   
       + <span data-ttu-id="182a9-136">Для внутреннего Node.js go toohello [портал Azure](https://portal.azure.com/), и мобильные приложения серверной части, нажмите кнопку **простой таблицы** > **TodoItem** tooview содержимое hello hello `TodoItem` таблицы.</span><span class="sxs-lookup"><span data-stu-id="182a9-136">For a Node.js backend, go toohello [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** tooview hello contents of hello `TodoItem` table.</span></span>
       + <span data-ttu-id="182a9-137">Для серверного приложения .NET, просмотр таблицы hello содержимое с помощью средства SQL например *SQL Server Management Studio*, или клиент REST, такие как *Fiddler* или *почтальон*.</span><span class="sxs-lookup"><span data-stu-id="182a9-137">For a .NET backend, view hello table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="182a9-138">Включите Wi-Fi hello устройства или симулятора.</span><span class="sxs-lookup"><span data-stu-id="182a9-138">Turn on WiFi in hello device or simulator.</span></span> <span data-ttu-id="182a9-139">Нажмите hello **обновление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="182a9-139">Next, press hello **Refresh** button.</span></span>
5. <span data-ttu-id="182a9-140">Просмотр данных TodoItem hello снова в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="182a9-140">View hello TodoItem data again in hello Azure portal.</span></span> <span data-ttu-id="182a9-141">Здравствуйте, появятся новые и измененные TodoItems.</span><span class="sxs-lookup"><span data-stu-id="182a9-141">hello new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="182a9-142">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="182a9-142">Additional Resources</span></span>
* <span data-ttu-id="182a9-143">[автономной синхронизации данных в мобильных приложениях Azure]</span><span class="sxs-lookup"><span data-stu-id="182a9-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="182a9-144">[Облака охватывает следующие темы. Автономная синхронизация в мобильных службах Azure] \(Примечание: hello видео на мобильных служб, но автономной синхронизации работает аналогичным образом в мобильных приложениях Azure\)</span><span class="sxs-lookup"><span data-stu-id="182a9-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: hello video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

[автономной синхронизации данных в мобильных приложениях Azure]: app-service-mobile-offline-data-sync.md

[создать приложение Android]: app-service-mobile-android-get-started.md

[Облака охватывает следующие темы. Автономная синхронизация в мобильных службах Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

