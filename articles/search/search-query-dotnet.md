---
title: "AAA» запроса индекса (API .NET - поиска Azure) | Документы Microsoft»"
description: "Построить запрос поиска в поиске Azure и использовать параметры сортировки и toofilter поиска результатов поиска."
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
ms.openlocfilehash: 8b3ba1cd1270aad038fb48d9053fcff35d243e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a><span data-ttu-id="af67b-103">Запросить индекс поиска Azure с помощью hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="af67b-103">Query your Azure Search index using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af67b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="af67b-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="af67b-105">Портал</span><span class="sxs-lookup"><span data-stu-id="af67b-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="af67b-106">.NET</span><span class="sxs-lookup"><span data-stu-id="af67b-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="af67b-107">REST</span><span class="sxs-lookup"><span data-stu-id="af67b-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="af67b-108">В этой статье мы покажем, как hello индекса с помощью tooquery [пакет SDK Azure Search .NET](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="af67b-108">This article will show you how tooquery an index using hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="af67b-109">Прежде чем приступать к выполнению инструкций из этого руководства, необходимо [создать индекс службы поиска Azure](search-what-is-an-index.md) и [заполнить его данными](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="af67b-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="af67b-110">Все приведенные здесь примеры кода написаны на языке C#.</span><span class="sxs-lookup"><span data-stu-id="af67b-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="af67b-111">Можно найти полный исходный код hello [на GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="af67b-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="af67b-112">Вы также можете прочесть об hello [пакет SDK Azure Search .NET](search-howto-dotnet-sdk.md) для более подробные руководства по hello примеров кода.</span><span class="sxs-lookup"><span data-stu-id="af67b-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="af67b-113">Определение ключа API запроса службы поиска Azure</span><span class="sxs-lookup"><span data-stu-id="af67b-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="af67b-114">Теперь, создав индекс поиска Azure, все почти готово tooissue запросы, использующие hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="af67b-114">Now that you have created an Azure Search index, you are almost ready tooissue queries using hello .NET SDK.</span></span> <span data-ttu-id="af67b-115">Во-первых необходимо будет tooobtain один hello ключей api запросов, которые были созданы для подготовленной службы поиска hello.</span><span class="sxs-lookup"><span data-stu-id="af67b-115">First, you will need tooobtain one of hello query api-keys that was generated for hello search service you provisioned.</span></span> <span data-ttu-id="af67b-116">Hello .NET SDK будет отправлять этот ключ api для каждой службы tooyour запроса.</span><span class="sxs-lookup"><span data-stu-id="af67b-116">hello .NET SDK will send this api-key on every request tooyour service.</span></span> <span data-ttu-id="af67b-117">Наличие действительного ключа позволяет установить отношения доверия, для каждого запроса, между Отправка запроса hello hello приложения и службы hello, обрабатывает его.</span><span class="sxs-lookup"><span data-stu-id="af67b-117">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="af67b-118">toofind ключи api службы, вы сможете войти в toohello [портал Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="af67b-118">toofind your service's api-keys you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="af67b-119">Перейдите в колонку службы поиска Azure tooyour</span><span class="sxs-lookup"><span data-stu-id="af67b-119">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="af67b-120">Щелкните значок «Ключи» hello</span><span class="sxs-lookup"><span data-stu-id="af67b-120">Click on hello "Keys" icon</span></span>

<span data-ttu-id="af67b-121">Ваша служба получит *ключи администратора* и *ключи запросов*.</span><span class="sxs-lookup"><span data-stu-id="af67b-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="af67b-122">Первичная и Вторичная *ключей администратора* предоставить полные права tooall операций, включая toomanage hello hello возможности службы, создания и удаления индексов, индексаторов и источников данных.</span><span class="sxs-lookup"><span data-stu-id="af67b-122">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="af67b-123">Существует два ключа, чтобы продолжить toouse hello вторичный ключ в случае tooregenerate hello первичного ключа и наоборот.</span><span class="sxs-lookup"><span data-stu-id="af67b-123">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="af67b-124">Ваш *запрос ключей* предоставить доступ только для чтения tooindexes и документы и представляют собой tooclient обычно распределенного приложения, издающие запросы поиска.</span><span class="sxs-lookup"><span data-stu-id="af67b-124">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="af67b-125">Запросы к индексу целях hello можно использовать один из ключей запроса.</span><span class="sxs-lookup"><span data-stu-id="af67b-125">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="af67b-126">Ключи администратора также может использоваться для запросов, но ключ запроса следует использовать в коде приложения, как это лучше отвечает hello [принципа наименьших прав доступа](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="af67b-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="af67b-127">Создайте экземпляр класса SearchIndexClient hello</span><span class="sxs-lookup"><span data-stu-id="af67b-127">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="af67b-128">tooissue запросы с hello пакет SDK Azure Search .NET, вам потребуется toocreate экземпляр hello `SearchIndexClient` класса.</span><span class="sxs-lookup"><span data-stu-id="af67b-128">tooissue queries with hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="af67b-129">Этот класс имеет несколько конструкторов.</span><span class="sxs-lookup"><span data-stu-id="af67b-129">This class has several constructors.</span></span> <span data-ttu-id="af67b-130">Hello один требуется принимает имя службы поиска, имя индекса и `SearchCredentials` объект в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="af67b-130">hello one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="af67b-131">`SearchCredentials` содержит ключ API.</span><span class="sxs-lookup"><span data-stu-id="af67b-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="af67b-132">Приведенный ниже код Hello создает новый `SearchIndexClient` для индекса «гостиницы» hello (созданных в [создать индекс поиска Azure с помощью hello пакета SDK для .NET](search-create-index-dotnet.md)) с использованием значений для hello имя службы поиска и ключ api, которые хранятся в файле конфигурации приложения hello файл (`appsettings.json` в случае, когда hello hello [образец приложения](http://aka.ms/search-dotnet-howto)):</span><span class="sxs-lookup"><span data-stu-id="af67b-132">hello code below creates a new `SearchIndexClient` for hello "hotels" index (created in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md)) using values for hello search service name and api-key that are stored in hello application's config file (`appsettings.json` in hello case of hello [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="af67b-133">У класса `SearchIndexClient` есть свойство `Documents`.</span><span class="sxs-lookup"><span data-stu-id="af67b-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="af67b-134">Это свойство предоставляет все hello методы должна tooquery индексах поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="af67b-134">This property provides all hello methods you need tooquery Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="af67b-135">Отправка запроса в индекс</span><span class="sxs-lookup"><span data-stu-id="af67b-135">Query your index</span></span>
<span data-ttu-id="af67b-136">Поиск с использованием hello .NET SDK сводится вызывающему Привет `Documents.Search` метод вашей `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="af67b-136">Searching with hello .NET SDK is as simple as calling hello `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="af67b-137">Этот метод принимает несколько параметров, включая текст поиска hello, вместе с `SearchParameters` объект, который может использоваться используется toofurther уточнение hello запрос.</span><span class="sxs-lookup"><span data-stu-id="af67b-137">This method takes a few parameters, including hello search text, along with a `SearchParameters` object that can be used toofurther refine hello query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="af67b-138">Типы запросов</span><span class="sxs-lookup"><span data-stu-id="af67b-138">Types of Queries</span></span>
<span data-ttu-id="af67b-139">Hello двух main [типами запросов](search-query-overview.md#types-of-queries) используется являются `search` и `filter`.</span><span class="sxs-lookup"><span data-stu-id="af67b-139">hello two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="af67b-140">Запрос `search` выполняет поиск по одному или нескольким условиям во всех *поддерживающих поиск* полях индекса.</span><span class="sxs-lookup"><span data-stu-id="af67b-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="af67b-141">Запрос `filter` оценивает логическое выражение во всех *фильтруемых* полях индекса.</span><span class="sxs-lookup"><span data-stu-id="af67b-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="af67b-142">Поиск и фильтры выполняются с использованием hello `Documents.Search` метод.</span><span class="sxs-lookup"><span data-stu-id="af67b-142">Both searches and filters are performed using hello `Documents.Search` method.</span></span> <span data-ttu-id="af67b-143">Запрос поиска можно передать в hello `searchText` параметра, а критерий фильтра может быть передан в hello `Filter` свойство hello `SearchParameters` класса.</span><span class="sxs-lookup"><span data-stu-id="af67b-143">A search query can be passed in hello `searchText` parameter, while a filter expression can be passed in hello `Filter` property of hello `SearchParameters` class.</span></span> <span data-ttu-id="af67b-144">toofilter без поиска, просто передать `"*"` для hello `searchText` параметра.</span><span class="sxs-lookup"><span data-stu-id="af67b-144">toofilter without searching, just pass `"*"` for hello `searchText` parameter.</span></span> <span data-ttu-id="af67b-145">toosearch без фильтрации, просто оставьте hello `Filter` свойство не задано, или не передавайте в `SearchParameters` экземпляра вообще.</span><span class="sxs-lookup"><span data-stu-id="af67b-145">toosearch without filtering, just leave hello `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="af67b-146">Примеры запросов</span><span class="sxs-lookup"><span data-stu-id="af67b-146">Example Queries</span></span>
<span data-ttu-id="af67b-147">Следующий образец кода Hello показано несколько способов hello tooquery «гостиницы «индекс определен в [создать индекс поиска Azure с помощью hello .NET SDK](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="af67b-147">hello following sample code shows a few different ways tooquery hello "hotels" index defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="af67b-148">Обратите внимание, что hello документов, возвращаемых с результатами поиска hello экземпляров hello `Hotel` класс, который был определен в [Здравствуйте, импорт данных в поиске Azure с помощью пакета SDK для .NET](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="af67b-148">Note that hello documents returned with hello search results are instances of hello `Hotel` class, which was defined in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="af67b-149">Здравствуйте, пример кода использует `WriteDocuments` toohello метод toooutput hello поиска результатов консоли.</span><span class="sxs-lookup"><span data-stu-id="af67b-149">hello sample code makes use of a `WriteDocuments` method toooutput hello search results toohello console.</span></span> <span data-ttu-id="af67b-150">Этот метод описан в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="af67b-150">This method is described in hello next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
Console.WriteLine("and return hello hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take hello top two results, and show only hotelName and ");
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

Console.WriteLine("Search hello entire index for hello term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="af67b-151">Обработка результатов поиска</span><span class="sxs-lookup"><span data-stu-id="af67b-151">Handle search results</span></span>
<span data-ttu-id="af67b-152">Hello `Documents.Search` возвращает метод `DocumentSearchResult` , содержащий результаты запроса hello hello.</span><span class="sxs-lookup"><span data-stu-id="af67b-152">hello `Documents.Search` method returns a `DocumentSearchResult` object that contains hello results of hello query.</span></span> <span data-ttu-id="af67b-153">пример Hello в предыдущем разделе hello использовать метод с именем `WriteDocuments` toooutput hello поиска результаты toohello консоли:</span><span class="sxs-lookup"><span data-stu-id="af67b-153">hello example in hello previous section used a method called `WriteDocuments` toooutput hello search results toohello console:</span></span>

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

<span data-ttu-id="af67b-154">Вот что hello результаты выглядят hello запросов в предыдущем разделе hello, если предполагается, что индекс гостиницы «hello» заполняется данными образец hello в [Здравствуйте, импорт данных в поиске Azure с помощью пакета SDK для .NET](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="af67b-154">Here is what hello results look like for hello queries in hello previous section, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search hello entire index for hello term 'budget' and return only hello hotelName field:

Name: Roach Motel

Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close tootown hall and hello river

Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search hello entire index for hello term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="af67b-155">Приведенный выше код образца Hello использует результаты поиска toooutput hello консоли.</span><span class="sxs-lookup"><span data-stu-id="af67b-155">hello sample code above uses hello console toooutput search results.</span></span> <span data-ttu-id="af67b-156">Аналогичным образом необходимо будет toodisplay результаты поиска в приложении.</span><span class="sxs-lookup"><span data-stu-id="af67b-156">You will likewise need toodisplay search results in your own application.</span></span> <span data-ttu-id="af67b-157">В разделе [этот пример на GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) пример отображением результатов поиска toorender в ASP.NET MVC веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="af67b-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how toorender search results in an ASP.NET MVC-based web application.</span></span>

