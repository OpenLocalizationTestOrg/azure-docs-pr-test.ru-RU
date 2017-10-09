---
title: "aaaEnable автономной синхронизации для приложения универсальной платформы Windows (UWP) с приложениями для мобильных устройств | Документы Microsoft"
description: "Узнайте, как toouse мобильного приложения Azure toocache и синхронизировать данные в приложении универсальной платформы Windows (UWP)."
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 8fe51773-90de-4014-8a38-41544446d9b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: a9f4ad02e92c2c423f10f07b7f1a4270aafd6c6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-windows-app"></a>Включение автономной синхронизации для приложения для Windows
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Обзор
Этом учебнике показано, как tooadd в автономном режиме поддерживают tooa приложения универсальной платформы Windows (UWP), с помощью внутреннего мобильного приложения Azure. Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением — Просмотр, добавление или изменение данных — даже в том случае, если нет сетевого соединения. Изменения сохраняются в локальной базе данных. Как только устройство hello вернется в оперативный режим, эти изменения синхронизируются с hello удаленной базы данных.

В этом учебнике обновление проекта приложения UWP hello из учебника hello [создать приложение Windows] toosupport hello автономным функциям мобильных приложений Azure. Если вы не используете hello загружен быстрый запуск сервера проекта, необходимо добавить проект tooyour пакеты расширения доступа hello данных. Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn Дополнительные сведения о функции hello автономной синхронизации, см. разделе hello [автономной синхронизации данных в мобильных приложениях Azure].

## <a name="requirements"></a>Требования
Этот учебник требует hello следующие необходимые компоненты:

