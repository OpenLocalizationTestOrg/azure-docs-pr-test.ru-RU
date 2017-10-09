---
title: "Поиск службы REST API версия 2015-02-28-Preview aaaAzure | Документы Microsoft"
description: "В версии 2015-02-28-Preview API REST службы поиска Azure реализованы экспериментальные функции, такие как анализаторы естественных языков и запросы moreLikeThis."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="96fee-103">API REST службы поиска Azure, версия 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="96fee-104">Эта статья является hello справочную документацию по `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-104">This article is hello reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-105">Этой предварительной версии расширяет hello текущей общедоступной версии, [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), предоставляя следующие экспериментальные функции hello:</span><span class="sxs-lookup"><span data-stu-id="96fee-105">This preview extends hello current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing hello following experimental features:</span></span>

* <span data-ttu-id="96fee-106">`moreLikeThis`параметр в hello запроса [поиск документов](#SearchDocs) API.</span><span class="sxs-lookup"><span data-stu-id="96fee-106">`moreLikeThis` query parameter in hello [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="96fee-107">Она находит другие документы, соответствующие tooanother конкретный документ.</span><span class="sxs-lookup"><span data-stu-id="96fee-107">It finds other documents that are relevant tooanother specific document.</span></span>

<span data-ttu-id="96fee-108">Несколько дополнительных частей приложения hello `2015-02-28-Preview` API-интерфейса REST описаны отдельно.</span><span class="sxs-lookup"><span data-stu-id="96fee-108">A few additional parts of hello `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="96fee-109">В частности, описаны такие возможности:</span><span class="sxs-lookup"><span data-stu-id="96fee-109">These include:</span></span>

