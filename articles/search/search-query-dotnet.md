---
title: "Отправка запросов в индекс службы поиска Azure с помощью API .NET | Документация Майкрософт"
description: "В службе поиска Azure можно создавать поисковые запросы и с помощью параметров поиска фильтровать, сортировать и уточнять результаты."
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 52bd0fd4cf70401dcf881c7f28d5cd91397bb059
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="query-your-azure-search-index-using-the-net-sdk"></a><span data-ttu-id="551a6-103">Отправка запросов в индекс службы поиска Azure с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="551a6-103">Query your Azure Search index using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="551a6-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="551a6-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="551a6-105">Портал</span><span class="sxs-lookup"><span data-stu-id="551a6-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="551a6-106">.NET</span><span class="sxs-lookup"><span data-stu-id="551a6-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="551a6-107">REST</span><span class="sxs-lookup"><span data-stu-id="551a6-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="551a6-108">В этой статье показано, как отправлять запросы в индекс с помощью [пакета SDK .NET для службы поиска Azure](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="551a6-108">This article will show you how to query an index using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="551a6-109">Прежде чем приступать к выполнению инструкций из этого руководства, необходимо [создать индекс службы поиска Azure](search-what-is-an-index.md) и [заполнить его данными](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="551a6-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="551a6-110">Все приведенные здесь примеры кода написаны на языке C#.</span><span class="sxs-lookup"><span data-stu-id="551a6-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="551a6-111">Полный исходный код можно найти на сайте [GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="551a6-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="551a6-112">Подробные примеры использования кода см. в сведениях о [пакете SDK .NET для службы поиска Azure](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="551a6-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="551a6-113">Определение ключа API запроса службы поиска Azure</span><span class="sxs-lookup"><span data-stu-id="551a6-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="551a6-114">Теперь, когда вы создали индекс службы поиска Azure, вы почти готовы отправлять запросы с помощью пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="551a6-114">Now that you have created an Azure Search index, you are almost ready to issue queries using the .NET SDK.</span></span> <span data-ttu-id="551a6-115">Для этого сначала нужно получить один из ключей API запроса, созданный для подготовленной службы поиска.</span><span class="sxs-lookup"><span data-stu-id="551a6-115">First, you will need to obtain one of the query api-keys that was generated for the search service you provisioned.</span></span> <span data-ttu-id="551a6-116">Пакет SDK для .NET отправляет этот ключ при каждом запросе к службе.</span><span class="sxs-lookup"><span data-stu-id="551a6-116">The .NET SDK will send this api-key on every request to your service.</span></span> <span data-ttu-id="551a6-117">Если есть действительный ключ, для каждого запроса устанавливаются отношения доверия между приложением, которое отправляет запрос, и службой, которая его обрабатывает.</span><span class="sxs-lookup"><span data-stu-id="551a6-117">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="551a6-118">Чтобы найти ключи API своей службы, войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="551a6-118">To find your service's api-keys you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="551a6-119">Перейдите к колонке службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="551a6-119">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="551a6-120">Щелкните значок "Ключи".</span><span class="sxs-lookup"><span data-stu-id="551a6-120">Click on the "Keys" icon</span></span>

