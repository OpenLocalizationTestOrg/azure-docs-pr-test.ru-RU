---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Предварительная документация по компоненту Synonyms (предварительная версия), доступному в REST API Поиска Azure."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 739a0ad77c68ea74ec25bc80c7539ac8b3f18201
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="d42fd-102">Synonyms в Поиске Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="d42fd-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="d42fd-103">Synonyms представляет собой поисковые системы, связывающие эквивалентные термины, которые неявно расширяют область запроса, даже если пользователь не указал их.</span><span class="sxs-lookup"><span data-stu-id="d42fd-103">Synonyms in search engines associate equivalent terms that implicitly expand the scope of a query, without the user having to actually provide the term.</span></span> <span data-ttu-id="d42fd-104">Например, если имеется термин "пес" с синонимами "собака" и "щенок", то документы, содержащие термины "пес", "собака" и "щенок", попадут в область запроса.</span><span class="sxs-lookup"><span data-stu-id="d42fd-104">For example, given the term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within the scope of the query.</span></span>

<span data-ttu-id="d42fd-105">В Поиске Azure добавление синонимов выполняется во время обработки запроса.</span><span class="sxs-lookup"><span data-stu-id="d42fd-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="d42fd-106">Можно добавить карту синонимов в службу, не прерывая текущие операции.</span><span class="sxs-lookup"><span data-stu-id="d42fd-106">You can add synonym maps to a service with no disruption to existing operations.</span></span> <span data-ttu-id="d42fd-107">Можно добавить свойство **synonymMaps** в определение поля, не перестраивая индекс.</span><span class="sxs-lookup"><span data-stu-id="d42fd-107">You can add a  **synonymMaps** property to a field definition without having to rebuild the index.</span></span> <span data-ttu-id="d42fd-108">Дополнительные сведения см. в статье [Update Index (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/update-index) (Обновление индекса (REST API службы Поиска Azure)).</span><span class="sxs-lookup"><span data-stu-id="d42fd-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="d42fd-109">Доступность функций</span><span class="sxs-lookup"><span data-stu-id="d42fd-109">Feature availability</span></span>

