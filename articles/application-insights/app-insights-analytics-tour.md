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
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="360e9-103">Знакомство с аналитикой в Application Insights</span><span class="sxs-lookup"><span data-stu-id="360e9-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="360e9-104">[Аналитика](app-insights-analytics.md) — мощное средство поиска функция hello [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="360e9-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="360e9-105">На этих страницах описан язык запросов Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="360e9-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="360e9-106">**[Вводное видео hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="360e9-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="360e9-107">**[Испытайте аналитика на нашем смоделированные данные](https://analytics.applicationinsights.io/demo)**  Если ваше приложение еще не отправляет данные tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="360e9-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="360e9-108">**[SQL-пользователей Памятка](https://aka.ms/sql-analytics)**  преобразует наиболее общих идиом hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>

<span data-ttu-id="360e9-109">Давайте пошагового tooget некоторых простых запросов, которого вы начали.</span><span class="sxs-lookup"><span data-stu-id="360e9-109">Let's take a walk through some basic queries tooget you started.</span></span>

## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="360e9-110">Подключение к данным tooyour Application Insights</span><span class="sxs-lookup"><span data-stu-id="360e9-110">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="360e9-111">Откройте аналитику в [колонке "Обзор"](app-insights-dashboards.md) приложения в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="360e9-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![На сайте portal.azure.com откройте ресурс Application Insights и щелкните "Аналитика".](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="360e9-113">Оператор [take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): отображение n строк</span><span class="sxs-lookup"><span data-stu-id="360e9-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="360e9-114">Точки данных, регистрирующие операции пользователя (обычно HTTP-запросы, полученные веб-приложением), хранятся в таблице `requests`.</span><span class="sxs-lookup"><span data-stu-id="360e9-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="360e9-115">Каждая строка является точки данных телеметрии, полученных от hello пакет SDK Application Insights в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="360e9-115">Each row is a telemetry data point received from hello Application Insights SDK in your app.</span></span>

<span data-ttu-id="360e9-116">Начнем с изучения несколько образцов строк таблицы hello:</span><span class="sxs-lookup"><span data-stu-id="360e9-116">Let's start by examining a few sample rows of hello table:</span></span>

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="360e9-118">Поместите курсор hello где-нибудь в инструкции hello пока ты.</span><span class="sxs-lookup"><span data-stu-id="360e9-118">Put hello cursor somewhere in hello statement before you click Go.</span></span> <span data-ttu-id="360e9-119">Инструкцию можно разделить на несколько строк, но она не должна содержать пустых строк.</span><span class="sxs-lookup"><span data-stu-id="360e9-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="360e9-120">Пустые строки — это удобный способ tookeep некоторые отдельные запросы в окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="360e9-120">Blank lines are a convenient way tookeep several separate queries in hello window.</span></span>
>
>

<span data-ttu-id="360e9-121">Выберите нужные столбцы, перетащите их, чтобы cгруппировать, и примените фильтр:</span><span class="sxs-lookup"><span data-stu-id="360e9-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Выберите столбец в правом верхнем углу результатов.](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="360e9-123">Разверните ни элемент toosee hello сведения:</span><span class="sxs-lookup"><span data-stu-id="360e9-123">Expand any item toosee hello detail:</span></span>

![Выберите "Таблица", а затем "Настроить столбцы".](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="360e9-125">Щелкните заголовок столбца порядок toore hello доступных результатов в веб-браузере hello hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-125">Click hello head of a column toore-order hello results available in hello web browser.</span></span> <span data-ttu-id="360e9-126">Но имейте в виду, что для большой результирующий набор, количество hello браузера загруженный toohello строк ограничено.</span><span class="sxs-lookup"><span data-stu-id="360e9-126">But be aware that for a large result set, hello number of rows downloaded toohello browser is limited.</span></span> <span data-ttu-id="360e9-127">Сортировка таким образом не всегда показывает hello фактическое высокий или низкого уровня элементов.</span><span class="sxs-lookup"><span data-stu-id="360e9-127">Sorting this way doesn't always show you hello actual highest or lowest items.</span></span> <span data-ttu-id="360e9-128">элементы toosort надежно и использовать hello `top` или `sort` оператор.</span><span class="sxs-lookup"><span data-stu-id="360e9-128">toosort items reliably, use hello `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="360e9-129">Операторы [top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) и [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="360e9-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="360e9-130">`take`является полезным tooget краткий пример результата, но он демонстрирует строки из таблицы hello в произвольном порядке.</span><span class="sxs-lookup"><span data-stu-id="360e9-130">`take` is useful tooget a quick sample of a result, but it shows rows from hello table in no particular order.</span></span> <span data-ttu-id="360e9-131">использовать tooget упорядоченное представление `top` (пример) или `sort` (через hello всю таблицу).</span><span class="sxs-lookup"><span data-stu-id="360e9-131">tooget an ordered view, use `top` (for a sample) or `sort` (over hello whole table).</span></span>

<span data-ttu-id="360e9-132">Показать hello первые n строк, упорядоченных по определенному столбцу:</span><span class="sxs-lookup"><span data-stu-id="360e9-132">Show me hello first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="360e9-133">*Синтаксис*. У большинства операторов есть параметры в виде ключевых слов, такие как `by`.</span><span class="sxs-lookup"><span data-stu-id="360e9-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="360e9-134">`desc` — по убыванию, `asc` — по возрастанию.</span><span class="sxs-lookup"><span data-stu-id="360e9-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="360e9-135">`top...` является более производительным способом выполнения `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="360e9-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="360e9-136">Можно было бы написать следующее:</span><span class="sxs-lookup"><span data-stu-id="360e9-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="360e9-137">Hello получим hello таким же, но оно будет выполняться немного медленнее.</span><span class="sxs-lookup"><span data-stu-id="360e9-137">hello result would be hello same, but it would run a bit more slowly.</span></span> <span data-ttu-id="360e9-138">(Также можно написать `order`, это псевдоним `sort`).</span><span class="sxs-lookup"><span data-stu-id="360e9-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="360e9-139">Hello заголовки столбцов в представлении таблицы hello также можно использовать toosort hello результатов на экране приветствия.</span><span class="sxs-lookup"><span data-stu-id="360e9-139">hello column headers in hello table view can also be used toosort hello results on hello screen.</span></span> <span data-ttu-id="360e9-140">Но, разумеется, если вы использовали `take` или `top` tooretrieve только его часть таблицы будет только изменить порядок hello записи извлеченным.</span><span class="sxs-lookup"><span data-stu-id="360e9-140">But of course, if you've used `take` or `top` tooretrieve just part of a table, you'll only re-order hello records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="360e9-141">Оператор [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): фильтрация по условию</span><span class="sxs-lookup"><span data-stu-id="360e9-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="360e9-142">Давайте отобразим только запросы, вернувшие конкретный код результата.</span><span class="sxs-lookup"><span data-stu-id="360e9-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="360e9-143">Hello `where` оператор принимает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="360e9-143">hello `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="360e9-144">Ниже приведены некоторые ключевые моменты:</span><span class="sxs-lookup"><span data-stu-id="360e9-144">Here are some key points about them:</span></span>

* <span data-ttu-id="360e9-145">`and`, `or`: логические операторы;</span><span class="sxs-lookup"><span data-stu-id="360e9-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="360e9-146">`==`, `<>`, `!=`: равно и не равно;</span><span class="sxs-lookup"><span data-stu-id="360e9-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="360e9-147">`=~`, `!~`: равенство и неравенство строк без учета регистра.</span><span class="sxs-lookup"><span data-stu-id="360e9-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="360e9-148">Существует множество других операторов сравнения строк.</span><span class="sxs-lookup"><span data-stu-id="360e9-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a><span data-ttu-id="360e9-149">Получение подходящего типа hello</span><span class="sxs-lookup"><span data-stu-id="360e9-149">Getting hello right type</span></span>
<span data-ttu-id="360e9-150">Поиск неудачных запросов:</span><span class="sxs-lookup"><span data-stu-id="360e9-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="360e9-151">Время</span><span class="sxs-lookup"><span data-stu-id="360e9-151">Time</span></span>

<span data-ttu-id="360e9-152">По умолчанию запросы являются ограниченными toohello последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="360e9-152">By default, your queries are restricted toohello last 24 hours.</span></span> <span data-ttu-id="360e9-153">Этот интервал можно изменить.</span><span class="sxs-lookup"><span data-stu-id="360e9-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="360e9-154">Переопределить hello временной диапазон, написав любой запрос, в которой указывается `timestamp` в предложении where.</span><span class="sxs-lookup"><span data-stu-id="360e9-154">Override hello time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="360e9-155">Например:</span><span class="sxs-lookup"><span data-stu-id="360e9-155">For example:</span></span>

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

<span data-ttu-id="360e9-156">функция диапазон времени Hello — эквивалент tooa «where» предложение вставить после каждого указываются hello исходных таблиц.</span><span class="sxs-lookup"><span data-stu-id="360e9-156">hello time range feature is equivalent tooa 'where' clause inserted after each mention of one of hello source tables.</span></span>

<span data-ttu-id="360e9-157">`ago(3d)` означает "три дня назад".</span><span class="sxs-lookup"><span data-stu-id="360e9-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="360e9-158">Другие единицы времени включают в себя часы (`2h`, `2.5h`), минуты (`25m`) и секунды (`10s`).</span><span class="sxs-lookup"><span data-stu-id="360e9-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="360e9-159">Другие примеры.</span><span class="sxs-lookup"><span data-stu-id="360e9-159">Other examples:</span></span>

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

<span data-ttu-id="360e9-160">[Справочник по значениям даты и времени](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="360e9-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="360e9-161">Оператор [Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): выбор, переименование и вычисление столбцов</span><span class="sxs-lookup"><span data-stu-id="360e9-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="360e9-162">Используйте [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out просто hello столбцы:</span><span class="sxs-lookup"><span data-stu-id="360e9-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out just hello columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="360e9-163">Также можно переименовать столбцы и определить новые:</span><span class="sxs-lookup"><span data-stu-id="360e9-163">You can also rename columns and define new ones:</span></span>

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

* <span data-ttu-id="360e9-165">Имена столбцов могут содержать пробелы или символы, если они заключены в квадратные скобки: `['...']` или `["..."]`.</span><span class="sxs-lookup"><span data-stu-id="360e9-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="360e9-166">`%`— hello обычные оператор остатка от деления.</span><span class="sxs-lookup"><span data-stu-id="360e9-166">`%` is hello usual modulo operator.</span></span>
* <span data-ttu-id="360e9-167">`1d` (т. е. цифра 1, а затем "d") — это литерал интервала времени, который означает один день.</span><span class="sxs-lookup"><span data-stu-id="360e9-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="360e9-168">Вот еще несколько литералов интервала времени: `12h`, `30m`, `10s`, `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="360e9-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="360e9-169">`floor`(псевдоним `bin`) округляет значение вниз toohello ближайшего числа, кратного hello базового значения.</span><span class="sxs-lookup"><span data-stu-id="360e9-169">`floor` (alias `bin`) rounds a value down toohello nearest multiple of hello base value you provide.</span></span> <span data-ttu-id="360e9-170">Поэтому `floor(aTime, 1s)` округляет времени работы toohello ближайшего секунду.</span><span class="sxs-lookup"><span data-stu-id="360e9-170">So `floor(aTime, 1s)` rounds a time down toohello nearest second.</span></span>

<span data-ttu-id="360e9-171">Выражения могут включать все обычные операторы hello (`+`, `-`,...), и имеется ряд полезных функций.</span><span class="sxs-lookup"><span data-stu-id="360e9-171">Expressions can include all hello usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="360e9-172">Extend</span><span class="sxs-lookup"><span data-stu-id="360e9-172">Extend</span></span>
<span data-ttu-id="360e9-173">Используйте, если необходимо просто toohello столбцы tooadd существующих [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="360e9-173">If you just want tooadd columns toohello existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="360e9-174">С помощью [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) является менее подробной, чем [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) Если tookeep все hello существующих столбцов.</span><span class="sxs-lookup"><span data-stu-id="360e9-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want tookeep all hello existing columns.</span></span>

### <a name="convert-toolocal-time"></a><span data-ttu-id="360e9-175">Преобразование времени toolocal</span><span class="sxs-lookup"><span data-stu-id="360e9-175">Convert toolocal time</span></span>

<span data-ttu-id="360e9-176">Метки времени всегда указываются в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="360e9-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="360e9-177">Поэтому если вы используете hello нам Тихоокеанский регион и является зимний, вы может следующим образом:</span><span class="sxs-lookup"><span data-stu-id="360e9-177">So if you're on hello US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="360e9-178">Оператор [Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): агрегирование групп строк</span><span class="sxs-lookup"><span data-stu-id="360e9-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="360e9-179">`Summarize` применяет указанную *функцию агрегирования* для групп строк.</span><span class="sxs-lookup"><span data-stu-id="360e9-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="360e9-180">Например, hello веб-приложение принимает toorespond tooa запрос передается в поле hello `duration`.</span><span class="sxs-lookup"><span data-stu-id="360e9-180">For example, hello time your web app takes toorespond tooa request is reported in hello field `duration`.</span></span> <span data-ttu-id="360e9-181">Давайте посмотрим, hello отклика запросов tooall времени:</span><span class="sxs-lookup"><span data-stu-id="360e9-181">Let's see hello average response time tooall requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="360e9-182">Или может разделить результат hello в запросы разных имен:</span><span class="sxs-lookup"><span data-stu-id="360e9-182">Or we could separate hello result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="360e9-183">`Summarize`Сбор данных о hello точек данных в потоке hello в группы, для которых hello `by` предложение одинаково.</span><span class="sxs-lookup"><span data-stu-id="360e9-183">`Summarize` collects hello data points in hello stream into groups for which hello `by` clause evaluates equally.</span></span> <span data-ttu-id="360e9-184">Каждое значение в hello `by` результатом выражения - имя каждой операции в hello в приведенном выше примере - строки в таблице результатов hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-184">Each value in hello `by` expression - each operation name in hello above example - results in a row in hello result table.</span></span>

<span data-ttu-id="360e9-185">Или можно сгруппировать результаты по времени дня:</span><span class="sxs-lookup"><span data-stu-id="360e9-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="360e9-186">Обратите внимание на то, как мы используем hello `bin` функции (также называемого `floor`).</span><span class="sxs-lookup"><span data-stu-id="360e9-186">Notice how we're using hello `bin` function (aka `floor`).</span></span> <span data-ttu-id="360e9-187">Если бы мы использовали `by timestamp`, то каждая входная строка попала бы в небольшую отдельную группу.</span><span class="sxs-lookup"><span data-stu-id="360e9-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="360e9-188">Для любого непрерывного скаляр like времени или чисел, у нас есть toobreak hello непрерывного диапазона в управляемую количество дискретных значений.</span><span class="sxs-lookup"><span data-stu-id="360e9-188">For any continuous scalar like times or numbers, we have toobreak hello continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="360e9-189">`bin`— Это просто hello знакомы округление вниз `floor` функции — является наиболее простым способом toodo hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-189">`bin` - which is just hello familiar rounding-down `floor` function - is hello easiest way toodo that.</span></span>

<span data-ttu-id="360e9-190">Мы используем hello и те же диапазоны метод tooreduce строк:</span><span class="sxs-lookup"><span data-stu-id="360e9-190">We can use hello same technique tooreduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="360e9-191">Обратите внимание, что можно использовать `name=` tooset hello имя результирующего столбца, либо в выражениях с агрегатными функциями hello или hello-BY.</span><span class="sxs-lookup"><span data-stu-id="360e9-191">Notice that you can use `name=` tooset hello name of a result column, either in hello aggregation expressions or hello by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="360e9-192">Подсчет данных выборки</span><span class="sxs-lookup"><span data-stu-id="360e9-192">Counting sampled data</span></span>
<span data-ttu-id="360e9-193">`sum(itemCount)`является hello рекомендуется статистической обработки событий toocount.</span><span class="sxs-lookup"><span data-stu-id="360e9-193">`sum(itemCount)` is hello recommended aggregation toocount events.</span></span> <span data-ttu-id="360e9-194">Во многих случаях itemCount == 1, поэтому функции hello просто подсчитывается hello количество строк в группе hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-194">In many cases, itemCount==1, so hello function simply counts up hello number of rows in hello group.</span></span> <span data-ttu-id="360e9-195">Однако когда [выборки](app-insights-sampling.md) — в операции, лишь часть hello исходные события сохраняются в виде точки данных в Application Insights, таким образом, для каждой точки данных, вы видите, `itemCount` события.</span><span class="sxs-lookup"><span data-stu-id="360e9-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of hello original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="360e9-196">Например, если выборка отменяет 75% от исходного события hello, а затем itemCount == 4 в записи сохраняются hello - то есть во всех зависимых записях присутствовали четыре исходной записи.</span><span class="sxs-lookup"><span data-stu-id="360e9-196">For example, if sampling discards 75% of hello original events, then itemCount==4 in hello retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="360e9-197">Адаптивная выборки приводит itemCount toobe выше периоды, когда приложение используется сильно.</span><span class="sxs-lookup"><span data-stu-id="360e9-197">Adaptive sampling causes itemCount toobe higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="360e9-198">Поэтому суммирования itemCount дает достоверной оценки hello исходное число событий.</span><span class="sxs-lookup"><span data-stu-id="360e9-198">Summing up itemCount therefore gives a good estimate of hello original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="360e9-199">Имеется также `count()` статистической обработки (и операции count), для случаев, где действительно toocount hello количество строк в группе.</span><span class="sxs-lookup"><span data-stu-id="360e9-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want toocount hello number of rows in a group.</span></span>

<span data-ttu-id="360e9-200">Существует ряд [статистических функций](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="360e9-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-hello-results"></a><span data-ttu-id="360e9-201">Создание диаграмм результатов hello</span><span class="sxs-lookup"><span data-stu-id="360e9-201">Charting hello results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="360e9-202">По умолчанию результаты отображаются в виде таблицы:</span><span class="sxs-lookup"><span data-stu-id="360e9-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="360e9-203">Мы можем лучше, чем hello таблицы представления.</span><span class="sxs-lookup"><span data-stu-id="360e9-203">We can do better than hello table view.</span></span> <span data-ttu-id="360e9-204">Давайте рассмотрим результаты hello в представлении диаграммы hello с параметром вертикальная черта hello:</span><span class="sxs-lookup"><span data-stu-id="360e9-204">Let's look at hello results in hello chart view with hello vertical bar option:</span></span>

![Щелкните "Диаграмма", затем выберите "Вертикальная линейчатая диаграмма" и назначьте оси x и y.](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="360e9-206">Обратите внимание, что, несмотря на то что мы не выполняется сортировка hello результаты по времени (как видно в отображении hello таблицы), hello диаграммы всегда отображаются даты в правильном порядке.</span><span class="sxs-lookup"><span data-stu-id="360e9-206">Notice that although we didn't sort hello results by time (as you can see in hello table display), hello chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="360e9-207">Временные диаграммы</span><span class="sxs-lookup"><span data-stu-id="360e9-207">Timecharts</span></span>
<span data-ttu-id="360e9-208">Отображение количества событий, возникающих каждый час:</span><span class="sxs-lookup"><span data-stu-id="360e9-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="360e9-209">Выберите вариант отображения диаграммы hello:</span><span class="sxs-lookup"><span data-stu-id="360e9-209">Select hello Chart display option:</span></span>

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="360e9-211">Множественные серии</span><span class="sxs-lookup"><span data-stu-id="360e9-211">Multiple series</span></span>
<span data-ttu-id="360e9-212">Несколько выражений в hello `summarize` предложение создает несколько столбцов.</span><span class="sxs-lookup"><span data-stu-id="360e9-212">Multiple expressions in hello `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="360e9-213">Несколько выражений в hello `by` предложение создает несколько строк, по одному для каждого сочетания значений.</span><span class="sxs-lookup"><span data-stu-id="360e9-213">Multiple expressions in hello `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Запросы к таблицам по часу и расположению](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="360e9-215">Разделение диаграммы по показателям</span><span class="sxs-lookup"><span data-stu-id="360e9-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="360e9-216">Если диаграммы таблицы, которая имеет строковый столбец и числовой столбец, строка hello можно использовать toosplit hello числовых данных в отдельные ряды точек.</span><span class="sxs-lookup"><span data-stu-id="360e9-216">If you chart a table that has a string column and a numeric column, hello string can be used toosplit hello numeric data into separate series of points.</span></span> <span data-ttu-id="360e9-217">Если имеется более одного столбца для строки, можно выбрать какие toouse столбец как hello дискриминатора.</span><span class="sxs-lookup"><span data-stu-id="360e9-217">If there's more than one string column, you can choose which column toouse as hello discriminator.</span></span>

![Разделение диаграммы аналитики](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="360e9-219">Частота возвращения</span><span class="sxs-lookup"><span data-stu-id="360e9-219">Bounce rate</span></span>

<span data-ttu-id="360e9-220">Преобразовать строку логическое tooa toouse его как дискриминатор:</span><span class="sxs-lookup"><span data-stu-id="360e9-220">Convert a boolean tooa string toouse it as a discriminator:</span></span>

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

### <a name="display-multiple-metrics"></a><span data-ttu-id="360e9-221">Отображение нескольких метрик</span><span class="sxs-lookup"><span data-stu-id="360e9-221">Display multiple metrics</span></span>
<span data-ttu-id="360e9-222">Если вы диаграммы, таблицы, которая имеет более одного числового столбца, в добавление toohello timestamp, можно отобразить любое их сочетание.</span><span class="sxs-lookup"><span data-stu-id="360e9-222">If you chart a table that has more than one numeric column, in addition toohello timestamp, you can display any combination of them.</span></span>

![Разделение диаграммы аналитики](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="360e9-224">Чтобы выбрать несколько столбцов числового типа, щелкните **Don't Split** (Не разделять).</span><span class="sxs-lookup"><span data-stu-id="360e9-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="360e9-225">Вы не удается разделить, строковый столбец в hello же времени, как отображение более чем одного числового столбца.</span><span class="sxs-lookup"><span data-stu-id="360e9-225">You can't split by a string column at hello same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="360e9-226">Ежедневный средний цикл</span><span class="sxs-lookup"><span data-stu-id="360e9-226">Daily average cycle</span></span>
<span data-ttu-id="360e9-227">Как использование отличаться за день Среднее hello</span><span class="sxs-lookup"><span data-stu-id="360e9-227">How does usage vary over hello average day?</span></span>

<span data-ttu-id="360e9-228">Число запросов на по времени hello остаток от деления одного дня разбиты на часы:</span><span class="sxs-lookup"><span data-stu-id="360e9-228">Count requests by hello time modulo one day, binned into hours:</span></span>

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
> <span data-ttu-id="360e9-230">Обратите внимание, что в настоящее время имеется tooconvert время длительности toodatetimes в порядке toodisplay на графике.</span><span class="sxs-lookup"><span data-stu-id="360e9-230">Notice that we currently have tooconvert time durations toodatetimes in order toodisplay on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="360e9-231">Сравнение серий для нескольких дней</span><span class="sxs-lookup"><span data-stu-id="360e9-231">Compare multiple daily series</span></span>
<span data-ttu-id="360e9-232">Как использование изменяться со временем hello дня в разных странах?</span><span class="sxs-lookup"><span data-stu-id="360e9-232">How does usage vary over hello time of day in different countries?</span></span>

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

## <a name="plot-a-distribution"></a><span data-ttu-id="360e9-234">Построение графика распределения</span><span class="sxs-lookup"><span data-stu-id="360e9-234">Plot a distribution</span></span>
<span data-ttu-id="360e9-235">Какое количество сеансов различной длительности существует?</span><span class="sxs-lookup"><span data-stu-id="360e9-235">How many sessions are there of different lengths?</span></span>

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

<span data-ttu-id="360e9-236">Последняя строка Hello является обязательным tooconvert toodatetime.</span><span class="sxs-lookup"><span data-stu-id="360e9-236">hello last line is required tooconvert toodatetime.</span></span> <span data-ttu-id="360e9-237">В настоящее время hello x ось диаграммы отображаются в виде скалярного только в том случае, если это значение datetime.</span><span class="sxs-lookup"><span data-stu-id="360e9-237">Currently hello x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="360e9-238">Hello `where` предложение исключает одноразовой сеансов (sessionDuration == 0) и наборы hello, длина hello оси x.</span><span class="sxs-lookup"><span data-stu-id="360e9-238">hello `where` clause excludes one-shot sessions (sessionDuration==0) and sets hello length of hello x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="360e9-239">Процентили</span><span class="sxs-lookup"><span data-stu-id="360e9-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="360e9-240">Какие диапазоны длительности покрывают различные процентные доли сеансов?</span><span class="sxs-lookup"><span data-stu-id="360e9-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="360e9-241">Использовать hello выше запрос, но заменить последнюю строку hello:</span><span class="sxs-lookup"><span data-stu-id="360e9-241">Use hello above query, but replace hello last line:</span></span>

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

<span data-ttu-id="360e9-242">Также мы удалили hello верхнего предела в hello, где предложение в порядке tooget исправить данные, включая все сеансы с более одного запроса:</span><span class="sxs-lookup"><span data-stu-id="360e9-242">We also removed hello upper limit in hello where clause, in order tooget correct figures including all sessions with more than one request:</span></span>

![result](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="360e9-244">Из полученных результатов мы видим следующее:</span><span class="sxs-lookup"><span data-stu-id="360e9-244">From which we can see that:</span></span>

* <span data-ttu-id="360e9-245">5 % сеансов имеют продолжительность менее 3 минут 34 секунд;</span><span class="sxs-lookup"><span data-stu-id="360e9-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="360e9-246">50 % сеансов имеют продолжительность менее 36 минут;</span><span class="sxs-lookup"><span data-stu-id="360e9-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="360e9-247">5 % сеансов имеют продолжительность более 7 дней.</span><span class="sxs-lookup"><span data-stu-id="360e9-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="360e9-248">tooget отдельные подразделение для каждой страны, мы просто иметь toobring hello client_CountryOrRegion столбец отдельно с помощью обоих суммировать операторы:</span><span class="sxs-lookup"><span data-stu-id="360e9-248">tooget a separate breakdown for each country, we just have toobring hello client_CountryOrRegion column separately through both summarize operators:</span></span>

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

## <a name="join"></a><span data-ttu-id="360e9-249">Объединение</span><span class="sxs-lookup"><span data-stu-id="360e9-249">Join</span></span>
<span data-ttu-id="360e9-250">У нас есть tooseveral доступа к таблицам, включая запросы и исключения.</span><span class="sxs-lookup"><span data-stu-id="360e9-250">We have access tooseveral tables, including requests and exceptions.</span></span>

<span data-ttu-id="360e9-251">toofind hello исключения связанные tooa запрос, который вернул ошибочный ответ, мы присоединить hello таблиц на `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="360e9-251">toofind hello exceptions related tooa request that returned a failure response, we can join hello tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="360e9-252">Это хороший способ toouse `project` tooselect просто hello столбцы необходимы, прежде чем выполнять hello соединения.</span><span class="sxs-lookup"><span data-stu-id="360e9-252">It's good practice toouse `project` tooselect just hello columns we need before performing hello join.</span></span>
<span data-ttu-id="360e9-253">В hello же предложения, мы переименовать столбец отметки времени hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-253">In hello same clauses, we rename hello timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a><span data-ttu-id="360e9-254">[Разрешить](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): присвоить значение переменной результата tooa</span><span class="sxs-lookup"><span data-stu-id="360e9-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result tooa variable</span></span>

<span data-ttu-id="360e9-255">Используйте `let` tooseparate hello части hello предшествующего выражения.</span><span class="sxs-lookup"><span data-stu-id="360e9-255">Use `let` tooseparate out hello parts of hello previous expression.</span></span> <span data-ttu-id="360e9-256">результаты Hello ничем не отличаются:</span><span class="sxs-lookup"><span data-stu-id="360e9-256">hello results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="360e9-257">В клиенте Analytics hello не следует размещать пустые строки между hello части запроса hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-257">In hello Analytics client, don't put blank lines between hello parts of hello query.</span></span> <span data-ttu-id="360e9-258">Убедитесь, что tooexecute все его.</span><span class="sxs-lookup"><span data-stu-id="360e9-258">Make sure tooexecute all of it.</span></span>
>

<span data-ttu-id="360e9-259">Используйте `toscalar` tooconvert значение tooa одной таблицы ячейки:</span><span class="sxs-lookup"><span data-stu-id="360e9-259">Use `toscalar` tooconvert a single table cell tooa value:</span></span>

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


### <a name="functions"></a><span data-ttu-id="360e9-260">Функции</span><span class="sxs-lookup"><span data-stu-id="360e9-260">Functions</span></span>

<span data-ttu-id="360e9-261">Используйте *позволить* toodefine функции:</span><span class="sxs-lookup"><span data-stu-id="360e9-261">Use *Let* toodefine a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="360e9-262">Доступ к вложенным объектам</span><span class="sxs-lookup"><span data-stu-id="360e9-262">Accessing nested objects</span></span>
<span data-ttu-id="360e9-263">Доступ к вложенным объектам осуществляется легко.</span><span class="sxs-lookup"><span data-stu-id="360e9-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="360e9-264">Например поток hello исключения можно увидеть структурированных объектов следующим образом:</span><span class="sxs-lookup"><span data-stu-id="360e9-264">For example, in hello exceptions stream you can see structured objects like this:</span></span>

![result](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="360e9-266">Можно выполнить сведение его, выбрав свойства hello интересующую вас:</span><span class="sxs-lookup"><span data-stu-id="360e9-266">You can flatten it by choosing hello properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="360e9-267">Обратите внимание, что соответствующий тип результата hello toohello toocast.</span><span class="sxs-lookup"><span data-stu-id="360e9-267">Note that you need toocast hello result toohello appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="360e9-268">Пользовательские свойства и измерения</span><span class="sxs-lookup"><span data-stu-id="360e9-268">Custom properties and measurements</span></span>
<span data-ttu-id="360e9-269">Если приложение подключается [пользовательские измерения (свойства) и пользовательских измерений](app-insights-api-custom-events-metrics.md#properties) tooevents, то они будут отображены в hello `customDimensions` и `customMeasurements` объектов.</span><span class="sxs-lookup"><span data-stu-id="360e9-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) tooevents, then you will see them in hello `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="360e9-270">Например, если приложение включает в себя:</span><span class="sxs-lookup"><span data-stu-id="360e9-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="360e9-271">tooextract эти значения в аналитике:</span><span class="sxs-lookup"><span data-stu-id="360e9-271">tooextract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

<span data-ttu-id="360e9-272">tooverify ли пользовательские измерение является определенного типа:</span><span class="sxs-lookup"><span data-stu-id="360e9-272">tooverify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="360e9-273">Панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="360e9-273">Dashboards</span></span>
<span data-ttu-id="360e9-274">Можно закрепить панель мониторинга tooa результаты в порядке toobring вместе всех важнейших диаграмм и таблиц.</span><span class="sxs-lookup"><span data-stu-id="360e9-274">You can pin your results tooa dashboard in order toobring together all your most important charts and tables.</span></span>

* <span data-ttu-id="360e9-275">[Панель мониторинга Azure общего](app-insights-dashboards.md#share-dashboards): щелкните значок булавки hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click hello pin icon.</span></span> <span data-ttu-id="360e9-276">Для этого необходимо иметь панель мониторинга, открытую для совместного использования.</span><span class="sxs-lookup"><span data-stu-id="360e9-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="360e9-277">В hello портал Azure откройте или создайте панель мониторинга и выберите общий ресурс.</span><span class="sxs-lookup"><span data-stu-id="360e9-277">In hello Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="360e9-278">[Панель мониторинга Power BI](app-insights-export-power-bi.md). Щелкните "Экспорт" > "Запрос Power BI".</span><span class="sxs-lookup"><span data-stu-id="360e9-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="360e9-279">Преимущество этого способа состоит в том, что можно отобразить запрос вместе с другими результатами из множества источников.</span><span class="sxs-lookup"><span data-stu-id="360e9-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="360e9-280">Объединение с импортированными данными</span><span class="sxs-lookup"><span data-stu-id="360e9-280">Combine with imported data</span></span>

<span data-ttu-id="360e9-281">Аналитика отчеты выглядят на панели мониторинга hello, но иногда может потребоваться tooa данных hello tootranslate дополнительные снизилось формы.</span><span class="sxs-lookup"><span data-stu-id="360e9-281">Analytics reports look great on hello dashboard, but sometimes you want tootranslate hello data tooa more digestible form.</span></span> <span data-ttu-id="360e9-282">Например предположим, что прошедшие проверку подлинности пользователи идентифицируются псевдоним в телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-282">For example, suppose your authenticated users are identified in hello telemetry by an alias.</span></span> <span data-ttu-id="360e9-283">Вы хотите их реального имена tooshow в результатах.</span><span class="sxs-lookup"><span data-stu-id="360e9-283">You'd like tooshow their real names in your results.</span></span> <span data-ttu-id="360e9-284">toodo, необходимые для сопоставления hello псевдонимы toohello реальные имена CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="360e9-284">toodo this, you need a CSV file that maps from hello aliases toohello real names.</span></span>

<span data-ttu-id="360e9-285">Можно импортировать файл данных и использовать его так же, как и любой из стандартных таблиц hello (запросы, исключения и т. д.).</span><span class="sxs-lookup"><span data-stu-id="360e9-285">You can import a data file and use it just like any of hello standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="360e9-286">Можно выполнять запросы к такой таблице отдельно либо соединить ее с другими таблицами.</span><span class="sxs-lookup"><span data-stu-id="360e9-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="360e9-287">Например, если у вас есть таблица с именем сопоставления пользователей и она содержит столбцы `realName` и `userId`, его можно будет использовать tootranslate hello `user_AuthenticatedId` в телеметрии hello запроса:</span><span class="sxs-lookup"><span data-stu-id="360e9-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it tootranslate hello `user_AuthenticatedId` field in hello request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="360e9-288">tooimport с таблицей, в колонке схемы hello под **другие источники данных**, выполните инструкции hello tooadd новый источник данных, загрузив образец данных.</span><span class="sxs-lookup"><span data-stu-id="360e9-288">tooimport a table, in hello Schema blade, under **Other Data Sources**, follow hello instructions tooadd a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="360e9-289">Затем можно использовать таблицы tooupload этого определения.</span><span class="sxs-lookup"><span data-stu-id="360e9-289">Then you can use this definition tooupload tables.</span></span>

<span data-ttu-id="360e9-290">Hello импорта компонент в настоящий момент в предварительной версии, поэтому изначально появится ссылка «Свяжитесь с нами» в группе «Других источников данных».</span><span class="sxs-lookup"><span data-stu-id="360e9-290">hello import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="360e9-291">Используйте этот toosign копирование toohello предварительной версии программы и hello связи, затем заменяется кнопка «Добавить новый источник данных».</span><span class="sxs-lookup"><span data-stu-id="360e9-291">Use this toosign up toohello preview program, and hello link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="360e9-292">Таблицы</span><span class="sxs-lookup"><span data-stu-id="360e9-292">Tables</span></span>
<span data-ttu-id="360e9-293">поток данных телеметрии, полученных из приложения Hello доступен через несколько таблиц.</span><span class="sxs-lookup"><span data-stu-id="360e9-293">hello stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="360e9-294">схемы Hello свойств, доступных для каждой таблицы отображается в левой части hello окна hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-294">hello schema of properties available for each table is visible at hello left of hello window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="360e9-295">Таблица запросов</span><span class="sxs-lookup"><span data-stu-id="360e9-295">Requests table</span></span>
<span data-ttu-id="360e9-296">Количество HTTP запрашивает tooyour веб-приложения и сегмент, имя страницы:</span><span class="sxs-lookup"><span data-stu-id="360e9-296">Count HTTP requests tooyour web app and segment by page name:</span></span>

![Число запросов, сегментированных по имени](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="360e9-298">Найти hello запросов, завершенных большинство:</span><span class="sxs-lookup"><span data-stu-id="360e9-298">Find hello requests that fail most:</span></span>

![Число запросов, сегментированных по имени](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="360e9-300">Таблица настраиваемых событий</span><span class="sxs-lookup"><span data-stu-id="360e9-300">Custom events table</span></span>
<span data-ttu-id="360e9-301">Если вы используете [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend собственные события, которые можно читать из этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="360e9-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend your own events, you can read them from this table.</span></span>

<span data-ttu-id="360e9-302">Рассмотрим пример, в котором код вашего приложения содержит следующие строки.</span><span class="sxs-lookup"><span data-stu-id="360e9-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="360e9-303">Частота hello отображения этих событий:</span><span class="sxs-lookup"><span data-stu-id="360e9-303">Display hello frequency of these events:</span></span>

![Частота отображения пользовательских событий](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="360e9-305">Извлечь показателей и измерений из hello событий:</span><span class="sxs-lookup"><span data-stu-id="360e9-305">Extract measurements and dimensions from hello events:</span></span>

![Частота отображения пользовательских событий](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="360e9-307">Таблица настраиваемых метрик</span><span class="sxs-lookup"><span data-stu-id="360e9-307">Custom metrics table</span></span>
<span data-ttu-id="360e9-308">Если вы используете [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend собственные значения метрики вы найдете его результаты в hello **customMetrics** потока.</span><span class="sxs-lookup"><span data-stu-id="360e9-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend your own metric values, you’ll find its results in hello **customMetrics** stream.</span></span> <span data-ttu-id="360e9-309">Например:</span><span class="sxs-lookup"><span data-stu-id="360e9-309">For example:</span></span>  

![Настраиваемые метрики в аналитике Application Insights](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="360e9-311">В [обозревателя метрик](app-insights-metrics-explorer.md), все пользовательские измерения tooany вложенный тип телеметрии появляются вместе в колонке hello метрик и метрик, отправляемых с помощью `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="360e9-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached tooany type of telemetry appear together in hello metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="360e9-312">Но в аналитику, настраиваемые измерения, по-прежнему присоединенного toowhichever тип телеметрии, они были перенесены на - события или запросы и т. д. — из-за метрики, отправленных TrackMetric отображаются в своих собственных потока.</span><span class="sxs-lookup"><span data-stu-id="360e9-312">But in Analytics, custom measurements are still attached toowhichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="360e9-313">Таблица счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="360e9-313">Performance counters table</span></span>
<span data-ttu-id="360e9-314">[Счетчики производительности](app-insights-performance-counters.md) показывают базовые системные метрики для вашего приложения, такие как использование ресурсов ЦП, памяти и сети.</span><span class="sxs-lookup"><span data-stu-id="360e9-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="360e9-315">Вы можете настроить hello SDK toosend Дополнительные счетчики, включая собственные пользовательские счетчики.</span><span class="sxs-lookup"><span data-stu-id="360e9-315">You can configure hello SDK toosend additional counters, including your own custom counters.</span></span>

<span data-ttu-id="360e9-316">Hello **performanceCounters** схема предоставляет hello `category`, `counter` имя, и `instance` имя каждого счетчика производительности.</span><span class="sxs-lookup"><span data-stu-id="360e9-316">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="360e9-317">Имена экземпляров счетчиков являются только применимые toosome счетчики производительности и обычно указывают, что относится имя hello числа hello toowhich hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-317">Counter instance names are only applicable toosome performance counters, and typically indicate hello name of hello process toowhich hello count relates.</span></span> <span data-ttu-id="360e9-318">Hello данные телеметрии для каждого приложения вы увидите только hello счетчики для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="360e9-318">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="360e9-319">Например, toosee какие счетчики доступны:</span><span class="sxs-lookup"><span data-stu-id="360e9-319">For example, toosee what counters are available:</span></span>

![Счетчики производительности в аналитике Application Insights](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="360e9-321">tooget диаграммы доступной памяти через hello выбранный период:</span><span class="sxs-lookup"><span data-stu-id="360e9-321">tooget a chart of available memory over hello selected period:</span></span>

![Временная диаграмма памяти в аналитике Application Insights](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="360e9-323">Как и другие данные телеметрии **performanceCounters** также есть столбец `cloud_RoleInstance` указывает удостоверение hello hello хост-компьютера, на котором выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="360e9-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host machine on which your app is running.</span></span> <span data-ttu-id="360e9-324">Например toocompare hello производительности приложения на разных компьютерах hello:</span><span class="sxs-lookup"><span data-stu-id="360e9-324">For example, toocompare hello performance of your app on hello different machines:</span></span>

![Производительность, сегментированная по экземпляру роли в аналитике Application Insights](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="360e9-326">Таблица исключений</span><span class="sxs-lookup"><span data-stu-id="360e9-326">Exceptions table</span></span>
<span data-ttu-id="360e9-327">В этой таблице доступны [исключения, выданные вашим приложением](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="360e9-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="360e9-328">toofind Здравствуйте HTTP-запросе, приложение обрабатывало при возникновении исключения hello, присоединение в operation_Id:</span><span class="sxs-lookup"><span data-stu-id="360e9-328">toofind hello HTTP request that your app was handling when hello exception was raised, join on operation_Id:</span></span>

![Соединение исключений с запросами по operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="360e9-330">Таблица временных параметров браузера</span><span class="sxs-lookup"><span data-stu-id="360e9-330">Browser timings table</span></span>
<span data-ttu-id="360e9-331">`browserTimings` показывает данные о загрузке страниц, собранных в браузерах пользователей.</span><span class="sxs-lookup"><span data-stu-id="360e9-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="360e9-332">[Настройка приложения для стороны клиента телеметрии](app-insights-javascript.md) чтобы toosee этих показателей.</span><span class="sxs-lookup"><span data-stu-id="360e9-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order toosee these metrics.</span></span>

<span data-ttu-id="360e9-333">Схема Hello включает [метрики, указывающее, hello длин разные этапы процесса загрузки страницы приветствия](app-insights-javascript.md#page-load-performance).</span><span class="sxs-lookup"><span data-stu-id="360e9-333">hello schema includes [metrics indicating hello lengths of different stages of hello page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="360e9-334">(Они не указывают hello продолжительность пользователям чтение страницы).</span><span class="sxs-lookup"><span data-stu-id="360e9-334">(They don’t indicate hello length of time your users read a page.)</span></span>  

<span data-ttu-id="360e9-335">Показать popularities hello разных страниц и время для каждой страницы загрузки:</span><span class="sxs-lookup"><span data-stu-id="360e9-335">Show hello popularities of different pages, and load times for each page:</span></span>

![Время загрузки страниц в аналитике](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="360e9-337">Таблица результатов тестов доступности</span><span class="sxs-lookup"><span data-stu-id="360e9-337">Availability results table</span></span>
<span data-ttu-id="360e9-338">`availabilityResults`Здравствуйте, показаны результаты вашей [веб-тестов](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="360e9-338">`availabilityResults` shows hello results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="360e9-339">Каждое выполнение тестов в каком-либо расположении тестирования регистрируется отдельно.</span><span class="sxs-lookup"><span data-stu-id="360e9-339">Each run of your tests from each test location is reported separately.</span></span>

![Время загрузки страниц в аналитике](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="360e9-341">Таблица зависимостей</span><span class="sxs-lookup"><span data-stu-id="360e9-341">Dependencies table</span></span>
<span data-ttu-id="360e9-342">Содержит результаты вызовов, что приложение делает toodatabases и API-интерфейс REST и другие вызывает tooTrackDependency().</span><span class="sxs-lookup"><span data-stu-id="360e9-342">Contains results of calls that your app makes toodatabases and REST APIs, and other calls tooTrackDependency().</span></span> <span data-ttu-id="360e9-343">Также включает вызовы AJAX из браузера hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-343">Also includes AJAX calls made from hello browser.</span></span>

<span data-ttu-id="360e9-344">Вызовы AJAX из браузера hello:</span><span class="sxs-lookup"><span data-stu-id="360e9-344">AJAX calls from hello browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="360e9-345">Вызовы зависимостей с сервера hello:</span><span class="sxs-lookup"><span data-stu-id="360e9-345">Dependency calls from hello server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="360e9-346">Серверные зависимости всегда отображает `success==False` Если hello не установлен агент аналитики приложений.</span><span class="sxs-lookup"><span data-stu-id="360e9-346">Server-side dependency results always show `success==False` if hello Application Insights Agent is not installed.</span></span> <span data-ttu-id="360e9-347">Однако hello другие данные указаны правильно.</span><span class="sxs-lookup"><span data-stu-id="360e9-347">However, hello other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="360e9-348">Таблица трассировок</span><span class="sxs-lookup"><span data-stu-id="360e9-348">Traces table</span></span>
<span data-ttu-id="360e9-349">Содержит hello телеметрии, отправленные приложения с помощью TrackTrace(), или [других платформ ведения журналов](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="360e9-349">Contains hello telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="360e9-350">Видео</span><span class="sxs-lookup"><span data-stu-id="360e9-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="360e9-351">Расширенные запросы:</span><span class="sxs-lookup"><span data-stu-id="360e9-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="360e9-352">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="360e9-352">Next steps</span></span>
* [<span data-ttu-id="360e9-353">Справочные материалы по аналитике</span><span class="sxs-lookup"><span data-stu-id="360e9-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="360e9-354">[SQL-пользователей Памятка](https://aka.ms/sql-analytics) преобразует наиболее общих идиом hello.</span><span class="sxs-lookup"><span data-stu-id="360e9-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates hello most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