* [<span data-ttu-id="96fee-110">Профили оценки</span><span class="sxs-lookup"><span data-stu-id="96fee-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="96fee-111">Индексаторы</span><span class="sxs-lookup"><span data-stu-id="96fee-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="96fee-112">Существуют различные версии службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="96fee-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="96fee-113">См. слишком[управление версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="96fee-113">Please refer too[Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="96fee-114">API, рассматриваемый в этом документе</span><span class="sxs-lookup"><span data-stu-id="96fee-114">APIs in this document</span></span>
<span data-ttu-id="96fee-115">API службы поиска Azure поддерживает две синтаксические схемы URL, которые можно использовать для операций API: простой синтаксис и синтаксис OData, который описан в статье о [поддержке OData в API службы поиска Azure](http://msdn.microsoft.com/library/azure/dn798932.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="96fee-116">Hello следующем списке показан простой синтаксис hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-116">hello following list shows hello simple syntax.</span></span>

[<span data-ttu-id="96fee-117">Создание индекса</span><span class="sxs-lookup"><span data-stu-id="96fee-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="96fee-118">Обновление индекса</span><span class="sxs-lookup"><span data-stu-id="96fee-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="96fee-119">Получение индекса</span><span class="sxs-lookup"><span data-stu-id="96fee-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="96fee-120">Получение списка индексов</span><span class="sxs-lookup"><span data-stu-id="96fee-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="96fee-121">Получение статистических данных индекса</span><span class="sxs-lookup"><span data-stu-id="96fee-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="96fee-122">Анализатор теста</span><span class="sxs-lookup"><span data-stu-id="96fee-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="96fee-123">Удаление индекса</span><span class="sxs-lookup"><span data-stu-id="96fee-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="96fee-124">Добавление, удаление и обновление данных в индексе</span><span class="sxs-lookup"><span data-stu-id="96fee-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="96fee-125">Поиск документов</span><span class="sxs-lookup"><span data-stu-id="96fee-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="96fee-126">Запрос документов</span><span class="sxs-lookup"><span data-stu-id="96fee-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="96fee-127">Подсчет документов</span><span class="sxs-lookup"><span data-stu-id="96fee-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="96fee-128">Предложения</span><span class="sxs-lookup"><span data-stu-id="96fee-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="96fee-129">Операции с индексом</span><span class="sxs-lookup"><span data-stu-id="96fee-129">Index Operations</span></span>
<span data-ttu-id="96fee-130">Для создания индексов в службе поиска Azure и управления ими используются простые HTTP-запросы (POST, GET, PUT, DELETE), отправляемые к определенному ресурсу индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="96fee-131">toocreate индекс первого сообщения документ JSON, описывающий hello схемы индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-131">toocreate an index, you first POST a JSON document that describes hello index schema.</span></span> <span data-ttu-id="96fee-132">Hello схема определяет поля hello hello индекса, их типы данных, и описание их использования (например, в полнотекстовый поиск, сортировка и фильтры аспекты).</span><span class="sxs-lookup"><span data-stu-id="96fee-132">hello schema defines hello fields of hello index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="96fee-133">Он также определяет профили оценки, средств подбора и другие атрибуты tooconfigure hello поведение hello индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-133">It also defines scoring profiles, suggesters and other attributes tooconfigure hello behavior of hello index.</span></span>

<span data-ttu-id="96fee-134">Hello ниже приведен пример схемы, используемый для поиска сведений об отелях с hello поле описания, определенном на двух языках.</span><span class="sxs-lookup"><span data-stu-id="96fee-134">hello following example provides an illustration of a schema used for searching on hotel information with hello Description field defined in two languages.</span></span> <span data-ttu-id="96fee-135">Обратите внимание на то, как атрибуты определяют, как используется поле hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-135">Notice how attributes control how hello field is used.</span></span> <span data-ttu-id="96fee-136">Здравствуйте, например `hotelId` используется как ключ документа hello (`"key": true`) и исключается из полнотекстового поиска (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="96fee-136">For example hello `hotelId` is used as hello document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

<span data-ttu-id="96fee-137">После создания индекса hello, вы отправите документы, заполняющие индекс hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-137">After hello index is created, you'll upload documents that populate hello index.</span></span> <span data-ttu-id="96fee-138">Этот этап описан в разделе [Добавление и обновление документов](#AddOrUpdateDocuments) .</span><span class="sxs-lookup"><span data-stu-id="96fee-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="96fee-139">Tooindexing Видеоролик с общими сведениями, в поиске Azure, в разделе hello [Channel 9 Cloud Cover серии о поиске Azure](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="96fee-139">For a video introduction tooindexing in Azure Search, see hello [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="96fee-140">Создание индекса</span><span class="sxs-lookup"><span data-stu-id="96fee-140">Create Index</span></span>
<span data-ttu-id="96fee-141">Индекс является основным средством организации и поиска документов в поиске Azure hello, аналогичные toohow таблицы организует записи в базе данных.</span><span class="sxs-lookup"><span data-stu-id="96fee-141">An index is hello primary means of organizing and searching documents in Azure Search, similar toohow a table organizes records in a database.</span></span> <span data-ttu-id="96fee-142">Каждый индекс имеет коллекцию документов, которые все соответствуют схеме индекса toohello (имена полей, типы данных и свойства), что индексы также указывают дополнительные конструкции (средства подбора смысловых вариантов, профили повышения и параметры CORS), которые определяют поведение других поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-142">Each index has a collection of documents that all conform toohello index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="96fee-143">Для создания нового индекса в службе поиска Azure используется HTTP-запрос POST или PUT.</span><span class="sxs-lookup"><span data-stu-id="96fee-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="96fee-144">текст Hello hello запроса является схемой JSON, указывает hello индекс и сведения о конфигурации.</span><span class="sxs-lookup"><span data-stu-id="96fee-144">hello body of hello request is a JSON schema that specifies hello index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="96fee-145">Кроме того можно использовать PUT и указать имя индекса hello hello URI.</span><span class="sxs-lookup"><span data-stu-id="96fee-145">Alternatively, you can use PUT and specify hello index name on hello URI.</span></span> <span data-ttu-id="96fee-146">Если индекс hello не существует, он будет создан.</span><span class="sxs-lookup"><span data-stu-id="96fee-146">If hello index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="96fee-147">Создание индекса определяет структуру hello hello документов сохраняются и используются в операциях поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-147">Creating an index determines hello structure of hello documents stored and used in search operations.</span></span> <span data-ttu-id="96fee-148">Заполнение индекса hello является отдельной операцией.</span><span class="sxs-lookup"><span data-stu-id="96fee-148">Populating hello index is a separate operation.</span></span> <span data-ttu-id="96fee-149">На этом этапе можно использовать [индексатор](https://msdn.microsoft.com/library/azure/mt183328.aspx) (для поддерживаемых источников данных) либо операции [добавления, обновления и удаления документов](https://msdn.microsoft.com/library/azure/dn798930.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="96fee-150">Hello инвертированный индекс создается в том случае, когда для публикации документов hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-150">hello inverted index is generated when hello documents are posted.</span></span>

<span data-ttu-id="96fee-151">**Примечание**: hello максимальное число может быть индексов зависит от ценового уровня.</span><span class="sxs-lookup"><span data-stu-id="96fee-151">**Note**: hello maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="96fee-152">Hello бесплатная служба позволяет создавать копии too3 индексов.</span><span class="sxs-lookup"><span data-stu-id="96fee-152">hello free service allows up too3 indexes.</span></span> <span data-ttu-id="96fee-153">В стандартной версии разрешено использовать до 50 индексов на одну службу поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="96fee-154">Дополнительные сведения см. в статье с описанием [пределов и ограничений](http://msdn.microsoft.com/library/azure/dn798934.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="96fee-155">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-155">**Request**</span></span>

<span data-ttu-id="96fee-156">Все запросы к службе отправляются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96fee-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="96fee-157">Hello **Create Index** можно составить запрос с помощью метода POST или PUT.</span><span class="sxs-lookup"><span data-stu-id="96fee-157">hello **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="96fee-158">При использовании POST необходимо указать имя индекса в тексте запроса hello, а также определение схемы индекса hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-158">When using POST, you must provide an index name in hello request body along with hello index schema definition.</span></span> <span data-ttu-id="96fee-159">С помощью метода PUT имя индекса hello является частью URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-159">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="96fee-160">Если индекс hello не существует, он создается.</span><span class="sxs-lookup"><span data-stu-id="96fee-160">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="96fee-161">Если он уже существует, это новое определение обновленных toohello.</span><span class="sxs-lookup"><span data-stu-id="96fee-161">If it already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="96fee-162">Имя индекса Hello должен состоять из строчных букв, начинаться с буквы или цифры, иметь нет символы косой черты или точек и быть не длиннее 128 символов.</span><span class="sxs-lookup"><span data-stu-id="96fee-162">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="96fee-163">После имени индекса hello начиная с буквы или цифры, hello остальная часть имени hello может включать любой буквы, числа и дефисы, при условии, что hello дефисы не являются последовательными.</span><span class="sxs-lookup"><span data-stu-id="96fee-163">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="96fee-164">Hello `api-version` является обязательным.</span><span class="sxs-lookup"><span data-stu-id="96fee-164">hello `api-version` is required.</span></span> <span data-ttu-id="96fee-165">Список доступных версий см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="96fee-166">**Заголовки запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-166">**Request Headers**</span></span>

<span data-ttu-id="96fee-167">Hello следующий список описывает hello необходимые и необязательные заголовки запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-167">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="96fee-168">`Content-Type`: обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="96fee-168">`Content-Type`: Required.</span></span> <span data-ttu-id="96fee-169">Установите это слишком`application/json`</span><span class="sxs-lookup"><span data-stu-id="96fee-169">Set this too`application/json`</span></span>
* <span data-ttu-id="96fee-170">`api-key`: обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="96fee-170">`api-key`: Required.</span></span> <span data-ttu-id="96fee-171">Hello `api-key` используется для</span><span class="sxs-lookup"><span data-stu-id="96fee-171">hello `api-key` is used to</span></span>
* <span data-ttu-id="96fee-172">Проверка подлинности службы поиска tooyour hello запроса.</span><span class="sxs-lookup"><span data-stu-id="96fee-172">authenticate hello request tooyour Search service.</span></span> <span data-ttu-id="96fee-173">Это строковое значение, уникальным tooyour службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-173">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="96fee-174">Hello **Create Index** запрос должен включать `api-key` заголовок указать ключ администратора tooyour (как противоположность tooa ключа запроса).</span><span class="sxs-lookup"><span data-stu-id="96fee-174">hello **Create Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="96fee-175">Необходимо также hello имя tooconstruct hello запроса URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-175">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="96fee-176">Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-176">You can get both hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="96fee-177">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.</span><span class="sxs-lookup"><span data-stu-id="96fee-177">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="96fee-178"><a name="RequestData"></a>
**Синтаксис текста запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="96fee-179">текст Hello hello запроса содержит определение схемы, включая hello список полей данных в документах, которые будут переданы в этот индекс, типы данных, атрибутов, а также необязательный список профилей оценки, используемые tooscore соответствующие документы в время запроса.</span><span class="sxs-lookup"><span data-stu-id="96fee-179">hello body of hello request contains a schema definition, which includes hello list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used tooscore matching documents at query time.</span></span>

<span data-ttu-id="96fee-180">Обратите внимание, что для запроса POST, необходимо указать имя индекса hello в тексте запроса hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-180">Note that for a POST request, you must specify hello index name in hello request body.</span></span>

<span data-ttu-id="96fee-181">Может существовать только одно ключевое поле в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-181">There can only be one key field in hello index.</span></span> <span data-ttu-id="96fee-182">Он имеет toobe строкового поля.</span><span class="sxs-lookup"><span data-stu-id="96fee-182">It has toobe a string field.</span></span> <span data-ttu-id="96fee-183">Это поле представляет уникальный идентификатор каждого документа, хранящегося в индексе hello hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-183">This field represents hello unique identifier for each document stored within hello index.</span></span>

<span data-ttu-id="96fee-184">Hello основные части индекса включить hello следующие:</span><span class="sxs-lookup"><span data-stu-id="96fee-184">hello main parts of an index include hello following:</span></span>

* `name`
* <span data-ttu-id="96fee-185">`fields` — поля, которые будут передаваться в этот индекс, включая имя, тип данных и свойства, определяющие доступные для каждого поля операции.</span><span class="sxs-lookup"><span data-stu-id="96fee-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="96fee-186">`suggesters` — средства подбора, которые используются для автозавершения и упреждающего ввода запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="96fee-187">`scoringProfiles`— профили оценки, которые используются для настраиваемого ранжирования показателей поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="96fee-188">Дополнительные сведения см. в статье о [добавлении профилей оценки](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="96fee-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` используется toodefine как документы и запросы разбиваются на токены индексируемые или для поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used toodefine how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="96fee-190">Дополнительные сведения см. в статье, посвященной [анализу в службе поиска Azure](https://aka.ms//azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="96fee-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="96fee-191">`defaultScoringProfile`использовать оценки поведений по умолчанию hello toooverwrite.</span><span class="sxs-lookup"><span data-stu-id="96fee-191">`defaultScoringProfile` used toooverwrite hello default scoring behaviors.</span></span>
* <span data-ttu-id="96fee-192">`corsOptions`tooallow запросы независимо от источника к индексу.</span><span class="sxs-lookup"><span data-stu-id="96fee-192">`corsOptions` tooallow cross-origin queries against your index.</span></span>

<span data-ttu-id="96fee-193">Hello синтаксис для структуризации полезных данных запроса hello выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="96fee-193">hello syntax for structuring hello request payload is as follows.</span></span> <span data-ttu-id="96fee-194">Далее в этом разделе приведен пример запроса.</span><span class="sxs-lookup"><span data-stu-id="96fee-194">A sample request is provided further on in this topic.</span></span>

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

<span data-ttu-id="96fee-195">**Атрибуты индекса**</span><span class="sxs-lookup"><span data-stu-id="96fee-195">**Index Attributes**</span></span>

<span data-ttu-id="96fee-196">Hello следующие атрибуты можно задать при создании индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-196">hello following attributes can be set when creating an index.</span></span> <span data-ttu-id="96fee-197">Подробные сведения об оценке и профилях см. в статье о [добавлении профилей оценки](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="96fee-198">`name`— Задает hello имя поля hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-198">`name` - Sets hello name of hello field.</span></span>

<span data-ttu-id="96fee-199">`type`— Задает hello типа данных для поля hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-199">`type` - Sets hello data type for hello field.</span></span>

<span data-ttu-id="96fee-200">`searchable`-Помечает hello поле как средство полнотекстового поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-200">`searchable` - Marks hello field as full-text search-able.</span></span> <span data-ttu-id="96fee-201">Это означает, что во время индексирования оно будет включено в анализ (в частности, для разбиения на слова).</span><span class="sxs-lookup"><span data-stu-id="96fee-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="96fee-202">Если задать `searchable` tooa значение поля «солнечный день», внутренне будет разделить на отдельные токены hello «солнечный» и «день».</span><span class="sxs-lookup"><span data-stu-id="96fee-202">If you set a `searchable` field tooa value like "sunny day", internally it will be split into hello individual tokens "sunny" and "day".</span></span> <span data-ttu-id="96fee-203">В результате эти слова смогут участвовать в полнотекстовом поиске.</span><span class="sxs-lookup"><span data-stu-id="96fee-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="96fee-204">У полей типа `Edm.String` и `Collection(Edm.String)` по умолчанию установлен флаг `searchable`.</span><span class="sxs-lookup"><span data-stu-id="96fee-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="96fee-205">Для полей других типов установить атрибут `searchable`нельзя.</span><span class="sxs-lookup"><span data-stu-id="96fee-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="96fee-206">**Примечание**: `searchable` поля потребляют дополнительное пространство в индексе, так как поиск Azure будет хранить дополнительную помеченную токенами версию значения поля hello для полнотекстового поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of hello field value for full-text searches.</span></span> <span data-ttu-id="96fee-207">Если вы хотите toosave модуль индекс и вы не нужен toobe поля, включенные в поиск, задайте `searchable` слишком`false`.</span><span class="sxs-lookup"><span data-stu-id="96fee-207">If you want toosave space in your index and you don't need a field toobe included in searches, set `searchable` too`false`.</span></span>

<span data-ttu-id="96fee-208">`filterable`-Позволяет toobe hello поля, на которые ссылается `$filter` запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-208">`filterable` - Allows hello field toobe referenced in `$filter` queries.</span></span> <span data-ttu-id="96fee-209">`filterable` отличается от `searchable` тем, как обрабатываются строки.</span><span class="sxs-lookup"><span data-stu-id="96fee-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="96fee-210">Для полей типа `Edm.String` и `Collection(Edm.String)` с атрибутом `filterable` не выполняется разбиение на слова, поэтому они могут попасть в результаты поиска только по точному совпадению.</span><span class="sxs-lookup"><span data-stu-id="96fee-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="96fee-211">Например, если задать такому полю `f` слишком «солнечный день» `$filter=f eq 'sunny'` не найдет совпадений, но `$filter=f eq 'sunny day'` будет.</span><span class="sxs-lookup"><span data-stu-id="96fee-211">For example, if you set such a field `f` too"sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="96fee-212">По умолчанию атрибут `filterable` устанавливается для всех полей.</span><span class="sxs-lookup"><span data-stu-id="96fee-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="96fee-213">`sortable`-По умолчанию hello система упорядочивает результаты по оценкам, но во многих случаях пользователям требуется, чтобы toosort по полям в документах hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-213">`sortable` - By default hello system sorts results by score, but in many experiences users will want toosort by fields in hello documents.</span></span> <span data-ttu-id="96fee-214">Для полей типа `Collection(Edm.String)` установить атрибут `sortable` нельзя.</span><span class="sxs-lookup"><span data-stu-id="96fee-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="96fee-215">Для всех остальных полей флаг `sortable` устанавливается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="96fee-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="96fee-216">`facetable` — как правило, используется для представления результатов поиска, в которых указывается количество найденных документов по категориям (например, при поиске цифровых фотоаппаратов можно разделить результаты по производителям, количеству мегапикселей, цене и т. п.).</span><span class="sxs-lookup"><span data-stu-id="96fee-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="96fee-217">Этот параметр не предназначен для использования с полями типа `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="96fee-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="96fee-218">Для всех остальных полей флаг `facetable` устанавливается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="96fee-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="96fee-219">**Примечание**. Поля типа `Edm.String`, для которых задан атрибут `filterable`, `sortable` или `facetable`, должны иметь длину не больше 32 КБ.</span><span class="sxs-lookup"><span data-stu-id="96fee-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="96fee-220">Это потому, что такие поля считаются одним условием поиска и hello Максимальная длина условия в поиске Azure составляет 32 КБ.</span><span class="sxs-lookup"><span data-stu-id="96fee-220">This is because such fields are treated as a single search term, and hello maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="96fee-221">Если вам требуется toostore больше текста, чем в однострочном поле, необходимо будет tooexplicitly задать `filterable`, `sortable`, и `facetable` слишком`false` в определении индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-221">If you need toostore more text than this in a single string field, you will need tooexplicitly set `filterable`, `sortable`, and `facetable` too`false` in your index definition.</span></span>
* <span data-ttu-id="96fee-222">**Примечание**: Если поля не имеет ни один из hello выше атрибуты значения слишком`true` (`searchable`, `filterable`, `sortable`, или`facetable`) hello поле эффективно исключается из hello инвертированный индекс.</span><span class="sxs-lookup"><span data-stu-id="96fee-222">**Note**: If a field has none of hello above attributes set too`true` (`searchable`, `filterable`, `sortable`,  or`facetable`) hello field is effectively excluded from hello inverted index.</span></span> <span data-ttu-id="96fee-223">Это могут быть поля, которые не используются в запросах, однако нужны в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="96fee-224">Исключение подобных полей из hello индекс повышает производительность.</span><span class="sxs-lookup"><span data-stu-id="96fee-224">Excluding such fields from hello index improves performance.</span></span>

<span data-ttu-id="96fee-225">`key`-Метки hello поле как содержащее уникальные идентификаторы для документов в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-225">`key` - Marks hello field as containing unique identifiers for documents within hello index.</span></span> <span data-ttu-id="96fee-226">Только одно поле должно быть выбрано в качестве hello `key` поле и он должен иметь тип `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="96fee-226">Exactly one field must be chosen as hello `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="96fee-227">Ключевые поля могут содержать используется toolook документов непосредственно через hello [уточняющего запроса API](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="96fee-227">Key fields can be used toolook up documents directly via hello [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="96fee-228">`retrievable`— Задает ли hello поля могут быть возвращены в результате поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-228">`retrievable` - Sets whether hello field can be returned in a search result.</span></span>  <span data-ttu-id="96fee-229">Это полезно, когда необходимо toouse поля (например, поле) в качестве фильтра, сортировки или оценки механизм, но hello поле toobe toohello видимым для конечного пользователя не требуется.</span><span class="sxs-lookup"><span data-stu-id="96fee-229">This is useful when you want toouse a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want hello field toobe visible toohello end user.</span></span> <span data-ttu-id="96fee-230">У полей с установленным свойством `true` for `key` .</span><span class="sxs-lookup"><span data-stu-id="96fee-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="96fee-231">`analyzer`-Задает имя анализатора toouse hello для поля hello hello во время поиска и индексирования.</span><span class="sxs-lookup"><span data-stu-id="96fee-231">`analyzer` - Sets hello name of hello analyzer toouse for hello field at search time and indexing time.</span></span> <span data-ttu-id="96fee-232">Привет, допустимые значения см. [анализаторы](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-232">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="96fee-233">Этот параметр можно использовать только с полями `searchable`, а с `searchAnalyzer` или `indexAnalyzer` его установить нельзя.</span><span class="sxs-lookup"><span data-stu-id="96fee-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="96fee-234">После выбора анализатора hello, он не может изменяться для поля hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-234">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="96fee-235">`searchAnalyzer`— Задает hello имя анализатора hello, используемые во время поиска для поля hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-235">`searchAnalyzer` - Sets hello name of hello analyzer used at search time for hello field.</span></span> <span data-ttu-id="96fee-236">Привет, допустимые значения см. [анализаторы](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-236">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="96fee-237">Этот параметр можно использовать только с полями, для которых задан атрибут `searchable`.</span><span class="sxs-lookup"><span data-stu-id="96fee-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="96fee-238">Она должна быть задана вместе с `indexAnalyzer` и не могут указываться вместе с hello `analyzer` параметр.</span><span class="sxs-lookup"><span data-stu-id="96fee-238">It must be set together with `indexAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="96fee-239">Этот анализатор можно обновить на существующее поле.</span><span class="sxs-lookup"><span data-stu-id="96fee-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="96fee-240">`indexAnalyzer`— Задает hello имя анализатора hello, используемые во время индексирования для поля hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-240">`indexAnalyzer` - Sets hello name of hello analyzer used at indexing time for hello field.</span></span> <span data-ttu-id="96fee-241">Привет, допустимые значения см. [анализаторы](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-241">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="96fee-242">Этот параметр можно использовать только с полями, для которых задан атрибут `searchable`.</span><span class="sxs-lookup"><span data-stu-id="96fee-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="96fee-243">Она должна быть задана вместе с `searchAnalyzer` и не могут указываться вместе с hello `analyzer` параметр.</span><span class="sxs-lookup"><span data-stu-id="96fee-243">It must be set together with `searchAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="96fee-244">После выбора анализатора hello, он не может изменяться для поля hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-244">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="96fee-245">`suggesters`— Задает hello режим поиска и полей, которые являются источником hello hello содержимого для предложений.</span><span class="sxs-lookup"><span data-stu-id="96fee-245">`suggesters` - Sets hello search mode and fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="96fee-246">Дополнительные сведения см. в разделе [Средства подбора](#Suggesters).</span><span class="sxs-lookup"><span data-stu-id="96fee-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="96fee-247">`scoringProfiles` — позволяет настроить механизм оценки, с помощью которого можно влиять на относительную позицию элементов в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="96fee-248">Профили оценки состоят из взвешенных полей и функций.</span><span class="sxs-lookup"><span data-stu-id="96fee-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="96fee-249">В разделе [Добавление профилей оценки](https://msdn.microsoft.com/library/azure/dn798928.aspx) Дополнительные сведения о hello атрибуты, используемые в профиль оценки.</span><span class="sxs-lookup"><span data-stu-id="96fee-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about hello attributes used in a scoring profile.</span></span>

<span data-ttu-id="96fee-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Поддержка языков**</span><span class="sxs-lookup"><span data-stu-id="96fee-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="96fee-251">Поля с поддержкой поиска подвергаются анализу, который чаще всего включает разбиение на слова, нормализацию текста и выделение условий поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="96fee-252">По умолчанию, доступные для поиска поля в поиске Azure анализируются с hello [стандартного анализатора Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) который разбивает текст на элементы, которые следуют[«Сегментация текста Юникод»](http://unicode.org/reports/tr29/) правила.</span><span class="sxs-lookup"><span data-stu-id="96fee-252">By default, searchable fields in Azure Search are analyzed with hello [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="96fee-253">Кроме того hello стандартный анализатор преобразует все символы tootheir нижний регистр.</span><span class="sxs-lookup"><span data-stu-id="96fee-253">Additionally, hello standard analyzer converts all characters tootheir lower case form.</span></span> <span data-ttu-id="96fee-254">Индексированных документов и условий поиска проходят hello анализа во время индексирования и обработки запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-254">Both indexed documents and search terms go through hello analysis during indexing and query processing.</span></span>

<span data-ttu-id="96fee-255">"Поиск Azure" поддерживает различные языки.</span><span class="sxs-lookup"><span data-stu-id="96fee-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="96fee-256">Для каждого из них необходим нестандартный анализатор текста, который учитывает особенности соответствующего языка.</span><span class="sxs-lookup"><span data-stu-id="96fee-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="96fee-257">В службе поиска Azure доступны анализаторы двух типов:</span><span class="sxs-lookup"><span data-stu-id="96fee-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="96fee-258">35 анализаторов на базе технологии Lucene.</span><span class="sxs-lookup"><span data-stu-id="96fee-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="96fee-259">50 анализаторов на базе собственной технологии Майкрософт для обработки естественных языков, которая используется в приложениях Office и поисковой системе Bing.</span><span class="sxs-lookup"><span data-stu-id="96fee-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="96fee-260">Некоторые разработчики могут использовать знакомую проста, открытая решения для Lucene hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-260">Some developers might prefer hello more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="96fee-261">Анализаторы Lucene работают быстрее, но анализаторы Microsoft hello предусмотрены расширенные возможности, такие как лемматизация, decompounding (на языках, таких как немецкий, датский, голландский, шведский, норвежский, эстонский, Готово, венгерский, словацкий) и распознавание сущности (URL-адреса в word сообщения электронной почты, дат, чисел).</span><span class="sxs-lookup"><span data-stu-id="96fee-261">Lucene analyzers are faster, but hello Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="96fee-262">Если это возможно следует выполнять сравнение обоих hello Майкрософт и Lucene анализаторы toodecide какая оптимален.</span><span class="sxs-lookup"><span data-stu-id="96fee-262">If possible, you should run comparisons of both hello Microsoft and Lucene analyzers toodecide which one is a better fit.</span></span>

<span data-ttu-id="96fee-263">***Сравнение***</span><span class="sxs-lookup"><span data-stu-id="96fee-263">***How they compare***</span></span>

<span data-ttu-id="96fee-264">Анализатор Lucene Hello английского языка расширяет стандартный анализатор hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-264">hello Lucene analyzer for English extends hello standard analyzer.</span></span> <span data-ttu-id="96fee-265">Он удаляет из слов признаки принадлежности (символы 's в конце), находит основу слов с помощью [стеммера Портера](http://tartarus.org/~martin/PorterStemmer/) и удаляет английские [стоп-слова](http://en.wikipedia.org/wiki/Stop_words).</span><span class="sxs-lookup"><span data-stu-id="96fee-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="96fee-266">В отличие от этого анализатор Microsoft hello выполняет лемматизация вместо морфологический поиск.</span><span class="sxs-lookup"><span data-stu-id="96fee-266">In comparison, hello Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="96fee-267">Это означает, что он гораздо лучше обрабатывает флективные и неправильные словоформы, а также позволяет получить более подходящие результаты поиска (дополнительные сведения см. в модуле 7 [презентации MVA, посвященной службе поиска Azure](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps)).</span><span class="sxs-lookup"><span data-stu-id="96fee-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="96fee-268">Индексирование с Microsoft анализаторы составляет в среднем два раза toothree медленнее, чем их эквиваленты Lucene, в зависимости от языка hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-268">Indexing with Microsoft analyzers is on average two toothree times slower than their Lucene equivalents, depending on hello language.</span></span> <span data-ttu-id="96fee-269">Время выполнения поискового запроса не должно значительно отличаться от запросов средних размеров.</span><span class="sxs-lookup"><span data-stu-id="96fee-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="96fee-270">***Конфигурация***</span><span class="sxs-lookup"><span data-stu-id="96fee-270">***Configuration***</span></span>

<span data-ttu-id="96fee-271">Для каждого поля в определении индекса hello, можно задать hello `analyzer` имя анализатора tooan свойства, которое указывает, какой язык и поставщика.</span><span class="sxs-lookup"><span data-stu-id="96fee-271">For each field in hello index definition, you can set hello `analyzer` property tooan analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="96fee-272">Здравствуйте, анализатор же будут применены при индексирования и поиска для этого поля.</span><span class="sxs-lookup"><span data-stu-id="96fee-272">hello same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="96fee-273">Например, могут быть отдельные поля для описания гостиницы английском, французском и испанском языке, существующие рядом в hello же индекс.</span><span class="sxs-lookup"><span data-stu-id="96fee-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in hello same index.</span></span> <span data-ttu-id="96fee-274">Используйте hello [параметр запроса «searchFields»](#SearchQueryParameters) toospecify toosearch какие поля конкретного языка с в запросах.</span><span class="sxs-lookup"><span data-stu-id="96fee-274">Use hello ['searchFields' query parameter](#SearchQueryParameters) toospecify which language-specific field toosearch against in your queries.</span></span> <span data-ttu-id="96fee-275">Можно просмотреть примеры запросов, которые включают hello `analyzer` свойство в [поиск документов](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="96fee-275">You can review query examples that include hello `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="96fee-276">***Список анализаторов***</span><span class="sxs-lookup"><span data-stu-id="96fee-276">***Analyzer list***</span></span>

<span data-ttu-id="96fee-277">Ниже приведен список поддерживаемых языков, а также имена анализатор Lucene и Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-277">Below is hello list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="96fee-278">Язык</span><span class="sxs-lookup"><span data-stu-id="96fee-278">Language</span></span></th>
        <th><span data-ttu-id="96fee-279">Название анализатора Майкрософт</span><span class="sxs-lookup"><span data-stu-id="96fee-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="96fee-280">Название анализатора Lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-281">Арабский</span><span class="sxs-lookup"><span data-stu-id="96fee-281">Arabic</span></span></td>
        <td><span data-ttu-id="96fee-282">ar.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-284">Армянский</span><span class="sxs-lookup"><span data-stu-id="96fee-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="96fee-285">hy.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="96fee-286">Бенгальский</span><span class="sxs-lookup"><span data-stu-id="96fee-286">Bangla</span></span></td>
        <td><span data-ttu-id="96fee-287">bn.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="96fee-288">Баскский</span><span class="sxs-lookup"><span data-stu-id="96fee-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="96fee-289">eu.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="96fee-290">Болгарский</span><span class="sxs-lookup"><span data-stu-id="96fee-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="96fee-291">bg.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-292">bg.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="96fee-293">Каталанский</span><span class="sxs-lookup"><span data-stu-id="96fee-293">Catalan</span></span></td>
        <td><span data-ttu-id="96fee-294">ca.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-295">ca.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="96fee-296">Китайский (упрощенное письмо)</span><span class="sxs-lookup"><span data-stu-id="96fee-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="96fee-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-299">Китайский (традиционное письмо)</span><span class="sxs-lookup"><span data-stu-id="96fee-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="96fee-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="96fee-302">Хорватский</span><span class="sxs-lookup"><span data-stu-id="96fee-302">Croatian</span></span></td>
        <td><span data-ttu-id="96fee-303">hr.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-304">Чешский</span><span class="sxs-lookup"><span data-stu-id="96fee-304">Czech</span></span></td>
        <td><span data-ttu-id="96fee-305">cs.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="96fee-307">Датский</span><span class="sxs-lookup"><span data-stu-id="96fee-307">Danish</span></span></td>
        <td><span data-ttu-id="96fee-308">da.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="96fee-310">Нидерландский</span><span class="sxs-lookup"><span data-stu-id="96fee-310">Dutch</span></span></td>
        <td><span data-ttu-id="96fee-311">nl.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="96fee-313">Английский</span><span class="sxs-lookup"><span data-stu-id="96fee-313">English</span></span></td>        
        <td><span data-ttu-id="96fee-314">en.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-316">Эстонский</span><span class="sxs-lookup"><span data-stu-id="96fee-316">Estonian</span></span></td>
        <td><span data-ttu-id="96fee-317">et.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-318">Финский</span><span class="sxs-lookup"><span data-stu-id="96fee-318">Finnish</span></span></td>
        <td><span data-ttu-id="96fee-319">fi.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-320">fi.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="96fee-321">Французский</span><span class="sxs-lookup"><span data-stu-id="96fee-321">French</span></span></td>
        <td><span data-ttu-id="96fee-322">fr.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-324">Галисийский</span><span class="sxs-lookup"><span data-stu-id="96fee-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="96fee-325">gl.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="96fee-326">Немецкий</span><span class="sxs-lookup"><span data-stu-id="96fee-326">German</span></span></td>
        <td><span data-ttu-id="96fee-327">de.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-329">Греческий</span><span class="sxs-lookup"><span data-stu-id="96fee-329">Greek</span></span></td>
        <td><span data-ttu-id="96fee-330">el.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-332">Гуджарати</span><span class="sxs-lookup"><span data-stu-id="96fee-332">Gujarati</span></span></td>
        <td><span data-ttu-id="96fee-333">gu.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-334">Иврит</span><span class="sxs-lookup"><span data-stu-id="96fee-334">Hebrew</span></span></td>
        <td><span data-ttu-id="96fee-335">he.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-336">Хинди</span><span class="sxs-lookup"><span data-stu-id="96fee-336">Hindi</span></span></td>
        <td><span data-ttu-id="96fee-337">hi.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-338">hi.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-339">Венгерский</span><span class="sxs-lookup"><span data-stu-id="96fee-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="96fee-340">hu.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-342">Исландский</span><span class="sxs-lookup"><span data-stu-id="96fee-342">Icelandic</span></span></td>
        <td><span data-ttu-id="96fee-343">is.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-344">Индонезийский (бахаса)</span><span class="sxs-lookup"><span data-stu-id="96fee-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="96fee-345">id.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-347">Ирландский</span><span class="sxs-lookup"><span data-stu-id="96fee-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="96fee-348">ga.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-349">Итальянский</span><span class="sxs-lookup"><span data-stu-id="96fee-349">Italian</span></span></td>
        <td><span data-ttu-id="96fee-350">it.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-352">Японский</span><span class="sxs-lookup"><span data-stu-id="96fee-352">Japanese</span></span></td>
        <td><span data-ttu-id="96fee-353">ja.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="96fee-355">Каннада</span><span class="sxs-lookup"><span data-stu-id="96fee-355">Kannada</span></span></td>
        <td><span data-ttu-id="96fee-356">ka.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-357">Корейский</span><span class="sxs-lookup"><span data-stu-id="96fee-357">Korean</span></span></td>
        <td><span data-ttu-id="96fee-358">ko.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-359">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-360">Латышский</span><span class="sxs-lookup"><span data-stu-id="96fee-360">Latvian</span></span></td>        
        <td><span data-ttu-id="96fee-361">lv.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-362">lv.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-363">Литовский</span><span class="sxs-lookup"><span data-stu-id="96fee-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="96fee-364">lt.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-365">Малаялам</span><span class="sxs-lookup"><span data-stu-id="96fee-365">Malayalam</span></span></td>
        <td><span data-ttu-id="96fee-366">ml.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-367">Малайский (латиница)</span><span class="sxs-lookup"><span data-stu-id="96fee-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="96fee-368">ms.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-369">Маратхи</span><span class="sxs-lookup"><span data-stu-id="96fee-369">Marathi</span></span></td>
        <td><span data-ttu-id="96fee-370">mr.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-371">Норвежский</span><span class="sxs-lookup"><span data-stu-id="96fee-371">Norwegian</span></span></td>
        <td><span data-ttu-id="96fee-372">nb.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-373">no.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="96fee-374">Персидский</span><span class="sxs-lookup"><span data-stu-id="96fee-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="96fee-375">fa.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="96fee-376">Польский</span><span class="sxs-lookup"><span data-stu-id="96fee-376">Polish</span></span></td>
        <td><span data-ttu-id="96fee-377">pl.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-378">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-379">Португальский (Бразилия)</span><span class="sxs-lookup"><span data-stu-id="96fee-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="96fee-380">pt-Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-381">pt-Br.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-382">Португальский (Португалия)</span><span class="sxs-lookup"><span data-stu-id="96fee-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="96fee-383">pt-Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="96fee-384">pt-Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-385">Панджаби</span><span class="sxs-lookup"><span data-stu-id="96fee-385">Punjabi</span></span></td>
        <td><span data-ttu-id="96fee-386">pa.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-387">Румынский</span><span class="sxs-lookup"><span data-stu-id="96fee-387">Romanian</span></span></td>
        <td><span data-ttu-id="96fee-388">ro.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-390">Русский</span><span class="sxs-lookup"><span data-stu-id="96fee-390">Russian</span></span></td>
        <td><span data-ttu-id="96fee-391">ru.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-392">ru.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-393">Сербский (кириллица)</span><span class="sxs-lookup"><span data-stu-id="96fee-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="96fee-394">sr-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-395">Сербский (латиница)</span><span class="sxs-lookup"><span data-stu-id="96fee-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="96fee-396">sr-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-397">Словацкий</span><span class="sxs-lookup"><span data-stu-id="96fee-397">Slovak</span></span></td>
        <td><span data-ttu-id="96fee-398">sk.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-399">Словенский</span><span class="sxs-lookup"><span data-stu-id="96fee-399">Slovenian</span></span></td>
        <td><span data-ttu-id="96fee-400">sl.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-401">Испанский</span><span class="sxs-lookup"><span data-stu-id="96fee-401">Spanish</span></span></td>
        <td><span data-ttu-id="96fee-402">es.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-403">es.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-404">Шведский</span><span class="sxs-lookup"><span data-stu-id="96fee-404">Swedish</span></span></td>
        <td><span data-ttu-id="96fee-405">sv.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="96fee-407">Тамильский</span><span class="sxs-lookup"><span data-stu-id="96fee-407">Tamil</span></span></td>
        <td><span data-ttu-id="96fee-408">ta.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-409">Телугу</span><span class="sxs-lookup"><span data-stu-id="96fee-409">Telugu</span></span></td>
        <td><span data-ttu-id="96fee-410">te.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-411">Тайский</span><span class="sxs-lookup"><span data-stu-id="96fee-411">Thai</span></span></td>
        <td><span data-ttu-id="96fee-412">th.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-413">th.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-414">Турецкий</span><span class="sxs-lookup"><span data-stu-id="96fee-414">Turkish</span></span></td>
        <td><span data-ttu-id="96fee-415">tr.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="96fee-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-417">Украинский</span><span class="sxs-lookup"><span data-stu-id="96fee-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="96fee-418">uk.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-419">Урду</span><span class="sxs-lookup"><span data-stu-id="96fee-419">Urdu</span></span></td>
        <td><span data-ttu-id="96fee-420">ur.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-421">Вьетнамский</span><span class="sxs-lookup"><span data-stu-id="96fee-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="96fee-422">vi.microsoft</span><span class="sxs-lookup"><span data-stu-id="96fee-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="96fee-423">Кроме того, в службе поиска Azure доступны независимые от языка конфигурации анализаторов.</span><span class="sxs-lookup"><span data-stu-id="96fee-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="96fee-424">Стандартное приведение к ASCII</span><span class="sxs-lookup"><span data-stu-id="96fee-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="96fee-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="96fee-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="96fee-426">Сегментация текста Юникода (стандартный лексический анализатор)</span><span class="sxs-lookup"><span data-stu-id="96fee-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="96fee-427">Фильтр свертки ASCII - преобразует символы Юникода, не принадлежащих toohello набор первых 127 символов ASCII в их эквиваленты ASCII.</span><span class="sxs-lookup"><span data-stu-id="96fee-427">ASCII folding filter - converts Unicode characters that don't belong toohello set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="96fee-428">Эта функция полезна для удаления диакритических знаков.</span><span class="sxs-lookup"><span data-stu-id="96fee-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="96fee-429">Все анализаторы, у которых в названии есть идентификатор <i>lucene</i>, работают на базе [языковых анализаторов Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="96fee-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="96fee-430">Можно найти дополнительные сведения о фильтре свертки ASCII hello [здесь](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="96fee-430">More information about hello ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="96fee-431">**Средства подбора**</span><span class="sxs-lookup"><span data-stu-id="96fee-431">**Suggesters**</span></span>

<span data-ttu-id="96fee-432">Объект `suggester` определяет поля в индексе, используемые toosupport автозавершения в поиске.</span><span class="sxs-lookup"><span data-stu-id="96fee-432">A `suggester` defines which fields in an index are used toosupport auto-complete in searches.</span></span> <span data-ttu-id="96fee-433">Обычно отправляются частичные строки поиска toohello [API предложений](#Suggestions) hello пользователь вводит запрос поиска, а hello API возвращает набор предлагаемых фраз.</span><span class="sxs-lookup"><span data-stu-id="96fee-433">Typically partial search strings are sent toohello [Suggestions API](#Suggestions) while hello user is typing a search query, and hello API returns a set of suggested phrases.</span></span> <span data-ttu-id="96fee-434">Средства подбора смысловых вариантов, определяемый в индексе hello определяет поля, используемые toobuild hello упреждающих условий.</span><span class="sxs-lookup"><span data-stu-id="96fee-434">A suggester that you define in hello index determines which fields are used toobuild hello type-ahead search terms.</span></span> <span data-ttu-id="96fee-435">Информацию о настройке см. в разделе [Средства подбора](#Suggesters).</span><span class="sxs-lookup"><span data-stu-id="96fee-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="96fee-436">**Профили оценки**</span><span class="sxs-lookup"><span data-stu-id="96fee-436">**Scoring profiles**</span></span>

<span data-ttu-id="96fee-437">Объект `scoringProfile` определяет пользовательские оценки поведений, которые позволяют влиять на элементы, отображаемые выше в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in hello search results.</span></span> <span data-ttu-id="96fee-438">Профили оценки состоят из взвешенных полей и функций.</span><span class="sxs-lookup"><span data-stu-id="96fee-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="96fee-439">toouse их, необходимо задать профиль по имени в строке запроса hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-439">toouse them, you specify a profile by name on hello query string.</span></span>

<span data-ttu-id="96fee-440">Профиль повышения по умолчанию работает за toocompute сцены hello Оценка поиска для каждого элемента в результирующем наборе.</span><span class="sxs-lookup"><span data-stu-id="96fee-440">A default scoring profile operates behind hello scenes toocompute a search score for every item in a result set.</span></span> <span data-ttu-id="96fee-441">Можно использовать профиль hello имени, внутренней оценки.</span><span class="sxs-lookup"><span data-stu-id="96fee-441">You can use hello internal, unnamed scoring profile.</span></span> <span data-ttu-id="96fee-442">Можно также задать `defaultScoringProfile` toouse пользовательского профиля по умолчанию hello, вызывается всякий раз, когда пользовательский профиль не указан в строке запроса hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-442">Alternatively, set `defaultScoringProfile` toouse a custom profile as hello default, invoked whenever a custom profile is not specified on hello query string.</span></span>

<span data-ttu-id="96fee-443">В разделе [оценки добавить профили tooa индекса поиска (API REST службы поиска Azure)](search-api-scoring-profiles-2015-02-28-preview.md) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="96fee-443">See [Add scoring profiles tooa search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="96fee-444">**Параметры CORS**</span><span class="sxs-lookup"><span data-stu-id="96fee-444">**CORS Options**</span></span>

<span data-ttu-id="96fee-445">Невозможно вызвать интерфейсы API по умолчанию Javascript на стороне клиента, поскольку hello браузер будет предотвращать все запросы независимо от источника.</span><span class="sxs-lookup"><span data-stu-id="96fee-445">Client-side Javascript cannot call any APIs by default since hello browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="96fee-446">Включить CORS (доступ к ресурсам независимо от источника), установка hello `corsOptions` атрибута tooallow запросы независимо от источника tooyour индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-446">Enable CORS (Cross-Origin Resource Sharing) by setting hello `corsOptions` attribute tooallow cross-origin queries tooyour index.</span></span> <span data-ttu-id="96fee-447">Обратите внимание на то, что по соображениям безопасности технологию CORS поддерживают только интерфейсы API запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="96fee-448">для CORS можно задать следующие параметры Hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-448">hello following options can be set for CORS:</span></span>

* <span data-ttu-id="96fee-449">`allowedOrigins`(обязательно): это список источников, которым будет предоставлен доступ tooyour индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-449">`allowedOrigins` (required): This is a list of origins that will be granted access tooyour index.</span></span> <span data-ttu-id="96fee-450">Это означает, что никакой код Javascript, запущенному из этих источников, будет разрешено tooquery индексе (при условии, что указан правильный ключ API hello).</span><span class="sxs-lookup"><span data-stu-id="96fee-450">This means that any Javascript code served from those origins will be allowed tooquery your index (assuming it provides hello correct API key).</span></span> <span data-ttu-id="96fee-451">Каждый источник обычно имеет форму hello `protocol://fully-qualified-domain-name:port` несмотря на то, что порт hello часто опускается.</span><span class="sxs-lookup"><span data-stu-id="96fee-451">Each origin is typically of hello form `protocol://fully-qualified-domain-name:port` although hello port is often omitted.</span></span> <span data-ttu-id="96fee-452">Дополнительные сведения см. в [этой статье](http://go.microsoft.com/fwlink/?LinkId=330822).</span><span class="sxs-lookup"><span data-stu-id="96fee-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="96fee-453">Источники tooall tooallow доступа, включить `*` как один элемент hello `allowedOrigins` массива.</span><span class="sxs-lookup"><span data-stu-id="96fee-453">If you want tooallow access tooall origins, include `*` as a single item in hello `allowedOrigins` array.</span></span> <span data-ttu-id="96fee-454">Напоминаем вам, что **так не рекомендуется делать в рабочих версиях служб поиска**.</span><span class="sxs-lookup"><span data-stu-id="96fee-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="96fee-455">Однако это может оказаться полезно для целей разработки или отладки.</span><span class="sxs-lookup"><span data-stu-id="96fee-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="96fee-456">`maxAgeInSeconds`(необязательно): браузеры используют это значение toodetermine hello продолжительность (в секундах) toocache предварительных ответов CORS.</span><span class="sxs-lookup"><span data-stu-id="96fee-456">`maxAgeInSeconds` (optional): Browsers use this value toodetermine hello duration (in seconds) toocache CORS preflight responses.</span></span> <span data-ttu-id="96fee-457">Это значение должно быть целой неотрицательной величиной.</span><span class="sxs-lookup"><span data-stu-id="96fee-457">This must be a non-negative integer.</span></span> <span data-ttu-id="96fee-458">Hello увеличить это значение задано, будет hello более высокую производительность, но hello больше времени, необходимое для эффекта tootake изменений политики CORS.</span><span class="sxs-lookup"><span data-stu-id="96fee-458">hello larger this value is, hello better performance will be, but hello longer it will take for CORS policy changes tootake effect.</span></span> <span data-ttu-id="96fee-459">Если это значение не задано, длительность по умолчанию составляет 5 минут.</span><span class="sxs-lookup"><span data-stu-id="96fee-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="96fee-460"><a name="CreateUpdateIndexExample"></a>
**Пример тела запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-460"><a name="CreateUpdateIndexExample"></a>
**Request Body Example**</span></span>

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

<span data-ttu-id="96fee-461">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-461">**Response**</span></span>

<span data-ttu-id="96fee-462">Для успешного запроса: "201 — Создан ресурс".</span><span class="sxs-lookup"><span data-stu-id="96fee-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="96fee-463">По умолчанию hello текст ответа будет содержать hello JSON для определения индекса hello, который был создан.</span><span class="sxs-lookup"><span data-stu-id="96fee-463">By default hello response body will contain hello JSON for hello index definition that was created.</span></span> <span data-ttu-id="96fee-464">Если hello `Prefer` заголовок запроса имеет слишком`return=minimal`, hello текст ответа будет пустым, и код состояния успеха hello будет «204 Нет содержимого» вместо «201 Создано».</span><span class="sxs-lookup"><span data-stu-id="96fee-464">If hello `Prefer` request header is set too`return=minimal`, hello response body will be empty and hello success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="96fee-465">Это верно независимо от того, было ли PUT или POST используется toocreate hello индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-465">This is true regardless of whether PUT or POST was used toocreate hello index.</span></span>

<span data-ttu-id="96fee-466">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="96fee-466">**Remarks**</span></span>

<span data-ttu-id="96fee-467">В настоящее время функции обновления схемы индекса поддерживаются в ограниченном объеме.</span><span class="sxs-lookup"><span data-stu-id="96fee-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="96fee-468">Обновления схемы, которые требуют переиндексирования (например, изменение типов полей), пока не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="96fee-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="96fee-469">Несмотря на то, что существующие поля нельзя изменить или удалить, новые поля добавляются tooan существующего индекса в любое время.</span><span class="sxs-lookup"><span data-stu-id="96fee-469">Although existing fields cannot be changed or deleted, new fields can be added tooan existing index at any time.</span></span> <span data-ttu-id="96fee-470">При добавлении нового поля все существующие документы в индексе hello автоматически будет иметь значение null для этого поля.</span><span class="sxs-lookup"><span data-stu-id="96fee-470">When a new field is added, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="96fee-471">Нет дополнительное пространство для хранения будут использоваться, пока новые документы добавляются toohello индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-471">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="96fee-472">Средства подбора</span><span class="sxs-lookup"><span data-stu-id="96fee-472">Suggesters</span></span>
<span data-ttu-id="96fee-473">функция предложений Hello в поиске Azure — это возможность упреждающего ввода или автозавершения запроса, предоставляя список потенциальных условий поиска в ответ toopartial строку входных данных, введенных в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-473">hello suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response toopartial string inputs entered into a search box.</span></span> <span data-ttu-id="96fee-474">Вы, наверняка, замечали предложения запроса при использовании коммерческих поисковых систем в Интернете. Например, если ввести в Bing ".NET", появится список условий для .NET 4.5, .NET Framework 3.5 и т. д.</span><span class="sxs-lookup"><span data-stu-id="96fee-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="96fee-475">При использовании REST API службы поиска hello, реализация вариантов поиска в настраиваемом приложении поиск Azure требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="96fee-475">When using hello Search service REST API, implementing suggestions in a custom Azure Search application requires hello following:</span></span>

* <span data-ttu-id="96fee-476">Включите варианты поиска, добавив **средства подбора** конструкция в индекс, задайте имя hello, режим поиска и список полей, для которого упреждающих вызывается.</span><span class="sxs-lookup"><span data-stu-id="96fee-476">Enable suggestions by adding a **suggester** construction in your index, giving hello name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="96fee-477">Например если указать «cityName» как поле источника, ввод частичной строки поиска «SEA» приведет к «Seattle», «Seaside» и «Seatac» (все три являются названиями реальных городов) доступно как пользователь toohello предложения запроса.</span><span class="sxs-lookup"><span data-stu-id="96fee-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions toohello user.</span></span>
* <span data-ttu-id="96fee-478">Вызовите варианты поиска, вызывающему Привет [API предложений](#Suggestions) в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="96fee-478">Invoke suggestions by calling hello [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="96fee-479">Обычно частичные строки поиска отправляются службе toohello hello пользователь вводит запрос поиска, а этот API возвращает набор предлагаемых фраз.</span><span class="sxs-lookup"><span data-stu-id="96fee-479">Typically partial search strings are sent toohello service while hello user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="96fee-480">В этой статье объясняется, как tooconfigure **средства подбора**.</span><span class="sxs-lookup"><span data-stu-id="96fee-480">This article explains how tooconfigure a **suggester**.</span></span> <span data-ttu-id="96fee-481">Следует также просмотреть hello [API предложений](#Suggestions) подробные сведения об использовании средства подбора.</span><span class="sxs-lookup"><span data-stu-id="96fee-481">You should also review hello [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="96fee-482">**Использование**</span><span class="sxs-lookup"><span data-stu-id="96fee-482">**Usage**</span></span>

<span data-ttu-id="96fee-483">`Suggesters`создаются в индексе hello и лучше всего работают при использовании определенного toosuggest документах по объектной модели, а не свободных терминов или фраз.</span><span class="sxs-lookup"><span data-stu-id="96fee-483">`Suggesters` are created in hello index and work best when used toosuggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="96fee-484">названия, имена и другие относительно небольшие фразы, которые могут определить элемент Hello наиболее кандидата поля:</span><span class="sxs-lookup"><span data-stu-id="96fee-484">hello best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="96fee-485">Менее эффективно выполняется поиск по таким полям с множеством повторяющихся элементов, как категории и теги, а также по очень длинным полям, таким как описания и комментарии.</span><span class="sxs-lookup"><span data-stu-id="96fee-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="96fee-486">Как часть определения индекса hello, можно добавить toohello одного средства подбора `suggesters` коллекции.</span><span class="sxs-lookup"><span data-stu-id="96fee-486">As part of hello index definition, you can add a single suggester toohello `suggesters` collection.</span></span> <span data-ttu-id="96fee-487">Свойства, определяющие средства подбора включить hello следующие:</span><span class="sxs-lookup"><span data-stu-id="96fee-487">Properties that define a suggester include hello following:</span></span>

* <span data-ttu-id="96fee-488">`name`: имя средства подбора hello hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-488">`name`: hello name of hello suggester.</span></span> <span data-ttu-id="96fee-489">Используйте имя средства подбора hello hello при вызове hello `suggest` API.</span><span class="sxs-lookup"><span data-stu-id="96fee-489">You use hello name of hello suggester when calling hello `suggest` API.</span></span>
* <span data-ttu-id="96fee-490">`searchMode`: hello toosearch стратегия, используемая фраз кандидатов.</span><span class="sxs-lookup"><span data-stu-id="96fee-490">`searchMode`: hello strategy used toosearch for candidate phrases.</span></span> <span data-ttu-id="96fee-491">Hello в настоящее время поддерживается только режим является `analyzingInfixMatching`, который выполняет гибкое сопоставление фраз в начале hello, или в середине предложений hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-491">hello only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at hello beginning or in hello middle of sentences.</span></span>
* <span data-ttu-id="96fee-492">`sourceFields`: Список из одного или нескольких полей, которые являются источником hello hello содержимого для предложений.</span><span class="sxs-lookup"><span data-stu-id="96fee-492">`sourceFields`: A list of one or more fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="96fee-493">Источниками могут быть только поля типов `Edm.String` и `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="96fee-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="96fee-494">Можно использовать только поля, для которых не задан настраиваемый языковой анализатор.</span><span class="sxs-lookup"><span data-stu-id="96fee-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="96fee-495">**Пример средства подбора**</span><span class="sxs-lookup"><span data-stu-id="96fee-495">**Suggester Example**</span></span>

<span data-ttu-id="96fee-496">Средства подбора является частью индекса hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-496">A suggester is part of hello index.</span></span> <span data-ttu-id="96fee-497">Может существовать только один средства подбора в hello `suggesters` коллекции поля коллекции в текущей версии hello, наряду с hello и `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="96fee-497">Only one suggester can exist in hello `suggesters` collection in hello current version, alongside hello fields collection and `scoringProfiles`.</span></span>

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> <span data-ttu-id="96fee-498">При использовании общедоступной предварительной версии поиска Azure hello `suggesters` заменяет более старое логическое свойство (`"suggestions": false`), которое поддерживало только предложения префиксов для коротких строк (3 – 25 символов).</span><span class="sxs-lookup"><span data-stu-id="96fee-498">If you used hello public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="96fee-499">Его замены `suggesters`, поддерживают инфиксные сопоставления, которые находят совпадающие термины в начале hello, или в середине содержимого поля hello счет улучшенного допуска на ошибки в строках поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at hello beginning or in hello middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="96fee-500">Начиная с выпуска общедоступной hello, теперь это единственная реализация API предложений hello hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-500">Starting with hello generally available release, this is now hello only implementation of hello suggestions API.</span></span> <span data-ttu-id="96fee-501">старые Hello `suggestions` свойства, которая была введена в `api-version=2014-07-31-Preview` продолжается toowork в этой версии, но не работает в hello `2015-02-28` или более поздней версии службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="96fee-501">hello older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues toowork in that version, but is not operational in hello `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="96fee-502">Обновление индекса</span><span class="sxs-lookup"><span data-stu-id="96fee-502">Update Index</span></span>
<span data-ttu-id="96fee-503">Обновить существующий индекс в службе поиска Azure можно с помощью HTTP-запроса PUT.</span><span class="sxs-lookup"><span data-stu-id="96fee-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="96fee-504">Обновления включают добавление новых полей toohello существующей схеме, изменение параметров CORS и изменение профилей оценки.</span><span class="sxs-lookup"><span data-stu-id="96fee-504">Updates can include adding new fields toohello existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="96fee-505">Дополнительную информацию см. в статье о [добавлении профилей оценки](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="96fee-506">Необходимо указать имя hello tooupdate индекс hello hello URI запроса:</span><span class="sxs-lookup"><span data-stu-id="96fee-506">You specify hello name of hello index tooupdate on hello request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="96fee-507">**Важно:** поддержка обновлений схемы индекса является ограниченной toooperations, не требующими перестроения индекса поиска hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-507">**Important:** Support for index schema updates is limited toooperations that don't require rebuilding hello search index.</span></span> <span data-ttu-id="96fee-508">Обновления схемы, которые требуют переиндексирования (например, изменение типов полей), пока не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="96fee-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="96fee-509">Новые поля можно добавлять в любой момент, однако изменять и удалять существующие поля пока нельзя.</span><span class="sxs-lookup"><span data-stu-id="96fee-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="96fee-510">Hello применимо и к слишком`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="96fee-510">hello same applies too`suggesters`.</span></span> <span data-ttu-id="96fee-511">Новые поля, которые могут быть добавлены средства подбора tooa в поля hello hello времени будут добавлены, но нельзя удалить поля из `suggesters` и существующие поля нельзя добавлять слишком`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="96fee-511">New fields may be added tooa suggester at hello time hello fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added too`suggesters`.</span></span>

<span data-ttu-id="96fee-512">При добавлении нового индекса tooan поля, все существующие документы в индексе hello автоматически будут иметь значение null для этого поля.</span><span class="sxs-lookup"><span data-stu-id="96fee-512">When adding a new field tooan index, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="96fee-513">Нет дополнительное пространство для хранения будут использоваться, пока новые документы добавляются toohello индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-513">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<span data-ttu-id="96fee-514">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-514">**Request**</span></span>

<span data-ttu-id="96fee-515">Все запросы к службе отправляются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96fee-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="96fee-516">Hello **обновление индекса** запроса создается с помощью HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="96fee-516">hello **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="96fee-517">С помощью метода PUT имя индекса hello является частью URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-517">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="96fee-518">Если индекс hello не существует, он создается.</span><span class="sxs-lookup"><span data-stu-id="96fee-518">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="96fee-519">Если hello индекс уже существует, это новое определение обновленных toohello.</span><span class="sxs-lookup"><span data-stu-id="96fee-519">If hello index already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="96fee-520">Имя индекса Hello должен состоять из строчных букв, начинаться с буквы или цифры, иметь нет символы косой черты или точек и быть не длиннее 128 символов.</span><span class="sxs-lookup"><span data-stu-id="96fee-520">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="96fee-521">После имени индекса hello начиная с буквы или цифры, hello остальная часть имени hello может включать любой буквы, числа и дефисы, при условии, что hello дефисы не являются последовательными.</span><span class="sxs-lookup"><span data-stu-id="96fee-521">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="96fee-522">`api-version=[string]` (обязательный).</span><span class="sxs-lookup"><span data-stu-id="96fee-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="96fee-523">Hello предварительной версии — `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-523">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-524">Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="96fee-525">**Заголовки запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-525">**Request Headers**</span></span>

<span data-ttu-id="96fee-526">Hello следующий список описывает hello необходимые и необязательные заголовки запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-526">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="96fee-527">`Content-Type`: обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="96fee-527">`Content-Type`: Required.</span></span> <span data-ttu-id="96fee-528">Установите это слишком`application/json`</span><span class="sxs-lookup"><span data-stu-id="96fee-528">Set this too`application/json`</span></span>
* <span data-ttu-id="96fee-529">`api-key`: обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="96fee-529">`api-key`: Required.</span></span> <span data-ttu-id="96fee-530">Hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-530">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="96fee-531">Это строковое значение, уникальным tooyour службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-531">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="96fee-532">Hello **обновление индекса** запрос должен включать `api-key` заголовок указать ключ администратора tooyour (как противоположность tooa ключа запроса).</span><span class="sxs-lookup"><span data-stu-id="96fee-532">hello **Update Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="96fee-533">Необходимо также hello имя tooconstruct hello запроса URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-533">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="96fee-534">Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-534">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="96fee-535">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.</span><span class="sxs-lookup"><span data-stu-id="96fee-535">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="96fee-536">**Синтаксис тела запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-536">**Request Body Syntax**</span></span>

<span data-ttu-id="96fee-537">При обновлении существующего индекса, текст hello должен содержать исходное определение схемы hello, а также hello новые поля, которые вы добавляете, а также hello изменения профилей оценки, средств подбора и параметры CORS, если таковые имеются.</span><span class="sxs-lookup"><span data-stu-id="96fee-537">When updating an existing index, hello body must include hello original schema definition, plus hello new fields you are adding, as well as hello modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="96fee-538">Если профили повышения hello и параметры CORS не изменяются, необходимо включить оригиналов hello из при создании индекса hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-538">If you are not modifying hello scoring profiles and CORS options, you must include hello originals from when hello index was created.</span></span> <span data-ttu-id="96fee-539">В целом hello наиболее toouse шаблон для обновлений является определение индекса hello tooretrieve с помощью метода GET, измените его, а затем обновить его с помощью метода PUT.</span><span class="sxs-lookup"><span data-stu-id="96fee-539">In general hello best pattern toouse for updates is tooretrieve hello index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="96fee-540">синтаксис схемы Hello использовать toocreate, индекса воспроизводится здесь для удобства.</span><span class="sxs-lookup"><span data-stu-id="96fee-540">hello schema syntax used toocreate an index is reproduced here for convenience.</span></span> <span data-ttu-id="96fee-541">Дополнительные сведения см. в разделе [Создание индекса](#CreateIndex).</span><span class="sxs-lookup"><span data-stu-id="96fee-541">See [Create Index](#CreateIndex) for more details.</span></span>

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


<span data-ttu-id="96fee-542">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-542">**Response**</span></span>

<span data-ttu-id="96fee-543">Для успешного запроса: "204 — Нет содержимого".</span><span class="sxs-lookup"><span data-stu-id="96fee-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="96fee-544">По умолчанию hello текст ответа будет пустым.</span><span class="sxs-lookup"><span data-stu-id="96fee-544">By default hello response body will be empty.</span></span> <span data-ttu-id="96fee-545">Тем не менее, если hello `Prefer` задан заголовок запроса слишком`return=representation`, hello текст ответа будет содержать hello JSON для определения индекса hello, который был обновлен.</span><span class="sxs-lookup"><span data-stu-id="96fee-545">However, if hello `Prefer` request header is set too`return=representation`, hello response body will contain hello JSON for hello index definition that was updated.</span></span> <span data-ttu-id="96fee-546">В этом случае будет hello код состояния успеха «200 OK».</span><span class="sxs-lookup"><span data-stu-id="96fee-546">In this case, hello success status code will be "200 OK".</span></span>

<span data-ttu-id="96fee-547">**Обновление определения индекса с пользовательскими анализаторами**</span><span class="sxs-lookup"><span data-stu-id="96fee-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="96fee-548">После определения анализатора, создателя маркеров, фильтра маркеров или фильтра знаков его нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="96fee-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="96fee-549">Новые шаблоны можно добавить существующий индекс tooan только в случае hello `allowIndexDowntime` tootrue установлен флаг в запрос обновления индекса hello:</span><span class="sxs-lookup"><span data-stu-id="96fee-549">New ones can be added tooan existing index only if hello `allowIndexDowntime` flag is set tootrue in hello index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="96fee-550">Обратите внимание, что эта операция будет помещена индекса в автономном режиме по крайней мере несколько секунд, вызывая вашей индексирования и запросов запрашивает toofail.</span><span class="sxs-lookup"><span data-stu-id="96fee-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests toofail.</span></span> <span data-ttu-id="96fee-551">Производительность и записи доступности hello индекса может быть несколько минут после обновления индекса hello с ослабленным зрением или больше времени для очень больших индексов.</span><span class="sxs-lookup"><span data-stu-id="96fee-551">Performance and write availability of hello index can be impaired for several minutes after hello index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="96fee-552">Получение списка индексов</span><span class="sxs-lookup"><span data-stu-id="96fee-552">List Indexes</span></span>
<span data-ttu-id="96fee-553">Hello **список индексов** возвращает список индексов hello в данный момент в службе поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="96fee-553">hello **List Indexes** operation returns a list of hello indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="96fee-554">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-554">**Request**</span></span>

<span data-ttu-id="96fee-555">Все запросы к службе отправляются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96fee-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="96fee-556">Hello **список индексов** запрос может быть создан с помощью метода GET hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-556">hello **List Indexes** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="96fee-557">`api-version=[string]` (обязательный).</span><span class="sxs-lookup"><span data-stu-id="96fee-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="96fee-558">Hello предварительной версии — `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-558">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-559">Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="96fee-560">**Заголовки запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-560">**Request Headers**</span></span>

<span data-ttu-id="96fee-561">Hello следующий список описывает hello необходимые и необязательные заголовки запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-561">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="96fee-562">`api-key`: обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="96fee-562">`api-key`: Required.</span></span> <span data-ttu-id="96fee-563">Hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-563">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="96fee-564">Это строковое значение, уникальным tooyour службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-564">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="96fee-565">Hello **список индексов** запрос должен включать `api-key` ключ администратора tooan набор (как противоположность tooa ключа запроса).</span><span class="sxs-lookup"><span data-stu-id="96fee-565">hello **List Indexes** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="96fee-566">Необходимо также hello имя tooconstruct hello запроса URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-566">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="96fee-567">Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-567">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="96fee-568">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.</span><span class="sxs-lookup"><span data-stu-id="96fee-568">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="96fee-569">**Тело запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-569">**Request Body**</span></span>

<span data-ttu-id="96fee-570">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="96fee-570">None.</span></span>

<span data-ttu-id="96fee-571">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-571">**Response**</span></span>

<span data-ttu-id="96fee-572">Код состояния: в качестве успешного ответа возвращается код "200 — ОК".</span><span class="sxs-lookup"><span data-stu-id="96fee-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="96fee-573">Вот пример тела запроса:</span><span class="sxs-lookup"><span data-stu-id="96fee-573">Here is an example response body:</span></span>

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

<span data-ttu-id="96fee-574">Обратите внимание, что можно отфильтровать ответ hello вниз toojust hello свойства, которые вас интересуют.</span><span class="sxs-lookup"><span data-stu-id="96fee-574">Note that you can filter hello response down toojust hello properties you're interested in.</span></span> <span data-ttu-id="96fee-575">Например, если требуется только список имен индексов используйте hello OData `$select` параметра запроса:</span><span class="sxs-lookup"><span data-stu-id="96fee-575">For example, if you want only a list of index names, use hello OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="96fee-576">В этом случае ответ hello hello в приведенном выше примере будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="96fee-576">In this case, hello response from hello above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="96fee-577">Это удобно toosave пропускной способности, если у вас много индексов в службе поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-577">This is a useful technique toosave bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="96fee-578">Получение индекса</span><span class="sxs-lookup"><span data-stu-id="96fee-578">Get Index</span></span>
<span data-ttu-id="96fee-579">Hello **получить индекс** операция получает hello определение индекса из поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="96fee-579">hello **Get Index** operation gets hello index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="96fee-580">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-580">**Request**</span></span>

<span data-ttu-id="96fee-581">Запросы к службе отправляются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96fee-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="96fee-582">Hello **получить индекс** запрос может быть создан с помощью метода GET hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-582">hello **Get Index** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="96fee-583">Hello [имя индекса] в URI запроса hello указывает, какой индекс tooreturn из коллекции индексов hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-583">hello [index name] in hello request URI specifies which index tooreturn from hello indexes collection.</span></span>

<span data-ttu-id="96fee-584">`api-version=[string]` (обязательный).</span><span class="sxs-lookup"><span data-stu-id="96fee-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="96fee-585">Hello предварительной версии — `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-585">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-586">Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="96fee-587">**Заголовки запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-587">**Request Headers**</span></span>

<span data-ttu-id="96fee-588">Hello следующий список описывает hello необходимые и необязательные заголовки запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-588">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="96fee-589">`api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-589">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="96fee-590">Это строковое значение, уникальным tooyour службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-590">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="96fee-591">Hello **получить индекс** запрос должен включать `api-key` ключ администратора tooan набор (как противоположность tooa ключа запроса).</span><span class="sxs-lookup"><span data-stu-id="96fee-591">hello **Get Index** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="96fee-592">Необходимо также hello имя tooconstruct hello запроса URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-592">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="96fee-593">Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-593">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="96fee-594">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.</span><span class="sxs-lookup"><span data-stu-id="96fee-594">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="96fee-595">**Тело запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-595">**Request Body**</span></span>

<span data-ttu-id="96fee-596">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="96fee-596">None.</span></span>

<span data-ttu-id="96fee-597">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-597">**Response**</span></span>

<span data-ttu-id="96fee-598">Код состояния: в качестве успешного ответа возвращается код "200 — ОК".</span><span class="sxs-lookup"><span data-stu-id="96fee-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="96fee-599">См. пример hello JSON в [создания и обновления индекса](#CreateUpdateIndexExample) пример hello полезные данные ответа.</span><span class="sxs-lookup"><span data-stu-id="96fee-599">See hello example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of hello response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="96fee-600">Удаление индекса</span><span class="sxs-lookup"><span data-stu-id="96fee-600">Delete Index</span></span>
<span data-ttu-id="96fee-601">Hello **удалить индекс** операция удаляет индекс и связанные документы из службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="96fee-601">hello **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="96fee-602">Имя индекса hello можно получить из панели мониторинга службы hello в hello портал Azure или hello API.</span><span class="sxs-lookup"><span data-stu-id="96fee-602">You can get hello index name from hello service dashboard in hello Azure portal, or from hello API.</span></span> <span data-ttu-id="96fee-603">Более подробные сведения см. в разделе [Получение списка индексов](#ListIndexes).</span><span class="sxs-lookup"><span data-stu-id="96fee-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="96fee-604">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-604">**Request**</span></span>

<span data-ttu-id="96fee-605">Запросы к службе отправляются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96fee-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="96fee-606">Hello **удалить индекс** запрос может быть создан с помощью метода DELETE hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-606">hello **Delete Index** request can be constructed using hello DELETE method.</span></span>

<span data-ttu-id="96fee-607">Hello [имя индекса] в URI запроса hello указывает, какой индекс toodelete из коллекции индексов hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-607">hello [index name] in hello request URI specifies which index toodelete from hello indexes collection.</span></span>

<span data-ttu-id="96fee-608">`api-version=[string]` (обязательный).</span><span class="sxs-lookup"><span data-stu-id="96fee-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="96fee-609">Hello предварительной версии — `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-609">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-610">Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="96fee-611">**Заголовки запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-611">**Request Headers**</span></span>

<span data-ttu-id="96fee-612">Hello следующий список описывает hello необходимые и необязательные заголовки запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-612">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="96fee-613">`api-key`: обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="96fee-613">`api-key`: Required.</span></span> <span data-ttu-id="96fee-614">Hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-614">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="96fee-615">Это строковое значение, URL-адрес службы уникальный tooyour.</span><span class="sxs-lookup"><span data-stu-id="96fee-615">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="96fee-616">Hello **удалить индекс** запрос должен включать `api-key` заголовок указать ключ администратора tooyour (как противоположность tooa ключа запроса).</span><span class="sxs-lookup"><span data-stu-id="96fee-616">hello **Delete Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="96fee-617">Необходимо также hello имя tooconstruct hello запроса URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-617">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="96fee-618">Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-618">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="96fee-619">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.</span><span class="sxs-lookup"><span data-stu-id="96fee-619">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="96fee-620">**Тело запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-620">**Request Body**</span></span>

<span data-ttu-id="96fee-621">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="96fee-621">None.</span></span>

<span data-ttu-id="96fee-622">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-622">**Response**</span></span>

<span data-ttu-id="96fee-623">Код состояния: в качестве успешного ответа возвращается код "204 — Нет содержимого".</span><span class="sxs-lookup"><span data-stu-id="96fee-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="96fee-624">Получение статистических данных индекса</span><span class="sxs-lookup"><span data-stu-id="96fee-624">Get Index Statistics</span></span>
<span data-ttu-id="96fee-625">Hello **получить статистику индекса** операция возвращает из поиска Azure количество документов для hello текущий индекс, а также об использовании хранилища.</span><span class="sxs-lookup"><span data-stu-id="96fee-625">hello **Get Index Statistics** operation returns from Azure Search a document count for hello current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="96fee-626">Статистика по количеству документов и размеру хранилища собирается каждые несколько минут, а не в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="96fee-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="96fee-627">Таким образом этот API возвращает статистику hello может не отражать изменения, вызванные последней операции индексирования.</span><span class="sxs-lookup"><span data-stu-id="96fee-627">Therefore, hello statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="96fee-628">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-628">**Request**</span></span>

<span data-ttu-id="96fee-629">Все запросы к службе отправляются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96fee-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="96fee-630">Hello **получить статистику индекса** запрос может быть создан с помощью метода GET hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-630">hello **Get Index Statistics** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="96fee-631">Hello [имя индекса] в URI запроса hello указывает hello службы tooreturn для статистики индекса hello указанному индексу.</span><span class="sxs-lookup"><span data-stu-id="96fee-631">hello [index name] in hello request URI tells hello service tooreturn index statistics for hello specified index.</span></span>

<span data-ttu-id="96fee-632">`api-version=[string]` (обязательный).</span><span class="sxs-lookup"><span data-stu-id="96fee-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="96fee-633">Hello предварительной версии — `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-633">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-634">Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="96fee-635">**Заголовки запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-635">**Request Headers**</span></span>

<span data-ttu-id="96fee-636">Hello следующий список описывает hello необходимые и необязательные заголовки запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-636">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="96fee-637">`api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-637">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="96fee-638">Это строковое значение, уникальным tooyour службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-638">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="96fee-639">Hello **получить статистику индекса** запрос должен включать `api-key` ключ администратора tooan набор (как противоположность tooa ключа запроса).</span><span class="sxs-lookup"><span data-stu-id="96fee-639">hello **Get Index Statistics** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="96fee-640">Необходимо также hello имя tooconstruct hello запроса URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-640">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="96fee-641">Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-641">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="96fee-642">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.</span><span class="sxs-lookup"><span data-stu-id="96fee-642">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="96fee-643">**Тело запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-643">**Request Body**</span></span>

<span data-ttu-id="96fee-644">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="96fee-644">None.</span></span>

<span data-ttu-id="96fee-645">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-645">**Response**</span></span>

<span data-ttu-id="96fee-646">Код состояния: в качестве успешного ответа возвращается код "200 — ОК".</span><span class="sxs-lookup"><span data-stu-id="96fee-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="96fee-647">текст ответа Hello имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="96fee-647">hello response body is in hello following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="96fee-648">Анализатор теста</span><span class="sxs-lookup"><span data-stu-id="96fee-648">Test Analyzer</span></span>
<span data-ttu-id="96fee-649">Hello **анализ API** показано, как анализатор разбивает текст на лексемы.</span><span class="sxs-lookup"><span data-stu-id="96fee-649">hello **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="96fee-650">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-650">**Request**</span></span>

<span data-ttu-id="96fee-651">Все запросы к службе отправляются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96fee-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="96fee-652">Hello **анализ API** запрос может быть создан с помощью метода POST hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-652">hello **Analyze API** request can be constructed using hello POST method.</span></span>

<span data-ttu-id="96fee-653">`api-version=[string]` (обязательный).</span><span class="sxs-lookup"><span data-stu-id="96fee-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="96fee-654">Hello предварительной версии — `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-654">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-655">Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="96fee-656">**Заголовки запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-656">**Request Headers**</span></span>

<span data-ttu-id="96fee-657">Hello следующий список описывает hello необходимые и необязательные заголовки запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-657">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="96fee-658">`api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-658">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="96fee-659">Это строковое значение, уникальным tooyour службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-659">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="96fee-660">Hello **анализ API** запрос должен включать `api-key` ключ администратора tooan набор (как противоположность tooa ключа запроса).</span><span class="sxs-lookup"><span data-stu-id="96fee-660">hello **Analyze API** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="96fee-661">Также потребуется имя индекса hello и hello имя tooconstruct hello запроса URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-661">You will also need hello index name and hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="96fee-662">Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-662">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="96fee-663">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.</span><span class="sxs-lookup"><span data-stu-id="96fee-663">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="96fee-664">**Тело запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-664">**Request Body**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="96fee-665">или</span><span class="sxs-lookup"><span data-stu-id="96fee-665">or</span></span>

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="96fee-666">Hello `analyzer_name`, `tokenizer_name`, `token_filter_name` и `char_filter_name` необходимых toobe допустимые имена встроенные или настраиваемые анализаторы, анализаторы, маркеров фильтры и фильтры char для индекса hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-666">hello `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need toobe valid names of predefined or custom analyzers, tokenizers, token filters and char filters for hello index.</span></span> <span data-ttu-id="96fee-667">toolearn дополнительных сведений о процессе hello лексической анализа в разделе [анализа в поиске Azure](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="96fee-667">toolearn more about hello process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="96fee-668">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-668">**Response**</span></span>

<span data-ttu-id="96fee-669">Код состояния: в качестве успешного ответа возвращается код "200 — ОК".</span><span class="sxs-lookup"><span data-stu-id="96fee-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="96fee-670">текст ответа Hello имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="96fee-670">hello response body is in hello following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

<span data-ttu-id="96fee-671">**Пример для API анализа**</span><span class="sxs-lookup"><span data-stu-id="96fee-671">**Analyze API example**</span></span>

<span data-ttu-id="96fee-672">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-672">**Request**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

<span data-ttu-id="96fee-673">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-673">**Response**</span></span>

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a><span data-ttu-id="96fee-674">Операции с документами</span><span class="sxs-lookup"><span data-stu-id="96fee-674">Document Operations</span></span>
<span data-ttu-id="96fee-675">В поиске Azure индекс хранится в облаке hello и заполняется с помощью документов JSON, передаче toohello службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-675">In Azure Search, an index is stored in hello cloud and populated using JSON documents that you upload toohello service.</span></span> <span data-ttu-id="96fee-676">Все отправленные документы hello составляют hello совокупность данных поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-676">All hello documents that you upload comprise hello corpus of your search data.</span></span> <span data-ttu-id="96fee-677">Документы содержат поля, некоторые из которых разбиваются на условия поиска при добавлении.</span><span class="sxs-lookup"><span data-stu-id="96fee-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="96fee-678">Hello `/docs` сегмент URL-адреса в hello API поиска Azure представляет коллекцию hello документов в индексе.</span><span class="sxs-lookup"><span data-stu-id="96fee-678">hello `/docs` URL segment in hello Azure Search API represents hello collection of documents in an index.</span></span> <span data-ttu-id="96fee-679">Все операции, выполняемые на hello коллекции, например отправка, объединение, удаление или запроса документов, выполняются в контексте отдельного индекса, поэтому URL-адреса hello hello для этих операций всегда начинаются с `/indexes/[index name]/docs` для имени данного индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-679">All operations performed on hello collection such as uploading, merging, deleting, or querying documents take place in hello context of a single index, so hello URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="96fee-680">Код приложения должен либо создать tooAzure tooupload документы JSON поиска, либо можно использовать [индексатора](https://msdn.microsoft.com/library/dn946891.aspx) tooload документов, если источник данных hello базы данных SQL Azure или Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="96fee-680">Your application code must either generate JSON documents tooupload tooAzure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents if hello data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="96fee-681">Как правило, индексы заполняются из одного указанного набора данных.</span><span class="sxs-lookup"><span data-stu-id="96fee-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="96fee-682">Необходимо запланировать наличие одного документа для каждого элемента, которое следует toosearch.</span><span class="sxs-lookup"><span data-stu-id="96fee-682">You should plan on having one document for each item that you want toosearch.</span></span> <span data-ttu-id="96fee-683">В приложении для видеопроката можно создать по одному документу для каждого фильма, в приложении для интернет-магазина — по документу для каждого номера SKU, в приложении для электронного обучения — по одному документу для каждого курса, в фирме, которая занимается научными исследованиями, — по документу для каждой научной работы из архива и т. д.</span><span class="sxs-lookup"><span data-stu-id="96fee-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="96fee-684">Документы состоят из одного или нескольких полей.</span><span class="sxs-lookup"><span data-stu-id="96fee-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="96fee-685">Поля могут содержать текст, который разбит службой поиска Azure на условия поиска, а также неразбитые и нетекстовые значения, которые можно использовать в фильтрах и профилях оценки.</span><span class="sxs-lookup"><span data-stu-id="96fee-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="96fee-686">Hello имена, типы данных и функции поиска, поддерживаемые для каждого поля определяются hello схемы индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-686">hello names, data types, and search features supported for each field are determined by hello index schema.</span></span> <span data-ttu-id="96fee-687">Одно из полей hello в каждой схеме индекса необходимо назначить в качестве идентификатора, и каждый документ должен иметь значение для поля идентификатора hello, однозначно определяющее этот документ в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-687">One of hello fields in each index schema must be designated as an ID, and each document must have a value for hello ID field that uniquely identifies that document in hello index.</span></span> <span data-ttu-id="96fee-688">Все прочие поля документа являются необязательными и будут по умолчанию tooa значение null, если не указано иное.</span><span class="sxs-lookup"><span data-stu-id="96fee-688">All other document fields are optional and will default tooa null value if left unspecified.</span></span> <span data-ttu-id="96fee-689">Обратите внимание, что значения null не занимают места в индекс поиска hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-689">Note that null values do not take up space in hello search index.</span></span>

<span data-ttu-id="96fee-690">Перед отправкой документов необходимо hello индекса, уже созданные в службе hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-690">Before you can upload documents, you must have already created hello index on hello service.</span></span> <span data-ttu-id="96fee-691">Подробные сведения о выполнении этого первого этапа см. в разделе [Создание индекса](#CreateIndex).</span><span class="sxs-lookup"><span data-stu-id="96fee-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="96fee-692">Добавления, обновления и удаления документов</span><span class="sxs-lookup"><span data-stu-id="96fee-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="96fee-693">Для добавления, объединения, объединения/добавления и удаления документов в определенном индексе используются HTTP-запросы POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="96fee-694">Для большого количества обновлений рекомендуется использовать пакетную обработку документов (too1000 документов на пакет) или около 16 МБ в пакете.</span><span class="sxs-lookup"><span data-stu-id="96fee-694">For large numbers of updates, batching of documents (up too1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="96fee-695">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-695">**Request**</span></span>

<span data-ttu-id="96fee-696">Все запросы к службе отправляются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96fee-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="96fee-697">Для добавления, объединения, объединения/добавления и удаления документов в определенном индексе используются HTTP-запросы POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="96fee-698">Hello URI запроса содержит [имя индекса], указав какие документы toopost индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-698">hello request URI includes [index name], specifying which index toopost documents.</span></span> <span data-ttu-id="96fee-699">Только вы можете публиковать документы tooone индекса одновременно.</span><span class="sxs-lookup"><span data-stu-id="96fee-699">You can only post documents tooone index at a time.</span></span>

<span data-ttu-id="96fee-700">`api-version=[string]` (обязательный).</span><span class="sxs-lookup"><span data-stu-id="96fee-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="96fee-701">Hello предварительной версии — `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-701">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-702">Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="96fee-703">**Заголовки запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-703">**Request Headers**</span></span>

<span data-ttu-id="96fee-704">Hello следующий список описывает hello необходимые и необязательные заголовки запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-704">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="96fee-705">`Content-Type`: обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="96fee-705">`Content-Type`: Required.</span></span> <span data-ttu-id="96fee-706">Установите это слишком`application/json`</span><span class="sxs-lookup"><span data-stu-id="96fee-706">Set this too`application/json`</span></span>
* <span data-ttu-id="96fee-707">`api-key`: обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="96fee-707">`api-key`: Required.</span></span> <span data-ttu-id="96fee-708">Hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-708">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="96fee-709">Это строковое значение, уникальным tooyour службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-709">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="96fee-710">Hello **добавьте документы** запрос должен включать `api-key` заголовок указать ключ администратора tooyour (как противоположность tooa ключа запроса).</span><span class="sxs-lookup"><span data-stu-id="96fee-710">hello **Add Documents** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="96fee-711">Необходимо также hello имя tooconstruct hello запроса URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-711">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="96fee-712">Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-712">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="96fee-713">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.</span><span class="sxs-lookup"><span data-stu-id="96fee-713">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="96fee-714">**Тело запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-714">**Request Body**</span></span>

<span data-ttu-id="96fee-715">Hello тексте hello запроса содержит один или несколько документов toobe индексированных.</span><span class="sxs-lookup"><span data-stu-id="96fee-715">hello body of hello request contains one or more documents toobe indexed.</span></span> <span data-ttu-id="96fee-716">Документы идентифицируются уникальным ключом.</span><span class="sxs-lookup"><span data-stu-id="96fee-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="96fee-717">С каждым документом связывается действие: добавить, объединить, объединить или добавить либо удалить.</span><span class="sxs-lookup"><span data-stu-id="96fee-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="96fee-718">Отправка запросов должен включать данные документа hello как набор пар «ключ значение».</span><span class="sxs-lookup"><span data-stu-id="96fee-718">Upload requests must include hello document data as a set of key/value pairs.</span></span>

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> <span data-ttu-id="96fee-719">Ключи документа могут содержать только буквы, цифры, дефисы ("–"), знак подчеркивания ("_") и знак равенства ("=").</span><span class="sxs-lookup"><span data-stu-id="96fee-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="96fee-720">Дополнительные сведения см. в разделе [Правила именования](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="96fee-721">**Действия с документами**</span><span class="sxs-lookup"><span data-stu-id="96fee-721">**Document Actions**</span></span>

* <span data-ttu-id="96fee-722">`upload`: Действие отправки — примерно tooan «вставки-обновления» где документ hello будет вставлена, если является новым и обновлен или заменен, если он существует.</span><span class="sxs-lookup"><span data-stu-id="96fee-722">`upload`: An upload action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="96fee-723">Обратите внимание, что в случае обновления hello заменяются все поля.</span><span class="sxs-lookup"><span data-stu-id="96fee-723">Note that all fields are replaced in hello update case.</span></span>
* <span data-ttu-id="96fee-724">`merge`: Обновления слияния, существующий документ с hello указаны поля.</span><span class="sxs-lookup"><span data-stu-id="96fee-724">`merge`: Merge updates an existing document with hello specified fields.</span></span> <span data-ttu-id="96fee-725">Если документ hello не существует, объединение hello завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="96fee-725">If hello document doesn't exist, hello merge will fail.</span></span> <span data-ttu-id="96fee-726">Любое поле, указанное для объединения приведет к замене существующего поля hello в документе hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-726">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="96fee-727">Это относится и к полям типа `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="96fee-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="96fee-728">Например, если hello документ содержит поле «теги» со значением `["budget"]` , и вы выполните объединение со значением `["economy", "pool"]` для «теги» hello окончательное значение поля hello «теги» будет `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="96fee-728">For example, if hello document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", hello final value of hello "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="96fee-729">а **не** `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="96fee-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="96fee-730">`mergeOrUpload`: ведет себя как `merge` Если документ с hello заданным ключом уже существует в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-730">`mergeOrUpload`: behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="96fee-731">Если существует документ hello ведет себя как `upload` с новым документом.</span><span class="sxs-lookup"><span data-stu-id="96fee-731">If hello document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="96fee-732">`delete`: Удалить удаляет hello указанный документ из индекса hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-732">`delete`: Delete removes hello specified document from hello index.</span></span> <span data-ttu-id="96fee-733">Обратите внимание, что все поля, укажите в `delete` операции, отличной от hello ключевое поле будет игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="96fee-733">Note that any fields you specify in a `delete` operation other than hello key field will be ignored.</span></span> <span data-ttu-id="96fee-734">Tooremove отдельного поля из документа, используйте `merge` вместо и просто задать поле hello явным образом слишком`null`.</span><span class="sxs-lookup"><span data-stu-id="96fee-734">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly too`null`.</span></span>

<span data-ttu-id="96fee-735">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-735">**Response**</span></span>

<span data-ttu-id="96fee-736">Код состояния: при успешном выполнении возвращается код "200 — ОК", указывающий на то, что все элементы проиндексированы.</span><span class="sxs-lookup"><span data-stu-id="96fee-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="96fee-737">Это обозначается hello `status` свойство tootrue для всех элементов, а также hello `statusCode` свойство tooeither 201 (для загруженных документов) или 200 (для слияния или удаления документов):</span><span class="sxs-lookup"><span data-stu-id="96fee-737">This is indicated by hello `status` property being set tootrue for all items, as well as hello `statusCode` property being set tooeither 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

<span data-ttu-id="96fee-738">Код состояния 207 (множественное состояние) возвращается, если хотя бы один элемент не удалось проиндексировать.</span><span class="sxs-lookup"><span data-stu-id="96fee-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="96fee-739">Элементы, которые не были проиндексированы имеют hello `status` toofalse набор полей.</span><span class="sxs-lookup"><span data-stu-id="96fee-739">Items that have not been indexed have hello `status` field set toofalse.</span></span> <span data-ttu-id="96fee-740">Hello `errorMessage` и `statusCode` свойства указывают, hello причину ошибки индексирования hello:</span><span class="sxs-lookup"><span data-stu-id="96fee-740">hello `errorMessage` and `statusCode` properties will indicate hello reason for hello indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="96fee-741">Hello в следующей таблице описывается hello различных на уровне документа коды состояния, которые могут быть возвращены в ответе hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-741">hello following table explains hello various per-document status codes that can be returned in hello response.</span></span> <span data-ttu-id="96fee-742">Обратите внимание, что некоторые указывают на проблемы hello запроса, пока другие описания временных ошибок.</span><span class="sxs-lookup"><span data-stu-id="96fee-742">Note that some indicate problems with hello request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="96fee-743">последний Hello следует повторить через некоторое время.</span><span class="sxs-lookup"><span data-stu-id="96fee-743">hello latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="96fee-744">Код состояния</span><span class="sxs-lookup"><span data-stu-id="96fee-744">Status code</span></span></th>
        <th><span data-ttu-id="96fee-745">Значение</span><span class="sxs-lookup"><span data-stu-id="96fee-745">Meaning</span></span></th>
        <th><span data-ttu-id="96fee-746">Возможность повторной попытки</span><span class="sxs-lookup"><span data-stu-id="96fee-746">Retryable</span></span></th>
        <th><span data-ttu-id="96fee-747">Примечания</span><span class="sxs-lookup"><span data-stu-id="96fee-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-748">200</span><span class="sxs-lookup"><span data-stu-id="96fee-748">200</span></span></td>
        <td><span data-ttu-id="96fee-749">Документ был успешно изменен или удален.</span><span class="sxs-lookup"><span data-stu-id="96fee-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="96fee-750">Недоступно</span><span class="sxs-lookup"><span data-stu-id="96fee-750">n/a</span></span></td>
        <td><span data-ttu-id="96fee-751">Операции удаления являются <a href="https://en.wikipedia.org/wiki/Idempotence">идемпотентными</a>.</span><span class="sxs-lookup"><span data-stu-id="96fee-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="96fee-752">То есть даже если ключ документа не существует в индексе hello, попытка операции удаления с этим ключом приведет к код состояния 200.</span><span class="sxs-lookup"><span data-stu-id="96fee-752">That is, even if a document key does not exist in hello index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-753">201</span><span class="sxs-lookup"><span data-stu-id="96fee-753">201</span></span></td>
        <td><span data-ttu-id="96fee-754">Документ создан.</span><span class="sxs-lookup"><span data-stu-id="96fee-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="96fee-755">Недоступно</span><span class="sxs-lookup"><span data-stu-id="96fee-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-756">400</span><span class="sxs-lookup"><span data-stu-id="96fee-756">400</span></span></td>
        <td><span data-ttu-id="96fee-757">Ошибка в документе hello, препятствующая индексируется.</span><span class="sxs-lookup"><span data-stu-id="96fee-757">There was an error in hello document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="96fee-758">Нет</span><span class="sxs-lookup"><span data-stu-id="96fee-758">No</span></span></td>
        <td><span data-ttu-id="96fee-759">Hello в ответ hello появится сообщение об неверные hello документа.</span><span class="sxs-lookup"><span data-stu-id="96fee-759">hello error message in hello response will indicate what is wrong with hello document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-760">404</span><span class="sxs-lookup"><span data-stu-id="96fee-760">404</span></span></td>
        <td><span data-ttu-id="96fee-761">не удалось объединить документ Hello hello ключ не существует в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-761">hello document could not be merged because hello given key doesn't exist in hello index.</span></span></td>
        <td><span data-ttu-id="96fee-762">Нет</span><span class="sxs-lookup"><span data-stu-id="96fee-762">No</span></span></td>
        <td><span data-ttu-id="96fee-763">Эта ошибка не возникает при передаче файлов, так как в этом случае создаются новые документы. Не возникает она и при удалении, так как такие операции являются <a href="https://en.wikipedia.org/wiki/Idempotence">идемпотентными</a>.</span><span class="sxs-lookup"><span data-stu-id="96fee-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-764">409</span><span class="sxs-lookup"><span data-stu-id="96fee-764">409</span></span></td>
        <td><span data-ttu-id="96fee-765">Конфликт версий была обнаружена при попытке tooindex документа.</span><span class="sxs-lookup"><span data-stu-id="96fee-765">A version conflict was detected when attempting tooindex a document.</span></span></td>
        <td><span data-ttu-id="96fee-766">Да</span><span class="sxs-lookup"><span data-stu-id="96fee-766">Yes</span></span></td>
        <td><span data-ttu-id="96fee-767">Это может произойти, если вы пытаетесь hello tooindex же документов на более чем один раз одновременно.</span><span class="sxs-lookup"><span data-stu-id="96fee-767">This can happen when you're trying tooindex hello same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-768">422</span><span class="sxs-lookup"><span data-stu-id="96fee-768">422</span></span></td>
        <td><span data-ttu-id="96fee-769">Индекс Hello временно недоступен, так как он был обновлен с too'true набор флаг allowIndexDowntime «hello» ".</span><span class="sxs-lookup"><span data-stu-id="96fee-769">hello index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'.</span></span></td>
        <td><span data-ttu-id="96fee-770">Да</span><span class="sxs-lookup"><span data-stu-id="96fee-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="96fee-771">503</span><span class="sxs-lookup"><span data-stu-id="96fee-771">503</span></span></td>
        <td><span data-ttu-id="96fee-772">Службе поиска временно недоступна, возможно, из-за tooheavy нагрузки.</span><span class="sxs-lookup"><span data-stu-id="96fee-772">Your search service is temporarily unavailable, possibly due tooheavy load.</span></span></td>
        <td><span data-ttu-id="96fee-773">Да</span><span class="sxs-lookup"><span data-stu-id="96fee-773">Yes</span></span></td>
        <td><span data-ttu-id="96fee-774">Код должен ожидания перед повтором попытки в данном случае или существует риск недоступности службы hello продление срока.</span><span class="sxs-lookup"><span data-stu-id="96fee-774">Your code should wait before retrying in this case or you risk prolonging hello service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="96fee-775">**Примечание**: Если код клиента часто сталкивается 207 ответа, одна из возможных причин является hello системы под нагрузкой.</span><span class="sxs-lookup"><span data-stu-id="96fee-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that hello system is under load.</span></span> <span data-ttu-id="96fee-776">Это можно проверить, проверив hello `statusCode` свойство 503.</span><span class="sxs-lookup"><span data-stu-id="96fee-776">You can confirm this by checking hello `statusCode` property for 503.</span></span> <span data-ttu-id="96fee-777">Если это так hello, мы рекомендуем ***регулирование запросов индексирования***.</span><span class="sxs-lookup"><span data-stu-id="96fee-777">If this is hello case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="96fee-778">В противном случае если трафик индексирования не уменьшится, hello системы может начать отклонять все запросы с ошибкой "503".</span><span class="sxs-lookup"><span data-stu-id="96fee-778">Otherwise, if indexing traffic doesn't subside, hello system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="96fee-779">Код состояния 429 указывает, что вы превысили квоту на число hello документов в индекс.</span><span class="sxs-lookup"><span data-stu-id="96fee-779">Status code 429 indicates that you have exceeded your quota on hello number of documents per index.</span></span> <span data-ttu-id="96fee-780">В этом случае нужно создать новый индекс или повысить предельную емкость.</span><span class="sxs-lookup"><span data-stu-id="96fee-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="96fee-781">**Пример**</span><span class="sxs-lookup"><span data-stu-id="96fee-781">**Example:**</span></span>

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
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a><span data-ttu-id="96fee-782">Поиск документов</span><span class="sxs-lookup"><span data-stu-id="96fee-782">Search Documents</span></span>
<span data-ttu-id="96fee-783">Объект **поиска** операции выдается как запрос GET или POST и указывает параметры, которые предоставляют hello критерии для отбора соответствующих документов.</span><span class="sxs-lookup"><span data-stu-id="96fee-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give hello criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="96fee-784">**При УЧЕТЕ toouse вместо GET**</span><span class="sxs-lookup"><span data-stu-id="96fee-784">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="96fee-785">При использовании HTTP GET hello toocall **поиска** API-интерфейса, необходимо помнить, что длина URL-адрес запроса hello hello не может превышать 8 КБ toobe.</span><span class="sxs-lookup"><span data-stu-id="96fee-785">When you use HTTP GET toocall hello **Search** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="96fee-786">Для большинства приложений этого достаточно.</span><span class="sxs-lookup"><span data-stu-id="96fee-786">This is usually enough for most applications.</span></span> <span data-ttu-id="96fee-787">В то же время некоторые приложения создают очень длинные запросы или выражения фильтров OData.</span><span class="sxs-lookup"><span data-stu-id="96fee-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="96fee-788">Лучший вариант для этих приложений — использование запроса HTTP POST, так как он позволяет увеличить фильтры и запросы по сравнению с GET.</span><span class="sxs-lookup"><span data-stu-id="96fee-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="96fee-789">С помощью POST, номер hello из выражений или предложения в запросе hello ограничивается коэффициент не hello размер hello необработанных запросов с момента hello предельного размера запроса для POST — приблизительно 16 МБ.</span><span class="sxs-lookup"><span data-stu-id="96fee-789">With POST, hello number of terms or clauses in a query is hello limiting factor, not hello size of hello raw query since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-790">Несмотря на то, что ограничение на размер запроса POST hello очень велика, поисковые запросы и выражения фильтра не может быть произвольным и довольно сложным.</span><span class="sxs-lookup"><span data-stu-id="96fee-790">Even though hello POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="96fee-791">Дополнительные сведения об ограничениях по сложности для запросов и фильтров поиска см. в статьях, посвященных [синтаксису запросов Lucene](https://msdn.microsoft.com/library/mt589323.aspx) и [синтаксису выражений OData](https://msdn.microsoft.com/library/dn798921.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="96fee-792">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-792">**Request**</span></span>

<span data-ttu-id="96fee-793">Запросы к службе отправляются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96fee-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="96fee-794">Hello **поиска** можно составить запрос методы с помощью hello GET или POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-794">hello **Search** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="96fee-795">URI запроса Hello указывает, какие tooquery индекса, для всех документов, соответствующих параметрам hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-795">hello request URI specifies which index tooquery, for all documents that match hello parameters.</span></span> <span data-ttu-id="96fee-796">Параметры указываются в строке запроса hello в случае hello запросов GET, а в запросе hello запрашивает текст в случае, когда hello POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-796">Parameters are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="96fee-797">Рекомендуется при создании запросов GET, следует помнить слишком[кодирование URL-адрес](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) конкретного запроса, параметров при вызове hello REST API напрямую.</span><span class="sxs-lookup"><span data-stu-id="96fee-797">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="96fee-798">Для операций **поиска** в число таких параметров входят:</span><span class="sxs-lookup"><span data-stu-id="96fee-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="96fee-799">Кодировка URL рекомендуется только для hello выше параметров запроса.</span><span class="sxs-lookup"><span data-stu-id="96fee-799">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="96fee-800">Если вы случайно URL-кодировали hello вся строка запроса (все после hello?), запросы будут нарушены.</span><span class="sxs-lookup"><span data-stu-id="96fee-800">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="96fee-801">Кроме того URL-кодирование необходима только при вызове hello получить напрямую с помощью API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="96fee-801">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="96fee-802">Кодировка URL-адрес не является обязательным при вызове **поиска** с помощью запроса POST, или при использовании hello [клиентская библиотека .NET](https://msdn.microsoft.com/library/dn951165.aspx), обрабатывающая для кодирования URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="96fee-802">No URL encoding is necessary when calling **Search** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="96fee-803"><a name="SearchQueryParameters"></a>
**Параметры запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="96fee-804">**Поиск** принимает несколько параметров, которые сообщают условия запроса и определяют способы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="96fee-805">Укажите эти параметры в URL-АДРЕСЕ hello строку запроса, при вызове **поиска** через GET, а также как свойства JSON в теле запроса hello при вызове **поиска** помощью POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-805">You provide these parameters in hello URL query string when calling **Search** via GET, and as JSON properties in hello request body when calling **Search** via POST.</span></span> <span data-ttu-id="96fee-806">синтаксис Hello для некоторых параметров немного отличается от GET и POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-806">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="96fee-807">Эти различия описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="96fee-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="96fee-808">`search=[string]`(необязательно) — текст toosearch для hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-808">`search=[string]` (optional) - hello text toosearch for.</span></span> <span data-ttu-id="96fee-809">По умолчанию ведется поиск по всем полям с атрибутом `searchable`, если не задан параметр `searchFields`.</span><span class="sxs-lookup"><span data-stu-id="96fee-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="96fee-810">При поиске `searchable` поля hello поиска сам текст размечается, поэтому несколько условий может отделяться пробелами (например: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="96fee-810">When searching `searchable` fields, hello search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="96fee-811">Используйте любой термин toomatch `*` (это может быть полезно для логической фильтрации запросов).</span><span class="sxs-lookup"><span data-stu-id="96fee-811">toomatch any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="96fee-812">Пропуск этого параметра имеет тот же эффект, как и настройка его слишком hello`*`.</span><span class="sxs-lookup"><span data-stu-id="96fee-812">Omitting this parameter has hello same effect as setting it too`*`.</span></span> <span data-ttu-id="96fee-813">В разделе [простой синтаксис запроса](https://msdn.microsoft.com/library/dn798920.aspx) конкретные сведения по синтаксису поиска hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on hello search syntax.</span></span>

* <span data-ttu-id="96fee-814">**Примечание**: hello результаты могут оказаться сюрпризом при выполнении запросов через `searchable` поля.</span><span class="sxs-lookup"><span data-stu-id="96fee-814">**Note**: hello results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="96fee-815">Hello разметчик содержит логику toohandle случаях общий tooEnglish текст как апострофы, запятые номера, и т. д. Например `search=123,456` будет соответствовать одному термину 123,456, а не hello отдельным терминам 123 и 456, так как запятые используются в качестве разделителя тысяч для больших чисел в английском языке.</span><span class="sxs-lookup"><span data-stu-id="96fee-815">hello tokenizer includes logic toohandle cases common tooEnglish text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than hello individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="96fee-816">По этой причине рекомендуется использовать пробелы, а не знаки пунктуации tooseparate термины в hello `search` параметра.</span><span class="sxs-lookup"><span data-stu-id="96fee-816">For this reason, we recommend using white space rather than punctuation tooseparate terms in hello `search` parameter.</span></span>

<span data-ttu-id="96fee-817">`searchMode=any|all`(необязательно, по умолчанию слишком`any`) — ли любые или все условия поиска hello в документе hello toocount порядок соответствия должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="96fee-817">`searchMode=any|all` (optional, defaults too`any`) - whether any or all of hello search terms must be matched in order toocount hello document as a match.</span></span>

<span data-ttu-id="96fee-818">`searchFields=[string]`(необязательно) — список hello toosearch имена полей с разделителями запятыми для hello указанный текст.</span><span class="sxs-lookup"><span data-stu-id="96fee-818">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified text.</span></span> <span data-ttu-id="96fee-819">Для целевых полей должен быть задан атрибут `searchable`.</span><span class="sxs-lookup"><span data-stu-id="96fee-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="96fee-820">`queryType=simple|full`(необязательно, по умолчанию слишком`simple`) — Если текста слишком «простой» поиск набора интерпретируется на любом языке простой запрос, позволяющий символы, такие как +, * и «».</span><span class="sxs-lookup"><span data-stu-id="96fee-820">`queryType=simple|full` (optional, defaults too`simple`) - when set too"simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="96fee-821">Запросы вычисляются для всех полей поиска (или полей, указанных в `searchFields`) в каждом документе по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="96fee-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="96fee-822">Если тип запроса hello задано слишком`full` поиск текста интерпретируется с использованием языка запросов Lucene hello, который позволяет выполнять поиск конкретных полей и Взвешенное.</span><span class="sxs-lookup"><span data-stu-id="96fee-822">When hello query type is set too`full` search text is interpreted using hello Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="96fee-823">В разделе [простой синтаксис запроса](https://msdn.microsoft.com/library/dn798920.aspx) и [синтаксис запроса Lucene](https://msdn.microsoft.com/library/mt589323.aspx) приведены конкретные сведения о синтаксисов поиска hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on hello search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="96fee-824">Диапазон поиска в hello Lucene язык запросов не поддерживается в пользу $filter обеспечивающую аналогичные функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="96fee-824">Range search in hello Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="96fee-825">`moreLikeThis=[key]` (необязательный) **Внимание!** Эта функция доступна только в версии `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-826">Этот параметр не может использоваться в запросе, который содержит параметр поиска текста hello, `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="96fee-826">This option cannot be used in a query that contains hello text search parameter, `search=[string]`.</span></span> <span data-ttu-id="96fee-827">Hello `moreLikeThis` параметр находит документы, аналогичные toohello документа, указанного в ключе документа hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-827">hello `moreLikeThis` parameter finds documents that are similar toohello document specified by hello document key.</span></span> <span data-ttu-id="96fee-828">При запросе поиска с `moreLikeThis`, список условий поиска создается на основе частоты hello и rarity терминов в исходном документе hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on hello frequency and rarity of terms in hello source document.</span></span> <span data-ttu-id="96fee-829">Эти термины, то используется toomake hello запроса.</span><span class="sxs-lookup"><span data-stu-id="96fee-829">Those terms are then used toomake hello request.</span></span> <span data-ttu-id="96fee-830">По умолчанию hello содержимое всех `searchable` поля считаются в том случае, если не `searchFields` — используется toorestrict вестись какие поля.</span><span class="sxs-lookup"><span data-stu-id="96fee-830">By default, hello contents of all `searchable` fields are considered unless `searchFields` is used toorestrict which fields are searched.</span></span>  

<span data-ttu-id="96fee-831">`$skip=#`(необязательно) — hello число поиска результатов tooskip; Не может быть больше 100 000.</span><span class="sxs-lookup"><span data-stu-id="96fee-831">`$skip=#` (optional) - hello number of search results tooskip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="96fee-832">Если требуется tooscan документов в последовательности, но нельзя использовать `$skip` из-за ограничений toothis, рассмотрите возможность использования `$orderby` с полностью упорядоченным ключом и `$filter` с запросом к диапазону вместо.</span><span class="sxs-lookup"><span data-stu-id="96fee-832">If you need tooscan documents in sequence but cannot use `$skip` due toothis limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-833">При вызове **поиска** с помощью запроса POST этот параметр называется `skip`, а не `$skip`.</span><span class="sxs-lookup"><span data-stu-id="96fee-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="96fee-834">`$top=#`(необязательно) — hello число поиска результатов tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="96fee-834">`$top=#` (optional) - hello number of search results tooretrieve.</span></span> <span data-ttu-id="96fee-835">Это можно использовать в сочетании с `$skip` постраничный просмотр на стороне клиента tooimplement результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-835">This can be used in conjunction with `$skip` tooimplement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-836">При вызове **поиска** с помощью запроса POST этот параметр называется `top`, а не `$top`.</span><span class="sxs-lookup"><span data-stu-id="96fee-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="96fee-837">`$count=true|false`(необязательно, по умолчанию слишком`false`) — указывает, является ли toofetch hello общее количество результатов.</span><span class="sxs-lookup"><span data-stu-id="96fee-837">`$count=true|false` (optional, defaults too`false`) - Specifies whether toofetch hello total count of results.</span></span> <span data-ttu-id="96fee-838">Это число hello все документы, которые соответствуют hello `search` и `$filter` параметров, игнорируя `$top` и `$skip`.</span><span class="sxs-lookup"><span data-stu-id="96fee-838">This is hello count of all documents that match hello `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="96fee-839">Установка этого значения слишком`true` может негативно сказаться на производительности.</span><span class="sxs-lookup"><span data-stu-id="96fee-839">Setting this value too`true` may have a performance impact.</span></span> <span data-ttu-id="96fee-840">Обратите внимание, что возврат сведений о количестве hello является приближением.</span><span class="sxs-lookup"><span data-stu-id="96fee-840">Note that hello count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-841">При вызове **поиска** с помощью запроса POST этот параметр называется `count`, а не `$count`.</span><span class="sxs-lookup"><span data-stu-id="96fee-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="96fee-842">`$orderby=[string]`(необязательно) — список выражений, разделенных запятыми toosort hello результаты по.</span><span class="sxs-lookup"><span data-stu-id="96fee-842">`$orderby=[string]` (optional) - A list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="96fee-843">Каждое выражение может быть именем поля или toohello вызов `geo.distance()` функции.</span><span class="sxs-lookup"><span data-stu-id="96fee-843">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="96fee-844">Каждое выражение может следовать `asc` tooindicated по возрастанию, и `desc` tooindicate по убыванию.</span><span class="sxs-lookup"><span data-stu-id="96fee-844">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="96fee-845">по умолчанию Hello по возрастанию.</span><span class="sxs-lookup"><span data-stu-id="96fee-845">hello default is ascending order.</span></span> <span data-ttu-id="96fee-846">Предложение WITH TIES будет нарушено из hello оценки совпадения документов.</span><span class="sxs-lookup"><span data-stu-id="96fee-846">Ties will be broken by hello match scores of documents.</span></span> <span data-ttu-id="96fee-847">Если не `$orderby` указан, порядок сортировки по умолчанию hello — по убыванию по оценке совпадения документа.</span><span class="sxs-lookup"><span data-stu-id="96fee-847">If no `$orderby` is specified, hello default sort order is descending by document match score.</span></span> <span data-ttu-id="96fee-848">Максимальное количество предложений `$orderby`— 32.</span><span class="sxs-lookup"><span data-stu-id="96fee-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-849">При вызове **поиска** с помощью запроса POST этот параметр называется `orderby`, а не `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="96fee-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="96fee-850">`$select=[string]`(необязательно) — список tooretrieve полей с разделителями запятыми.</span><span class="sxs-lookup"><span data-stu-id="96fee-850">`$select=[string]` (optional) - A list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="96fee-851">Если не указан, включаются все поля, помеченные как извлекаемые в схеме hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-851">If unspecified, all fields marked as retrievable in hello schema are included.</span></span> <span data-ttu-id="96fee-852">Можно также явно запросить все поля, установив этот параметр слишком`*`.</span><span class="sxs-lookup"><span data-stu-id="96fee-852">You can also explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-853">При вызове **поиска** с помощью запроса POST этот параметр называется `select`, а не `$select`.</span><span class="sxs-lookup"><span data-stu-id="96fee-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="96fee-854">`facet=[string]`(ноль или более) - toofacet поле по.</span><span class="sxs-lookup"><span data-stu-id="96fee-854">`facet=[string]` (zero or more) - A field toofacet by.</span></span> <span data-ttu-id="96fee-855">При необходимости строка hello может содержать параметры toocustomize hello аспекты выраженное запятыми `name:value` пары.</span><span class="sxs-lookup"><span data-stu-id="96fee-855">Optionally hello string may contain parameters toocustomize hello faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="96fee-856">Ниже перечислены возможные параметры.</span><span class="sxs-lookup"><span data-stu-id="96fee-856">Valid parameters are:</span></span>

* <span data-ttu-id="96fee-857">`count` (максимальное количество условий аспектирования; значение по умолчанию — 10).</span><span class="sxs-lookup"><span data-stu-id="96fee-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="96fee-858">Отсутствие максимума, но более высокие значения к снижению соответствующей производительности, особенно в том случае, если поля hello аспекта содержит большое количество уникальных условий.</span><span class="sxs-lookup"><span data-stu-id="96fee-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if hello faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="96fee-859">Например: `facet=category,count:5` возвращает hello top пять категорий в результатах аспекта.</span><span class="sxs-lookup"><span data-stu-id="96fee-859">For example: `facet=category,count:5` gets hello top five categories in facet results.</span></span>  
  * <span data-ttu-id="96fee-860">**Примечание**: Если hello `count` параметр меньше hello число уникальных слов, hello результатов может оказаться неточным.</span><span class="sxs-lookup"><span data-stu-id="96fee-860">**Note**: If hello `count` parameter is less than hello number of unique terms, hello results may not be accurate.</span></span> <span data-ttu-id="96fee-861">Это происходит из-за toohello способ распределения запросов аспекта по сегментам.</span><span class="sxs-lookup"><span data-stu-id="96fee-861">This is due toohello way faceting queries are distributed across shards.</span></span> <span data-ttu-id="96fee-862">Увеличение `count` обычно повышает hello точность подсчета терминов hello, но ценой падения производительности.</span><span class="sxs-lookup"><span data-stu-id="96fee-862">Increasing `count` generally increases hello accuracy of hello term counts, but at a performance cost.</span></span>
* <span data-ttu-id="96fee-863">`sort`(один из `count` toosort *по убыванию* по количеству, `-count` toosort *по возрастанию* по количеству, `value` toosort *по возрастанию* по значению, или `-value` toosort *по убыванию* по значению)</span><span class="sxs-lookup"><span data-stu-id="96fee-863">`sort` (one of `count` toosort *descending* by count, `-count` toosort *ascending* by count, `value` toosort *ascending* by value, or `-value` toosort *descending* by value)</span></span>
  * <span data-ttu-id="96fee-864">Например: `facet=category,count:3,sort:count` возвращает hello тремя верхними категориями в результатах аспекта в убывающем порядке по hello число документов с именем каждого города.</span><span class="sxs-lookup"><span data-stu-id="96fee-864">For example: `facet=category,count:3,sort:count` gets hello top three categories in facet results in descending order by hello number of documents with each city name.</span></span> <span data-ttu-id="96fee-865">Например если тремя верхними категориями hello, бюджет, Motel и Luxury и Budget имеет 5 совпадений, Motel имеет 6, а Luxury имеет 4, затем hello контейнеров будет в порядке hello Motel, Budget, Luxury.</span><span class="sxs-lookup"><span data-stu-id="96fee-865">For example, if hello top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then hello buckets will be in hello order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="96fee-866">Пример. `facet=rating,sort:-value` возвращает контейнеры со всеми возможными значениями оценки rating, отсортированные в убывающем порядке по значению.</span><span class="sxs-lookup"><span data-stu-id="96fee-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="96fee-867">Например если hello оценок от 1 too5, hello контейнеров будет упорядочен 5, 4, 3, 2, 1, вне зависимости от того, сколько документов соответствует каждой оценке.</span><span class="sxs-lookup"><span data-stu-id="96fee-867">For example, if hello ratings are from 1 too5, hello buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="96fee-868">`values` (разделенные символами вертикальной черты числовые значения или значения типа `Edm.DateTimeOffset`, задающие динамический набор значений записей аспектов)</span><span class="sxs-lookup"><span data-stu-id="96fee-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="96fee-869">Например: `facet=baseRate,values:10|20` создает три сегмента: один для базовой ставки от 0 вверх toobut, не включая 10, один для 10 вверх toobut, не включая 20 и одну для 20 или выше.</span><span class="sxs-lookup"><span data-stu-id="96fee-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up toobut not including 10, one for 10 up toobut not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="96fee-870">Пример. `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` возвращает два контейнера: один для гостиниц, отремонтированных до февраля 2010 г., и один — для гостиниц, отремонтированных 1 февраля 2010 г. или позже.</span><span class="sxs-lookup"><span data-stu-id="96fee-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="96fee-871">`interval` (целочисленный интервал больше 0 для числе либо `minute`, `hour`, `day`, `week`, `month`, `quarter` или `year` для значений даты и времени)</span><span class="sxs-lookup"><span data-stu-id="96fee-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="96fee-872">Пример. `facet=baseRate,interval:100` возвращает контейнеры для диапазонов базового тарифа с интервалом 100.</span><span class="sxs-lookup"><span data-stu-id="96fee-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="96fee-873">Например, для базовых тарифов от 60 до 600 долларов будут возвращены контейнеры 0–100, 100–200, 200–300, 300–400, 400–500 и 500–600.</span><span class="sxs-lookup"><span data-stu-id="96fee-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="96fee-874">Пример: `facet=lastRenovationDate,interval:year` возвращает по одному контейнеру для каждого года, в течение которого выполнялся ремонт гостиниц.</span><span class="sxs-lookup"><span data-stu-id="96fee-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="96fee-875">Параметр `timeoffset` ([+-]чч:мм, [+-]ччмм или [+-]чч) `timeoffset` является необязательным.</span><span class="sxs-lookup"><span data-stu-id="96fee-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="96fee-876">Его можно объединять только с hello `interval` параметр и только если примененные tooa поле типа `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="96fee-876">It can only be combined with hello `interval` option, and only when applied tooa field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="96fee-877">значение Hello указывает tooaccount смещения времени hello UTC для при задании времени границы.</span><span class="sxs-lookup"><span data-stu-id="96fee-877">hello value specifies hello UTC time offset tooaccount for in setting time boundaries.</span></span>
  * <span data-ttu-id="96fee-878">Например: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` использует hello день границу, которая начинается в формате UTC 01:00:00 (полуночи в hello целевой часовой пояс)</span><span class="sxs-lookup"><span data-stu-id="96fee-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses hello day boundary that starts at 01:00:00 UTC (midnight in hello target time zone)</span></span>
* <span data-ttu-id="96fee-879">**Примечание**: `count` и `sort` могут быть объединены в hello же спецификации аспекта, но они не могут сочетаться с `interval` или `values`, и `interval` и `values` не может сочетаться друг с другом.</span><span class="sxs-lookup"><span data-stu-id="96fee-879">**Note**: `count` and `sort` can be combined in hello same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="96fee-880">**Примечание**. Границы интервала для даты и времени вычисляются на основе времени в формате UTC, если не указан параметр `timeoffset`.</span><span class="sxs-lookup"><span data-stu-id="96fee-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="96fee-881">Например: для `facet=lastRenovationDate,interval:day`, границ hello день начинается в 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="96fee-881">For example: for `facet=lastRenovationDate,interval:day`, hello day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="96fee-882">При вызове **поиска** с помощью запроса POST этот параметр называется `facets`, а не `facet`.</span><span class="sxs-lookup"><span data-stu-id="96fee-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="96fee-883">Кроме того, она задается в виде JSON-массива строк, где каждая строка представляет собой отдельное выражение аспектирования.</span><span class="sxs-lookup"><span data-stu-id="96fee-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="96fee-884">`$filter=[string]` (необязательный): выражение структурированного поиска в стандартном синтаксисе OData.</span><span class="sxs-lookup"><span data-stu-id="96fee-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-885">При вызове **поиска** с помощью запроса POST этот параметр называется `filter`, а не `$filter`.</span><span class="sxs-lookup"><span data-stu-id="96fee-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="96fee-886">`highlight=[string]` (необязательный): набор имен полей через запятую, используемых для выделения совпадений.</span><span class="sxs-lookup"><span data-stu-id="96fee-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="96fee-887">Для выделения можно использовать только поля с атрибутом `searchable` .</span><span class="sxs-lookup"><span data-stu-id="96fee-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="96fee-888">`highlightPreTag=[string]`(необязательно, по умолчанию слишком`<em>`) — тег toohit выделяет строку.</span><span class="sxs-lookup"><span data-stu-id="96fee-888">`highlightPreTag=[string]` (optional, defaults too`<em>`) - A string tag that prepends toohit highlights.</span></span> <span data-ttu-id="96fee-889">Для него должно быть задано значение `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="96fee-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-890">При вызове **поиска** GET, зарезервированные символы в URL-АДРЕСЕ hello должна использоваться закодированные (например, % 23 вместо #).</span><span class="sxs-lookup"><span data-stu-id="96fee-890">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="96fee-891">`highlightPostTag=[string]`(необязательно, по умолчанию слишком`</em>`)-строковый тег, который добавляет toohit выделение.</span><span class="sxs-lookup"><span data-stu-id="96fee-891">`highlightPostTag=[string]` (optional, defaults too`</em>`) - a string tag that appends toohit highlights.</span></span> <span data-ttu-id="96fee-892">Для него должно быть задано значение `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="96fee-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-893">При вызове **поиска** GET, зарезервированные символы в URL-АДРЕСЕ hello должна использоваться закодированные (например, % 23 вместо #).</span><span class="sxs-lookup"><span data-stu-id="96fee-893">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="96fee-894">`scoringProfile=[string]`(необязательно) — имя hello оценки tooevaluate профиль соответствует оценок для соответствующих документов в результатах hello toosort заказа.</span><span class="sxs-lookup"><span data-stu-id="96fee-894">`scoringProfile=[string]` (optional) - hello name of a scoring profile tooevaluate match scores for matching documents in order toosort hello results.</span></span>

<span data-ttu-id="96fee-895">`scoringParameter=[string]`(ноль или более) — указывает hello значения для каждого параметра, определенного в функции оценки (например, `referencePointParameter`) с использованием формата hello `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="96fee-895">`scoringParameter=[string]` (zero or more) - Indicates hello values for each parameter defined in a scoring function (for example, `referencePointParameter`) using hello format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="96fee-896">Например, если профиль оценки hello определена функция с параметр с именем параметра строки запроса «mylocation» hello будет `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="96fee-896">For example, if hello scoring profile defines a function with a parameter called "mylocation" hello query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="96fee-897">Первый тире Hello отделяет hello имя из списка значений hello, во время второго дефиса hello является частью hello первое значение (в данном примере — долгота).</span><span class="sxs-lookup"><span data-stu-id="96fee-897">hello first dash separates hello name from hello value list, while hello second dash is part of hello first value (longitude in this example).</span></span>
* <span data-ttu-id="96fee-898">Для оценки параметров такие, как для тега повышение приоритета, который может содержать запятые, знаки можно экранировать таких значений в списке hello, используя одинарные кавычки.</span><span class="sxs-lookup"><span data-stu-id="96fee-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in hello list using single quotes.</span></span> <span data-ttu-id="96fee-899">Если значения hello, сами содержат одинарные кавычки, их можно экранировать путем удвоения.</span><span class="sxs-lookup"><span data-stu-id="96fee-899">If hello values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="96fee-900">Например, если тег повышение параметр с именем «mytag» и требуется tooboost теге hello значения «Hello, о ' Брайен» и «Smith», hello запроса строки из вариантов `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="96fee-900">For example, if you have a tag boosting parameter called "mytag" and you want tooboost on hello tag values "Hello, O'Brien" and "Smith", hello query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="96fee-901">Обратите внимание, что кавычки нужны только для значений, содержащих запятые.</span><span class="sxs-lookup"><span data-stu-id="96fee-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-902">При вызове **поиска** с помощью запроса POST этот параметр называется `scoringParameters`, а не `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="96fee-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="96fee-903">Кроме того, она задается в виде массива JSON строк, где каждая строка представляет собой отдельную пару `name-values` .</span><span class="sxs-lookup"><span data-stu-id="96fee-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="96fee-904">`minimumCoverage`(необязательно, по умолчанию too100) - число от 0 до 100, указывающее процент hello hello индекса, который необходимо рассмотреть в поисковом запросе в порядке для запроса toobe hello сообщить об успешном выполнении.</span><span class="sxs-lookup"><span data-stu-id="96fee-904">`minimumCoverage` (optional, defaults too100) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a search query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="96fee-905">По умолчанию должны быть доступны всем индексом hello или `Search` возвращает код состояния HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="96fee-905">By default, hello entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="96fee-906">Если задать `minimumCoverage` и `Search` завершается успешно, он вернет HTTP 200 и включить `@search.coverage` значение, указывающее процент hello hello индекса, который был включен в запрос hello ответа hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-907">Значение параметра tooa ниже, чем 100 может быть полезным для обеспечения доступности поиска даже для служб с только одной реплики.</span><span class="sxs-lookup"><span data-stu-id="96fee-907">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="96fee-908">Однако не все соответствующие документы гарантируется toobe присутствуют в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-908">However, not all matching documents are guaranteed toobe present in hello search results.</span></span> <span data-ttu-id="96fee-909">Если отзыв поиска является более важным tooyour приложения, чем доступности, то он является наиболее tooleave `minimumCoverage` значение по умолчанию 100.</span><span class="sxs-lookup"><span data-stu-id="96fee-909">If search recall is more important tooyour application than availability, then it's best tooleave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="96fee-910">`api-version=[string]` (обязательный).</span><span class="sxs-lookup"><span data-stu-id="96fee-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="96fee-911">Hello предварительной версии — `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-911">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-912">Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="96fee-913">Примечание: Для этой операции hello `api-version` указан как параметр запроса в URL-АДРЕСЕ hello независимо от того, вызов **поиска** с GET или POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-913">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="96fee-914">**Заголовки запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-914">**Request Headers**</span></span>

<span data-ttu-id="96fee-915">Hello следующий список описывает hello необходимые и необязательные заголовки запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-915">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="96fee-916">`api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-916">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="96fee-917">Это строковое значение, URL-адрес службы уникальный tooyour.</span><span class="sxs-lookup"><span data-stu-id="96fee-917">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="96fee-918">Hello **поиска** запроса можно указать ключ администратора либо ключ запроса для `api-key`.</span><span class="sxs-lookup"><span data-stu-id="96fee-918">hello **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="96fee-919">Необходимо также hello имя tooconstruct hello запроса URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-919">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="96fee-920">Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-920">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="96fee-921">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.</span><span class="sxs-lookup"><span data-stu-id="96fee-921">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="96fee-922">**Тело запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-922">**Request Body**</span></span>

<span data-ttu-id="96fee-923">Для запроса GET: нет.</span><span class="sxs-lookup"><span data-stu-id="96fee-923">For GET: None.</span></span>

<span data-ttu-id="96fee-924">Для запроса POST:</span><span class="sxs-lookup"><span data-stu-id="96fee-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

<span data-ttu-id="96fee-925">**Продолжение частичных ответов поиска**</span><span class="sxs-lookup"><span data-stu-id="96fee-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="96fee-926">Иногда поиска Azure не может возвращать все hello запрошенные результаты в одном ответе поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-926">Sometimes Azure Search can't return all hello requested results in a single Search response.</span></span> <span data-ttu-id="96fee-927">Это может происходить по разным причинам, например запросы слишком много документов, не указывая hello запроса `$top` или указания значения для `$top` слишком большого объема.</span><span class="sxs-lookup"><span data-stu-id="96fee-927">This can happen for different reasons, such as when hello query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="96fee-928">В таких случаях службы поиска Azure входят hello `@odata.nextLink` заметки в текст ответа hello и также `@search.nextPageParameters` если бы это был запрос POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-928">In such cases, Azure Search will include hello `@odata.nextLink` annotation in hello response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="96fee-929">Значения hello tooformulate эти заметки можно использовать другой поиска запроса tooget hello следующая часть ответа на запросы поиска hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-929">You can use hello values of these annotations tooformulate another Search request tooget hello next part of hello search response.</span></span> <span data-ttu-id="96fee-930">Это называется ***продолжения*** hello исходный запрос для поиска и hello заметки обычно вызываются ***токены продолжения***.</span><span class="sxs-lookup"><span data-stu-id="96fee-930">This is called a ***continuation*** of hello original Search request, and hello annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="96fee-931">В разделе [приведенном ниже примере hello](#SearchResponse) сведения о синтаксисе hello этих заметок и где они отображаются в текст ответа hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-931">See [hello example below](#SearchResponse) for details on hello syntax of these annotations and where they appear in hello response body.</span></span> 

<span data-ttu-id="96fee-932">Hello причины, почему поиска Azure может возвращать маркеры продолжения: toochange зависит от реализации и подчиняется.</span><span class="sxs-lookup"><span data-stu-id="96fee-932">hello reasons why Azure Search might return continuation tokens are implementation-specific and subject toochange.</span></span> <span data-ttu-id="96fee-933">Надежные клиенты всегда должен быть готов toohandle случаях возвращаются меньше документов, чем ожидалось, а токен продолжения — включить toocontinue извлечения документов.</span><span class="sxs-lookup"><span data-stu-id="96fee-933">Robust clients should always be ready toohandle cases where fewer documents than expected are returned and a continuation token is included toocontinue retrieving documents.</span></span> <span data-ttu-id="96fee-934">Также Обратите внимание, что необходимо использовать hello же метод HTTP, как исходный запрос hello в toocontinue порядке.</span><span class="sxs-lookup"><span data-stu-id="96fee-934">Also note that you must use hello same HTTP method as hello original request in order toocontinue.</span></span> <span data-ttu-id="96fee-935">Например, если был отправлен запрос GET, все отправляемые запросы на продолжение должны также использовать GET (это справедливо и для POST).</span><span class="sxs-lookup"><span data-stu-id="96fee-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="96fee-936"><a name="SearchResponse"></a>
**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="96fee-937">Код состояния: в качестве успешного ответа возвращается код "200 — ОК".</span><span class="sxs-lookup"><span data-stu-id="96fee-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

<span data-ttu-id="96fee-938">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="96fee-938">**Examples:**</span></span>

<span data-ttu-id="96fee-939">Дополнительные примеры можно найти на hello [синтаксис выражений OData для поиска Azure](https://msdn.microsoft.com/library/azure/dn798921.aspx) страницы.</span><span class="sxs-lookup"><span data-stu-id="96fee-939">You can find additional examples on hello [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="96fee-940">Hello поиска индекса с сортировкой по убыванию по дате.</span><span class="sxs-lookup"><span data-stu-id="96fee-940">Search hello Index sorted descending by date.</span></span>

    <span data-ttu-id="96fee-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span><span class="sxs-lookup"><span data-stu-id="96fee-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="96fee-943">В поиске аспекта поиск в указателе hello и извлекаются аспекты для категорий, оценок, тегов, а также элементы со значениями baseRate в указанных диапазонах:</span><span class="sxs-lookup"><span data-stu-id="96fee-943">In a faceted search, search hello index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="96fee-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span><span class="sxs-lookup"><span data-stu-id="96fee-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="96fee-946">С помощью фильтра, сузить hello предыдущие результаты запроса аспекта после hello пользователь щелкает оценка 3 и категорию «Motel»:</span><span class="sxs-lookup"><span data-stu-id="96fee-946">Using a filter, narrow down hello previous faceted query results after hello user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="96fee-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span><span class="sxs-lookup"><span data-stu-id="96fee-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="96fee-949">Установка для результатов аспектного поиска верхнего предела на количество уникальных условий поиска, возвращаемых запросом.</span><span class="sxs-lookup"><span data-stu-id="96fee-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="96fee-950">по умолчанию Hello равно 10, но можно увеличить или уменьшить это значение с помощью hello `count` параметром hello `facet` атрибута:</span><span class="sxs-lookup"><span data-stu-id="96fee-950">hello default is 10, but you can increase or decrease this value using hello `count` parameter on hello `facet` attribute:</span></span>

    <span data-ttu-id="96fee-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span><span class="sxs-lookup"><span data-stu-id="96fee-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="96fee-953">Hello поиска индекса в пределах определенных полей; Например поле конкретного языка:</span><span class="sxs-lookup"><span data-stu-id="96fee-953">Search hello Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="96fee-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span><span class="sxs-lookup"><span data-stu-id="96fee-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="96fee-956">Поиск hello индекс по нескольким полям.</span><span class="sxs-lookup"><span data-stu-id="96fee-956">Search hello Index across multiple fields.</span></span> <span data-ttu-id="96fee-957">Например можно хранить и запроса для поиска полей на нескольких языках в hello же индекс.</span><span class="sxs-lookup"><span data-stu-id="96fee-957">For example, you can store and query searchable fields in multiple languages, all within hello same index.</span></span>  <span data-ttu-id="96fee-958">Если описания на английском и французском сосуществовать в hello же документа, можно возвращать все hello в результаты запроса:</span><span class="sxs-lookup"><span data-stu-id="96fee-958">If English and French descriptions co-exist in hello same document, you can return any or all in hello query results:</span></span>

    <span data-ttu-id="96fee-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span><span class="sxs-lookup"><span data-stu-id="96fee-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="96fee-961">Обратите внимание на то, что запрос можно отправить только к одному индексу.</span><span class="sxs-lookup"><span data-stu-id="96fee-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="96fee-962">Не следует создавать несколько индексов для каждого языка, если не планируете tooquery одну за другой.</span><span class="sxs-lookup"><span data-stu-id="96fee-962">Do not create multiple indexes for each language unless you plan tooquery one at a time.</span></span>

7)    <span data-ttu-id="96fee-963">Разбиение на страницы: Get hello первую страницу элементов (размер страницы — 10):</span><span class="sxs-lookup"><span data-stu-id="96fee-963">Paging - Get hello 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="96fee-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="96fee-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="96fee-966">Разбиение на страницы: Get hello вторую страницу элементов (размер страницы — 10):</span><span class="sxs-lookup"><span data-stu-id="96fee-966">Paging - Get hello 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="96fee-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="96fee-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="96fee-969">Получение определенного набора полей.</span><span class="sxs-lookup"><span data-stu-id="96fee-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="96fee-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span><span class="sxs-lookup"><span data-stu-id="96fee-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="96fee-972">Получение документов, соответствующих определенному выражению фильтра.</span><span class="sxs-lookup"><span data-stu-id="96fee-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="96fee-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span><span class="sxs-lookup"><span data-stu-id="96fee-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="96fee-975">Индекс поиска hello и возврат фрагментов с выделением попаданий</span><span class="sxs-lookup"><span data-stu-id="96fee-975">Search hello index and return fragments with hit highlights</span></span>

    <span data-ttu-id="96fee-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span><span class="sxs-lookup"><span data-stu-id="96fee-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="96fee-978">Поиск в указателе hello и возвращать документы, отсортированные от ближе toofarther от базового каталога</span><span class="sxs-lookup"><span data-stu-id="96fee-978">Search hello index and return documents sorted from closer toofarther away from a reference location</span></span>

    <span data-ttu-id="96fee-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span><span class="sxs-lookup"><span data-stu-id="96fee-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="96fee-981">Поиск hello индекса при условии, что существует профиля оценки «geo» вместе с двумя функциями оценки расстояния, один из которых определяет параметр с именем «currentLocation», другая определяет параметр с именем «lastLocation»</span><span class="sxs-lookup"><span data-stu-id="96fee-981">Search hello index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="96fee-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span><span class="sxs-lookup"><span data-stu-id="96fee-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="96fee-984">Поиск документов с помощью индекса hello [синтаксис простого запроса](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-984">Find documents in hello index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="96fee-985">Этот запрос возвращает гостиницы, где для поиска поля содержат hello термины «comfort» и «location», но не «motel»:</span><span class="sxs-lookup"><span data-stu-id="96fee-985">This query returns hotels where searchable fields contain hello terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="96fee-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="96fee-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="96fee-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="96fee-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="96fee-988">Обратите внимание на использование hello `searchMode=all` выше.</span><span class="sxs-lookup"><span data-stu-id="96fee-988">Note hello use of `searchMode=all` above.</span></span> <span data-ttu-id="96fee-989">Включая этот параметр переопределяет значение по умолчанию hello `searchMode=any`, что гарантирует, `-motel` означает «И не» вместо «Или не».</span><span class="sxs-lookup"><span data-stu-id="96fee-989">Including this parameter overrides hello default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="96fee-990">Без `searchMode=all`, вы получаете «Или не», который расширяется, а не ограничивает результаты поиска, и это может быть counter-intuitive toosome пользователей.</span><span class="sxs-lookup"><span data-stu-id="96fee-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive toosome users.</span></span>

15) <span data-ttu-id="96fee-991">Поиск документов с помощью индекса hello [синтаксис запроса lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-991">Find documents in hello index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="96fee-992">Этот запрос возвращает гостиницы, где hello поле категории содержит hello термин «бюджет» и все просматриваемые полей, содержащих hello фразу «недавно отремонтированных».</span><span class="sxs-lookup"><span data-stu-id="96fee-992">This query returns hotels where hello category field contains hello term "budget" and all searchable fields containing hello phrase "recently renovated".</span></span> <span data-ttu-id="96fee-993">Документы, содержащие фразу hello «недавно отремонтированных» более высоким рангом в результате значение boost термин hello (3)</span><span class="sxs-lookup"><span data-stu-id="96fee-993">Documents containing hello phrase "recently renovated" are ranked higher as a result of hello term boost value (3)</span></span>

    <span data-ttu-id="96fee-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span><span class="sxs-lookup"><span data-stu-id="96fee-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="96fee-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="96fee-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="96fee-996">Запрос документов</span><span class="sxs-lookup"><span data-stu-id="96fee-996">Lookup Document</span></span>
<span data-ttu-id="96fee-997">Hello **поиск документов** операция получает документ из поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="96fee-997">hello **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="96fee-998">Это полезно в том случае, когда пользователь щелкает определенный результат поиска, и требуется toolook конкретные сведения о документе.</span><span class="sxs-lookup"><span data-stu-id="96fee-998">This is useful when a user clicks on a specific search result, and you want toolook up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="96fee-999">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-999">**Request**</span></span>

<span data-ttu-id="96fee-1000">Запросы к службе отправляются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96fee-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="96fee-1001">Hello **поиск документов** запрос можно составить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="96fee-1001">hello **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="96fee-1002">Кроме того можно использовать традиционный синтаксис OData hello для поиска ключа:</span><span class="sxs-lookup"><span data-stu-id="96fee-1002">Alternatively, you can use hello traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="96fee-1003">Hello URI запроса содержит [имя индекса] и [key], указав какие tooretrieve документ, соответствующий индекс.</span><span class="sxs-lookup"><span data-stu-id="96fee-1003">hello request URI includes an [index name] and [key], specifying which document tooretrieve from which index.</span></span> <span data-ttu-id="96fee-1004">За один раз можно получить только один документ.</span><span class="sxs-lookup"><span data-stu-id="96fee-1004">You can only get one document at a time.</span></span> <span data-ttu-id="96fee-1005">Используйте **поиска** tooget несколько документов в одном запросе.</span><span class="sxs-lookup"><span data-stu-id="96fee-1005">Use **Search** tooget multiple documents in a single request.</span></span>

<span data-ttu-id="96fee-1006">**Параметры запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-1006">**Query Parameters**</span></span>

<span data-ttu-id="96fee-1007">`$select=[string]`(необязательно) — список tooretrieve полей с разделителями запятыми.</span><span class="sxs-lookup"><span data-stu-id="96fee-1007">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="96fee-1008">Если не задано или имеет слишком`*`, все поля, помеченные в схеме hello извлекаемые, включены в проекцию hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-1008">If unspecified or set too`*`, all fields marked as retrievable in hello schema are included in hello projection.</span></span>

<span data-ttu-id="96fee-1009">`api-version=[string]` (обязательный).</span><span class="sxs-lookup"><span data-stu-id="96fee-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="96fee-1010">Hello предварительной версии — `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1010">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-1011">Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="96fee-1012">Примечание: Для этой операции hello `api-version` указан как параметр запроса.</span><span class="sxs-lookup"><span data-stu-id="96fee-1012">Note: For this operation, hello `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="96fee-1013">**Заголовки запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-1013">**Request Headers**</span></span>

<span data-ttu-id="96fee-1014">Hello следующий список описывает hello необходимые и необязательные заголовки запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-1014">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="96fee-1015">`api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-1015">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="96fee-1016">Это строковое значение, URL-адрес службы уникальный tooyour.</span><span class="sxs-lookup"><span data-stu-id="96fee-1016">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="96fee-1017">Hello **поиск документов** запроса можно указать ключ администратора либо ключ запроса для `api-key`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1017">hello **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="96fee-1018">Необходимо также hello имя tooconstruct hello запроса URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-1018">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="96fee-1019">Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-1019">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="96fee-1020">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.</span><span class="sxs-lookup"><span data-stu-id="96fee-1020">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="96fee-1021">**Тело запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-1021">**Request Body**</span></span>

<span data-ttu-id="96fee-1022">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="96fee-1022">None.</span></span>

<span data-ttu-id="96fee-1023">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-1023">**Response**</span></span>

<span data-ttu-id="96fee-1024">Код состояния: в качестве успешного ответа возвращается код "200 — ОК".</span><span class="sxs-lookup"><span data-stu-id="96fee-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

<span data-ttu-id="96fee-1025">**Пример**</span><span class="sxs-lookup"><span data-stu-id="96fee-1025">**Example**</span></span>

<span data-ttu-id="96fee-1026">Поиск документов hello с ключом "2"</span><span class="sxs-lookup"><span data-stu-id="96fee-1026">Lookup hello document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="96fee-1027">Поиск документов hello с ключом "3" с использованием синтаксиса OData:</span><span class="sxs-lookup"><span data-stu-id="96fee-1027">Lookup hello document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="96fee-1028">Подсчет документов</span><span class="sxs-lookup"><span data-stu-id="96fee-1028">Count Documents</span></span>
<span data-ttu-id="96fee-1029">Hello **подсчет документов** операция получает число hello число документов в индекс поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-1029">hello **Count Documents** operation retrieves a count of hello number of documents in a search index.</span></span> <span data-ttu-id="96fee-1030">Hello `$count` синтаксис является частью hello протокол OData.</span><span class="sxs-lookup"><span data-stu-id="96fee-1030">hello `$count` syntax is part of hello OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="96fee-1031">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-1031">**Request**</span></span>

<span data-ttu-id="96fee-1032">Запросы к службе отправляются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96fee-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="96fee-1033">Hello **подсчет документов** запрос может быть создан с помощью метода GET hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-1033">hello **Count Documents** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="96fee-1034">Hello [имя индекса] в URI запроса hello сообщает hello службы tooreturn количество всех элементов в коллекции документов указанного индекса hello hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-1034">hello [index name] in hello request URI tells hello service tooreturn a count of all items in hello docs collection of hello specified index.</span></span>

<span data-ttu-id="96fee-1035">`api-version=[string]` (обязательный).</span><span class="sxs-lookup"><span data-stu-id="96fee-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="96fee-1036">Hello предварительной версии — `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1036">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-1037">Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="96fee-1038">**Заголовки запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-1038">**Request Headers**</span></span>

<span data-ttu-id="96fee-1039">Hello следующий список описывает hello необходимые и необязательные заголовки запросов.</span><span class="sxs-lookup"><span data-stu-id="96fee-1039">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="96fee-1040">`Accept`: Это значение должно быть задано слишком`text/plain`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1040">`Accept`: This value must be set too`text/plain`.</span></span>
* <span data-ttu-id="96fee-1041">`api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-1041">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="96fee-1042">Это строковое значение, URL-адрес службы уникальный tooyour.</span><span class="sxs-lookup"><span data-stu-id="96fee-1042">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="96fee-1043">Hello **подсчет документов** запроса можно указать ключ администратора либо ключ запроса для `api-key`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1043">hello **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="96fee-1044">Необходимо также hello имя tooconstruct hello запроса URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-1044">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="96fee-1045">Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-1045">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="96fee-1046">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.</span><span class="sxs-lookup"><span data-stu-id="96fee-1046">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="96fee-1047">**Тело запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-1047">**Request Body**</span></span>

<span data-ttu-id="96fee-1048">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="96fee-1048">None.</span></span>

<span data-ttu-id="96fee-1049">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-1049">**Response**</span></span>

<span data-ttu-id="96fee-1050">Код состояния: в качестве успешного ответа возвращается код "200 — ОК".</span><span class="sxs-lookup"><span data-stu-id="96fee-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="96fee-1051">текст ответа Hello содержит значение числа hello как целое число в формате обычного текста.</span><span class="sxs-lookup"><span data-stu-id="96fee-1051">hello response body contains hello count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="96fee-1052">Предложения</span><span class="sxs-lookup"><span data-stu-id="96fee-1052">Suggestions</span></span>
<span data-ttu-id="96fee-1053">Hello **предложения** операция получает предложения на основании частичного ввода условия поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-1053">hello **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="96fee-1054">Он обычно используется в поиск поля tooprovide упреждающих предложений при вводе условия поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-1054">It's typically used in search boxes tooprovide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="96fee-1055">Предложения запросов направлены на предложение целевых документов, поэтому предложенные hello, что текст может повторяться, если несколько документов-кандидатов соответствует hello же поиска входных данных.</span><span class="sxs-lookup"><span data-stu-id="96fee-1055">Suggestion requests aim at suggesting target documents, so hello suggested text may be repeated if multiple candidate documents match hello same search input.</span></span> <span data-ttu-id="96fee-1056">Можно использовать `$select` tooretrieve других документов поля (включая hello ключ документа), чтобы можно было определить, какой документ является источником каждого предложения hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-1056">You can use `$select` tooretrieve other document fields (including hello document key) so that you can tell which document is hello source for each suggestion.</span></span>

<span data-ttu-id="96fee-1057">Операция **вызова предложений** выполняется как запрос GET или POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="96fee-1058">**При УЧЕТЕ toouse вместо GET**</span><span class="sxs-lookup"><span data-stu-id="96fee-1058">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="96fee-1059">При использовании HTTP GET hello toocall **предложения** API-интерфейса, необходимо помнить, что длина URL-адрес запроса hello hello не может превышать 8 КБ toobe.</span><span class="sxs-lookup"><span data-stu-id="96fee-1059">When you use HTTP GET toocall hello **Suggestions** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="96fee-1060">Для большинства приложений этого достаточно.</span><span class="sxs-lookup"><span data-stu-id="96fee-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="96fee-1061">В то же время некоторые приложения создают очень длинные запросы, в частности выражения фильтров OData.</span><span class="sxs-lookup"><span data-stu-id="96fee-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="96fee-1062">Лучший вариант для этих приложений — использование запроса HTTP POST, так как он позволяет увеличить фильтры по сравнению с GET.</span><span class="sxs-lookup"><span data-stu-id="96fee-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="96fee-1063">С помощью запроса POST hello количество предложений в фильтре hello ограничивающим фактором, не hello размер строки фильтра необработанные hello, поскольку hello предельного размера запроса для POST — приблизительно 16 МБ.</span><span class="sxs-lookup"><span data-stu-id="96fee-1063">With POST, hello number of clauses in a filter is hello limiting factor, not hello size of hello raw filter string since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-1064">Несмотря на то, что ограничение на размер запроса POST hello очень велика, критерии фильтра не может быть произвольным и довольно сложным.</span><span class="sxs-lookup"><span data-stu-id="96fee-1064">Even though hello POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="96fee-1065">Дополнительные сведения об ограничениях сложности фильтров см. в статье, посвященной [синтаксису выражений OData](https://msdn.microsoft.com/library/dn798921.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="96fee-1066">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="96fee-1066">**Request**</span></span>

<span data-ttu-id="96fee-1067">Запросы к службе отправляются по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="96fee-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="96fee-1068">Hello **предложения** можно составить запрос методы с помощью hello GET или POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-1068">hello **Suggestions** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="96fee-1069">URI запроса Hello указывает имя hello hello tooquery индекса.</span><span class="sxs-lookup"><span data-stu-id="96fee-1069">hello request URI specifies hello name of hello index tooquery.</span></span> <span data-ttu-id="96fee-1070">Параметры, такие как hello частично введенное условие поиска, указанные в строке запроса hello в случае hello запросов GET, а в запросе hello запрашивает текст в случае, когда hello POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-1070">Parameters, such as hello partially input search term, are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="96fee-1071">Рекомендуется при создании запросов GET, следует помнить слишком[кодирование URL-адрес](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) конкретного запроса, параметров при вызове hello REST API напрямую.</span><span class="sxs-lookup"><span data-stu-id="96fee-1071">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="96fee-1072">Для операций **вызова предложений** эти параметры указаны ниже.</span><span class="sxs-lookup"><span data-stu-id="96fee-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="96fee-1073">Кодировка URL рекомендуется только для hello выше параметров запроса.</span><span class="sxs-lookup"><span data-stu-id="96fee-1073">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="96fee-1074">Если вы случайно URL-кодировали hello вся строка запроса (все после hello?), запросы будут нарушены.</span><span class="sxs-lookup"><span data-stu-id="96fee-1074">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="96fee-1075">Кроме того URL-кодирование необходима только при вызове hello получить напрямую с помощью API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="96fee-1075">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="96fee-1076">Кодировка URL-адрес не является обязательным при вызове **предложения** с помощью запроса POST, или при использовании hello [клиентская библиотека .NET](https://msdn.microsoft.com/library/dn951165.aspx), обрабатывающая для кодирования URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="96fee-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="96fee-1077">**Параметры запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-1077">**Query Parameters**</span></span>

<span data-ttu-id="96fee-1078">**Предложения** принимает несколько параметров, которые сообщают условия запроса и определяют способы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="96fee-1079">Укажите эти параметры в URL-АДРЕСЕ hello строку запроса, при вызове **предложения** через GET, а также как свойства JSON в теле запроса hello при вызове **предложения** помощью POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-1079">You provide these parameters in hello URL query string when calling **Suggestions** via GET, and as JSON properties in hello request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="96fee-1080">синтаксис Hello для некоторых параметров немного отличается от GET и POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-1080">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="96fee-1081">Эти различия описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="96fee-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="96fee-1082">`search=[string]`-hello запросы toosuggest toouse полнотекстового поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-1082">`search=[string]` - hello search text toouse toosuggest queries.</span></span> <span data-ttu-id="96fee-1083">Минимальная длина — 1 символ, максимальная — 100 символов.</span><span class="sxs-lookup"><span data-stu-id="96fee-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="96fee-1084">`highlightPreTag=[string]`(необязательно) — тег строки toosearch попаданий.</span><span class="sxs-lookup"><span data-stu-id="96fee-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends toosearch hits.</span></span> <span data-ttu-id="96fee-1085">Для него должно быть задано значение `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-1086">При вызове **предложения** GET, зарезервированные символы в URL-АДРЕСЕ hello должна использоваться закодированные (например, % 23 вместо #).</span><span class="sxs-lookup"><span data-stu-id="96fee-1086">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="96fee-1087">`highlightPostTag=[string]`(необязательно) — строковый тег, который добавляет toosearch попаданий.</span><span class="sxs-lookup"><span data-stu-id="96fee-1087">`highlightPostTag=[string]` (optional) - a string tag that appends toosearch hits.</span></span> <span data-ttu-id="96fee-1088">Для него должно быть задано значение `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-1089">При вызове **предложения** GET, зарезервированные символы в URL-АДРЕСЕ hello должна использоваться закодированные (например, % 23 вместо #).</span><span class="sxs-lookup"><span data-stu-id="96fee-1089">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="96fee-1090">`suggesterName=[string]`— Имя средства подбора hello, как указано в hello hello `suggesters` коллекцию, которая входит в определение индекса hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-1090">`suggesterName=[string]` - hello name of hello suggester as specified in hello `suggesters` collection that's part of hello index definition.</span></span> <span data-ttu-id="96fee-1091">`suggester` определяет, в каких полях выполняется поиск предложений по условиям запроса.</span><span class="sxs-lookup"><span data-stu-id="96fee-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="96fee-1092">Дополнительные сведения см. в разделе [Средства подбора](#Suggesters).</span><span class="sxs-lookup"><span data-stu-id="96fee-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="96fee-1093">`fuzzy=[boolean]`(необязательно, по умолчанию = ложь)-Если для параметра задано tootrue API будет находить предложения даже при наличии замененного или отсутствующего символа в тексте hello поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-1093">`fuzzy=[boolean]` (optional, default = false) - when set tootrue this API will find suggestions even if there's a substituted or missing character in hello search text.</span></span> <span data-ttu-id="96fee-1094">В определенных ситуациях это улучшает результат, однако ведет к снижению производительности, так как запросы по нечеткому соответствию обрабатываются медленнее и потребляют больше ресурсов.</span><span class="sxs-lookup"><span data-stu-id="96fee-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="96fee-1095">`searchFields=[string]`(необязательно) — список hello toosearch имена полей с разделителями запятыми для hello указанный искомый текст.</span><span class="sxs-lookup"><span data-stu-id="96fee-1095">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified search text.</span></span> <span data-ttu-id="96fee-1096">Для целевых полей должен быть разрешен поиск предложений.</span><span class="sxs-lookup"><span data-stu-id="96fee-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="96fee-1097">`$top=#`(необязательно, по умолчанию = 5)-число tooretrieve предложения hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-1097">`$top=#` (optional, default = 5) - hello number of suggestions tooretrieve.</span></span> <span data-ttu-id="96fee-1098">Это значение должно быть в диапазоне от 1 до 100.</span><span class="sxs-lookup"><span data-stu-id="96fee-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-1099">При вызове **предложений** с помощью запроса POST этот параметр называется `top`, а не `$top`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="96fee-1100">`$filter=[string]`(необязательно) — выражение, фильтрующее документы hello, рассматриваемые для предложений.</span><span class="sxs-lookup"><span data-stu-id="96fee-1100">`$filter=[string]` (optional) - an expression that filters hello documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-1101">При вызове **предложений** с помощью запроса POST этот параметр называется `filter`, а не `$filter`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="96fee-1102">`$orderby=[string]`(необязательно) — список выражений, разделенных запятыми toosort hello результаты по.</span><span class="sxs-lookup"><span data-stu-id="96fee-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="96fee-1103">Каждое выражение может быть именем поля или toohello вызов `geo.distance()` функции.</span><span class="sxs-lookup"><span data-stu-id="96fee-1103">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="96fee-1104">Каждое выражение может следовать `asc` tooindicated по возрастанию, и `desc` tooindicate по убыванию.</span><span class="sxs-lookup"><span data-stu-id="96fee-1104">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="96fee-1105">по умолчанию Hello по возрастанию.</span><span class="sxs-lookup"><span data-stu-id="96fee-1105">hello default is ascending order.</span></span> <span data-ttu-id="96fee-1106">Максимальное количество предложений `$orderby`— 32.</span><span class="sxs-lookup"><span data-stu-id="96fee-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-1107">При вызове **предложений** с помощью запроса POST этот параметр называется `orderby`, а не `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="96fee-1108">`$select=[string]`(необязательно) — список tooretrieve полей с разделителями запятыми.</span><span class="sxs-lookup"><span data-stu-id="96fee-1108">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="96fee-1109">Если не указано, только hello ключ документа и возвращается текст подсказки.</span><span class="sxs-lookup"><span data-stu-id="96fee-1109">If unspecified, only hello document key and suggestion text is returned.</span></span> <span data-ttu-id="96fee-1110">Можно явно запросить все поля, установив этот параметр слишком`*`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1110">You can explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-1111">При вызове **предложений** с помощью запроса POST этот параметр называется `select`, а не `$select`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="96fee-1112">`minimumCoverage`(необязательно, по умолчанию too80) - число от 0 до 100, указывающее процент hello hello индекса, который должен быть охвачен предложения запроса в порядке для запроса toobe hello сообщить об успешном выполнении.</span><span class="sxs-lookup"><span data-stu-id="96fee-1112">`minimumCoverage` (optional, defaults too80) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a suggestions query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="96fee-1113">По умолчанию, должен быть доступен по крайней мере 80% hello индекса или `Suggest` возвращает код состояния HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="96fee-1113">By default, at least 80% of hello index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="96fee-1114">Если задать `minimumCoverage` и `Suggest` завершается успешно, он вернет HTTP 200 и включить `@search.coverage` значение, указывающее процент hello hello индекса, который был включен в запрос hello ответа hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="96fee-1115">Значение параметра tooa ниже, чем 100 может быть полезным для обеспечения доступности поиска даже для служб с только одной реплики.</span><span class="sxs-lookup"><span data-stu-id="96fee-1115">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="96fee-1116">Однако не все соответствующие предложения гарантируется toobe присутствуют в результатах hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-1116">However, not all matching suggestions are guaranteed toobe present in hello results.</span></span> <span data-ttu-id="96fee-1117">Если отзыв является более важным tooyour приложения, чем доступности, то он является наилучшим образом не toolower `minimumCoverage` ниже его значение по умолчанию, равное 80.</span><span class="sxs-lookup"><span data-stu-id="96fee-1117">If recall is more important tooyour application than availability, then it's best not toolower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="96fee-1118">`api-version=[string]` (обязательный).</span><span class="sxs-lookup"><span data-stu-id="96fee-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="96fee-1119">Hello предварительной версии — `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1119">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="96fee-1120">Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).</span><span class="sxs-lookup"><span data-stu-id="96fee-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="96fee-1121">Примечание: Для этой операции hello `api-version` указан как параметр запроса в URL-АДРЕСЕ hello независимо от того, вызов **предложения** с GET или POST.</span><span class="sxs-lookup"><span data-stu-id="96fee-1121">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="96fee-1122">**Заголовки запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-1122">**Request Headers**</span></span>

<span data-ttu-id="96fee-1123">Hello следующий список описывает hello необходимые и необязательные заголовки запросов</span><span class="sxs-lookup"><span data-stu-id="96fee-1123">hello following list describes hello required and optional request headers</span></span>

* <span data-ttu-id="96fee-1124">`api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="96fee-1124">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="96fee-1125">Это строковое значение, URL-адрес службы уникальный tooyour.</span><span class="sxs-lookup"><span data-stu-id="96fee-1125">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="96fee-1126">Hello **предложения** запроса можно указать ключ администратора либо ключ запроса как hello `api-key`.</span><span class="sxs-lookup"><span data-stu-id="96fee-1126">hello **Suggestions** request can specify either an admin key or query key as hello `api-key`.</span></span>

<span data-ttu-id="96fee-1127">Необходимо также hello имя tooconstruct hello запроса URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="96fee-1127">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="96fee-1128">Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96fee-1128">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="96fee-1129">В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.</span><span class="sxs-lookup"><span data-stu-id="96fee-1129">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="96fee-1130">**Тело запроса**</span><span class="sxs-lookup"><span data-stu-id="96fee-1130">**Request Body**</span></span>

<span data-ttu-id="96fee-1131">Для запроса GET: нет.</span><span class="sxs-lookup"><span data-stu-id="96fee-1131">For GET: None.</span></span>

<span data-ttu-id="96fee-1132">Для запроса POST:</span><span class="sxs-lookup"><span data-stu-id="96fee-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="96fee-1133">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="96fee-1133">**Response**</span></span>

<span data-ttu-id="96fee-1134">Код состояния: в качестве успешного ответа возвращается код "200 — ОК".</span><span class="sxs-lookup"><span data-stu-id="96fee-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="96fee-1135">Если параметр проекции hello используется tooretrieve поля, они включаются в каждый элемент массива hello:</span><span class="sxs-lookup"><span data-stu-id="96fee-1135">If hello projection option is used tooretrieve fields they are included in each element of hello array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="96fee-1136">**Пример**</span><span class="sxs-lookup"><span data-stu-id="96fee-1136">**Example**</span></span>

<span data-ttu-id="96fee-1137">Получение 5 предложений, где «lux» hello частичного ввода условия поиска</span><span class="sxs-lookup"><span data-stu-id="96fee-1137">Retrieve 5 suggestions where hello partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
