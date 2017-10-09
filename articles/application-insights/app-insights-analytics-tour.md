---
title: "Обзор aaaA аналитика в Azure Application Insights | Документы Microsoft"
description: "Короткие примеры все запросы основной hello в Analytics hello мощное средство аналитики приложений."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a>Знакомство с аналитикой в Application Insights
[Аналитика](app-insights-analytics.md) — мощное средство поиска функция hello [Application Insights](app-insights-overview.md). На этих страницах описан язык запросов Log Analytics.

* **[Вводное видео hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Испытайте аналитика на нашем смоделированные данные](https://analytics.applicationinsights.io/demo)**  Если ваше приложение еще не отправляет данные tooApplication аналитики.
* **[SQL-пользователей Памятка](https://aka.ms/sql-analytics)**  преобразует наиболее общих идиом hello.

Давайте пошагового tooget некоторых простых запросов, которого вы начали.

## <a name="connect-tooyour-application-insights-data"></a>Подключение к данным tooyour Application Insights
Откройте аналитику в [колонке "Обзор"](app-insights-dashboards.md) приложения в Application Insights.

![На сайте portal.azure.com откройте ресурс Application Insights и щелкните "Аналитика".](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a>Оператор [take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): отображение n строк
Точки данных, регистрирующие операции пользователя (обычно HTTP-запросы, полученные веб-приложением), хранятся в таблице `requests`. Каждая строка является точки данных телеметрии, полученных от hello пакет SDK Application Insights в вашем приложении.

Начнем с изучения несколько образцов строк таблицы hello:

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> Поместите курсор hello где-нибудь в инструкции hello пока ты. Инструкцию можно разделить на несколько строк, но она не должна содержать пустых строк. Пустые строки — это удобный способ tookeep некоторые отдельные запросы в окне приветствия.
>
>

Выберите нужные столбцы, перетащите их, чтобы cгруппировать, и примените фильтр:

![Выберите столбец в правом верхнем углу результатов.](./media/app-insights-analytics-tour/030.png)

Разверните ни элемент toosee hello сведения:

![Выберите "Таблица", а затем "Настроить столбцы".](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> Щелкните заголовок столбца порядок toore hello доступных результатов в веб-браузере hello hello. Но имейте в виду, что для большой результирующий набор, количество hello браузера загруженный toohello строк ограничено. Сортировка таким образом не всегда показывает hello фактическое высокий или низкого уровня элементов. элементы toosort надежно и использовать hello `top` или `sort` оператор.
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a>Операторы [top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) и [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)
`take`является полезным tooget краткий пример результата, но он демонстрирует строки из таблицы hello в произвольном порядке. использовать tooget упорядоченное представление `top` (пример) или `sort` (через hello всю таблицу).

Показать hello первые n строк, упорядоченных по определенному столбцу:

```AIQL

    requests | top 10 by timestamp desc
```

* *Синтаксис*. У большинства операторов есть параметры в виде ключевых слов, такие как `by`.
* `desc` — по убыванию, `asc` — по возрастанию.

![](./media/app-insights-analytics-tour/260.png)

`top...` является более производительным способом выполнения `sort ... | take...`. Можно было бы написать следующее:

```AIQL

    requests | sort by timestamp desc | take 10
```

Hello получим hello таким же, но оно будет выполняться немного медленнее. (Также можно написать `order`, это псевдоним `sort`).

Hello заголовки столбцов в представлении таблицы hello также можно использовать toosort hello результатов на экране приветствия. Но, разумеется, если вы использовали `take` или `top` tooretrieve только его часть таблицы будет только изменить порядок hello записи извлеченным.

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a>Оператор [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): фильтрация по условию

Давайте отобразим только запросы, вернувшие конкретный код результата.

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

Hello `where` оператор принимает логическое выражение. Ниже приведены некоторые ключевые моменты:

* `and`, `or`: логические операторы;
* `==`, `<>`, `!=`: равно и не равно;
* `=~`, `!~`: равенство и неравенство строк без учета регистра. Существует множество других операторов сравнения строк.

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a>Получение подходящего типа hello
Поиск неудачных запросов:

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a>Время

По умолчанию запросы являются ограниченными toohello последние 24 часа. Этот интервал можно изменить.

![](./media/app-insights-analytics-tour/change-time-range.png)

Переопределить hello временной диапазон, написав любой запрос, в которой указывается `timestamp` в предложении where. Например:

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

функция диапазон времени Hello — эквивалент tooa «where» предложение вставить после каждого указываются hello исходных таблиц.

`ago(3d)` означает "три дня назад". Другие единицы времени включают в себя часы (`2h`, `2.5h`), минуты (`25m`) и секунды (`10s`).

Другие примеры.

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

[Справочник по значениям даты и времени](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a>Оператор [Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): выбор, переименование и вычисление столбцов
Используйте [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out просто hello столбцы:

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

Также можно переименовать столбцы и определить новые:

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![result](./media/app-insights-analytics-tour/270.png)

* Имена столбцов могут содержать пробелы или символы, если они заключены в квадратные скобки: `['...']` или `["..."]`.
* `%`— hello обычные оператор остатка от деления.
* `1d` (т. е. цифра 1, а затем "d") — это литерал интервала времени, который означает один день. Вот еще несколько литералов интервала времени: `12h`, `30m`, `10s`, `0.01s`.
* `floor`(псевдоним `bin`) округляет значение вниз toohello ближайшего числа, кратного hello базового значения. Поэтому `floor(aTime, 1s)` округляет времени работы toohello ближайшего секунду.

Выражения могут включать все обычные операторы hello (`+`, `-`,...), и имеется ряд полезных функций.

## <a name="extend"></a>Extend
Используйте, если необходимо просто toohello столбцы tooadd существующих [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

С помощью [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) является менее подробной, чем [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) Если tookeep все hello существующих столбцов.

### <a name="convert-toolocal-time"></a>Преобразование времени toolocal

Метки времени всегда указываются в формате UTC. Поэтому если вы используете hello нам Тихоокеанский регион и является зимний, вы может следующим образом:

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a>Оператор [Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): агрегирование групп строк
`Summarize` применяет указанную *функцию агрегирования* для групп строк.

Например, hello веб-приложение принимает toorespond tooa запрос передается в поле hello `duration`. Давайте посмотрим, hello отклика запросов tooall времени:

![](./media/app-insights-analytics-tour/410.png)

Или может разделить результат hello в запросы разных имен:

![](./media/app-insights-analytics-tour/420.png)

`Summarize`Сбор данных о hello точек данных в потоке hello в группы, для которых hello `by` предложение одинаково. Каждое значение в hello `by` результатом выражения - имя каждой операции в hello в приведенном выше примере - строки в таблице результатов hello.

Или можно сгруппировать результаты по времени дня:

![](./media/app-insights-analytics-tour/430.png)

Обратите внимание на то, как мы используем hello `bin` функции (также называемого `floor`). Если бы мы использовали `by timestamp`, то каждая входная строка попала бы в небольшую отдельную группу. Для любого непрерывного скаляр like времени или чисел, у нас есть toobreak hello непрерывного диапазона в управляемую количество дискретных значений. `bin`— Это просто hello знакомы округление вниз `floor` функции — является наиболее простым способом toodo hello.

Мы используем hello и те же диапазоны метод tooreduce строк:

![](./media/app-insights-analytics-tour/440.png)

Обратите внимание, что можно использовать `name=` tooset hello имя результирующего столбца, либо в выражениях с агрегатными функциями hello или hello-BY.

## <a name="counting-sampled-data"></a>Подсчет данных выборки
`sum(itemCount)`является hello рекомендуется статистической обработки событий toocount. Во многих случаях itemCount == 1, поэтому функции hello просто подсчитывается hello количество строк в группе hello. Однако когда [выборки](app-insights-sampling.md) — в операции, лишь часть hello исходные события сохраняются в виде точки данных в Application Insights, таким образом, для каждой точки данных, вы видите, `itemCount` события.

Например, если выборка отменяет 75% от исходного события hello, а затем itemCount == 4 в записи сохраняются hello - то есть во всех зависимых записях присутствовали четыре исходной записи.

Адаптивная выборки приводит itemCount toobe выше периоды, когда приложение используется сильно.

Поэтому суммирования itemCount дает достоверной оценки hello исходное число событий.

![](./media/app-insights-analytics-tour/510.png)

Имеется также `count()` статистической обработки (и операции count), для случаев, где действительно toocount hello количество строк в группе.

Существует ряд [статистических функций](https://docs.loganalytics.io/learn/tutorials/aggregations.html).

## <a name="charting-hello-results"></a>Создание диаграмм результатов hello
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

По умолчанию результаты отображаются в виде таблицы:

![](./media/app-insights-analytics-tour/225.png)

Мы можем лучше, чем hello таблицы представления. Давайте рассмотрим результаты hello в представлении диаграммы hello с параметром вертикальная черта hello:

![Щелкните "Диаграмма", затем выберите "Вертикальная линейчатая диаграмма" и назначьте оси x и y.](./media/app-insights-analytics-tour/230.png)

Обратите внимание, что, несмотря на то что мы не выполняется сортировка hello результаты по времени (как видно в отображении hello таблицы), hello диаграммы всегда отображаются даты в правильном порядке.


## <a name="timecharts"></a>Временные диаграммы
Отображение количества событий, возникающих каждый час:

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

Выберите вариант отображения диаграммы hello:

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a>Множественные серии
Несколько выражений в hello `summarize` предложение создает несколько столбцов.

Несколько выражений в hello `by` предложение создает несколько строк, по одному для каждого сочетания значений.

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Запросы к таблицам по часу и расположению](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a>Разделение диаграммы по показателям
Если диаграммы таблицы, которая имеет строковый столбец и числовой столбец, строка hello можно использовать toosplit hello числовых данных в отдельные ряды точек. Если имеется более одного столбца для строки, можно выбрать какие toouse столбец как hello дискриминатора.

![Разделение диаграммы аналитики](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a>Частота возвращения

Преобразовать строку логическое tooa toouse его как дискриминатор:

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a>Отображение нескольких метрик
Если вы диаграммы, таблицы, которая имеет более одного числового столбца, в добавление toohello timestamp, можно отобразить любое их сочетание.

![Разделение диаграммы аналитики](./media/app-insights-analytics-tour/110.png)

Чтобы выбрать несколько столбцов числового типа, щелкните **Don't Split** (Не разделять). Вы не удается разделить, строковый столбец в hello же времени, как отображение более чем одного числового столбца.

## <a name="daily-average-cycle"></a>Ежедневный средний цикл
Как использование отличаться за день Среднее hello

Число запросов на по времени hello остаток от деления одного дня разбиты на часы:

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![Линейчатая диаграмма часов для среднего дня](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> Обратите внимание, что в настоящее время имеется tooconvert время длительности toodatetimes в порядке toodisplay на графике.
>
>

## <a name="compare-multiple-daily-series"></a>Сравнение серий для нескольких дней
Как использование изменяться со временем hello дня в разных странах?

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![Разделение по client_CountryOrRegion](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a>Построение графика распределения
Какое количество сеансов различной длительности существует?

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

Последняя строка Hello является обязательным tooconvert toodatetime. В настоящее время hello x ось диаграммы отображаются в виде скалярного только в том случае, если это значение datetime.

Hello `where` предложение исключает одноразовой сеансов (sessionDuration == 0) и наборы hello, длина hello оси x.

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[Процентили](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
Какие диапазоны длительности покрывают различные процентные доли сеансов?

Использовать hello выше запрос, но заменить последнюю строку hello:

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

Также мы удалили hello верхнего предела в hello, где предложение в порядке tooget исправить данные, включая все сеансы с более одного запроса:

![result](./media/app-insights-analytics-tour/180.png)

Из полученных результатов мы видим следующее:

* 5 % сеансов имеют продолжительность менее 3 минут 34 секунд;
* 50 % сеансов имеют продолжительность менее 36 минут;
* 5 % сеансов имеют продолжительность более 7 дней.

tooget отдельные подразделение для каждой страны, мы просто иметь toobring hello client_CountryOrRegion столбец отдельно с помощью обоих суммировать операторы:

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a>Объединение
У нас есть tooseveral доступа к таблицам, включая запросы и исключения.

toofind hello исключения связанные tooa запрос, который вернул ошибочный ответ, мы присоединить hello таблиц на `session_Id`:

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


Это хороший способ toouse `project` tooselect просто hello столбцы необходимы, прежде чем выполнять hello соединения.
В hello же предложения, мы переименовать столбец отметки времени hello.

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a>[Разрешить](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): присвоить значение переменной результата tooa

Используйте `let` tooseparate hello части hello предшествующего выражения. результаты Hello ничем не отличаются:

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> В клиенте Analytics hello не следует размещать пустые строки между hello части запроса hello. Убедитесь, что tooexecute все его.
>

Используйте `toscalar` tooconvert значение tooa одной таблицы ячейки:

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a>Функции

Используйте *позволить* toodefine функции:

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a>Доступ к вложенным объектам
Доступ к вложенным объектам осуществляется легко. Например поток hello исключения можно увидеть структурированных объектов следующим образом:

![result](./media/app-insights-analytics-tour/520.png)

Можно выполнить сведение его, выбрав свойства hello интересующую вас:

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

Обратите внимание, что соответствующий тип результата hello toohello toocast.


## <a name="custom-properties-and-measurements"></a>Пользовательские свойства и измерения
Если приложение подключается [пользовательские измерения (свойства) и пользовательских измерений](app-insights-api-custom-events-metrics.md#properties) tooevents, то они будут отображены в hello `customDimensions` и `customMeasurements` объектов.

Например, если приложение включает в себя:

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

tooextract эти значения в аналитике:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

tooverify ли пользовательские измерение является определенного типа:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a>Панели мониторинга
Можно закрепить панель мониторинга tooa результаты в порядке toobring вместе всех важнейших диаграмм и таблиц.

* [Панель мониторинга Azure общего](app-insights-dashboards.md#share-dashboards): щелкните значок булавки hello. Для этого необходимо иметь панель мониторинга, открытую для совместного использования. В hello портал Azure откройте или создайте панель мониторинга и выберите общий ресурс.
* [Панель мониторинга Power BI](app-insights-export-power-bi.md). Щелкните "Экспорт" > "Запрос Power BI". Преимущество этого способа состоит в том, что можно отобразить запрос вместе с другими результатами из множества источников.

## <a name="combine-with-imported-data"></a>Объединение с импортированными данными

Аналитика отчеты выглядят на панели мониторинга hello, но иногда может потребоваться tooa данных hello tootranslate дополнительные снизилось формы. Например предположим, что прошедшие проверку подлинности пользователи идентифицируются псевдоним в телеметрии hello. Вы хотите их реального имена tooshow в результатах. toodo, необходимые для сопоставления hello псевдонимы toohello реальные имена CSV-файл.

Можно импортировать файл данных и использовать его так же, как и любой из стандартных таблиц hello (запросы, исключения и т. д.). Можно выполнять запросы к такой таблице отдельно либо соединить ее с другими таблицами. Например, если у вас есть таблица с именем сопоставления пользователей и она содержит столбцы `realName` и `userId`, его можно будет использовать tootranslate hello `user_AuthenticatedId` в телеметрии hello запроса:

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

tooimport с таблицей, в колонке схемы hello под **другие источники данных**, выполните инструкции hello tooadd новый источник данных, загрузив образец данных. Затем можно использовать таблицы tooupload этого определения.

Hello импорта компонент в настоящий момент в предварительной версии, поэтому изначально появится ссылка «Свяжитесь с нами» в группе «Других источников данных». Используйте этот toosign копирование toohello предварительной версии программы и hello связи, затем заменяется кнопка «Добавить новый источник данных».


## <a name="tables"></a>Таблицы
поток данных телеметрии, полученных из приложения Hello доступен через несколько таблиц. схемы Hello свойств, доступных для каждой таблицы отображается в левой части hello окна hello.

### <a name="requests-table"></a>Таблица запросов
Количество HTTP запрашивает tooyour веб-приложения и сегмент, имя страницы:

![Число запросов, сегментированных по имени](./media/app-insights-analytics-tour/analytics-count-requests.png)

Найти hello запросов, завершенных большинство:

![Число запросов, сегментированных по имени](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a>Таблица настраиваемых событий
Если вы используете [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend собственные события, которые можно читать из этой таблицы.

Рассмотрим пример, в котором код вашего приложения содержит следующие строки.

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

Частота hello отображения этих событий:

![Частота отображения пользовательских событий](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

Извлечь показателей и измерений из hello событий:

![Частота отображения пользовательских событий](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a>Таблица настраиваемых метрик
Если вы используете [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend собственные значения метрики вы найдете его результаты в hello **customMetrics** потока. Например:  

![Настраиваемые метрики в аналитике Application Insights](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> В [обозревателя метрик](app-insights-metrics-explorer.md), все пользовательские измерения tooany вложенный тип телеметрии появляются вместе в колонке hello метрик и метрик, отправляемых с помощью `TrackMetric()`. Но в аналитику, настраиваемые измерения, по-прежнему присоединенного toowhichever тип телеметрии, они были перенесены на - события или запросы и т. д. — из-за метрики, отправленных TrackMetric отображаются в своих собственных потока.
>
>

### <a name="performance-counters-table"></a>Таблица счетчиков производительности
[Счетчики производительности](app-insights-performance-counters.md) показывают базовые системные метрики для вашего приложения, такие как использование ресурсов ЦП, памяти и сети. Вы можете настроить hello SDK toosend Дополнительные счетчики, включая собственные пользовательские счетчики.

Hello **performanceCounters** схема предоставляет hello `category`, `counter` имя, и `instance` имя каждого счетчика производительности. Имена экземпляров счетчиков являются только применимые toosome счетчики производительности и обычно указывают, что относится имя hello числа hello toowhich hello. Hello данные телеметрии для каждого приложения вы увидите только hello счетчики для этого приложения. Например, toosee какие счетчики доступны:

![Счетчики производительности в аналитике Application Insights](./media/app-insights-analytics-tour/analytics-performance-counters.png)

tooget диаграммы доступной памяти через hello выбранный период:

![Временная диаграмма памяти в аналитике Application Insights](./media/app-insights-analytics-tour/analytics-available-memory.png)

Как и другие данные телеметрии **performanceCounters** также есть столбец `cloud_RoleInstance` указывает удостоверение hello hello хост-компьютера, на котором выполняется приложение. Например toocompare hello производительности приложения на разных компьютерах hello:

![Производительность, сегментированная по экземпляру роли в аналитике Application Insights](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a>Таблица исключений
В этой таблице доступны [исключения, выданные вашим приложением](app-insights-asp-net-exceptions.md).

toofind Здравствуйте HTTP-запросе, приложение обрабатывало при возникновении исключения hello, присоединение в operation_Id:

![Соединение исключений с запросами по operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a>Таблица временных параметров браузера
`browserTimings` показывает данные о загрузке страниц, собранных в браузерах пользователей.

[Настройка приложения для стороны клиента телеметрии](app-insights-javascript.md) чтобы toosee этих показателей.

Схема Hello включает [метрики, указывающее, hello длин разные этапы процесса загрузки страницы приветствия](app-insights-javascript.md#page-load-performance). (Они не указывают hello продолжительность пользователям чтение страницы).  

Показать popularities hello разных страниц и время для каждой страницы загрузки:

![Время загрузки страниц в аналитике](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a>Таблица результатов тестов доступности
`availabilityResults`Здравствуйте, показаны результаты вашей [веб-тестов](app-insights-monitor-web-app-availability.md). Каждое выполнение тестов в каком-либо расположении тестирования регистрируется отдельно.

![Время загрузки страниц в аналитике](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a>Таблица зависимостей
Содержит результаты вызовов, что приложение делает toodatabases и API-интерфейс REST и другие вызывает tooTrackDependency(). Также включает вызовы AJAX из браузера hello.

Вызовы AJAX из браузера hello:

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

Вызовы зависимостей с сервера hello:

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

Серверные зависимости всегда отображает `success==False` Если hello не установлен агент аналитики приложений. Однако hello другие данные указаны правильно.

### <a name="traces-table"></a>Таблица трассировок
Содержит hello телеметрии, отправленные приложения с помощью TrackTrace(), или [других платформ ведения журналов](app-insights-asp-net-trace-logs.md).

## <a name="video"></a>Видео 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

Расширенные запросы:

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a>Дальнейшие действия
* [Справочные материалы по аналитике](app-insights-analytics-reference.md)
* [SQL-пользователей Памятка](https://aka.ms/sql-analytics) преобразует наиболее общих идиом hello.

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
