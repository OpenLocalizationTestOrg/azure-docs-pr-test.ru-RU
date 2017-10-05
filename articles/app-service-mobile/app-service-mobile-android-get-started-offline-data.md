---
title: "Включение автономной синхронизации для мобильного приложения Azure (Android)"
description: "Узнайте, как использовать мобильные приложения службы приложений для кэширования и синхронизации автономных данных в приложении Android."
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
ms.openlocfilehash: 304323c1816302e8c1f68f36a029aee55e02c54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="8a211-103">Включение автономной синхронизации для мобильного приложения Android</span><span class="sxs-lookup"><span data-stu-id="8a211-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="8a211-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8a211-104">Overview</span></span>
<span data-ttu-id="8a211-105">В этом учебнике рассматривается функция автономной синхронизации мобильных приложений Azure для Android.</span><span class="sxs-lookup"><span data-stu-id="8a211-105">This tutorial covers the offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="8a211-106">Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением &mdash;просматривать, добавлять или изменять данные &mdash; даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="8a211-106">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="8a211-107">Изменения сохраняются в локальной базе данных.</span><span class="sxs-lookup"><span data-stu-id="8a211-107">Changes are stored in a local database.</span></span> <span data-ttu-id="8a211-108">Как только устройство возвращается в режим подключения к сети, эти изменения синхронизируются с удаленной внутренним сервером.</span><span class="sxs-lookup"><span data-stu-id="8a211-108">Once the device is back online, these changes are synced with the remote backend.</span></span>

