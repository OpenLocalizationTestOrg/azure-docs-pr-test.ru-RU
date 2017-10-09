---
title: "aaaEnable автономной синхронизации для мобильного приложения Azure (Xamarin Android)"
description: "Узнайте, как toouse приложение службы мобильных приложений toocache и синхронизации автономные данные в приложение Xamarin Android"
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 91d59e4b-abaa-41f4-80cf-ee7933b32568
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 216ba76ae49f583273cc61b63114a415eca2477b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinandroid-mobile-app"></a>Включение автономной синхронизации для мобильного приложения Xamarin.Android
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Обзор
В этом учебнике рассказывается функции hello автономной синхронизации мобильных приложений Azure для Xamarin.Android. Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением — Просмотр, добавление или изменение данных — даже в том случае, если нет сетевого соединения. Изменения сохраняются в локальной базе данных.
Как только устройство hello вернется в оперативный режим, эти изменения синхронизируются с hello удаленной службы.

В этом учебнике обновить hello клиентский проект из учебника hello [создать приложение Xamarin Android] toosupport hello автономным функциям мобильных приложений Azure. Если вы не используете hello загружен быстрый запуск сервера проекта, необходимо добавить проект tooyour пакеты расширения доступа hello данных. Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn Дополнительные сведения о функции hello автономной синхронизации, см. разделе hello [автономной синхронизации данных в мобильных приложениях Azure].

## <a name="update-hello-client-app-toosupport-offline-features"></a>Обновление автономных функции приложения клиента toosupport hello
Автономные компоненты мобильного приложения Azure позволяют toointeract с локальной базы данных в автономный режим. toouse инициализировать эти функции в вашем приложении [SyncContext] tooa локального хранилища. Затем ссылаться на таблицы через hello [IMobileServiceSyncTable] [IMobileServiceSyncTable] интерфейса. SQLite используется как hello локальное хранилище на устройстве hello.

1. В Visual Studio откройте диспетчер пакетов NuGet hello в проекте hello, выполненной в hello [создать приложение Xamarin Android] учебника.  Поиск и установка hello **Microsoft.Azure.Mobile.Client.SQLiteStore** пакет NuGet.
2. Откройте файл ToDoActivity.cs hello и раскомментируйте hello `#define OFFLINE_SYNC_ENABLED` определения.
3. В Visual Studio нажмите клавишу hello **F5** ключевые toorebuild и выполнения hello клиентского приложения. приложение Hello работает так же, как было до включения автономной синхронизации hello. Тем не менее hello локальной базы данных теперь заполняется данными, можно использовать в автономный режим.

## <a name="update-sync"></a>Обновить toodisconnect приложения hello из внутреннего hello
В этом разделе можно разделить hello подключения tooyour мобильное приложение серверной toosimulate ситуации вне сети. При добавлении элементов данных, то обработчик исключений о том, что приложение hello находится в автономном режиме. В этом состоянии новые элементы, добавленные в hello локального хранения и синхронизируемые с внутреннего сервера мобильного приложения hello, при выполнении принудительной в подключенном состоянии.

