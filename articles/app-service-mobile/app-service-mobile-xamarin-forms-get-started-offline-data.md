---
title: "aaaEnable автономную синхронизацию Azure мобильное приложение (Xamarin.Forms) | Документы Microsoft"
description: "Узнайте, как приложение службы мобильных приложений toocache и синхронизации автономных данных в приложении Xamarin.Forms toouse"
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a>Включение автономной синхронизации мобильного приложения Xamarin.Forms
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Обзор
В этом учебнике рассказывается функции hello автономной синхронизации мобильных приложений Azure для Xamarin.Forms. Автономная синхронизация позволяет конечным пользователям взаимодействовать с мобильным приложением — просматривать, добавлять или изменять данные — даже при отсутствии подключения к сети. Изменения сохраняются в локальной базе данных. Как только устройство hello вернется в оперативный режим, эти изменения синхронизируются с hello удаленной службы.

Этот учебник основывается на hello решения Xamarin.Forms краткое руководство для мобильных приложений, созданный после завершения этого учебника [создание приложения Xamarin iOS]. решение краткое руководство Hello для Xamarin.Forms содержит hello кода toosupport автономной синхронизации, которой требуется только toobe включена. В этом учебнике обновить tooturn решения hello краткое руководство о hello автономных компонентах мобильных приложений Azure. Мы также выделяет hello автономного код в приложение hello. Если решение краткое руководство загружаются hello не используется, необходимо добавить проект tooyour пакеты расширения доступа hello данных. Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure][1].

toolearn Дополнительные сведения о функции hello автономной синхронизации, см. разделе hello [автономной синхронизации данных в мобильных приложениях Azure][2].

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a>Включить функции автономной синхронизации в решении hello краткое руководство
Код автономной синхронизации Hello включен в проект hello с помощью директивы препроцессора C#. Здравствуйте, когда **OFFLINE\_СИНХРОНИЗАЦИИ\_включено** символ определен, эти пути кода, включаются в сборку hello. Для приложений Windows также необходимо установить платформу SQLite hello.

1. В Visual Studio щелкните правой кнопкой мыши решение hello > **управление пакетами NuGet для решения...** , выполните поиск и установка **Microsoft.Azure.Mobile.Client.SQLiteStore** пакет NuGet для всех проектов в решении hello.
2. В hello обозревателе решений откройте файл TodoItemManager.cs hello из проекта hello с **переносимой** в hello имя, являющееся проекта переносимой библиотеки классов, затем снимите комментарий hello, следующий за директивой препроцессора:

        #define OFFLINE_SYNC_ENABLED
3. (Необязательно) toosupport устройства Windows, установите одно из следующих пакетов среды выполнения SQLite hello.

   * **Среда выполнения Windows 8.1**: установите [SQLite для Windows 8.1][3].
   * **Windows Phone 8.1**: установите [SQLite для Windows Phone 8.1][4].
   * **Универсальная платформа Windows** установить [SQLite для универсальной универсальное приложение для Windows hello][5].

     Несмотря на то, что hello краткое руководство не содержит проект универсального приложения Windows, Xamarin Forms поддерживается hello универсальной платформы Windows.
4. (Необязательно) В каждом проекте приложения Windows, щелкните правой кнопкой мыши **ссылки** > **добавить ссылку...** , разверните hello **Windows** папки > **расширения**.
    Включить соответствующие hello **SQLite для Windows** пакета SDK, а также hello **Visual C++ 2013 среды выполнения для Windows** SDK.
    Hello SQLite SDK имена будут немного отличаться с каждой платформы Windows.

## <a name="review-hello-client-sync-code"></a>Просмотрите код синхронизации приветствия клиента
Ниже приведен краткий обзор уже содержание hello учебника код внутри hello `#if OFFLINE_SYNC_ENABLED` директивы. Функциональность автономной синхронизации — в файле проекта TodoItemManager.cs hello в hello проекта переносимой библиотеки классов. Концептуальный обзор функции hello. в разделе [автономной синхронизации данных в мобильных приложениях Azure][2].

* Перед выполнением любых операций таблицы hello локального хранилища должен быть инициализирован. Hello локального хранилища базы данных инициализируется в hello **TodoItemManager** конструктор класса с помощью hello, следующий код:

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    Этот код создает новый локальный SQLite базу данных с помощью hello **MobileServiceSQLiteStore** класса.

    Hello **DefineTable** метод создает таблицу в hello локального хранилища, соответствующий hello поля типа указано hello.  Тип Hello не имеет tooinclude все столбцы hello hello удаленной базы данных. Это возможно toostore подмножество столбцов.
* Hello **todoTable** в **TodoItemManager** — **IMobileServiceSyncTable** введите вместо **IMobileServiceTable**. Этот класс использует hello локальной базы данных для всех создания, чтения, обновления и удаления (CRUD) табличные операции. Решите, когда эти изменения передаются внутреннего сервера мобильного приложения toohello путем вызова **PushAsync** на hello **IMobileServiceSyncContext**. Hello контекста синхронизации помогает сохранить связи между таблицами, отслеживания и опубликуйте изменения во всех таблицах в клиентском приложении был изменен при **PushAsync** вызывается.

    следующие Hello **SyncAsync** toosync с внутреннего сервера мобильного приложения hello вызывается метод:

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }

            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting tooserver's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    В этом примере используется простой обработки ошибок с помощью обработчика синхронизации по умолчанию hello. Реальном приложении будет обрабатываться hello различные ошибки, например состояния сети и сервера конфликтует с помощью пользовательского **IMobileServiceSyncHandler** реализации.

