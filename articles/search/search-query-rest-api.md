---
title: "Отправка запросов в индекс службы поиска Azure с помощью REST API | Документация Майкрософт"
description: "В службе поиска Azure можно создавать поисковые запросы и с помощью параметров поиска фильтровать, сортировать и уточнять результаты."
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 49062bec233ad35cd457f9665fa94c1855343582
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="query-your-azure-search-index-using-the-rest-api"></a><span data-ttu-id="09c78-103">Отправка запросов в индекс службы поиска Azure с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="09c78-103">Query your Azure Search index using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="09c78-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="09c78-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="09c78-105">Портал</span><span class="sxs-lookup"><span data-stu-id="09c78-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="09c78-106">.NET</span><span class="sxs-lookup"><span data-stu-id="09c78-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="09c78-107">REST</span><span class="sxs-lookup"><span data-stu-id="09c78-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="09c78-108">В этой статье мы расскажем, как создать запрос к индексу с помощью [REST API службы поиска Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="09c78-108">This article shows you how to query an index using the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="09c78-109">Прежде чем приступать к выполнению инструкций из этого руководства, необходимо [создать индекс службы поиска Azure](search-what-is-an-index.md) и [заполнить его данными](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="09c78-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="09c78-110">Общие сведения см. в статье [Как работает полнотекстовый поиск в службе поиска Azure](search-lucene-query-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="09c78-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="09c78-111">Определение ключа API запроса службы поиска Azure</span><span class="sxs-lookup"><span data-stu-id="09c78-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="09c78-112">Ключевым компонентом каждой операции поиска с REST API службы поиска Azure является *ключ API* , созданный для службы, которую вы подготовили.</span><span class="sxs-lookup"><span data-stu-id="09c78-112">A key component of every search operation against the Azure Search REST API is the *api-key* that was generated for the service you provisioned.</span></span> <span data-ttu-id="09c78-113">Если есть действительный ключ, для каждого запроса устанавливаются отношения доверия между приложением, которое отправляет запрос, и службой, которая его обрабатывает.</span><span class="sxs-lookup"><span data-stu-id="09c78-113">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="09c78-114">Чтобы найти ключи API своей службы, войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="09c78-114">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="09c78-115">Перейдите к колонке службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="09c78-115">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="09c78-116">Щелкните значок "Ключи".</span><span class="sxs-lookup"><span data-stu-id="09c78-116">Click the "Keys" icon</span></span>

<span data-ttu-id="09c78-117">Ваша служба получит *ключи администратора* и *ключи запросов*.</span><span class="sxs-lookup"><span data-stu-id="09c78-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="09c78-118">Первичные и вторичные *ключи администратора* предоставляют полный доступ ко всем операциям, включая возможность управлять службой, создавать и удалять индексы, индексаторы и источники данных.</span><span class="sxs-lookup"><span data-stu-id="09c78-118">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="09c78-119">Ключей два, поэтому вы можете и дальше использовать вторичный ключ, если решите повторно создать первичный ключ, и наоборот.</span><span class="sxs-lookup"><span data-stu-id="09c78-119">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="09c78-120">*Ключи запросов* предоставляют только разрешение на чтение индексов и документов; обычно они добавляются в клиентские приложения, которые создают запросы на поиск.</span><span class="sxs-lookup"><span data-stu-id="09c78-120">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="09c78-121">Для отправки запросов в индекс можно использовать один из ключей запросов.</span><span class="sxs-lookup"><span data-stu-id="09c78-121">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="09c78-122">Для запросов можно использовать также ключи администратора, но в коде приложения следует использовать ключ запроса, так как этот вариант лучше соответствует [принципу предоставления минимальных прав](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="09c78-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="09c78-123">Формулировка запроса</span><span class="sxs-lookup"><span data-stu-id="09c78-123">Formulate your query</span></span>
<span data-ttu-id="09c78-124">Существует два способа [поиска в индексе с помощью REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="09c78-124">There are two ways to [search your index using the REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="09c78-125">Один из них — отправка HTTP-запроса POST с текстом, содержащим объект JSON, в котором определены параметры запроса.</span><span class="sxs-lookup"><span data-stu-id="09c78-125">One way is to issue an HTTP POST request where your query parameters are defined in a JSON object in the request body.</span></span> <span data-ttu-id="09c78-126">Другой способ — отправка HTTP-запроса GET, содержащего URL-адрес, в котором определены параметры запроса.</span><span class="sxs-lookup"><span data-stu-id="09c78-126">The other way is to issue an HTTP GET request where your query parameters are defined within the request URL.</span></span> <span data-ttu-id="09c78-127">Обратите внимание, что в запросе POST предусмотрены [менее жесткие ограничения](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) на размер параметров запроса, чем в запросе GET.</span><span class="sxs-lookup"><span data-stu-id="09c78-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on the size of query parameters than GET.</span></span> <span data-ttu-id="09c78-128">Поэтому мы рекомендуем использовать запрос POST, за исключением особых случаев, когда удобнее использовать запрос GET.</span><span class="sxs-lookup"><span data-stu-id="09c78-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="09c78-129">Как для POST, так и для GET в URL-адресе запроса необходимо указать *имя службы*, *имя индекса*, а также правильную *версию API* (текущая версия API на момент публикации этого документа — `2016-09-01`).</span><span class="sxs-lookup"><span data-stu-id="09c78-129">For both POST and GET, you need to provide your *service name*, *index name*, and the proper *API version* (the current API version is `2016-09-01` at the time of publishing this document) in the request URL.</span></span> <span data-ttu-id="09c78-130">Если вы используете запрос GET, его параметры указываются в *строке запроса* в конце URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="09c78-130">For GET, the *query string* at the end of the URL is where you provide the query parameters.</span></span> <span data-ttu-id="09c78-131">Ниже приведен формат URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="09c78-131">See below for the URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="09c78-132">Формат для POST такой же, но в параметрах в строке запроса указывается только версия API.</span><span class="sxs-lookup"><span data-stu-id="09c78-132">The format for POST is the same, but with only api-version in the query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="09c78-133">Примеры запросов</span><span class="sxs-lookup"><span data-stu-id="09c78-133">Example Queries</span></span>
<span data-ttu-id="09c78-134">Вот несколько примеров запросов к индексу с именем hotels.</span><span class="sxs-lookup"><span data-stu-id="09c78-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="09c78-135">Эти запросы отображаются в формате GET и POST.</span><span class="sxs-lookup"><span data-stu-id="09c78-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="09c78-136">Здесь выполняется поиск термина budget по всему индексу и возвращается только поле `hotelName`.</span><span class="sxs-lookup"><span data-stu-id="09c78-136">Search the entire index for the term 'budget' and return only the `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="09c78-137">Примените фильтр к индексу, чтобы найти гостиницы с номерами дешевле 150 долларов США за ночь, и получите значения `hotelId` и `description`.</span><span class="sxs-lookup"><span data-stu-id="09c78-137">Apply a filter to the index to find hotels cheaper than $150 per night, and return the `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="09c78-138">Здесь выполняются поиск по всему индексу и сортировка по полю `lastRenovationDate` в порядке убывания, выбираются два первых результата и отображаются только значения `hotelName` и `lastRenovationDate`.</span><span class="sxs-lookup"><span data-stu-id="09c78-138">Search the entire index, order by a specific field (`lastRenovationDate`) in descending order, take the top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a><span data-ttu-id="09c78-139">Отправка HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="09c78-139">Submit your HTTP request</span></span>
<span data-ttu-id="09c78-140">Теперь, когда вы сформулировали запрос как часть URL-адреса HTTP-запроса (для GET) или основного текста (для POST), можно определить заголовки запроса и отправить запрос.</span><span class="sxs-lookup"><span data-stu-id="09c78-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="09c78-141">Запрос и заголовки запроса</span><span class="sxs-lookup"><span data-stu-id="09c78-141">Request and Request Headers</span></span>
<span data-ttu-id="09c78-142">Необходимо определить два заголовка запроса для GET или три — для POST:</span><span class="sxs-lookup"><span data-stu-id="09c78-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="09c78-143">В заголовке `api-key` должно быть задано значение ключа запроса, определенное на шаге 1 выше.</span><span class="sxs-lookup"><span data-stu-id="09c78-143">The `api-key` header must be set to the query key you found in step I above.</span></span> <span data-ttu-id="09c78-144">Хотя в качестве заголовка `api-key` подходит и ключ администратора, рекомендуется использовать ключ запроса, так как он предоставляет доступ к индексам и документам только с правами на чтение.</span><span class="sxs-lookup"><span data-stu-id="09c78-144">You can also use an admin key as the `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access to indexes and documents.</span></span>
2. <span data-ttu-id="09c78-145">В заголовке `Accept` должно быть задано значение `application/json`.</span><span class="sxs-lookup"><span data-stu-id="09c78-145">The `Accept` header must be set to `application/json`.</span></span>
3. <span data-ttu-id="09c78-146">Только для запросов POST: в заголовке `Content-Type` тоже должно быть задано значение `application/json`.</span><span class="sxs-lookup"><span data-stu-id="09c78-146">For POST only, the `Content-Type` header should also be set to `application/json`.</span></span>

<span data-ttu-id="09c78-147">Ниже приведен HTTP-запрос GET для поиска по индексу hotels с использованием REST API службы поиска Azure и простого запроса, который ищет термин motel.</span><span class="sxs-lookup"><span data-stu-id="09c78-147">See below for an HTTP GET request to search the "hotels" index using the Azure Search REST API, using a simple query that searches for the term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="09c78-148">Вот тот же пример запроса, но на этот раз используется HTTP-запрос POST:</span><span class="sxs-lookup"><span data-stu-id="09c78-148">Here is the same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="09c78-149">При успешном выполнении запроса возвращается код состояния `200 OK` , а результаты поиска возвращаются в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="09c78-149">A successful query request will result in a Status Code of `200 OK` and the search results are returned as JSON in the response body.</span></span> <span data-ttu-id="09c78-150">Вот так выглядят результаты приведенного выше запроса при условии, что индекс hotels заполнен примерами данных из статьи [Импорт данных в службе поиска Azure с помощью REST API](search-import-data-rest-api.md) (код JSON отформатирован для наглядности).</span><span class="sxs-lookup"><span data-stu-id="09c78-150">Here is what the results for the above query look like, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the REST API](search-import-data-rest-api.md) (note that the JSON has been formatted for clarity).</span></span>

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

<span data-ttu-id="09c78-151">Дополнительные сведения см. в статье [Поиск документов (REST API службы поиска Azure)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) в разделе "Ответ".</span><span class="sxs-lookup"><span data-stu-id="09c78-151">To learn more, please visit the "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="09c78-152">Дополнительные сведения о других кодах состояния HTTP, которые могут быть возвращены в случае сбоя, см. в статье [Коды состояния HTTP (поиск в Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="09c78-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
