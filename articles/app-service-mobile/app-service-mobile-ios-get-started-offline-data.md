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
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a>Включение автономной синхронизации с помощью мобильных приложений iOS
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Обзор
В этом учебнике автономной синхронизации с hello функция службы приложений Azure мобильные приложения для iOS. С автономной синхронизации конечные пользователи могут взаимодействовать с tooview мобильного приложения и добавлять изменения данных, даже в том случае, если они не имеют сетевых подключений. Изменения сохраняются в локальной базе данных. После hello устройство вернется в оперативный режим, hello изменения синхронизируются с hello удаленного серверной части.

Если это ваш первый опыт работы с мобильным приложениям, следует сначала выполнить учебника hello [создать приложение iOS]. Если проект сервера краткое загружаются hello не используется, необходимо добавить проект tooyour пакеты расширения доступа к данным hello. Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn Дополнительные сведения о функции hello автономной синхронизации, в разделе [автономной синхронизации данных в мобильных приложениях].

## <a name="review-sync"></a>Просмотрите код синхронизации приветствия клиента
Hello клиентский проект, загруженный для hello [создать приложение iOS] учебник уже содержит код, который поддерживает синхронизацию в автономном режиме с помощью локальной базы данных на базе основных данных. В этом разделе перечислены новые уже включен в учебник кода hello. Концептуальный обзор функции hello. в разделе [автономной синхронизации данных в мобильных приложениях].

С помощью функции hello автономной синхронизации данных мобильных приложений конечные пользователи могут взаимодействовать с локальной базы данных даже в том случае, когда hello сеть недоступна. toouse эти функции в вашем приложении инициализации контекста синхронизации hello `MSClient` и ссылаться на локальное хранилище. Затем можно ссылаться на таблицы через hello **MSSyncTable** интерфейса.

В **QSTodoService.m** (Objective-C) или **ToDoTableViewController.swift** (Swift), обратите внимание, что тип члена hello hello **syncTable** —  **MSSyncTable**. Автономная синхронизация использует этот интерфейс таблицы синхронизации вместо **MSTable**. При использовании таблицы синхронизации, все операции перейдите toohello локальное хранилище и синхронизируются только с hello удаленного серверной части с явной передачи и операций по запросу.

 tooget tooa синхронизации ссылочной таблицы, используйте hello **syncTableWithName** метод `MSClient`. Автономная синхронизация функций tooremove, **tableWithName** вместо него.

Перед выполнением любых операций таблицы hello локального хранилища должен быть инициализирован. Ниже приведен соответствующий код hello:

* **Objective-C**. В hello **QSTodoService.init** метод:

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* **Swift**. В hello **ToDoTableViewController.viewDidLoad** метод:

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   Этот метод создает локального хранилища с помощью hello `MSCoreDataStore` предоставляет интерфейс, который hello пакет SDK для мобильных приложений. Кроме того, можно предоставить различные локальное хранилище путем реализации hello `MSSyncContextDataSource` протокола. Кроме того, hello первый параметр **MSSyncContext** является используется toospecify обработчика конфликтов. Так как мы прошли `nil`, мы получаем конфликтов по умолчанию hello обработчик, который не выполняется на любого конфликта.

Теперь давайте выполнения операции синхронизации фактическое hello и получение данных из удаленного серверной части hello:

* **Objective-C**. `syncData`Помещает сначала новые изменения, а затем вызывает **pullData** tooget данных из удаленного серверной части hello. Здравствуйте, в свою очередь, **pullData** метод получает новые данные, совпадает с запросом:

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
* **Swift**:
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

В версии hello Objective-C в `syncData`, сначала вызовите **pushWithCompletion** в контексте синхронизации hello. Этот метод является членом `MSSyncContext` (и не hello синхронизации сама таблица), так как он помещает изменения для всех таблиц. Только те записи, которые были изменены каким-либо образом локально (с помощью операции CUD) отправляются toohello сервера. Затем hello вспомогательный **pullData** вызове, который вызывает **MSSyncTable.pullWithQuery** tooretrieve удаленных данных и сохраняет его в локальной базе данных hello.

В версии Swift hello, так как операция отправки hello не является обязательным, отсутствует вызов слишком**pushWithCompletion**. Если все ожидающие изменения в контексте hello синхронизации для таблицы hello, осуществляющего принудительной отправки, запросу всегда выдает push сначала. Однако при наличии более одной таблицы синхронизации, это лучший tooensure принудительной вызова tooexplicitly, что все, что является согласованным для всех связанных таблиц.