* Visual Studio 2013 в Windows 8.1 или более поздней версии;
* Выполнение заданий на странице [Создание приложения Windows][Создание приложения Windows].
* [Хранилище SQLite для мобильных служб Azure][sqlite store nuget]
* [SQLite для разработки универсальной платформы Windows](http://www.sqlite.org/downloads)

## <a name="update-hello-client-app-toosupport-offline-features"></a>Обновление автономных функции приложения клиента toosupport hello
Автономные компоненты мобильного приложения Azure позволяют toointeract с локальной базы данных в автономный режим. toouse инициализировать эти функции в вашем приложении [SyncContext] [ synccontext] tooa локального хранилища. Затем ссылаться на таблицы через hello [IMobileServiceSyncTable][IMobileServiceSyncTable] интерфейса. SQLite используется как hello локальное хранилище на устройстве hello.

1. Установка hello [SQLite среды выполнения для универсальной платформы Windows hello](http://sqlite.org/2016/sqlite-uwp-3120200.vsix).
2. В Visual Studio откройте hello диспетчер пакетов NuGet для проекта приложения UWP hello, выполненной в hello [создать приложение Windows] учебника.
    Поиск и установка hello **Microsoft.Azure.Mobile.Client.SQLiteStore** пакет NuGet.
3. В обозревателе решений щелкните правой кнопкой мыши **Ссылки** > **Добавить ссылку...** > **Универсальная платформа Windows** > **Расширения**, а затем включите **SQLite для универсальной платформы Windows** и **среду выполнения Visual C++ 2015 для приложений универсальной платформы Windows**.

    ![Добавить ссылку на SQLite UWP][1]
4. Откройте файл MainPage.xaml.cs hello и раскомментируйте hello `#define OFFLINE_SYNC_ENABLED` определения.
5. В Visual Studio нажмите клавишу hello **F5** ключевые toorebuild и выполнения hello клиентского приложения. приложение Hello работает так же, как было до включения автономной синхронизации hello. Тем не менее hello локальной базы данных теперь заполняется данными, можно использовать в автономный режим.

## <a name="update-sync"></a>Обновить toodisconnect приложения hello из внутреннего hello
В этом разделе можно разделить hello подключения tooyour мобильное приложение серверной toosimulate ситуации вне сети. При добавлении элементов данных, то обработчик исключений о том, что приложение hello находится в автономном режиме. В этом состоянии новые элементы, добавленные в hello локального хранения и будут синхронизированы с hello внутреннего сервера мобильного приложения, при принудительной следующий запуск в подключенном состоянии.

1. Измените App.xaml.cs в общем проекте hello. Закомментируйте hello инициализации hello **MobileServiceClient** и добавьте следующие строки, которое используется URL-адрес недопустимый мобильное приложение hello:

         public static MobileServiceClient MobileService = new MobileServiceClient("https://your-service.azurewebsites.fail");

    Можно также продемонстрировать поведение вне сети, отключив Wi-Fi и сотовой сети на устройстве hello или использовать режим "в самолете".
2. Нажмите клавишу **F5** toobuild и запустите приложение hello. Обратите внимание, синхронизации не удалось выполнить обновление Здравствуйте, при запуске приложения.
3. Введите новые элементы. Учтите, что при каждом нажатии кнопки **Сохранить** отправка завершается сбоем с состоянием [CancelledByNetworkError]. Тем не менее новые элементы todo hello существует в локальном хранилище hello, пока не могут быть принудительно toohello внутреннего сервера мобильного приложения.  В рабочей среде приложения, при отключении этих исключений, которые клиентское приложение hello ведет себя как если бы она по-прежнему подключен toohello внутреннего сервера мобильного приложения.
4. Закройте приложение hello и перезапустите его tooverify, hello новые элементы, созданные сохраненного toohello локального хранилища.
5. В Visual Studio в откройте **обозреватель сервера**. Перейдите tooyour базы данных в **Azure**->**баз данных SQL**. Щелкните правой кнопкой мыши базу данных и выберите пункт **Открыть в обозревателе объектов SQL Server**. Теперь можно просмотреть tooyour таблицы базы данных SQL и ее содержимое. Убедитесь, что не изменилось hello данные в базе данных серверной части hello.
6. (Необязательно) С помощью средства REST, например Fiddler или почтальон tooquery вашей мобильной серверной части, используя запрос GET в форме `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Обновить tooreconnect приложения hello внутренний сервер приложений для мобильных устройств
В этом разделе Чтобы заново подключить внутреннего сервера мобильного приложения toohello приложения hello. Эти изменения имитировать повторное подключение сети на приложение hello.

При первом запуске приложения hello, hello `OnNavigatedTo` вызовов обработчика событий `InitLocalStoreAsync`. Этот метод в свою очередь вызывает `SyncAsync` toosync локального хранения с hello серверной базе данных. приложение Hello попыток toosync во время запуска.

1. Откройте App.xaml.cs в общем проекте hello и раскомментируйте предыдущая инициализация `MobileServiceClient` URL-адрес мобильного приложения hello правильный toouse hello.
2. Нажмите клавишу hello **F5** ключевые toorebuild и приложение hello выполнения. Hello приложение выполнит синхронизацию локальных изменений с серверной hello мобильного приложения Azure, с помощью принудительной отправки и запросов операций при hello `OnNavigatedTo` выполняется обработчик события.
3. (Необязательно) Представление hello обновленных данных, с помощью обозревателя объектов SQL Server или средством REST, например Fiddler. Обратите внимание hello данные синхронизированы между hello мобильного приложения Azure серверной базой данных и hello локального хранилища.
4. В приложение hello, нажмите кнопку Проверить hello поле рядом с несколько элементов toocomplete их в локальном хранилище hello.

   `UpdateCheckedTodoItem`вызовы `SyncAsync` элемент toosync каждого завершена с внутреннего сервера мобильного приложения hello. `SyncAsync` вызывает операцию отправки и извлечения данных. Тем не менее **при каждом выполнении запросу к таблице hello клиента были внесены изменения, push всегда выполняется автоматически**. Это поведение гарантирует, что все таблицы в локальном хранилище hello вместе со связями остаются согласованными. Такое поведение может привести к непредвиденной отправке данных.  Дополнительные сведения об этом поведении см. в статье [автономной синхронизации данных в мобильных приложениях Azure].

## <a name="api-summary"></a>Сводные данные API
toosupport hello автономным функциям мобильных служб, мы использовали hello [IMobileServiceSyncTable] интерфейс и инициализируется [MobileServiceClient.SyncContext] [ synccontext] с помощью локальной базы данных SQLite. При автономном режиме, hello обычных операций CRUD по мобильным приложениям работать как приложение hello подключен, пока выполняются операции hello относительно hello локального хранилища. Hello следующие методы, используемые toosynchronize hello локальное хранилище с сервером hello:

* **[PushAsync]**  , так как этот метод является членом [IMobileServicesSyncContext], изменения по всем таблицам помещаются в стек toohello серверной части. Только те записи, локальные изменения отправляются toohello сервера.
* **[PullAsync]**. Извлечение запускается из объекта [IMobileServiceSyncTable]. При наличии отслеживаемых изменений в таблице hello, неявное принудительной выполняется toomake останутся согласованность всех таблиц в локальном хранилище hello вместе со связями. Hello *pushOtherTables* управляет другой таблицы в контексте hello помещаются в неявных push. Hello *запроса* принимает [IMobileServiceTableQuery<T> ] [ IMobileServiceTableQuery] или hello toofilter строка запроса OData возвращаемых данных. Hello *queryId* используется параметр toodefine добавочной синхронизации. Дополнительные сведения см. в разделе [Как работает автономная синхронизация](app-service-mobile-offline-data-sync.md#how-sync-works).
* **[PurgeAsync]**  приложения должен периодически вызывать этот метод toopurge устаревшие данные из локального хранилища hello. Используйте hello *принудительно* параметр при необходимости toopurge любые изменения, которые не были синхронизированы.

Дополнительные сведения об этих понятиях см. в разделе [Как работает автономная синхронизация](app-service-mobile-offline-data-sync.md#how-sync-works).

## <a name="more-info"></a>Подробнее
Hello следующих разделах подробную информацию на функции hello автономной синхронизации мобильных приложений.

* [автономной синхронизации данных в мобильных приложениях Azure]
* [Использование пакета SDK .NET для мобильных приложений Azure][8]

<!-- Anchors. -->
[Update hello app toosupport offline features]: #enable-offline-app
[Update hello sync behavior of hello app]: #update-sync
[Update hello app tooreconnect your Mobile Apps backend]: #update-online-app
[Next Steps]:#next-steps

<!-- Images -->
[1]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-reference-sqlite-dialog.png
[11]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-wp81-reference-sqlite-dialog.png
[13]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/cpu-architecture.png


<!-- URLs. -->
[автономной синхронизации данных в мобильных приложениях Azure]: app-service-mobile-offline-data-sync.md
[Создание приложения Windows]: app-service-mobile-windows-store-dotnet-get-started.md
[SQLite for Windows 8.1]: http://go.microsoft.com/fwlink/?LinkID=716919
[SQLite for Windows Phone 8.1]: http://go.microsoft.com/fwlink/?LinkID=716920
[SQLite for Windows 10]: http://go.microsoft.com/fwlink/?LinkID=716921
[synccontext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[sqlite store nuget]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client.SQLiteStore/
[IMobileServiceSyncTable]: https://msdn.microsoft.com/library/azure/mt691742(v=azure.10).aspx
[IMobileServiceTableQuery]: https://msdn.microsoft.com/library/azure/dn250631(v=azure.10).aspx
[IMobileServicesSyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynccontext(v=azure.10).aspx
[MobileServicePushFailedException]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushfailedexception(v=azure.10).aspx
[Status]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushcompletionresult.status(v=azure.10).aspx
[CancelledByNetworkError]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushstatus(v=azure.10).aspx
[PullAsync]: https://msdn.microsoft.com/library/azure/mt667558(v=azure.10).aspx
[PushAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileservicesynccontextextensions.pushasync(v=azure.10).aspx
[PurgeAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynctable.purgeasync(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
