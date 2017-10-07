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
# <a name="enable-offline-sync-for-your-android-mobile-app"></a>Включение автономной синхронизации для мобильного приложения Android
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Обзор
В этом учебнике приведены функции hello автономной синхронизации мобильных приложений Azure для Android. Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением&mdash;Просмотр, добавление или изменение данных&mdash;даже в том случае, если нет сетевого соединения. Изменения сохраняются в локальной базе данных. Как только устройство hello вернется в оперативный режим, эти изменения синхронизируются с hello удаленной базы данных.

Если это ваш первый опыт работы с мобильных приложений Azure, сначала следует выполнить hello учебника [создать приложение Android]. Если вы не используете hello загружен быстрый запуск сервера проекта, необходимо добавить проект tooyour пакеты расширения доступа hello данных. Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn Дополнительные сведения о функции hello автономной синхронизации, см. разделе hello [автономной синхронизации данных в мобильных приложениях Azure].

## <a name="update-hello-app-toosupport-offline-sync"></a>Обновление автономной синхронизации hello приложения toosupport
С автономной синхронизации можно просматривать, записывать tooand из *синхронизации таблицы* (с помощью hello *IMobileServiceSyncTable* интерфейса), который является частью **SQLite** базы данных на устройстве.

toopush и запросу изменения между устройством hello и мобильных служб Azure, вы используете *контекст синхронизации* (*MobileServiceClient.SyncContext*), который инициализируется с помощью hello локальной базы данных toostore данные локально.

1. В `TodoActivity.java`, закомментируйте hello существующим определением `mToDoTable` и раскомментируйте следующую версию таблицы hello синхронизации:
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. В hello `onCreate` метод закомментируйте hello существующей инициализации `mToDoTable` и раскомментируйте это определение:
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. В `refreshItemsFromTable` закомментируйте определение hello `results` и раскомментируйте это определение:
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. Закомментируйте определение hello `refreshItemsFromMobileServiceTable`.
5. Раскомментируйте hello определение `refreshItemsFromMobileServiceTableSyncTable`:
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. Раскомментируйте hello определение `sync`:
   
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

## <a name="test-hello-app"></a>Тестовое приложение hello
В этом разделе тестировать поведение hello Wi-Fi на и затем выключите toocreate Wi-Fi в случае автономной работы.

При добавлении элементов данных, они хранятся в локальное хранилище SQLite hello, но не синхронизирован toohello мобильной службы, до нажатия клавиши hello **обновление** кнопки. Другие приложения могут применяться другие требования относительно toobe синхронизирован, когда потребуется данных, но для демонстрационных целей этого учебника имеет явно запросить пользователя hello.

При нажатии этой кнопки запускается новая фоновая задача. Помещает сначала все изменения, внесенные toohello локального хранилища с помощью контекст синхронизации, а затем переносит все изменения данных из локальной таблицы Azure toohello.

### <a name="offline-testing"></a>Тестирование в автономном режиме
1. Место hello устройство или симулятор в *режим "в самолете"*. Это позволит смоделировать автономный сценарий.
2. Добавьте несколько элементов *ToDo* или отметьте некоторые элементы как завершенные. Закройте hello устройство или симулятор (или приложение hello принудительно закрыть) и перезапустите. Убедитесь, что изменения были сохранены на устройстве hello, так как они хранятся в локальном хранилище SQLite hello.
3. Просмотрите содержимое hello hello Azure *TodoItem* таблицы с помощью средства SQL, таких как *SQL Server Management Studio*, или клиент REST, такие как *Fiddler* или  *Почтальон*. Убедитесь, что новые элементы hello *не* был синхронизирован toohello сервера
   
       + Для внутреннего Node.js go toohello [портал Azure](https://portal.azure.com/), и мобильные приложения серверной части, нажмите кнопку **простой таблицы** > **TodoItem** tooview содержимое hello hello `TodoItem` таблицы.
       + Для серверного приложения .NET, просмотр таблицы hello содержимое с помощью средства SQL например *SQL Server Management Studio*, или клиент REST, такие как *Fiddler* или *почтальон*.
4. Включите Wi-Fi hello устройства или симулятора. Нажмите hello **обновление** кнопки.
5. Просмотр данных TodoItem hello снова в hello портал Azure. Здравствуйте, появятся новые и измененные TodoItems.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [автономной синхронизации данных в мобильных приложениях Azure]
* [Облака охватывает следующие темы. Автономная синхронизация в мобильных службах Azure] \(Примечание: hello видео на мобильных служб, но автономной синхронизации работает аналогичным образом в мобильных приложениях Azure\)

<!-- URLs. -->

[автономной синхронизации данных в мобильных приложениях Azure]: app-service-mobile-offline-data-sync.md

[создать приложение Android]: app-service-mobile-android-get-started.md

[Облака охватывает следующие темы. Автономная синхронизация в мобильных службах Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

