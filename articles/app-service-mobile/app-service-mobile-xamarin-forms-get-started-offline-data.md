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
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="64e68-103">Включение автономной синхронизации мобильного приложения Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="64e68-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="64e68-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="64e68-104">Overview</span></span>
<span data-ttu-id="64e68-105">В этом учебнике рассказывается функции hello автономной синхронизации мобильных приложений Azure для Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="64e68-105">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="64e68-106">Автономная синхронизация позволяет конечным пользователям взаимодействовать с мобильным приложением — просматривать, добавлять или изменять данные — даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="64e68-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="64e68-107">Изменения сохраняются в локальной базе данных.</span><span class="sxs-lookup"><span data-stu-id="64e68-107">Changes are stored in a local database.</span></span> <span data-ttu-id="64e68-108">Как только устройство hello вернется в оперативный режим, эти изменения синхронизируются с hello удаленной службы.</span><span class="sxs-lookup"><span data-stu-id="64e68-108">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="64e68-109">Этот учебник основывается на hello решения Xamarin.Forms краткое руководство для мобильных приложений, созданный после завершения этого учебника [создание приложения Xamarin iOS].</span><span class="sxs-lookup"><span data-stu-id="64e68-109">This tutorial is based on hello Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="64e68-110">решение краткое руководство Hello для Xamarin.Forms содержит hello кода toosupport автономной синхронизации, которой требуется только toobe включена.</span><span class="sxs-lookup"><span data-stu-id="64e68-110">hello quickstart solution for Xamarin.Forms contains hello code toosupport offline sync, which just needs toobe enabled.</span></span> <span data-ttu-id="64e68-111">В этом учебнике обновить tooturn решения hello краткое руководство о hello автономных компонентах мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="64e68-111">In this tutorial, you update hello quickstart solution tooturn on hello offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="64e68-112">Мы также выделяет hello автономного код в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="64e68-112">We also highlight hello offline-specific code in hello app.</span></span> <span data-ttu-id="64e68-113">Если решение краткое руководство загружаются hello не используется, необходимо добавить проект tooyour пакеты расширения доступа hello данных.</span><span class="sxs-lookup"><span data-stu-id="64e68-113">If you do not use hello downloaded quickstart solution, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="64e68-114">Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure][1].</span><span class="sxs-lookup"><span data-stu-id="64e68-114">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="64e68-115">toolearn Дополнительные сведения о функции hello автономной синхронизации, см. разделе hello [автономной синхронизации данных в мобильных приложениях Azure][2].</span><span class="sxs-lookup"><span data-stu-id="64e68-115">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a><span data-ttu-id="64e68-116">Включить функции автономной синхронизации в решении hello краткое руководство</span><span class="sxs-lookup"><span data-stu-id="64e68-116">Enable offline sync functionality in hello quickstart solution</span></span>
<span data-ttu-id="64e68-117">Код автономной синхронизации Hello включен в проект hello с помощью директивы препроцессора C#.</span><span class="sxs-lookup"><span data-stu-id="64e68-117">hello offline sync code is included in hello project by using C# preprocessor directives.</span></span> <span data-ttu-id="64e68-118">Здравствуйте, когда **OFFLINE\_СИНХРОНИЗАЦИИ\_включено** символ определен, эти пути кода, включаются в сборку hello.</span><span class="sxs-lookup"><span data-stu-id="64e68-118">When hello **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in hello build.</span></span> <span data-ttu-id="64e68-119">Для приложений Windows также необходимо установить платформу SQLite hello.</span><span class="sxs-lookup"><span data-stu-id="64e68-119">For Windows apps, you must also install hello SQLite platform.</span></span>

