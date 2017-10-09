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
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a>Запросить индекс поиска Azure с помощью hello .NET SDK
> [!div class="op_single_selector"]
> * [Обзор](search-query-overview.md)
> * [Портал](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

В этой статье мы покажем, как hello индекса с помощью tooquery [пакет SDK Azure Search .NET](https://aka.ms/search-sdk).

Прежде чем приступать к выполнению инструкций из этого руководства, необходимо [создать индекс службы поиска Azure](search-what-is-an-index.md) и [заполнить его данными](search-what-is-data-import.md).

> [!NOTE]
> Все приведенные здесь примеры кода написаны на языке C#. Можно найти полный исходный код hello [на GitHub](http://aka.ms/search-dotnet-howto). Вы также можете прочесть об hello [пакет SDK Azure Search .NET](search-howto-dotnet-sdk.md) для более подробные руководства по hello примеров кода.

## <a name="identify-your-azure-search-services-query-api-key"></a>Определение ключа API запроса службы поиска Azure
Теперь, создав индекс поиска Azure, все почти готово tooissue запросы, использующие hello .NET SDK. Во-первых необходимо будет tooobtain один hello ключей api запросов, которые были созданы для подготовленной службы поиска hello. Hello .NET SDK будет отправлять этот ключ api для каждой службы tooyour запроса. Наличие действительного ключа позволяет установить отношения доверия, для каждого запроса, между Отправка запроса hello hello приложения и службы hello, обрабатывает его.

1. toofind ключи api службы, вы сможете войти в toohello [портал Azure](https://portal.azure.com/)
2. Перейдите в колонку службы поиска Azure tooyour
3. Щелкните значок «Ключи» hello

Ваша служба получит *ключи администратора* и *ключи запросов*.

* Первичная и Вторичная *ключей администратора* предоставить полные права tooall операций, включая toomanage hello hello возможности службы, создания и удаления индексов, индексаторов и источников данных. Существует два ключа, чтобы продолжить toouse hello вторичный ключ в случае tooregenerate hello первичного ключа и наоборот.
* Ваш *запрос ключей* предоставить доступ только для чтения tooindexes и документы и представляют собой tooclient обычно распределенного приложения, издающие запросы поиска.

Запросы к индексу целях hello можно использовать один из ключей запроса. Ключи администратора также может использоваться для запросов, но ключ запроса следует использовать в коде приложения, как это лучше отвечает hello [принципа наименьших прав доступа](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Создайте экземпляр класса SearchIndexClient hello
tooissue запросы с hello пакет SDK Azure Search .NET, вам потребуется toocreate экземпляр hello `SearchIndexClient` класса. Этот класс имеет несколько конструкторов. Hello один требуется принимает имя службы поиска, имя индекса и `SearchCredentials` объект в качестве параметров. `SearchCredentials` содержит ключ API.

Приведенный ниже код Hello создает новый `SearchIndexClient` для индекса «гостиницы» hello (созданных в [создать индекс поиска Azure с помощью hello пакета SDK для .NET](search-create-index-dotnet.md)) с использованием значений для hello имя службы поиска и ключ api, которые хранятся в файле конфигурации приложения hello файл (`appsettings.json` в случае, когда hello hello [образец приложения](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

У класса `SearchIndexClient` есть свойство `Documents`. Это свойство предоставляет все hello методы должна tooquery индексах поиска Azure.

## <a name="query-your-index"></a>Отправка запроса в индекс
Поиск с использованием hello .NET SDK сводится вызывающему Привет `Documents.Search` метод вашей `SearchIndexClient`. Этот метод принимает несколько параметров, включая текст поиска hello, вместе с `SearchParameters` объект, который может использоваться используется toofurther уточнение hello запрос.

#### <a name="types-of-queries"></a>Типы запросов
Hello двух main [типами запросов](search-query-overview.md#types-of-queries) используется являются `search` и `filter`. Запрос `search` выполняет поиск по одному или нескольким условиям во всех *поддерживающих поиск* полях индекса. Запрос `filter` оценивает логическое выражение во всех *фильтруемых* полях индекса.

Поиск и фильтры выполняются с использованием hello `Documents.Search` метод. Запрос поиска можно передать в hello `searchText` параметра, а критерий фильтра может быть передан в hello `Filter` свойство hello `SearchParameters` класса. toofilter без поиска, просто передать `"*"` для hello `searchText` параметра. toosearch без фильтрации, просто оставьте hello `Filter` свойство не задано, или не передавайте в `SearchParameters` экземпляра вообще.

#### <a name="example-queries"></a>Примеры запросов
Следующий образец кода Hello показано несколько способов hello tooquery «гостиницы «индекс определен в [создать индекс поиска Azure с помощью hello .NET SDK](search-create-index-dotnet.md#DefineIndex). Обратите внимание, что hello документов, возвращаемых с результатами поиска hello экземпляров hello `Hotel` класс, который был определен в [Здравствуйте, импорт данных в поиске Azure с помощью пакета SDK для .NET](search-import-data-dotnet.md#HotelClass). Здравствуйте, пример кода использует `WriteDocuments` toohello метод toooutput hello поиска результатов консоли. Этот метод описан в следующем разделе hello.

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

## <a name="handle-search-results"></a>Обработка результатов поиска
Hello `Documents.Search` возвращает метод `DocumentSearchResult` , содержащий результаты запроса hello hello. пример Hello в предыдущем разделе hello использовать метод с именем `WriteDocuments` toooutput hello поиска результаты toohello консоли:

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

Вот что hello результаты выглядят hello запросов в предыдущем разделе hello, если предполагается, что индекс гостиницы «hello» заполняется данными образец hello в [Здравствуйте, импорт данных в поиске Azure с помощью пакета SDK для .NET](search-import-data-dotnet.md):

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

Приведенный выше код образца Hello использует результаты поиска toooutput hello консоли. Аналогичным образом необходимо будет toodisplay результаты поиска в приложении. В разделе [этот пример на GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) пример отображением результатов поиска toorender в ASP.NET MVC веб-приложения.