В hello Objective-C и Swift версий можно использовать hello **pullWithQuery** toospecify метод toofilter запроса hello tooretrieve записи. В этом примере hello запрос получает все записи в удаленном hello `TodoItem` таблицы.

Здравствуйте, второй параметр **pullWithQuery** является Идентификатором запроса, который используется для *добавочной синхронизации*. Добавочной синхронизации извлекает только те записи, которые были изменены с момента последней синхронизации hello, с помощью записи hello `UpdatedAt` отметка времени (называется `updatedAt` в hello локальное хранилище.) hello идентификатор запроса должен быть строку описания, которое является уникальным для каждого логического запроса в приложение. tooopt за пределы добавочной синхронизации, передайте `nil` как hello ИД запроса. Этот подход может привести к снижению производительности, так как при каждой операции извлечения будут извлекаться все записи.

приложение Hello Objective-C синхронизируется при изменении или добавлении данных, когда пользователь выполняет обновление жестов hello и при запуске.

Swift приложение Hello синхронизируется при пользователем hello жестов hello обновления и при запуске.

За hello синхронизации приложения всякий раз, когда данные изменения (Objective-C) или при запуске приложение hello (Objective-C и Swift), приложение hello предполагается, что этот пользователь hello находится в оперативном режиме. В следующем разделе потребуется обновить приложение hello, чтобы пользователи могли изменять даже в том случае, если они находятся в автономном режиме.

## <a name="review-core-data"></a>Просмотрите hello основных данных модели
При использовании автономного хранилища hello основных данных, необходимо определить отдельные таблицы и поля в модели данных. Пример приложения Hello уже есть модель данных с hello неправильный формат. В этом разделе будут рассмотрены tooshow эти таблицы как они используются.

Откройте **QSDataModel.xcdatamodeld**. Четыре таблицы будут определены - 3, используемым hello SDK и элементов, используемая для hello задачи:
  * MS_TableOperations: Отслеживает hello элементы, которые должны toobe синхронизируются с сервером hello.
  * MS_TableOperationErrors: отслеживает ошибки, возникающие во время автономной синхронизации.
  * MS_TableConfig: Отслеживает hello время последнего обновления hello последняя операция синхронизации для всех операций по запросу.
  * TodoItem: Задача hello сохраняет сообщения. Здравствуйте, системные столбцы **createdAt**, **updatedAt**, и **версии** — это необязательные системные свойства.

> [!NOTE]
> пакет SDK для мобильных приложений Hello резервирует имена столбцов, которые начинаются с «**``**». Не используйте этот префикс где-либо, кроме системных столбцов. В противном случае в именах столбцов изменяются при использовании удаленного серверной части hello.
>
>

При использовании функции автономных синхронизации hello определение hello три системные таблицы и таблицы данных hello.

### <a name="system-tables"></a>Системные таблицы

**MS_TableOperations**  

![Атрибуты таблицы MS_TableOperations][defining-core-data-tableoperations-entity]

| Атрибут | Тип |
| --- | --- |
| id | Integer 64 |
| itemId | Строка |
| properties | Двоичные данные |
| таблица | Строка |
| tableKind | Integer 16 |


