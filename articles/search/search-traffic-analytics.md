---
title: "aaaSearch аналитика трафика службы для службы поиска Azure | Документы Microsoft"
description: "Включите аналитику трафика службы поиска для поиска Azure, размещенной облачной службой поиска в Microsoft Azure, toounlock ценной информации о данных и пользователи."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="8fe57-103">Что такое аналитика поискового трафика?</span><span class="sxs-lookup"><span data-stu-id="8fe57-103">What is search traffic analytics</span></span>
<span data-ttu-id="8fe57-104">Аналитика поискового трафика — это модель реализации цикла обратной связи для службы поиска.</span><span class="sxs-lookup"><span data-stu-id="8fe57-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="8fe57-105">Этот шаблон описывает hello необходимые данные и как toocollect его с помощью Application Insights, отраслевым лидером для наблюдения за службами в нескольких платформ.</span><span class="sxs-lookup"><span data-stu-id="8fe57-105">This pattern describes hello necessary data and how toocollect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="8fe57-106">Аналитика поискового трафика позволяет обеспечить видимость службы поиска и получить сведения о пользователях и их поведении.</span><span class="sxs-lookup"><span data-stu-id="8fe57-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="8fe57-107">Когда данные о выберите пользователей, это toomake возможные решения, которые улучшить возможности поиска и tooback off при результаты hello, не ожидаемых.</span><span class="sxs-lookup"><span data-stu-id="8fe57-107">By having data about what your users choose, it's possible toomake decisions that further improve your search experience, and tooback off when hello results are not what expected.</span></span>

<span data-ttu-id="8fe57-108">Поиск Azure предлагает решение телеметрии, объединяющая аналитики приложения Azure и Power BI tooprovide глубокого мониторинга и отслеживания.</span><span class="sxs-lookup"><span data-stu-id="8fe57-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI tooprovide in-depth monitoring and tracking.</span></span> <span data-ttu-id="8fe57-109">Поскольку взаимодействие с поиском Azure только через API-интерфейсы, hello телеметрии должен быть реализован разработчиками hello поиском, следуйте инструкциям hello на этой странице.</span><span class="sxs-lookup"><span data-stu-id="8fe57-109">Because interaction with Azure Search is only through APIs, hello telemetry must be implemented by hello developers using search, following hello instructions in this page.</span></span>

## <a name="identify-hello-relevant-search-data"></a><span data-ttu-id="8fe57-110">Определить данные, соответствующие поиска hello</span><span class="sxs-lookup"><span data-stu-id="8fe57-110">Identify hello relevant search data</span></span>

<span data-ttu-id="8fe57-111">toohave поиска полезных метрик, это необходимые toolog некоторые сигналы от пользователей hello приложения hello поиска.</span><span class="sxs-lookup"><span data-stu-id="8fe57-111">toohave useful search metrics, it's necessary toolog some signals from hello users of hello search application.</span></span> <span data-ttu-id="8fe57-112">Эти сигналы обозначения содержимого, что интересуют пользователей и их соответствующие tootheir необходимо учитывать.</span><span class="sxs-lookup"><span data-stu-id="8fe57-112">These signals signify content that users are interested in and that they consider relevant tootheir needs.</span></span>

<span data-ttu-id="8fe57-113">Аналитика поискового трафика учитывает два типа событий:</span><span class="sxs-lookup"><span data-stu-id="8fe57-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="8fe57-114">События поиска, инициированные пользователями. Представляют интерес только поисковые запросы, инициируемые пользователем.</span><span class="sxs-lookup"><span data-stu-id="8fe57-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="8fe57-115">Запросов, используемый toopopulate поиска аспектов, дополнительное содержимое или все внутренние сведения не представляют интереса, а также Наклон и смещение результаты.</span><span class="sxs-lookup"><span data-stu-id="8fe57-115">Search requests used toopopulate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="8fe57-116">События click создаваемого пользователем: с помощью щелчков в этом документе мы ссылку tooa пользователя при выборе отдельного результата поиска, возвращенные запросом поиска.</span><span class="sxs-lookup"><span data-stu-id="8fe57-116">User generated click events: By clicks in this document, we refer tooa user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="8fe57-117">Щелчок обычно означает, что документ релевантный для конкретного поискового запроса.</span><span class="sxs-lookup"><span data-stu-id="8fe57-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="8fe57-118">Связывая поиска и нажмите кнопку события с идентификатором корреляции, это поведение hello возможных tooanalyze пользователей на приложение.</span><span class="sxs-lookup"><span data-stu-id="8fe57-118">By linking search and click events with a correlation id, it's possible tooanalyze hello behaviors of users on your application.</span></span> <span data-ttu-id="8fe57-119">Эти знания для поиска, невозможно tooobtain с только поиск журналов трафика.</span><span class="sxs-lookup"><span data-stu-id="8fe57-119">These search insights are impossible tooobtain with only search traffic logs.</span></span>

