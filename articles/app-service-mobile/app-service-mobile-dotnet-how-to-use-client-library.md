---
title: "Клиентская библиотека управляемых aaaWorking с hello мобильные приложения службы приложений (Windows | Документы Microsoft"
description: "Узнайте, как toouse клиент .NET для приложений мобильных служб Azure приложения с приложениями Windows и Xamarin."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="36310-103">Управление toouse hello клиента для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="36310-103">How toouse hello managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="36310-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="36310-104">Overview</span></span>
<span data-ttu-id="36310-105">В этом руководстве показано, как tooperform распространенные сценарии, с помощью hello управление клиентскую библиотеку для приложений Azure приложение службы мобильных приложений для Windows и Xamarin.</span><span class="sxs-lookup"><span data-stu-id="36310-105">This guide shows you how tooperform common scenarios using hello managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="36310-106">При наличии новых приложений tooMobile следует первый завершение hello [примеры использования мобильных приложений Azure] [ 1] учебника.</span><span class="sxs-lookup"><span data-stu-id="36310-106">If you are new tooMobile Apps, you should consider first completing hello [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="36310-107">В этом руководстве рассматривается hello клиентского управляемого пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="36310-107">In this guide, we focus on hello client-side managed SDK.</span></span> <span data-ttu-id="36310-108">toolearn Подробнее о hello серверные пакеты SDK для мобильных приложений см. в разделе документации hello hello [.NET SDK сервера] [ 2] или [пакета SDK для Node.js Server] [ 3].</span><span class="sxs-lookup"><span data-stu-id="36310-108">toolearn more about hello server-side SDKs for Mobile Apps, see hello documentation for hello [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="36310-109">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="36310-109">Reference documentation</span></span>
<span data-ttu-id="36310-110">Hello справочная документация для клиента hello SDK находится здесь: [Справочник по клиентским Azure мобильных приложений .NET][4].</span><span class="sxs-lookup"><span data-stu-id="36310-110">hello reference documentation for hello client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="36310-111">Несколько примеров клиента можно также найти в hello [репозитории GitHub примеров Azure][5].</span><span class="sxs-lookup"><span data-stu-id="36310-111">You can also find several client samples in hello [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="36310-112">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="36310-112">Supported Platforms</span></span>
<span data-ttu-id="36310-113">Hello платформой .NET поддерживает hello следующих платформ:</span><span class="sxs-lookup"><span data-stu-id="36310-113">hello .NET Platform supports hello following platforms:</span></span>

* <span data-ttu-id="36310-114">выпуски Xamarin Android для API 19–24 (от KitKat до Nougat);</span><span class="sxs-lookup"><span data-stu-id="36310-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="36310-115">выпуски Xamarin iOS для iOS 8.0 и более поздних версий;</span><span class="sxs-lookup"><span data-stu-id="36310-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="36310-116">Универсальные приложения Windows</span><span class="sxs-lookup"><span data-stu-id="36310-116">Universal Windows Platform</span></span>
* <span data-ttu-id="36310-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="36310-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="36310-118">Windows Phone 8.0, за исключением приложений Silverlight.</span><span class="sxs-lookup"><span data-stu-id="36310-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="36310-119">Проверка подлинности «сервер потока» Hello использует WebView для hello, представленных пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="36310-119">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="36310-120">Если устройство hello не может toopresent WebView пользовательского интерфейса, другие методы проверки подлинности требуется.</span><span class="sxs-lookup"><span data-stu-id="36310-120">If hello device is not able toopresent a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="36310-121">Поэтому данный пакет SDK не подходит для различного рода часов и других устройств с аналогичными ограничениями.</span><span class="sxs-lookup"><span data-stu-id="36310-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="36310-122"><a name="setup"></a>Настройка и необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="36310-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="36310-123">Предполагается, что вы уже создали и опубликовали проект внутреннего сервера мобильных приложений, который содержит по меньшей мере одну таблицу.</span><span class="sxs-lookup"><span data-stu-id="36310-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="36310-124">Hello код, используемый в этом разделе, с именем таблицы hello `TodoItem` и имеет hello следующие столбцы: `Id`, `Text`, и `Complete`.</span><span class="sxs-lookup"><span data-stu-id="36310-124">In hello code used in this topic, hello table is named `TodoItem` and it has hello following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="36310-125">Эта таблица является hello в одной таблице, созданной при ознакомлении [примеры использования мобильных приложений Azure][1].</span><span class="sxs-lookup"><span data-stu-id="36310-125">This table is hello same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="36310-126">Hello соответствующий типизированный клиентский тип в C# — hello, следуя класса:</span><span class="sxs-lookup"><span data-stu-id="36310-126">hello corresponding typed client-side type in C# is hello following class:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

<span data-ttu-id="36310-127">Hello [JsonPropertyAttribute] [ 6] — hello используется toodefine *PropertyName* сопоставление между полями клиента hello и hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="36310-127">hello [JsonPropertyAttribute][6] is used toodefine hello *PropertyName* mapping between hello client field and hello table field.</span></span>

<span data-ttu-id="36310-128">toolearn как toocreate таблицы в серверной части мобильных приложений, в разделе hello [разделе .NET SDK сервера] [ 7] или hello [пакета SDK для Node.js Server разделе] [ 8] .</span><span class="sxs-lookup"><span data-stu-id="36310-128">toolearn how toocreate tables in your Mobile Apps backend, see hello [.NET Server SDK topic][7] or hello [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="36310-129">При создании серверной части мобильное приложение hello Azure с помощью портала hello краткое руководство, можно также использовать hello **простой таблицы** в hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="36310-129">If you created your Mobile App backend in hello Azure portal using hello QuickStart, you can also use hello **Easy tables** setting in hello [Azure portal].</span></span>

### <a name="how-to-install-hello-managed-client-sdk-package"></a><span data-ttu-id="36310-130">Как: hello установки управляемого пакета SDK для клиента</span><span class="sxs-lookup"><span data-stu-id="36310-130">How to: Install hello managed client SDK package</span></span>
<span data-ttu-id="36310-131">Используйте один из следующих методов tooinstall hello hello управляемого пакета SDK для клиента для мобильных приложений от [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="36310-131">Use one of hello following methods tooinstall hello managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="36310-132">**Visual Studio** правой кнопкой мыши проект, нажмите кнопку **управление пакетами NuGet**, поиск hello `Microsoft.Azure.Mobile.Client` пакета, а затем нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="36310-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="36310-133">**Xamarin Studio** правой кнопкой мыши проект, нажмите кнопку **добавить** > **Добавление пакетов NuGet**, поиск hello `Microsoft.Azure.Mobile.Client `пакета, а затем нажмите кнопку **добавить Пакет**.</span><span class="sxs-lookup"><span data-stu-id="36310-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="36310-134">В файле основного действия помните следующее hello tooadd **с помощью** инструкции:</span><span class="sxs-lookup"><span data-stu-id="36310-134">In your main activity file, remember tooadd hello following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="36310-135"><a name="symbolsource"></a>Практическое руководство. Работа с отладочными символами в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="36310-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="36310-136">Hello символы для имен Microsoft.Azure.Mobile hello доступны на [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="36310-136">hello symbols for hello Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="36310-137">См. toothe [инструкции SymbolSource] [ 11] toointegrate SymbolSource вместе с Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="36310-137">Refer toothe [SymbolSource instructions][11] toointegrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="36310-138"><a name="create-client"></a>Создание клиента мобильные приложения hello</span><span class="sxs-lookup"><span data-stu-id="36310-138"><a name="create-client"></a>Create hello Mobile Apps client</span></span>
<span data-ttu-id="36310-139">Hello следующий код создает hello [MobileServiceClient] [ 12] объект, являющийся tooaccess используется внутренний сервер приложений для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="36310-139">hello following code creates hello [MobileServiceClient][12] object that is used tooaccess your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="36310-140">В предыдущих кода hello, замените `MOBILE_APP_URL` hello URL-адрес внутреннего сервера мобильного приложения hello, которая находится в серверной части мобильного приложения в hello в колонке [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="36310-140">In hello preceding code, replace `MOBILE_APP_URL` with hello URL of hello Mobile App backend, which is found in the blade for your Mobile App backend in hello [Azure portal].</span></span> <span data-ttu-id="36310-141">Объект MobileServiceClient Hello должен быть Singleton-классом.</span><span class="sxs-lookup"><span data-stu-id="36310-141">hello MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="36310-142">Работа с таблицами</span><span class="sxs-lookup"><span data-stu-id="36310-142">Work with Tables</span></span>
<span data-ttu-id="36310-143">Здравствуйте, приведенные ниже сведения раздела как toosearch и получить записи и изменение данных hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="36310-143">hello following section details how toosearch and retrieve records and modify hello data within hello table.</span></span>  <span data-ttu-id="36310-144">рассматриваются следующие вопросы Hello.</span><span class="sxs-lookup"><span data-stu-id="36310-144">hello following topics are covered:</span></span>

* [<span data-ttu-id="36310-145">Создание ссылки на таблицу</span><span class="sxs-lookup"><span data-stu-id="36310-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="36310-146">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="36310-146">Query data</span></span>](#querying)
* [<span data-ttu-id="36310-147">Фильтрация возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="36310-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="36310-148">Сортировка возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="36310-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="36310-149">Возврат данных на страницах</span><span class="sxs-lookup"><span data-stu-id="36310-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="36310-150">Выбор определенных столбцов</span><span class="sxs-lookup"><span data-stu-id="36310-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="36310-151">Поиск записи по идентификатору</span><span class="sxs-lookup"><span data-stu-id="36310-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="36310-152">Работа с нетипизированными запросами</span><span class="sxs-lookup"><span data-stu-id="36310-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="36310-153">Вставка данных</span><span class="sxs-lookup"><span data-stu-id="36310-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="36310-154">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="36310-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="36310-155">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="36310-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="36310-156">Разрешение конфликтов и оптимистичный параллелизм</span><span class="sxs-lookup"><span data-stu-id="36310-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="36310-157">Привязка tooa пользовательский интерфейс Windows</span><span class="sxs-lookup"><span data-stu-id="36310-157">Binding tooa Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="36310-158">Изменение размера страницы приветствия</span><span class="sxs-lookup"><span data-stu-id="36310-158">Changing hello Page Size</span></span>](#pagesize)

### <span data-ttu-id="36310-159"><a name="instantiating"></a>Практическое руководство. Создание ссылки на таблицу</span><span class="sxs-lookup"><span data-stu-id="36310-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="36310-160">Все фрагменты кода hello, доступ к данным или изменяет данные в таблице базы данных вызывает функции hello `MobileServiceTable` объекта.</span><span class="sxs-lookup"><span data-stu-id="36310-160">All hello code that accesses or modifies data in a backend table calls functions on hello `MobileServiceTable` object.</span></span> <span data-ttu-id="36310-161">Получить toohello ссылочной таблице, вызывающему Привет [Функция GetTable] метод следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36310-161">Obtain a reference toohello table by calling hello [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="36310-162">Hello вернул объект использует модель сериализации типизированных hello.</span><span class="sxs-lookup"><span data-stu-id="36310-162">hello returned object uses hello typed serialization model.</span></span> <span data-ttu-id="36310-163">Также поддерживается нетипизированная модель сериализации.</span><span class="sxs-lookup"><span data-stu-id="36310-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="36310-164">Следующий пример [создает ссылочной таблице нетипизированного tooan]:</span><span class="sxs-lookup"><span data-stu-id="36310-164">The following example [creates a reference tooan untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="36310-165">В нетипизированный запросов необходимо указывать hello базовой строки запроса OData.</span><span class="sxs-lookup"><span data-stu-id="36310-165">In untyped queries, you must specify hello underlying OData query string.</span></span>

### <span data-ttu-id="36310-166"><a name="querying"></a>Практическое руководство. Запрос данных из мобильного приложения</span><span class="sxs-lookup"><span data-stu-id="36310-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="36310-167">В этом разделе описывается, как tooissue запрашивает внутренней toohello мобильного приложения, включая hello следующие функциональные возможности:</span><span class="sxs-lookup"><span data-stu-id="36310-167">This section describes how tooissue queries toohello Mobile App backend, which includes hello following functionality:</span></span>

* [<span data-ttu-id="36310-168">Фильтрация возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="36310-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="36310-169">Сортировка возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="36310-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="36310-170">Возврат данных на страницах</span><span class="sxs-lookup"><span data-stu-id="36310-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="36310-171">Выбор определенных столбцов</span><span class="sxs-lookup"><span data-stu-id="36310-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="36310-172">Поиск данных по идентификатору</span><span class="sxs-lookup"><span data-stu-id="36310-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="36310-173">Размер страницы управляемого сервера — принудительно tooprevent все строки из возвращаемых.</span><span class="sxs-lookup"><span data-stu-id="36310-173">A server-driven page size is enforced tooprevent all rows from being returned.</span></span>  <span data-ttu-id="36310-174">Разбиение на страницы предотвращает отрицательно влияет на службы hello запросов по умолчанию для больших наборов данных.</span><span class="sxs-lookup"><span data-stu-id="36310-174">Paging keeps default requests for large data sets from negatively impacting hello service.</span></span>  <span data-ttu-id="36310-175">tooreturn более 50 строк используйте hello `Skip` и `Take` метода, как описано в [возвращать данные на страницах](#paging).</span><span class="sxs-lookup"><span data-stu-id="36310-175">tooreturn more than 50 rows, use hello `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="36310-176"><a name="filtering"></a>Практическое руководство. Фильтрация возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="36310-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="36310-177">Hello следующий код показывает, как toofilter данных, включая `Where` предложения в запросе.</span><span class="sxs-lookup"><span data-stu-id="36310-177">hello following code illustrates how toofilter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="36310-178">Возвращает все элементы из `todoTable` которого `Complete` значение свойства равно слишком`false`.</span><span class="sxs-lookup"><span data-stu-id="36310-178">It returns all items from `todoTable` whose `Complete` property is equal too`false`.</span></span> <span data-ttu-id="36310-179">Hello [где] функция применяется предикат для hello запрос к таблице hello фильтрации строк.</span><span class="sxs-lookup"><span data-stu-id="36310-179">hello [Where] function applies a row filtering predicate to hello query against hello table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="36310-180">Hello URI внутреннего toohello запрос, отправленный hello можно просмотреть с помощью программного обеспечения проверки сообщения, например средства разработчика браузера или [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="36310-180">You can view hello URI of hello request sent toohello backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="36310-181">Если взглянуть на URI запроса hello, обратите внимание, строка hello запроса было изменено:</span><span class="sxs-lookup"><span data-stu-id="36310-181">If you look at hello request URI, notice that hello query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="36310-182">Этот запрос OData преобразуется в SQL-запрос по hello Server SDK:</span><span class="sxs-lookup"><span data-stu-id="36310-182">This OData request is translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="36310-183">Здравствуйте, функции, передаваемой toohello `Where` метод может иметь произвольное число условий.</span><span class="sxs-lookup"><span data-stu-id="36310-183">hello function that is passed toohello `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="36310-184">В этом примере это дерево будет преобразовано в SQL-запрос по hello Server SDK:</span><span class="sxs-lookup"><span data-stu-id="36310-184">This example would be translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="36310-185">Этот запрос также можно разбить на несколько предложений:</span><span class="sxs-lookup"><span data-stu-id="36310-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="36310-186">Здравствуйте, два метода являются эквивалентными и могут быть взаимозаменяемыми.</span><span class="sxs-lookup"><span data-stu-id="36310-186">hello two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="36310-187">Здравствуйте первого варианта&mdash;объединения нескольких предикатов в одном запросе&mdash;является более компактным и рекомендуемые.</span><span class="sxs-lookup"><span data-stu-id="36310-187">hello former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="36310-188">Hello `Where` предложение поддерживает операции, которые будет преобразовано в подмножестве OData hello.</span><span class="sxs-lookup"><span data-stu-id="36310-188">hello `Where` clause supports operations that be translated into hello OData subset.</span></span> <span data-ttu-id="36310-189">К этим операциям относятся:</span><span class="sxs-lookup"><span data-stu-id="36310-189">Operations include:</span></span>

* <span data-ttu-id="36310-190">операторы сравнения (==,! =, <, < =, >, > =);</span><span class="sxs-lookup"><span data-stu-id="36310-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="36310-191">арифметические операторы (+, -, /, *, %);</span><span class="sxs-lookup"><span data-stu-id="36310-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="36310-192">указание точности чисел (Math.Floor, Math.Ceiling);</span><span class="sxs-lookup"><span data-stu-id="36310-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="36310-193">строковые функции (Length, Substring, Replace, IndexOf, StartsWith, EndsWith);</span><span class="sxs-lookup"><span data-stu-id="36310-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="36310-194">свойства даты (Year, Month, Day, Hour, Minute, Second);</span><span class="sxs-lookup"><span data-stu-id="36310-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="36310-195">свойства доступа к объекту;</span><span class="sxs-lookup"><span data-stu-id="36310-195">Access properties of an object, and</span></span>
* <span data-ttu-id="36310-196">выражения, сочетающие в себе любые из этих операций.</span><span class="sxs-lookup"><span data-stu-id="36310-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="36310-197">Если поддерживает учитывая то, что hello SDK сервера, можно рассмотреть hello [документации OData v3].</span><span class="sxs-lookup"><span data-stu-id="36310-197">When considering what hello Server SDK supports, you can consider hello [OData v3 Documentation].</span></span>

### <span data-ttu-id="36310-198"><a name="sorting"></a>Практическое руководство. Сортировка возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="36310-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="36310-199">Hello следующий код показывает, как toosort данных, включая [OrderBy] или [OrderByDescending] функции в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="36310-199">hello following code illustrates how toosort data by including an [OrderBy] or [OrderByDescending] function in hello query.</span></span> <span data-ttu-id="36310-200">Возвращает элементы из `todoTable` сортируются по возрастанию по hello `Text` поля.</span><span class="sxs-lookup"><span data-stu-id="36310-200">It returns items from `todoTable` sorted ascending by hello `Text` field.</span></span>

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <span data-ttu-id="36310-201"><a name="paging"></a>Практическое руководство. Возврат данных на страницах</span><span class="sxs-lookup"><span data-stu-id="36310-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="36310-202">По умолчанию hello серверной возвращает hello только первые 50 строк.</span><span class="sxs-lookup"><span data-stu-id="36310-202">By default, hello backend returns only hello first 50 rows.</span></span> <span data-ttu-id="36310-203">Можно увеличить hello число возвращенных строк, вызывающему Привет [принимать] метод.</span><span class="sxs-lookup"><span data-stu-id="36310-203">You can increase hello number of returned rows by calling hello [Take] method.</span></span> <span data-ttu-id="36310-204">Используйте `Take` вместе с hello [пропустить] метод toorequest конкретных «страница» общего набора данных hello возвращаемых запросом hello.</span><span class="sxs-lookup"><span data-stu-id="36310-204">Use `Take` along with hello [Skip] method toorequest a specific "page" of hello total dataset returned by hello query.</span></span> <span data-ttu-id="36310-205">Hello при выполнении следующего запроса возвращает hello три верхних элементов в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="36310-205">hello following query, when executed, returns hello top three items in hello table.</span></span>

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="36310-206">Hello следующий измененный запрос пропускает hello первые три результаты и возвращает hello трех следующих результатов.</span><span class="sxs-lookup"><span data-stu-id="36310-206">hello following revised query skips hello first three results and returns hello next three results.</span></span> <span data-ttu-id="36310-207">Этот запрос получает hello второй «страницы» данных, где размер страницы приветствия трех элементов.</span><span class="sxs-lookup"><span data-stu-id="36310-207">This query produces hello second "page" of data, where hello page size is three items.</span></span>

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="36310-208">Hello [IncludeTotalCount] метод запрашивает hello общее число *все* hello записей, которые были бы возвращены, условии указано любые ограничения или разбиения на страницы:</span><span class="sxs-lookup"><span data-stu-id="36310-208">hello [IncludeTotalCount] method requests hello total count for *all* hello records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="36310-209">В приложении реального мира можно использовать аналогичный toohello запросы предшествующий пример с сопоставимых пользовательского интерфейса или элемент управления страничного навигатора для перехода между страницами.</span><span class="sxs-lookup"><span data-stu-id="36310-209">In a real world app, you can use queries similar toohello preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="36310-210">ограничение 50 строк toooverride hello в серверном приложении мобильного приложения, необходимо также применить hello [EnableQueryAttribute] toohello открытый метод GET и укажите hello разбиение по страницам.</span><span class="sxs-lookup"><span data-stu-id="36310-210">toooverride hello 50-row limit in a Mobile App backend, you must also apply hello [EnableQueryAttribute] toohello public GET method and specify hello paging behavior.</span></span> <span data-ttu-id="36310-211">При toohello применяется метод, hello следующие задает too1000 максимальное число возвращенных строк:</span><span class="sxs-lookup"><span data-stu-id="36310-211">When applied toohello method, hello following sets the maximum returned rows too1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="36310-212"><a name="selecting"></a>Практическое руководство. Выбор определенных столбцов</span><span class="sxs-lookup"><span data-stu-id="36310-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="36310-213">Можно указать набор свойств tooinclude в hello, добавив [выберите] предложение tooyour запроса.</span><span class="sxs-lookup"><span data-stu-id="36310-213">You can specify which set of properties tooinclude in hello results by adding a [Select] clause tooyour query.</span></span> <span data-ttu-id="36310-214">Здравствуйте, например, как следующий код показывает одно поле tooselect и также как tooselect и отформатировать несколько полей:</span><span class="sxs-lookup"><span data-stu-id="36310-214">For example, hello following code shows how tooselect just one field and also how tooselect and format multiple fields:</span></span>

```
// Select one field -- just hello Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

<span data-ttu-id="36310-215">Здравствуйте, все функции, описанные в данный момент являются аддитивными, поэтому мы можно сохранить цепочки их.</span><span class="sxs-lookup"><span data-stu-id="36310-215">All hello functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="36310-216">Каждый вызов цепочек влияет на несколько запросов hello.</span><span class="sxs-lookup"><span data-stu-id="36310-216">Each chained call affects more of hello query.</span></span> <span data-ttu-id="36310-217">Еще один пример:</span><span class="sxs-lookup"><span data-stu-id="36310-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="36310-218"><a name="lookingup"></a>Практическое руководство. Поиск данных по идентификатору</span><span class="sxs-lookup"><span data-stu-id="36310-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="36310-219">Hello [LookupAsync] функция может быть используется toolook объектов из базы данных hello с определенным идентификатором.</span><span class="sxs-lookup"><span data-stu-id="36310-219">hello [LookupAsync] function can be used toolook up objects from hello database with a particular ID.</span></span>

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="36310-220"><a name="untypedqueries"></a>Практическое руководство. Выполнение нетипизированных запросов</span><span class="sxs-lookup"><span data-stu-id="36310-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="36310-221">При выполнении запроса с помощью объекта нетипизированного таблицы, необходимо явно указать строку запроса OData hello путем вызова [ReadAsync], как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="36310-221">When executing a query using an untyped table object, you must explicitly specify hello OData query string by calling [ReadAsync], as in hello following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="36310-222">Вы будете получать значения JSON, которые можно использовать в качестве контейнера свойств.</span><span class="sxs-lookup"><span data-stu-id="36310-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="36310-223">Дополнительные сведения о JToken и Newtonsoft Json.NET см. в разделе hello [Json.NET] сайта.</span><span class="sxs-lookup"><span data-stu-id="36310-223">For more information on JToken and Newtonsoft Json.NET, see hello [Json.NET] site.</span></span>

### <span data-ttu-id="36310-224"><a name="inserting"></a>Практическое руководство. Вставка данных в серверную часть мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="36310-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="36310-225">Все типы клиентов должны содержать член с именем **Id**(идентификатор), который по умолчанию является строкой.</span><span class="sxs-lookup"><span data-stu-id="36310-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="36310-226">Это **идентификатор** требуется для выполнения операций CRUD и hello в автономном режиме синхронизации. следующий код иллюстрирует способ toouse hello [InsertAsync] метод tooinsert новых строк в таблицу.</span><span class="sxs-lookup"><span data-stu-id="36310-226">This **Id** is required to perform CRUD operations and for offline sync. hello following code illustrates how toouse hello [InsertAsync] method tooinsert new rows into a table.</span></span> <span data-ttu-id="36310-227">параметр Hello содержит hello toobe данных, добавляются в виде объекта .NET.</span><span class="sxs-lookup"><span data-stu-id="36310-227">hello parameter contains hello data toobe inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="36310-228">Если пользовательские уникальное значение идентификатора не включается в hello `todoItem` во время операции вставки, идентификатор GUID создается сервером hello.</span><span class="sxs-lookup"><span data-stu-id="36310-228">If a unique custom ID value is not included in hello `todoItem` during an insert, a GUID is generated by hello server.</span></span>
<span data-ttu-id="36310-229">Вы можете получить hello созданный идентификатор, изучая hello объекта после возвращения вызова hello.</span><span class="sxs-lookup"><span data-stu-id="36310-229">You can retrieve hello generated Id by inspecting hello object after hello call returns.</span></span>

<span data-ttu-id="36310-230">tooinsert нетипизированных данных, могут воспользоваться преимуществами Json.NET:</span><span class="sxs-lookup"><span data-stu-id="36310-230">tooinsert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="36310-231">Вот пример использования электронного адреса в качестве уникального строкового идентификатора.</span><span class="sxs-lookup"><span data-stu-id="36310-231">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="36310-232">Работа со значениями идентификаторов</span><span class="sxs-lookup"><span data-stu-id="36310-232">Working with ID values</span></span>
<span data-ttu-id="36310-233">Мобильные приложения поддерживает уникальная строка пользовательские значения для таблицы hello **идентификатор** столбца.</span><span class="sxs-lookup"><span data-stu-id="36310-233">Mobile Apps supports unique custom string values for hello table's **id** column.</span></span> <span data-ttu-id="36310-234">Строковое значение позволяет приложениям toouse пользовательские значения, такие как адреса электронной почты или имена пользователей для идентификатора hello.</span><span class="sxs-lookup"><span data-stu-id="36310-234">A string value allows applications toouse custom values such as email addresses or user names for hello ID.</span></span>  <span data-ttu-id="36310-235">Идентификаторами строк предоставить hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="36310-235">String IDs provide you with hello following benefits:</span></span>

* <span data-ttu-id="36310-236">Идентификаторы создаются без создания базы данных toohello кругового пути.</span><span class="sxs-lookup"><span data-stu-id="36310-236">IDs are generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="36310-237">Записи, проще toomerge из различных таблиц или баз данных.</span><span class="sxs-lookup"><span data-stu-id="36310-237">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="36310-238">Значения идентификаторов можно удобно интегрировать с логикой приложения.</span><span class="sxs-lookup"><span data-stu-id="36310-238">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="36310-239">Если строковое значение идентификатора для вставленной записи не задан, внутреннего сервера мобильного приложения hello формирует уникальное значение для идентификатора.</span><span class="sxs-lookup"><span data-stu-id="36310-239">When a string ID value is not set on an inserted record, hello Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="36310-240">Можно использовать hello [Guid.NewGuid] toogenerate метод собственный идентификатор значения на приветствия клиента или на внутреннем сервере hello.</span><span class="sxs-lookup"><span data-stu-id="36310-240">You can use hello [Guid.NewGuid] method toogenerate your own ID values, either on hello client or in hello backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="36310-241"><a name="modifying"></a>Практическое руководство. Изменение данных в серверной части мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="36310-241"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="36310-242">Hello следующий код показывает, как toouse hello [UpdateAsync] tooupdate метод существующей записи с hello таким же ИДЕНТИФИКАТОРОМ с новыми данными.</span><span class="sxs-lookup"><span data-stu-id="36310-242">hello following code illustrates how toouse hello [UpdateAsync] method tooupdate an existing record with hello same ID with new information.</span></span> <span data-ttu-id="36310-243">параметр Hello содержит toobe данных hello обновлен как объект .NET.</span><span class="sxs-lookup"><span data-stu-id="36310-243">hello parameter contains hello data toobe updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="36310-244">tooupdate нетипизированных данных, могут воспользоваться преимуществами [Json.NET] следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36310-244">tooupdate untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="36310-245">При выполнении обновления необходимо указать поле `id` .</span><span class="sxs-lookup"><span data-stu-id="36310-245">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="36310-246">Hello внутренним сервером hello `id` tooidentify поля которого tooupdate строк.</span><span class="sxs-lookup"><span data-stu-id="36310-246">hello backend uses hello `id` field tooidentify which row tooupdate.</span></span> <span data-ttu-id="36310-247">Hello `id` поля можно получить из результата hello hello `InsertAsync` вызова.</span><span class="sxs-lookup"><span data-stu-id="36310-247">hello `id` field can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="36310-248">`ArgumentException` Возникает при попытке tooupdate элемент без предоставления hello `id` значение.</span><span class="sxs-lookup"><span data-stu-id="36310-248">An `ArgumentException` is raised if you try tooupdate an item without providing hello `id` value.</span></span>

### <span data-ttu-id="36310-249"><a name="deleting"></a>Практическое руководство. Удаление данных в серверной части мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="36310-249"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="36310-250">Hello следующий код показывает, как toouse hello [DeleteAsync] toodelete метод существующего экземпляра.</span><span class="sxs-lookup"><span data-stu-id="36310-250">hello following code illustrates how toouse hello [DeleteAsync] method toodelete an existing instance.</span></span> <span data-ttu-id="36310-251">экземпляр Hello определяется hello `id` наборе на hello полей `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="36310-251">hello instance is identified by hello `id` field set on hello `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="36310-252">toodelete нетипизированных данных, может использовать преимущества Json.NET следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36310-252">toodelete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="36310-253">При создании запроса на удаление необходимо указать идентификатор.</span><span class="sxs-lookup"><span data-stu-id="36310-253">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="36310-254">Другие свойства, не передаются toohello службы или учитываются в службе hello.</span><span class="sxs-lookup"><span data-stu-id="36310-254">Other properties are not passed toohello service or are ignored at hello service.</span></span> <span data-ttu-id="36310-255">Здравствуйте, результат `DeleteAsync` обычно является вызов `null`.</span><span class="sxs-lookup"><span data-stu-id="36310-255">hello result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="36310-256">toopass идентификатор Hello в можно получить из результата hello hello `InsertAsync` вызова.</span><span class="sxs-lookup"><span data-stu-id="36310-256">hello ID toopass in can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="36310-257">Объект `MobileServiceInvalidOperationException` возникает при попытке toodelete элемент без указания hello `id` поля.</span><span class="sxs-lookup"><span data-stu-id="36310-257">A `MobileServiceInvalidOperationException` is thrown when you try toodelete an item without specifying hello `id` field.</span></span>

### <span data-ttu-id="36310-258"><a name="optimisticconcurrency"></a>Практическое руководство. Использование оптимистичного параллелизма для устранения конфликтов</span><span class="sxs-lookup"><span data-stu-id="36310-258"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="36310-259">Два или несколько клиентов могут записывать изменения toohello же элемент в hello, же время.</span><span class="sxs-lookup"><span data-stu-id="36310-259">Two or more clients may write changes toohello same item at hello same time.</span></span> <span data-ttu-id="36310-260">Без обнаружения конфликтов последняя запись hello перезапишет все предыдущие обновления.</span><span class="sxs-lookup"><span data-stu-id="36310-260">Without conflict detection, hello last write would overwrite any previous updates.</span></span> <span data-ttu-id="36310-261">**управлении оптимистичным параллелизмом** предполагается, что каждая транзакция может фиксироваться, поэтому не использует блокировки каких-либо ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36310-261">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="36310-262">Прежде чем фиксировать транзакции, управление оптимистичным параллелизмом проверяет, что никакая другая транзакция изменила данные hello.</span><span class="sxs-lookup"><span data-stu-id="36310-262">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified hello data.</span></span> <span data-ttu-id="36310-263">Если был изменен hello данных hello Фиксация транзакции выполняется откат.</span><span class="sxs-lookup"><span data-stu-id="36310-263">If hello data has been modified, hello committing transaction is rolled back.</span></span>

<span data-ttu-id="36310-264">Мобильные приложения поддерживает управление оптимистичным параллелизмом, отслеживая изменения tooeach элемента с помощью hello `version` столбец системного свойства, определенные для каждой таблицы в серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="36310-264">Mobile Apps supports optimistic concurrency control by tracking changes tooeach item using hello `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="36310-265">Каждый раз при обновлении записи мобильные приложения задает hello `version` свойства для этой записи tooa новое значение.</span><span class="sxs-lookup"><span data-stu-id="36310-265">Each time a record is updated, Mobile Apps sets hello `version` property for that record tooa new value.</span></span> <span data-ttu-id="36310-266">Во время каждого запроса update hello `version` hello-записи, входящий в состав hello запроса является сравниваемых toohello же свойство для записи hello на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="36310-266">During each update request, hello `version` property of hello record included with hello request is compared toohello same property for hello record on hello server.</span></span> <span data-ttu-id="36310-267">При передаче версию с hello запроса не соответствует hello серверной части, а затем вызывает hello клиентская библиотека `MobileServicePreconditionFailedException<T>` исключение.</span><span class="sxs-lookup"><span data-stu-id="36310-267">If the version passed with hello request does not match hello backend, then hello client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="36310-268">Тип Hello, входящий в состав hello исключение — hello запись с hello серверной части содержащего hello серверы версий hello записи.</span><span class="sxs-lookup"><span data-stu-id="36310-268">hello type included with hello exception is hello record from hello backend containing hello servers version of hello record.</span></span> <span data-ttu-id="36310-269">Hello затем приложение может использовать этот toodecide сведения ли запрос tooexecute hello обновления, указав правильный hello `version` значение от изменений toocommit hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="36310-269">hello application can then use this information toodecide whether tooexecute hello update request again with hello correct `version` value from hello backend toocommit changes.</span></span>

<span data-ttu-id="36310-270">Определения столбцов для класса таблицы hello для hello `version` системы свойство tooenable оптимистичного параллелизма.</span><span class="sxs-lookup"><span data-stu-id="36310-270">Define a column on hello table class for hello `version` system property tooenable optimistic concurrency.</span></span> <span data-ttu-id="36310-271">Например:</span><span class="sxs-lookup"><span data-stu-id="36310-271">For example:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

<span data-ttu-id="36310-272">Приложения, использующие нетипизированный таблиц включите оптимистичного параллелизма, установка hello `Version` флаг `SystemProperties` из hello таблицы следующим образом.</span><span class="sxs-lookup"><span data-stu-id="36310-272">Applications using untyped tables enable optimistic concurrency by setting hello `Version` flag on the `SystemProperties` of hello table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="36310-273">При оптимистическом параллелизме tooenabling сложения, должен перехватывать hello `MobileServicePreconditionFailedException<T>` исключений в коде, при вызове [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="36310-273">In addition tooenabling optimistic concurrency, you must also catch hello `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="36310-274">Разрешить конфликт hello, применяя hello правильный `version` toothe обновленные записи и вызов [UpdateAsync] с hello разрешил запись.</span><span class="sxs-lookup"><span data-stu-id="36310-274">Resolve hello conflict by applying hello correct `version` toothe updated record and call [UpdateAsync] with hello resolved record.</span></span> <span data-ttu-id="36310-275">Hello, следующий код показывает, как tooresolve записи один раз конфликт:</span><span class="sxs-lookup"><span data-stu-id="36310-275">hello following code shows how tooresolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="36310-276">Дополнительные сведения см. в разделе hello [автономной синхронизации данных в мобильных приложениях Azure] раздела.</span><span class="sxs-lookup"><span data-stu-id="36310-276">For more information, see hello [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="36310-277"><a name="binding"></a>Как: пользовательский интерфейс Windows tooa мобильных приложениях привязки данных</span><span class="sxs-lookup"><span data-stu-id="36310-277"><a name="binding"></a>How to: Bind Mobile Apps data tooa Windows user interface</span></span>
<span data-ttu-id="36310-278">В этом разделе показано, как toodisplay возвращают объекты данных с помощью элементов пользовательского интерфейса в приложении Windows.</span><span class="sxs-lookup"><span data-stu-id="36310-278">This section shows how toodisplay returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="36310-279">В следующем примере кода привязывает источник toohello hello списка с помощью запроса для неполных элементов.</span><span class="sxs-lookup"><span data-stu-id="36310-279">The following example code binds toohello source of hello list with a query for incomplete items.</span></span> <span data-ttu-id="36310-280">При использовании [MobileServiceCollection] создается коллекция привязок, поддерживающих мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="36310-280">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="36310-281">Некоторые элементы управления в hello управляемых поддержку среды выполнения, называют интерфейс [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="36310-281">Some controls in hello managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="36310-282">Этот интерфейс позволяет toorequest элементов управления при прокрутке hello дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="36310-282">This interface allows controls toorequest extra data when hello user scrolls.</span></span> <span data-ttu-id="36310-283">Имеется встроенная поддержка для универсальных приложений Windows через этот интерфейс [MobileServiceIncrementalLoadingCollection], которая автоматически обрабатывает вызовы из элементов управления hello.</span><span class="sxs-lookup"><span data-stu-id="36310-283">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from hello controls.</span></span> <span data-ttu-id="36310-284">Используйте `MobileServiceIncrementalLoadingCollection` в приложениях для Windows, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="36310-284">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="36310-285">toouse hello новую коллекцию в приложениях Windows Phone 8 и «Silverlight», используйте hello `ToCollection` методы расширения в `IMobileServiceTableQuery<T>` и `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="36310-285">toouse hello new collection on Windows Phone 8 and "Silverlight" apps, use hello `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="36310-286">вызов данных tooload `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="36310-286">tooload data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="36310-287">При использовании коллекции hello создаются путем вызова `ToCollectionAsync` или `ToCollection`, получить коллекцию, которая может быть tooUI связанных элементов управления.</span><span class="sxs-lookup"><span data-stu-id="36310-287">When you use hello collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound tooUI controls.</span></span>  <span data-ttu-id="36310-288">Эта коллекция поддерживает разбиение по страницам.</span><span class="sxs-lookup"><span data-stu-id="36310-288">This collection is paging-aware.</span></span>  <span data-ttu-id="36310-289">Так как коллекция элементов hello загружает данные из сети, иногда загрузка завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="36310-289">Since hello collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="36310-290">toohandle таких сбоев переопределить hello `OnException` метод `MobileServiceIncrementalLoadingCollection` toohandle исключения, возникающие в результате вызовов слишком`LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="36310-290">toohandle such failures, override hello `OnException` method on `MobileServiceIncrementalLoadingCollection` toohandle exceptions resulting from calls too`LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="36310-291">Рекомендуется, если таблица содержит много полей, но требуется только toodisplay некоторые из них в элементе управления.</span><span class="sxs-lookup"><span data-stu-id="36310-291">Consider if your table has many fields but you only want toodisplay some of them in your control.</span></span> <span data-ttu-id="36310-292">Вы можете использовать руководство hello в hello предшествующий раздел «[выбирать отдельные столбцы](#selecting)» tooselect toodisplay определенные столбцы в hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="36310-292">You may use hello guidance in hello preceding section "[Select specific columns](#selecting)" tooselect specific columns toodisplay in hello UI.</span></span>

### <span data-ttu-id="36310-293"><a name="pagesize"></a>Hello изменение размера страницы</span><span class="sxs-lookup"><span data-stu-id="36310-293"><a name="pagesize"></a>Change hello Page size</span></span>
<span data-ttu-id="36310-294">По умолчанию мобильные приложения Azure выдают не больше 50 элементов на запрос.</span><span class="sxs-lookup"><span data-stu-id="36310-294">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="36310-295">Можно изменить объем подкачки hello увеличив hello максимальный размер страницы приветствия клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="36310-295">You can change hello paging size by increasing hello maximum page size on both hello client and server.</span></span>  <span data-ttu-id="36310-296">tooincrease Здравствуйте запрошенный размер страницы, укажите `PullOptions` при использовании `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="36310-296">tooincrease hello requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="36310-297">При условии, что были внесены hello `PageSize` равно tooor больше 100 в пределах сервера hello, запрос возвращает до 100 элементов.</span><span class="sxs-lookup"><span data-stu-id="36310-297">Assuming you have made hello `PageSize` equal tooor greater than 100 within hello server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="36310-298"><a name="#offlinesync"></a>Работа с автономными таблицами</span><span class="sxs-lookup"><span data-stu-id="36310-298"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="36310-299">Автономные таблицы используйте локального хранения данных toostore SQLite для использования в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="36310-299">Offline tables use a local SQLite store toostore data for use when offline.</span></span>  <span data-ttu-id="36310-300">Все операции осуществляются с hello таблицы локального SQLite хранилища вместо хранилище hello удаленного сервера.</span><span class="sxs-lookup"><span data-stu-id="36310-300">All table operations are done against hello local SQLite store instead of hello remote server store.</span></span>  <span data-ttu-id="36310-301">toocreate автономной таблицы, сначала подготовить проект:</span><span class="sxs-lookup"><span data-stu-id="36310-301">toocreate an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="36310-302">В Visual Studio щелкните правой кнопкой мыши решение hello > **управление пакетами NuGet для решения...** , выполните поиск и установка **Microsoft.Azure.Mobile.Client.SQLiteStore** пакет NuGet для всех проектов в решении hello.</span><span class="sxs-lookup"><span data-stu-id="36310-302">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="36310-303">(Необязательно) toosupport устройства Windows, установите одно из следующих пакетов среды выполнения SQLite hello.</span><span class="sxs-lookup"><span data-stu-id="36310-303">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="36310-304">**Среда выполнения Windows 8.1**: установите [SQLite для Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="36310-304">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="36310-305">**Windows Phone 8.1**: установите [SQLite для Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="36310-305">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="36310-306">**Универсальная платформа Windows** установить [SQLite для универсальных приложений Windows hello][5].</span><span class="sxs-lookup"><span data-stu-id="36310-306">**Universal Windows Platform** Install [SQLite for hello Universal Windows][5].</span></span>
3. <span data-ttu-id="36310-307">(необязательно).</span><span class="sxs-lookup"><span data-stu-id="36310-307">(Optional).</span></span> <span data-ttu-id="36310-308">Для устройств Windows, нажмите кнопку **ссылки** > **добавить ссылку...** , разверните hello **Windows** папки > **расширения**, включите соответствующий hello **SQLite для Windows** пакета SDK, а также hello  **Среда выполнения 2013 Visual C++ для Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="36310-308">For Windows devices, click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**, then enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="36310-309">Hello SQLite SDK имена будут немного отличаться с каждой платформы Windows.</span><span class="sxs-lookup"><span data-stu-id="36310-309">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="36310-310">Чтобы можно было создать ссылку на таблицу, необходимо подготовить hello локального хранилища:</span><span class="sxs-lookup"><span data-stu-id="36310-310">Before a table reference can be created, hello local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="36310-311">Инициализации хранилища, обычно осуществляется сразу после создания клиента hello.</span><span class="sxs-lookup"><span data-stu-id="36310-311">Store initialization is normally done immediately after hello client is created.</span></span>  <span data-ttu-id="36310-312">Hello **OfflineDbPath** должно быть имя файла можно использовать на всех платформах, которые вы поддерживаете.</span><span class="sxs-lookup"><span data-stu-id="36310-312">hello **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="36310-313">Если путь hello полный путь (то есть, он начинается с косой черты), то используется этот путь.</span><span class="sxs-lookup"><span data-stu-id="36310-313">If hello path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="36310-314">Если hello путь задан не полностью, hello файл помещается в месте конкретную платформу.</span><span class="sxs-lookup"><span data-stu-id="36310-314">If hello path is not fully qualified, hello file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="36310-315">Для устройств iOS и Android путь по умолчанию hello — папка «Личные файлы» hello.</span><span class="sxs-lookup"><span data-stu-id="36310-315">For iOS and Android devices, hello default path is hello "Personal Files" folder.</span></span>
* <span data-ttu-id="36310-316">Для устройств Windows hello путь по умолчанию — папка «AppData» hello конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="36310-316">For Windows devices, hello default path is hello application-specific "AppData" folder.</span></span>

<span data-ttu-id="36310-317">Ссылки на таблицу можно получить, используя hello `GetSyncTable<>` метод:</span><span class="sxs-lookup"><span data-stu-id="36310-317">A table reference can be obtained using hello `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="36310-318">Tooauthenticate toouse автономной таблицы не обязательно.</span><span class="sxs-lookup"><span data-stu-id="36310-318">You do not need tooauthenticate toouse an offline table.</span></span>  <span data-ttu-id="36310-319">Tooauthenticate необходим только в том случае, при которой осуществляется взаимодействие с серверной службы hello.</span><span class="sxs-lookup"><span data-stu-id="36310-319">You only need tooauthenticate when you are communicating with hello backend service.</span></span>

### <span data-ttu-id="36310-320"><a name="syncoffline"></a>Синхронизация автономной таблицы</span><span class="sxs-lookup"><span data-stu-id="36310-320"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="36310-321">Автономные таблиц не синхронизирован с серверной hello по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="36310-321">Offline tables are not synchronized with hello backend by default.</span></span>  <span data-ttu-id="36310-322">Синхронизация происходит в два этапа.</span><span class="sxs-lookup"><span data-stu-id="36310-322">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="36310-323">Можно передавать изменения отдельно от скачивания новых элементов.</span><span class="sxs-lookup"><span data-stu-id="36310-323">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="36310-324">Ниже приведен типичный метод синхронизации.</span><span class="sxs-lookup"><span data-stu-id="36310-324">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
            //Use a different query name for each unique query in your program
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

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
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

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

<span data-ttu-id="36310-325">Если слишком hello первый аргумент`PullAsync` имеет значение null, то добавочной синхронизации не используется.</span><span class="sxs-lookup"><span data-stu-id="36310-325">If hello first argument too`PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="36310-326">Каждая операция синхронизации извлекает все записи.</span><span class="sxs-lookup"><span data-stu-id="36310-326">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="36310-327">Выполняет неявную Hello SDK `PushAsync()` прежде чем извлекать записей.</span><span class="sxs-lookup"><span data-stu-id="36310-327">hello SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="36310-328">Обработка конфликтов происходит в методе `PullAsync()`.</span><span class="sxs-lookup"><span data-stu-id="36310-328">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="36310-329">Можно обработать конфликтов в hello таким же, как online таблиц.</span><span class="sxs-lookup"><span data-stu-id="36310-329">You can deal with conflicts in hello same way as online tables.</span></span>  <span data-ttu-id="36310-330">Hello конфликтов производится при `PullAsync()` вызывается вместо во время hello insert, update или delete.</span><span class="sxs-lookup"><span data-stu-id="36310-330">hello conflict is produced when `PullAsync()` is called instead of during hello insert, update, or delete.</span></span> <span data-ttu-id="36310-331">Если возникает несколько конфликтов, они объединяются в одно исключение MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="36310-331">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="36310-332">Каждая ошибка должна обрабатываться отдельно.</span><span class="sxs-lookup"><span data-stu-id="36310-332">Handle each failure separately.</span></span>

## <span data-ttu-id="36310-333"><a name="#customapi"></a>Работа с настраиваемым API</span><span class="sxs-lookup"><span data-stu-id="36310-333"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="36310-334">Пользовательский API позволяет toodefine пользовательских конечных точек, предоставляющих функциональные возможности сервера, которые не сопоставляются tooan вставки, обновления, удаления или операцию чтения.</span><span class="sxs-lookup"><span data-stu-id="36310-334">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="36310-335">При использовании настраиваемого интерфейса API вы получаете больше возможностей для управления сообщениями, в том числе для чтения и установки заголовков HTTP-сообщений, а также определения форматов текста сообщений, отличных от JSON.</span><span class="sxs-lookup"><span data-stu-id="36310-335">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="36310-336">Вызов пользовательского API путем вызова одного из hello [InvokeApiAsync] методов на приветствия клиента.</span><span class="sxs-lookup"><span data-stu-id="36310-336">You call a custom API by calling one of hello [InvokeApiAsync] methods on hello client.</span></span> <span data-ttu-id="36310-337">Например, следующая строка кода hello отправляет запрос POST toohello **completeAll** API hello серверную часть:</span><span class="sxs-lookup"><span data-stu-id="36310-337">For example, hello following line of code sends a POST request toohello **completeAll** API on hello backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="36310-338">Эта форма представляет собой вызов типизированный метод и требует этого hello **MarkAllResult** возвращают тип определен.</span><span class="sxs-lookup"><span data-stu-id="36310-338">This form is a typed method call and requires that hello **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="36310-339">Поддерживаются типизированные и нетипизированные методы.</span><span class="sxs-lookup"><span data-stu-id="36310-339">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="36310-340">метод InvokeApiAsync() Hello добавляет/api/toohello API обратиться toocall Если hello API начинается с «/».</span><span class="sxs-lookup"><span data-stu-id="36310-340">hello InvokeApiAsync() method prepends '/api/' toohello API that you wish toocall unless hello API starts with a '/'.</span></span>
<span data-ttu-id="36310-341">Например:</span><span class="sxs-lookup"><span data-stu-id="36310-341">For example:</span></span>

* <span data-ttu-id="36310-342">`InvokeApiAsync("completeAll",...)`вызывает /api/completeAll серверную часть hello</span><span class="sxs-lookup"><span data-stu-id="36310-342">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on hello backend</span></span>
* <span data-ttu-id="36310-343">`InvokeApiAsync("/.auth/me",...)`вызывает /.auth/me серверную часть hello</span><span class="sxs-lookup"><span data-stu-id="36310-343">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on hello backend</span></span>

<span data-ttu-id="36310-344">InvokeApiAsync toocall можно использовать любой WebAPI, включая те WebAPIs, которые не определены с помощью мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="36310-344">You can use InvokeApiAsync toocall any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="36310-345">При использовании InvokeApiAsync() hello соответствующие заголовки, включая заголовки проверки подлинности, отправляются с запросом hello.</span><span class="sxs-lookup"><span data-stu-id="36310-345">When you use InvokeApiAsync(), hello appropriate headers, including authentication headers, are sent with hello request.</span></span>

## <span data-ttu-id="36310-346"><a name="authentication"></a>Аутентификация пользователей</span><span class="sxs-lookup"><span data-stu-id="36310-346"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="36310-347">Мобильные приложения поддерживают аутентификацию и авторизацию пользователей с помощью различных внешних поставщиков удостоверений: Facebook, Google, учетной записи Майкрософт, Twitter и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36310-347">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="36310-348">Можно задать разрешения для таблицы toorestrict доступ для определенных операций tooonly проверку подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="36310-348">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="36310-349">Hello идентификаторов правил авторизации tooimplement прошедших проверку подлинности пользователей также можно использовать в серверных скриптах.</span><span class="sxs-lookup"><span data-stu-id="36310-349">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="36310-350">Дополнительные сведения см. в разделе учебника hello [приложение tooyour authentication добавить].</span><span class="sxs-lookup"><span data-stu-id="36310-350">For more information, see hello tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="36310-351">Поддерживаются два потока аутентификации: *управляемой клиентом* и *управляемый сервером*.</span><span class="sxs-lookup"><span data-stu-id="36310-351">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="36310-352">Поток управляемого сервером Hello обеспечивает hello простой проверки подлинности, как зависит от поставщика hello веб-интерфейс проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="36310-352">hello server-managed flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="36310-353">Hello клиента управляемого потока позволяет более глубокую интеграцию с возможности определенных устройств, как он основывается на пакеты SDK поставщика конкретного устройства.</span><span class="sxs-lookup"><span data-stu-id="36310-353">hello client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="36310-354">Мы рекомендуем использовать в рабочих приложениях поток, управляемый клиентом.</span><span class="sxs-lookup"><span data-stu-id="36310-354">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="36310-355">tooset проверку подлинности, необходимо зарегистрировать приложение с одним или несколькими поставщиками удостоверений.</span><span class="sxs-lookup"><span data-stu-id="36310-355">tooset up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="36310-356">Поставщик удостоверений Hello создает идентификатор клиента и секрет клиента для приложения.</span><span class="sxs-lookup"><span data-stu-id="36310-356">hello identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="36310-357">Затем эти значения устанавливаются в вашей серверной tooenable службе приложений Azure проверки подлинности и авторизации.</span><span class="sxs-lookup"><span data-stu-id="36310-357">These values are then set in your backend tooenable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="36310-358">Для получения дополнительной информации выполните hello подробные инструкции в учебнике [приложение tooyour authentication добавить].</span><span class="sxs-lookup"><span data-stu-id="36310-358">For more information, follow hello detailed instructions in the tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="36310-359">в этом разделе рассматриваются следующие вопросы Hello:</span><span class="sxs-lookup"><span data-stu-id="36310-359">hello following topics are covered in this section:</span></span>

* [<span data-ttu-id="36310-360">Управляемая клиентом проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="36310-360">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="36310-361">Управляемая сервером проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="36310-361">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="36310-362">Маркер проверки подлинности кэширования hello</span><span class="sxs-lookup"><span data-stu-id="36310-362">Caching hello authentication token</span></span>](#caching)

### <span data-ttu-id="36310-363"><a name="clientflow"></a>Управляемая клиентом проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="36310-363"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="36310-364">Приложения могут независимо обращаться hello поставщика удостоверений и, после чего укажите hello возвращенный токен во время входа серверной части.</span><span class="sxs-lookup"><span data-stu-id="36310-364">Your app can independently contact hello identity provider and then provide hello returned token during login with your backend.</span></span> <span data-ttu-id="36310-365">Этот порядок клиента позволяет tooprovide единого интерфейса входа для пользователей или tooretrieve дополнительные пользовательские данные от поставщика удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="36310-365">This client flow enables you tooprovide a single sign-on experience for users or tooretrieve additional user data from hello identity provider.</span></span> <span data-ttu-id="36310-366">Проверки подлинности для потока клиента — предпочтительный toousing потока сервере как поставщик удостоверений hello SDK предоставляет более естественным вид UX и обеспечивает дополнительные настройки.</span><span class="sxs-lookup"><span data-stu-id="36310-366">Client flow authentication is preferred toousing a server flow as hello identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="36310-367">Примеры для hello следующие шаблоны проверки подлинности клиента потока:</span><span class="sxs-lookup"><span data-stu-id="36310-367">Examples are provided for hello following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="36310-368">Библиотека проверки подлинности Active Directory</span><span class="sxs-lookup"><span data-stu-id="36310-368">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="36310-369">Facebook или Google</span><span class="sxs-lookup"><span data-stu-id="36310-369">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="36310-370">Пакет Live SDK</span><span class="sxs-lookup"><span data-stu-id="36310-370">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="36310-371"><a name="adal"></a>Проверять подлинность пользователей с hello библиотеку аутентификации Active Directory</span><span class="sxs-lookup"><span data-stu-id="36310-371"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="36310-372">Можно использовать hello библиотеку проверки подлинности Active Directory (ADAL) tooinitiate пользователя проверку подлинности от клиента hello, с использованием проверки подлинности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36310-372">You can use hello Active Directory Authentication Library (ADAL) tooinitiate user authentication from hello client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="36310-373">Настройте внутренний сервер мобильных приложений для входа AAD, следующие hello [как tooconfigure приложения службы для имени входа Active Directory] учебника.</span><span class="sxs-lookup"><span data-stu-id="36310-373">Configure your mobile app backend for AAD sign-on by following hello [How tooconfigure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="36310-374">Убедитесь, что необязательный шаг toocomplete hello регистрации собственного клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="36310-374">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="36310-375">В Visual Studio и Xamarin Studio, откройте проект и добавить toothe ссылки `Microsoft.IdentityModel.CLients.ActiveDirectory` пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="36310-375">In Visual Studio or Xamarin Studio, open your project and add a reference toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="36310-376">Включите в диапазон поиска предварительные версии.</span><span class="sxs-lookup"><span data-stu-id="36310-376">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="36310-377">Добавьте hello следующие приложения tooyour кода, в соответствии с toohello платформы, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="36310-377">Add hello following code tooyour application, according toohello platform you are using.</span></span> <span data-ttu-id="36310-378">В каждой из них внесите hello после замены.</span><span class="sxs-lookup"><span data-stu-id="36310-378">In each, make hello following replacements:</span></span>

   * <span data-ttu-id="36310-379">Замените **вставки ЦЕНТРА здесь** hello имя клиента hello, в котором подготовлено приложения.</span><span class="sxs-lookup"><span data-stu-id="36310-379">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="36310-380">Формат должен быть следующим: https://login.microsoftonline.com/contoso.onmicrosoft.com. Это значение можно скопировать из hello вкладка домена в Azure Active Directory в hello [классический портал Azure].</span><span class="sxs-lookup"><span data-stu-id="36310-380">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="36310-381">Замените **вставки РЕСУРСОВ-идентификатор здесь** с Идентификатором hello клиент для мобильного приложения серверной части.</span><span class="sxs-lookup"><span data-stu-id="36310-381">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="36310-382">Можно получить идентификатор клиента hello hello **Дополнительно** в разделе **параметры Azure Active Directory** hello портала.</span><span class="sxs-lookup"><span data-stu-id="36310-382">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="36310-383">Замените **вставки КЛИЕНТА-идентификатор здесь** с Идентификатором клиента hello, скопированные из собственного клиентского приложения hello.</span><span class="sxs-lookup"><span data-stu-id="36310-383">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="36310-384">Замените **вставки ПЕРЕНАПРАВЛЕНИЯ-URI здесь** с веб-узла */.auth/login/done* конечную точку, используя hello схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="36310-384">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="36310-385">Это значение должно быть примерно слишком*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="36310-385">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="36310-386">Hello код, необходимый для каждой платформы выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36310-386">hello code needed for each platform follows:</span></span>

     <span data-ttu-id="36310-387">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="36310-387">**Windows:**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     <span data-ttu-id="36310-388">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="36310-388">**Xamarin.iOS**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     <span data-ttu-id="36310-389">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="36310-389">**Xamarin.Android**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <span data-ttu-id="36310-390"><a name="client-facebook"></a>Единый вход с помощью маркера Google или Facebook</span><span class="sxs-lookup"><span data-stu-id="36310-390"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="36310-391">Вы можете использовать поток клиентских hello, как показано в этом фрагменте кода для Google или Facebook.</span><span class="sxs-lookup"><span data-stu-id="36310-391">You can use hello client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <span data-ttu-id="36310-392"><a name="client-livesdk"></a>Здравствуйте, единого входа в систему под учетной записью Майкрософт с помощью пакета SDK Live</span><span class="sxs-lookup"><span data-stu-id="36310-392"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with hello Live SDK</span></span>
<span data-ttu-id="36310-393">tooauthenticate пользователей, необходимо зарегистрировать приложения в учетной записи Майкрософт Центр разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="36310-393">tooauthenticate users, you must register your app at hello Microsoft account Developer Center.</span></span> <span data-ttu-id="36310-394">Настройте регистрационные данные для серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="36310-394">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="36310-395">toocreate Microsoft Регистрация учетной записи и подключите его серверной tooyour мобильного приложения, завершения hello шагов в [регистрации вашего приложения toouse имя входа учетной записи Майкрософт].</span><span class="sxs-lookup"><span data-stu-id="36310-395">toocreate a Microsoft account registration and connect it tooyour Mobile App backend, complete hello steps in [Register your app toouse a Microsoft account login].</span></span> <span data-ttu-id="36310-396">При наличии магазина Windows и Windows Phone 8/Silverlight версии приложения сначала зарегистрируйте версии магазина Windows hello.</span><span class="sxs-lookup"><span data-stu-id="36310-396">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register hello Windows Store version first.</span></span>

<span data-ttu-id="36310-397">Hello следующий код выполняет проверку подлинности с помощью пакета SDK Live и использует hello, возвращается токен toosign в серверной части tooyour мобильное приложение.</span><span class="sxs-lookup"><span data-stu-id="36310-397">hello following code authenticates using Live SDK and uses hello returned token toosign in tooyour Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

<span data-ttu-id="36310-398">Дополнительные сведения см. в разделе hello [пакета SDK Live Windows] документации.</span><span class="sxs-lookup"><span data-stu-id="36310-398">For more information, see hello [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="36310-399"><a name="serverflow"></a>Управляемая сервером проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="36310-399"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="36310-400">После регистрации поставщика удостоверений, вызовите hello [LoginAsync] метод hello [MobileServiceClient] с hello [MobileServiceAuthenticationProvider] значение поставщика.</span><span class="sxs-lookup"><span data-stu-id="36310-400">Once you have registered your identity provider, call hello [LoginAsync] method on hello [MobileServiceClient] with hello [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="36310-401">Например hello следующий код инициирует вход потока сервера с помощью Facebook.</span><span class="sxs-lookup"><span data-stu-id="36310-401">For example, hello following code initiates a server flow sign-in by using Facebook.</span></span>

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

<span data-ttu-id="36310-402">При использовании поставщика удостоверений, отличные от Facebook, измените значение hello [MobileServiceAuthenticationProvider] toohello значение для поставщика.</span><span class="sxs-lookup"><span data-stu-id="36310-402">If you are using an identity provider other than Facebook, change hello value of [MobileServiceAuthenticationProvider] toohello value for your provider.</span></span>

<span data-ttu-id="36310-403">В потоке сервера службы приложений Azure управляет поток проверки подлинности OAuth hello путем отображения приветствия на странице входа hello выбранного поставщика.</span><span class="sxs-lookup"><span data-stu-id="36310-403">In a server flow, Azure App Service manages hello OAuth authentication flow by displaying hello sign-in page of hello selected provider.</span></span>  <span data-ttu-id="36310-404">Один раз возвращает поставщик удостоверений hello, службе приложений Azure создает маркер проверки подлинности службы приложений.</span><span class="sxs-lookup"><span data-stu-id="36310-404">Once hello identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="36310-405">Hello [LoginAsync] возвращает [MobileServiceUser], который предоставляет оба hello [UserId] из hello и проверкой подлинности пользователя hello [ MobileServiceAuthenticationToken], как веб-токен JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="36310-405">hello [LoginAsync] method returns a [MobileServiceUser], which provides both hello [UserId] of hello authenticated user and hello [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="36310-406">Этот маркер можно поместить в кэш и повторно использовать, пока не истечет срок его действия.</span><span class="sxs-lookup"><span data-stu-id="36310-406">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="36310-407">Дополнительные сведения см. в разделе [токена проверки подлинности hello кэширование](#caching).</span><span class="sxs-lookup"><span data-stu-id="36310-407">For more information, see [Caching hello authentication token](#caching).</span></span>

### <span data-ttu-id="36310-408"><a name="caching"></a>Маркер проверки подлинности кэширования hello</span><span class="sxs-lookup"><span data-stu-id="36310-408"><a name="caching"></a>Caching hello authentication token</span></span>
<span data-ttu-id="36310-409">В некоторых случаях можно избежать toohello входа hello вызов метода после первого успешного прохождения проверки подлинности hello, сохраняя hello токена проверки подлинности от поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="36310-409">In some cases, hello call toohello login method can be avoided after hello first successful authentication by storing hello authentication token from hello provider.</span></span>  <span data-ttu-id="36310-410">Можно использовать для приложений магазина Windows и UWP [PasswordVault] toocache текущего проверки подлинности маркера после успешного входа в систему, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36310-410">Windows Store and UWP apps can use [PasswordVault] toocache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="36310-411">Hello UserId значение хранится в виде hello hello учетных данных пользователя и маркер hello — hello, хранятся в виде hello пароль.</span><span class="sxs-lookup"><span data-stu-id="36310-411">hello UserId value is stored as hello UserName of hello credential and hello token is hello stored as hello Password.</span></span> <span data-ttu-id="36310-412">В последующих начинающих можно проверить hello **PasswordVault** для кэшированных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="36310-412">On subsequent start-ups, you can check hello **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="36310-413">Hello следующий пример использует кэшированные учетные данные, когда они находятся, а в противном случае попытки tooauthenticate с серверной hello.</span><span class="sxs-lookup"><span data-stu-id="36310-413">hello following example uses cached credentials when they are found, and otherwise attempts tooauthenticate again with hello backend:</span></span>

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

<span data-ttu-id="36310-414">Выйти из системы пользователя, также необходимо удалить hello хранимых учетных данных, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36310-414">When you sign out a user, you must also remove hello stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="36310-415">Приложения Xamarin использовать hello [Xamarin.Auth] API-интерфейсы в учетных данных хранилища toosecurely **учетной записи** объекта.</span><span class="sxs-lookup"><span data-stu-id="36310-415">Xamarin    apps use hello [Xamarin.Auth] APIs toosecurely store credentials in an **Account** object.</span></span> <span data-ttu-id="36310-416">Пример использования этих интерфейсов API см. в разделе hello [AuthStore.cs] файл исходного кода в hello [совместное использование образец фото ContosoMoments](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="36310-416">For an example of using these APIs, see hello [AuthStore.cs] code file in hello [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="36310-417">При использовании управляемой клиентом проверки подлинности, также могут кэшироваться hello токен доступа, полученный от поставщика, например Facebook или Twitter.</span><span class="sxs-lookup"><span data-stu-id="36310-417">When you use client-managed authentication, you can also cache hello access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="36310-418">Этот токен может быть предоставленный toorequest новый маркер проверки подлинности из внутренней hello, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36310-418">This token can be supplied toorequest a new authentication token from hello backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="36310-419"><a name="pushnotifications"></a>Push-уведомления</span><span class="sxs-lookup"><span data-stu-id="36310-419"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="36310-420">Hello ниже описывается Push-уведомления:</span><span class="sxs-lookup"><span data-stu-id="36310-420">hello following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="36310-421">Регистрация для получения push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="36310-421">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="36310-422">Получение SID пакета Магазина Windows</span><span class="sxs-lookup"><span data-stu-id="36310-422">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="36310-423">Регистрация с помощью межплатформенных шаблонов</span><span class="sxs-lookup"><span data-stu-id="36310-423">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="36310-424"><a name="register-for-push"></a>Практическое руководство. Регистрация для получения push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="36310-424"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="36310-425">Клиент мобильные приложения Hello позволяет tooregister для push-уведомлений с концентраторами уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="36310-425">hello Mobile Apps client enables you tooregister for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="36310-426">При регистрации, можно получить дескриптор, который получен из hello платформой службы Push-уведомлений (PNS).</span><span class="sxs-lookup"><span data-stu-id="36310-426">When registering, you obtain a handle that you obtain from hello platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="36310-427">Затем укажите это значение вместе с любыми тегами, при создании регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="36310-427">You then provide this value along with any tags when you create hello registration.</span></span> <span data-ttu-id="36310-428">Hello следующий код регистрирует приложения Windows для push-уведомлений с hello Windows Notification Service (WNS):</span><span class="sxs-lookup"><span data-stu-id="36310-428">hello following code registers your Windows app for push notifications with hello Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="36310-429">При отправке tooWNS, необходимо [получить ИД безопасности пакета магазина Windows](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="36310-429">If you are pushing tooWNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="36310-430">Дополнительные сведения о приложениях Windows включая tooregister для регистрации шаблонов, см. в [уведомления tooyour добавить push приложения].</span><span class="sxs-lookup"><span data-stu-id="36310-430">For more information on Windows apps, including how tooregister for template registrations, see [Add push notifications tooyour app].</span></span>

<span data-ttu-id="36310-431">Запрос теги из hello клиента не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="36310-431">Requesting tags from hello client is not supported.</span></span>  <span data-ttu-id="36310-432">Запросы тегов автоматически отбрасываются из регистрации.</span><span class="sxs-lookup"><span data-stu-id="36310-432">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="36310-433">При желании tooregister устройства с тегами, создайте настраиваемый API, который использует hello API концентраторов уведомлений tooperform hello регистрации от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="36310-433">If you wish tooregister your device with tags, create a Custom API that uses hello Notification Hubs API tooperform hello registration on your behalf.</span></span>  <span data-ttu-id="36310-434">[Вызов пользовательского API hello](#customapi) вместо hello `RegisterNativeAsync()` метод.</span><span class="sxs-lookup"><span data-stu-id="36310-434">[Call hello Custom API](#customapi) instead of hello `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="36310-435"><a name="package-sid"></a>Практическое руководство. Получение SID пакета Магазина Windows</span><span class="sxs-lookup"><span data-stu-id="36310-435"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="36310-436">Для включения push-уведомлений для приложений Магазина Windows необходим SID пакета.</span><span class="sxs-lookup"><span data-stu-id="36310-436">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="36310-437">tooreceive пакета SID, зарегистрировать приложение в магазине Windows hello.</span><span class="sxs-lookup"><span data-stu-id="36310-437">tooreceive a package SID, register your application with hello Windows Store.</span></span>

<span data-ttu-id="36310-438">tooobtain это значение:</span><span class="sxs-lookup"><span data-stu-id="36310-438">tooobtain this value:</span></span>

1. <span data-ttu-id="36310-439">В обозревателе решений Visual Studio, щелкните правой кнопкой мыши проект приложения для магазина Windows hello, щелкните **хранилища** > **связать приложение с hello хранилища...** .</span><span class="sxs-lookup"><span data-stu-id="36310-439">In Visual Studio Solution Explorer, right-click hello Windows Store app project, click **Store** > **Associate App with hello Store...**.</span></span>
2. <span data-ttu-id="36310-440">В мастере приветствия щелкните **Далее**, войти в учетную запись Майкрософт, введите имя приложения в **зарезервировать новое имя приложения**, нажмите кнопку **резерва**.</span><span class="sxs-lookup"><span data-stu-id="36310-440">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="36310-441">После регистрации приложения hello hello успешно создан, выберите имя приложения, нажмите кнопку **Далее**, а затем нажмите кнопку **связать**.</span><span class="sxs-lookup"><span data-stu-id="36310-441">After hello app registration is successfully created, select hello app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="36310-442">Войдите в toohello [центра разработчиков Windows] с учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="36310-442">Log in toohello [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="36310-443">В разделе **Мои приложения**, нажмите кнопку регистрации приложения hello, вы создали.</span><span class="sxs-lookup"><span data-stu-id="36310-443">Under **My apps**, click hello app registration you created.</span></span>
5. <span data-ttu-id="36310-444">Нажмите кнопку **управления приложениями** > **удостоверение приложения**, а затем прокрутите экран вниз toofind вашей **ИД безопасности пакета**.</span><span class="sxs-lookup"><span data-stu-id="36310-444">Click **App management** > **App identity**, and then scroll down toofind your **Package SID**.</span></span>

<span data-ttu-id="36310-445">В большинстве случаев идентификатор безопасности пакета hello рассматривать его как универсальный код Ресурса, в этом случае необходимо toouse *ms-app: / /* как схему hello.</span><span class="sxs-lookup"><span data-stu-id="36310-445">Many uses of hello package SID treat it as a URI, in which case you need toouse *ms-app://* as hello scheme.</span></span> <span data-ttu-id="36310-446">Запишите hello версии пакета SID, полученная путем сцепления это значение в качестве префикса.</span><span class="sxs-lookup"><span data-stu-id="36310-446">Make note of hello version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="36310-447">Приложения Xamarin требуются некоторые возможности tooregister toobe дополнительный код приложение, запущенное на платформах hello iOS или Android.</span><span class="sxs-lookup"><span data-stu-id="36310-447">Xamarin apps require some additional code toobe able tooregister an app running on hello iOS or Android platforms.</span></span> <span data-ttu-id="36310-448">Дополнительные сведения см. в разделе hello для вашей платформы:</span><span class="sxs-lookup"><span data-stu-id="36310-448">For more information, see hello topic for your platform:</span></span>

* [<span data-ttu-id="36310-449">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="36310-449">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="36310-450">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="36310-450">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="36310-451"><a name="register-xplat"></a>Как: Register извещающих шаблоны toosend кросс платформенных уведомлений</span><span class="sxs-lookup"><span data-stu-id="36310-451"><a name="register-xplat"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="36310-452">шаблоны tooregister использовать hello `RegisterAsync()` метод hello шаблонов, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="36310-452">tooregister templates, use hello `RegisterAsync()` method with hello templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="36310-453">Шаблоны должны быть `JObject` типы и могут содержать несколько шаблонов в hello следующий формат JSON:</span><span class="sxs-lookup"><span data-stu-id="36310-453">Your templates should be `JObject` types and can contain multiple templates in hello following JSON format:</span></span>

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

<span data-ttu-id="36310-454">Здравствуйте, метод **RegisterAsync()** также принимает вторичной плитки:</span><span class="sxs-lookup"><span data-stu-id="36310-454">hello method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="36310-455">Во время регистрации все теги удаляются в целях безопасности.</span><span class="sxs-lookup"><span data-stu-id="36310-455">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="36310-456">теги tooadd tooinstallations или шаблоны в установках см. в разделе [работа с сервера базы данных hello .NET SDK для мобильных приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="36310-456">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="36310-457">Использование этих зарегистрированных шаблонов уведомлений toosend ссылаться toohello [API-интерфейсов концентраторы уведомлений].</span><span class="sxs-lookup"><span data-stu-id="36310-457">toosend notifications utilizing these registered templates, refer toohello [Notification Hubs APIs].</span></span>

## <span data-ttu-id="36310-458"><a name="misc"></a>Разное</span><span class="sxs-lookup"><span data-stu-id="36310-458"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="36310-459"><a name="errors"></a>Практическое руководство. Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="36310-459"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="36310-460">При возникновении ошибки в серверном приложении hello hello клиент вызывает SDK `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="36310-460">When an error occurs in hello backend, hello client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="36310-461">В следующем примере показан способ toohandle исключение, которое возвращается сервером hello:</span><span class="sxs-lookup"><span data-stu-id="36310-461">The following example shows how toohandle an exception that is returned by hello backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

<span data-ttu-id="36310-462">Еще один пример работы с состояниями ошибки можно найти в hello [пример файлов мобильных приложений].</span><span class="sxs-lookup"><span data-stu-id="36310-462">Another example of dealing with error conditions can be found in hello [Mobile Apps Files Sample].</span></span> <span data-ttu-id="36310-463">[LoggingHandler] пример предоставляет делегат ведения журнала обработчик toolog hello запросов toohello серверной части.</span><span class="sxs-lookup"><span data-stu-id="36310-463">The [LoggingHandler] example provides a logging delegate handler toolog hello requests being made toohello backend.</span></span>

### <span data-ttu-id="36310-464"><a name="headers"></a>Практическое руководство. Настройка заголовков запроса</span><span class="sxs-lookup"><span data-stu-id="36310-464"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="36310-465">toosupport в данном случае определенное приложение, может потребоваться toocustomize связь с внутреннего сервера мобильного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="36310-465">toosupport your specific app scenario, you might need toocustomize communication with hello Mobile App backend.</span></span> <span data-ttu-id="36310-466">Например вы можете требуется tooadd исходящего запроса с tooevery пользовательский заголовок или даже коды состояния ответов.</span><span class="sxs-lookup"><span data-stu-id="36310-466">For example, you may want tooadd a custom header tooevery outgoing request or even change responses status codes.</span></span> <span data-ttu-id="36310-467">Можно использовать пользовательский [DelegatingHandler], как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="36310-467">You can use a custom [DelegatingHandler], as in hello following example:</span></span>

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

[приложение tooyour authentication добавить]: app-service-mobile-windows-store-dotnet-get-started-users.md
[автономной синхронизации данных в мобильных приложениях Azure]: app-service-mobile-offline-data-sync.md
[уведомления tooyour добавить push приложения]: app-service-mobile-windows-store-dotnet-get-started-push.md
[регистрации вашего приложения toouse имя входа учетной записи Майкрософт]: app-service-mobile-how-to-configure-microsoft-authentication.md
[как tooconfigure приложения службы для имени входа Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[Функция GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[создает ссылочной таблице нетипизированного tooan]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[принимать]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[выберите]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[пропустить]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[где]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[портал Azure]: https://portal.azure.com/
[классический портал Azure]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[центра разработчиков Windows]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[пакета SDK Live Windows]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[API-интерфейсов концентраторы уведомлений]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[пример файлов мобильных приложений]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[документации OData v3]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