1. <span data-ttu-id="64e68-120">В Visual Studio щелкните правой кнопкой мыши решение hello > **управление пакетами NuGet для решения...** , выполните поиск и установка **Microsoft.Azure.Mobile.Client.SQLiteStore** пакет NuGet для всех проектов в решении hello.</span><span class="sxs-lookup"><span data-stu-id="64e68-120">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="64e68-121">В hello обозревателе решений откройте файл TodoItemManager.cs hello из проекта hello с **переносимой** в hello имя, являющееся проекта переносимой библиотеки классов, затем снимите комментарий hello, следующий за директивой препроцессора:</span><span class="sxs-lookup"><span data-stu-id="64e68-121">In hello Solution Explorer, open hello TodoItemManager.cs file from hello project with **Portable** in hello name, which is Portable Class Library project, then uncomment hello following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="64e68-122">(Необязательно) toosupport устройства Windows, установите одно из следующих пакетов среды выполнения SQLite hello.</span><span class="sxs-lookup"><span data-stu-id="64e68-122">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="64e68-123">**Среда выполнения Windows 8.1**: установите [SQLite для Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="64e68-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="64e68-124">**Windows Phone 8.1**: установите [SQLite для Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="64e68-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="64e68-125">**Универсальная платформа Windows** установить [SQLite для универсальной универсальное приложение для Windows hello][5].</span><span class="sxs-lookup"><span data-stu-id="64e68-125">**Universal Windows Platform** Install [SQLite for hello Universal Windows Universal][5].</span></span>

     <span data-ttu-id="64e68-126">Несмотря на то, что hello краткое руководство не содержит проект универсального приложения Windows, Xamarin Forms поддерживается hello универсальной платформы Windows.</span><span class="sxs-lookup"><span data-stu-id="64e68-126">Although hello quickstart does not contain a Universal Windows project, hello Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="64e68-127">(Необязательно) В каждом проекте приложения Windows, щелкните правой кнопкой мыши **ссылки** > **добавить ссылку...** , разверните hello **Windows** папки > **расширения**.</span><span class="sxs-lookup"><span data-stu-id="64e68-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="64e68-128">Включить соответствующие hello **SQLite для Windows** пакета SDK, а также hello **Visual C++ 2013 среды выполнения для Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="64e68-128">Enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="64e68-129">Hello SQLite SDK имена будут немного отличаться с каждой платформы Windows.</span><span class="sxs-lookup"><span data-stu-id="64e68-129">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-hello-client-sync-code"></a><span data-ttu-id="64e68-130">Просмотрите код синхронизации приветствия клиента</span><span class="sxs-lookup"><span data-stu-id="64e68-130">Review hello client sync code</span></span>
<span data-ttu-id="64e68-131">Ниже приведен краткий обзор уже содержание hello учебника код внутри hello `#if OFFLINE_SYNC_ENABLED` директивы.</span><span class="sxs-lookup"><span data-stu-id="64e68-131">Here is a brief overview of what is already included in hello tutorial code inside hello `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="64e68-132">Функциональность автономной синхронизации — в файле проекта TodoItemManager.cs hello в hello проекта переносимой библиотеки классов.</span><span class="sxs-lookup"><span data-stu-id="64e68-132">The offline sync functionality is in hello TodoItemManager.cs project file in hello Portable Class Library project.</span></span> <span data-ttu-id="64e68-133">Концептуальный обзор функции hello. в разделе [автономной синхронизации данных в мобильных приложениях Azure][2].</span><span class="sxs-lookup"><span data-stu-id="64e68-133">For a conceptual overview of hello feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="64e68-134">Перед выполнением любых операций таблицы hello локального хранилища должен быть инициализирован.</span><span class="sxs-lookup"><span data-stu-id="64e68-134">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="64e68-135">Hello локального хранилища базы данных инициализируется в hello **TodoItemManager** конструктор класса с помощью hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="64e68-135">hello local store database is initialized in hello **TodoItemManager** class constructor by using hello following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="64e68-136">Этот код создает новый локальный SQLite базу данных с помощью hello **MobileServiceSQLiteStore** класса.</span><span class="sxs-lookup"><span data-stu-id="64e68-136">This code creates a new local SQLite database using hello **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="64e68-137">Hello **DefineTable** метод создает таблицу в hello локального хранилища, соответствующий hello поля типа указано hello.</span><span class="sxs-lookup"><span data-stu-id="64e68-137">hello **DefineTable** method creates a table in hello local store that matches hello fields in hello provided type.</span></span>  <span data-ttu-id="64e68-138">Тип Hello не имеет tooinclude все столбцы hello hello удаленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="64e68-138">hello type doesn't have tooinclude all hello columns that are in hello remote database.</span></span> <span data-ttu-id="64e68-139">Это возможно toostore подмножество столбцов.</span><span class="sxs-lookup"><span data-stu-id="64e68-139">It is possible toostore a subset of columns.</span></span>
* <span data-ttu-id="64e68-140">Hello **todoTable** в **TodoItemManager** — **IMobileServiceSyncTable** введите вместо **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="64e68-140">hello **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="64e68-141">Этот класс использует hello локальной базы данных для всех создания, чтения, обновления и удаления (CRUD) табличные операции.</span><span class="sxs-lookup"><span data-stu-id="64e68-141">This class uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="64e68-142">Решите, когда эти изменения передаются внутреннего сервера мобильного приложения toohello путем вызова **PushAsync** на hello **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="64e68-142">You decide when those changes are pushed toohello Mobile App backend by calling **PushAsync** on hello **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="64e68-143">Hello контекста синхронизации помогает сохранить связи между таблицами, отслеживания и опубликуйте изменения во всех таблицах в клиентском приложении был изменен при **PushAsync** вызывается.</span><span class="sxs-lookup"><span data-stu-id="64e68-143">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="64e68-144">следующие Hello **SyncAsync** toosync с внутреннего сервера мобильного приложения hello вызывается метод:</span><span class="sxs-lookup"><span data-stu-id="64e68-144">hello following **SyncAsync** method is called toosync with hello Mobile App backend:</span></span>

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

    <span data-ttu-id="64e68-145">В этом примере используется простой обработки ошибок с помощью обработчика синхронизации по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="64e68-145">This sample uses simple error handling with hello default sync handler.</span></span> <span data-ttu-id="64e68-146">Реальном приложении будет обрабатываться hello различные ошибки, например состояния сети и сервера конфликтует с помощью пользовательского **IMobileServiceSyncHandler** реализации.</span><span class="sxs-lookup"><span data-stu-id="64e68-146">A real application would handle hello various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="64e68-147">Рекомендации по автономной синхронизации</span><span class="sxs-lookup"><span data-stu-id="64e68-147">Offline sync considerations</span></span>
<span data-ttu-id="64e68-148">В образце hello hello **SyncAsync** метод вызывается только при запуске и при запросе синхронизации.</span><span class="sxs-lookup"><span data-stu-id="64e68-148">In hello sample, hello **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="64e68-149">tooinitiate синхронизации в приложении Android или iOS, запросу вниз в списке элементов hello; для Windows, используйте hello **синхронизации** кнопки.</span><span class="sxs-lookup"><span data-stu-id="64e68-149">tooinitiate a sync in an Android or iOS app, pull down on hello items list; for Windows, use hello **Sync** button.</span></span> <span data-ttu-id="64e68-150">В реальном приложении также может разместить hello триггер синхронизации, при изменении состояния сети hello.</span><span class="sxs-lookup"><span data-stu-id="64e68-150">In a real-world application, you could also make hello sync trigger when hello network state changes.</span></span>

<span data-ttu-id="64e68-151">При выполнении запросу к таблице, имеющей ожидающие локального обновления отслеживаются контекстом hello, извлечь операции автоматически триггеры предыдущей принудительной контекста.</span><span class="sxs-lookup"><span data-stu-id="64e68-151">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="64e68-152">При обновлении, добавление и завершение работы элементов в этом примере, можно опустить hello явные **PushAsync** вызова.</span><span class="sxs-lookup"><span data-stu-id="64e68-152">When refreshing, adding, and completing items in this sample, you can omit hello explicit **PushAsync** call.</span></span>

<span data-ttu-id="64e68-153">В коде указано hello запрашиваются все записи в удаленной таблице TodoItem hello, но это также возможно toofilter записей, передавая идентификатор запроса и запрос слишком**PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="64e68-153">In hello provided code, all records in hello remote TodoItem table are queried, but it is also possible toofilter records by passing a query id and query too**PushAsync**.</span></span> <span data-ttu-id="64e68-154">Дополнительные сведения см в разделе hello *добавочной синхронизации* в [автономной синхронизации данных в мобильных приложениях Azure][2].</span><span class="sxs-lookup"><span data-stu-id="64e68-154">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="64e68-155">Запустить клиентское приложение hello</span><span class="sxs-lookup"><span data-stu-id="64e68-155">Run hello client app</span></span>
<span data-ttu-id="64e68-156">С автономной синхронизации теперь включена запустите клиентское приложение hello по крайней мере один раз в каждой базе данных локального хранилища платформы toopopulate hello.</span><span class="sxs-lookup"><span data-stu-id="64e68-156">With offline sync now enabled, run hello client application at least once on each platform toopopulate hello local store database.</span></span> <span data-ttu-id="64e68-157">Позже имитировать автономный режим и изменить hello данные в локальном хранилище hello, когда приложение hello отключен от сети.</span><span class="sxs-lookup"><span data-stu-id="64e68-157">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="update-hello-sync-behavior-of-hello-client-app"></a><span data-ttu-id="64e68-158">Обновить hello синхронизации поведение клиентского приложения hello</span><span class="sxs-lookup"><span data-stu-id="64e68-158">Update hello sync behavior of hello client app</span></span>
<span data-ttu-id="64e68-159">В этом разделе измените toosimulate проекта клиента hello в случае автономной работы с помощью URL-адрес приложения, недопустимый для серверной части.</span><span class="sxs-lookup"><span data-stu-id="64e68-159">In this section, modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="64e68-160">Кроме того, можно отключить сетевых подключений, перемещая устройства слишком «"Режим" в самолете».</span><span class="sxs-lookup"><span data-stu-id="64e68-160">Alternatively, you can turn off network connections by moving your device too"Airplane mode."</span></span>  <span data-ttu-id="64e68-161">При добавлении или изменении элементов данных, эти изменения, которые содержатся в локальном хранилище hello, но не синхронизированных данных серверной части toohello сохранение, пока hello подключение будет восстановлено.</span><span class="sxs-lookup"><span data-stu-id="64e68-161">When you add or change data items, these changes are held in hello local store, but not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="64e68-162">В hello обозревателе решений откройте файл проекта Constants.cs hello из hello **переносимой** проекта и измените значение hello `ApplicationURL` недопустимый URL-адрес toopoint tooan:</span><span class="sxs-lookup"><span data-stu-id="64e68-162">In hello Solution Explorer, open hello Constants.cs project file from hello **Portable** project and change hello value of `ApplicationURL` toopoint tooan invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="64e68-163">Привет открыть файл TodoItemManager.cs из hello **переносимой** проекта, а затем добавьте **перехватывать** для hello базовый **исключение** toohello класса **try... catch** блока в **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="64e68-163">Open hello TodoItemManager.cs file from hello **Portable** project, then add a **catch** for hello base **Exception** class toohello **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="64e68-164">Это **перехватывать** блок записывает консоли toohello сообщение hello исключения, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="64e68-164">This **catch** block writes hello exception message toohello console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="64e68-165">Постройте и запустите клиентское приложение hello.</span><span class="sxs-lookup"><span data-stu-id="64e68-165">Build and run hello client app.</span></span>  <span data-ttu-id="64e68-166">Добавьте несколько новых элементов.</span><span class="sxs-lookup"><span data-stu-id="64e68-166">Add some new items.</span></span> <span data-ttu-id="64e68-167">Обратите внимание, в консоли hello для каждой попытки toosync с серверной hello регистрируется исключение.</span><span class="sxs-lookup"><span data-stu-id="64e68-167">Notice that an exception is logged in hello console for each attempt toosync with hello backend.</span></span> <span data-ttu-id="64e68-168">Эти новые элементы существуют только в локальном хранилище hello, пока их можно отправить toohello мобильной серверной части.</span><span class="sxs-lookup"><span data-stu-id="64e68-168">These new items exist only in hello local store until they can be pushed toohello mobile backend.</span></span> <span data-ttu-id="64e68-169">клиентское приложение Hello, ведет себя как toohello подключенной базы данных, поддерживающий все создавать, читать, update, операции удаления (CRUD).</span><span class="sxs-lookup"><span data-stu-id="64e68-169">hello client app behaves as if it is connected toohello backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="64e68-170">Закройте приложение hello и перезапустите его tooverify, hello новые элементы, созданные сохраненного toohello локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="64e68-170">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>
5. <span data-ttu-id="64e68-171">(Необязательно) С помощью Visual Studio tooview вашей toosee таблицы базы данных SQL Azure, hello данные в базе данных серверной части hello не изменились.</span><span class="sxs-lookup"><span data-stu-id="64e68-171">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="64e68-172">В Visual Studio в откройте **обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="64e68-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="64e68-173">Перейдите tooyour базы данных в **Azure**->**баз данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="64e68-173">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="64e68-174">Щелкните правой кнопкой мыши базу данных и выберите пункт **Открыть в обозревателе объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="64e68-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="64e68-175">Теперь можно просмотреть tooyour таблицы базы данных SQL и ее содержимое.</span><span class="sxs-lookup"><span data-stu-id="64e68-175">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a><span data-ttu-id="64e68-176">Обновление серверной части мобильных tooreconnect приложения hello клиента</span><span class="sxs-lookup"><span data-stu-id="64e68-176">Update hello client app tooreconnect your mobile backend</span></span>
<span data-ttu-id="64e68-177">В этом разделе переподключение hello toohello мобильного внутреннего сервера приложения, которое имитирует приложение hello, приходящие обратно tooan оперативном состоянии.</span><span class="sxs-lookup"><span data-stu-id="64e68-177">In this section, reconnect hello app toohello mobile backend, which simulates hello app coming back tooan online state.</span></span> <span data-ttu-id="64e68-178">При выполнении жестов hello обновления данных — синхронизированных tooyour мобильной серверной части.</span><span class="sxs-lookup"><span data-stu-id="64e68-178">When you perform hello refresh gesture, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="64e68-179">Снова откройте Constants.cs.</span><span class="sxs-lookup"><span data-stu-id="64e68-179">Reopen Constants.cs.</span></span> <span data-ttu-id="64e68-180">Правильный hello `applicationURL` toopoint toohello исправьте URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="64e68-180">Correct hello `applicationURL` toopoint toohello correct URL.</span></span>
2. <span data-ttu-id="64e68-181">Повторное построение и запуск клиентского приложения hello.</span><span class="sxs-lookup"><span data-stu-id="64e68-181">Rebuild and run hello client app.</span></span> <span data-ttu-id="64e68-182">приложение Hello попыток toosync с внутреннего сервера мобильного приложения hello после запуска.</span><span class="sxs-lookup"><span data-stu-id="64e68-182">hello app attempts toosync with hello mobile app backend after launching.</span></span> <span data-ttu-id="64e68-183">Проверьте регистрацию ни одного исключения в консоли отладки hello.</span><span class="sxs-lookup"><span data-stu-id="64e68-183">Verify that no exceptions are logged in hello debug console.</span></span>
3. <span data-ttu-id="64e68-184">(Необязательно) Представление hello обновленные данные, с помощью обозревателя объектов SQL Server или средств REST, как Fiddler или [почтальон][6].</span><span class="sxs-lookup"><span data-stu-id="64e68-184">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="64e68-185">Обратите внимание hello данные синхронизированы между hello серверной базой данных и hello локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="64e68-185">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="64e68-186">Обратите внимание, данные hello синхронизации между базой данных hello и локальное хранилище hello и содержит элементы hello, добавленного в автономном приложении.</span><span class="sxs-lookup"><span data-stu-id="64e68-186">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64e68-187">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="64e68-187">Additional Resources</span></span>
* <span data-ttu-id="64e68-188">[Синхронизация автономных данных в мобильных приложениях Azure][2]</span><span class="sxs-lookup"><span data-stu-id="64e68-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="64e68-189">[Использование пакета SDK .NET для мобильных приложений Azure][8]</span><span class="sxs-lookup"><span data-stu-id="64e68-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