## <a name="how-tooimplement-search-traffic-analytics"></a><span data-ttu-id="8fe57-120">Как tooimplement поиск аналитика трафика</span><span class="sxs-lookup"><span data-stu-id="8fe57-120">How tooimplement search traffic analytics</span></span>

<span data-ttu-id="8fe57-121">сигналы Hello упоминалось в предыдущем hello что раздел должен получить данные из приложения hello поиска как hello пользователь взаимодействует с ним.</span><span class="sxs-lookup"><span data-stu-id="8fe57-121">hello signals mentioned in hello preceding section must be gathered from hello search application as hello user interacts with it.</span></span> <span data-ttu-id="8fe57-122">Application Insights — это расширяемое решение мониторинга с гибкими параметрами инструментирования, доступное для нескольких платформ.</span><span class="sxs-lookup"><span data-stu-id="8fe57-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="8fe57-123">Использование Application Insights позволяет воспользоваться преимуществами отчеты поиска Power BI hello, созданные упрощает поиск Azure toomake hello анализа данных.</span><span class="sxs-lookup"><span data-stu-id="8fe57-123">Usage of Application Insights lets you take advantage of hello Power BI search reports created by Azure Search toomake hello analysis of data easier.</span></span>

<span data-ttu-id="8fe57-124">В hello [портала](https://portal.azure.com) страница для службы поиска Azure, колонке hello аналитика трафика службы поиска содержит памятку для следующего этот шаблон телеметрии.</span><span class="sxs-lookup"><span data-stu-id="8fe57-124">In hello [portal](https://portal.azure.com) page for your Azure Search service, hello Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="8fe57-125">Можно также выбрать или создать ресурс Application Insights и разделе hello необходимых данных, в одном месте.</span><span class="sxs-lookup"><span data-stu-id="8fe57-125">You can also select or create an Application Insights resource, and see hello necessary data, all in one place.</span></span>

![Инструкции по аналитике поискового трафика][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="8fe57-127">1. Выбор ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="8fe57-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="8fe57-128">Обязательно tooselect toouse ресурса Application Insights, или создайте его, если вы их еще нет.</span><span class="sxs-lookup"><span data-stu-id="8fe57-128">You need tooselect an Application Insights resource toouse or create one if you don't have one already.</span></span> <span data-ttu-id="8fe57-129">Можно использовать ресурс, уже в hello toolog используйте требуемое пользовательских событий.</span><span class="sxs-lookup"><span data-stu-id="8fe57-129">You can use a resource that's already in use toolog hello required custom events.</span></span>

<span data-ttu-id="8fe57-130">При создании ресурса Application Insights все типы приложений допустимы для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="8fe57-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="8fe57-131">Выберите hello один, наилучшим образом соответствующего hello платформы, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="8fe57-131">Select hello one that best fits hello platform you are using.</span></span>

<span data-ttu-id="8fe57-132">Для создания клиентских hello телеметрии для приложения необходим ключ инструментирования hello.</span><span class="sxs-lookup"><span data-stu-id="8fe57-132">You need hello instrumentation key for creating hello telemetry client for your application.</span></span> <span data-ttu-id="8fe57-133">Вы можете получить из панели мониторинга портала Application Insights hello, или его можно получить на странице hello аналитика трафика службы поиска, выбрав экземпляр hello требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="8fe57-133">You can get it from hello Application Insights portal dashboard, or you can get it from hello Search Traffic Analytics page, selecting hello instance you want toouse.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="8fe57-134">2. Инструментирование приложения</span><span class="sxs-lookup"><span data-stu-id="8fe57-134">2. Instrument your application</span></span>

<span data-ttu-id="8fe57-135">Этот этап — где инструментирование собственного приложения поиска с помощью ресурса Application Insights hello вашей hello, созданный в шаге выше.</span><span class="sxs-lookup"><span data-stu-id="8fe57-135">This phase is where you instrument your own search application, using hello Application Insights resource your created in hello step above.</span></span> <span data-ttu-id="8fe57-136">Состоит из четырех этапов процесса toothis:</span><span class="sxs-lookup"><span data-stu-id="8fe57-136">There are four steps toothis process:</span></span>

<span data-ttu-id="8fe57-137">**I. Создание клиента телеметрии** это hello объекта, который отправляет события toohello ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8fe57-137">**I. Create a telemetry client** This is hello object that sends events toohello Application Insights Resource.</span></span>

<span data-ttu-id="8fe57-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="8fe57-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="8fe57-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="8fe57-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="8fe57-140">Другие языки и платформы, см. в разделе hello завершения [списка](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="8fe57-140">For other languages and platforms, see hello complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="8fe57-141">**II. Идентификатор поиска для корреляции запроса** запросов поиска toocorrelate щелчков мыши это необходимые toohave идентификатор корреляции, связывающий эти два различных события.</span><span class="sxs-lookup"><span data-stu-id="8fe57-141">**II. Request a Search ID for correlation** toocorrelate search requests with clicks, it's necessary toohave a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="8fe57-142">Служба поиска Azure предоставляет идентификатор поиска, когда он запрашивается с заголовком:</span><span class="sxs-lookup"><span data-stu-id="8fe57-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="8fe57-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="8fe57-143">*C#*</span></span>

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="8fe57-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="8fe57-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="8fe57-145">**III. Регистрация событий поиска.**</span><span class="sxs-lookup"><span data-stu-id="8fe57-145">**III. Log Search events**</span></span>

<span data-ttu-id="8fe57-146">Каждый раз, выдает запрос на поиск пользователей, необходимо войти, событие поиска с hello следующие схемы пользовательские события Application Insights:</span><span class="sxs-lookup"><span data-stu-id="8fe57-146">Every time that a search request is issued by a user, you should log that as a search event with hello following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="8fe57-147">**ServiceName**: имя службы поиска (string) **SearchId**: Уникальный идентификатор (guid) запроса поиска hello (поставляется в ответа на запросы поиска hello) **IndexName**: индекс службы поиска (string) запрашивать toobe **QueryTerms**: условия поиска (string), введенные пользователем hello, **ResultCount**: (int) количество документов, которые были возвращены (поставляется в ответа на запросы поиска hello)  **ScoringProfile**: имя hello оценки профиль, используемый, если таковые имеются (string)</span><span class="sxs-lookup"><span data-stu-id="8fe57-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello search query (comes in hello search response) **IndexName**: (string) search service index toobe queried **QueryTerms**: (string) search terms entered by hello user **ResultCount**: (int) number of documents that were returned (comes in hello search response) **ScoringProfile**: (string) name of hello scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="8fe57-148">Количества запросов для создаваемого пользователем запросов путем добавления $count = true tooyour поискового запроса.</span><span class="sxs-lookup"><span data-stu-id="8fe57-148">Request count on user generated queries by adding $count=true tooyour search query.</span></span> <span data-ttu-id="8fe57-149">Дополнительные сведения см. [здесь](https://docs.microsoft.com/rest/api/searchservice/search-documents#request).</span><span class="sxs-lookup"><span data-stu-id="8fe57-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="8fe57-150">Не забывайте tooonly запросов поиска журналов, созданных пользователями.</span><span class="sxs-lookup"><span data-stu-id="8fe57-150">Remember tooonly log search queries that are generated by users.</span></span>
>

<span data-ttu-id="8fe57-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="8fe57-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="8fe57-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="8fe57-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="8fe57-153">**IV. Регистрация событий щелчка.**</span><span class="sxs-lookup"><span data-stu-id="8fe57-153">**IV. Log Click events**</span></span>

<span data-ttu-id="8fe57-154">Каждый щелчок документа — это событие, которое необходимо зарегистрировать для анализа поиска.</span><span class="sxs-lookup"><span data-stu-id="8fe57-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="8fe57-155">Используйте эти события toolog пользовательские события Application Insights с hello следующие схемы:</span><span class="sxs-lookup"><span data-stu-id="8fe57-155">Use Application Insights custom events toolog these events with hello following schema:</span></span>

<span data-ttu-id="8fe57-156">**ServiceName**: имя службы поиска (string) **SearchId**: Уникальный идентификатор (guid) запроса связанных поиска hello **DocId**: идентификатор документа (string) **позиции** : страница результатов (int) ранг документа hello в поиске hello</span><span class="sxs-lookup"><span data-stu-id="8fe57-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello related search query **DocId**: (string) document identifier **Position**: (int) rank of hello document in hello search results page</span></span>

> [!NOTE]
> <span data-ttu-id="8fe57-157">Позиция ссылается toohello фундаментальный заказа в приложении.</span><span class="sxs-lookup"><span data-stu-id="8fe57-157">Position refers toohello cardinal order in your application.</span></span> <span data-ttu-id="8fe57-158">Все бесплатные tooset это число, столько, сколько он всегда имеет hello же tooallow для сравнения.</span><span class="sxs-lookup"><span data-stu-id="8fe57-158">You are free tooset this number, as long as it's always hello same, tooallow for comparison.</span></span>
>

<span data-ttu-id="8fe57-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="8fe57-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="8fe57-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="8fe57-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="8fe57-161">3. Анализ с помощью Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="8fe57-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="8fe57-162">После инструментированного приложения и проверки, что приложение правильно подключенной tooApplication аналитики можно использовать стандартный шаблон, полученные при поиске Azure для Power BI desktop.</span><span class="sxs-lookup"><span data-stu-id="8fe57-162">After you have instrumented your app and verified your application is correctly connected tooApplication Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="8fe57-163">Этот шаблон содержит диаграммы и таблицы, которые помогают сделать более обоснованные решения tooimprove производительность поиска и релевантности.</span><span class="sxs-lookup"><span data-stu-id="8fe57-163">This template contains charts and tables that help you make more informed decisions tooimprove your search performance and relevance.</span></span>

<span data-ttu-id="8fe57-164">tooinstantiate hello Power BI шаблона рабочего стола, необходимо три элемента информации об Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8fe57-164">tooinstantiate hello Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="8fe57-165">Эти данные можно найти в hello страницы аналитика трафика службы поиска, при выборе toouse ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="8fe57-165">This data can be found in hello Search Traffic Analytics page, when you select hello resource toouse</span></span>

![Данные Application Insights в колонке hello аналитика трафика службы поиска][2]

<span data-ttu-id="8fe57-167">Метрики, включенных в шаблон рабочего стола hello Power BI.</span><span class="sxs-lookup"><span data-stu-id="8fe57-167">Metrics included in hello Power BI desktop template:</span></span>

*   <span data-ttu-id="8fe57-168">Щелкните по скорости (CTR): отношение пользователи, выбравшие toohello конкретный документ, количество общее операций поиска.</span><span class="sxs-lookup"><span data-stu-id="8fe57-168">Click through Rate (CTR): ratio of users who click on a specific document toohello number of total searches.</span></span>
*   <span data-ttu-id="8fe57-169">Поисковые запросы без щелчков. Условия основных запросов, для которых не выполнялись щелчки.</span><span class="sxs-lookup"><span data-stu-id="8fe57-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="8fe57-170">Наиболее щелчке документы: наиболее щелчке документы по Идентификатору в hello последние 24 часа, 7 дней и 30 дней.</span><span class="sxs-lookup"><span data-stu-id="8fe57-170">Most clicked documents: most clicked documents by ID in hello last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="8fe57-171">Пары популярных термин документа: условия, которые приводят к hello нажатии того же документа, упорядоченные по щелчков мыши.</span><span class="sxs-lookup"><span data-stu-id="8fe57-171">Popular term-document pairs: terms that result in hello same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="8fe57-172">Время tooclick: щелчков группируются по времени с момента hello поискового запроса</span><span class="sxs-lookup"><span data-stu-id="8fe57-172">Time tooclick: clicks bucketed by time since hello search query</span></span>

![Шаблон Power BI для чтения из Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="8fe57-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8fe57-174">Next Steps</span></span>
<span data-ttu-id="8fe57-175">Инструментирование поиска tooget мощная и полезных данных приложения о службе поиска.</span><span class="sxs-lookup"><span data-stu-id="8fe57-175">Instrument your search application tooget powerful and insightful data about your search service.</span></span>

<span data-ttu-id="8fe57-176">Дополнительные сведения об Application Insights см. [здесь](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="8fe57-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="8fe57-177">Посетите Application Insights [странице цен](https://azure.microsoft.com/pricing/details/application-insights/) toolearn Дополнительные сведения об их разных уровнях.</span><span class="sxs-lookup"><span data-stu-id="8fe57-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) toolearn more about their different service tiers.</span></span>

<span data-ttu-id="8fe57-178">Узнайте больше о создании удивительных отчетов.</span><span class="sxs-lookup"><span data-stu-id="8fe57-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="8fe57-179">См. статью [Начало работы с Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="8fe57-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
