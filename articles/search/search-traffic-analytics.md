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
# <a name="what-is-search-traffic-analytics"></a>Что такое аналитика поискового трафика?
Аналитика поискового трафика — это модель реализации цикла обратной связи для службы поиска. Этот шаблон описывает hello необходимые данные и как toocollect его с помощью Application Insights, отраслевым лидером для наблюдения за службами в нескольких платформ.

Аналитика поискового трафика позволяет обеспечить видимость службы поиска и получить сведения о пользователях и их поведении. Когда данные о выберите пользователей, это toomake возможные решения, которые улучшить возможности поиска и tooback off при результаты hello, не ожидаемых.

Поиск Azure предлагает решение телеметрии, объединяющая аналитики приложения Azure и Power BI tooprovide глубокого мониторинга и отслеживания. Поскольку взаимодействие с поиском Azure только через API-интерфейсы, hello телеметрии должен быть реализован разработчиками hello поиском, следуйте инструкциям hello на этой странице.

## <a name="identify-hello-relevant-search-data"></a>Определить данные, соответствующие поиска hello

toohave поиска полезных метрик, это необходимые toolog некоторые сигналы от пользователей hello приложения hello поиска. Эти сигналы обозначения содержимого, что интересуют пользователей и их соответствующие tootheir необходимо учитывать.

Аналитика поискового трафика учитывает два типа событий:

1. События поиска, инициированные пользователями. Представляют интерес только поисковые запросы, инициируемые пользователем. Запросов, используемый toopopulate поиска аспектов, дополнительное содержимое или все внутренние сведения не представляют интереса, а также Наклон и смещение результаты.

2. События click создаваемого пользователем: с помощью щелчков в этом документе мы ссылку tooa пользователя при выборе отдельного результата поиска, возвращенные запросом поиска. Щелчок обычно означает, что документ релевантный для конкретного поискового запроса.

Связывая поиска и нажмите кнопку события с идентификатором корреляции, это поведение hello возможных tooanalyze пользователей на приложение. Эти знания для поиска, невозможно tooobtain с только поиск журналов трафика.

## <a name="how-tooimplement-search-traffic-analytics"></a>Как tooimplement поиск аналитика трафика

сигналы Hello упоминалось в предыдущем hello что раздел должен получить данные из приложения hello поиска как hello пользователь взаимодействует с ним. Application Insights — это расширяемое решение мониторинга с гибкими параметрами инструментирования, доступное для нескольких платформ. Использование Application Insights позволяет воспользоваться преимуществами отчеты поиска Power BI hello, созданные упрощает поиск Azure toomake hello анализа данных.