## <a name="offline-sync-considerations"></a>Рекомендации по автономной синхронизации
В образце hello hello **SyncAsync** метод вызывается только при запуске и при запросе синхронизации.  tooinitiate синхронизации в приложении Android или iOS, запросу вниз в списке элементов hello; для Windows, используйте hello **синхронизации** кнопки. В реальном приложении также может разместить hello триггер синхронизации, при изменении состояния сети hello.

При выполнении запросу к таблице, имеющей ожидающие локального обновления отслеживаются контекстом hello, извлечь операции автоматически триггеры предыдущей принудительной контекста. При обновлении, добавление и завершение работы элементов в этом примере, можно опустить hello явные **PushAsync** вызова.

В коде указано hello запрашиваются все записи в удаленной таблице TodoItem hello, но это также возможно toofilter записей, передавая идентификатор запроса и запрос слишком**PushAsync**. Дополнительные сведения см в разделе hello *добавочной синхронизации* в [автономной синхронизации данных в мобильных приложениях Azure][2].

## <a name="run-hello-client-app"></a>Запустить клиентское приложение hello
С автономной синхронизации теперь включена запустите клиентское приложение hello по крайней мере один раз в каждой базе данных локального хранилища платформы toopopulate hello. Позже имитировать автономный режим и изменить hello данные в локальном хранилище hello, когда приложение hello отключен от сети.

## <a name="update-hello-sync-behavior-of-hello-client-app"></a>Обновить hello синхронизации поведение клиентского приложения hello
В этом разделе измените toosimulate проекта клиента hello в случае автономной работы с помощью URL-адрес приложения, недопустимый для серверной части. Кроме того, можно отключить сетевых подключений, перемещая устройства слишком «"Режим" в самолете».  При добавлении или изменении элементов данных, эти изменения, которые содержатся в локальном хранилище hello, но не синхронизированных данных серверной части toohello сохранение, пока hello подключение будет восстановлено.

1. В hello обозревателе решений откройте файл проекта Constants.cs hello из hello **переносимой** проекта и измените значение hello `ApplicationURL` недопустимый URL-адрес toopoint tooan:

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. Привет открыть файл TodoItemManager.cs из hello **переносимой** проекта, а затем добавьте **перехватывать** для hello базовый **исключение** toohello класса **try... catch** блока в **SyncAsync**. Это **перехватывать** блок записывает консоли toohello сообщение hello исключения, следующим образом:

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. Постройте и запустите клиентское приложение hello.  Добавьте несколько новых элементов. Обратите внимание, в консоли hello для каждой попытки toosync с серверной hello регистрируется исключение. Эти новые элементы существуют только в локальном хранилище hello, пока их можно отправить toohello мобильной серверной части. клиентское приложение Hello, ведет себя как toohello подключенной базы данных, поддерживающий все создавать, читать, update, операции удаления (CRUD).
4. Закройте приложение hello и перезапустите его tooverify, hello новые элементы, созданные сохраненного toohello локального хранилища.
5. (Необязательно) С помощью Visual Studio tooview вашей toosee таблицы базы данных SQL Azure, hello данные в базе данных серверной части hello не изменились.

    В Visual Studio в откройте **обозреватель сервера**. Перейдите tooyour базы данных в **Azure**->**баз данных SQL**. Щелкните правой кнопкой мыши базу данных и выберите пункт **Открыть в обозревателе объектов SQL Server**. Теперь можно просмотреть tooyour таблицы базы данных SQL и ее содержимое.

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a>Обновление серверной части мобильных tooreconnect приложения hello клиента
В этом разделе переподключение hello toohello мобильного внутреннего сервера приложения, которое имитирует приложение hello, приходящие обратно tooan оперативном состоянии. При выполнении жестов hello обновления данных — синхронизированных tooyour мобильной серверной части.

1. Снова откройте Constants.cs. Правильный hello `applicationURL` toopoint toohello исправьте URL-адрес.
2. Повторное построение и запуск клиентского приложения hello. приложение Hello попыток toosync с внутреннего сервера мобильного приложения hello после запуска. Проверьте регистрацию ни одного исключения в консоли отладки hello.
3. (Необязательно) Представление hello обновленные данные, с помощью обозревателя объектов SQL Server или средств REST, как Fiddler или [почтальон][6]. Обратите внимание hello данные синхронизированы между hello серверной базой данных и hello локального хранилища.

    Обратите внимание, данные hello синхронизации между базой данных hello и локальное хранилище hello и содержит элементы hello, добавленного в автономном приложении.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Синхронизация автономных данных в мобильных приложениях Azure][2]
* [Использование пакета SDK .NET для мобильных приложений Azure][8]

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