<span data-ttu-id="d42fd-110">Сейчас возможности синонимов доступны в предварительной версии и поддерживаются только последней предварительной версией API (api-version=2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="d42fd-110">The synonyms feature is currently in preview and only supported in the latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="d42fd-111">Портал Azure такую поддержку пока не предоставляет.</span><span class="sxs-lookup"><span data-stu-id="d42fd-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="d42fd-112">Так как версия API указывается в запросе, можно совмещать общедоступную и предварительную версии API в одном приложении.</span><span class="sxs-lookup"><span data-stu-id="d42fd-112">Because the API version is specified on the request, it's possible to combine generally available (GA) and preview APIs in the same app.</span></span> <span data-ttu-id="d42fd-113">Тем не менее предварительные версии API не регулируются соглашением об уровне обслуживания, и их возможности могут измениться, поэтому мы не рекомендуем использовать их в рабочих приложениях.</span><span class="sxs-lookup"><span data-stu-id="d42fd-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-to-use-synonyms-in-azure-search"></a><span data-ttu-id="d42fd-114">Как использовать синонимы в Поиске Azure</span><span class="sxs-lookup"><span data-stu-id="d42fd-114">How to use synonyms in Azure search</span></span>

<span data-ttu-id="d42fd-115">В Поиске Azure функция синонимов основана на картах синонимов, определяемых и передаваемых в службу пользователем.</span><span class="sxs-lookup"><span data-stu-id="d42fd-115">In Azure Search, synonym support is based on synonym maps that you define and upload to your service.</span></span> <span data-ttu-id="d42fd-116">Эти карты представляют собой независимый ресурс (как индексы или источники данных) и могут использоваться любым полем, поддерживающим поиск, в любом индекс в службе поиска.</span><span class="sxs-lookup"><span data-stu-id="d42fd-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="d42fd-117">Карты синонимов и индексы обслуживаются независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="d42fd-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="d42fd-118">После определения карты синонимов и ее передачи в службу можно включить функцию синонимов для поля, добавив новое свойство **synonymMaps** в определение этого поля.</span><span class="sxs-lookup"><span data-stu-id="d42fd-118">Once you define a synonym map and upload it to your service, you can enable the synonym feature on a field by adding a new property called **synonymMaps** in the field definition.</span></span> <span data-ttu-id="d42fd-119">Создание, обновление и удаление карты синоним всегда относится ко всему документу. Это означает, что нельзя постепенно создавать, обновлять или удалять части карты синонимов.</span><span class="sxs-lookup"><span data-stu-id="d42fd-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of the synonym map incrementally.</span></span> <span data-ttu-id="d42fd-120">Для обновления даже одной записи требуется перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="d42fd-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="d42fd-121">Внедрение синонимов в приложение поиска состоит из двух этапов:</span><span class="sxs-lookup"><span data-stu-id="d42fd-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="d42fd-122">Добавление карты синонимов в службу поиска с помощью интерфейсов API, приведенных ниже.</span><span class="sxs-lookup"><span data-stu-id="d42fd-122">Add a synonym map to your search service through the APIs below.</span></span>  

2.  <span data-ttu-id="d42fd-123">Настройка поля, поддерживающего поиск, для использования карты синонимов в определении индекса.</span><span class="sxs-lookup"><span data-stu-id="d42fd-123">Configure a searchable field to use the synonym map in the index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="d42fd-124">Интерфейсы API ресурсов SynonymMaps</span><span class="sxs-lookup"><span data-stu-id="d42fd-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="d42fd-125">Добавить или обновить кату синонимов в службе можно с помощью запроса POST или PUT.</span><span class="sxs-lookup"><span data-stu-id="d42fd-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="d42fd-126">Для передачи карты синонимов в службу используется запрос POST или PUT.</span><span class="sxs-lookup"><span data-stu-id="d42fd-126">Synonym maps are uploaded to the service via POST or PUT.</span></span> <span data-ttu-id="d42fd-127">Правила должны быть разделены символами новой строки (\n).</span><span class="sxs-lookup"><span data-stu-id="d42fd-127">Each rule must be delimited by the new line character ('\n').</span></span> <span data-ttu-id="d42fd-128">Можно определить до 5000 правил на карту синонимов в службе уровня "Бесплатный" и до 10 000 правил для всех прочих номеров SKU.</span><span class="sxs-lookup"><span data-stu-id="d42fd-128">You can define up to 5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="d42fd-129">Каждое правило может содержать до 20 расширений.</span><span class="sxs-lookup"><span data-stu-id="d42fd-129">Each rule can have up to 20 expansions.</span></span>

<span data-ttu-id="d42fd-130">В этой предварительной версии должны использоваться карты синонимов в формате Apache Solr, который описан ниже.</span><span class="sxs-lookup"><span data-stu-id="d42fd-130">In this preview, synonym maps must be in the Apache Solr format which is explained below.</span></span> <span data-ttu-id="d42fd-131">Если у вас есть словарь синонимов в другом формате и вы хотите использовать его напрямую, сообщите нам об этом с помощью [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="d42fd-131">If you have an existing synonym dictionary in a different format and want to use it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="d42fd-132">Карту синонимов можно создать с помощью запроса HTTP POST, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="d42fd-132">You can create a new synonym map using HTTP POST, as in the following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="d42fd-133">Кроме того, можно использовать запрос PUT и указать имя карты синонимов в универсальном коде ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="d42fd-133">Alternatively, you can use PUT and specify the synonym map name on the URI.</span></span> <span data-ttu-id="d42fd-134">Если такой карты синонимов не существует, она будет создана.</span><span class="sxs-lookup"><span data-stu-id="d42fd-134">If the synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="d42fd-135">Формат синонимов Apache Solr</span><span class="sxs-lookup"><span data-stu-id="d42fd-135">Apache Solr synonym format</span></span>

<span data-ttu-id="d42fd-136">Формат Solr поддерживает эквивалентные и явные сопоставления синонимов.</span><span class="sxs-lookup"><span data-stu-id="d42fd-136">The Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="d42fd-137">Правила сопоставления соответствуют спецификации фильтра синонимов с открытым кодом Apache Solr, описанной в этом документе: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="d42fd-137">Mapping rules adhere to the open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="d42fd-138">Ниже приведен пример правила для эквивалентных синонимов.</span><span class="sxs-lookup"><span data-stu-id="d42fd-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="d42fd-139">При использовании этого правила поисковый запрос "США" будет расширен до следующего запроса: "США" ИЛИ "Соединенные Штаты" ИЛИ "Соединенные Штаты Америки".</span><span class="sxs-lookup"><span data-stu-id="d42fd-139">With the rule above, a search query "USA" will expand to "USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="d42fd-140">Явное сопоставление обозначается стрелкой "=>".</span><span class="sxs-lookup"><span data-stu-id="d42fd-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="d42fd-141">При указании такого сопоставления последовательность терминов поискового запроса, которая соответствует левой части сопоставления "=>", будет заменена альтернативными вариантами из правой части.</span><span class="sxs-lookup"><span data-stu-id="d42fd-141">When specified, a term sequence of a search query that matches the left hand side of "=>" will be replaced with the alternatives on the right hand side.</span></span> <span data-ttu-id="d42fd-142">Согласно приведенному ниже правилу, поисковые запросы "Санкт-Петербург", "Питер"</span><span class="sxs-lookup"><span data-stu-id="d42fd-142">Given the rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="d42fd-143">или "СПБ" будут перезаписаны запросом "СПБ".</span><span class="sxs-lookup"><span data-stu-id="d42fd-143">or "WA" will all be rewritten to "WA".</span></span> <span data-ttu-id="d42fd-144">Явное сопоставление применяется только в указанном направлении, и в этом случае запрос "СПБ" не будет перезаписан запросом "Санкт-Петербург".</span><span class="sxs-lookup"><span data-stu-id="d42fd-144">Explicit mapping only applies in the direction specified and does not rewrite the query "WA" to "Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="d42fd-145">Вывод карт синонимов в службе.</span><span class="sxs-lookup"><span data-stu-id="d42fd-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="d42fd-146">Получение карты синонимов в службе.</span><span class="sxs-lookup"><span data-stu-id="d42fd-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="d42fd-147">Удаление карты синонимов в службе.</span><span class="sxs-lookup"><span data-stu-id="d42fd-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-to-use-the-synonym-map-in-the-index-definition"></a><span data-ttu-id="d42fd-148">Настройка поля, поддерживающего поиск, для использования карты синонимов в определении индекса.</span><span class="sxs-lookup"><span data-stu-id="d42fd-148">Configure a searchable field to use the synonym map in the index definition.</span></span>

<span data-ttu-id="d42fd-149">Новое свойство поля **synonymMaps** можно использовать для указания карты синонимов для поля, поддерживающего поиск.</span><span class="sxs-lookup"><span data-stu-id="d42fd-149">A new field property **synonymMaps** can be used to specify a synonym map to use for a searchable field.</span></span> <span data-ttu-id="d42fd-150">Карты синонимов — это ресурсы уровня службы, и на них может ссылаться любое поле индекса в службе.</span><span class="sxs-lookup"><span data-stu-id="d42fd-150">Synonym maps are service level resources and can be referenced by any field of an index under the service.</span></span>

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

<span data-ttu-id="d42fd-151">Свойство **synonymMaps** можно указать полей, поддерживающих поиск, типа Edm.String или Collection(Edm.String).</span><span class="sxs-lookup"><span data-stu-id="d42fd-151">**synonymMaps** can be specified for searchable fields of the type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="d42fd-152">В этой предварительной версии можно использовать только одну карту синонимов на поле.</span><span class="sxs-lookup"><span data-stu-id="d42fd-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="d42fd-153">Если вы хотите использовать несколько карт синонимов, сообщите нам об этом с помощью [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="d42fd-153">If you want to use multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="d42fd-154">Влияние синонимов на другие функции поиска</span><span class="sxs-lookup"><span data-stu-id="d42fd-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="d42fd-155">Функция синонимов перезаписывает исходный запрос, добавляя синонимы с оператором ИЛИ.</span><span class="sxs-lookup"><span data-stu-id="d42fd-155">The synonyms feature rewrites the original query with synonyms with the OR operator.</span></span> <span data-ttu-id="d42fd-156">По этой причине функция выделения совпадений и профиль повышения считают исходный термин и его синонимы эквивалентными.</span><span class="sxs-lookup"><span data-stu-id="d42fd-156">For this reason, hit highlighting and scoring profiles treat the original term and synonyms as equivalent.</span></span>

<span data-ttu-id="d42fd-157">Функция синонимов применяется к поисковым запросам и не действует для фильтров и аспектов.</span><span class="sxs-lookup"><span data-stu-id="d42fd-157">Synonym feature applies to search queries and does not apply to filters or facets.</span></span> <span data-ttu-id="d42fd-158">Аналогичным образом, предложения основываются только на исходном термине. Совпадения для синонимов в ответе не отображаются.</span><span class="sxs-lookup"><span data-stu-id="d42fd-158">Similarly, suggestions are based only on the original term; synonym matches do not appear in the response.</span></span>

<span data-ttu-id="d42fd-159">Расширения синонимов не применяются к поисковым терминам с подстановочными знаками. Это также относится к терминам, содержащим префикс, нечеткое условие и регулярное выражение.</span><span class="sxs-lookup"><span data-stu-id="d42fd-159">Synonym expansions do not apply to wildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="d42fd-160">Советы по созданию карты синонимов</span><span class="sxs-lookup"><span data-stu-id="d42fd-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="d42fd-161">Краткая и хорошо спроектированная карта синонимов намного эффективнее, чем всеобъемлющий список возможных совпадений.</span><span class="sxs-lookup"><span data-stu-id="d42fd-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="d42fd-162">Слишком большие или сложные словари увеличивают длительность анализа и задерживают обработку запросов, если в запрос добавляется несколько синонимов.</span><span class="sxs-lookup"><span data-stu-id="d42fd-162">Excessively large or complex dictionaries take longer to parse and affect the query latency if the query expands to many synonyms.</span></span> <span data-ttu-id="d42fd-163">Вместо того, чтобы гадать, какие термины могут использоваться, можно получить фактические термины, воспользовавшись [отчетом об анализе трафика поиска](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="d42fd-163">Rather than guess at which terms might be used, you can get the actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="d42fd-164">В качестве предварительного и проверочного упражнения включите и используйте этот отчет, чтобы точно определять, для каких терминов подходит поиск синонимов, и продолжайте использовать его, чтобы проверять, улучшаются ли результаты карты синонимов.</span><span class="sxs-lookup"><span data-stu-id="d42fd-164">As both a preliminary and validation exercise, enable and then use this report to precisely determine which terms will benefit from a synonym match, and then continue to use it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="d42fd-165">В стандартном отчете элементы "Most common search queries" (Последние поисковые запросы) и "Zero-result search queries" (Поисковые запросы с нулевым результатом) будут содержать необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="d42fd-165">In the predefined report, the tiles "Most common search queries" and "Zero-result search queries" will give you the necessary information.</span></span>

- <span data-ttu-id="d42fd-166">Можно создать несколько карт синонимов для приложения поиска (например, для разных языков, если приложение поддерживает многоязычную базу клиентов).</span><span class="sxs-lookup"><span data-stu-id="d42fd-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="d42fd-167">В настоящее время поле может использовать только одну карту.</span><span class="sxs-lookup"><span data-stu-id="d42fd-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="d42fd-168">Свойство synonymMaps поля можно обновить в любое время.</span><span class="sxs-lookup"><span data-stu-id="d42fd-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d42fd-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d42fd-169">Next Steps</span></span>

- <span data-ttu-id="d42fd-170">Если у вас есть индекс в среде разработки (не в рабочей среде), поэкспериментируйте с небольшим словарем, чтобы узнать, как добавление синонимов изменяет результаты поиска, включая влияние на профили повышения, выделение совпадений и предложения.</span><span class="sxs-lookup"><span data-stu-id="d42fd-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary to see how the addition of synonyms changes the search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="d42fd-171">[Включите аналитику трафика поиска](search-traffic-analytics.md) и используйте стандартный отчет Power BI, чтобы узнать, какие термины указываются чаще всего и какие возвращают ноль документов.</span><span class="sxs-lookup"><span data-stu-id="d42fd-171">[Enable search traffic analytics](search-traffic-analytics.md) and use the predefined Power BI report to learn which terms are used the most, and which ones return zero documents.</span></span> <span data-ttu-id="d42fd-172">Получив эти сведения, отредактируйте словарь, добавив синонимы для неэффективных запросов, которые должны выдавать документы из индекса.</span><span class="sxs-lookup"><span data-stu-id="d42fd-172">Armed with these insights, revise the dictionary to include synonyms for unproductive queries that should be resolving to documents in your index.</span></span>
