---
title: "Отправка данных в службу поиска Azure c помощью REST API | Документация Майкрософт"
description: "Узнайте, как отправлять данные в индекс службы поиска Azure с помощью REST API."
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
ms.openlocfilehash: f22a33ed86fbfc46dfa732239263a49f34c4afee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-rest-api"></a><span data-ttu-id="3d76c-103">Отправка данных в службу поиска Azure с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="3d76c-103">Upload data to Azure Search using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="3d76c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="3d76c-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="3d76c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="3d76c-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="3d76c-106">REST</span><span class="sxs-lookup"><span data-stu-id="3d76c-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="3d76c-107">В этой статье объясняется, как использовать [REST API службы поиска Azure](https://docs.microsoft.com/rest/api/searchservice/) для импорта данных в индекс службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="3d76c-107">This article will show you how to use the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) to import data into an Azure Search index.</span></span>

<span data-ttu-id="3d76c-108">Прежде чем приступать к выполнению инструкций из этого руководства, вам нужно [создать индекс службы поиска Azure](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="3d76c-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="3d76c-109">Для передачи документов в индекс с помощью REST API вам нужно отправить HTTP-запрос POST на URL-адрес конечной точки индекса.</span><span class="sxs-lookup"><span data-stu-id="3d76c-109">In order to push documents into your index using the REST API, you will issue an HTTP POST request to your index's URL endpoint.</span></span> <span data-ttu-id="3d76c-110">Текст HTTP-запроса является объектом JSON, который содержит документы для добавления, изменения или удаления.</span><span class="sxs-lookup"><span data-stu-id="3d76c-110">The body of the HTTP request body is a JSON object containing the documents to be added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="3d76c-111">Определение ключа API администратора службы поиска Azure</span><span class="sxs-lookup"><span data-stu-id="3d76c-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="3d76c-112">Когда вы отправляете HTTP-запросы к службе с помощью REST API, *каждый* запрос API должен содержать ключ API, который был создан для подготовленной службы поиска.</span><span class="sxs-lookup"><span data-stu-id="3d76c-112">When issuing HTTP requests against your service using the REST API, *each* API request must include the api-key that was generated for the Search service you provisioned.</span></span> <span data-ttu-id="3d76c-113">Если есть действительный ключ, для каждого запроса устанавливаются отношения доверия между приложением, которое отправляет запрос, и службой, которая его обрабатывает.</span><span class="sxs-lookup"><span data-stu-id="3d76c-113">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="3d76c-114">Чтобы найти ключи API своей службы, войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3d76c-114">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="3d76c-115">Перейдите к колонке службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="3d76c-115">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="3d76c-116">Щелкните значок "Ключи".</span><span class="sxs-lookup"><span data-stu-id="3d76c-116">Click on the "Keys" icon</span></span>

<span data-ttu-id="3d76c-117">Ваша служба получит *ключи администратора* и *ключи запросов*.</span><span class="sxs-lookup"><span data-stu-id="3d76c-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="3d76c-118">Первичные и вторичные *ключи администратора* предоставляют полный доступ ко всем операциям, включая возможность управлять службой, создавать и удалять индексы, индексаторы и источники данных.</span><span class="sxs-lookup"><span data-stu-id="3d76c-118">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="3d76c-119">Ключей два, поэтому вы можете и дальше использовать вторичный ключ, если решите повторно создать первичный ключ, и наоборот.</span><span class="sxs-lookup"><span data-stu-id="3d76c-119">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="3d76c-120">*Ключи запросов* предоставляют только разрешение на чтение индексов и документов; обычно они добавляются в клиентские приложения, которые создают запросы на поиск.</span><span class="sxs-lookup"><span data-stu-id="3d76c-120">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="3d76c-121">Для импорта данных в индекс можно использовать первичный или вторичный ключ администратора.</span><span class="sxs-lookup"><span data-stu-id="3d76c-121">For the purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="3d76c-122">Выбор операций индексирования</span><span class="sxs-lookup"><span data-stu-id="3d76c-122">Decide which indexing action to use</span></span>
<span data-ttu-id="3d76c-123">В интерфейсе REST API можно создавать HTTP-запросы POST с текстом запроса JSON, отправляемые в конечную точку вашего индекса службы поиска Azure по URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="3d76c-123">When using the REST API, you will issue HTTP POST requests with JSON request bodies to your Azure Search index's endpoint URL.</span></span> <span data-ttu-id="3d76c-124">Объект JSON в тексте HTTP-запроса содержит массив JSON с именем value. Этот массив включает объекты JSON — документы, которые вы хотите добавить в свой индекс, обновить или удалить.</span><span class="sxs-lookup"><span data-stu-id="3d76c-124">The JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like to add to your index, update, or delete.</span></span>

<span data-ttu-id="3d76c-125">Каждый объект JSON в массиве value представляет документ для индексирования,</span><span class="sxs-lookup"><span data-stu-id="3d76c-125">Each JSON object in the "value" array represents a document to be indexed.</span></span> <span data-ttu-id="3d76c-126">д.).</span><span class="sxs-lookup"><span data-stu-id="3d76c-126">Each of these objects contains the document's key and specifies the desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="3d76c-127">В зависимости от выбранной операции для каждого документа будут включены только определенные поля.</span><span class="sxs-lookup"><span data-stu-id="3d76c-127">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="3d76c-128">Описание</span><span class="sxs-lookup"><span data-stu-id="3d76c-128">Description</span></span> | <span data-ttu-id="3d76c-129">Необходимые поля для каждого документа</span><span class="sxs-lookup"><span data-stu-id="3d76c-129">Necessary fields for each document</span></span> | <span data-ttu-id="3d76c-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="3d76c-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="3d76c-131">Операция `upload` аналогична операции upsert, которая добавляет документ, если он новый, и обновляет либо заменяет его, если он уже существует.</span><span class="sxs-lookup"><span data-stu-id="3d76c-131">An `upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="3d76c-132">Поле key, а также другие поля, которые вы хотите определить.</span><span class="sxs-lookup"><span data-stu-id="3d76c-132">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="3d76c-133">При обновлении или замене существующего документа все поля, не указанные в запросе, получат значение `null`.</span><span class="sxs-lookup"><span data-stu-id="3d76c-133">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="3d76c-134">Это происходит, даже если для поля указано непустое значение.</span><span class="sxs-lookup"><span data-stu-id="3d76c-134">This occurs even when the field was previously set to a non-null value.</span></span> |
| `merge` |<span data-ttu-id="3d76c-135">Обновляет существующий документ с использованием указанных полей.</span><span class="sxs-lookup"><span data-stu-id="3d76c-135">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="3d76c-136">Если документ не существует в индексе, объединение завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="3d76c-136">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="3d76c-137">Поле key, а также другие поля, которые вы хотите определить.</span><span class="sxs-lookup"><span data-stu-id="3d76c-137">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="3d76c-138">Поля, указанные в запросе на объединение, заменяют собой существующие поля документа.</span><span class="sxs-lookup"><span data-stu-id="3d76c-138">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="3d76c-139">Это относится и к полям типа `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="3d76c-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="3d76c-140">Например, если документ содержит поле `tags` со значением `["budget"]` и вы выполняете операцию объединения со значением `["economy", "pool"]` для поля `tags`, в итоге поле `tags` примет значение `["economy", "pool"]`,</span><span class="sxs-lookup"><span data-stu-id="3d76c-140">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="3d76c-141">а не `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="3d76c-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="3d76c-142">Эта операция аналогична операции `merge`, если документ с указанным значением ключа уже существует в индексе.</span><span class="sxs-lookup"><span data-stu-id="3d76c-142">This action behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="3d76c-143">Если документа нет, эта операция выполняется так же, как и операция `upload` с новым документом.</span><span class="sxs-lookup"><span data-stu-id="3d76c-143">If the document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="3d76c-144">Поле key, а также другие поля, которые вы хотите определить.</span><span class="sxs-lookup"><span data-stu-id="3d76c-144">key, plus any other fields you wish to define</span></span> |- |
| `delete` |<span data-ttu-id="3d76c-145">Удаление указанного документа из индекса.</span><span class="sxs-lookup"><span data-stu-id="3d76c-145">Removes the specified document from the index.</span></span> |<span data-ttu-id="3d76c-146">Только ключ</span><span class="sxs-lookup"><span data-stu-id="3d76c-146">key only</span></span> |<span data-ttu-id="3d76c-147">Все указанные поля, которые отличаются от ключевого поля, будут игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="3d76c-147">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="3d76c-148">Чтобы удалить из документа определенное поле, лучше воспользуйтесь операцией `merge`, явным образом задав для требуемого поля значение NULL.</span><span class="sxs-lookup"><span data-stu-id="3d76c-148">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to null.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="3d76c-149">Создание HTTP-запроса и текста запроса</span><span class="sxs-lookup"><span data-stu-id="3d76c-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="3d76c-150">Теперь, когда вы выбрали нужные значения полей для операций индекса, можно приступать к созданию HTTP-запроса и текста запроса JSON для импорта данных.</span><span class="sxs-lookup"><span data-stu-id="3d76c-150">Now that you have gathered the necessary field values for your index actions, you are ready to construct the actual HTTP request and JSON request body to import your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="3d76c-151">Запрос и заголовки запроса</span><span class="sxs-lookup"><span data-stu-id="3d76c-151">Request and Request Headers</span></span>
<span data-ttu-id="3d76c-152">В URL-адресе необходимо указать имя службы, имя индекса (в нашем случае это hotels), а также правильную версию API (текущая версия API на момент публикации этого документа — `2016-09-01` ).</span><span class="sxs-lookup"><span data-stu-id="3d76c-152">In the URL, you will need to provide your service name, index name ("hotels" in this case), as well as the proper API version (the current API version is `2016-09-01` at the time of publishing this document).</span></span> <span data-ttu-id="3d76c-153">Необходимо также определить заголовки запросов `Content-Type` и `api-key`.</span><span class="sxs-lookup"><span data-stu-id="3d76c-153">You will need to define the `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="3d76c-154">Для заголовка последнего запроса используйте один из ключей администратора службы.</span><span class="sxs-lookup"><span data-stu-id="3d76c-154">For the latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="3d76c-155">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="3d76c-155">Request Body</span></span>
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
            "description": "Close to town hall and the river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="3d76c-156">В этом примере мы используем операции `upload`, `mergeOrUpload` и `delete` в качестве операций поиска.</span><span class="sxs-lookup"><span data-stu-id="3d76c-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="3d76c-157">Предположим, что пример индекса с именем hotels уже заполнен несколькими документами.</span><span class="sxs-lookup"><span data-stu-id="3d76c-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="3d76c-158">Обратите внимание: нам не понадобилось указывать все поля документа при использовании операции `mergeOrUpload`, а при использовании `delete` мы указали только ключ документа (`hotelId`).</span><span class="sxs-lookup"><span data-stu-id="3d76c-158">Note how we did not have to specify all the possible document fields when using `mergeOrUpload` and how we only specified the document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="3d76c-159">Также помните о том, что в один запрос на индексирование можно включить максимум 1000 документов (или 16 МБ).</span><span class="sxs-lookup"><span data-stu-id="3d76c-159">Also, note that you can only include up to 1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="3d76c-160">Анализ кода HTTP-ответа</span><span class="sxs-lookup"><span data-stu-id="3d76c-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="3d76c-161">200</span><span class="sxs-lookup"><span data-stu-id="3d76c-161">200</span></span>
<span data-ttu-id="3d76c-162">После успешной отправки запроса на индексирование вы получите HTTP-ответ с кодом состояния `200 OK`.</span><span class="sxs-lookup"><span data-stu-id="3d76c-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="3d76c-163">Текст JSON в HTTP-ответе будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="3d76c-163">The JSON body of the HTTP response will be as follows:</span></span>

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

#### <a name="207"></a><span data-ttu-id="3d76c-164">207</span><span class="sxs-lookup"><span data-stu-id="3d76c-164">207</span></span>
<span data-ttu-id="3d76c-165">Код состояния `207` возвращается, если хотя бы один элемент не удалось проиндексировать.</span><span class="sxs-lookup"><span data-stu-id="3d76c-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="3d76c-166">Текст JSON HTTP-ответа будет содержать сведения о документах, которые не удалось проиндексировать.</span><span class="sxs-lookup"><span data-stu-id="3d76c-166">The JSON body of the HTTP response will contain information about the unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "The search service is too busy to process this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> <span data-ttu-id="3d76c-167">Часто это означает, что служба поиска настолько загружена, что запросы на индексирование начинают возвращать ответы `503`.</span><span class="sxs-lookup"><span data-stu-id="3d76c-167">This often means that the load on your search service is reaching a point where indexing requests will begin to return `503` responses.</span></span> <span data-ttu-id="3d76c-168">В таком случае мы настоятельно рекомендуем задержать выполнение клиентского кода и повторить попытку позже.</span><span class="sxs-lookup"><span data-stu-id="3d76c-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="3d76c-169">За это время система восстановится, что повысит вероятность успешной обработки будущих запросов.</span><span class="sxs-lookup"><span data-stu-id="3d76c-169">This will give the system some time to recover, increasing the chances that future requests will succeed.</span></span> <span data-ttu-id="3d76c-170">Непрерывные повторные попытки выполнить запрос только усугубят проблему.</span><span class="sxs-lookup"><span data-stu-id="3d76c-170">Rapidly retrying your requests will only prolong the situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="3d76c-171">429</span><span class="sxs-lookup"><span data-stu-id="3d76c-171">429</span></span>
<span data-ttu-id="3d76c-172">Код состояния `429` возвращается, если вы превысили квоту на количество документов, которые можно включить в индекс.</span><span class="sxs-lookup"><span data-stu-id="3d76c-172">A status code of `429` will be returned when you have exceeded your quota on the number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="3d76c-173">503</span><span class="sxs-lookup"><span data-stu-id="3d76c-173">503</span></span>
<span data-ttu-id="3d76c-174">Код состояния `503` возвращается, если ни один из элементов в запросе не был проиндексирован.</span><span class="sxs-lookup"><span data-stu-id="3d76c-174">A status code of `503` will be returned if none of the items in the request were successfully indexed.</span></span> <span data-ttu-id="3d76c-175">Эта ошибка означает, что система перегружена и запрос не может быть обработан в данный момент.</span><span class="sxs-lookup"><span data-stu-id="3d76c-175">This error means that the system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="3d76c-176">В таком случае мы настоятельно рекомендуем задержать выполнение клиентского кода и повторить попытку позже.</span><span class="sxs-lookup"><span data-stu-id="3d76c-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="3d76c-177">За это время система восстановится, что повысит вероятность успешной обработки будущих запросов.</span><span class="sxs-lookup"><span data-stu-id="3d76c-177">This will give the system some time to recover, increasing the chances that future requests will succeed.</span></span> <span data-ttu-id="3d76c-178">Непрерывные повторные попытки выполнить запрос только усугубят проблему.</span><span class="sxs-lookup"><span data-stu-id="3d76c-178">Rapidly retrying your requests will only prolong the situation.</span></span>
>
>

<span data-ttu-id="3d76c-179">Дополнительные сведения о действиях с документами и ответах об успешном выполнении и ошибках см. в статье, посвященной [добавлению, обновлению и удалению документов](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span><span class="sxs-lookup"><span data-stu-id="3d76c-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="3d76c-180">Дополнительные сведения о других кодах состояния HTTP, которые могут быть возвращены в случае сбоя, см. в статье [Коды состояния HTTP (поиск Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="3d76c-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d76c-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3d76c-181">Next steps</span></span>
<span data-ttu-id="3d76c-182">Заполнив индекс службы поиска Azure, вы можете приступать к отправке запросов на поиск документов.</span><span class="sxs-lookup"><span data-stu-id="3d76c-182">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="3d76c-183">Дополнительные сведения см. в статье [Запросы в службе поиска Azure](search-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d76c-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