<span data-ttu-id="551a6-121">Ваша служба получит *ключи администратора* и *ключи запросов*.</span><span class="sxs-lookup"><span data-stu-id="551a6-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="551a6-122">Первичные и вторичные *ключи администратора* предоставляют полный доступ ко всем операциям, включая возможность управлять службой, создавать и удалять индексы, индексаторы и источники данных.</span><span class="sxs-lookup"><span data-stu-id="551a6-122">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="551a6-123">Ключей два, поэтому вы можете и дальше использовать вторичный ключ, если решите повторно создать первичный ключ, и наоборот.</span><span class="sxs-lookup"><span data-stu-id="551a6-123">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="551a6-124">*Ключи запросов* предоставляют только разрешение на чтение индексов и документов; обычно они добавляются в клиентские приложения, которые создают запросы на поиск.</span><span class="sxs-lookup"><span data-stu-id="551a6-124">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="551a6-125">Для отправки запросов в индекс можно использовать один из ключей запросов.</span><span class="sxs-lookup"><span data-stu-id="551a6-125">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="551a6-126">Для запросов можно использовать также ключи администратора, но в коде приложения следует использовать ключ запроса, так как этот вариант лучше соответствует [принципу предоставления минимальных прав](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="551a6-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="551a6-127">Создание экземпляра класса SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="551a6-127">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="551a6-128">Чтобы отправлять запросы с помощью пакета SDK .NET для службы поиска Azure, нужно создать экземпляр класса `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="551a6-128">To issue queries with the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="551a6-129">Этот класс имеет несколько конструкторов.</span><span class="sxs-lookup"><span data-stu-id="551a6-129">This class has several constructors.</span></span> <span data-ttu-id="551a6-130">Нужный вам конструктор принимает в качестве параметров имя службы поиска, имя индекса и объект `SearchCredentials` .</span><span class="sxs-lookup"><span data-stu-id="551a6-130">The one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="551a6-131">`SearchCredentials` содержит ключ API.</span><span class="sxs-lookup"><span data-stu-id="551a6-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="551a6-132">Приведенный ниже код создает класс `SearchIndexClient` для индекса hotels, используя значения имени службы поиска и ключа API, которые хранятся в файле конфигурации приложения (`appsettings.json` в случае [примера приложения](http://aka.ms/search-dotnet-howto)). Инструкции по созданию индекса hotels см. в статье [Создание индекса службы поиска Azure с помощью пакета SDK для .NET](search-create-index-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="551a6-132">The code below creates a new `SearchIndexClient` for the "hotels" index (created in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md)) using values for the search service name and api-key that are stored in the application's config file (`appsettings.json` in the case of the [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="551a6-133">У класса `SearchIndexClient` есть свойство `Documents`.</span><span class="sxs-lookup"><span data-stu-id="551a6-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="551a6-134">Это свойство предоставляет все методы, которые требуются для отправки запросов в индексы службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="551a6-134">This property provides all the methods you need to query Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="551a6-135">Отправка запроса в индекс</span><span class="sxs-lookup"><span data-stu-id="551a6-135">Query your index</span></span>
<span data-ttu-id="551a6-136">Поиск с помощью пакета SDK для .NET сводится к вызову метода `Documents.Search` для класса `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="551a6-136">Searching with the .NET SDK is as simple as calling the `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="551a6-137">Этот метод принимает несколько параметров, включая текст поиска и объект `SearchParameters` , с помощью которого можно уточнить запрос.</span><span class="sxs-lookup"><span data-stu-id="551a6-137">This method takes a few parameters, including the search text, along with a `SearchParameters` object that can be used to further refine the query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="551a6-138">Типы запросов</span><span class="sxs-lookup"><span data-stu-id="551a6-138">Types of Queries</span></span>
<span data-ttu-id="551a6-139">Два основных [типа запросов](search-query-overview.md#types-of-queries), которые вы будете использовать, — это `search` и `filter`.</span><span class="sxs-lookup"><span data-stu-id="551a6-139">The two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="551a6-140">Запрос `search` выполняет поиск по одному или нескольким условиям во всех *поддерживающих поиск* полях индекса.</span><span class="sxs-lookup"><span data-stu-id="551a6-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="551a6-141">Запрос `filter` оценивает логическое выражение во всех *фильтруемых* полях индекса.</span><span class="sxs-lookup"><span data-stu-id="551a6-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="551a6-142">Поиск и фильтрация выполняются с помощью метода `Documents.Search` .</span><span class="sxs-lookup"><span data-stu-id="551a6-142">Both searches and filters are performed using the `Documents.Search` method.</span></span> <span data-ttu-id="551a6-143">Поисковый запрос можно передать в параметре `searchText`, а выражение фильтра — в свойстве `Filter` класса `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="551a6-143">A search query can be passed in the `searchText` parameter, while a filter expression can be passed in the `Filter` property of the `SearchParameters` class.</span></span> <span data-ttu-id="551a6-144">Чтобы выполнить фильтрацию и при этом не выполнять поиск, в качестве значения параметра `searchText` укажите `"*"`.</span><span class="sxs-lookup"><span data-stu-id="551a6-144">To filter without searching, just pass `"*"` for the `searchText` parameter.</span></span> <span data-ttu-id="551a6-145">Чтобы выполнить поиск, не прибегая к фильтрации, не задавайте значение свойства `Filter` или вообще не передавайте его в экземпляр `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="551a6-145">To search without filtering, just leave the `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="551a6-146">Примеры запросов</span><span class="sxs-lookup"><span data-stu-id="551a6-146">Example Queries</span></span>
<span data-ttu-id="551a6-147">В следующем примере кода показано несколько разных способов отправки запросов в индекс hotels, описанный в статье [Создание индекса службы поиска Azure с помощью пакета SDK для .NET](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="551a6-147">The following sample code shows a few different ways to query the "hotels" index defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="551a6-148">Обратите внимание, что документы, возвращаемые в результатах поиска, — это экземпляры класса `Hotel` , описанного в статье [Импорт данных в службу поиска Azure с помощью пакета SDK для .NET](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="551a6-148">Note that the documents returned with the search results are instances of the `Hotel` class, which was defined in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="551a6-149">Пример кода выводит результаты поиска на консоль с помощью метода `WriteDocuments` .</span><span class="sxs-lookup"><span data-stu-id="551a6-149">The sample code makes use of a `WriteDocuments` method to output the search results to the console.</span></span> <span data-ttu-id="551a6-150">Этот метод описан в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="551a6-150">This method is described in the next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
Console.WriteLine("and return the hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take the top two results, and show only hotelName and ");
Console.WriteLine("lastRenovationDate:\n");

parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.WriteLine("Search the entire index for the term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="551a6-151">Обработка результатов поиска</span><span class="sxs-lookup"><span data-stu-id="551a6-151">Handle search results</span></span>
<span data-ttu-id="551a6-152">Метод `Documents.Search` возвращает объект `DocumentSearchResult`, содержащий результаты запроса.</span><span class="sxs-lookup"><span data-stu-id="551a6-152">The `Documents.Search` method returns a `DocumentSearchResult` object that contains the results of the query.</span></span> <span data-ttu-id="551a6-153">В примере из предыдущего раздела результаты поиска выводятся на консоль с помощью метода `WriteDocuments` .</span><span class="sxs-lookup"><span data-stu-id="551a6-153">The example in the previous section used a method called `WriteDocuments` to output the search results to the console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="551a6-154">Вот как будут выглядеть результаты запросов из предыдущего раздела (если индекс hotels заполнен демонстрационными данными, как описано в статье [Импорт данных в службу поиска Azure с помощью пакета SDK для .NET](search-import-data-dotnet.md)).</span><span class="sxs-lookup"><span data-stu-id="551a6-154">Here is what the results look like for the queries in the previous section, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search the entire index for the term 'budget' and return only the hotelName field:

Name: Roach Motel

Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close to town hall and the river

Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search the entire index for the term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="551a6-155">Приведенный выше пример кода выводит результаты поиска в консоль.</span><span class="sxs-lookup"><span data-stu-id="551a6-155">The sample code above uses the console to output search results.</span></span> <span data-ttu-id="551a6-156">Таким же образом вам нужно будет показывать результаты поиска и в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="551a6-156">You will likewise need to display search results in your own application.</span></span> <span data-ttu-id="551a6-157">Сведения о том, как отображать результаты поиска в веб-приложении ASP.NET с использованием схемы MVC, см. в [этом примере на сайте GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample).</span><span class="sxs-lookup"><span data-stu-id="551a6-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how to render search results in an ASP.NET MVC-based web application.</span></span>