<span data-ttu-id="8a211-109">Если вы впервые работаете с мобильными приложениями Azure, сначала ознакомьтесь с руководством [Создание приложения Android].</span><span class="sxs-lookup"><span data-stu-id="8a211-109">If this is your first experience with Azure Mobile Apps, you should first complete the tutorial [Create an Android App].</span></span> <span data-ttu-id="8a211-110">Если вы не используете скачанный проект быстрого запуска сервера, в проект необходимо добавить пакет расширений доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="8a211-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="8a211-111">в статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="8a211-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="8a211-112">Дополнительные сведения о функции автономной синхронизации см. в статье [Автономная синхронизация данных в мобильных приложениях Azure].</span><span class="sxs-lookup"><span data-stu-id="8a211-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-app-to-support-offline-sync"></a><span data-ttu-id="8a211-113">Обновление приложения для поддержки синхронизации автономных данных</span><span class="sxs-lookup"><span data-stu-id="8a211-113">Update the app to support offline sync</span></span>
<span data-ttu-id="8a211-114">При включенной синхронизации автономных данных операции чтения и записи осуществляются с помощью *таблицы синхронизации* (с помощью интерфейса *IMobileServiceSyncTable*), которая является частью базы данных **SQLite** на вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="8a211-114">With offline sync, you read to and write from a *sync table* (using the *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="8a211-115">Для принудительной отправки изменений на устройстве в мобильные службы Azure и получения изменений из мобильных служб используйте *контекст синхронизации* (*MobileServiceClient.SyncContext*), который инициализируется с помощью локальной базы данных.</span><span class="sxs-lookup"><span data-stu-id="8a211-115">To push and pull changes between the device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with the local database to store data locally.</span></span>

1. <span data-ttu-id="8a211-116">В `TodoActivity.java` закомментируйте существующее определение `mToDoTable` и раскомментируйте версию таблицы синхронизации.</span><span class="sxs-lookup"><span data-stu-id="8a211-116">In `TodoActivity.java`, comment out the existing definition of `mToDoTable` and uncomment the sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="8a211-117">В методе `onCreate` закомментируйте существующую инициализацию `mToDoTable` и раскомментируйте следующее определение.</span><span class="sxs-lookup"><span data-stu-id="8a211-117">In the `onCreate` method, comment out the existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="8a211-118">В `refreshItemsFromTable` закомментируйте определение `results` и раскомментируйте следующее определение.</span><span class="sxs-lookup"><span data-stu-id="8a211-118">In `refreshItemsFromTable` comment out the definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="8a211-119">Закомментируйте определение `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="8a211-119">Comment out the definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="8a211-120">Раскомментируйте определение `refreshItemsFromMobileServiceTableSyncTable`.</span><span class="sxs-lookup"><span data-stu-id="8a211-120">Uncomment the definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync the data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="8a211-121">Раскомментируйте определение `sync`.</span><span class="sxs-lookup"><span data-stu-id="8a211-121">Uncomment the definition of `sync`:</span></span>
   
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

## <a name="test-the-app"></a><span data-ttu-id="8a211-122">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="8a211-122">Test the app</span></span>
<span data-ttu-id="8a211-123">В этом разделе мы протестируем поведение приложения при доступной сети Wi-Fi, а затем отключим Wi-Fi и рассмотрим автономный сценарий.</span><span class="sxs-lookup"><span data-stu-id="8a211-123">In this section, you test the behavior with WiFi on, and then turn off WiFi to create an offline scenario.</span></span>

<span data-ttu-id="8a211-124">Добавляемые элементы данных будут находиться в локальном хранилище SQLight, но не будут синхронизированы с мобильной службой, пока вы не нажмете кнопку **Обновить** .</span><span class="sxs-lookup"><span data-stu-id="8a211-124">When you add data items, they are held in the local SQLite store, but not synced to the mobile service until you press the **Refresh** button.</span></span> <span data-ttu-id="8a211-125">У разных приложений могут быть разные требования к синхронизации данных, но для демонстрационных целей этого учебника мы будем считать, что пользователь явно запрашивает ее.</span><span class="sxs-lookup"><span data-stu-id="8a211-125">Other apps may have different requirements regarding when data needs to be synchronized, but for demo purposes this tutorial has the user explicitly request it.</span></span>

<span data-ttu-id="8a211-126">При нажатии этой кнопки запускается новая фоновая задача.</span><span class="sxs-lookup"><span data-stu-id="8a211-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="8a211-127">Сначала она отправляет все изменения, внесенные в локальное хранилище, используя контекст синхронизации, а затем переносит все измененные данные из службы Azure в локальную таблицу.</span><span class="sxs-lookup"><span data-stu-id="8a211-127">It first pushes all changes made to the local store using synchronization context, then pulls all changed data from Azure to the local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="8a211-128">Тестирование в автономном режиме</span><span class="sxs-lookup"><span data-stu-id="8a211-128">Offline testing</span></span>
1. <span data-ttu-id="8a211-129">Переведите устройство или эмулятор в режим *В самолете*.</span><span class="sxs-lookup"><span data-stu-id="8a211-129">Place the device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="8a211-130">Это позволит смоделировать автономный сценарий.</span><span class="sxs-lookup"><span data-stu-id="8a211-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="8a211-131">Добавьте несколько элементов *ToDo* или отметьте некоторые элементы как завершенные.</span><span class="sxs-lookup"><span data-stu-id="8a211-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="8a211-132">Выйдите из эмулятора (или принудительно закройте приложение) и перезапустите его.</span><span class="sxs-lookup"><span data-stu-id="8a211-132">Quit the device or simulator (or forcibly close the app) and restart.</span></span> <span data-ttu-id="8a211-133">Убедитесь, что изменения на устройстве по прежнему отображаются (так как они хранятся в локальном хранилище SQLight).</span><span class="sxs-lookup"><span data-stu-id="8a211-133">Verify that your changes have been persisted on the device because they are held in the local SQLite store.</span></span>
3. <span data-ttu-id="8a211-134">Просмотрите содержимое таблицы Azure *TodoItem* с помощью инструмента SQL, например *SQL Server Management Studio* или с помощью клиента REST, например *Fiddler* или *Postman*.</span><span class="sxs-lookup"><span data-stu-id="8a211-134">View the contents of the Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="8a211-135">Убедитесь, что новые элементы *не* были синхронизированы с сервером.</span><span class="sxs-lookup"><span data-stu-id="8a211-135">Verify that the new items have *not* been synced to the server</span></span>
   
       + <span data-ttu-id="8a211-136">Для серверной части Node.js перейдите на [портал Azure](https://portal.azure.com/), затем на странице серверной части своего мобильного приложения щелкните **Easy Tables** > **TodoItem**, чтобы просмотреть содержимое таблицы `TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="8a211-136">For a Node.js backend, go to the [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** to view the contents of the `TodoItem` table.</span></span>
       + <span data-ttu-id="8a211-137">Для серверной части .NET просмотрите содержимое таблицы с помощью средства SQL, например *SQL Server Management Studio*, или с помощью клиента REST, например *Fiddler* или *Postman*.</span><span class="sxs-lookup"><span data-stu-id="8a211-137">For a .NET backend, view the table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="8a211-138">Включите Wi-Fi в эмуляторе или на устройстве.</span><span class="sxs-lookup"><span data-stu-id="8a211-138">Turn on WiFi in the device or simulator.</span></span> <span data-ttu-id="8a211-139">Затем нажмите кнопку **Обновить** .</span><span class="sxs-lookup"><span data-stu-id="8a211-139">Next, press the **Refresh** button.</span></span>
5. <span data-ttu-id="8a211-140">Снова просмотрите данные TodoItem на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8a211-140">View the TodoItem data again in the Azure portal.</span></span> <span data-ttu-id="8a211-141">Должны отображаться как новые, так и измененные TodoItem.</span><span class="sxs-lookup"><span data-stu-id="8a211-141">The new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a211-142">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8a211-142">Additional Resources</span></span>
* <span data-ttu-id="8a211-143">[Автономная синхронизация данных в мобильных приложениях Azure]</span><span class="sxs-lookup"><span data-stu-id="8a211-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="8a211-144">[Облачное покрытие: автономная синхронизация в мобильных службах Azure] \(примечание: видео рассказывает о мобильных службах, однако точно так же автономная синхронизация работает в мобильных службах Azure\).</span><span class="sxs-lookup"><span data-stu-id="8a211-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: the video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

<span data-ttu-id="8a211-145">[Автономная синхронизация данных в мобильных приложениях Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="8a211-145">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

<span data-ttu-id="8a211-146">[Создание приложения Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="8a211-146">[Create an Android App]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="8a211-147">[Облачное покрытие: автономная синхронизация в мобильных службах Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="8a211-147">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

