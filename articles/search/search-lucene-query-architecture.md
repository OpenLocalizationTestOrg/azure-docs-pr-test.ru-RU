---
title: "Архитектура aaaFull text search engine (Lucene) в поиске Azure | Документы Microsoft"
description: "Объяснение Lucene обработки и документа извлечения основные принципы запросов для полнотекстового поиска, как связанные tooAzure поиска."
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a><span data-ttu-id="452d5-103">Как работает полнотекстовый поиск в службе поиска Azure</span><span class="sxs-lookup"><span data-stu-id="452d5-103">How full text search works in Azure Search</span></span>

<span data-ttu-id="452d5-104">Эта статья предназначена для разработчиков, которым нужно тщательно разобраться с работой полнотекстового поиска Lucene в поиске Azure.</span><span class="sxs-lookup"><span data-stu-id="452d5-104">This article is for developers who need a deeper understanding of how Lucene full text search works in Azure Search.</span></span> <span data-ttu-id="452d5-105">Для текстовых запросов служба поиска Azure в большинстве сценариев быстро предоставляет ожидаемые результаты, однако иногда вы можете получить и неточные результаты.</span><span class="sxs-lookup"><span data-stu-id="452d5-105">For text queries, Azure Search will seamlessly deliver expected results in most scenarios, but occasionally you might get a result that seems "off" somehow.</span></span> <span data-ttu-id="452d5-106">В таких случаях наличие фона в hello четыре этапа выполнения запроса Lucene (запросов анализа Лексический анализ, документов, соответствующих оценки) может помочь определить конкретные изменения tooquery параметры или индекс конфигурацию, которая будет доставлять hello желаемый результат.</span><span class="sxs-lookup"><span data-stu-id="452d5-106">In these situations, having a background in hello four stages of Lucene query execution (query parsing, lexical analysis, document matching, scoring) can help you identify specific changes tooquery parameters or index configuration that will deliver hello desired outcome.</span></span> 

> [!Note] 
> <span data-ttu-id="452d5-107">В службе поиска Azure для полнотекстового поиска используется Lucene, но процесс не ограничивается интеграцией Lucene.</span><span class="sxs-lookup"><span data-stu-id="452d5-107">Azure Search uses Lucene for full text search, but Lucene integration is not exhaustive.</span></span> <span data-ttu-id="452d5-108">Выборочно представлять и расширить Lucene функциональность tooenable hello сценарии важно tooAzure поиска.</span><span class="sxs-lookup"><span data-stu-id="452d5-108">We selectively expose and extend Lucene functionality tooenable hello scenarios important tooAzure Search.</span></span> 

## <a name="architecture-overview-and-diagram"></a><span data-ttu-id="452d5-109">Схема архитектуры и ее обзор</span><span class="sxs-lookup"><span data-stu-id="452d5-109">Architecture overview and diagram</span></span>

<span data-ttu-id="452d5-110">Обработка полнотекстового поиска запроса начинается с синтаксический анализ условий поиска tooextract текст запроса hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-110">Processing a full text search query starts with parsing hello query text tooextract search terms.</span></span> <span data-ttu-id="452d5-111">Hello поисковая система использует tooretrieve индексировать документы с совпадающими терминами.</span><span class="sxs-lookup"><span data-stu-id="452d5-111">hello search engine uses an index tooretrieve documents with matching terms.</span></span> <span data-ttu-id="452d5-112">Отдельные запросы условия иногда разбивкой и воссозданы в новой формы toocast широкой net за то, что может рассматриваться как возможные совпадения.</span><span class="sxs-lookup"><span data-stu-id="452d5-112">Individual query terms are sometimes broken down and reconstituted into new forms toocast a broader net over what could be considered as a potential match.</span></span> <span data-ttu-id="452d5-113">Затем результирующий набор сортируется по релевантности оценка назначенного tooeach отдельных сопоставления документа.</span><span class="sxs-lookup"><span data-stu-id="452d5-113">A result set is then sorted by a relevance score assigned tooeach individual matching document.</span></span> <span data-ttu-id="452d5-114">Те вверху hello hello рангом список возвращаются вызывающему приложению toohello.</span><span class="sxs-lookup"><span data-stu-id="452d5-114">Those at hello top of hello ranked list are returned toohello calling application.</span></span>

<span data-ttu-id="452d5-115">Итак, запрос выполняется в четыре этапа:</span><span class="sxs-lookup"><span data-stu-id="452d5-115">Restated, query execution has four stages:</span></span> 

1. <span data-ttu-id="452d5-116">синтаксический анализ запроса;</span><span class="sxs-lookup"><span data-stu-id="452d5-116">Query parsing</span></span> 
2. <span data-ttu-id="452d5-117">лексический анализ;</span><span class="sxs-lookup"><span data-stu-id="452d5-117">Lexical analysis</span></span> 
3. <span data-ttu-id="452d5-118">извлечение документа;</span><span class="sxs-lookup"><span data-stu-id="452d5-118">Document retrieval</span></span> 
4. <span data-ttu-id="452d5-119">оценка.</span><span class="sxs-lookup"><span data-stu-id="452d5-119">Scoring</span></span> 

<span data-ttu-id="452d5-120">Hello приведенной ниже схеме показано tooprocess компоненты, используемые hello поисковый запрос.</span><span class="sxs-lookup"><span data-stu-id="452d5-120">hello diagram below illustrates hello components used tooprocess a search request.</span></span> 

 ![Схема архитектуры запросов Lucene в службе поиска Azure][1]


| <span data-ttu-id="452d5-122">Ключевые компоненты</span><span class="sxs-lookup"><span data-stu-id="452d5-122">Key components</span></span> | <span data-ttu-id="452d5-123">Описание функций</span><span class="sxs-lookup"><span data-stu-id="452d5-123">Functional description</span></span> | 
|----------------|------------------------|
|<span data-ttu-id="452d5-124">**Средства синтаксического анализа запроса**</span><span class="sxs-lookup"><span data-stu-id="452d5-124">**Query parsers**</span></span> | <span data-ttu-id="452d5-125">Отдельные операторы выражений запросов и создать hello запрос структуры запроса дерева, отправляемых toobe toohello поисковой системы.</span><span class="sxs-lookup"><span data-stu-id="452d5-125">Separate query terms from query operators and create hello query structure (a query tree) toobe sent toohello search engine.</span></span> |
|<span data-ttu-id="452d5-126">**Анализаторы**</span><span class="sxs-lookup"><span data-stu-id="452d5-126">**Analyzers**</span></span> | <span data-ttu-id="452d5-127">Выполняют лексический анализ терминов запроса,</span><span class="sxs-lookup"><span data-stu-id="452d5-127">Perform lexical analysis on query terms.</span></span> <span data-ttu-id="452d5-128">что может включать их преобразование, удаление или расширение.</span><span class="sxs-lookup"><span data-stu-id="452d5-128">This process can involve transforming, removing, or expanding of query terms.</span></span> |
|<span data-ttu-id="452d5-129">**Индекс**</span><span class="sxs-lookup"><span data-stu-id="452d5-129">**Index**</span></span> | <span data-ttu-id="452d5-130">Структуру данных, эффективно использовать toostore и организации с возможностью поиска термины, извлеченные из индексированных документов.</span><span class="sxs-lookup"><span data-stu-id="452d5-130">An efficient data structure used toostore and organize searchable terms extracted from indexed documents.</span></span> |
|<span data-ttu-id="452d5-131">**Поисковая система**</span><span class="sxs-lookup"><span data-stu-id="452d5-131">**Search engine**</span></span> | <span data-ttu-id="452d5-132">Извлекает и оценки соответствия документов на основании содержимого hello hello инвертированный индекс.</span><span class="sxs-lookup"><span data-stu-id="452d5-132">Retrieves and scores matching documents based on hello contents of hello inverted index.</span></span> |

## <a name="anatomy-of-a-search-request"></a><span data-ttu-id="452d5-133">Схема поискового запроса</span><span class="sxs-lookup"><span data-stu-id="452d5-133">Anatomy of a search request</span></span>

<span data-ttu-id="452d5-134">Поисковый запрос представляет собой полную спецификацию содержимого, возвращаемого в результирующем наборе.</span><span class="sxs-lookup"><span data-stu-id="452d5-134">A search request is a complete specification of what should be returned in a result set.</span></span> <span data-ttu-id="452d5-135">В самой простой форме это пустой запрос с отсутствием каких-либо критериев.</span><span class="sxs-lookup"><span data-stu-id="452d5-135">In simplest form, it is an empty query with no criteria of any kind.</span></span> <span data-ttu-id="452d5-136">Более реалистичный пример включает параметры, некоторые запрос условия, возможно с областью toocertain поля, возможно критерий фильтра и упорядочения правила.</span><span class="sxs-lookup"><span data-stu-id="452d5-136">A more realistic example includes parameters, several query terms, perhaps scoped toocertain fields, with possibly a filter expression and ordering rules.</span></span>  

