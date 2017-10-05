---
title: "Работа с управляемой клиентской библиотекой мобильных приложений службы приложений (Windows) | Документация Майкрософт"
description: "Узнайте, как использовать клиент .NET для мобильных приложений службы приложений Azure с приложениями Windows и Xamarin."
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
ms.openlocfilehash: 5f4cc3e97ba7adde2aaac471951a3130d79910f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="9e600-103">Использование управляемого клиента для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9e600-103">How to use the managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="9e600-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="9e600-104">Overview</span></span>
<span data-ttu-id="9e600-105">В этом руководстве показано, как реализовать типичные сценарии с использованием управляемой клиентской библиотеки для мобильных приложений службы приложений Azure в приложениях Windows и Xamarin.</span><span class="sxs-lookup"><span data-stu-id="9e600-105">This guide shows you how to perform common scenarios using the managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="9e600-106">Если вы не знакомы с мобильными приложениями, рекомендуем сначала прочитать [краткое руководство по мобильным приложениям Azure][1].</span><span class="sxs-lookup"><span data-stu-id="9e600-106">If you are new to Mobile Apps, you should consider first completing the [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="9e600-107">В данном руководстве мы сосредоточимся на управляемом пакете SDK клиентской части.</span><span class="sxs-lookup"><span data-stu-id="9e600-107">In this guide, we focus on the client-side managed SDK.</span></span> <span data-ttu-id="9e600-108">Дополнительные сведения о серверных пакетах SDK для мобильных приложений см. в документации по [серверному пакету SDK для .NET][2] или [серверному пакету SDK для Node.js][3].</span><span class="sxs-lookup"><span data-stu-id="9e600-108">To learn more about the server-side SDKs for Mobile Apps, see the documentation for the [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="9e600-109">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="9e600-109">Reference documentation</span></span>
<span data-ttu-id="9e600-110">Справочная документация по клиентскому пакету SDK находится в [справочнике по клиенту мобильных приложений Azure для .NET][4].</span><span class="sxs-lookup"><span data-stu-id="9e600-110">The reference documentation for the client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="9e600-111">Несколько примеров клиентов доступно в [репозитории GitHub с примерами Azure][5].</span><span class="sxs-lookup"><span data-stu-id="9e600-111">You can also find several client samples in the [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="9e600-112">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="9e600-112">Supported Platforms</span></span>
<span data-ttu-id="9e600-113">Платформа .NET поддерживает следующие платформы:</span><span class="sxs-lookup"><span data-stu-id="9e600-113">The .NET Platform supports the following platforms:</span></span>

* <span data-ttu-id="9e600-114">выпуски Xamarin Android для API 19–24 (от KitKat до Nougat);</span><span class="sxs-lookup"><span data-stu-id="9e600-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="9e600-115">выпуски Xamarin iOS для iOS 8.0 и более поздних версий;</span><span class="sxs-lookup"><span data-stu-id="9e600-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="9e600-116">Универсальные приложения Windows</span><span class="sxs-lookup"><span data-stu-id="9e600-116">Universal Windows Platform</span></span>
* <span data-ttu-id="9e600-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="9e600-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="9e600-118">Windows Phone 8.0, за исключением приложений Silverlight.</span><span class="sxs-lookup"><span data-stu-id="9e600-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="9e600-119">"Серверная" аутентификация использует WebView для представляемого пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="9e600-119">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="9e600-120">Если устройство не может представить пользовательский интерфейс WebView, требуется применять другие способы аутентификации.</span><span class="sxs-lookup"><span data-stu-id="9e600-120">If the device is not able to present a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="9e600-121">Поэтому данный пакет SDK не подходит для различного рода часов и других устройств с аналогичными ограничениями.</span><span class="sxs-lookup"><span data-stu-id="9e600-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="9e600-122"><a name="setup"></a>Настройка и необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="9e600-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="9e600-123">Предполагается, что вы уже создали и опубликовали проект внутреннего сервера мобильных приложений, который содержит по меньшей мере одну таблицу.</span><span class="sxs-lookup"><span data-stu-id="9e600-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="9e600-124">В коде, который используется в этом разделе, применяется таблица `TodoItem`, которая содержит следующие столбцы: `Id`, `Text` и `Complete`.</span><span class="sxs-lookup"><span data-stu-id="9e600-124">In the code used in this topic, the table is named `TodoItem` and it has the following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="9e600-125">Это та же таблица, которая была создана при выполнении [краткого руководства по мобильным приложениям Azure][1].</span><span class="sxs-lookup"><span data-stu-id="9e600-125">This table is the same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="9e600-126">Соответствующий типизированный тип на стороне клиента является приведенным ниже классом в C#.</span><span class="sxs-lookup"><span data-stu-id="9e600-126">The corresponding typed client-side type in C# is the following class:</span></span>

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

<span data-ttu-id="9e600-127">Атрибут [JsonPropertyAttribute][6] используется для определения сопоставления *PropertyName* между полем клиента и таблицы.</span><span class="sxs-lookup"><span data-stu-id="9e600-127">The [JsonPropertyAttribute][6] is used to define the *PropertyName* mapping between the client field and the table field.</span></span>

<span data-ttu-id="9e600-128">Дополнительные сведения о создании таблиц в серверной части мобильных приложений см. в статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure][7] или [Использование пакета SDK Node.js для мобильных приложений Azure][8].</span><span class="sxs-lookup"><span data-stu-id="9e600-128">To learn how to create tables in your Mobile Apps backend, see the [.NET Server SDK topic][7] or the [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="9e600-129">При создании серверной части мобильного приложения на портале Azure с помощью краткого руководства можно использовать параметр **Простые таблицы** на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="9e600-129">If you created your Mobile App backend in the Azure portal using the QuickStart, you can also use the **Easy tables** setting in the [Azure portal].</span></span>

### <a name="how-to-install-the-managed-client-sdk-package"></a><span data-ttu-id="9e600-130">Практическое руководство. Установка пакета SDK для управляемого клиента</span><span class="sxs-lookup"><span data-stu-id="9e600-130">How to: Install the managed client SDK package</span></span>
<span data-ttu-id="9e600-131">Используйте один из следующих методов установки пакета SDK для управляемого клиента для мобильных приложений с сайта [NuGet][9].</span><span class="sxs-lookup"><span data-stu-id="9e600-131">Use one of the following methods to install the managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="9e600-132">**Visual Studio**. Щелкните правой кнопкой мыши свой проект, выберите пункт **Управление пакетами NuGet**, найдите пакет `Microsoft.Azure.Mobile.Client` и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="9e600-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="9e600-133">**Xamarin Studio**. Щелкните правой кнопкой мыши проект, выберите пункт **Добавить** > **Добавить пакеты NuGet**, найдите пакет `Microsoft.Azure.Mobile.Client ` и нажмите кнопку **Добавить пакет**.</span><span class="sxs-lookup"><span data-stu-id="9e600-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="9e600-134">В своем основном файле действий не забудьте добавить следующий оператор **using** .</span><span class="sxs-lookup"><span data-stu-id="9e600-134">In your main activity file, remember to add the following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="9e600-135"><a name="symbolsource"></a>Практическое руководство. Работа с отладочными символами в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e600-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="9e600-136">Символы для пространства имен Microsoft.Azure.Mobile доступны в [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="9e600-136">The symbols for the Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="9e600-137">Ознакомьтесь с [инструкциями по SymbolSource][11], чтобы интегрировать SymbolSource с Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e600-137">Refer to the [SymbolSource instructions][11] to integrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="9e600-138"><a name="create-client"></a>Создание клиента мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="9e600-138"><a name="create-client"></a>Create the Mobile Apps client</span></span>
<span data-ttu-id="9e600-139">Следующий код создает объект [MobileServiceClient][12], используемый для доступа к серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="9e600-139">The following code creates the [MobileServiceClient][12] object that is used to access your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="9e600-140">В приведенном выше коде замените `MOBILE_APP_URL` URL-адресом серверной части мобильного приложения, который можно найти в колонке серверной части мобильного приложения на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="9e600-140">In the preceding code, replace `MOBILE_APP_URL` with the URL of the Mobile App backend, which is found in the blade for your Mobile App backend in the [Azure portal].</span></span> <span data-ttu-id="9e600-141">Объект MobileServiceClient должен быть одноэлементным.</span><span class="sxs-lookup"><span data-stu-id="9e600-141">The MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="9e600-142">Работа с таблицами</span><span class="sxs-lookup"><span data-stu-id="9e600-142">Work with Tables</span></span>
<span data-ttu-id="9e600-143">Ниже подробно описано, как выполнить поиск, извлечение записей и изменение данных в таблице.</span><span class="sxs-lookup"><span data-stu-id="9e600-143">The following section details how to search and retrieve records and modify the data within the table.</span></span>  <span data-ttu-id="9e600-144">В этой статье рассматриваются следующие темы:</span><span class="sxs-lookup"><span data-stu-id="9e600-144">The following topics are covered:</span></span>

* [<span data-ttu-id="9e600-145">Создание ссылки на таблицу</span><span class="sxs-lookup"><span data-stu-id="9e600-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="9e600-146">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="9e600-146">Query data</span></span>](#querying)
* [<span data-ttu-id="9e600-147">Фильтрация возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="9e600-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="9e600-148">Сортировка возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="9e600-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="9e600-149">Возврат данных на страницах</span><span class="sxs-lookup"><span data-stu-id="9e600-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="9e600-150">Выбор определенных столбцов</span><span class="sxs-lookup"><span data-stu-id="9e600-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="9e600-151">Поиск записи по идентификатору</span><span class="sxs-lookup"><span data-stu-id="9e600-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="9e600-152">Работа с нетипизированными запросами</span><span class="sxs-lookup"><span data-stu-id="9e600-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="9e600-153">Вставка данных</span><span class="sxs-lookup"><span data-stu-id="9e600-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="9e600-154">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="9e600-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="9e600-155">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="9e600-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="9e600-156">Разрешение конфликтов и оптимистичный параллелизм</span><span class="sxs-lookup"><span data-stu-id="9e600-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="9e600-157">Привязка к пользовательскому интерфейсу Windows</span><span class="sxs-lookup"><span data-stu-id="9e600-157">Binding to a Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="9e600-158">Изменение размера страницы</span><span class="sxs-lookup"><span data-stu-id="9e600-158">Changing the Page Size</span></span>](#pagesize)

### <span data-ttu-id="9e600-159"><a name="instantiating"></a>Практическое руководство. Создание ссылки на таблицу</span><span class="sxs-lookup"><span data-stu-id="9e600-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="9e600-160">Весь код, который открывает или изменяет данные в таблице серверной части, вызывает функции для объекта `MobileServiceTable` .</span><span class="sxs-lookup"><span data-stu-id="9e600-160">All the code that accesses or modifies data in a backend table calls functions on the `MobileServiceTable` object.</span></span> <span data-ttu-id="9e600-161">Получите ссылку на таблицу, вызвав метод [GetTable] , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9e600-161">Obtain a reference to the table by calling the [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="9e600-162">Возвращаемый объект использует типизированную модель сериализации.</span><span class="sxs-lookup"><span data-stu-id="9e600-162">The returned object uses the typed serialization model.</span></span> <span data-ttu-id="9e600-163">Также поддерживается нетипизированная модель сериализации.</span><span class="sxs-lookup"><span data-stu-id="9e600-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="9e600-164">Следующий пример [создает ссылку на нетипизированную таблицу].</span><span class="sxs-lookup"><span data-stu-id="9e600-164">The following example [creates a reference to an untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="9e600-165">В нетипизированных запросах необходимо указать соответствующую строку запроса OData.</span><span class="sxs-lookup"><span data-stu-id="9e600-165">In untyped queries, you must specify the underlying OData query string.</span></span>

### <span data-ttu-id="9e600-166"><a name="querying"></a>Практическое руководство. Запрос данных из мобильного приложения</span><span class="sxs-lookup"><span data-stu-id="9e600-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="9e600-167">В этом разделе показано, как отправлять запросы к внутреннему серверу мобильных приложений. Описаны следующие функциональные возможности:</span><span class="sxs-lookup"><span data-stu-id="9e600-167">This section describes how to issue queries to the Mobile App backend, which includes the following functionality:</span></span>

* [<span data-ttu-id="9e600-168">Фильтрация возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="9e600-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="9e600-169">Сортировка возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="9e600-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="9e600-170">Возврат данных на страницах</span><span class="sxs-lookup"><span data-stu-id="9e600-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="9e600-171">Выбор определенных столбцов</span><span class="sxs-lookup"><span data-stu-id="9e600-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="9e600-172">Поиск данных по идентификатору</span><span class="sxs-lookup"><span data-stu-id="9e600-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="9e600-173">Для предотвращения возврата всех строк принудительно применяется размер страницы, управляемый сервером.</span><span class="sxs-lookup"><span data-stu-id="9e600-173">A server-driven page size is enforced to prevent all rows from being returned.</span></span>  <span data-ttu-id="9e600-174">Разбиение по страницам предотвращает негативное воздействие больших наборов данных на функционирование службы.</span><span class="sxs-lookup"><span data-stu-id="9e600-174">Paging keeps default requests for large data sets from negatively impacting the service.</span></span>  <span data-ttu-id="9e600-175">Для возвращения более 50 строк используйте методы `Skip` и `Take`, как описано в разделе [Возвращение данных на страницах](#paging).</span><span class="sxs-lookup"><span data-stu-id="9e600-175">To return more than 50 rows, use the `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="9e600-176"><a name="filtering"></a>Практическое руководство. Фильтрация возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="9e600-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="9e600-177">Следующий код иллюстрирует способ фильтрации данных путем включения предложения `Where` в запрос.</span><span class="sxs-lookup"><span data-stu-id="9e600-177">The following code illustrates how to filter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="9e600-178">Он возвращает все элементы таблицы `todoTable`, свойство `Complete` которых равно `false`.</span><span class="sxs-lookup"><span data-stu-id="9e600-178">It returns all items from `todoTable` whose `Complete` property is equal to `false`.</span></span> <span data-ttu-id="9e600-179">Функция [Where] применяет предикат фильтрации строк для запросов к таблице.</span><span class="sxs-lookup"><span data-stu-id="9e600-179">The [Where] function applies a row filtering predicate to the query against the table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="9e600-180">Универсальный код ресурса (URI) запроса, отправленного в серверную часть, можно просмотреть с помощью программы проверки сообщений, такой как средства разработчика браузера или [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="9e600-180">You can view the URI of the request sent to the backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="9e600-181">Если взглянуть на универсальный код ресурса (URI) запроса, можно отметить, что сама строка запроса изменена.</span><span class="sxs-lookup"><span data-stu-id="9e600-181">If you look at the request URI, notice that the query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="9e600-182">Этот запрос OData с помощью пакета SDK для сервера преобразуется в SQL-запрос.</span><span class="sxs-lookup"><span data-stu-id="9e600-182">This OData request is translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="9e600-183">Функция, которая передается в метод `Where` , может включать в себя произвольное число условий.</span><span class="sxs-lookup"><span data-stu-id="9e600-183">The function that is passed to the `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="9e600-184">Этот пример должен быть преобразован в SQL-запрос с помощью пакета SDK для сервера.</span><span class="sxs-lookup"><span data-stu-id="9e600-184">This example would be translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="9e600-185">Этот запрос также можно разбить на несколько предложений:</span><span class="sxs-lookup"><span data-stu-id="9e600-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="9e600-186">Эти два способа эквивалентны и могут быть взаимозаменяемыми.</span><span class="sxs-lookup"><span data-stu-id="9e600-186">The two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="9e600-187">Первый вариант — &mdash;объединение нескольких предикатов в одном запросе&mdash; — является более компактным и рекомендуемым.</span><span class="sxs-lookup"><span data-stu-id="9e600-187">The former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="9e600-188">Предложение `Where` поддерживает операции, которые будут преобразованы в подмножество OData.</span><span class="sxs-lookup"><span data-stu-id="9e600-188">The `Where` clause supports operations that be translated into the OData subset.</span></span> <span data-ttu-id="9e600-189">К этим операциям относятся:</span><span class="sxs-lookup"><span data-stu-id="9e600-189">Operations include:</span></span>

* <span data-ttu-id="9e600-190">операторы сравнения (==,! =, <, < =, >, > =);</span><span class="sxs-lookup"><span data-stu-id="9e600-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="9e600-191">арифметические операторы (+, -, /, *, %);</span><span class="sxs-lookup"><span data-stu-id="9e600-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="9e600-192">указание точности чисел (Math.Floor, Math.Ceiling);</span><span class="sxs-lookup"><span data-stu-id="9e600-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="9e600-193">строковые функции (Length, Substring, Replace, IndexOf, StartsWith, EndsWith);</span><span class="sxs-lookup"><span data-stu-id="9e600-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="9e600-194">свойства даты (Year, Month, Day, Hour, Minute, Second);</span><span class="sxs-lookup"><span data-stu-id="9e600-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="9e600-195">свойства доступа к объекту;</span><span class="sxs-lookup"><span data-stu-id="9e600-195">Access properties of an object, and</span></span>
* <span data-ttu-id="9e600-196">выражения, сочетающие в себе любые из этих операций.</span><span class="sxs-lookup"><span data-stu-id="9e600-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="9e600-197">Чтобы узнать, что поддерживает пакет SDK для сервера, обратитесь к [документации по OData версии 3].</span><span class="sxs-lookup"><span data-stu-id="9e600-197">When considering what the Server SDK supports, you can consider the [OData v3 Documentation].</span></span>

### <span data-ttu-id="9e600-198"><a name="sorting"></a>Практическое руководство. Сортировка возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="9e600-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="9e600-199">В следующем коде показано, как сортировать данные, включая в запрос функцию [OrderBy] или [OrderByDescending].</span><span class="sxs-lookup"><span data-stu-id="9e600-199">The following code illustrates how to sort data by including an [OrderBy] or [OrderByDescending] function in the query.</span></span> <span data-ttu-id="9e600-200">Он возвращает элементы таблицы `todoTable`, упорядочивая их по возрастанию значений в поле `Text`.</span><span class="sxs-lookup"><span data-stu-id="9e600-200">It returns items from `todoTable` sorted ascending by the `Text` field.</span></span>

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

### <span data-ttu-id="9e600-201"><a name="paging"></a>Практическое руководство. Возврат данных на страницах</span><span class="sxs-lookup"><span data-stu-id="9e600-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="9e600-202">По умолчанию внутренний сервер возвращает только первые 50 строк.</span><span class="sxs-lookup"><span data-stu-id="9e600-202">By default, the backend returns only the first 50 rows.</span></span> <span data-ttu-id="9e600-203">Число возвращенных строк можно увеличить путем вызова метода [Take] .</span><span class="sxs-lookup"><span data-stu-id="9e600-203">You can increase the number of returned rows by calling the [Take] method.</span></span> <span data-ttu-id="9e600-204">Чтобы запросить определенную "страницу" общего набора данных, возвращенного запросом, используйте метод `Take` вместе с методом [Skip] .</span><span class="sxs-lookup"><span data-stu-id="9e600-204">Use `Take` along with the [Skip] method to request a specific "page" of the total dataset returned by the query.</span></span> <span data-ttu-id="9e600-205">При выполнении следующего запроса будут возвращены три главных элемента в таблице.</span><span class="sxs-lookup"><span data-stu-id="9e600-205">The following query, when executed, returns the top three items in the table.</span></span>

```
// Define a filtered query that returns the top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="9e600-206">Следующий измененный запрос пропускает первые три результата и возвращает следующие три.</span><span class="sxs-lookup"><span data-stu-id="9e600-206">The following revised query skips the first three results and returns the next three results.</span></span> <span data-ttu-id="9e600-207">Данный запрос фактически выдает вторую "страницу" данных, где размер страницы составляет три элемента.</span><span class="sxs-lookup"><span data-stu-id="9e600-207">This query produces the second "page" of data, where the page size is three items.</span></span>

```
// Define a filtered query that skips the top 3 items and returns the next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="9e600-208">Метод [IncludeTotalCount] запрашивает общее количество *всех* записей, которые должны быть возвращены, без учета указанных предложений paging/limit.</span><span class="sxs-lookup"><span data-stu-id="9e600-208">The [IncludeTotalCount] method requests the total count for *all* the records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="9e600-209">В реальных приложениях можно использовать запросы, подобные вышеуказанным, с постраничным навигатором или другим совместимым пользовательским интерфейсом, позволяющим переходить между страницами.</span><span class="sxs-lookup"><span data-stu-id="9e600-209">In a real world app, you can use queries similar to the preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="9e600-210">Чтобы переопределить ограничение серверной части мобильного приложения в 50 строк, необходимо также применить класс [EnableQueryAttribute] к общедоступному методу GET и настроить разбиение по страницам.</span><span class="sxs-lookup"><span data-stu-id="9e600-210">To override the 50-row limit in a Mobile App backend, you must also apply the [EnableQueryAttribute] to the public GET method and specify the paging behavior.</span></span> <span data-ttu-id="9e600-211">В этом случае максимальное количество возвращаемых строк увеличивается до 1000:</span><span class="sxs-lookup"><span data-stu-id="9e600-211">When applied to the method, the following sets the maximum returned rows to 1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="9e600-212"><a name="selecting"></a>Практическое руководство. Выбор определенных столбцов</span><span class="sxs-lookup"><span data-stu-id="9e600-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="9e600-213">Набор свойств, который войдет в результаты, можно задать, добавив в запрос предложение [Select] .</span><span class="sxs-lookup"><span data-stu-id="9e600-213">You can specify which set of properties to include in the results by adding a [Select] clause to your query.</span></span> <span data-ttu-id="9e600-214">Например, в следующем коде показано, как выбрать только одно поле, а также способы выбора и форматирования нескольких полей:</span><span class="sxs-lookup"><span data-stu-id="9e600-214">For example, the following code shows how to select just one field and also how to select and format multiple fields:</span></span>

```
// Select one field -- just the Text
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

<span data-ttu-id="9e600-215">Все описанные функции являются аддитивными, поэтому мы можем создавать из них цепочки.</span><span class="sxs-lookup"><span data-stu-id="9e600-215">All the functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="9e600-216">Каждый последующий цепной вызов все больше влияет на запрос.</span><span class="sxs-lookup"><span data-stu-id="9e600-216">Each chained call affects more of the query.</span></span> <span data-ttu-id="9e600-217">Еще один пример:</span><span class="sxs-lookup"><span data-stu-id="9e600-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="9e600-218"><a name="lookingup"></a>Практическое руководство. Поиск данных по идентификатору</span><span class="sxs-lookup"><span data-stu-id="9e600-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="9e600-219">Функцию [LookupAsync] можно использовать для поиска в базе данных объектов с определенным идентификатором.</span><span class="sxs-lookup"><span data-stu-id="9e600-219">The [LookupAsync] function can be used to look up objects from the database with a particular ID.</span></span>

```
// This query filters out the item with the ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="9e600-220"><a name="untypedqueries"></a>Практическое руководство. Выполнение нетипизированных запросов</span><span class="sxs-lookup"><span data-stu-id="9e600-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="9e600-221">При выполнении запроса с помощью объекта нетипизированной таблицы необходимо явно указать строку запроса OData, вызвав функцию [ReadAsync], как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="9e600-221">When executing a query using an untyped table object, you must explicitly specify the OData query string by calling [ReadAsync], as in the following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="9e600-222">Вы будете получать значения JSON, которые можно использовать в качестве контейнера свойств.</span><span class="sxs-lookup"><span data-stu-id="9e600-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="9e600-223">Более подробные сведения о JToken и Newtonsoft Json.NET см. на сайте [Json.NET].</span><span class="sxs-lookup"><span data-stu-id="9e600-223">For more information on JToken and Newtonsoft Json.NET, see the [Json.NET] site.</span></span>

### <span data-ttu-id="9e600-224"><a name="inserting"></a>Практическое руководство. Вставка данных в серверную часть мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="9e600-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="9e600-225">Все типы клиентов должны содержать член с именем **Id**(идентификатор), который по умолчанию является строкой.</span><span class="sxs-lookup"><span data-stu-id="9e600-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="9e600-226">Этот **идентификатор** необходим для выполнения операций CRUD и автономной синхронизации.</span><span class="sxs-lookup"><span data-stu-id="9e600-226">This **Id** is required to perform CRUD operations and for offline sync.</span></span> <span data-ttu-id="9e600-227">В следующем коде показано, как вставить новые строки в таблицу с помощью метода [InsertAsync] .</span><span class="sxs-lookup"><span data-stu-id="9e600-227">The following code illustrates how to use the [InsertAsync] method to insert new rows into a table.</span></span> <span data-ttu-id="9e600-228">Параметр содержит данные, которые вставляются в качестве объекта .NET.</span><span class="sxs-lookup"><span data-stu-id="9e600-228">The parameter contains the data to be inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="9e600-229">Если при вставке в `todoItem` не добавлено значение уникального пользовательского идентификатора, то GUID создается сервером.</span><span class="sxs-lookup"><span data-stu-id="9e600-229">If a unique custom ID value is not included in the `todoItem` during an insert, a GUID is generated by the server.</span></span>
<span data-ttu-id="9e600-230">Созданный идентификатор можно получить, проверив объект после возвращения вызова.</span><span class="sxs-lookup"><span data-stu-id="9e600-230">You can retrieve the generated Id by inspecting the object after the call returns.</span></span>

<span data-ttu-id="9e600-231">Для вставки нетипизированных данных можно использовать Json.NET.</span><span class="sxs-lookup"><span data-stu-id="9e600-231">To insert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="9e600-232">Вот пример использования электронного адреса в качестве уникального строкового идентификатора.</span><span class="sxs-lookup"><span data-stu-id="9e600-232">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="9e600-233">Работа со значениями идентификаторов</span><span class="sxs-lookup"><span data-stu-id="9e600-233">Working with ID values</span></span>
<span data-ttu-id="9e600-234">Мобильные приложения поддерживают уникальные настраиваемые строковые значения для столбца **Id** таблицы.</span><span class="sxs-lookup"><span data-stu-id="9e600-234">Mobile Apps supports unique custom string values for the table's **id** column.</span></span> <span data-ttu-id="9e600-235">Строковое значение позволяет приложениям использовать в качестве идентификатора настраиваемые значения, такие как электронные адреса или имена пользователей.</span><span class="sxs-lookup"><span data-stu-id="9e600-235">A string value allows applications to use custom values such as email addresses or user names for the ID.</span></span>  <span data-ttu-id="9e600-236">Строковые идентификаторы предоставляют следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="9e600-236">String IDs provide you with the following benefits:</span></span>

* <span data-ttu-id="9e600-237">Идентификаторы создаются без обмена данными с базой данных.</span><span class="sxs-lookup"><span data-stu-id="9e600-237">IDs are generated without making a round trip to the database.</span></span>
* <span data-ttu-id="9e600-238">Можно легко объединять записи из разных таблиц или баз данных.</span><span class="sxs-lookup"><span data-stu-id="9e600-238">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="9e600-239">Значения идентификаторов можно удобно интегрировать с логикой приложения.</span><span class="sxs-lookup"><span data-stu-id="9e600-239">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="9e600-240">Если для вставленной записи не задано значение строкового идентификатора, внутренний сервер мобильных приложений создает уникальное значение для идентификатора.</span><span class="sxs-lookup"><span data-stu-id="9e600-240">When a string ID value is not set on an inserted record, the Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="9e600-241">Для создания собственных значений идентификатора в клиенте или серверной части можно использовать метод [Guid.NewGuid] .</span><span class="sxs-lookup"><span data-stu-id="9e600-241">You can use the [Guid.NewGuid] method to generate your own ID values, either on the client or in the backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="9e600-242"><a name="modifying"></a>Практическое руководство. Изменение данных в серверной части мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="9e600-242"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="9e600-243">Следующий код показывает, как обновить существующую запись с тем же идентификатором с помощью метода [UpdateAsync] .</span><span class="sxs-lookup"><span data-stu-id="9e600-243">The following code illustrates how to use the [UpdateAsync] method to update an existing record with the same ID with new information.</span></span> <span data-ttu-id="9e600-244">Параметр содержит данные, которые обновляются в качестве объекта .NET.</span><span class="sxs-lookup"><span data-stu-id="9e600-244">The parameter contains the data to be updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="9e600-245">Для обновления нетипизированных данных можно использовать [Json.NET] следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9e600-245">To update untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="9e600-246">При выполнении обновления необходимо указать поле `id` .</span><span class="sxs-lookup"><span data-stu-id="9e600-246">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="9e600-247">Серверная часть использует поле `id` , чтобы определить, какую из строк нужно обновить.</span><span class="sxs-lookup"><span data-stu-id="9e600-247">The backend uses the `id` field to identify which row to update.</span></span> <span data-ttu-id="9e600-248">Поле `id` можно получить из результатов вызова метода `InsertAsync`.</span><span class="sxs-lookup"><span data-stu-id="9e600-248">The `id` field can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="9e600-249">При попытке обновить элемент без указания значения `id` порождается исключение `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="9e600-249">An `ArgumentException` is raised if you try to update an item without providing the `id` value.</span></span>

### <span data-ttu-id="9e600-250"><a name="deleting"></a>Практическое руководство. Удаление данных в серверной части мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="9e600-250"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="9e600-251">Следующий код показывает, как удалить существующий экземпляр с помощью метода [DeleteAsync] .</span><span class="sxs-lookup"><span data-stu-id="9e600-251">The following code illustrates how to use the [DeleteAsync] method to delete an existing instance.</span></span> <span data-ttu-id="9e600-252">Экземпляр идентифицируется по полю `id`, заданному в свойстве `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="9e600-252">The instance is identified by the `id` field set on the `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="9e600-253">Для удаления нетипизированных данных можно использовать Json.NET следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9e600-253">To delete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="9e600-254">При создании запроса на удаление необходимо указать идентификатор.</span><span class="sxs-lookup"><span data-stu-id="9e600-254">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="9e600-255">Другие свойства не передаются в службу или игнорируются ею.</span><span class="sxs-lookup"><span data-stu-id="9e600-255">Other properties are not passed to the service or are ignored at the service.</span></span> <span data-ttu-id="9e600-256">В результате вызова функции `DeleteAsync` обычно возвращается значение `null`.</span><span class="sxs-lookup"><span data-stu-id="9e600-256">The result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="9e600-257">Идентификатор для передачи можно получить в результате вызова метода `InsertAsync` .</span><span class="sxs-lookup"><span data-stu-id="9e600-257">The ID to pass in can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="9e600-258">При попытке удалить элемент без указания поля `id` порождается исключение `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="9e600-258">A `MobileServiceInvalidOperationException` is thrown when you try to delete an item without specifying the `id` field.</span></span>

### <span data-ttu-id="9e600-259"><a name="optimisticconcurrency"></a>Практическое руководство. Использование оптимистичного параллелизма для устранения конфликтов</span><span class="sxs-lookup"><span data-stu-id="9e600-259"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="9e600-260">Иногда два и более клиентов могут одновременно записывать изменения в один и тот же элемент.</span><span class="sxs-lookup"><span data-stu-id="9e600-260">Two or more clients may write changes to the same item at the same time.</span></span> <span data-ttu-id="9e600-261">Без механизма определения конфликтов последняя операция записи переписывала бы любые предыдущие обновления.</span><span class="sxs-lookup"><span data-stu-id="9e600-261">Without conflict detection, the last write would overwrite any previous updates.</span></span> <span data-ttu-id="9e600-262">**управлении оптимистичным параллелизмом** предполагается, что каждая транзакция может фиксироваться, поэтому не использует блокировки каких-либо ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9e600-262">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="9e600-263">Перед фиксацией транзакции управление оптимистичным параллелизмом проверяет, что никакие другие транзакции не изменили данные.</span><span class="sxs-lookup"><span data-stu-id="9e600-263">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified the data.</span></span> <span data-ttu-id="9e600-264">Если данные были изменены, фиксирующая транзакция откатывается.</span><span class="sxs-lookup"><span data-stu-id="9e600-264">If the data has been modified, the committing transaction is rolled back.</span></span>

<span data-ttu-id="9e600-265">Мобильные приложения поддерживают управление оптимистичным параллелизмом за счет отслеживания изменений в каждом элементе с помощью столбца системных свойств `version` , определенного для каждой таблицы в серверной части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="9e600-265">Mobile Apps supports optimistic concurrency control by tracking changes to each item using the `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="9e600-266">При каждом обновлении записи мобильные приложения задают новое значение свойства `version` для этой записи.</span><span class="sxs-lookup"><span data-stu-id="9e600-266">Each time a record is updated, Mobile Apps sets the `version` property for that record to a new value.</span></span> <span data-ttu-id="9e600-267">При обработке каждого запроса на обновление свойство `version` записи, включенное в запрос, сравнивается с тем же свойством записи на сервере.</span><span class="sxs-lookup"><span data-stu-id="9e600-267">During each update request, the `version` property of the record included with the request is compared to the same property for the record on the server.</span></span> <span data-ttu-id="9e600-268">Если версия, переданная с запросом, не соответствует серверной части, то клиентская библиотека порождает исключение `MobileServicePreconditionFailedException<T>` .</span><span class="sxs-lookup"><span data-stu-id="9e600-268">If the version passed with the request does not match the backend, then the client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="9e600-269">Тип, включенный в исключение, является записью серверной части, которая содержит версию записи на сервере.</span><span class="sxs-lookup"><span data-stu-id="9e600-269">The type included with the exception is the record from the backend containing the servers version of the record.</span></span> <span data-ttu-id="9e600-270">Затем приложение может использовать эти данные, чтобы решить, следует ли повторно выполнить полученный из серверной части запрос изменения с правильным значением `version` для фиксации изменений.</span><span class="sxs-lookup"><span data-stu-id="9e600-270">The application can then use this information to decide whether to execute the update request again with the correct `version` value from the backend to commit changes.</span></span>

<span data-ttu-id="9e600-271">Чтобы включить оптимистичный параллелизм, определите столбец в классе таблицы для системного свойства `version` .</span><span class="sxs-lookup"><span data-stu-id="9e600-271">Define a column on the table class for the `version` system property to enable optimistic concurrency.</span></span> <span data-ttu-id="9e600-272">Например:</span><span class="sxs-lookup"><span data-stu-id="9e600-272">For example:</span></span>

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

<span data-ttu-id="9e600-273">Приложения, в которых используются нетипизированные таблицы, включают оптимистичный параллелизм, устанавливая флаг `Version` в таблице `SystemProperties` следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9e600-273">Applications using untyped tables enable optimistic concurrency by setting the `Version` flag on the `SystemProperties` of the table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="9e600-274">Наряду с включением оптимистичного параллелизма при вызове [UpdateAsync] также необходимо перехватывать исключение `MobileServicePreconditionFailedException<T>` в коде.</span><span class="sxs-lookup"><span data-stu-id="9e600-274">In addition to enabling optimistic concurrency, you must also catch the `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="9e600-275">Разрешите конфликт, применив правильный `version` к обновленной записи и вызвав [UpdateAsync] с разрешенной записью.</span><span class="sxs-lookup"><span data-stu-id="9e600-275">Resolve the conflict by applying the correct `version` to the updated record and call [UpdateAsync] with the resolved record.</span></span> <span data-ttu-id="9e600-276">В следующем коде показано, как разрешить конфликт записи после его обнаружения:</span><span class="sxs-lookup"><span data-stu-id="9e600-276">The following code shows how to resolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at the remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, the item has changed since the last query
        // Resolve the conflict between the local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user to choose the resoltion between versions
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
        // To resolve the conflict, update the version of the item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while the user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="9e600-277">Дополнительные сведения см. в разделе [Автономная синхронизация данных в мобильных приложениях Azure].</span><span class="sxs-lookup"><span data-stu-id="9e600-277">For more information, see the [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="9e600-278"><a name="binding"></a>Практическое руководство. Привязка данных мобильных приложений к пользовательскому интерфейсу Windows</span><span class="sxs-lookup"><span data-stu-id="9e600-278"><a name="binding"></a>How to: Bind Mobile Apps data to a Windows user interface</span></span>
<span data-ttu-id="9e600-279">В этом разделе показано, как отображать возвращенные объекты данных с использованием элементов пользовательского интерфейса в приложении Windows.</span><span class="sxs-lookup"><span data-stu-id="9e600-279">This section shows how to display returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="9e600-280">Следующий пример кода осуществляет привязку к источнику списка с помощью запроса незавершенных элементов.</span><span class="sxs-lookup"><span data-stu-id="9e600-280">The following example code binds to the source of the list with a query for incomplete items.</span></span> <span data-ttu-id="9e600-281">При использовании [MobileServiceCollection] создается коллекция привязок, поддерживающих мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="9e600-281">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound to a UI list control
IEnumerable itemsControl  = items;

// Bind this to a ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="9e600-282">Некоторые элементы управления в управляемой среде выполнения Windows поддерживают интерфейс [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="9e600-282">Some controls in the managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="9e600-283">Этот интерфейс позволяет элементам управления запрашивать дополнительные данные во время прокрутки, выполняемой пользователем.</span><span class="sxs-lookup"><span data-stu-id="9e600-283">This interface allows controls to request extra data when the user scrolls.</span></span> <span data-ttu-id="9e600-284">Предусмотрена встроенная поддержка этого интерфейса для универсальных приложений Windows через коллекцию [MobileServiceIncrementalLoadingCollection], которая автоматически обрабатывает вызовы от элементов управления.</span><span class="sxs-lookup"><span data-stu-id="9e600-284">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from the controls.</span></span> <span data-ttu-id="9e600-285">Используйте `MobileServiceIncrementalLoadingCollection` в приложениях для Windows, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9e600-285">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="9e600-286">Чтобы использовать новую коллекцию в приложениях для Windows Phone 8 и Silverlight, используйте методы расширения `ToCollection` в интерфейсах `IMobileServiceTableQuery<T>` и `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="9e600-286">To use the new collection on Windows Phone 8 and "Silverlight" apps, use the `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="9e600-287">Для загрузки данных вызовите `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="9e600-287">To load data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="9e600-288">При использовании коллекции, созданной вызовом метода `ToCollectionAsync` или `ToCollection`, вы получите коллекцию, которую можно привязать к элементам управления пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="9e600-288">When you use the collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound to UI controls.</span></span>  <span data-ttu-id="9e600-289">Эта коллекция поддерживает разбиение по страницам.</span><span class="sxs-lookup"><span data-stu-id="9e600-289">This collection is paging-aware.</span></span>  <span data-ttu-id="9e600-290">Так как коллекция загружает данные из сети, иногда происходит сбой загрузки.</span><span class="sxs-lookup"><span data-stu-id="9e600-290">Since the collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="9e600-291">Чтобы обработать подобные ошибки, переопределите метод `OnException` в классе `MobileServiceIncrementalLoadingCollection` для обработки исключений, возникающих в результате вызова метода `LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="9e600-291">To handle such failures, override the `OnException` method on `MobileServiceIncrementalLoadingCollection` to handle exceptions resulting from calls to `LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="9e600-292">Представьте, что в таблице есть множество полей, однако необходимо отобразить только те из них, которыми вам нужно управлять.</span><span class="sxs-lookup"><span data-stu-id="9e600-292">Consider if your table has many fields but you only want to display some of them in your control.</span></span> <span data-ttu-id="9e600-293">С помощью инструкций в разделе[Выбор конкретных столбцов](#selecting)выше можно выбрать столбцы, отображаемые в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="9e600-293">You may use the guidance in the preceding section "[Select specific columns](#selecting)" to select specific columns to display in the UI.</span></span>

### <span data-ttu-id="9e600-294"><a name="pagesize"></a>Изменение размера страницы</span><span class="sxs-lookup"><span data-stu-id="9e600-294"><a name="pagesize"></a>Change the Page size</span></span>
<span data-ttu-id="9e600-295">По умолчанию мобильные приложения Azure выдают не больше 50 элементов на запрос.</span><span class="sxs-lookup"><span data-stu-id="9e600-295">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="9e600-296">Можно изменить параметры разбиения по страницам, увеличив максимальный размер страницы для клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="9e600-296">You can change the paging size by increasing the maximum page size on both the client and server.</span></span>  <span data-ttu-id="9e600-297">Чтобы увеличить размер запрошенной страницы, при использовании `PullAsync()` укажите `PullOptions`.</span><span class="sxs-lookup"><span data-stu-id="9e600-297">To increase the requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="9e600-298">Предположим, мы установили на сервере значение `PageSize`, равное или большее 100. Тогда каждый запрос будет возвращать до 100 элементов.</span><span class="sxs-lookup"><span data-stu-id="9e600-298">Assuming you have made the `PageSize` equal to or greater than 100 within the server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="9e600-299"><a name="#offlinesync"></a>Работа с автономными таблицами</span><span class="sxs-lookup"><span data-stu-id="9e600-299"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="9e600-300">Автономные таблицы используют локальное хранилище SQLite для хранения данных, которые могут использоваться в режиме "вне сети".</span><span class="sxs-lookup"><span data-stu-id="9e600-300">Offline tables use a local SQLite store to store data for use when offline.</span></span>  <span data-ttu-id="9e600-301">Во всех операциях с таблицами используется локальное хранилище SQLite, а не хранилище удаленного сервера.</span><span class="sxs-lookup"><span data-stu-id="9e600-301">All table operations are done against the local SQLite store instead of the remote server store.</span></span>  <span data-ttu-id="9e600-302">Чтобы создать автономную таблицу, сначала необходимо подготовить проект.</span><span class="sxs-lookup"><span data-stu-id="9e600-302">To create an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="9e600-303">В Visual Studio щелкните правой кнопкой мыши решение, выберите пункт **Управление пакетами NuGet для решения…**, а затем найдите и установите пакет NuGet **Microsoft.Azure.Mobile.Client.SQLiteStore** для всех проектов в решении.</span><span class="sxs-lookup"><span data-stu-id="9e600-303">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="9e600-304">(Необязательный шаг.) Чтобы обеспечить поддержку устройств Windows, установите один из следующих пакетов среды выполнения SQLite:</span><span class="sxs-lookup"><span data-stu-id="9e600-304">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="9e600-305">**Среда выполнения Windows 8.1**: установите [SQLite для Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="9e600-305">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="9e600-306">**Windows Phone 8.1**: установите [SQLite для Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="9e600-306">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="9e600-307">**Универсальная платформа Windows**: установите [SQLite для универсальной платформы Windows][5].</span><span class="sxs-lookup"><span data-stu-id="9e600-307">**Universal Windows Platform** Install [SQLite for the Universal Windows][5].</span></span>
3. <span data-ttu-id="9e600-308">(необязательно).</span><span class="sxs-lookup"><span data-stu-id="9e600-308">(Optional).</span></span> <span data-ttu-id="9e600-309">Для устройств с Windows щелкните правой кнопкой мыши **Ссылки** > **Добавить ссылку…**, разверните папку **Windows** > **Расширения**, а затем включите соответствующий пакет SDK **SQLite для Windows** и пакет SDK **среды выполнения Visual C++ 2013 для Windows**.</span><span class="sxs-lookup"><span data-stu-id="9e600-309">For Windows devices, click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**, then enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="9e600-310">Имена пакетов SDK для SQLite немного отличаются в зависимости от версии платформы Windows.</span><span class="sxs-lookup"><span data-stu-id="9e600-310">The SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="9e600-311">Перед созданием ссылки на таблицу необходимо подготовить локальное хранилище.</span><span class="sxs-lookup"><span data-stu-id="9e600-311">Before a table reference can be created, the local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes the SyncContext using the default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="9e600-312">Обычно хранилище инициализируется сразу же после создания клиента.</span><span class="sxs-lookup"><span data-stu-id="9e600-312">Store initialization is normally done immediately after the client is created.</span></span>  <span data-ttu-id="9e600-313">Значением **OfflineDbPath** должно быть имя файла, подходящее для всех платформ, которые вы поддерживаете.</span><span class="sxs-lookup"><span data-stu-id="9e600-313">The **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="9e600-314">Если указан полный путь (то есть начинающийся с косой черты), то используется он.</span><span class="sxs-lookup"><span data-stu-id="9e600-314">If the path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="9e600-315">Если путь не полный, то файл помещается в расположение для конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="9e600-315">If the path is not fully qualified, the file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="9e600-316">Для устройств iOS и Android по умолчанию выбрана папка Personal Files.</span><span class="sxs-lookup"><span data-stu-id="9e600-316">For iOS and Android devices, the default path is the "Personal Files" folder.</span></span>
* <span data-ttu-id="9e600-317">Для устройств с Windows по умолчанию выбрана папка AppData конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="9e600-317">For Windows devices, the default path is the application-specific "AppData" folder.</span></span>

<span data-ttu-id="9e600-318">Ссылку на таблицу можно получить с помощью метода `GetSyncTable<>`.</span><span class="sxs-lookup"><span data-stu-id="9e600-318">A table reference can be obtained using the `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="9e600-319">Для использования автономной таблицы не обязательно проходить аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="9e600-319">You do not need to authenticate to use an offline table.</span></span>  <span data-ttu-id="9e600-320">Ее необходимо проходить только при обмене данными с внутренней службой.</span><span class="sxs-lookup"><span data-stu-id="9e600-320">You only need to authenticate when you are communicating with the backend service.</span></span>

### <span data-ttu-id="9e600-321"><a name="syncoffline"></a>Синхронизация автономной таблицы</span><span class="sxs-lookup"><span data-stu-id="9e600-321"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="9e600-322">По умолчанию автономные таблицы не синхронизируются с серверной частью.</span><span class="sxs-lookup"><span data-stu-id="9e600-322">Offline tables are not synchronized with the backend by default.</span></span>  <span data-ttu-id="9e600-323">Синхронизация происходит в два этапа.</span><span class="sxs-lookup"><span data-stu-id="9e600-323">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="9e600-324">Можно передавать изменения отдельно от скачивания новых элементов.</span><span class="sxs-lookup"><span data-stu-id="9e600-324">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="9e600-325">Ниже приведен типичный метод синхронизации.</span><span class="sxs-lookup"><span data-stu-id="9e600-325">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //The first parameter is a query name that is used internally by the client SDK to implement incremental sync.
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

    // Simple error/conflict handling. A real application would handle the various errors like network conditions,
    // server conflicts and others via the IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting to server's copy.
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

<span data-ttu-id="9e600-326">Если первый аргумент для `PullAsync` имеет значение NULL, то добавочная синхронизация не используется.</span><span class="sxs-lookup"><span data-stu-id="9e600-326">If the first argument to `PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="9e600-327">Каждая операция синхронизации извлекает все записи.</span><span class="sxs-lookup"><span data-stu-id="9e600-327">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="9e600-328">Пакет SDK выполняет неявную операцию `PushAsync()` перед извлечением записей.</span><span class="sxs-lookup"><span data-stu-id="9e600-328">The SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="9e600-329">Обработка конфликтов происходит в методе `PullAsync()`.</span><span class="sxs-lookup"><span data-stu-id="9e600-329">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="9e600-330">Конфликты можно обработать таким же образом, как для таблиц в сети.</span><span class="sxs-lookup"><span data-stu-id="9e600-330">You can deal with conflicts in the same way as online tables.</span></span>  <span data-ttu-id="9e600-331">Конфликт возникает, когда во время вставки, обновления или удаления вызывается `PullAsync()`.</span><span class="sxs-lookup"><span data-stu-id="9e600-331">The conflict is produced when `PullAsync()` is called instead of during the insert, update, or delete.</span></span> <span data-ttu-id="9e600-332">Если возникает несколько конфликтов, они объединяются в одно исключение MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="9e600-332">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="9e600-333">Каждая ошибка должна обрабатываться отдельно.</span><span class="sxs-lookup"><span data-stu-id="9e600-333">Handle each failure separately.</span></span>

## <span data-ttu-id="9e600-334"><a name="#customapi"></a>Работа с настраиваемым API</span><span class="sxs-lookup"><span data-stu-id="9e600-334"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="9e600-335">Настраиваемый интерфейс API позволяет определить пользовательские конечные точки, которые предоставляют функциональные возможности сервера, не сопоставляемые с операциями вставки, обновления, удаления или чтения.</span><span class="sxs-lookup"><span data-stu-id="9e600-335">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="9e600-336">При использовании настраиваемого интерфейса API вы получаете больше возможностей для управления сообщениями, в том числе для чтения и установки заголовков HTTP-сообщений, а также определения форматов текста сообщений, отличных от JSON.</span><span class="sxs-lookup"><span data-stu-id="9e600-336">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="9e600-337">Настраиваемый API можно вызвать путем вызова одного из методов [InvokeApiAsync] для клиента.</span><span class="sxs-lookup"><span data-stu-id="9e600-337">You call a custom API by calling one of the [InvokeApiAsync] methods on the client.</span></span> <span data-ttu-id="9e600-338">Например, следующая строка кода отправляет запрос POST API-интерфейсу **completeAll** в серверную часть:</span><span class="sxs-lookup"><span data-stu-id="9e600-338">For example, the following line of code sends a POST request to the **completeAll** API on the backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="9e600-339">Это вызов типизированного метода, для которого требуется определить тип возвращаемого значения **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="9e600-339">This form is a typed method call and requires that the **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="9e600-340">Поддерживаются типизированные и нетипизированные методы.</span><span class="sxs-lookup"><span data-stu-id="9e600-340">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="9e600-341">Метод InvokeApiAsync() добавляет /api/ к имени API, к которому нужно совершить вызов, если имя API не начинается с "/".</span><span class="sxs-lookup"><span data-stu-id="9e600-341">The InvokeApiAsync() method prepends '/api/' to the API that you wish to call unless the API starts with a '/'.</span></span>
<span data-ttu-id="9e600-342">Например:</span><span class="sxs-lookup"><span data-stu-id="9e600-342">For example:</span></span>

* <span data-ttu-id="9e600-343">`InvokeApiAsync("completeAll",...)` вызывает /api/completeAll на сервере.</span><span class="sxs-lookup"><span data-stu-id="9e600-343">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on the backend</span></span>
* <span data-ttu-id="9e600-344">`InvokeApiAsync("/.auth/me",...)` вызывает /.auth/me на сервере.</span><span class="sxs-lookup"><span data-stu-id="9e600-344">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on the backend</span></span>

<span data-ttu-id="9e600-345">InvokeApiAsync можно использовать для вызова любого веб-API, включая веб-API, не определенные с помощью мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="9e600-345">You can use InvokeApiAsync to call any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="9e600-346">При использовании InvokeApiAsync() в запросе отправляются соответствующие заголовки, включая заголовки аутентификации.</span><span class="sxs-lookup"><span data-stu-id="9e600-346">When you use InvokeApiAsync(), the appropriate headers, including authentication headers, are sent with the request.</span></span>

## <span data-ttu-id="9e600-347"><a name="authentication"></a>Аутентификация пользователей</span><span class="sxs-lookup"><span data-stu-id="9e600-347"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="9e600-348">Мобильные приложения поддерживают аутентификацию и авторизацию пользователей с помощью различных внешних поставщиков удостоверений: Facebook, Google, учетной записи Майкрософт, Twitter и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9e600-348">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="9e600-349">Можно задать разрешения таблиц, чтобы предоставить доступ к определенным операциям только пользователям, прошедшим проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="9e600-349">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="9e600-350">Удостоверения пользователей, прошедших проверку подлинности, также можно применять для реализации правил авторизации в серверных скриптах.</span><span class="sxs-lookup"><span data-stu-id="9e600-350">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="9e600-351">Дополнительные сведения см. в учебнике [Добавление проверки подлинности в приложение].</span><span class="sxs-lookup"><span data-stu-id="9e600-351">For more information, see the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="9e600-352">Поддерживаются два потока аутентификации: *управляемой клиентом* и *управляемый сервером*.</span><span class="sxs-lookup"><span data-stu-id="9e600-352">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="9e600-353">Управляемый сервером поток обеспечивает самый простой способ аутентификации, так как он использует веб-интерфейс аутентификации.</span><span class="sxs-lookup"><span data-stu-id="9e600-353">The server-managed flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="9e600-354">Управляемый клиентом поток обеспечивает более тесную интеграцию с возможностями устройства, так как использует пакеты SDK конкретного поставщика для конкретного устройства.</span><span class="sxs-lookup"><span data-stu-id="9e600-354">The client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="9e600-355">Мы рекомендуем использовать в рабочих приложениях поток, управляемый клиентом.</span><span class="sxs-lookup"><span data-stu-id="9e600-355">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="9e600-356">Чтобы настроить аутентификацию, следует зарегистрировать приложение в одном или нескольких поставщиках удостоверений.</span><span class="sxs-lookup"><span data-stu-id="9e600-356">To set up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="9e600-357">Поставщик удостоверений создаст идентификатор клиента и секрет клиента для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="9e600-357">The identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="9e600-358">Затем эти значения задаются в серверной части и используются для аутентификации и авторизации в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="9e600-358">These values are then set in your backend to enable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="9e600-359">Дополнительные сведения приведены в руководстве [Добавление проверки подлинности в приложение].</span><span class="sxs-lookup"><span data-stu-id="9e600-359">For more information, follow the detailed instructions in the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="9e600-360">В этом разделе рассматриваются следующие темы.</span><span class="sxs-lookup"><span data-stu-id="9e600-360">The following topics are covered in this section:</span></span>

* [<span data-ttu-id="9e600-361">Управляемая клиентом проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="9e600-361">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="9e600-362">Управляемая сервером проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="9e600-362">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="9e600-363">Кэширование маркера аутентификации</span><span class="sxs-lookup"><span data-stu-id="9e600-363">Caching the authentication token</span></span>](#caching)

### <span data-ttu-id="9e600-364"><a name="clientflow"></a>Управляемая клиентом проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="9e600-364"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="9e600-365">Приложение может самостоятельно связаться с поставщиком удостоверений и передать серверной части вашего приложения полученный маркер для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9e600-365">Your app can independently contact the identity provider and then provide the returned token during login with your backend.</span></span> <span data-ttu-id="9e600-366">Этот клиентский поток позволяет пользователям выполнять единый вход или получать дополнительные данные о пользователе от поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="9e600-366">This client flow enables you to provide a single sign-on experience for users or to retrieve additional user data from the identity provider.</span></span> <span data-ttu-id="9e600-367">Клиентский поток аутентификации предпочтительнее, чем серверный, так как пакет SDK поставщика удостоверений обеспечивает более естественный интерфейс входа для пользователя и позволяет выполнять дополнительную настройку.</span><span class="sxs-lookup"><span data-stu-id="9e600-367">Client flow authentication is preferred to using a server flow as the identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="9e600-368">Доступны примеры организации некоторых клиентских потоков проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9e600-368">Examples are provided for the following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="9e600-369">Библиотека проверки подлинности Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e600-369">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="9e600-370">Facebook или Google</span><span class="sxs-lookup"><span data-stu-id="9e600-370">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="9e600-371">Пакет Live SDK</span><span class="sxs-lookup"><span data-stu-id="9e600-371">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="9e600-372"><a name="adal"></a>Аутентификация пользователей с помощью библиотеки аутентификации Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e600-372"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="9e600-373">Вы можете использовать библиотеку проверки подлинности Active Directory (ADAL) для управления входом пользователей из клиента с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9e600-373">You can use the Active Directory Authentication Library (ADAL) to initiate user authentication from the client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="9e600-374">Настройте серверную часть мобильного приложения для входа с помощью AAD, следуя указаниям в учебнике [Настройка приложения службы приложений для использования службы входа Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="9e600-374">Configure your mobile app backend for AAD sign-on by following the [How to configure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="9e600-375">Обязательно выполните дополнительный этап регистрации собственного клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="9e600-375">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="9e600-376">Откройте проект в Visual Studio или Xamarin Studio и добавьте ссылку на пакет NuGet `Microsoft.IdentityModel.CLients.ActiveDirectory` .</span><span class="sxs-lookup"><span data-stu-id="9e600-376">In Visual Studio or Xamarin Studio, open your project and add a reference to the `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="9e600-377">Включите в диапазон поиска предварительные версии.</span><span class="sxs-lookup"><span data-stu-id="9e600-377">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="9e600-378">Добавьте в приложение код, соответствующий используемой платформе, который приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="9e600-378">Add the following code to your application, according to the platform you are using.</span></span> <span data-ttu-id="9e600-379">В каждом коде выполните следующие замены.</span><span class="sxs-lookup"><span data-stu-id="9e600-379">In each, make the following replacements:</span></span>

   * <span data-ttu-id="9e600-380">Замените строку **INSERT-AUTHORITY-HERE** именем клиента, в котором подготовлено приложение.</span><span class="sxs-lookup"><span data-stu-id="9e600-380">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="9e600-381">Формат должен быть следующим: https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="9e600-381">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="9e600-382">Это значение можно скопировать на вкладке "Домен" в разделе Azure Active Directory на [классическом портале Azure].</span><span class="sxs-lookup"><span data-stu-id="9e600-382">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="9e600-383">Замените текст **INSERT-RESOURCE-ID-HERE** идентификатором клиента для серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="9e600-383">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="9e600-384">Идентификатор клиента можно скопировать на портале в разделе **Настройки Azure Active Directory** на вкладке **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="9e600-384">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="9e600-385">Замените текст **INSERT-CLIENT-ID-HERE** идентификатором клиента, скопированным из собственного клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="9e600-385">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="9e600-386">Замените текст **INSERT-REDIRECT-URI-HERE** конечной точкой сайта */.auth/login/done* , используя схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9e600-386">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="9e600-387">Это значение должно быть похоже на *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="9e600-387">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="9e600-388">Ниже приведены колы для каждой платформы.</span><span class="sxs-lookup"><span data-stu-id="9e600-388">The code needed for each platform follows:</span></span>

     <span data-ttu-id="9e600-389">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="9e600-389">**Windows:**</span></span>

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

     <span data-ttu-id="9e600-390">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="9e600-390">**Xamarin.iOS**</span></span>

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

     <span data-ttu-id="9e600-391">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="9e600-391">**Xamarin.Android**</span></span>

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

#### <span data-ttu-id="9e600-392"><a name="client-facebook"></a>Единый вход с помощью маркера Google или Facebook</span><span class="sxs-lookup"><span data-stu-id="9e600-392"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="9e600-393">В этом фрагменте показан пример использования клиентского потока для Google или Facebook.</span><span class="sxs-lookup"><span data-stu-id="9e600-393">You can use the client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using the Facebook or Google SDK.
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
            // to MobileServiceAuthenticationProvider.Google if using Google auth.
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

#### <span data-ttu-id="9e600-394"><a name="client-livesdk"></a>Единый вход с использованием учетной записи Майкрософт и пакета Live SDK</span><span class="sxs-lookup"><span data-stu-id="9e600-394"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with the Live SDK</span></span>
<span data-ttu-id="9e600-395">Чтобы аутентифицировать пользователей, необходимо зарегистрировать свое приложение в центре разработчиков учетных записей Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="9e600-395">To authenticate users, you must register your app at the Microsoft account Developer Center.</span></span> <span data-ttu-id="9e600-396">Настройте регистрационные данные для серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="9e600-396">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="9e600-397">Выполните действия, описанные в разделе [Регистрация приложения для входа с использованием учетной записи Майкрософт], чтобы создать учетную запись Майкрософт и подключить ее к серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="9e600-397">To create a Microsoft account registration and connect it to your Mobile App backend, complete the steps in [Register your app to use a Microsoft account login].</span></span> <span data-ttu-id="9e600-398">Если у вас есть версии приложения Магазина Windows и Windows Phone 8/Silverlight, сначала зарегистрируйте версию для Магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="9e600-398">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register the Windows Store version first.</span></span>

<span data-ttu-id="9e600-399">Следующий код выполняет аутентификацию с помощью пакета Live SDK и использует возвращенный маркер для входа в серверную часть мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="9e600-399">The following code authenticates using Live SDK and uses the returned token to sign in to your Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get the URL the Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create the authentication client for Windows Store using the service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create the authentication client for Windows Phone using the client ID of the registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request the authentication token from the Live authentication service.
        // The wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about the logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use the Microsoft account auth token to sign in to App Service.
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

<span data-ttu-id="9e600-400">Дополнительные сведения см. в документации по [пакету SDK для Windows Live].</span><span class="sxs-lookup"><span data-stu-id="9e600-400">For more information, see the [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="9e600-401"><a name="serverflow"></a>Управляемая сервером проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="9e600-401"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="9e600-402">После регистрации поставщика удостоверений вызовите метод [LoginAsync] для [MobileServiceClient], передав ему значение [MobileServiceAuthenticationProvider], соответствующее вашему поставщику.</span><span class="sxs-lookup"><span data-stu-id="9e600-402">Once you have registered your identity provider, call the [LoginAsync] method on the [MobileServiceClient] with the [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="9e600-403">Например, следующий код запускает вход в систему через поток сервера с помощью Facebook.</span><span class="sxs-lookup"><span data-stu-id="9e600-403">For example, the following code initiates a server flow sign-in by using Facebook.</span></span>

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

<span data-ttu-id="9e600-404">Если используется поставщик удостоверений, отличный от Facebook, измените значение [MobileServiceAuthenticationProvider] на значение для своего поставщика.</span><span class="sxs-lookup"><span data-stu-id="9e600-404">If you are using an identity provider other than Facebook, change the value of [MobileServiceAuthenticationProvider] to the value for your provider.</span></span>

<span data-ttu-id="9e600-405">При использовании серверного потока служба приложений Azure управляет потоком аутентификации OAuth, отображая страницу входа выбранного поставщика.</span><span class="sxs-lookup"><span data-stu-id="9e600-405">In a server flow, Azure App Service manages the OAuth authentication flow by displaying the sign-in page of the selected provider.</span></span>  <span data-ttu-id="9e600-406">После получения ответа от поставщика удостоверений служба приложений Azure создает маркер аутентификации службы приложений.</span><span class="sxs-lookup"><span data-stu-id="9e600-406">Once the identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="9e600-407">Метод [LoginAsync] возвращает ответ [MobileServiceUser], в котором содержится как [userId] авторизованного пользователя, так и [MobileServiceAuthenticationToken] в качестве веб-маркера JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="9e600-407">The [LoginAsync] method returns a [MobileServiceUser], which provides both the [UserId] of the authenticated user and the [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="9e600-408">Этот маркер можно поместить в кэш и повторно использовать, пока не истечет срок его действия.</span><span class="sxs-lookup"><span data-stu-id="9e600-408">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="9e600-409">Дополнительные сведения см. в разделе [Кэширование маркера проверки подлинности](#caching).</span><span class="sxs-lookup"><span data-stu-id="9e600-409">For more information, see [Caching the authentication token](#caching).</span></span>

### <span data-ttu-id="9e600-410"><a name="caching"></a>Кэширование маркера проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="9e600-410"><a name="caching"></a>Caching the authentication token</span></span>
<span data-ttu-id="9e600-411">В некоторых случаях после первой успешной аутентификации можно не выполнять вызов метода входа в систему. Для этого следует сохранить маркер аутентификации.</span><span class="sxs-lookup"><span data-stu-id="9e600-411">In some cases, the call to the login method can be avoided after the first successful authentication by storing the authentication token from the provider.</span></span>  <span data-ttu-id="9e600-412">Приложения Магазина Windows и UWP могут использовать [PasswordVault] для сохранения текущего маркера аутентификации после успешного входа в систему.</span><span class="sxs-lookup"><span data-stu-id="9e600-412">Windows Store and UWP apps can use [PasswordVault] to cache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="9e600-413">Значение идентификатора пользователя (UserId) хранится в параметре UserName учетных данных. Маркер проверки подлинности хранится в параметре Password.</span><span class="sxs-lookup"><span data-stu-id="9e600-413">The UserId value is stored as the UserName of the credential and the token is the stored as the Password.</span></span> <span data-ttu-id="9e600-414">При последующих запусках вы можете проверить, сохранились ли учетные данные в **PasswordVault**.</span><span class="sxs-lookup"><span data-stu-id="9e600-414">On subsequent start-ups, you can check the **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="9e600-415">В следующем примере используются сохраненные учетные данные, если они есть. В противном случае выполняется новая попытка пройти проверку подлинности в серверной части.</span><span class="sxs-lookup"><span data-stu-id="9e600-415">The following example uses cached credentials when they are found, and otherwise attempts to authenticate again with the backend:</span></span>

```
// Try to retrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create the current user from the stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache the token as shown above.
}
```

<span data-ttu-id="9e600-416">При выходе пользователя из приложения необходимо удалить сохраненные учетные данные, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9e600-416">When you sign out a user, you must also remove the stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="9e600-417">Приложения Xamarin используют интерфейсы API [Xamarin.Auth], которые позволяют безопасно хранить учетные данные в объекте **Account**.</span><span class="sxs-lookup"><span data-stu-id="9e600-417">Xamarin    apps use the [Xamarin.Auth] APIs to securely store credentials in an **Account** object.</span></span> <span data-ttu-id="9e600-418">Пример использования этих API см. в файле кода [AuthStore.cs], который включен в [пример совместного использования фотографий ContosoMoments](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="9e600-418">For an example of using these APIs, see the [AuthStore.cs] code file in the [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="9e600-419">Если вы используете клиентский поток проверки подлинности, вы можете сохранить маркер доступа, полученный от поставщика, такого как Facebook или Twitter.</span><span class="sxs-lookup"><span data-stu-id="9e600-419">When you use client-managed authentication, you can also cache the access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="9e600-420">Этот маркер можно использовать для запроса нового маркера проверки подлинности у серверной части:</span><span class="sxs-lookup"><span data-stu-id="9e600-420">This token can be supplied to request a new authentication token from the backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using the access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="9e600-421"><a name="pushnotifications"></a>Push-уведомления</span><span class="sxs-lookup"><span data-stu-id="9e600-421"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="9e600-422">Push-уведомления рассматриваются в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="9e600-422">The following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="9e600-423">Регистрация для получения push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="9e600-423">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="9e600-424">Получение SID пакета Магазина Windows</span><span class="sxs-lookup"><span data-stu-id="9e600-424">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="9e600-425">Регистрация с помощью межплатформенных шаблонов</span><span class="sxs-lookup"><span data-stu-id="9e600-425">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="9e600-426"><a name="register-for-push"></a>Практическое руководство. Регистрация для получения push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="9e600-426"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="9e600-427">Клиент мобильных приложений позволяет выполнить регистрацию для получения push-уведомлений с помощью центров уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="9e600-427">The Mobile Apps client enables you to register for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="9e600-428">При регистрации вы получаете маркер из службы push-уведомлений (PNS).</span><span class="sxs-lookup"><span data-stu-id="9e600-428">When registering, you obtain a handle that you obtain from the platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="9e600-429">Это значение необходимо указать при регистрации вместе со всеми тегами.</span><span class="sxs-lookup"><span data-stu-id="9e600-429">You then provide this value along with any tags when you create the registration.</span></span> <span data-ttu-id="9e600-430">Следующий код регистрирует ваше приложение Windows для получения push-уведомлений через службу уведомлений Windows (WNS):</span><span class="sxs-lookup"><span data-stu-id="9e600-430">The following code registers your Windows app for push notifications with the Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using the new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="9e600-431">При отправке push-уведомлений в WNS необходимо [получить идентификатор безопасности пакета Магазина Windows](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="9e600-431">If you are pushing to WNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="9e600-432">Дополнительные сведения о приложениях Windows, включая способ регистрации шаблонов, см. в разделе [Добавление push-уведомлений в приложение].</span><span class="sxs-lookup"><span data-stu-id="9e600-432">For more information on Windows apps, including how to register for template registrations, see [Add push notifications to your app].</span></span>

<span data-ttu-id="9e600-433">Запрос тегов от клиента не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="9e600-433">Requesting tags from the client is not supported.</span></span>  <span data-ttu-id="9e600-434">Запросы тегов автоматически отбрасываются из регистрации.</span><span class="sxs-lookup"><span data-stu-id="9e600-434">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="9e600-435">Если вы хотите зарегистрировать устройство с тегами, создайте пользовательский интерфейс API, который использует API центров уведомлений для выполнения регистрации от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="9e600-435">If you wish to register your device with tags, create a Custom API that uses the Notification Hubs API to perform the registration on your behalf.</span></span>  <span data-ttu-id="9e600-436">[Используйте вызов настраиваемого API](#customapi) вместо метода `RegisterNativeAsync()`.</span><span class="sxs-lookup"><span data-stu-id="9e600-436">[Call the Custom API](#customapi) instead of the `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="9e600-437"><a name="package-sid"></a>Практическое руководство. Получение SID пакета Магазина Windows</span><span class="sxs-lookup"><span data-stu-id="9e600-437"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="9e600-438">Для включения push-уведомлений для приложений Магазина Windows необходим SID пакета.</span><span class="sxs-lookup"><span data-stu-id="9e600-438">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="9e600-439">Для получения идентификатора безопасности пакета зарегистрируйте приложение в Магазине Windows.</span><span class="sxs-lookup"><span data-stu-id="9e600-439">To receive a package SID, register your application with the Windows Store.</span></span>

<span data-ttu-id="9e600-440">Для получения этого значения выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9e600-440">To obtain this value:</span></span>

1. <span data-ttu-id="9e600-441">В обозревателе решений Visual Studio щелкните правой кнопкой мыши проект приложения Магазина Windows и щелкните **Магазин** > **Связать приложение с Магазином…**.</span><span class="sxs-lookup"><span data-stu-id="9e600-441">In Visual Studio Solution Explorer, right-click the Windows Store app project, click **Store** > **Associate App with the Store...**.</span></span>
2. <span data-ttu-id="9e600-442">В окне мастера нажмите кнопку **Далее**, выполните вход с помощью учетной записи Майкрософт, введите имя приложения в поле **Зарезервировать новое имя приложения** и нажмите кнопку **Зарезервировать**.</span><span class="sxs-lookup"><span data-stu-id="9e600-442">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="9e600-443">После успешного создания регистрации приложения выберите имя приложения, нажмите кнопку **Далее**, а затем кнопку **Связать**.</span><span class="sxs-lookup"><span data-stu-id="9e600-443">After the app registration is successfully created, select the app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="9e600-444">Выполните вход в [Центр разработки для Windows] с использованием учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="9e600-444">Log in to the [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="9e600-445">В разделе **Мои приложения**щелкните созданную регистрацию приложения.</span><span class="sxs-lookup"><span data-stu-id="9e600-445">Under **My apps**, click the app registration you created.</span></span>
5. <span data-ttu-id="9e600-446">Щелкните **Управление приложениями** > **Удостоверение приложения**, а затем выполните прокрутку вниз, чтобы найти ваш **идентификатор безопасности пакета**.</span><span class="sxs-lookup"><span data-stu-id="9e600-446">Click **App management** > **App identity**, and then scroll down to find your **Package SID**.</span></span>

<span data-ttu-id="9e600-447">Во многих случаях идентификатор безопасности пакета рассматривается как универсальный код ресурса (URI). В этом случае необходимо использовать *ms-app://* в качестве схемы.</span><span class="sxs-lookup"><span data-stu-id="9e600-447">Many uses of the package SID treat it as a URI, in which case you need to use *ms-app://* as the scheme.</span></span> <span data-ttu-id="9e600-448">Запишите версию ИД безопасности пакета, получаемую путем сцепления этого значения в качестве префикса.</span><span class="sxs-lookup"><span data-stu-id="9e600-448">Make note of the version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="9e600-449">Приложениям Xamarin требуется дополнительный код для регистрации приложений, работающих на платформе iOS или Android.</span><span class="sxs-lookup"><span data-stu-id="9e600-449">Xamarin apps require some additional code to be able to register an app running on the iOS or Android platforms.</span></span> <span data-ttu-id="9e600-450">Дополнительные сведения см. в разделе для вашей платформы:</span><span class="sxs-lookup"><span data-stu-id="9e600-450">For more information, see the topic for your platform:</span></span>

* [<span data-ttu-id="9e600-451">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="9e600-451">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="9e600-452">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="9e600-452">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="9e600-453"><a name="register-xplat"></a>Использование шаблонов для отправки кроссплатформенных push- уведомлений</span><span class="sxs-lookup"><span data-stu-id="9e600-453"><a name="register-xplat"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="9e600-454">Чтобы зарегистрировать шаблоны, используйте метод `RegisterAsync()` с шаблонами, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9e600-454">To register templates, use the `RegisterAsync()` method with the templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="9e600-455">Шаблоны должны иметь тип `JObject` и могут содержать несколько шаблонов в приведенном ниже формате JSON.</span><span class="sxs-lookup"><span data-stu-id="9e600-455">Your templates should be `JObject` types and can contain multiple templates in the following JSON format:</span></span>

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

<span data-ttu-id="9e600-456">Метод **RegisterAsync()** принимает также вспомогательные плитки:</span><span class="sxs-lookup"><span data-stu-id="9e600-456">The method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="9e600-457">Во время регистрации все теги удаляются в целях безопасности.</span><span class="sxs-lookup"><span data-stu-id="9e600-457">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="9e600-458">В статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure] показано, как добавлять теги для установки устройства или шаблоны в пределах установки.</span><span class="sxs-lookup"><span data-stu-id="9e600-458">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="9e600-459">Для отправки уведомлений с использованием этих зарегистрированных шаблонов ознакомьтесь со [справочниками по API].</span><span class="sxs-lookup"><span data-stu-id="9e600-459">To send notifications utilizing these registered templates, refer to the [Notification Hubs APIs].</span></span>

## <span data-ttu-id="9e600-460"><a name="misc"></a>Разное</span><span class="sxs-lookup"><span data-stu-id="9e600-460"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="9e600-461"><a name="errors"></a>Практическое руководство. Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="9e600-461"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="9e600-462">При возникновении ошибки в серверной части пакет SDK для клиента порождает исключение `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="9e600-462">When an error occurs in the backend, the client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="9e600-463">Следующий пример демонстрирует обработку исключения, возвращенного серверной частью:</span><span class="sxs-lookup"><span data-stu-id="9e600-463">The following example shows how to handle an exception that is returned by the backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into the database. When the operation completes
    // and App Service has assigned an Id, the item is added to the CollectionView
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

<span data-ttu-id="9e600-464">Еще один пример работы с состояниями ошибки можно найти в [примере файлов мобильных приложений].</span><span class="sxs-lookup"><span data-stu-id="9e600-464">Another example of dealing with error conditions can be found in the [Mobile Apps Files Sample].</span></span> <span data-ttu-id="9e600-465">Пример [LoggingHandler] предоставляет обработчик делегированного входа для ведения журнала запросов к серверной части.</span><span class="sxs-lookup"><span data-stu-id="9e600-465">The [LoggingHandler] example provides a logging delegate handler to log the requests being made to the backend.</span></span>

### <span data-ttu-id="9e600-466"><a name="headers"></a>Практическое руководство. Настройка заголовков запроса</span><span class="sxs-lookup"><span data-stu-id="9e600-466"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="9e600-467">Для поддержки определенного сценария приложения вам может потребоваться настроить связь с внутренним сервером мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="9e600-467">To support your specific app scenario, you might need to customize communication with the Mobile App backend.</span></span> <span data-ttu-id="9e600-468">Например, может возникнуть необходимость добавлять настраиваемый заголовок к каждому исходящему запросу или даже изменять коды состояний ответов.</span><span class="sxs-lookup"><span data-stu-id="9e600-468">For example, you may want to add a custom header to every outgoing request or even change responses status codes.</span></span> <span data-ttu-id="9e600-469">Вы можете использовать настраиваемый метод [DelegatingHandler], как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="9e600-469">You can use a custom [DelegatingHandler], as in the following example:</span></span>

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
        // Change the request-side here based on the HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do the request
        var response = await base.SendAsync(request, cancellationToken);

        // Change the response-side here based on the HttpResponseMessage

        // Return the modified response
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

<span data-ttu-id="9e600-470">[Добавление проверки подлинности в приложение]: app-service-mobile-windows-store-dotnet-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="9e600-470">[Add authentication to your app]: app-service-mobile-windows-store-dotnet-get-started-users.md</span></span>
<span data-ttu-id="9e600-471">[Автономная синхронизация данных в мобильных приложениях Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="9e600-471">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="9e600-472">[Добавление push-уведомлений в приложение]: app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="9e600-472">[Add push notifications to your app]: app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="9e600-473">[Регистрация приложения для входа с использованием учетной записи Майкрософт]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="9e600-473">[Register your app to use a Microsoft account login]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="9e600-474">[Настройка приложения службы приложений для использования службы входа Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="9e600-474">[How to configure App Service for Active Directory login]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>

<!-- Microsoft URLs. -->
<span data-ttu-id="9e600-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-481">[создает ссылку на нетипизированную таблицу]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-481">[creates a reference to an untyped table]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span></span>
<span data-ttu-id="9e600-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span></span>
<span data-ttu-id="9e600-497">[портале Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="9e600-497">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="9e600-498">[классическом портале Azure]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="9e600-498">[Azure classic portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="9e600-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span></span>
<span data-ttu-id="9e600-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span></span>
<span data-ttu-id="9e600-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span></span>
<span data-ttu-id="9e600-502">[Центр разработки для Windows]: https://dev.windows.com/en-us/overview</span><span class="sxs-lookup"><span data-stu-id="9e600-502">[Windows Dev Center]: https://dev.windows.com/en-us/overview</span></span>
<span data-ttu-id="9e600-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span></span>
<span data-ttu-id="9e600-504">[пакету SDK для Windows Live]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-504">[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span></span>
<span data-ttu-id="9e600-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span></span>
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
<span data-ttu-id="9e600-506">[справочниками по API]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span><span class="sxs-lookup"><span data-stu-id="9e600-506">[Notification Hubs APIs]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span></span>
<span data-ttu-id="9e600-507">[примере файлов мобильных приложений]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span><span class="sxs-lookup"><span data-stu-id="9e600-507">[Mobile Apps Files Sample]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span></span>
<span data-ttu-id="9e600-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span><span class="sxs-lookup"><span data-stu-id="9e600-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span></span>

<!-- External URLs -->
<span data-ttu-id="9e600-509">[документации по OData версии 3]: http://www.odata.org/documentation/odata-version-3-0/</span><span class="sxs-lookup"><span data-stu-id="9e600-509">[OData v3 Documentation]: http://www.odata.org/documentation/odata-version-3-0/</span></span>
<span data-ttu-id="9e600-510">[Fiddler]: http://www.telerik.com/fiddler</span><span class="sxs-lookup"><span data-stu-id="9e600-510">[Fiddler]: http://www.telerik.com/fiddler</span></span>
<span data-ttu-id="9e600-511">[Json.NET]: http://www.newtonsoft.com/json</span><span class="sxs-lookup"><span data-stu-id="9e600-511">[Json.NET]: http://www.newtonsoft.com/json</span></span>
<span data-ttu-id="9e600-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span><span class="sxs-lookup"><span data-stu-id="9e600-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span></span>
<span data-ttu-id="9e600-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span><span class="sxs-lookup"><span data-stu-id="9e600-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span></span>
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
