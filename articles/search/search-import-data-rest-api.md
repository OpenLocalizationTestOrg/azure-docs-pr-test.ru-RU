---
title: "AAA» передачи данных (REST API - службы поиска Azure) | Документы Microsoft»"
description: "Узнайте, как индекс tooan tooupload данных в поиске Azure с помощью hello REST API."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a><span data-ttu-id="a2f15-103">Здравствуйте, передачи данных tooAzure поиска с помощью API-интерфейса REST</span><span class="sxs-lookup"><span data-stu-id="a2f15-103">Upload data tooAzure Search using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="a2f15-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a2f15-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="a2f15-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a2f15-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="a2f15-106">REST</span><span class="sxs-lookup"><span data-stu-id="a2f15-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="a2f15-107">В этой статье будет показано, как toouse hello [REST API поиска Azure](https://docs.microsoft.com/rest/api/searchservice/) tooimport данных в индекс поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="a2f15-107">This article will show you how toouse hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="a2f15-108">Прежде чем приступать к выполнению инструкций из этого руководства, вам нужно [создать индекс службы поиска Azure](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="a2f15-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="a2f15-109">В порядке toopush документов в индекс с помощью API-интерфейса REST hello будут выдаваться конечная точка индекса запрос HTTP POST tooyour URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a2f15-109">In order toopush documents into your index using hello REST API, you will issue an HTTP POST request tooyour index's URL endpoint.</span></span> <span data-ttu-id="a2f15-110">текст Hello hello HTTP-запроса, что текст является объект JSON, содержащий документы hello toobe добавлены, изменены или удалены.</span><span class="sxs-lookup"><span data-stu-id="a2f15-110">hello body of hello HTTP request body is a JSON object containing hello documents toobe added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="a2f15-111">Определение ключа API администратора службы поиска Azure</span><span class="sxs-lookup"><span data-stu-id="a2f15-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="a2f15-112">При выдаче HTTP-запросы к службе с помощью REST API hello *каждого* API запрос должен включать hello api ключ, созданный для hello подготовке службы поиска.</span><span class="sxs-lookup"><span data-stu-id="a2f15-112">When issuing HTTP requests against your service using hello REST API, *each* API request must include hello api-key that was generated for hello Search service you provisioned.</span></span> <span data-ttu-id="a2f15-113">Наличие действительного ключа позволяет установить отношения доверия, для каждого запроса, между Отправка запроса hello hello приложения и службы hello, обрабатывает его.</span><span class="sxs-lookup"><span data-stu-id="a2f15-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="a2f15-114">toofind ключи api службы, вы сможете войти toohello [портал Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="a2f15-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="a2f15-115">Перейдите в колонку службы поиска Azure tooyour</span><span class="sxs-lookup"><span data-stu-id="a2f15-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="a2f15-116">Щелкните значок «Ключи» hello</span><span class="sxs-lookup"><span data-stu-id="a2f15-116">Click on hello "Keys" icon</span></span>

<span data-ttu-id="a2f15-117">Ваша служба получит *ключи администратора* и *ключи запросов*.</span><span class="sxs-lookup"><span data-stu-id="a2f15-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="a2f15-118">Первичная и Вторичная *ключей администратора* предоставить полные права tooall операций, включая toomanage hello hello возможности службы, создания и удаления индексов, индексаторов и источников данных.</span><span class="sxs-lookup"><span data-stu-id="a2f15-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="a2f15-119">Существует два ключа, чтобы продолжить toouse hello вторичный ключ в случае tooregenerate hello первичного ключа и наоборот.</span><span class="sxs-lookup"><span data-stu-id="a2f15-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="a2f15-120">Ваш *запрос ключей* предоставить доступ только для чтения tooindexes и документы и представляют собой tooclient обычно распределенного приложения, издающие запросы поиска.</span><span class="sxs-lookup"><span data-stu-id="a2f15-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="a2f15-121">Импорт данных в индекс целях hello, можно использовать ключ администратора первичной или вторичной.</span><span class="sxs-lookup"><span data-stu-id="a2f15-121">For hello purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="a2f15-122">Решите, какие индексирования toouse действие</span><span class="sxs-lookup"><span data-stu-id="a2f15-122">Decide which indexing action toouse</span></span>
<span data-ttu-id="a2f15-123">При использовании REST API hello, URL-адрес конечной точки JSON запроса тел tooyour индекс поиска Azure будут выдаваться HTTP-запросы POST.</span><span class="sxs-lookup"><span data-stu-id="a2f15-123">When using hello REST API, you will issue HTTP POST requests with JSON request bodies tooyour Azure Search index's endpoint URL.</span></span> <span data-ttu-id="a2f15-124">объект JSON Hello в тексте запроса HTTP будет содержать один массив JSON с именем «value», содержащий JSON объектов, представляющих документы хотелось бы tooadd tooyour индекс, обновить или удалить.</span><span class="sxs-lookup"><span data-stu-id="a2f15-124">hello JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like tooadd tooyour index, update, or delete.</span></span>

