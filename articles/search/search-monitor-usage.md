---
title: "aaaMonitor использования и статистики в службе поиска Azure | Документы Microsoft"
description: "Отслеживайте потребление ресурсов и размера индексов для Поиска Azure, размещенной облачной службы поиска в Microsoft Azure."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
tags: azure-portal
ms.assetid: 122948de-d29a-426e-88b4-58cbcee4bc23
ms.service: search
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/01/2017
ms.author: betorres
ms.openlocfilehash: f38eabb5d04a410e11eaaff22157da8aba9e4845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-an-azure-search-service"></a>Мониторинг службы поиска Azure

Поиск Azure предлагает различные ресурсы для отслеживания использования и производительности служб поиска. Он предоставляет доступ к toometrics, журналы, статистика индекса и расширенные возможности мониторинга в Power BI. Эта статья описывает, как tooenable hello различные стратегии мониторинга и как toointerpret hello результирующие данные.

## <a name="azure-search-metrics"></a>Метрики Поиска Azure
Метрики позволяют почти в реальном времени отслеживать службу поиска, и они доступны для каждой службы без дополнительной настройки. Они позволяют отслеживать производительность hello службы для копирования too30 дней.

Поиск Azure собирает данные для трех различных метрик:

* Поиск задержка: время служба поиска hello необходимости tooprocess поисковые запросы, объединение идет Поминутно.
* Запросов поиска в секунду: число запросов поиска, получаемых в секунду (данные агрегируются поминутно).
* Процент регулируемых поисковых запросов: процент отрегулированных запросов поиска (данные агрегируются поминутно).

![Снимок экрана. Число запросов в секунду][1]

### <a name="set-up-alerts"></a>Настройка оповещений
Со страницы подробные метрики hello можно настроить оповещения tootrigger уведомление по электронной почте или автоматическое действие при метрики пересекает пороговое значение, которое вы определили.

Дополнительные сведения о метриках проверьте hello Полная документация по Azure монитора.  

## <a name="how-tootrack-resource-usage"></a>Как tootrack использование ресурсов
Отслеживание hello роста индексов и размер документа может помочь заранее настроить емкость до обращения hello верхний предел, установленным для службы. Это можно сделать на портале hello или программным путем с помощью API-интерфейса REST hello.

### <a name="using-hello-portal"></a>С помощью портала hello