1. Измените ToDoActivity.cs в общий проект hello. Изменение hello **applicationURL** toopoint, недопустимый tooan URL-адрес:

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    Также можно показать автономного поведение путем отключения Wi-Fi и сотовой сети на устройстве hello, или с помощью режима "в самолете".
2. Нажмите клавишу **F5** toobuild и запустите приложение hello. Обратите внимание, синхронизации не удалось выполнить обновление Здравствуйте, при запуске приложения.
3. Введите новые элементы. Учтите, что при каждом нажатии кнопки **Сохранить** отправка завершается сбоем с состоянием [CancelledByNetworkError]. Тем не менее новые элементы todo hello существует в локальном хранилище hello, пока не могут быть принудительно toohello внутреннего сервера мобильного приложения.  В рабочей среде приложения, при отключении этих исключений, которые клиентское приложение hello ведет себя как если бы она по-прежнему подключен toohello внутреннего сервера мобильного приложения.
4. Закройте приложение hello и перезапустите его tooverify, hello новые элементы, созданные сохраненного toohello локального хранилища.
5. В Visual Studio в откройте **обозреватель сервера**. Перейдите tooyour базы данных в **Azure**->**баз данных SQL**. Щелкните правой кнопкой мыши базу данных и выберите пункт **Открыть в обозревателе объектов SQL Server**. Теперь можно просмотреть tooyour таблицы базы данных SQL и ее содержимое. Убедитесь, что не изменилось hello данные в базе данных серверной части hello.
6. (Необязательно) С помощью средства REST, например Fiddler или почтальон tooquery вашей мобильной серверной части, используя запрос GET в форме `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Обновить tooreconnect приложения hello внутренний сервер приложений для мобильных устройств
В этом разделе переподключить внутреннего сервера мобильного приложения toohello приложения hello. При первом запуске приложения hello, hello `OnCreate` вызовов обработчика событий `OnRefreshItemsSelected`. Этот метод вызывает метод `SyncAsync` toosync локального хранения с hello серверной базе данных.

1. Откройте ToDoActivity.cs в общий проект hello и отменить изменения в hello **applicationURL** свойство.
2. Нажмите клавишу hello **F5** ключевые toorebuild и приложение hello выполнения. Hello приложение выполнит синхронизацию локальных изменений с серверной hello мобильного приложения Azure, с помощью принудительной отправки и запросов операций при hello `OnRefreshItemsSelected` выполнения метода.
3. (Необязательно) Представление hello обновленных данных, с помощью обозревателя объектов SQL Server или средством REST, например Fiddler. Обратите внимание hello данные синхронизированы между hello мобильного приложения Azure серверной базой данных и hello локального хранилища.
4. В приложение hello, нажмите кнопку Проверить hello поле рядом с несколько элементов toocomplete их в локальном хранилище hello.

   `CheckItem`вызовы `SyncAsync` элемент toosync каждого завершена с внутреннего сервера мобильного приложения hello. `SyncAsync` вызывает операцию отправки и извлечения данных. **При каждом выполнении запросу к таблице hello клиента были внесены изменения, push всегда выполняется автоматически**. Это позволяет обеспечить согласованность всех таблиц в локальном хранилище, а также связей между ними. Такое поведение может привести к непредвиденной отправке данных. Дополнительные сведения об этом поведении см. в статье [автономной синхронизации данных в мобильных приложениях Azure].

## <a name="review-hello-client-sync-code"></a>Просмотрите код синхронизации приветствия клиента
Hello Xamarin клиентский проект, загруженный после завершения учебника hello [создать приложение Xamarin Android] уже содержит код поддержки синхронизации в автономном режиме с помощью локальной базы данных SQLite. Ниже приведен краткий обзор уже содержание hello учебника код. Концептуальный обзор функции hello. в разделе [автономной синхронизации данных в мобильных приложениях Azure].

* Перед выполнением любых операций таблицы hello локального хранилища должен быть инициализирован. Hello базы данных в локальном хранилище инициализируется при `ToDoActivity.OnCreate()` выполняет `ToDoActivity.InitLocalStoreAsync()`. Этот метод создает локальную базу данных SQLite, с помощью hello `MobileServiceSQLiteStore` класс, предоставляемый клиентом hello мобильных приложений Azure SDK.

    Hello `DefineTable` метод создает таблицу в hello локального хранилища, соответствующий hello поля в типе hello предоставленный `ToDoItem` в этом случае. Тип Hello не имеет tooinclude все столбцы hello hello удаленной базы данных. Это возможно toostore только подмножество столбцов.

        // ToDoActivity.cs
        private async Task InitLocalStoreAsync()
        {
            // new code tooinitialize hello SQLite store
            string path = Path.Combine(System.Environment
                .GetFolderPath(System.Environment.SpecialFolder.Personal), localDbFilename);

            if (!File.Exists(path))
            {
                File.Create(path).Dispose();
            }

            var store = new MobileServiceSQLiteStore(path);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            // toouse a different conflict handler, pass a parameter tooInitializeAsync.
            // For more details, see http://go.microsoft.com/fwlink/?LinkId=521416.
            await client.SyncContext.InitializeAsync(store);
        }
* Hello `toDoTable` членом `ToDoActivity` имеет hello `IMobileServiceSyncTable` введите вместо `IMobileServiceTable`. Hello IMobileServiceSyncTable направляет все создания, чтения, обновления и удаления (CRUD) таблицы операций toohello локального хранилища базы данных.

    Решите, когда изменения передаются внутреннего сервера приложения Azure Mobile toohello путем вызова `IMobileServiceSyncContext.PushAsync()`. Hello контекста синхронизации помогает сохранить связи между таблицами, отслеживания и опубликуйте изменения во всех таблицах в клиентском приложении был изменен при `PushAsync` вызывается.

    Hello предоставленный код вызывает `ToDoActivity.SyncAsync()` toosync при обновлении списка todoitem hello или todoitem добавляется или завершено. Синхронизация кода Hello после каждого локального изменения.

    В коде указано hello все записи hello удаленного `TodoItem` получат таблицы, но это также возможно toofilter записей, передавая идентификатор запроса и запрос слишком`PushAsync`. Дополнительные сведения см в разделе hello *добавочной синхронизации* в [автономной синхронизации данных в мобильных приложениях Azure].

        // ToDoActivity.cs
        private async Task SyncAsync()
        {
            try {
                await client.SyncContext.PushAsync();
                await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
            } catch (Java.Net.MalformedURLException) {
                CreateAndShowDialog (new Exception ("There was an error creating hello Mobile Service. Verify hello URL"), "Error");
            } catch (Exception e) {
                CreateAndShowDialog (e, "Error");
            }
        }

## <a name="additional-resources"></a>Дополнительные ресурсы
* [автономной синхронизации данных в мобильных приложениях Azure]
* [Использование пакета SDK .NET для мобильных приложений Azure][8]

<!-- URLs. -->
[создать приложение Xamarin Android]: ../app-service-mobile-xamarin-android-get-started.md
[автономной синхронизации данных в мобильных приложениях Azure]: ../app-service-mobile-offline-data-sync.md

<!-- Images -->

<!-- URLs. -->
[Создание приложения Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md
[Автономная синхронизация данных в мобильных приложениях Azure]: app-service-mobile-offline-data-sync.md
[Xamarin Studio]: http://xamarin.com/download
[Xamarin extension]: http://xamarin.com/visual-studio
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