<span data-ttu-id="a2f15-125">Каждый объект JSON в массиве «value» hello представляет toobe документа, в индекс.</span><span class="sxs-lookup"><span data-stu-id="a2f15-125">Each JSON object in hello "value" array represents a document toobe indexed.</span></span> <span data-ttu-id="a2f15-126">Каждый из этих объектов содержит ключ документа hello и действие hello требуемого индексирования (отправка, слияние, удаление, и т. д).</span><span class="sxs-lookup"><span data-stu-id="a2f15-126">Each of these objects contains hello document's key and specifies hello desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="a2f15-127">В зависимости от того, какой из hello следующие действия, которые можно выбрать только определенные поля должны быть включены для каждого документа:</span><span class="sxs-lookup"><span data-stu-id="a2f15-127">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="a2f15-128">Описание</span><span class="sxs-lookup"><span data-stu-id="a2f15-128">Description</span></span> | <span data-ttu-id="a2f15-129">Необходимые поля для каждого документа</span><span class="sxs-lookup"><span data-stu-id="a2f15-129">Necessary fields for each document</span></span> | <span data-ttu-id="a2f15-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="a2f15-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="a2f15-131">`upload` Действие — примерно tooan «вставки-обновления» где документ hello будет вставлена, если является новым и обновлен или заменен, если он существует.</span><span class="sxs-lookup"><span data-stu-id="a2f15-131">An `upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="a2f15-132">ключ, а также другие поля, нужно toodefine</span><span class="sxs-lookup"><span data-stu-id="a2f15-132">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="a2f15-133">При обновлении или замене существующего документа, любое поле, которое не указано в запросе hello будет иметь слишком его поле`null`.</span><span class="sxs-lookup"><span data-stu-id="a2f15-133">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="a2f15-134">Это происходит даже в том случае, если поле hello было установлено ранее tooa непустое значение.</span><span class="sxs-lookup"><span data-stu-id="a2f15-134">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `merge` |<span data-ttu-id="a2f15-135">Обновления, существующий документ с hello указаны поля.</span><span class="sxs-lookup"><span data-stu-id="a2f15-135">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="a2f15-136">Если документ hello не существует в индексе hello, hello слияния завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="a2f15-136">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="a2f15-137">ключ, а также другие поля, нужно toodefine</span><span class="sxs-lookup"><span data-stu-id="a2f15-137">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="a2f15-138">Любое поле, указанное для объединения приведет к замене существующего поля hello в документе hello.</span><span class="sxs-lookup"><span data-stu-id="a2f15-138">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="a2f15-139">Это относится и к полям типа `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="a2f15-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="a2f15-140">Например, если hello документ содержит поле `tags` со значением `["budget"]` , и вы выполните объединение со значением `["economy", "pool"]` для `tags`, hello окончательное значение hello `tags` поле будет `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="a2f15-140">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="a2f15-141">а не `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="a2f15-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="a2f15-142">Это действие ведет себя как `merge` Если документ с hello заданным ключом уже существует в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="a2f15-142">This action behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="a2f15-143">Если документ hello не существует, он ведет себя как `upload` с новым документом.</span><span class="sxs-lookup"><span data-stu-id="a2f15-143">If hello document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="a2f15-144">ключ, а также другие поля, нужно toodefine</span><span class="sxs-lookup"><span data-stu-id="a2f15-144">key, plus any other fields you wish toodefine</span></span> |- |
| `delete` |<span data-ttu-id="a2f15-145">Удаляет указанный документ hello из индекса hello.</span><span class="sxs-lookup"><span data-stu-id="a2f15-145">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="a2f15-146">Только ключ</span><span class="sxs-lookup"><span data-stu-id="a2f15-146">key only</span></span> |<span data-ttu-id="a2f15-147">Все поля, укажите вместо hello ключевое поле будет игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="a2f15-147">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="a2f15-148">Tooremove отдельного поля из документа, используйте `merge` вместо и просто задать поле hello явно toonull.</span><span class="sxs-lookup"><span data-stu-id="a2f15-148">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly toonull.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="a2f15-149">Создание HTTP-запроса и текста запроса</span><span class="sxs-lookup"><span data-stu-id="a2f15-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="a2f15-150">Теперь, когда собранные значения hello необходимые поля для действий индекса, будут готовы tooconstruct hello самого запроса HTTP и JSON запроса текст tooimport данных.</span><span class="sxs-lookup"><span data-stu-id="a2f15-150">Now that you have gathered hello necessary field values for your index actions, you are ready tooconstruct hello actual HTTP request and JSON request body tooimport your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="a2f15-151">Запрос и заголовки запроса</span><span class="sxs-lookup"><span data-stu-id="a2f15-151">Request and Request Headers</span></span>
<span data-ttu-id="a2f15-152">В URL-адрес hello, нужно будет tooprovide на имя службы, имя индекса («гостиницы» в данном случае), а также hello правильную версию API (текущая версия API hello `2016-09-01` во время публикации в этом документе hello).</span><span class="sxs-lookup"><span data-stu-id="a2f15-152">In hello URL, you will need tooprovide your service name, index name ("hotels" in this case), as well as hello proper API version (hello current API version is `2016-09-01` at hello time of publishing this document).</span></span> <span data-ttu-id="a2f15-153">Вам потребуется toodefine hello `Content-Type` и `api-key` заголовки запроса.</span><span class="sxs-lookup"><span data-stu-id="a2f15-153">You will need toodefine hello `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="a2f15-154">В последнем hello можно используйте один из ключей администратора службы.</span><span class="sxs-lookup"><span data-stu-id="a2f15-154">For hello latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="a2f15-155">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="a2f15-155">Request Body</span></span>
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="a2f15-156">В этом примере мы используем операции `upload`, `mergeOrUpload` и `delete` в качестве операций поиска.</span><span class="sxs-lookup"><span data-stu-id="a2f15-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="a2f15-157">Предположим, что пример индекса с именем hotels уже заполнен несколькими документами.</span><span class="sxs-lookup"><span data-stu-id="a2f15-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="a2f15-158">Обратите внимание на то, как бы не было toospecify все поля hello возможных документа при использовании `mergeOrUpload` и как мы указан только ключ документа hello (`hotelId`) при использовании `delete`.</span><span class="sxs-lookup"><span data-stu-id="a2f15-158">Note how we did not have toospecify all hello possible document fields when using `mergeOrUpload` and how we only specified hello document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="a2f15-159">Кроме того Обратите внимание, что может включать только документы too1000 (или 16 МБ) в одном запросе индексирования.</span><span class="sxs-lookup"><span data-stu-id="a2f15-159">Also, note that you can only include up too1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="a2f15-160">Анализ кода HTTP-ответа</span><span class="sxs-lookup"><span data-stu-id="a2f15-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="a2f15-161">200</span><span class="sxs-lookup"><span data-stu-id="a2f15-161">200</span></span>
<span data-ttu-id="a2f15-162">После успешной отправки запроса на индексирование вы получите HTTP-ответ с кодом состояния `200 OK`.</span><span class="sxs-lookup"><span data-stu-id="a2f15-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="a2f15-163">Hello JSON-тексте hello HTTP-ответа будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a2f15-163">hello JSON body of hello HTTP response will be as follows:</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a><span data-ttu-id="a2f15-164">207</span><span class="sxs-lookup"><span data-stu-id="a2f15-164">207</span></span>
<span data-ttu-id="a2f15-165">Код состояния `207` возвращается, если хотя бы один элемент не удалось проиндексировать.</span><span class="sxs-lookup"><span data-stu-id="a2f15-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="a2f15-166">Hello JSON-тексте hello HTTP-ответа будет содержать сведения о неудачных документов hello.</span><span class="sxs-lookup"><span data-stu-id="a2f15-166">hello JSON body of hello HTTP response will contain information about hello unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> <span data-ttu-id="a2f15-167">Часто это означает, что hello нагрузки на поиск службы достижение точки, где запросы индексирования начнутся tooreturn `503` ответов.</span><span class="sxs-lookup"><span data-stu-id="a2f15-167">This often means that hello load on your search service is reaching a point where indexing requests will begin tooreturn `503` responses.</span></span> <span data-ttu-id="a2f15-168">В таком случае мы настоятельно рекомендуем задержать выполнение клиентского кода и повторить попытку позже.</span><span class="sxs-lookup"><span data-stu-id="a2f15-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="a2f15-169">Это позволит получить hello системы toorecover некоторое время, увеличить вероятность hello будущие запросы будут выполнены успешно.</span><span class="sxs-lookup"><span data-stu-id="a2f15-169">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="a2f15-170">Быстрое повторение запросов только продлит проблемную ситуацию hello.</span><span class="sxs-lookup"><span data-stu-id="a2f15-170">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="a2f15-171">429</span><span class="sxs-lookup"><span data-stu-id="a2f15-171">429</span></span>
<span data-ttu-id="a2f15-172">Код состояния `429` будет возвращаться при превысили квоту на число hello документов в индекс.</span><span class="sxs-lookup"><span data-stu-id="a2f15-172">A status code of `429` will be returned when you have exceeded your quota on hello number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="a2f15-173">503</span><span class="sxs-lookup"><span data-stu-id="a2f15-173">503</span></span>
<span data-ttu-id="a2f15-174">Код состояния `503` будет возвращено, если ни один из элементов hello в запросе hello были успешно проиндексированы.</span><span class="sxs-lookup"><span data-stu-id="a2f15-174">A status code of `503` will be returned if none of hello items in hello request were successfully indexed.</span></span> <span data-ttu-id="a2f15-175">Эта ошибка означает, что является hello системы находящейся под интенсивной нагрузкой, и в настоящее время не удается обработать ваш запрос.</span><span class="sxs-lookup"><span data-stu-id="a2f15-175">This error means that hello system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="a2f15-176">В таком случае мы настоятельно рекомендуем задержать выполнение клиентского кода и повторить попытку позже.</span><span class="sxs-lookup"><span data-stu-id="a2f15-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="a2f15-177">Это позволит получить hello системы toorecover некоторое время, увеличить вероятность hello будущие запросы будут выполнены успешно.</span><span class="sxs-lookup"><span data-stu-id="a2f15-177">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="a2f15-178">Быстрое повторение запросов только продлит проблемную ситуацию hello.</span><span class="sxs-lookup"><span data-stu-id="a2f15-178">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

<span data-ttu-id="a2f15-179">Дополнительные сведения о действиях с документами и ответах об успешном выполнении и ошибках см. в статье, посвященной [добавлению, обновлению и удалению документов](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span><span class="sxs-lookup"><span data-stu-id="a2f15-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="a2f15-180">Дополнительные сведения о других кодах состояния HTTP, которые могут быть возвращены в случае сбоя, см. в статье [Коды состояния HTTP (поиск Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="a2f15-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2f15-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a2f15-181">Next steps</span></span>
<span data-ttu-id="a2f15-182">После заполнения индекса поиска Azure, будет готов toostart выдача запросов toosearch для документов.</span><span class="sxs-lookup"><span data-stu-id="a2f15-182">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="a2f15-183">Дополнительные сведения см. в статье [Запросы в службе поиска Azure](search-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2f15-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
