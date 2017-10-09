---
title: "AAA» запроса индекса (API REST - службы поиска Azure) | Документы Microsoft»"
description: "Построить запрос поиска в поиске Azure и использовать параметры сортировки и toofilter поиска результатов поиска."
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
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a><span data-ttu-id="dcba4-103">Запросить индекс поиска Azure с помощью API-интерфейса REST hello</span><span class="sxs-lookup"><span data-stu-id="dcba4-103">Query your Azure Search index using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="dcba4-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="dcba4-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="dcba4-105">Портал</span><span class="sxs-lookup"><span data-stu-id="dcba4-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="dcba4-106">.NET</span><span class="sxs-lookup"><span data-stu-id="dcba4-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="dcba4-107">REST</span><span class="sxs-lookup"><span data-stu-id="dcba4-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="dcba4-108">В этой статье показано, как hello индекса с помощью tooquery [REST API поиска Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="dcba4-108">This article shows you how tooquery an index using hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="dcba4-109">Прежде чем приступать к выполнению инструкций из этого руководства, необходимо [создать индекс службы поиска Azure](search-what-is-an-index.md) и [заполнить его данными](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="dcba4-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="dcba4-110">Общие сведения см. в статье [Как работает полнотекстовый поиск в службе поиска Azure](search-lucene-query-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="dcba4-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="dcba4-111">Определение ключа API запроса службы поиска Azure</span><span class="sxs-lookup"><span data-stu-id="dcba4-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="dcba4-112">Ключевым компонентом каждой операции поиска для hello REST API поиска Azure является hello *ключ api* , созданном для службы hello подготовке.</span><span class="sxs-lookup"><span data-stu-id="dcba4-112">A key component of every search operation against hello Azure Search REST API is hello *api-key* that was generated for hello service you provisioned.</span></span> <span data-ttu-id="dcba4-113">Наличие действительного ключа позволяет установить отношения доверия, для каждого запроса, между Отправка запроса hello hello приложения и службы hello, обрабатывает его.</span><span class="sxs-lookup"><span data-stu-id="dcba4-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="dcba4-114">toofind ключи api службы, вы сможете войти toohello [портал Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="dcba4-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="dcba4-115">Перейдите в колонку службы поиска Azure tooyour</span><span class="sxs-lookup"><span data-stu-id="dcba4-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="dcba4-116">Щелкните значок «Ключи» hello</span><span class="sxs-lookup"><span data-stu-id="dcba4-116">Click hello "Keys" icon</span></span>

<span data-ttu-id="dcba4-117">Ваша служба получит *ключи администратора* и *ключи запросов*.</span><span class="sxs-lookup"><span data-stu-id="dcba4-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="dcba4-118">Первичная и Вторичная *ключей администратора* предоставить полные права tooall операций, включая toomanage hello hello возможности службы, создания и удаления индексов, индексаторов и источников данных.</span><span class="sxs-lookup"><span data-stu-id="dcba4-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="dcba4-119">Существует два ключа, чтобы продолжить toouse hello вторичный ключ в случае tooregenerate hello первичного ключа и наоборот.</span><span class="sxs-lookup"><span data-stu-id="dcba4-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="dcba4-120">Ваш *запрос ключей* предоставить доступ только для чтения tooindexes и документы и представляют собой tooclient обычно распределенного приложения, издающие запросы поиска.</span><span class="sxs-lookup"><span data-stu-id="dcba4-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="dcba4-121">Запросы к индексу целях hello можно использовать один из ключей запроса.</span><span class="sxs-lookup"><span data-stu-id="dcba4-121">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="dcba4-122">Ключи администратора также может использоваться для запросов, но ключ запроса следует использовать в коде приложения, как это лучше отвечает hello [принципа наименьших прав доступа](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="dcba4-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="dcba4-123">Формулировка запроса</span><span class="sxs-lookup"><span data-stu-id="dcba4-123">Formulate your query</span></span>
<span data-ttu-id="dcba4-124">Существует два способа слишком[поиска индекса с помощью API-интерфейса REST hello](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="dcba4-124">There are two ways too[search your index using hello REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="dcba4-125">Один из способов — tooissue запрос HTTP POST, где определяются параметры запроса в объект JSON в теле запроса hello.</span><span class="sxs-lookup"><span data-stu-id="dcba4-125">One way is tooissue an HTTP POST request where your query parameters are defined in a JSON object in hello request body.</span></span> <span data-ttu-id="dcba4-126">Hello другим способом является tooissue запрос HTTP GET, где определяются параметры запроса в URL-адрес запроса hello.</span><span class="sxs-lookup"><span data-stu-id="dcba4-126">hello other way is tooissue an HTTP GET request where your query parameters are defined within hello request URL.</span></span> <span data-ttu-id="dcba4-127">POST имеет несколько [ослаблены ограничения](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) на размер hello параметров запроса от GET.</span><span class="sxs-lookup"><span data-stu-id="dcba4-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on hello size of query parameters than GET.</span></span> <span data-ttu-id="dcba4-128">Поэтому мы рекомендуем использовать запрос POST, за исключением особых случаев, когда удобнее использовать запрос GET.</span><span class="sxs-lookup"><span data-stu-id="dcba4-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="dcba4-129">Для POST и GET требуются tooprovide вашей *имя службы*, *имя индекса*и соответствующие hello *версия API* (hello текущая версия API — `2016-09-01` во время hello публикации в этом документе) URL-адрес запроса hello.</span><span class="sxs-lookup"><span data-stu-id="dcba4-129">For both POST and GET, you need tooprovide your *service name*, *index name*, and hello proper *API version* (hello current API version is `2016-09-01` at hello time of publishing this document) in hello request URL.</span></span> <span data-ttu-id="dcba4-130">GET, hello *строку запроса* hello конец hello URL-адреса является вам необходимо указать параметры запроса hello.</span><span class="sxs-lookup"><span data-stu-id="dcba4-130">For GET, hello *query string* at hello end of hello URL is where you provide hello query parameters.</span></span> <span data-ttu-id="dcba4-131">Ниже приведена hello формат URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="dcba4-131">See below for hello URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="dcba4-132">Hello формате для БЛОГА Здравствуйте, таким же, но с только api-version в hello параметры строки запроса.</span><span class="sxs-lookup"><span data-stu-id="dcba4-132">hello format for POST is hello same, but with only api-version in hello query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="dcba4-133">Примеры запросов</span><span class="sxs-lookup"><span data-stu-id="dcba4-133">Example Queries</span></span>
<span data-ttu-id="dcba4-134">Вот несколько примеров запросов к индексу с именем hotels.</span><span class="sxs-lookup"><span data-stu-id="dcba4-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="dcba4-135">Эти запросы отображаются в формате GET и POST.</span><span class="sxs-lookup"><span data-stu-id="dcba4-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="dcba4-136">Поиск hello термин «бюджет» Привет всем индексом и возвращать только hello `hotelName` поля:</span><span class="sxs-lookup"><span data-stu-id="dcba4-136">Search hello entire index for hello term 'budget' and return only hello `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="dcba4-137">Применить фильтр toohello индекс toofind гостиницы дешевле, чем 150 за ночь и вернуться hello `hotelId` и `description`:</span><span class="sxs-lookup"><span data-stu-id="dcba4-137">Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="dcba4-138">Всего индекса поиска hello, упорядочение по определенному полю (`lastRenovationDate`) по убыванию, принимают результаты двух верхних hello и Показать только `hotelName` и `lastRenovationDate`:</span><span class="sxs-lookup"><span data-stu-id="dcba4-138">Search hello entire index, order by a specific field (`lastRenovationDate`) in descending order, take hello top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

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

## <a name="submit-your-http-request"></a><span data-ttu-id="dcba4-139">Отправка HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="dcba4-139">Submit your HTTP request</span></span>
<span data-ttu-id="dcba4-140">Теперь, когда вы сформулировали запрос как часть URL-адреса HTTP-запроса (для GET) или основного текста (для POST), можно определить заголовки запроса и отправить запрос.</span><span class="sxs-lookup"><span data-stu-id="dcba4-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="dcba4-141">Запрос и заголовки запроса</span><span class="sxs-lookup"><span data-stu-id="dcba4-141">Request and Request Headers</span></span>
<span data-ttu-id="dcba4-142">Необходимо определить два заголовка запроса для GET или три — для POST:</span><span class="sxs-lookup"><span data-stu-id="dcba4-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="dcba4-143">Hello `api-key` заголовка должно быть установлено toohello ключа запроса, определенные в действии я выше.</span><span class="sxs-lookup"><span data-stu-id="dcba4-143">hello `api-key` header must be set toohello query key you found in step I above.</span></span> <span data-ttu-id="dcba4-144">Можно также использовать ключ администратора как hello `api-key` заголовок, но рекомендуется использовать ключ запроса, так как он только предоставляет tooindexes доступ только для чтения и документы.</span><span class="sxs-lookup"><span data-stu-id="dcba4-144">You can also use an admin key as hello `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access tooindexes and documents.</span></span>
2. <span data-ttu-id="dcba4-145">Hello `Accept` заголовка должно быть установлено слишком`application/json`.</span><span class="sxs-lookup"><span data-stu-id="dcba4-145">hello `Accept` header must be set too`application/json`.</span></span>
3. <span data-ttu-id="dcba4-146">POST, hello `Content-Type` заголовок также должен быть установлен слишком`application/json`.</span><span class="sxs-lookup"><span data-stu-id="dcba4-146">For POST only, hello `Content-Type` header should also be set too`application/json`.</span></span>

<span data-ttu-id="dcba4-147">Ниже приведена HTTP GET запроса toosearch hello «гостиницы» индекса при помощи hello REST API поиска Azure, с помощью простой запрос, который выполняет поиск hello термин «motel»:</span><span class="sxs-lookup"><span data-stu-id="dcba4-147">See below for an HTTP GET request toosearch hello "hotels" index using hello Azure Search REST API, using a simple query that searches for hello term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="dcba4-148">Вот hello же пример запроса, в настоящее время с помощью HTTP POST:</span><span class="sxs-lookup"><span data-stu-id="dcba4-148">Here is hello same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="dcba4-149">Код состояния запроса успешный запрос приведет к `200 OK` и hello результаты поиска возвращаются в виде JSON в теле ответа hello.</span><span class="sxs-lookup"><span data-stu-id="dcba4-149">A successful query request will result in a Status Code of `200 OK` and hello search results are returned as JSON in hello response body.</span></span> <span data-ttu-id="dcba4-150">Вот какие hello результаты для hello выше запрос, как будет выглядеть, при условии, что индекс гостиницы «hello» заполняется данными образец hello в [Здравствуйте, импорт данных в поиске Azure с помощью API-интерфейса REST](search-import-data-rest-api.md) (Обратите внимание, что hello JSON был отформатирован для ясности).</span><span class="sxs-lookup"><span data-stu-id="dcba4-150">Here is what hello results for hello above query look like, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello REST API](search-import-data-rest-api.md) (note that hello JSON has been formatted for clarity).</span></span>

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

<span data-ttu-id="dcba4-151">toolearn, посетите раздел «Ответ» hello [поиск документов](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="dcba4-151">toolearn more, please visit hello "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="dcba4-152">Дополнительные сведения о других кодах состояния HTTP, которые могут быть возвращены в случае сбоя, см. в статье [Коды состояния HTTP (поиск Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="dcba4-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