В hello [портала](https://portal.azure.com) страница для службы поиска Azure, колонке hello аналитика трафика службы поиска содержит памятку для следующего этот шаблон телеметрии. Можно также выбрать или создать ресурс Application Insights и разделе hello необходимых данных, в одном месте.

![Инструкции по аналитике поискового трафика][1]

### <a name="1-select-an-application-insights-resource"></a>1. Выбор ресурса Application Insights

Обязательно tooselect toouse ресурса Application Insights, или создайте его, если вы их еще нет. Можно использовать ресурс, уже в hello toolog используйте требуемое пользовательских событий.

При создании ресурса Application Insights все типы приложений допустимы для этого сценария. Выберите hello один, наилучшим образом соответствующего hello платформы, которую вы используете.

Для создания клиентских hello телеметрии для приложения необходим ключ инструментирования hello. Вы можете получить из панели мониторинга портала Application Insights hello, или его можно получить на странице hello аналитика трафика службы поиска, выбрав экземпляр hello требуется toouse.

### <a name="2-instrument-your-application"></a>2. Инструментирование приложения

Этот этап — где инструментирование собственного приложения поиска с помощью ресурса Application Insights hello вашей hello, созданный в шаге выше. Состоит из четырех этапов процесса toothis:

**I. Создание клиента телеметрии** это hello объекта, который отправляет события toohello ресурс Application Insights.

*C#*

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

*JavaScript*

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

Другие языки и платформы, см. в разделе hello завершения [списка](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).

**II. Идентификатор поиска для корреляции запроса** запросов поиска toocorrelate щелчков мыши это необходимые toohave идентификатор корреляции, связывающий эти два различных события. Служба поиска Azure предоставляет идентификатор поиска, когда он запрашивается с заголовком:

*C#*

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

*JavaScript*

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

**III. Регистрация событий поиска.**

Каждый раз, выдает запрос на поиск пользователей, необходимо войти, событие поиска с hello следующие схемы пользовательские события Application Insights:

**ServiceName**: имя службы поиска (string) **SearchId**: Уникальный идентификатор (guid) запроса поиска hello (поставляется в ответа на запросы поиска hello) **IndexName**: индекс службы поиска (string) запрашивать toobe **QueryTerms**: условия поиска (string), введенные пользователем hello, **ResultCount**: (int) количество документов, которые были возвращены (поставляется в ответа на запросы поиска hello)  **ScoringProfile**: имя hello оценки профиль, используемый, если таковые имеются (string)

> [!NOTE]
> Количества запросов для создаваемого пользователем запросов путем добавления $count = true tooyour поискового запроса. Дополнительные сведения см. [здесь](https://docs.microsoft.com/rest/api/searchservice/search-documents#request).
>

> [!NOTE]
> Не забывайте tooonly запросов поиска журналов, созданных пользователями.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

*JavaScript*

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

**IV. Регистрация событий щелчка.**

Каждый щелчок документа — это событие, которое необходимо зарегистрировать для анализа поиска. Используйте эти события toolog пользовательские события Application Insights с hello следующие схемы:

**ServiceName**: имя службы поиска (string) **SearchId**: Уникальный идентификатор (guid) запроса связанных поиска hello **DocId**: идентификатор документа (string) **позиции** : страница результатов (int) ранг документа hello в поиске hello

> [!NOTE]
> Позиция ссылается toohello фундаментальный заказа в приложении. Все бесплатные tooset это число, столько, сколько он всегда имеет hello же tooallow для сравнения.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

*JavaScript*

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a>3. Анализ с помощью Power BI Desktop

После инструментированного приложения и проверки, что приложение правильно подключенной tooApplication аналитики можно использовать стандартный шаблон, полученные при поиске Azure для Power BI desktop.
Этот шаблон содержит диаграммы и таблицы, которые помогают сделать более обоснованные решения tooimprove производительность поиска и релевантности.

tooinstantiate hello Power BI шаблона рабочего стола, необходимо три элемента информации об Application Insights. Эти данные можно найти в hello страницы аналитика трафика службы поиска, при выборе toouse ресурсов hello

![Данные Application Insights в колонке hello аналитика трафика службы поиска][2]

Метрики, включенных в шаблон рабочего стола hello Power BI.

*   Щелкните по скорости (CTR): отношение пользователи, выбравшие toohello конкретный документ, количество общее операций поиска.
*   Поисковые запросы без щелчков. Условия основных запросов, для которых не выполнялись щелчки.
*   Наиболее щелчке документы: наиболее щелчке документы по Идентификатору в hello последние 24 часа, 7 дней и 30 дней.
*   Пары популярных термин документа: условия, которые приводят к hello нажатии того же документа, упорядоченные по щелчков мыши.
*   Время tooclick: щелчков группируются по времени с момента hello поискового запроса

![Шаблон Power BI для чтения из Application Insights][3]


## <a name="next-steps"></a>Дальнейшие действия
Инструментирование поиска tooget мощная и полезных данных приложения о службе поиска.

Дополнительные сведения об Application Insights см. [здесь](https://go.microsoft.com/fwlink/?linkid=842905). Посетите Application Insights [странице цен](https://azure.microsoft.com/pricing/details/application-insights/) toolearn Дополнительные сведения об их разных уровнях.

Узнайте больше о создании удивительных отчетов. См. статью [Начало работы с Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/).

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