<span data-ttu-id="452d5-137">Hello ниже приведен запрос поиска может отправить tooAzure поиска с помощью hello [API-интерфейса REST](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="452d5-137">hello following example is a search request you might send tooAzure Search using hello [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

<span data-ttu-id="452d5-138">Для этого запроса hello поисковая система hello следующие:</span><span class="sxs-lookup"><span data-stu-id="452d5-138">For this request, hello search engine does hello following:</span></span>

1. <span data-ttu-id="452d5-139">Отфильтровывает документы, где цена hello менее 60 и меньше 300 долларов.</span><span class="sxs-lookup"><span data-stu-id="452d5-139">Filters out documents where hello price is at least $60 and less than $300.</span></span>
2. <span data-ttu-id="452d5-140">Выполняет запрос hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-140">Executes hello query.</span></span> <span data-ttu-id="452d5-141">В этом примере запрос поиска hello состоит фраз и условиями: `"Spacious, air-condition* +\"Ocean view\""` (пользователи обычно не ввести знаки препинания, но его включением в примере hello позволяет нам tooexplain как анализаторы обрабатывать).</span><span class="sxs-lookup"><span data-stu-id="452d5-141">In this example, hello search query consists of phrases and terms: `"Spacious, air-condition* +\"Ocean view\""` (users typically don't enter punctuation, but including it in hello example allows us tooexplain how analyzers handle it).</span></span> <span data-ttu-id="452d5-142">Для этого запроса hello поисковая система проверяет описание hello и поля заголовка, указываемой `searchFields` документы, содержащие «Аквамарин view» и дополнительно hello термин «снижает» или термины, которые начинаются с префикса hello «air-condition».</span><span class="sxs-lookup"><span data-stu-id="452d5-142">For this query, hello search engine scans hello description and title fields specified in `searchFields` for documents that contain "Ocean view", and additionally on hello term "spacious", or on terms that start with hello prefix "air-condition".</span></span> <span data-ttu-id="452d5-143">Hello `searchMode` параметр является используется toomatch на любой термин (по умолчанию) или все из них, в случае если условие не указано явно (`+`).</span><span class="sxs-lookup"><span data-stu-id="452d5-143">hello `searchMode` parameter is used toomatch on any term (default) or all of them, for cases where a term is not explicitly required (`+`).</span></span>
3. <span data-ttu-id="452d5-144">Заказы hello результирующий набор гостиницы по сходству tooa заданное место geography, а затем возвращается вызывающему приложению toohello.</span><span class="sxs-lookup"><span data-stu-id="452d5-144">Orders hello resulting set of hotels by proximity tooa given geography location, and then returned toohello calling application.</span></span> 

<span data-ttu-id="452d5-145">Hello основная часть этой статьи посвящена обработку hello *поискового запроса*: `"Spacious, air-condition* +\"Ocean view\""`.</span><span class="sxs-lookup"><span data-stu-id="452d5-145">hello majority of this article is about processing of hello *search query*: `"Spacious, air-condition* +\"Ocean view\""`.</span></span> <span data-ttu-id="452d5-146">Фильтрация и упорядочение выходят за рамки этого руководства.</span><span class="sxs-lookup"><span data-stu-id="452d5-146">Filtering and ordering are out of scope.</span></span> <span data-ttu-id="452d5-147">Дополнительные сведения см. в разделе hello [справочная документация по API поиска](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="452d5-147">For more information, see hello [Search API reference documentation](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a><span data-ttu-id="452d5-148">Этап 1. Синтаксический анализ запроса</span><span class="sxs-lookup"><span data-stu-id="452d5-148">Stage 1: Query parsing</span></span> 

<span data-ttu-id="452d5-149">Как уже отмечалось, строка hello запроса является первой строки запроса hello hello:</span><span class="sxs-lookup"><span data-stu-id="452d5-149">As noted, hello query string is hello first line of hello request:</span></span> 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

<span data-ttu-id="452d5-150">Анализатор отделяет операторы запросов Hello (такие как `*` и `+` в примере hello) из поиска терминов и деконструирование hello поискового запроса в *вложенные запросы* относится к поддерживаемым типам:</span><span class="sxs-lookup"><span data-stu-id="452d5-150">hello query parser separates operators (such as `*` and `+` in hello example) from search terms, and deconstructs hello search query into *subqueries* of a supported type:</span></span> 

+ <span data-ttu-id="452d5-151">*запрос термина* — для автономных терминов (например, spacious);</span><span class="sxs-lookup"><span data-stu-id="452d5-151">*term query* for standalone terms (like spacious)</span></span>
+ <span data-ttu-id="452d5-152">*запрос фразы* — для терминов, заключенных в кавычки (например, ocean view);</span><span class="sxs-lookup"><span data-stu-id="452d5-152">*phrase query* for quoted terms (like ocean view)</span></span>
+ <span data-ttu-id="452d5-153">*запрос префикса* — для терминов, за которыми следует оператор префикса `*` (например, air-condition).</span><span class="sxs-lookup"><span data-stu-id="452d5-153">*prefix query* for terms followed by a prefix operator `*` (like air-condition)</span></span>

<span data-ttu-id="452d5-154">Полный список поддерживаемых типов запросов см. в статье о [синтаксисе запросов Lucene в службе поиска Azure](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search).</span><span class="sxs-lookup"><span data-stu-id="452d5-154">For a full list of supported query types see [Lucene query sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span></span>

<span data-ttu-id="452d5-155">Операторы, связанный с вложенным запросом определяют hello запрос «должно быть» или «должен быть» удовлетворен в порядке документа toobe совпадении.</span><span class="sxs-lookup"><span data-stu-id="452d5-155">Operators associated with a subquery determine whether hello query "must be" or "should be" satisfied in order for a document toobe considered a match.</span></span> <span data-ttu-id="452d5-156">Например `+"Ocean view"` «необходимо» из-за toohello `+` оператор.</span><span class="sxs-lookup"><span data-stu-id="452d5-156">For example, `+"Ocean view"` is "must" due toohello `+` operator.</span></span> 

<span data-ttu-id="452d5-157">средство синтаксического анализа запросов Hello перестраивает hello вложенные запросы в *дерево запроса* (внутренняя структура представляющий hello запрос), он передает на toohello поисковой системы.</span><span class="sxs-lookup"><span data-stu-id="452d5-157">hello query parser restructures hello subqueries into a *query tree* (an internal structure representing hello query) it passes on toohello search engine.</span></span> <span data-ttu-id="452d5-158">Hello первой стадии синтаксического анализа запроса дерево запроса hello выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="452d5-158">In hello first stage of query parsing, hello query tree looks like this.</span></span>  

 ![Режим поиска логических запросов any][2]

### <a name="supported-parsers-simple-and-full-lucene"></a><span data-ttu-id="452d5-160">Поддерживаемые средства синтаксического анализа запроса для упрощенного и полного языка запросов Lucene</span><span class="sxs-lookup"><span data-stu-id="452d5-160">Supported parsers: Simple and Full Lucene</span></span> 

 <span data-ttu-id="452d5-161">Служба поиска Azure поддерживает два разных языка запросов — `simple` (по умолчанию) и `full`.</span><span class="sxs-lookup"><span data-stu-id="452d5-161">Azure Search exposes two different query languages, `simple` (default) and `full`.</span></span> <span data-ttu-id="452d5-162">Путем установки hello `queryType` параметр в запрос поиска, вы указываете hello синтаксического анализа запросов языка запроса выбрать, чтобы оно было известно как toointerpret Здравствуйте, операторах и синтаксисе.</span><span class="sxs-lookup"><span data-stu-id="452d5-162">By setting hello `queryType` parameter with your search request, you tell hello query parser which query language you choose so that it knows how toointerpret hello operators and syntax.</span></span> <span data-ttu-id="452d5-163">Hello [язык простой запрос](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) производится интуитивно понятно и надежной, ввод данных пользователем часто подходящий toointerpret как-без обработки на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="452d5-163">hello [Simple query langauge](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) is intuitive and robust, often suitable toointerpret user input as-is without client-side processing.</span></span> <span data-ttu-id="452d5-164">Он поддерживает те же операторы запросов,что и поисковые системы в Интернете.</span><span class="sxs-lookup"><span data-stu-id="452d5-164">It supports query operators familiar from web search engines.</span></span> <span data-ttu-id="452d5-165">Hello [полного Lucene язык запросов](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), который можно получить, установив `queryType=full`, расширяет язык простого запроса по умолчанию hello, добавляя поддержку дополнительные операторы и типы запросов как подстановочный знак, Нечеткий, регулярных выражений и запросов в области полей.</span><span class="sxs-lookup"><span data-stu-id="452d5-165">hello [Full Lucene query language](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), which you get by setting `queryType=full`, extends hello default Simple query language by adding support for more operators and query types like wildcard, fuzzy, regex, and field-scoped queries.</span></span> <span data-ttu-id="452d5-166">Например, регулярное выражение, отправленное в простой синтаксис запросов, будет интерпретироваться как строка запроса, а не как выражение.</span><span class="sxs-lookup"><span data-stu-id="452d5-166">For example, a regular expression sent in Simple query syntax would be interpreted as a query string and not an expression.</span></span> <span data-ttu-id="452d5-167">Пример запроса Hello в этой статье использует язык запросов полного Lucene hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-167">hello example request in this article uses hello Full Lucene query language.</span></span>

### <a name="impact-of-searchmode-on-hello-parser"></a><span data-ttu-id="452d5-168">Влияние поиска searchMode анализатор hello</span><span class="sxs-lookup"><span data-stu-id="452d5-168">Impact of searchMode on hello parser</span></span> 

<span data-ttu-id="452d5-169">Другим параметром запрос поиска, который влияет на синтаксический анализ является hello `searchMode` параметра.</span><span class="sxs-lookup"><span data-stu-id="452d5-169">Another search request parameter that affects parsing is hello `searchMode` parameter.</span></span> <span data-ttu-id="452d5-170">Он управляет hello оператор по умолчанию для запросов типа Boolean: все (по умолчанию) или все.</span><span class="sxs-lookup"><span data-stu-id="452d5-170">It controls hello default operator for Boolean queries: any (default) or all.</span></span>  

<span data-ttu-id="452d5-171">При `searchMode=any`, которой по умолчанию hello, разделитель пространства hello снижает и air-condition или (`||`), что эквивалентно hello образец текста запроса:</span><span class="sxs-lookup"><span data-stu-id="452d5-171">When `searchMode=any`, which is hello default, hello space delimiter between spacious and air-condition is OR (`||`), making hello sample query text equivalent to:</span></span> 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

<span data-ttu-id="452d5-172">Явные операторы, такие как `+` в `+"Ocean view"`, однозначны создания логического запроса (hello термин *должен* совпадают).</span><span class="sxs-lookup"><span data-stu-id="452d5-172">Explicit operators, such as `+` in `+"Ocean view"`, are unambiguous in boolean query construction (hello term *must* match).</span></span> <span data-ttu-id="452d5-173">Очевидно, как условия hello toointerpret осталось: снижает и air-condition.</span><span class="sxs-lookup"><span data-stu-id="452d5-173">Less obvious is how toointerpret hello remaining terms: spacious and air-condition.</span></span> <span data-ttu-id="452d5-174">Следует hello поисковая система поиска соответствий на Океан *и* снижает *и* air-condition?</span><span class="sxs-lookup"><span data-stu-id="452d5-174">Should hello search engine find matches on ocean view *and* spacious *and* air-condition?</span></span> <span data-ttu-id="452d5-175">Или следует найти Океан, а также *любого* из оставшихся условия hello?</span><span class="sxs-lookup"><span data-stu-id="452d5-175">Or should it find ocean view plus *either one* of hello remaining terms?</span></span> 

<span data-ttu-id="452d5-176">По умолчанию (`searchMode=any`), hello поисковой системы предполагает более широкой Интерпретация hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-176">By default (`searchMode=any`), hello search engine assumes hello broader interpretation.</span></span> <span data-ttu-id="452d5-177">Будет выполняться поиск соответствия по какому-либо из терминов, что *представляет* семантику оператора or.</span><span class="sxs-lookup"><span data-stu-id="452d5-177">Either field *should* be matched, reflecting "or" semantics.</span></span> <span data-ttu-id="452d5-178">Hello начального запроса дерева ранее проиллюстрировать на примере hello две «должно» операции, по умолчанию отображает hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-178">hello initial query tree illustrated previously, with hello two "should" operations, shows hello default.</span></span>  

<span data-ttu-id="452d5-179">Предположим, что мы задали параметр `searchMode=all`.</span><span class="sxs-lookup"><span data-stu-id="452d5-179">Suppose that we now set `searchMode=all`.</span></span> <span data-ttu-id="452d5-180">В этом случае пространство hello интерпретируется как операция «и».</span><span class="sxs-lookup"><span data-stu-id="452d5-180">In this case, hello space is interpreted as an "and" operation.</span></span> <span data-ttu-id="452d5-181">Каждый из оставшихся условия hello оба следует предоставить в tooqualify hello документа как совпадение.</span><span class="sxs-lookup"><span data-stu-id="452d5-181">Each of hello remaining terms must both be present in hello document tooqualify as a match.</span></span> <span data-ttu-id="452d5-182">результирующий запрос Образец Hello интерпретируется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="452d5-182">hello resulting sample query would be interpreted as follows:</span></span> 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

<span data-ttu-id="452d5-183">Измененный запрос дерева для этого запроса будет следующим образом, когда соответствующий документ представляет пересечение hello все три вложенных запросов:</span><span class="sxs-lookup"><span data-stu-id="452d5-183">A modified query tree for this query would be as follows, where a matching document is hello intersection of all three subqueries:</span></span> 

 ![Режим поиска логических запросов all][3]

> [!Note] 
> <span data-ttu-id="452d5-185">Для выполнения репрезентативных запросов лучше выбрать `searchMode=any`, а не `searchMode=all`.</span><span class="sxs-lookup"><span data-stu-id="452d5-185">Choosing `searchMode=any` over `searchMode=all` is a decision best arrived at by running representative queries.</span></span> <span data-ttu-id="452d5-186">Пользователи, имеющие вероятность tooinclude операторы (общее при поиске документа хранит) может оказаться результатов более понятными, если `searchMode=all` информирует конструкции логический запрос.</span><span class="sxs-lookup"><span data-stu-id="452d5-186">Users who are likely tooinclude operators (common when searching document stores) might find results more intuitive if `searchMode=all` informs boolean query constructs.</span></span> <span data-ttu-id="452d5-187">Дополнительные сведения о hello взаимозависимость между `searchMode` и операторы, в разделе [синтаксис простого запроса](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span><span class="sxs-lookup"><span data-stu-id="452d5-187">For more about hello interplay between `searchMode` and operators, see [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span></span>

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a><span data-ttu-id="452d5-188">Этап 2. Лексический анализ</span><span class="sxs-lookup"><span data-stu-id="452d5-188">Stage 2: Lexical analysis</span></span> 

<span data-ttu-id="452d5-189">Процесс лексические анализаторы *терминов запросов* и *фразу запросы* после структурированные дерево запроса hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-189">Lexical analyzers process *term queries* and *phrase queries* after hello query tree is structured.</span></span> <span data-ttu-id="452d5-190">Анализатор принимает hello текстовое входов заданному tooit анализатором hello, процессы hello текст и затем отправляет обратно токеном условия, которые toobe частью hello дерево запроса.</span><span class="sxs-lookup"><span data-stu-id="452d5-190">An analyzer accepts hello text inputs given tooit by hello parser, processes hello text, and then sends back tokenized terms toobe incorporated into hello query tree.</span></span> 

<span data-ttu-id="452d5-191">Наиболее распространенная форма Hello лексического анализа является *лингвистический анализ* преобразующий запроса термов на основании определенных tooa правилами заданного языка:</span><span class="sxs-lookup"><span data-stu-id="452d5-191">hello most common form of lexical analysis is *linguistic analysis* which transforms query terms based on rules specific tooa given language:</span></span> 

* <span data-ttu-id="452d5-192">Уменьшение форма запроса термин toohello корневого слова</span><span class="sxs-lookup"><span data-stu-id="452d5-192">Reducing a query term toohello root form of a word</span></span> 
* <span data-ttu-id="452d5-193">удаляет слова, которые не представляют смысла (стоп-слова, например артикли the и and в английском языке);</span><span class="sxs-lookup"><span data-stu-id="452d5-193">Removing non-essential words (stopwords, such as "the" or "and" in English)</span></span> 
* <span data-ttu-id="452d5-194">разбивает составные слова на части;</span><span class="sxs-lookup"><span data-stu-id="452d5-194">Breaking a composite word into component parts</span></span> 
* <span data-ttu-id="452d5-195">преобразовывает слова с верхним регистром в нижний.</span><span class="sxs-lookup"><span data-stu-id="452d5-195">Lower casing an upper case word</span></span> 

<span data-ttu-id="452d5-196">Все эти операции, как правило, различия tooerase ввода текста hello, предоставляемые hello пользователя и hello терминов, хранящийся в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-196">All of these operations tend tooerase differences between hello text input provided by hello user and hello terms stored in hello index.</span></span> <span data-ttu-id="452d5-197">Такие операции выходят за пределы обработки текста и требуется обширный опыт сам язык hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-197">Such operations go beyond text processing and require in-depth knowledge of hello language itself.</span></span> <span data-ttu-id="452d5-198">tooadd этого слоя лингвистические учета, поиска Azure поддерживает длинный список [языковых анализаторов](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene и Microsoft.</span><span class="sxs-lookup"><span data-stu-id="452d5-198">tooadd this layer of linguistic awareness, Azure Search supports a long list of [language analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support) from both Lucene and Microsoft.</span></span>

> [!Note]
> <span data-ttu-id="452d5-199">Анализ требований может варьироваться от минимальной tooelaborate в зависимости от вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="452d5-199">Analysis requirements can range from minimal tooelaborate depending on your scenario.</span></span> <span data-ttu-id="452d5-200">Можно управлять сложности лексического анализа, hello, выбрав один из анализаторов предопределенные hello или создав собственный [пользовательского анализатора](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="452d5-200">You can control complexity of lexical analysis by hello selecting one of hello predefined analyzers or by creating your own [custom analyzer](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span></span> <span data-ttu-id="452d5-201">Анализаторы области toosearchable поля и указаны как часть определения поля.</span><span class="sxs-lookup"><span data-stu-id="452d5-201">Analyzers are scoped toosearchable fields and are specified as part of a field definition.</span></span> <span data-ttu-id="452d5-202">Это позволяет toovary лексического анализа на основе каждого поля.</span><span class="sxs-lookup"><span data-stu-id="452d5-202">This allows you toovary lexical analysis on a per-field basis.</span></span> <span data-ttu-id="452d5-203">Не указан, hello *Стандартная* анализатор Lucene используется.</span><span class="sxs-lookup"><span data-stu-id="452d5-203">Unspecified, hello *standard* Lucene analyzer is used.</span></span>

<span data-ttu-id="452d5-204">В нашем примере предыдущего tooanalysis hello начального запроса дерева имеет hello термин «Spacious» с заглавную букву «S» и интерпретирует запятую, которая hello синтаксического анализа запросов как часть поисковому запросу hello (запятая не считается оператор языка запроса).</span><span class="sxs-lookup"><span data-stu-id="452d5-204">In our example, prior tooanalysis, hello initial query tree has hello term "Spacious," with an uppercase "S" and a comma that hello query parser interprets as a part of hello query term (a comma is not considered a query language operator).</span></span>  

<span data-ttu-id="452d5-205">При анализатора по умолчанию hello обрабатывает hello термина, будет «представление Аквамарин» и «снижает» в нижнем регистре и удалите символ запятой hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-205">When hello default analyzer processes hello term, it will lowercase "ocean view" and "spacious", and remove hello comma character.</span></span> <span data-ttu-id="452d5-206">дерево Hello измененный запрос будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="452d5-206">hello modified query tree will look as follows:</span></span> 

 ![Логический запрос с терминами после анализа][4]

### <a name="testing-analyzer-behaviors"></a><span data-ttu-id="452d5-208">Проверка поведения анализатора</span><span class="sxs-lookup"><span data-stu-id="452d5-208">Testing analyzer behaviors</span></span> 

<span data-ttu-id="452d5-209">поведение Hello анализатор можно проверить при помощи hello [анализ API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span><span class="sxs-lookup"><span data-stu-id="452d5-209">hello behavior of an analyzer can be tested using hello [Analyze API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span></span> <span data-ttu-id="452d5-210">Укажите нужный tooanalyze toosee какие термины, учитывая анализатор будет формировать текст hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-210">Provide hello text you want tooanalyze toosee what terms given analyzer will generate.</span></span> <span data-ttu-id="452d5-211">Например как стандартный анализатор hello будет обрабатывать toosee Здравствуйте, текст «air-condition», может выдавать hello, следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="452d5-211">For example, toosee how hello standard analyzer would process hello text "air-condition", you can issue hello following request:</span></span>

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

<span data-ttu-id="452d5-212">стандартный анализатор Hello разбивает входной текст hello на hello, следующие два маркера, Создание примечаний к их атрибутов, например Пуск и конечного смещения (используется для выделения попаданий), а также их расположения (используется для сопоставления фразы):</span><span class="sxs-lookup"><span data-stu-id="452d5-212">hello standard analyzer breaks hello input text into hello following two tokens, annotating them with attributes like start and end offsets (used for hit highlighting) as well as their position (used for phrase matching):</span></span>

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-toolexical-analysis"></a><span data-ttu-id="452d5-213">Анализ toolexical исключения</span><span class="sxs-lookup"><span data-stu-id="452d5-213">Exceptions toolexical analysis</span></span> 

<span data-ttu-id="452d5-214">Лексический анализ применяется только tooquery типы, требующие полного условия — запрос термин или фраза запроса.</span><span class="sxs-lookup"><span data-stu-id="452d5-214">Lexical analysis applies only tooquery types that require complete terms – either a term query or a phrase query.</span></span> <span data-ttu-id="452d5-215">Он не распространяется tooquery типы с неполными условия — префикс запрос, шаблон запроса, регулярное выражение запроса или tooa Нечеткий уточняющий запрос.</span><span class="sxs-lookup"><span data-stu-id="452d5-215">It doesn’t apply tooquery types with incomplete terms – prefix query, wildcard query, regex query – or tooa fuzzy query.</span></span> <span data-ttu-id="452d5-216">Те запроса типов, включая запрос префикс hello термин *air-condition\**  в нашем примере добавляются непосредственно дерево запроса toohello, минуя этап анализа hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-216">Those query types, including hello prefix query with term *air-condition\** in our example, are added directly toohello query tree, bypassing hello analysis stage.</span></span> <span data-ttu-id="452d5-217">Hello только преобразование, выполненное на условиях запроса этих типов строчной версии.</span><span class="sxs-lookup"><span data-stu-id="452d5-217">hello only transformation performed on query terms of those types is lowercasing.</span></span>

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a><span data-ttu-id="452d5-218">Этап 3. Извлечение документа</span><span class="sxs-lookup"><span data-stu-id="452d5-218">Stage 3: Document retrieval</span></span> 

<span data-ttu-id="452d5-219">Получение документа относится toofinding документы с совпадающими терминами в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-219">Document retrieval refers toofinding documents with matching terms in hello index.</span></span> <span data-ttu-id="452d5-220">Лучше всего этот этап рассмотреть на примере.</span><span class="sxs-lookup"><span data-stu-id="452d5-220">This stage is understood best through an example.</span></span> <span data-ttu-id="452d5-221">Начнем с индексом гостиницы, имеющих hello, следуя простой схемы:</span><span class="sxs-lookup"><span data-stu-id="452d5-221">Let's start with a hotels index having hello following simple schema:</span></span> 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

<span data-ttu-id="452d5-222">Далее предполагается, что этот индекс содержит следующие четыре документы hello:</span><span class="sxs-lookup"><span data-stu-id="452d5-222">Further assume that this index contains hello following four documents:</span></span> 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

<span data-ttu-id="452d5-223">**Как индексируются термины**</span><span class="sxs-lookup"><span data-stu-id="452d5-223">**How terms are indexed**</span></span>

<span data-ttu-id="452d5-224">Получение toounderstand помогает tooknow с основными сведениями об индексировании.</span><span class="sxs-lookup"><span data-stu-id="452d5-224">toounderstand retrieval, it helps tooknow a few basics about indexing.</span></span> <span data-ttu-id="452d5-225">Hello единицей хранилища является инвертированного индекса, по одному для каждого поля для поиска.</span><span class="sxs-lookup"><span data-stu-id="452d5-225">hello unit of storage is an inverted index, one for each searchable field.</span></span> <span data-ttu-id="452d5-226">Обращенный индекс содержит отсортированный список со всеми терминами из всех документов.</span><span class="sxs-lookup"><span data-stu-id="452d5-226">Within an inverted index is a sorted list of all terms from all documents.</span></span> <span data-ttu-id="452d5-227">Каждый термин сопоставляет toohello список документов, в которых он применяется, как видно в приведенном ниже примере hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-227">Each term maps toohello list of documents in which it occurs, as evident in hello example below.</span></span>

<span data-ttu-id="452d5-228">условия tooproduce hello в инвертированном индексе, hello поисковая система выполняет лексического анализа над содержимым hello документов, аналогичные toowhat происходит во время обработки запроса.</span><span class="sxs-lookup"><span data-stu-id="452d5-228">tooproduce hello terms in an inverted index, hello search engine performs lexical analysis over hello content of documents, similar toowhat happens during query processing.</span></span> <span data-ttu-id="452d5-229">Текстовые входные данные передаются tooan анализатора в нижнем регистре, удаляются знаки пунктуации и т. д., в зависимости от конфигурации анализатора hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-229">Text inputs are passed tooan analyzer, lower-cased, stripped of punctuation, and so forth, depending on hello analyzer configuration.</span></span> <span data-ttu-id="452d5-230">Общие, но не обязательны, toouse hello же анализаторы для поиска и индексирования операции, чтобы больше похожи на условия в индексе hello выражений запросов.</span><span class="sxs-lookup"><span data-stu-id="452d5-230">It's common, but not required, toouse hello same analyzers for search and indexing operations so that query terms look more like terms inside hello index.</span></span>

> [!Note]
> <span data-ttu-id="452d5-231">Служба поиска Azure позволяет указать различные анализаторы для индексирования и поиска с помощью дополнительных параметров полей — `indexAnalyzer` и `searchAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="452d5-231">Azure Search lets you specify different analyzers for indexing and search via additional `indexAnalyzer` and `searchAnalyzer` field parameters.</span></span> <span data-ttu-id="452d5-232">Если не указано, hello анализатора hello `analyzer` свойство используется для индексирования и поиска.</span><span class="sxs-lookup"><span data-stu-id="452d5-232">If unspecified, hello analyzer set with hello `analyzer` property is used for both indexing and searching.</span></span>  

<span data-ttu-id="452d5-233">**Обращенный индекс для примеров документов**</span><span class="sxs-lookup"><span data-stu-id="452d5-233">**Inverted index for example documents**</span></span>

<span data-ttu-id="452d5-234">Возвращение примере tooour для hello **заголовок** поле hello инвертированный индекс выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="452d5-234">Returning tooour example, for hello **title** field, hello inverted index looks like this:</span></span>

| <span data-ttu-id="452d5-235">Термин</span><span class="sxs-lookup"><span data-stu-id="452d5-235">Term</span></span> | <span data-ttu-id="452d5-236">Список документов</span><span class="sxs-lookup"><span data-stu-id="452d5-236">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="452d5-237">atman</span><span class="sxs-lookup"><span data-stu-id="452d5-237">atman</span></span> | <span data-ttu-id="452d5-238">1</span><span class="sxs-lookup"><span data-stu-id="452d5-238">1</span></span> |
| <span data-ttu-id="452d5-239">beach</span><span class="sxs-lookup"><span data-stu-id="452d5-239">beach</span></span> | <span data-ttu-id="452d5-240">2</span><span class="sxs-lookup"><span data-stu-id="452d5-240">2</span></span> |
| <span data-ttu-id="452d5-241">hotel</span><span class="sxs-lookup"><span data-stu-id="452d5-241">hotel</span></span> | <span data-ttu-id="452d5-242">1, 3</span><span class="sxs-lookup"><span data-stu-id="452d5-242">1, 3</span></span> |
| <span data-ttu-id="452d5-243">ocean</span><span class="sxs-lookup"><span data-stu-id="452d5-243">ocean</span></span> | <span data-ttu-id="452d5-244">4.</span><span class="sxs-lookup"><span data-stu-id="452d5-244">4</span></span>  |
| <span data-ttu-id="452d5-245">playa</span><span class="sxs-lookup"><span data-stu-id="452d5-245">playa</span></span> | <span data-ttu-id="452d5-246">3</span><span class="sxs-lookup"><span data-stu-id="452d5-246">3</span></span> |
| <span data-ttu-id="452d5-247">resort</span><span class="sxs-lookup"><span data-stu-id="452d5-247">resort</span></span> | <span data-ttu-id="452d5-248">3</span><span class="sxs-lookup"><span data-stu-id="452d5-248">3</span></span> |
| <span data-ttu-id="452d5-249">retreat</span><span class="sxs-lookup"><span data-stu-id="452d5-249">retreat</span></span> | <span data-ttu-id="452d5-250">4.</span><span class="sxs-lookup"><span data-stu-id="452d5-250">4</span></span> |

<span data-ttu-id="452d5-251">В поле заголовка hello, только *гостиницы* отображается в двух документов: 1, 3.</span><span class="sxs-lookup"><span data-stu-id="452d5-251">In hello title field, only *hotel* shows up in two documents: 1, 3.</span></span>

<span data-ttu-id="452d5-252">Для hello **описание** поля, индекс hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="452d5-252">For hello **description** field, hello index is as follows:</span></span>

| <span data-ttu-id="452d5-253">Термин</span><span class="sxs-lookup"><span data-stu-id="452d5-253">Term</span></span> | <span data-ttu-id="452d5-254">Список документов</span><span class="sxs-lookup"><span data-stu-id="452d5-254">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="452d5-255">air</span><span class="sxs-lookup"><span data-stu-id="452d5-255">air</span></span> | <span data-ttu-id="452d5-256">3</span><span class="sxs-lookup"><span data-stu-id="452d5-256">3</span></span>
| <span data-ttu-id="452d5-257">и</span><span class="sxs-lookup"><span data-stu-id="452d5-257">and</span></span> | <span data-ttu-id="452d5-258">4.</span><span class="sxs-lookup"><span data-stu-id="452d5-258">4</span></span>
| <span data-ttu-id="452d5-259">beach</span><span class="sxs-lookup"><span data-stu-id="452d5-259">beach</span></span> | <span data-ttu-id="452d5-260">1</span><span class="sxs-lookup"><span data-stu-id="452d5-260">1</span></span>
| <span data-ttu-id="452d5-261">conditioned</span><span class="sxs-lookup"><span data-stu-id="452d5-261">conditioned</span></span> | <span data-ttu-id="452d5-262">3</span><span class="sxs-lookup"><span data-stu-id="452d5-262">3</span></span>
| <span data-ttu-id="452d5-263">comfortable</span><span class="sxs-lookup"><span data-stu-id="452d5-263">comfortable</span></span> | <span data-ttu-id="452d5-264">3</span><span class="sxs-lookup"><span data-stu-id="452d5-264">3</span></span>
| <span data-ttu-id="452d5-265">distance</span><span class="sxs-lookup"><span data-stu-id="452d5-265">distance</span></span> | <span data-ttu-id="452d5-266">1</span><span class="sxs-lookup"><span data-stu-id="452d5-266">1</span></span>
| <span data-ttu-id="452d5-267">island</span><span class="sxs-lookup"><span data-stu-id="452d5-267">island</span></span> | <span data-ttu-id="452d5-268">2</span><span class="sxs-lookup"><span data-stu-id="452d5-268">2</span></span>
| <span data-ttu-id="452d5-269">kauaʻi</span><span class="sxs-lookup"><span data-stu-id="452d5-269">kauaʻi</span></span> | <span data-ttu-id="452d5-270">2</span><span class="sxs-lookup"><span data-stu-id="452d5-270">2</span></span>
| <span data-ttu-id="452d5-271">located</span><span class="sxs-lookup"><span data-stu-id="452d5-271">located</span></span> | <span data-ttu-id="452d5-272">2</span><span class="sxs-lookup"><span data-stu-id="452d5-272">2</span></span>
| <span data-ttu-id="452d5-273">north</span><span class="sxs-lookup"><span data-stu-id="452d5-273">north</span></span> | <span data-ttu-id="452d5-274">2</span><span class="sxs-lookup"><span data-stu-id="452d5-274">2</span></span>
| <span data-ttu-id="452d5-275">ocean</span><span class="sxs-lookup"><span data-stu-id="452d5-275">ocean</span></span> | <span data-ttu-id="452d5-276">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="452d5-276">1, 2, 3</span></span>
| <span data-ttu-id="452d5-277">of</span><span class="sxs-lookup"><span data-stu-id="452d5-277">of</span></span> | <span data-ttu-id="452d5-278">2</span><span class="sxs-lookup"><span data-stu-id="452d5-278">2</span></span>
| <span data-ttu-id="452d5-279">on</span><span class="sxs-lookup"><span data-stu-id="452d5-279">on</span></span> |<span data-ttu-id="452d5-280">2</span><span class="sxs-lookup"><span data-stu-id="452d5-280">2</span></span>
| <span data-ttu-id="452d5-281">quiet</span><span class="sxs-lookup"><span data-stu-id="452d5-281">quiet</span></span> | <span data-ttu-id="452d5-282">4.</span><span class="sxs-lookup"><span data-stu-id="452d5-282">4</span></span>
| <span data-ttu-id="452d5-283">rooms</span><span class="sxs-lookup"><span data-stu-id="452d5-283">rooms</span></span>  | <span data-ttu-id="452d5-284">1, 3</span><span class="sxs-lookup"><span data-stu-id="452d5-284">1, 3</span></span>
| <span data-ttu-id="452d5-285">secluded</span><span class="sxs-lookup"><span data-stu-id="452d5-285">secluded</span></span> | <span data-ttu-id="452d5-286">4.</span><span class="sxs-lookup"><span data-stu-id="452d5-286">4</span></span>
| <span data-ttu-id="452d5-287">shore</span><span class="sxs-lookup"><span data-stu-id="452d5-287">shore</span></span> | <span data-ttu-id="452d5-288">2</span><span class="sxs-lookup"><span data-stu-id="452d5-288">2</span></span>
| <span data-ttu-id="452d5-289">spacious</span><span class="sxs-lookup"><span data-stu-id="452d5-289">spacious</span></span> | <span data-ttu-id="452d5-290">1</span><span class="sxs-lookup"><span data-stu-id="452d5-290">1</span></span>
| <span data-ttu-id="452d5-291">Привет</span><span class="sxs-lookup"><span data-stu-id="452d5-291">hello</span></span> | <span data-ttu-id="452d5-292">1, 2</span><span class="sxs-lookup"><span data-stu-id="452d5-292">1, 2</span></span>
| <span data-ttu-id="452d5-293">слишком</span><span class="sxs-lookup"><span data-stu-id="452d5-293">too</span></span>| <span data-ttu-id="452d5-294">1</span><span class="sxs-lookup"><span data-stu-id="452d5-294">1</span></span>
| <span data-ttu-id="452d5-295">view</span><span class="sxs-lookup"><span data-stu-id="452d5-295">view</span></span> | <span data-ttu-id="452d5-296">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="452d5-296">1, 2, 3</span></span>
| <span data-ttu-id="452d5-297">walking</span><span class="sxs-lookup"><span data-stu-id="452d5-297">walking</span></span> | <span data-ttu-id="452d5-298">1</span><span class="sxs-lookup"><span data-stu-id="452d5-298">1</span></span>
| <span data-ttu-id="452d5-299">на</span><span class="sxs-lookup"><span data-stu-id="452d5-299">with</span></span> | <span data-ttu-id="452d5-300">3</span><span class="sxs-lookup"><span data-stu-id="452d5-300">3</span></span>


<span data-ttu-id="452d5-301">**Соответствие терминов запроса индексированным терминам**</span><span class="sxs-lookup"><span data-stu-id="452d5-301">**Matching query terms against indexed terms**</span></span>

<span data-ttu-id="452d5-302">Имея hello инвертированный индексов выше, давайте вернуться toohello образец запроса и увидеть, как соответствующих документов находятся в этом примере.</span><span class="sxs-lookup"><span data-stu-id="452d5-302">Given hello inverted indices above, let’s return toohello sample query and see how matching documents are found for our example query.</span></span> <span data-ttu-id="452d5-303">Помните, что это дерево hello окончательный запрос выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="452d5-303">Recall that hello final query tree looks like this:</span></span> 

 ![Логический запрос с терминами после анализа][4]

<span data-ttu-id="452d5-305">Во время выполнения запроса отдельные запросы выполняются для поля поиска hello независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="452d5-305">During query execution, individual queries are executed against hello searchable fields independently.</span></span> 

+ <span data-ttu-id="452d5-306">Hello TermQuery «снижает» соответствует документам 1 (гостиницы Atman).</span><span class="sxs-lookup"><span data-stu-id="452d5-306">hello TermQuery, "spacious", matches document 1 (Hotel Atman).</span></span> 

+ <span data-ttu-id="452d5-307">Hello PrefixQuery, «air-condition *», не соответствует все документы.</span><span class="sxs-lookup"><span data-stu-id="452d5-307">hello PrefixQuery, "air-condition*", doesn't match any documents.</span></span> 

  <span data-ttu-id="452d5-308">Именно такие случаи и запутывают разработчиков.</span><span class="sxs-lookup"><span data-stu-id="452d5-308">This is a behavior that sometimes confuses developers.</span></span> <span data-ttu-id="452d5-309">Несмотря на то, что термин hello помещении с существует в документе hello, она разбивается на два слова анализатором по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-309">Although hello term air-conditioned exists in hello document, it is split into two terms by hello default analyzer.</span></span> <span data-ttu-id="452d5-310">Вспомним, что запросы префикса, содержащие частичные термины, анализу не подлежат.</span><span class="sxs-lookup"><span data-stu-id="452d5-310">Recall that prefix queries, which contain partial terms, are not analyzed.</span></span> <span data-ttu-id="452d5-311">Поэтому условия с префиксом «air-condition» ищутся в hello инвертированный индекс и не найден.</span><span class="sxs-lookup"><span data-stu-id="452d5-311">Therefore terms with prefix "air-condition" are looked up in hello inverted index and not found.</span></span>

+ <span data-ttu-id="452d5-312">Hello PhraseQuery «Аквамарин view», находит hello термины «Аквамарин» и «представление» и проверяет близости hello терминов в исходном документе hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-312">hello PhraseQuery, "ocean view", looks up hello terms "ocean" and "view" and checks hello proximity of terms in hello original document.</span></span> <span data-ttu-id="452d5-313">Документы, 1, 2 и 3 соответствует этот запрос в поле описания hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-313">Documents 1, 2 and 3 match this query in hello description field.</span></span> <span data-ttu-id="452d5-314">Обратите внимание документ 4 имеет Аквамарин термин hello в заголовок hello, но не рассматриваются как совпадающие, как мы ищем hello фразу «Аквамарин view», а не отдельные слова.</span><span class="sxs-lookup"><span data-stu-id="452d5-314">Notice document 4 has hello term ocean in hello title but isn’t considered a match, as we're looking for hello "ocean view" phrase rather than individual words.</span></span> 

> [!Note]
> <span data-ttu-id="452d5-315">Запрос поиска выполняется независимо друг от друга для всех полей для поиска в индекс поиска Azure, если не ограничить набор с hello поля hello hello `searchFields` параметра, как показано в hello пример поискового запроса.</span><span class="sxs-lookup"><span data-stu-id="452d5-315">A search query is executed independently against all searchable fields in hello Azure Search index unless you limit hello fields set with hello `searchFields` parameter, as illustrated in hello example search request.</span></span> <span data-ttu-id="452d5-316">Документы, соответствующие условиям hello выбранных полей возвращаются.</span><span class="sxs-lookup"><span data-stu-id="452d5-316">Documents that match in any of hello selected fields are returned.</span></span> 

<span data-ttu-id="452d5-317">На всей для рассматриваемого запроса hello hello hello документов, которые соответствуют не 1, 2, 3.</span><span class="sxs-lookup"><span data-stu-id="452d5-317">On hello whole, for hello query in question, hello documents that match are 1, 2, 3.</span></span> 

## <a name="stage-4-scoring"></a><span data-ttu-id="452d5-318">Этап 4. Оценка</span><span class="sxs-lookup"><span data-stu-id="452d5-318">Stage 4: Scoring</span></span>  

<span data-ttu-id="452d5-319">Каждому документу в результирующем наборе поиска присваивается оценка релевантности.</span><span class="sxs-lookup"><span data-stu-id="452d5-319">Every document in a search result set is assigned a relevance score.</span></span> <span data-ttu-id="452d5-320">функция Hello оценку значимости hello — toorank более поздней версии, эти документы, которые лучше всего ответить пользователь вопрос по hello поискового запроса.</span><span class="sxs-lookup"><span data-stu-id="452d5-320">hello function of hello relevance score is toorank higher those documents that best answer a user question as expressed by hello search query.</span></span> <span data-ttu-id="452d5-321">Оценка Hello вычисляется на основе статистических свойств, соответствующих условий.</span><span class="sxs-lookup"><span data-stu-id="452d5-321">hello score is computed based on statistical properties of terms that matched.</span></span> <span data-ttu-id="452d5-322">Является основой для оценки формула hello hello [(частота термина обратная частота документа) TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span><span class="sxs-lookup"><span data-stu-id="452d5-322">At hello core of hello scoring formula is [TF/IDF (term frequency-inverse document frequency)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span></span> <span data-ttu-id="452d5-323">В запросах, содержащий редко и общие термины TF-IDF способствует результаты, содержащие термин редких hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-323">In queries containing rare and common terms, TF/IDF promotes results containing hello rare term.</span></span> <span data-ttu-id="452d5-324">Например, в гипотетический индекс со всех статей Википедии, из документы запроса сопоставленная hello *президент hello*, документов, соответствующих на *президент* считаются важнее документы, соответствующие на **.</span><span class="sxs-lookup"><span data-stu-id="452d5-324">For example, in a hypothetical index with all Wikipedia articles, from documents that matched hello query *hello president*, documents matching on *president* are considered more relevant than documents matching on *the*.</span></span>


### <a name="scoring-example"></a><span data-ttu-id="452d5-325">Пример оценки</span><span class="sxs-lookup"><span data-stu-id="452d5-325">Scoring example</span></span>

<span data-ttu-id="452d5-326">Отзыв hello три документы, соответствующие наш пример запроса:</span><span class="sxs-lookup"><span data-stu-id="452d5-326">Recall hello three documents that matched our example query:</span></span>
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

<span data-ttu-id="452d5-327">Лучше всего документа 1 сопоставленная hello запроса, так как оба hello термин *снижает* и необходимые фразы hello *Океан* происходят в поле описания hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-327">Document 1 matched hello query best because both hello term *spacious* and hello required phrase *ocean view* occur in hello description field.</span></span> <span data-ttu-id="452d5-328">следующие два документов Hello соответствует только hello фразу *Океан*.</span><span class="sxs-lookup"><span data-stu-id="452d5-328">hello next two documents match only hello phrase *ocean view*.</span></span> <span data-ttu-id="452d5-329">Он может неожиданным этот показатель релевантности hello для документа, 2 и 3 отличается, несмотря на то, что они сопоставлены запроса hello в hello таким же образом.</span><span class="sxs-lookup"><span data-stu-id="452d5-329">It might be surprising that hello relevance score for document 2 and 3 is different even though they matched hello query in hello same way.</span></span> <span data-ttu-id="452d5-330">Это так, как hello оценки формула имеет несколько компонентов, чем просто TF-IDF-ФАЙЛ.</span><span class="sxs-lookup"><span data-stu-id="452d5-330">It's because hello scoring formula has more components than just TF/IDF.</span></span> <span data-ttu-id="452d5-331">В этом случае документу 3 была присвоена оценка выше, так как его описание короче.</span><span class="sxs-lookup"><span data-stu-id="452d5-331">In this case, document 3 was assigned a slightly higher score because its description is shorter.</span></span> <span data-ttu-id="452d5-332">Дополнительные сведения о [Lucene практические формулы оценки](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand, как длина поля и другие факторы могут повлиять на hello оценку значимости.</span><span class="sxs-lookup"><span data-stu-id="452d5-332">Learn about [Lucene's Practical Scoring Formula](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand how field length and other factors can influence hello relevance score.</span></span>

<span data-ttu-id="452d5-333">Некоторые запроса типов (подстановочный знак, префикс, регулярное выражение) всегда влияют на оценку константой toohello общий документ оценки.</span><span class="sxs-lookup"><span data-stu-id="452d5-333">Some query types (wildcard, prefix, regex) always contribute a constant score toohello overall document score.</span></span> <span data-ttu-id="452d5-334">Это позволяет совпадений, найденных с помощью toobe расширения запроса включены в результаты hello, но без влияния на ранжирование hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-334">This allows matches found through query expansion toobe included in hello results, but without affecting hello ranking.</span></span> 

<span data-ttu-id="452d5-335">В примере объясняется, почему это важно.</span><span class="sxs-lookup"><span data-stu-id="452d5-335">An example illustrates why this matters.</span></span> <span data-ttu-id="452d5-336">Поиск с подстановочными знаками, включая поиск префиксных форм являются неоднозначным по определению, поскольку ввода hello частичную строку с возможных совпадений на очень большое количество различных условий (рассмотрите возможность ввода «Обзор *», с совпадений, обнаруженных на «учебники», «tourettes», и « tourmaline»).</span><span class="sxs-lookup"><span data-stu-id="452d5-336">Wildcard searches, including prefix searches, are ambiguous by definition because hello input is a partial string with potential matches on a very large number of disparate terms (consider an input of "tour*", with matches found on “tours”, “tourettes”, and “tourmaline”).</span></span> <span data-ttu-id="452d5-337">Условии hello характера эти результаты, нет способа определить tooreasonably какие из терминов являются более полезна, чем другие.</span><span class="sxs-lookup"><span data-stu-id="452d5-337">Given hello nature of these results, there is no way tooreasonably infer which terms are more valuable than others.</span></span> <span data-ttu-id="452d5-338">Именно поэтому при оценке результатов в запросах с подстановочными знаками, префиксами и регулярными выражениями стоит игнорировать частоту встречаемости термина.</span><span class="sxs-lookup"><span data-stu-id="452d5-338">For this reason, we ignore term frequencies when scoring results in queries of types wildcard, prefix and regex.</span></span> <span data-ttu-id="452d5-339">В составной поискового запроса, включающий условия частичных или полных результатов из частичного ввода hello были включены с константой оценки tooavoid смещения в сторону может привести к непредвиденным совпадений.</span><span class="sxs-lookup"><span data-stu-id="452d5-339">In a multi-part search request that includes partial and complete terms, results from hello partial input are incorporated with a constant score tooavoid bias towards potentially unexpected matches.</span></span>

### <a name="score-tuning"></a><span data-ttu-id="452d5-340">Настройка оценки</span><span class="sxs-lookup"><span data-stu-id="452d5-340">Score tuning</span></span>

<span data-ttu-id="452d5-341">Существует два способа tootune релевантности в поиске Azure:</span><span class="sxs-lookup"><span data-stu-id="452d5-341">There are two ways tootune relevance scores in Azure Search:</span></span>

1. <span data-ttu-id="452d5-342">**Профили оценки** promote документы в списке hello отсортированных результатов на основе набора правил.</span><span class="sxs-lookup"><span data-stu-id="452d5-342">**Scoring profiles** promote documents in hello ranked list of results based on a set of rules.</span></span> <span data-ttu-id="452d5-343">В нашем примере мы рассмотреть документов, в поле "Название" hello важнее документов, в поле описания hello соответствия соответствия.</span><span class="sxs-lookup"><span data-stu-id="452d5-343">In our example, we could consider documents that matched in hello title field more relevant than documents that matched in hello description field.</span></span> <span data-ttu-id="452d5-344">Кроме того, если бы для индекса было задано поле цены для каждого отеля, мы могли бы повысить позиции документов с более низкой стоимостью.</span><span class="sxs-lookup"><span data-stu-id="452d5-344">Additionally, if our index had a price field for each hotel, we could promote documents with lower price.</span></span> <span data-ttu-id="452d5-345">Дополнительные сведения как слишком[добавить индекс поиска tooa профилей оценки.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span><span class="sxs-lookup"><span data-stu-id="452d5-345">Learn more how too[add Scoring Profiles tooa search index.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span></span>
2. <span data-ttu-id="452d5-346">**Терминов подъема** (доступно только в синтаксисе запроса hello полного Lucene) предоставляет подъема оператор `^` , может быть применен tooany частью дерева запроса hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-346">**Term boosting** (available only in hello Full Lucene query syntax) provides a boosting operator `^` that can be applied tooany part of hello query tree.</span></span> <span data-ttu-id="452d5-347">В нашем примере вместо поиска по префиксу hello *air-condition*\*, один выполнить поиск точного указания термина либо hello *air-condition* hello префикс, но документы, которые соответствуют hello точное Термин более высоким рангом, применяя boost toohello термин запроса: *воздух условие ^ 2 || AIR-Condition**.</span><span class="sxs-lookup"><span data-stu-id="452d5-347">In our example, instead of searching on hello prefix *air-condition*\*, one could search for either hello exact term *air-condition* or hello prefix, but documents that match on hello exact term are ranked higher by applying boost toohello term query: *air-condition^2||air-condition**.</span></span> <span data-ttu-id="452d5-348">Дополнительные сведения см. в разделе о [повышении приоритета слов](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span><span class="sxs-lookup"><span data-stu-id="452d5-348">Learn more about [term boosting](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span></span>


### <a name="scoring-in-a-distributed-index"></a><span data-ttu-id="452d5-349">Оценка в распределенном индексе</span><span class="sxs-lookup"><span data-stu-id="452d5-349">Scoring in a distributed index</span></span>

<span data-ttu-id="452d5-350">Все индексы в поиске Azure, автоматически разбить на несколько сегментов, позволяет нам tooquickly распространение индекса hello между несколькими узлами во время масштабирования службы вверх или уменьшения масштаба.</span><span class="sxs-lookup"><span data-stu-id="452d5-350">All indexes in Azure Search are automatically split into multiple shards, allowing us tooquickly distribute hello index among multiple nodes during service scale up or scale down.</span></span> <span data-ttu-id="452d5-351">Когда инициирован поисковый запрос, он выполняется отдельно для каждого сегмента.</span><span class="sxs-lookup"><span data-stu-id="452d5-351">When a search request is issued, it’s issued against each shard independently.</span></span> <span data-ttu-id="452d5-352">Hello результаты из каждого сегмента затем объединяется и упорядочены по оценке (если другие порядок не определяется).</span><span class="sxs-lookup"><span data-stu-id="452d5-352">hello results from each shard are then merged and ordered by score (if no other ordering is defined).</span></span> <span data-ttu-id="452d5-353">Это важные tooknow, hello не по всем сегментам оценки функция весовые коэффициенты запроса частоты от его частота обратный документа в всех документов в сегмент hello!</span><span class="sxs-lookup"><span data-stu-id="452d5-353">It is important tooknow that hello scoring function weights query term frequency against its inverse document frequency in all documents within hello shard, not across all shards!</span></span>

<span data-ttu-id="452d5-354">Это значит, что оценка релевантности *может* отличаться для идентичных документов, если они находятся в разных сегментах.</span><span class="sxs-lookup"><span data-stu-id="452d5-354">This means a relevance score *could* be different for identical documents if they reside on different shards.</span></span> <span data-ttu-id="452d5-355">К счастью достигнутое обычно toodisappear по мере роста hello число документов в индексе hello из-за распространения toomore даже термин.</span><span class="sxs-lookup"><span data-stu-id="452d5-355">Fortunately, such differences tend toodisappear as hello number of documents in hello index grows due toomore even term distribution.</span></span> <span data-ttu-id="452d5-356">Это не возможные tooassume на какого сегмента будут располагаться любое данного документа.</span><span class="sxs-lookup"><span data-stu-id="452d5-356">It’s not possible tooassume on which shard any given document will be placed.</span></span> <span data-ttu-id="452d5-357">Тем не менее, при условии, что ключ документа не изменяется, она будет всегда соответствовать toohello же сегментов.</span><span class="sxs-lookup"><span data-stu-id="452d5-357">However, assuming a document key doesn't change, it will always be assigned toohello same shard.</span></span>

<span data-ttu-id="452d5-358">В общем случае оценке документа не лучший hello атрибут сортировки документов, если важен порядок стабильности.</span><span class="sxs-lookup"><span data-stu-id="452d5-358">In general, document score is not hello best attribute for ordering documents if order stability is important.</span></span> <span data-ttu-id="452d5-359">Например, имея два документа с одинаковой оценкой, нет гарантии, какой из них отображается первым в последующих запусках hello того же запроса.</span><span class="sxs-lookup"><span data-stu-id="452d5-359">For example, given two document with an identical score, there is no guarantee which one appears first in subsequent runs of hello same query.</span></span> <span data-ttu-id="452d5-360">Оценке документа следует только предоставить общем смысле релевантности документа относительный tooother документов в наборе результатов hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-360">Document score should only give a general sense of document relevance relative tooother documents in hello results set.</span></span>

## <a name="conclusion"></a><span data-ttu-id="452d5-361">Заключение</span><span class="sxs-lookup"><span data-stu-id="452d5-361">Conclusion</span></span>

<span data-ttu-id="452d5-362">Успех Hello средства поиска в Интернете вызвало ожиданий для полнотекстового поиска по личных данных.</span><span class="sxs-lookup"><span data-stu-id="452d5-362">hello success of internet search engines has raised expectations for full text search over private data.</span></span> <span data-ttu-id="452d5-363">Практически для любого типа результатов поиска, теперь ожидается hello engine toounderstand нашей назначение, даже если написаны с ошибками термины или является неполным.</span><span class="sxs-lookup"><span data-stu-id="452d5-363">For almost any kind of search experience, we now expect hello engine toounderstand our intent, even when terms are misspelled or incomplete.</span></span> <span data-ttu-id="452d5-364">Более того, могут даже возвращаться совпадения на основе терминов с приблизительным эквивалентным значением или синонимов, которые не были указаны.</span><span class="sxs-lookup"><span data-stu-id="452d5-364">We might even expect matches based on near equivalent terms or synonyms that we never actually specified.</span></span>

<span data-ttu-id="452d5-365">С технической точки зрения полнотекстовый поиск является очень сложными, требующих сложных лингвистический анализ и систематический подход tooprocessing таким образом, чтобы уточнить, разверните и преобразования toodeliver условия запроса соответствующую.</span><span class="sxs-lookup"><span data-stu-id="452d5-365">From a technical standpoint, full text search is highly complex, requiring sophisticated linguistic analysis and a systematic approach tooprocessing in ways that distill, expand, and transform query terms toodeliver a relevant result.</span></span> <span data-ttu-id="452d5-366">Учитывая специфические сложности hello, существует много факторов, влияющих на результат hello запроса.</span><span class="sxs-lookup"><span data-stu-id="452d5-366">Given hello inherent complexities, there are a lot of factors that can affect hello outcome of a query.</span></span> <span data-ttu-id="452d5-367">По этой причине инвестиции hello время toounderstand hello механизм полнотекстового поиска предлагает очевидные преимущества при попытке toowork через непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="452d5-367">For this reason, investing hello time toounderstand hello mechanics of full text search offers tangible benefits when trying toowork through unexpected results.</span></span>  

<span data-ttu-id="452d5-368">В этой статье использовать полнотекстовый поиск в контексте hello поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="452d5-368">This article explored full text search in hello context of Azure Search.</span></span> <span data-ttu-id="452d5-369">Мы надеемся, что она позволяет достаточно фона toorecognize возможные причины и способы их устранения по устранению общих проблем запроса.</span><span class="sxs-lookup"><span data-stu-id="452d5-369">We hope it gives you sufficient background toorecognize potential causes and resolutions for addressing common query problems.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="452d5-370">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="452d5-370">Next steps</span></span>

+ <span data-ttu-id="452d5-371">Создание индекса образец hello, пробное использование различных запросов и просмотрите результаты.</span><span class="sxs-lookup"><span data-stu-id="452d5-371">Build hello sample index, try out different queries and review results.</span></span> <span data-ttu-id="452d5-372">Инструкции см. в разделе [сборки и запроса индекса в портале hello](search-get-started-portal.md#query-index).</span><span class="sxs-lookup"><span data-stu-id="452d5-372">For instructions, see [Build and query an index in hello portal](search-get-started-portal.md#query-index).</span></span>

+ <span data-ttu-id="452d5-373">Повторите дополнительного синтаксиса hello [поиск документов](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) разделе "Пример" или из [синтаксис простого запроса](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) в обозреватель поиска в портале hello.</span><span class="sxs-lookup"><span data-stu-id="452d5-373">Try additional query syntax from hello [Search Documents](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) example section or from [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Search explorer in hello portal.</span></span>

+ <span data-ttu-id="452d5-374">Просмотрите [профилей оценки](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) Если tootune ранжирования в приложении поиска.</span><span class="sxs-lookup"><span data-stu-id="452d5-374">Review [scoring profiles](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) if you want tootune ranking in your search application.</span></span>

+ <span data-ttu-id="452d5-375">Узнайте, как tooapply [лексические анализаторы языка](https://docs.microsoft.com/rest/api/searchservice/language-support).</span><span class="sxs-lookup"><span data-stu-id="452d5-375">Learn how tooapply [language-specific lexical analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support).</span></span>

+ <span data-ttu-id="452d5-376">[Настройте пользовательские анализаторы](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) для минимальной или специализированной обработки определенных полей.</span><span class="sxs-lookup"><span data-stu-id="452d5-376">[Configure custom analyzers](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) for either minimal processing or specialized processing on specific fields.</span></span>

+ <span data-ttu-id="452d5-377">[Параллельно сравните стандартный анализатор и анализатор английского языка](http://alice.unearth.ai/) на этом демонстрационном веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="452d5-377">[Compare standard and English analyzers](http://alice.unearth.ai/)) side-by-side on this demo web site.</span></span> 

## <a name="see-also"></a><span data-ttu-id="452d5-378">См. также</span><span class="sxs-lookup"><span data-stu-id="452d5-378">See also</span></span>

<span data-ttu-id="452d5-379">[Search Documents (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/search-documents) (Поиск по документам (REST API службы поиска Azure))</span><span class="sxs-lookup"><span data-stu-id="452d5-379">[Search Documents REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents)</span></span>

[<span data-ttu-id="452d5-380">Простой синтаксис запросов</span><span class="sxs-lookup"><span data-stu-id="452d5-380">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

<span data-ttu-id="452d5-381">[Lucene query syntax in Azure Search](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (Синтаксис запросов Lucene в службе поиска Azure)</span><span class="sxs-lookup"><span data-stu-id="452d5-381">[Full Lucene query syntax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span></span>

[<span data-ttu-id="452d5-382">Обработка результатов поиска</span><span class="sxs-lookup"><span data-stu-id="452d5-382">Handle search results</span></span>](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