**MS_TableOperationErrors**

 ![Атрибуты таблицы MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| Атрибут | Тип |
| --- | --- |
| id |Строка |
| operationId |Integer 64 |
| properties |Двоичные данные |
| tableKind |Integer 16 |

 **MS_TableConfig**

 ![][defining-core-data-tableconfig-entity]

| Атрибут | Тип |
| --- | --- |
| id |Строка |
| key |Строка |
| keyType |Integer 64 |
| таблица |Строка |
| значение |Строка |

### <a name="data-table"></a>Таблица данных

**TodoItem**

| Атрибут | Тип | Примечание. |
| --- | --- | --- |
| id | Строка, помеченная как обязательная |Первичный ключ в удаленном хранилище |
| complete | Логический | Поле элемента списка дел |
| text |Строка |Поле элемента списка дел |
| дата создания | Дата | (необязательно) Сопоставляет слишком**createdAt** системного свойства |
| дата обновления | Дата | (необязательно) Сопоставляет слишком**updatedAt** системного свойства |
| версия | Строка | (необязательно) Используется toodetect конфликты, tooversion карты |

## <a name="setup-sync"></a>Изменить поведение синхронизации hello приложение hello
В этом разделе можно изменить приложение hello, чтобы он не выполняется синхронизация на запуск приложения или при вставки и обновления элементов. Она синхронизируется только в том случае, когда кнопка жестов hello обновления выполняется.

**Objective-C**:

1. В **QSTodoListViewController.m**, измените hello **viewDidLoad** tooremove метод hello вызовов слишком`[self refresh]` конце hello метод hello. Теперь hello данных не синхронизированы с сервером hello на запуск приложения. Она синхронизируется с содержимым hello hello локального хранилища.
2. В **QSTodoService.m**, изменять определение hello `addItem` , чтобы он не синхронизировать после вставки элемента hello. Удалите hello `self syncData` блокировку и замените hello следующее:

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. Изменить определение hello `completeItem` как было сказано ранее. Удалите блок hello для `self syncData` и заменить ее именем hello следующее:
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

**Swift**:

В `viewDidLoad`в **ToDoTableViewController.swift**, закомментируйте hello две строки, показанный здесь, toostop синхронизации на запуск приложения. На момент написания этой статьи hello приложение Swift Todo hello не обновить службу hello когда кто-то добавляет или завершения элемент. Обновляет службу hello только на запуск приложения.

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <a name="test-app"></a>Тестовое приложение hello
В этом разделе подключения tooan toosimulate недопустимый URL-адрес в случае автономной работы. При добавлении элементов данных, все они удерживали в hello хранить локальные основные данные, но они все не синхронизированы с серверной части мобильное приложение hello.

1. Изменить URL-адрес мобильного приложения hello в **QSTodoService.m** tooan недопустимый URL-адрес, а также выполнения hello приложение еще раз:

   **Objective-C**. В файле QSTodoService.m:
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   **Swift**. В файле ToDoTableViewController.swift:
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. Добавьте несколько элементов списка дел. Закройте имитатор hello (или приложение hello принудительно закрыть) и перезапустите ее. Убедитесь, что изменения сохранились.

3. Просмотрите содержимое hello hello удаленного **TodoItem** таблицы:
   * Для серверной Node.js, go toohello [портал Azure](https://portal.azure.com/) и в серверной части вашего мобильного приложения, выберите **простой таблицы** > **TodoItem**.  
   * Для серверной части .NET используйте средства SQL, например SQL Server Management Studio, или клиент REST, например Fiddler или Postman.  

4. Убедитесь, что новые элементы hello *не* был синхронизирован с сервером hello.

5. Изменение hello URL-адрес обратной toohello исправьте значение одного их в **QSTodoService.m**и приложение hello повторного запуска.

6. Для выполнения обновления жестов hello перетащите вниз hello список элементов.  
Отобразится счетчик хода выполнения.

7. Представление hello **TodoItem** данных еще раз. Теперь должны отображаться Hello задача новых и измененных элементов.

## <a name="summary"></a>Сводка
Функция автономного синхронизации toosupport hello, мы использовали hello `MSSyncTable` интерфейс и инициализируется `MSClient.syncContext` с локальным хранилищем. В этом случае локальное хранилище hello был баз данных на основе основных данных.

При использовании локального хранилища основных данных, необходимо определить несколько таблиц с hello [исправить системные свойства](#review-core-data).

Обычный Hello создание, чтение, обновление и удаление (CRUD) для мобильным приложениям применяются как в том случае, если приложение hello по-прежнему подключен, но все операции hello происходят запросы hello локального хранилища.

При локальном хранилище hello мы синхронизируются с сервером hello, мы использовали hello **MSSyncTable.pullWithQuery** метод.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [автономной синхронизации данных в мобильных приложениях]
* [Облака охватывает следующие темы. Автономная синхронизация в мобильных службах Azure] \(hello видео посвящена мобильных служб, но мобильные приложения в автономный режим синхронизации работает аналогичным образом.\)

<!-- URLs. -->


[создать приложение iOS]: app-service-mobile-ios-get-started.md
[автономной синхронизации данных в мобильных приложениях]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Облака охватывает следующие темы. Автономная синхронизация в мобильных службах Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