Использование ресурсов toomonitor, просмотреть счетчики hello и статистики для службы в hello [портала](https://portal.azure.com).

1. Войдите в toohello [портала](https://portal.azure.com).
2. Откройте панель мониторинга службы hello службы поиска Azure. Плитки для hello службы можно найти на домашней странице hello или просмотре toohello службы перейдите на hello JumpBar.

раздел, посвященный использованию Hello включает индикатор, который определяет, какая часть доступных ресурсов, сейчас используются. Сведения об ограничениях индексов, документов и объема хранилища для каждой службы см. в статье [Ограничения поиска Azure](search-limits-quotas-capacity.md).

  ![Плитка "Использование"][2]

> [!NOTE]
> Снимок экрана приветствия для hello бесплатной службы, которая содержит не более одной реплики и каждой секции можно только индексы узла 3, 10 000 документов или 50 МБ данных, наступит раньше. Службы, созданные на уровне "Базовый" или "Стандартный", предоставляют значительно больше возможностей. Дополнительные сведения о выборе ценовой категории см. в статье [Выбор SKU или ценовой категории для службы поиска Azure](search-sku-tier.md).
>
>

### <a name="using-hello-rest-api"></a>С помощью API-интерфейса REST hello
Hello REST API поиска Azure и hello .NET SDK предоставляют программный доступ tooservice метрики.  Если вы используете [индексаторы](https://msdn.microsoft.com/library/azure/dn946891.aspx) tooload индекса из базы данных SQL Azure или Azure Cosmos DB дополнительный API-Интерфейс-числа доступных tooget hello, требуется.

* [Получение статистики индексов](/rest/api/searchservice/get-index-statistics)
* [Подсчет документов](/rest/api/searchservice/count-documents)
* [Получение состояния индексатора](/rest/api/searchservice/get-indexer-status)

## <a name="how-tooexport-logs-and-metrics"></a>Каким образом ведет журнал tooexport и метрики

Вы можете экспортировать hello журналы операций службы и hello необработанных данных для метрик hello, описанные в предшествующих раздел hello. Журналы операций позволяют понять, как используется служба hello и могут быть использованы из Power BI, когда данные копируются tooa учетной записи хранилища. С этой целью Поиск Azure предлагает пакет Power BI для мониторинга содержимого.


### <a name="enabling-monitoring"></a>Включение мониторинга
Откройте службы поиска Azure в hello [портал Azure](http://portal.azure.com) под hello включение наблюдения на параметр.

Выбор данных hello требуется tooexport: журналы и показатели. Можно скопировать его tooa учетной записи хранилища, отправкой tooan концентратора событий или экспортировать его tooLog Analytics.

![Как tooenable мониторинга на портале hello][3]

с помощью PowerShell или Azure CLI hello tooenable см. в документации hello [здесь](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs).

### <a name="logs-and-metrics-schemas"></a>Журналы и схемы метрик
При хранения скопированных tooa hello данных учетной записи, hello данные форматируются как JSON и его место в два контейнера:

* insights-logs-operationlogs: для поиска журналов трафика
* insights-metrics-pt1m: для метрик

Для каждого часа и каждого контейнера создается один большой двоичный объект.

Пример пути: `resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`

#### <a name="log-schema"></a>Схема журнала
большие двоичные объекты для Hello журналы содержат журналы трафика службы поиска.
Каждый большой двоичный объект имеет один корневой объект под названием **records** , который содержит массив объектов журнала.
Каждый BLOB-объект имеет записей на все операции hello, выполняемых на каждом hello того же часа.

| Имя | Тип | Пример | Примечания |
| --- | --- | --- | --- |
| time |datetime; |"2015-12-07T00:00:43.6872559Z" |Отметка времени операции hello |
| resourceId |string |"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/> MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE" |Идентификатор вашего ресурса |
| operationName |string |"Query.Search" |Имя Hello операции hello |
| operationVersion |string |"2015-02-28" |Hello api-version используется |
| category |string |"OperationLogs" |константа |
| resultType |string |Success |Возможные значения: Success или Failure |
| resultSignature |int |200 |Код результата HTTP |
| durationMS |int |50 |Время выполнения операции hello в миллисекундах |
| properties |object |см. в следующей таблице hello |Объект, содержащий данные об операции |

**Схема свойств**
| Имя | Тип | Пример | Примечания |
| --- | --- | --- | --- |
| Описание |string |"GET /indexes('content')/docs" |Конечная точка Hello операции |
| Запрос |string |"?search=AzureSearch&$count=true&api-version=2015-02-28" |Параметры запроса Hello |
| Документы |int |42 |Количество обработанных документов |
| IndexName |string |"testindex" |Имя индекса hello, связанные с операцией hello |

#### <a name="metrics-schema"></a>Схема метрик
| Имя | Тип | Пример | Примечания |
| --- | --- | --- | --- |
| resourceId |string |"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/>MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE" |Идентификатор вашего ресурса |
| metricName |string |"Latency" |Имя метрики hello Hello |
| Twitter в режиме реального |datetime; |"2015-12-07T00:00:43.6872559Z" |Отметка времени Hello операции |
| average |int |64 |Среднее значение Hello hello необработанных выборок в интервале времени метрики hello |
| minimum |int |37 |Минимальное значение Hello hello необработанных выборок в интервале времени метрики hello |
| maximum |int |78 |Максимальное значение Hello hello необработанных выборок в интервале времени метрики hello |
| total |int |258 |Общее значение Hello hello необработанных выборок в интервале времени метрики hello |
| count |int |4. |Метрика hello toogenerate используется Hello количество необработанных выборок |
| timegrain |string |"PT1M" |Hello интервала метрика hello в формате ISO 8601 |

Все метрики передают данные с интервалом в одну минуту. Каждая метрика отражает минимальное, максимальное и среднее значения за минуту.

Метрика SearchQueriesPerSecond hello минимальное значение — наименьшее значение hello для поисковых запросов в секунду, которое было зарегистрировано в течение этой минуты. Hello применимо и к toohello максимальное значение. Среднее, hello статистические через минуту всей hello.
Определите, этот сценарий за одну минуту: одной секунде высокой нагрузки, hello максимальное значение для SearchQueriesPerSecond, следуют 58 секунд среднюю нагрузку, и наконец одной секунды с более одного запроса, это минимальное hello.

Для ThrottledSearchQueriesPercentage, минимальное, максимальное, среднее и общего количества, все имеют hello одинаковые значения: hello процент поисковые запросы, которые были регулированию из hello общее число запросов поиска в течение одной минуты.

## <a name="analyzing-your-data-with-power-bi"></a>Анализ данных с помощью Power BI

Мы рекомендуем использовать [Power BI](https://powerbi.microsoft.com) tooexplore и визуализации данных. Можно легко подключать tooyour учетной записи хранилища Azure и быстро приступить к анализу данных.

Поиск Azure предоставляет [пакет содержимого Power BI](https://app.powerbi.com/getdata/services/azure-search) , позволяет вам toomonitor и понять трафика поиска с помощью стандартных диаграмм и таблиц. Он содержит набор отчетов Power BI, которые автоматически подключаются tooyour данных и предоставления visual ценной информации о службе поиска. Дополнительные сведения см. в разделе hello [странице справки пакета содержимого](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/).

![Панель мониторинга Power BI для Поиска Azure][4]

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите [масштабирования реплик и секции](search-limits-quotas-capacity.md) рекомендации по как toobalance hello выделения секции и реплики для существующей службы.

Более подробные сведения об администрировании службы поиска см. в статье [Администрирование службы поиска Azure на портале Azure](search-manage.md), а рекомендации по настройке в статье [Рекомендации по производительности и оптимизации Поиска Azure](search-performance-optimization.md).

Узнайте больше о создании удивительных отчетов. См. статью [Начало работы с Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).

<!--Image references-->
[1]: ./media/search-monitor-usage/AzSearch-Monitor-BarChart.PNG
[2]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG
[3]: ./media/search-monitor-usage/AzureSearch-Enable-Monitoring.PNG
[4]: ./media/search-monitor-usage/AzureSearch-PowerBI-Dashboard.png
