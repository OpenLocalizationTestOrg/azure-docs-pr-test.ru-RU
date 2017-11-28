---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Предварительная документация для функции hello синонимы (Предварительная версия), отображаемые в hello REST API поиска Azure."
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
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="4a7c1-102">Synonyms в Поиске Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="4a7c1-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="4a7c1-103">Синонимы в поисковых системах связать эквивалентные термины, которые неявно расширить область hello запроса, без необходимости предоставить термин hello tooactually пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-103">Synonyms in search engines associate equivalent terms that implicitly expand hello scope of a query, without hello user having tooactually provide hello term.</span></span> <span data-ttu-id="4a7c1-104">Например заданного hello термин «dog» и взаимосвязи синонимов «овчарка» и «малышку в продажу», документы, содержащие «dog», «овчарка» или «малышку в продажу» будет попадают в области hello hello запроса.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-104">For example, given hello term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within hello scope of hello query.</span></span>

<span data-ttu-id="4a7c1-105">В Поиске Azure добавление синонимов выполняется во время обработки запроса.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="4a7c1-106">Вы можете добавить синоним maps tooa службы с операциями tooexisting без перебоев в работе.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-106">You can add synonym maps tooa service with no disruption tooexisting operations.</span></span> <span data-ttu-id="4a7c1-107">Можно добавить **synonymMaps** определение поля tooa свойства без необходимости toorebuild hello индекса.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-107">You can add a  **synonymMaps** property tooa field definition without having toorebuild hello index.</span></span> <span data-ttu-id="4a7c1-108">Дополнительные сведения см. в статье [Update Index (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/update-index) (Обновление индекса (REST API службы Поиска Azure)).</span><span class="sxs-lookup"><span data-stu-id="4a7c1-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="4a7c1-109">Доступность функций</span><span class="sxs-lookup"><span data-stu-id="4a7c1-109">Feature availability</span></span>

<span data-ttu-id="4a7c1-110">синонимы Hello компонент в настоящий момент в Предварительный просмотр и поддерживается в только hello последнюю версию api предварительной версии (api-version = 2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="4a7c1-110">hello synonyms feature is currently in preview and only supported in hello latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="4a7c1-111">Портал Azure такую поддержку пока не предоставляет.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="4a7c1-112">Поскольку при запросе hello указана версия hello API, он является возможные toocombine общедоступной (GA) и API предварительной версии в hello то же приложение.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-112">Because hello API version is specified on hello request, it's possible toocombine generally available (GA) and preview APIs in hello same app.</span></span> <span data-ttu-id="4a7c1-113">Тем не менее предварительные версии API не регулируются соглашением об уровне обслуживания, и их возможности могут измениться, поэтому мы не рекомендуем использовать их в рабочих приложениях.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-toouse-synonyms-in-azure-search"></a><span data-ttu-id="4a7c1-114">Как поиск toouse синонимы в Azure</span><span class="sxs-lookup"><span data-stu-id="4a7c1-114">How toouse synonyms in Azure search</span></span>

<span data-ttu-id="4a7c1-115">В поиске Azure поддержка синонимов основан на синоним maps определение и tooyour служба отправки.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-115">In Azure Search, synonym support is based on synonym maps that you define and upload tooyour service.</span></span> <span data-ttu-id="4a7c1-116">Эти карты представляют собой независимый ресурс (как индексы или источники данных) и могут использоваться любым полем, поддерживающим поиск, в любом индекс в службе поиска.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="4a7c1-117">Карты синонимов и индексы обслуживаются независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="4a7c1-118">После определения схемы синонима и tooyour служба отправки функции hello синоним для поля можно включить, добавив новое свойство с именем **synonymMaps** в определение поля hello.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-118">Once you define a synonym map and upload it tooyour service, you can enable hello synonym feature on a field by adding a new property called **synonymMaps** in hello field definition.</span></span> <span data-ttu-id="4a7c1-119">Создание, обновление и удаление карты синоним всегда равно операции целого документа, это означает, что нельзя создать, обновить или удалять части карты синоним hello постепенно.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of hello synonym map incrementally.</span></span> <span data-ttu-id="4a7c1-120">Для обновления даже одной записи требуется перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="4a7c1-121">Внедрение синонимов в приложение поиска состоит из двух этапов:</span><span class="sxs-lookup"><span data-stu-id="4a7c1-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="4a7c1-122">Добавление службы поиска tooyour синоним карты через API-интерфейсы ниже hello.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-122">Add a synonym map tooyour search service through hello APIs below.</span></span>  

2.  <span data-ttu-id="4a7c1-123">Настройка соответствия синоним hello toouse для поиска полей в определение индекса hello.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-123">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="4a7c1-124">Интерфейсы API ресурсов SynonymMaps</span><span class="sxs-lookup"><span data-stu-id="4a7c1-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="4a7c1-125">Добавить или обновить кату синонимов в службе можно с помощью запроса POST или PUT.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="4a7c1-126">Синоним maps передаются службе toohello с помощью POST или PUT.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-126">Synonym maps are uploaded toohello service via POST or PUT.</span></span> <span data-ttu-id="4a7c1-127">Каждое правило должны быть разделены hello символ новой строки («\n»).</span><span class="sxs-lookup"><span data-stu-id="4a7c1-127">Each rule must be delimited by hello new line character ('\n').</span></span> <span data-ttu-id="4a7c1-128">Можно определить too5, 000 правил для каждой карты синонима в бесплатной службы и 10 000 правил во всех SKU.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-128">You can define up too5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="4a7c1-129">Каждое правило может находиться до too20 расширения.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-129">Each rule can have up too20 expansions.</span></span>

<span data-ttu-id="4a7c1-130">В этой предварительной версии maps синоним должен быть в формате hello Apache Solr, который описывается ниже.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-130">In this preview, synonym maps must be in hello Apache Solr format which is explained below.</span></span> <span data-ttu-id="4a7c1-131">Если существующий словарь синонима в другом формате и хотите toouse ее напрямую, сообщите нам об этом на [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="4a7c1-131">If you have an existing synonym dictionary in a different format and want toouse it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="4a7c1-132">Можно создать новую карту синоним, с помощью HTTP POST, как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-132">You can create a new synonym map using HTTP POST, as in hello following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="4a7c1-133">Кроме того можно использовать PUT и указать имя синонима hello на hello URI.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-133">Alternatively, you can use PUT and specify hello synonym map name on hello URI.</span></span> <span data-ttu-id="4a7c1-134">Если карта синоним hello не существует, он будет создан.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-134">If hello synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="4a7c1-135">Формат синонимов Apache Solr</span><span class="sxs-lookup"><span data-stu-id="4a7c1-135">Apache Solr synonym format</span></span>

<span data-ttu-id="4a7c1-136">Формат Solr Hello поддерживает синоним эквивалентны, явные сопоставления.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-136">hello Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="4a7c1-137">Правила сопоставления придерживаться открытой toohello синоним спецификацию фильтра Solr Apache, описанные в этом документе: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="4a7c1-137">Mapping rules adhere toohello open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="4a7c1-138">Ниже приведен пример правила для эквивалентных синонимов.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="4a7c1-139">С правилом hello выше, запрос поиска «США» будет расширяться слишком «США» или «Соединенные Штаты» или «США».</span><span class="sxs-lookup"><span data-stu-id="4a7c1-139">With hello rule above, a search query "USA" will expand too"USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="4a7c1-140">Явное сопоставление обозначается стрелкой "=>".</span><span class="sxs-lookup"><span data-stu-id="4a7c1-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="4a7c1-141">При указании последовательность термин поискового запроса, который соответствует hello левой части «= >» будет заменена альтернативы hello hello правой стороны.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-141">When specified, a term sequence of a search query that matches hello left hand side of "=>" will be replaced with hello alternatives on hello right hand side.</span></span> <span data-ttu-id="4a7c1-142">Имея hello снизу, поисковые запросы «Вашингтон», «Штат Вашингтон.»</span><span class="sxs-lookup"><span data-stu-id="4a7c1-142">Given hello rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="4a7c1-143">или «WA» будет все переписать слишком «WA».</span><span class="sxs-lookup"><span data-stu-id="4a7c1-143">or "WA" will all be rewritten too"WA".</span></span> <span data-ttu-id="4a7c1-144">Явное сопоставление только применяется в указанном направлении hello и не перезаписывает hello запроса «WA» слишком «Вашингтон», в данном случае.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-144">Explicit mapping only applies in hello direction specified and does not rewrite hello query "WA" too"Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="4a7c1-145">Вывод карт синонимов в службе.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="4a7c1-146">Получение карты синонимов в службе.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="4a7c1-147">Удаление карты синонимов в службе.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a><span data-ttu-id="4a7c1-148">Настройка соответствия синоним hello toouse для поиска полей в определение индекса hello.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-148">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

<span data-ttu-id="4a7c1-149">Новое свойство поля **synonymMaps** может быть используется toospecify toouse карты синоним для поля с возможностью поиска.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-149">A new field property **synonymMaps** can be used toospecify a synonym map toouse for a searchable field.</span></span> <span data-ttu-id="4a7c1-150">Синоним карты являются ресурсами уровня службы и позволяет ссылаться на любое поле в рамках службы hello индекса.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-150">Synonym maps are service level resources and can be referenced by any field of an index under hello service.</span></span>

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

<span data-ttu-id="4a7c1-151">**synonymMaps** могут быть указаны для поиска полей типа hello «Edm.String» или «Collection(Edm.String)».</span><span class="sxs-lookup"><span data-stu-id="4a7c1-151">**synonymMaps** can be specified for searchable fields of hello type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="4a7c1-152">В этой предварительной версии можно использовать только одну карту синонимов на поле.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="4a7c1-153">Если вы хотите toouse несколько карт синоним, сообщите нам на [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="4a7c1-153">If you want toouse multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="4a7c1-154">Влияние синонимов на другие функции поиска</span><span class="sxs-lookup"><span data-stu-id="4a7c1-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="4a7c1-155">функция синонимы Hello перезаписывает hello исходного запроса с синонимами с hello оператор OR.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-155">hello synonyms feature rewrites hello original query with synonyms with hello OR operator.</span></span> <span data-ttu-id="4a7c1-156">По этой причине попаданий выделение и профили оценки обрабатывают исходный термин hello и синонимы как эквивалентные.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-156">For this reason, hit highlighting and scoring profiles treat hello original term and synonyms as equivalent.</span></span>

<span data-ttu-id="4a7c1-157">Функция синоним применяется toosearch запросы и не применяется toofilters или аспекты.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-157">Synonym feature applies toosearch queries and does not apply toofilters or facets.</span></span> <span data-ttu-id="4a7c1-158">Аналогичным образом предложения основаны только на исходный термин hello; Синоним совпадения не отображаются в ответ hello.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-158">Similarly, suggestions are based only on hello original term; synonym matches do not appear in hello response.</span></span>

<span data-ttu-id="4a7c1-159">Синоним расширения неприменимы условия поиска toowildcard; префикс, Нечеткий и регулярное выражение условия не преобразуются.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-159">Synonym expansions do not apply toowildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="4a7c1-160">Советы по созданию карты синонимов</span><span class="sxs-lookup"><span data-stu-id="4a7c1-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="4a7c1-161">Краткая и хорошо спроектированная карта синонимов намного эффективнее, чем всеобъемлющий список возможных совпадений.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="4a7c1-162">Чрезмерно больших или сложных словари занять больше времени, tooparse и влияет на задержку hello запроса, если запрос hello разворачивается toomany синонимы.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-162">Excessively large or complex dictionaries take longer tooparse and affect hello query latency if hello query expands toomany synonyms.</span></span> <span data-ttu-id="4a7c1-163">Вместо предположения, в котором могут использоваться термины, могут получать фактические условия hello через [поиска отчет об анализе трафика](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="4a7c1-163">Rather than guess at which terms might be used, you can get hello actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="4a7c1-164">В качестве упражнения проверки и предварительно включить и затем использовать этот отчет tooprecisely определить, какие условия будет преимущества соответствие синонима, а затем продолжить toouse его как проверки, что ваша карта синоним зарегистрировавшем лучшие показатели.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-164">As both a preliminary and validation exercise, enable and then use this report tooprecisely determine which terms will benefit from a synonym match, and then continue toouse it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="4a7c1-165">В отчете hello предопределенные hello плитки «наиболее общие запросы поиска» и «запросов нулевой результат поиска» даст hello необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-165">In hello predefined report, hello tiles "Most common search queries" and "Zero-result search queries" will give you hello necessary information.</span></span>

- <span data-ttu-id="4a7c1-166">Можно создать несколько карт синонимов для приложения поиска (например, для разных языков, если приложение поддерживает многоязычную базу клиентов).</span><span class="sxs-lookup"><span data-stu-id="4a7c1-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="4a7c1-167">В настоящее время поле может использовать только одну карту.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="4a7c1-168">Свойство synonymMaps поля можно обновить в любое время.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a7c1-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4a7c1-169">Next Steps</span></span>

- <span data-ttu-id="4a7c1-170">При наличии существующего индекса в среде разработки (нерабочей) Поэкспериментируйте с toosee небольшой словарь как hello Добавление синонимов изменяется hello поисковый интерфейс, включая влияние на профили оценки, попаданий выделение и предложения.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary toosee how hello addition of synonyms changes hello search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="4a7c1-171">[Включить аналитику трафика службы поиска](search-traffic-analytics.md) и hello использование стандартного отчета Power BI, какие термины toolearn hello большинство и какие другие возвращаемого документы.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-171">[Enable search traffic analytics](search-traffic-analytics.md) and use hello predefined Power BI report toolearn which terms are used hello most, and which ones return zero documents.</span></span> <span data-ttu-id="4a7c1-172">Используя эти знания, пересмотрите hello словарь tooinclude синонимы для производительности запросов, которые должны разрешения toodocuments в индексе.</span><span class="sxs-lookup"><span data-stu-id="4a7c1-172">Armed with these insights, revise hello dictionary tooinclude synonyms for unproductive queries that should be resolving toodocuments in your index.</span></span>
