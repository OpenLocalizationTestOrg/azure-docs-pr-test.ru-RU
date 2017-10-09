---
title: "Индекс поиска Azure aaaQuery | Документы Microsoft"
description: "Построить запрос поиска в поиске Azure и использовать параметры сортировки и toofilter поиска результатов поиска."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 69205d7a-363f-4b92-a53f-6ca818a3d2c7
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: ashmaka
ms.openlocfilehash: 4a5ffffe179695fc09446760e21a738dd36c29b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index"></a>Отправка запросов в индекс службы поиска Azure
> [!div class="op_single_selector"]
> * [Обзор](search-query-overview.md)
> * [Портал](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

При отправке запросов поиска tooAzure поиска, существует несколько параметров, которые могут быть указаны вместе с hello фактических слов, введенные в поле поиска hello приложения. Эти параметры запроса разрешить tooachieve некоторые более глубокого управления hello [возможности полнотекстового поиска](search-lucene-query-architecture.md).

Ниже приведен список, который приводится краткое описание наиболее частые способы использования параметров запроса hello в поиске Azure. Для полного покрытия параметров запроса и их поведении см. в разделе hello подробные страницы для hello [API-интерфейса REST](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) и [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters#microsoft_azure_search_models_searchparameters#properties_summary).

## <a name="types-of-queries"></a>Типы запросов
Поиск Azure предлагает множество запросов очень мощной toocreate параметры. Hello два основных типа запроса будет использоваться являются `search` и `filter`. Объект `search` запрос ищет один или несколько термов во всех *с возможностью поиска* поля в индексе и работает hello, как и ожидается поисковой системы, например Google и Bing toowork. Запрос `filter` оценивает логическое выражение во всех *фильтруемых* полях индекса. В отличие от `search` запросы, `filter` запросов соответствуют hello точное содержимое поля, то есть они с учетом регистра для полей строк.

Запросы этих двух типов можно использовать вместе или по отдельности. При их совместном использовании, фильтр hello — применяется весь индекс первого toohello и затем выполняется поиск hello на hello результаты фильтрации hello. Фильтры таким образом могут быть полезным приемом tooimprove производительности запросов, поскольку сокращают hello набор документов, hello tooprocess потребности запроса поиска.

Hello синтаксис выражений фильтра является подмножеством hello [языка фильтров OData](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search). Для запросов поиска можно использовать либо hello [упрощенным синтаксисом](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) или hello [синтаксис запроса Lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) которые рассматриваются ниже.

### <a name="simple-query-syntax"></a>Простой синтаксис запросов
Hello [синтаксис простого запроса](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) — язык запросов по умолчанию hello, используемых в поиске Azure. синтаксис простого запроса Hello поддерживает ряд общих операторы поиска, включая hello AND, OR, не, фразы, суффикс и приоритет операторов.

### <a name="lucene-query-syntax"></a>синтаксис запросов Lucene
Hello [синтаксис запроса Lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) позволяет toouse hello широкое распространение, а также выразительный язык запросов разработаны в рамках программы [Apache Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html).

Этот синтаксис запроса позволяет tooeasily достижения hello следующие возможности: [запросов в области полей](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fields), [нечеткого поиска](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fuzzy), [поиск по сходству](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_proximity), [ терминов подъема](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_termboost), [поиска регулярного выражения](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_regex), [поиск по маске](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_wildcard), [синтаксис основы](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_syntax), и [запросов с помощью логические операторы](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_boolean).

## <a name="ordering-results"></a>Упорядочение результатов
При получении результатов для запроса поиска, можно запросить, что поиск Azure служит hello результаты, упорядоченные по значениям одного поля. По умолчанию службы поиска Azure упорядочивает результаты поиска hello на основании hello ранг Оценка поиска каждого документа, который является производным от [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).

Если требуется, чтобы результаты, упорядоченные по значение, отличное от оценки поиска hello tooreturn поиска Azure, можно использовать hello `orderby` параметр поиска. Можно задать значение hello hello `orderby` tooinclude поле параметра именует и вызывает toohello [ `geo.distance()` функция](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search) для представления значения. Каждое выражение может следовать `asc` tooindicate, что результаты запрашиваются в порядке возрастания и `desc` tooindicate, что результаты запрашиваются в порядке убывания. Ранжирование по умолчанию Hello по возрастанию.

## <a name="paging"></a>Разбиение по страницам
Поиск Azure позволяет легко tooimplement разбивка на страницы результатов поиска. С помощью hello `top` и `skip` параметров, можно плавно издающие запросы поиска, которые позволяют tooreceive hello полного набора результатов поиска в управляемый, упорядоченный подмножества, легко включить рекомендации хорошо поиска пользовательского интерфейса. При получении этих более малые подмножества результатов, вы также можете получать hello число документов в hello полного набора результатов поиска.

Дополнительные сведения о разбиении на страницы результатов поиска в статья hello [отображением результатов поиска toopage в поиске Azure](search-pagination-page-layout.md).

## <a name="hit-highlighting"></a>Выделение совпадений
В поиске Azure, выделяя hello точное части результатов поиска, соответствующих поисковому запросу hello легко выполняется с помощью hello `highlight`, `highlightPreTag`, и `highlightPostTag` параметров. Можно указать, какие *с возможностью поиска* поля должны иметь их совпадающего текста уделяется внимания, а также указание возвращает hello точное строка теги tooappend toohello начало и конец hello совпадающий текст поиска Azure.

## <a name="try-out-query-syntax"></a>Знакомство с синтаксисом запросов

Hello лучшим способом toounderstand синтаксические отличия — путем отправки запросов и просмотр результатов.

+ Используйте [обозреватель поиска](search-explorer.md) в hello портал Azure. Развернув [индекс образец hello](search-get-started-portal.md), можно запросить индекс hello в минутах, с помощью средства в портале hello.

+ Используйте [Fiddler](search-fiddler.md) или Chrome почтальон toosubmit запросы tooan индекса вы отправили tooyour службы поиска. Оба средства поддерживают конечную точку HTTP tooan вызовы REST. 
