---
title: "Обзор аналитики в Azure Application Insights | Документация Майкрософт"
description: "Короткие примеры всех основных запросов в аналитике, мощном инструменте поиска Application Insights."
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
ms.openlocfilehash: f5650d212eb2f8c460f062b3c11ae14c1e026ba6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="0c866-103">Знакомство с аналитикой в Application Insights</span><span class="sxs-lookup"><span data-stu-id="0c866-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="0c866-104">[Аналитика](app-insights-analytics.md) — это мощный инструмент поиска [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0c866-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="0c866-105">На этих страницах описан язык запросов Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0c866-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="0c866-106">**[Просмотрите видео с вводной информацией](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="0c866-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="0c866-107">**[Протестируйте аналитику на смоделированных данных](https://analytics.applicationinsights.io/demo)**, если ваше приложение еще не отправляет данные в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0c866-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="0c866-108">**[Памятка для пользователей SQL](https://aka.ms/sql-analytics)** содержит сопоставление наиболее распространенных идиом.</span><span class="sxs-lookup"><span data-stu-id="0c866-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>

<span data-ttu-id="0c866-109">Давайте рассмотрим некоторые основные запросы, которые помогут вам начать работу с системой.</span><span class="sxs-lookup"><span data-stu-id="0c866-109">Let's take a walk through some basic queries to get you started.</span></span>

## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="0c866-110">Подключение к данным Application Insights</span><span class="sxs-lookup"><span data-stu-id="0c866-110">Connect to your Application Insights data</span></span>
<span data-ttu-id="0c866-111">Откройте аналитику в [колонке "Обзор"](app-insights-dashboards.md) приложения в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0c866-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![На сайте portal.azure.com откройте ресурс Application Insights и щелкните "Аналитика".](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="0c866-113">Оператор [take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): отображение n строк</span><span class="sxs-lookup"><span data-stu-id="0c866-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="0c866-114">Точки данных, регистрирующие операции пользователя (обычно HTTP-запросы, полученные веб-приложением), хранятся в таблице `requests`.</span><span class="sxs-lookup"><span data-stu-id="0c866-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="0c866-115">Каждая строка представляет точку данных телеметрии, полученную из пакета SDK Application Insights в приложении.</span><span class="sxs-lookup"><span data-stu-id="0c866-115">Each row is a telemetry data point received from the Application Insights SDK in your app.</span></span>

<span data-ttu-id="0c866-116">Начнем с изучения нескольких образцов строк таблицы:</span><span class="sxs-lookup"><span data-stu-id="0c866-116">Let's start by examining a few sample rows of the table:</span></span>

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="0c866-118">Поместите курсор в любой части инструкции, а затем нажмите кнопку "Выполнить".</span><span class="sxs-lookup"><span data-stu-id="0c866-118">Put the cursor somewhere in the statement before you click Go.</span></span> <span data-ttu-id="0c866-119">Инструкцию можно разделить на несколько строк, но она не должна содержать пустых строк.</span><span class="sxs-lookup"><span data-stu-id="0c866-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="0c866-120">Пустыми строками удобно разделить несколько запросов в одном окне.</span><span class="sxs-lookup"><span data-stu-id="0c866-120">Blank lines are a convenient way to keep several separate queries in the window.</span></span>
>
>

<span data-ttu-id="0c866-121">Выберите нужные столбцы, перетащите их, чтобы cгруппировать, и примените фильтр:</span><span class="sxs-lookup"><span data-stu-id="0c866-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Выберите столбец в правом верхнем углу результатов.](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="0c866-123">Разверните любой элемент, чтобы просмотреть сведения о нем:</span><span class="sxs-lookup"><span data-stu-id="0c866-123">Expand any item to see the detail:</span></span>

![Выберите "Таблица", а затем "Настроить столбцы".](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="0c866-125">Чтобы изменить порядок результатов, доступных в веб-браузере, щелкните заголовок столбца.</span><span class="sxs-lookup"><span data-stu-id="0c866-125">Click the head of a column to re-order the results available in the web browser.</span></span> <span data-ttu-id="0c866-126">Но имейте в виду, что для большого результирующего набора в браузер загружается ограниченное количество строк.</span><span class="sxs-lookup"><span data-stu-id="0c866-126">But be aware that for a large result set, the number of rows downloaded to the browser is limited.</span></span> <span data-ttu-id="0c866-127">Сортировка таким способом не всегда показывает фактические наибольшие или наименьшие элементы.</span><span class="sxs-lookup"><span data-stu-id="0c866-127">Sorting this way doesn't always show you the actual highest or lowest items.</span></span> <span data-ttu-id="0c866-128">Чтобы безошибочно отсортировать элементы, используйте операторы `top` или `sort`.</span><span class="sxs-lookup"><span data-stu-id="0c866-128">To sort items reliably, use the `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="0c866-129">Операторы [top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) и [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="0c866-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="0c866-130">`take` позволяет получить быструю выборку из результата, но отображает строки из таблицы в произвольном порядке.</span><span class="sxs-lookup"><span data-stu-id="0c866-130">`take` is useful to get a quick sample of a result, but it shows rows from the table in no particular order.</span></span> <span data-ttu-id="0c866-131">Чтобы упорядочить строки, используйте `top` (для выборки) или `sort` (для всей таблицы).</span><span class="sxs-lookup"><span data-stu-id="0c866-131">To get an ordered view, use `top` (for a sample) or `sort` (over the whole table).</span></span>

<span data-ttu-id="0c866-132">Показать первые n строк, упорядоченных по одному из столбцов:</span><span class="sxs-lookup"><span data-stu-id="0c866-132">Show me the first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="0c866-133">*Синтаксис*. У большинства операторов есть параметры в виде ключевых слов, такие как `by`.</span><span class="sxs-lookup"><span data-stu-id="0c866-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="0c866-134">`desc` — по убыванию, `asc` — по возрастанию.</span><span class="sxs-lookup"><span data-stu-id="0c866-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="0c866-135">`top...` является более производительным способом выполнения `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="0c866-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="0c866-136">Можно было бы написать следующее:</span><span class="sxs-lookup"><span data-stu-id="0c866-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="0c866-137">Результат будет таким же, но запрос станет выполняться немного медленнее.</span><span class="sxs-lookup"><span data-stu-id="0c866-137">The result would be the same, but it would run a bit more slowly.</span></span> <span data-ttu-id="0c866-138">(Также можно написать `order`, это псевдоним `sort`).</span><span class="sxs-lookup"><span data-stu-id="0c866-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="0c866-139">Заголовки столбцов в табличном представлении также можно использовать для сортировки результатов на экране.</span><span class="sxs-lookup"><span data-stu-id="0c866-139">The column headers in the table view can also be used to sort the results on the screen.</span></span> <span data-ttu-id="0c866-140">Но, разумеется, если вы использовали `take` или `top` для получения только части таблицы, отсортировать можно только полученные записи.</span><span class="sxs-lookup"><span data-stu-id="0c866-140">But of course, if you've used `take` or `top` to retrieve just part of a table, you'll only re-order the records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="0c866-141">Оператор [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): фильтрация по условию</span><span class="sxs-lookup"><span data-stu-id="0c866-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="0c866-142">Давайте отобразим только запросы, вернувшие конкретный код результата.</span><span class="sxs-lookup"><span data-stu-id="0c866-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="0c866-143">Оператор `where` принимает логическое выражение.</span><span class="sxs-lookup"><span data-stu-id="0c866-143">The `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="0c866-144">Ниже приведены некоторые ключевые моменты:</span><span class="sxs-lookup"><span data-stu-id="0c866-144">Here are some key points about them:</span></span>

* <span data-ttu-id="0c866-145">`and`, `or`: логические операторы;</span><span class="sxs-lookup"><span data-stu-id="0c866-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="0c866-146">`==`, `<>`, `!=`: равно и не равно;</span><span class="sxs-lookup"><span data-stu-id="0c866-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="0c866-147">`=~`, `!~`: равенство и неравенство строк без учета регистра.</span><span class="sxs-lookup"><span data-stu-id="0c866-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="0c866-148">Существует множество других операторов сравнения строк.</span><span class="sxs-lookup"><span data-stu-id="0c866-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-the-right-type"></a><span data-ttu-id="0c866-149">Получение правильного типа</span><span class="sxs-lookup"><span data-stu-id="0c866-149">Getting the right type</span></span>
<span data-ttu-id="0c866-150">Поиск неудачных запросов:</span><span class="sxs-lookup"><span data-stu-id="0c866-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="0c866-151">Время</span><span class="sxs-lookup"><span data-stu-id="0c866-151">Time</span></span>

<span data-ttu-id="0c866-152">По умолчанию отображаются запросы только за последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="0c866-152">By default, your queries are restricted to the last 24 hours.</span></span> <span data-ttu-id="0c866-153">Этот интервал можно изменить.</span><span class="sxs-lookup"><span data-stu-id="0c866-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="0c866-154">Для этого в предложении where в запросе следует указать `timestamp`.</span><span class="sxs-lookup"><span data-stu-id="0c866-154">Override the time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="0c866-155">Например:</span><span class="sxs-lookup"><span data-stu-id="0c866-155">For example:</span></span>

```AIQL

    // What were the slowest requests over the past 3 days?
    requests
    | where timestamp > ago(3d)  // Override the time range
    | top 5 by duration
```

<span data-ttu-id="0c866-156">Функция диапазона времени эквивалентна предложению where, добавленному после каждого упоминания какой-либо из исходных таблиц.</span><span class="sxs-lookup"><span data-stu-id="0c866-156">The time range feature is equivalent to a 'where' clause inserted after each mention of one of the source tables.</span></span>

<span data-ttu-id="0c866-157">`ago(3d)` означает "три дня назад".</span><span class="sxs-lookup"><span data-stu-id="0c866-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="0c866-158">Другие единицы времени включают в себя часы (`2h`, `2.5h`), минуты (`25m`) и секунды (`10s`).</span><span class="sxs-lookup"><span data-stu-id="0c866-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="0c866-159">Другие примеры.</span><span class="sxs-lookup"><span data-stu-id="0c866-159">Other examples:</span></span>

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

<span data-ttu-id="0c866-160">[Справочник по значениям даты и времени](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="0c866-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="0c866-161">Оператор [Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): выбор, переименование и вычисление столбцов</span><span class="sxs-lookup"><span data-stu-id="0c866-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="0c866-162">С помощью оператора [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) можно выбрать только нужные столбцы.</span><span class="sxs-lookup"><span data-stu-id="0c866-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) to pick out just the columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="0c866-163">Также можно переименовать столбцы и определить новые:</span><span class="sxs-lookup"><span data-stu-id="0c866-163">You can also rename columns and define new ones:</span></span>

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

* <span data-ttu-id="0c866-165">Имена столбцов могут содержать пробелы или символы, если они заключены в квадратные скобки: `['...']` или `["..."]`.</span><span class="sxs-lookup"><span data-stu-id="0c866-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="0c866-166">`%` — обычный оператор остатка от деления.</span><span class="sxs-lookup"><span data-stu-id="0c866-166">`%` is the usual modulo operator.</span></span>
* <span data-ttu-id="0c866-167">`1d` (т. е. цифра 1, а затем "d") — это литерал интервала времени, который означает один день.</span><span class="sxs-lookup"><span data-stu-id="0c866-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="0c866-168">Вот еще несколько литералов интервала времени: `12h`, `30m`, `10s`, `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="0c866-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="0c866-169">`floor` (псевдоним `bin`) округляет значение до ближайшего числа, кратного указанному базовому значению.</span><span class="sxs-lookup"><span data-stu-id="0c866-169">`floor` (alias `bin`) rounds a value down to the nearest multiple of the base value you provide.</span></span> <span data-ttu-id="0c866-170">Например, `floor(aTime, 1s)` округляет время до ближайшей секунды.</span><span class="sxs-lookup"><span data-stu-id="0c866-170">So `floor(aTime, 1s)` rounds a time down to the nearest second.</span></span>

<span data-ttu-id="0c866-171">Выражения могут включать в себя все обычные операторы (`+`, `-` и т. д.) и ряд полезных функций.</span><span class="sxs-lookup"><span data-stu-id="0c866-171">Expressions can include all the usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="0c866-172">Extend</span><span class="sxs-lookup"><span data-stu-id="0c866-172">Extend</span></span>
<span data-ttu-id="0c866-173">Для добавления новых столбцов к существующим можно использовать оператор [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html).</span><span class="sxs-lookup"><span data-stu-id="0c866-173">If you just want to add columns to the existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="0c866-174">Если вы хотите сохранить все существующие столбцы, можете воспользоваться [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html). Это менее подробный вариант, чем [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html).</span><span class="sxs-lookup"><span data-stu-id="0c866-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want to keep all the existing columns.</span></span>

### <a name="convert-to-local-time"></a><span data-ttu-id="0c866-175">Преобразование в местное время</span><span class="sxs-lookup"><span data-stu-id="0c866-175">Convert to local time</span></span>

<span data-ttu-id="0c866-176">Метки времени всегда указываются в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="0c866-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="0c866-177">Поэтому, если вы находитесь на тихоокеанском побережье США зимой, то запрос может быть следующим:</span><span class="sxs-lookup"><span data-stu-id="0c866-177">So if you're on the US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="0c866-178">Оператор [Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): агрегирование групп строк</span><span class="sxs-lookup"><span data-stu-id="0c866-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="0c866-179">`Summarize` применяет указанную *функцию агрегирования* для групп строк.</span><span class="sxs-lookup"><span data-stu-id="0c866-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="0c866-180">Например, время, требуемое веб-приложению для ответа на запрос, указано в поле `duration`.</span><span class="sxs-lookup"><span data-stu-id="0c866-180">For example, the time your web app takes to respond to a request is reported in the field `duration`.</span></span> <span data-ttu-id="0c866-181">Давайте рассмотрим среднее время ответа для всех запросов:</span><span class="sxs-lookup"><span data-stu-id="0c866-181">Let's see the average response time to all requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="0c866-182">Или можно разделить результат по запросам с разными именами:</span><span class="sxs-lookup"><span data-stu-id="0c866-182">Or we could separate the result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="0c866-183">Оператор `Summarize` собирает точки данных в потоке в группы, для которых предложение `by` вычисляется одинаково.</span><span class="sxs-lookup"><span data-stu-id="0c866-183">`Summarize` collects the data points in the stream into groups for which the `by` clause evaluates equally.</span></span> <span data-ttu-id="0c866-184">Каждое значение в выражении `by` , то есть каждое имя операции в приведенном выше примере, соответствует строке в таблице результатов.</span><span class="sxs-lookup"><span data-stu-id="0c866-184">Each value in the `by` expression - each operation name in the above example - results in a row in the result table.</span></span>

<span data-ttu-id="0c866-185">Или можно сгруппировать результаты по времени дня:</span><span class="sxs-lookup"><span data-stu-id="0c866-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="0c866-186">Обратите внимание на то, как используется функция `bin` (также называемая `floor`).</span><span class="sxs-lookup"><span data-stu-id="0c866-186">Notice how we're using the `bin` function (aka `floor`).</span></span> <span data-ttu-id="0c866-187">Если бы мы использовали `by timestamp`, то каждая входная строка попала бы в небольшую отдельную группу.</span><span class="sxs-lookup"><span data-stu-id="0c866-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="0c866-188">Для любого непрерывного скаляра, такого как значения времени или числовые значения, нужно разбить единый диапазон на удобное количество дискретных значений.</span><span class="sxs-lookup"><span data-stu-id="0c866-188">For any continuous scalar like times or numbers, we have to break the continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="0c866-189">Проще всего это сделать с помощью функции `bin`, которая представляет собой привычную функцию округления в меньшую сторону `floor`.</span><span class="sxs-lookup"><span data-stu-id="0c866-189">`bin` - which is just the familiar rounding-down `floor` function - is the easiest way to do that.</span></span>

<span data-ttu-id="0c866-190">Ту же методику можно использовать и для сокращения диапазонов строк:</span><span class="sxs-lookup"><span data-stu-id="0c866-190">We can use the same technique to reduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="0c866-191">Обратите внимание, что с помощью `name=` можно задать имя столбца результатов в агрегатных выражениях или предложении By.</span><span class="sxs-lookup"><span data-stu-id="0c866-191">Notice that you can use `name=` to set the name of a result column, either in the aggregation expressions or the by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="0c866-192">Подсчет данных выборки</span><span class="sxs-lookup"><span data-stu-id="0c866-192">Counting sampled data</span></span>
<span data-ttu-id="0c866-193">`sum(itemCount)` .</span><span class="sxs-lookup"><span data-stu-id="0c866-193">`sum(itemCount)` is the recommended aggregation to count events.</span></span> <span data-ttu-id="0c866-194">Во многих случаях itemCount==1, поэтому функция просто подсчитывает количество строк в группе.</span><span class="sxs-lookup"><span data-stu-id="0c866-194">In many cases, itemCount==1, so the function simply counts up the number of rows in the group.</span></span> <span data-ttu-id="0c866-195">Но если выполняется [выборка](app-insights-sampling.md), то лишь часть исходных событий сохраняется в виде точек данных в Application Insights, поэтому для каждой отображаемой точки данных существуют события `itemCount`.</span><span class="sxs-lookup"><span data-stu-id="0c866-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of the original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="0c866-196">Например, если выборка отбрасывает 75 % исходных событий, то в сохраняемых записях itemCount==4. Это значит, что для каждой сохраняемой записи было четыре исходные записи.</span><span class="sxs-lookup"><span data-stu-id="0c866-196">For example, if sampling discards 75% of the original events, then itemCount==4 in the retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="0c866-197">В результате адаптивной выборки itemCount увеличивается в периоды, когда приложение интенсивно используется.</span><span class="sxs-lookup"><span data-stu-id="0c866-197">Adaptive sampling causes itemCount to be higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="0c866-198">Таким образом, суммирование по itemCount позволяет правильно оценить исходное число событий.</span><span class="sxs-lookup"><span data-stu-id="0c866-198">Summing up itemCount therefore gives a good estimate of the original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="0c866-199">Существует также функция агрегирования `count()` (и операция подсчета), используемая, когда действительно нужно подсчитать количество строк в группе.</span><span class="sxs-lookup"><span data-stu-id="0c866-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want to count the number of rows in a group.</span></span>

<span data-ttu-id="0c866-200">Существует ряд [статистических функций](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="0c866-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-the-results"></a><span data-ttu-id="0c866-201">Отображение результатов</span><span class="sxs-lookup"><span data-stu-id="0c866-201">Charting the results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="0c866-202">По умолчанию результаты отображаются в виде таблицы:</span><span class="sxs-lookup"><span data-stu-id="0c866-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="0c866-203">Мы можем добиться лучшего результата по сравнению с таким табличным представлением.</span><span class="sxs-lookup"><span data-stu-id="0c866-203">We can do better than the table view.</span></span> <span data-ttu-id="0c866-204">Давайте посмотрим на результаты в диаграмме с вертикальными столбцами:</span><span class="sxs-lookup"><span data-stu-id="0c866-204">Let's look at the results in the chart view with the vertical bar option:</span></span>

![Щелкните "Диаграмма", затем выберите "Вертикальная линейчатая диаграмма" и назначьте оси x и y.](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="0c866-206">Обратите внимание, что хотя мы не сортировали результаты по времени (как видно в окне таблицы), дата и время на диаграмме всегда отображаются в правильном порядке.</span><span class="sxs-lookup"><span data-stu-id="0c866-206">Notice that although we didn't sort the results by time (as you can see in the table display), the chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="0c866-207">Временные диаграммы</span><span class="sxs-lookup"><span data-stu-id="0c866-207">Timecharts</span></span>
<span data-ttu-id="0c866-208">Отображение количества событий, возникающих каждый час:</span><span class="sxs-lookup"><span data-stu-id="0c866-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="0c866-209">Выберите вариант отображения диаграммы:</span><span class="sxs-lookup"><span data-stu-id="0c866-209">Select the Chart display option:</span></span>

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="0c866-211">Множественные серии</span><span class="sxs-lookup"><span data-stu-id="0c866-211">Multiple series</span></span>
<span data-ttu-id="0c866-212">Из нескольких выражений в `summarize` создается несколько столбцов.</span><span class="sxs-lookup"><span data-stu-id="0c866-212">Multiple expressions in the `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="0c866-213">Из нескольких выражений в предложении `by` создаются несколько строк, по одной для каждого сочетания значений.</span><span class="sxs-lookup"><span data-stu-id="0c866-213">Multiple expressions in the `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Запросы к таблицам по часу и расположению](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="0c866-215">Разделение диаграммы по показателям</span><span class="sxs-lookup"><span data-stu-id="0c866-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="0c866-216">При представлении на диаграмме данных таблицы, в которой есть столбцы строкового и числового типа, строки можно использовать для разделения числовых данных на отдельные ряды точек.</span><span class="sxs-lookup"><span data-stu-id="0c866-216">If you chart a table that has a string column and a numeric column, the string can be used to split the numeric data into separate series of points.</span></span> <span data-ttu-id="0c866-217">Если есть несколько столбцов строкового типа, можно выбрать один из этих столбцов для использования в качестве дискриминатора.</span><span class="sxs-lookup"><span data-stu-id="0c866-217">If there's more than one string column, you can choose which column to use as the discriminator.</span></span>

![Разделение диаграммы аналитики](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="0c866-219">Частота возвращения</span><span class="sxs-lookup"><span data-stu-id="0c866-219">Bounce rate</span></span>

<span data-ttu-id="0c866-220">Преобразуйте логическое значение в строку для использования в качестве дискриминатора.</span><span class="sxs-lookup"><span data-stu-id="0c866-220">Convert a boolean to a string to use it as a discriminator:</span></span>

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

### <a name="display-multiple-metrics"></a><span data-ttu-id="0c866-221">Отображение нескольких метрик</span><span class="sxs-lookup"><span data-stu-id="0c866-221">Display multiple metrics</span></span>
<span data-ttu-id="0c866-222">При представлении на диаграмме данных таблицы, содержащей несколько столбцов числового типа, помимо метки времени можно отобразить любое сочетание метрик.</span><span class="sxs-lookup"><span data-stu-id="0c866-222">If you chart a table that has more than one numeric column, in addition to the timestamp, you can display any combination of them.</span></span>

![Разделение диаграммы аналитики](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="0c866-224">Чтобы выбрать несколько столбцов числового типа, щелкните **Don't Split** (Не разделять).</span><span class="sxs-lookup"><span data-stu-id="0c866-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="0c866-225">Если отображаются несколько столбцов числового типа, невозможно разделить данные по столбцу строкового типа.</span><span class="sxs-lookup"><span data-stu-id="0c866-225">You can't split by a string column at the same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="0c866-226">Ежедневный средний цикл</span><span class="sxs-lookup"><span data-stu-id="0c866-226">Daily average cycle</span></span>
<span data-ttu-id="0c866-227">Как изменяется использование в течение среднего дня?</span><span class="sxs-lookup"><span data-stu-id="0c866-227">How does usage vary over the average day?</span></span>

<span data-ttu-id="0c866-228">Количество запросов в зависимости от времени по модулю в один день, сгруппированное по часам:</span><span class="sxs-lookup"><span data-stu-id="0c866-228">Count requests by the time modulo one day, binned into hours:</span></span>

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
> <span data-ttu-id="0c866-230">Обратите внимание, что в настоящее время необходимо преобразовать интервалы времени в значения datetime для отображения на графике.</span><span class="sxs-lookup"><span data-stu-id="0c866-230">Notice that we currently have to convert time durations to datetimes in order to display on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="0c866-231">Сравнение серий для нескольких дней</span><span class="sxs-lookup"><span data-stu-id="0c866-231">Compare multiple daily series</span></span>
<span data-ttu-id="0c866-232">Как изменяется использование в течение дня в разных странах?</span><span class="sxs-lookup"><span data-stu-id="0c866-232">How does usage vary over the time of day in different countries?</span></span>

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

## <a name="plot-a-distribution"></a><span data-ttu-id="0c866-234">Построение графика распределения</span><span class="sxs-lookup"><span data-stu-id="0c866-234">Plot a distribution</span></span>
<span data-ttu-id="0c866-235">Какое количество сеансов различной длительности существует?</span><span class="sxs-lookup"><span data-stu-id="0c866-235">How many sessions are there of different lengths?</span></span>

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

<span data-ttu-id="0c866-236">Последняя строка необходима для преобразования в данные даты и времени.</span><span class="sxs-lookup"><span data-stu-id="0c866-236">The last line is required to convert to datetime.</span></span> <span data-ttu-id="0c866-237">В настоящее время ось x графика отображается в виде скаляра, только если на ней представлены данные даты и времени.</span><span class="sxs-lookup"><span data-stu-id="0c866-237">Currently the x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="0c866-238">Предложение `where` исключает одноразовые сеансы (sessionDuration==0) и задает длину оси x.</span><span class="sxs-lookup"><span data-stu-id="0c866-238">The `where` clause excludes one-shot sessions (sessionDuration==0) and sets the length of the x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="0c866-239">Процентили</span><span class="sxs-lookup"><span data-stu-id="0c866-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="0c866-240">Какие диапазоны длительности покрывают различные процентные доли сеансов?</span><span class="sxs-lookup"><span data-stu-id="0c866-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="0c866-241">Используйте приведенный выше запрос, но вместо последней строки укажите следующую:</span><span class="sxs-lookup"><span data-stu-id="0c866-241">Use the above query, but replace the last line:</span></span>

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

<span data-ttu-id="0c866-242">Мы также удалили верхний предел в предложении where, чтобы получить правильные данные, включая все сеансы с несколькими запросами:</span><span class="sxs-lookup"><span data-stu-id="0c866-242">We also removed the upper limit in the where clause, in order to get correct figures including all sessions with more than one request:</span></span>

![result](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="0c866-244">Из полученных результатов мы видим следующее:</span><span class="sxs-lookup"><span data-stu-id="0c866-244">From which we can see that:</span></span>

* <span data-ttu-id="0c866-245">5 % сеансов имеют продолжительность менее 3 минут 34 секунд;</span><span class="sxs-lookup"><span data-stu-id="0c866-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="0c866-246">50 % сеансов имеют продолжительность менее 36 минут;</span><span class="sxs-lookup"><span data-stu-id="0c866-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="0c866-247">5 % сеансов имеют продолжительность более 7 дней.</span><span class="sxs-lookup"><span data-stu-id="0c866-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="0c866-248">Для получения отдельных результатов для каждой страны нужно просто отделить столбец client_CountryOrRegion с помощью обоих операторов суммирования:</span><span class="sxs-lookup"><span data-stu-id="0c866-248">To get a separate breakdown for each country, we just have to bring the client_CountryOrRegion column separately through both summarize operators:</span></span>

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

## <a name="join"></a><span data-ttu-id="0c866-249">Объединение</span><span class="sxs-lookup"><span data-stu-id="0c866-249">Join</span></span>
<span data-ttu-id="0c866-250">Имеется доступ к нескольким таблицам, включая запросы и исключения.</span><span class="sxs-lookup"><span data-stu-id="0c866-250">We have access to several tables, including requests and exceptions.</span></span>

<span data-ttu-id="0c866-251">Чтобы найти исключения, связанные с запросом, который завершился неудачно, можно соединить таблицы по `session_Id`.</span><span class="sxs-lookup"><span data-stu-id="0c866-251">To find the exceptions related to a request that returned a failure response, we can join the tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="0c866-252">Рекомендуется использовать `project` только для выбора необходимых столбцов перед выполнением соединения.</span><span class="sxs-lookup"><span data-stu-id="0c866-252">It's good practice to use `project` to select just the columns we need before performing the join.</span></span>
<span data-ttu-id="0c866-253">В тех же предложениях мы переименуем столбец timestamp.</span><span class="sxs-lookup"><span data-stu-id="0c866-253">In the same clauses, we rename the timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-to-a-variable"></a><span data-ttu-id="0c866-254">Оператор [let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): присвоение результата переменной</span><span class="sxs-lookup"><span data-stu-id="0c866-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result to a variable</span></span>

<span data-ttu-id="0c866-255">С помощью оператора `let` можно разделить части предыдущего выражения.</span><span class="sxs-lookup"><span data-stu-id="0c866-255">Use `let` to separate out the parts of the previous expression.</span></span> <span data-ttu-id="0c866-256">Результаты не изменились:</span><span class="sxs-lookup"><span data-stu-id="0c866-256">The results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="0c866-257">Не добавляйте пустые строки между частями запроса в клиенте аналитики.</span><span class="sxs-lookup"><span data-stu-id="0c866-257">In the Analytics client, don't put blank lines between the parts of the query.</span></span> <span data-ttu-id="0c866-258">Обязательно выполните все части.</span><span class="sxs-lookup"><span data-stu-id="0c866-258">Make sure to execute all of it.</span></span>
>

<span data-ttu-id="0c866-259">Используйте `toscalar` для преобразования одной ячейки таблицы в значение:</span><span class="sxs-lookup"><span data-stu-id="0c866-259">Use `toscalar` to convert a single table cell to a value:</span></span>

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


### <a name="functions"></a><span data-ttu-id="0c866-260">Функции</span><span class="sxs-lookup"><span data-stu-id="0c866-260">Functions</span></span>

<span data-ttu-id="0c866-261">Используйте *Let* для определения функции.</span><span class="sxs-lookup"><span data-stu-id="0c866-261">Use *Let* to define a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="0c866-262">Доступ к вложенным объектам</span><span class="sxs-lookup"><span data-stu-id="0c866-262">Accessing nested objects</span></span>
<span data-ttu-id="0c866-263">Доступ к вложенным объектам осуществляется легко.</span><span class="sxs-lookup"><span data-stu-id="0c866-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="0c866-264">Например, в потоке исключений структурированные объекты выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0c866-264">For example, in the exceptions stream you can see structured objects like this:</span></span>

![result](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="0c866-266">Этот поток можно выровнять, выбрав необходимые свойства.</span><span class="sxs-lookup"><span data-stu-id="0c866-266">You can flatten it by choosing the properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="0c866-267">Обратите внимание на то, что необходимо привести результат к соответствующему типу.</span><span class="sxs-lookup"><span data-stu-id="0c866-267">Note that you need to cast the result to the appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="0c866-268">Пользовательские свойства и измерения</span><span class="sxs-lookup"><span data-stu-id="0c866-268">Custom properties and measurements</span></span>
<span data-ttu-id="0c866-269">Если ваше приложение прикрепляет к событиям [пользовательские измерения (свойства) или пользовательские показатели](app-insights-api-custom-events-metrics.md#properties), они будут отображаться в объектах `customDimensions` и `customMeasurements`.</span><span class="sxs-lookup"><span data-stu-id="0c866-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) to events, then you will see them in the `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="0c866-270">Например, если приложение включает в себя:</span><span class="sxs-lookup"><span data-stu-id="0c866-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="0c866-271">Чтобы извлечь эти значения в аналитике, необходимо выполнить следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="0c866-271">To extract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast to expected type

```

<span data-ttu-id="0c866-272">Чтобы проверить, относится ли пользовательское измерение к определенному типу:</span><span class="sxs-lookup"><span data-stu-id="0c866-272">To verify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="0c866-273">Панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="0c866-273">Dashboards</span></span>
<span data-ttu-id="0c866-274">Результаты можно закрепить на панели мониторинга, чтобы все важные диаграммы и таблицы были под рукой.</span><span class="sxs-lookup"><span data-stu-id="0c866-274">You can pin your results to a dashboard in order to bring together all your most important charts and tables.</span></span>

* <span data-ttu-id="0c866-275">[Панель мониторинга Azure в общем доступе](app-insights-dashboards.md#share-dashboards). Щелкните значок булавки.</span><span class="sxs-lookup"><span data-stu-id="0c866-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click the pin icon.</span></span> <span data-ttu-id="0c866-276">Для этого необходимо иметь панель мониторинга, открытую для совместного использования.</span><span class="sxs-lookup"><span data-stu-id="0c866-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="0c866-277">На портале Azure откройте или создайте панель мониторинга, а затем щелкните "Общий доступ".</span><span class="sxs-lookup"><span data-stu-id="0c866-277">In the Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="0c866-278">[Панель мониторинга Power BI](app-insights-export-power-bi.md). Щелкните "Экспорт" > "Запрос Power BI".</span><span class="sxs-lookup"><span data-stu-id="0c866-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="0c866-279">Преимущество этого способа состоит в том, что можно отобразить запрос вместе с другими результатами из множества источников.</span><span class="sxs-lookup"><span data-stu-id="0c866-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="0c866-280">Объединение с импортированными данными</span><span class="sxs-lookup"><span data-stu-id="0c866-280">Combine with imported data</span></span>

<span data-ttu-id="0c866-281">Аналитические отчеты отлично выглядят на панели мониторинга, но иногда необходимо преобразовать данные в более удобную форму.</span><span class="sxs-lookup"><span data-stu-id="0c866-281">Analytics reports look great on the dashboard, but sometimes you want to translate the data to a more digestible form.</span></span> <span data-ttu-id="0c866-282">Например предположим, что аутентифицированные пользователи идентифицируются в данных телеметрии по псевдониму.</span><span class="sxs-lookup"><span data-stu-id="0c866-282">For example, suppose your authenticated users are identified in the telemetry by an alias.</span></span> <span data-ttu-id="0c866-283">А вы хотите показать в результатах их настоящие имена.</span><span class="sxs-lookup"><span data-stu-id="0c866-283">You'd like to show their real names in your results.</span></span> <span data-ttu-id="0c866-284">В этом случае вам необходим CSV-файл для сопоставления настоящих имен и псевдонимов.</span><span class="sxs-lookup"><span data-stu-id="0c866-284">To do this, you need a CSV file that maps from the aliases to the real names.</span></span>

<span data-ttu-id="0c866-285">Можно импортировать файл данных и использовать его как стандартную таблицу (включая запросы, исключения и т. д.).</span><span class="sxs-lookup"><span data-stu-id="0c866-285">You can import a data file and use it just like any of the standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="0c866-286">Можно выполнять запросы к такой таблице отдельно либо соединить ее с другими таблицами.</span><span class="sxs-lookup"><span data-stu-id="0c866-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="0c866-287">Например, если у вас есть таблица usermap и она содержит столбцы `realName` и `userId`, то с ее помощью можно преобразовать поле `user_AuthenticatedId` в телеметрии запросов.</span><span class="sxs-lookup"><span data-stu-id="0c866-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it to translate the `user_AuthenticatedId` field in the request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get the realName field from the usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="0c866-288">Для импорта таблицы в колонке "Схема" следуйте инструкциям в разделе **Другие источники данных**, чтобы добавить новый источник данных, передав образец данных.</span><span class="sxs-lookup"><span data-stu-id="0c866-288">To import a table, in the Schema blade, under **Other Data Sources**, follow the instructions to add a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="0c866-289">Затем это определение можно использовать для передачи таблиц.</span><span class="sxs-lookup"><span data-stu-id="0c866-289">Then you can use this definition to upload tables.</span></span>

<span data-ttu-id="0c866-290">В настоящее время доступна предварительная версия функции импорта, поэтому в разделе "Другие источники данных" сначала будет отображаться ссылка "Свяжитесь с нами".</span><span class="sxs-lookup"><span data-stu-id="0c866-290">The import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="0c866-291">Используйте ее для регистрации в программе по ознакомлению с предварительной версией, и позже на месте ссылки появится кнопка "Добавить новый источник данных".</span><span class="sxs-lookup"><span data-stu-id="0c866-291">Use this to sign up to the preview program, and the link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="0c866-292">Таблицы</span><span class="sxs-lookup"><span data-stu-id="0c866-292">Tables</span></span>
<span data-ttu-id="0c866-293">Поток данных телеметрии, полученных из приложения, доступен в нескольких таблицах.</span><span class="sxs-lookup"><span data-stu-id="0c866-293">The stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="0c866-294">Схема свойств, доступных для каждой таблицы, отображается в левой части окна.</span><span class="sxs-lookup"><span data-stu-id="0c866-294">The schema of properties available for each table is visible at the left of the window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="0c866-295">Таблица запросов</span><span class="sxs-lookup"><span data-stu-id="0c866-295">Requests table</span></span>
<span data-ttu-id="0c866-296">Подсчитайте число HTTP-запросов к веб-приложению и сегментируйте их по имени страницы.</span><span class="sxs-lookup"><span data-stu-id="0c866-296">Count HTTP requests to your web app and segment by page name:</span></span>

![Число запросов, сегментированных по имени](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="0c866-298">Найдите запросы, чаще всего завершавшиеся сбоем.</span><span class="sxs-lookup"><span data-stu-id="0c866-298">Find the requests that fail most:</span></span>

![Число запросов, сегментированных по имени](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="0c866-300">Таблица настраиваемых событий</span><span class="sxs-lookup"><span data-stu-id="0c866-300">Custom events table</span></span>
<span data-ttu-id="0c866-301">Если вы используете [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) для отправки своих собственных событий, то их можно считать из этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="0c866-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) to send your own events, you can read them from this table.</span></span>

<span data-ttu-id="0c866-302">Рассмотрим пример, в котором код вашего приложения содержит следующие строки.</span><span class="sxs-lookup"><span data-stu-id="0c866-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="0c866-303">Отобразите частоту этих событий.</span><span class="sxs-lookup"><span data-stu-id="0c866-303">Display the frequency of these events:</span></span>

![Частота отображения пользовательских событий](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="0c866-305">Извлеките показатели и измерения из событий.</span><span class="sxs-lookup"><span data-stu-id="0c866-305">Extract measurements and dimensions from the events:</span></span>

![Частота отображения пользовательских событий](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="0c866-307">Таблица настраиваемых метрик</span><span class="sxs-lookup"><span data-stu-id="0c866-307">Custom metrics table</span></span>
<span data-ttu-id="0c866-308">Если вы используете [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) для отправки своих собственных значений метрик, то вы найдете полученные результаты в потоке **customMetrics**.</span><span class="sxs-lookup"><span data-stu-id="0c866-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to send your own metric values, you’ll find its results in the **customMetrics** stream.</span></span> <span data-ttu-id="0c866-309">Например:</span><span class="sxs-lookup"><span data-stu-id="0c866-309">For example:</span></span>  

![Настраиваемые метрики в аналитике Application Insights](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="0c866-311">В [обозревателе метрик](app-insights-metrics-explorer.md) все пользовательские показатели, прикрепленные к любому типу телеметрии, отображаются в колонке метрик вместе с метриками, отправленными с помощью `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="0c866-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached to any type of telemetry appear together in the metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="0c866-312">Однако в аналитике пользовательские показатели по-прежнему прикреплены к типу телеметрии, в котором они были выполнены (события, запросы и т. п.), а метрики, отправляемые TrackMetric, отображаются в своем собственном потоке.</span><span class="sxs-lookup"><span data-stu-id="0c866-312">But in Analytics, custom measurements are still attached to whichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="0c866-313">Таблица счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="0c866-313">Performance counters table</span></span>
<span data-ttu-id="0c866-314">[Счетчики производительности](app-insights-performance-counters.md) показывают базовые системные метрики для вашего приложения, такие как использование ресурсов ЦП, памяти и сети.</span><span class="sxs-lookup"><span data-stu-id="0c866-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="0c866-315">Можно настроить пакет SDK для отправки дополнительных счетчиков, включая собственные пользовательские счетчики.</span><span class="sxs-lookup"><span data-stu-id="0c866-315">You can configure the SDK to send additional counters, including your own custom counters.</span></span>

<span data-ttu-id="0c866-316">Схема **PerformanceCounters** предоставляет `category`, имя `counter` и имя `instance` каждого счетчика производительности.</span><span class="sxs-lookup"><span data-stu-id="0c866-316">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="0c866-317">Имена экземпляров счетчиков применимы только к некоторым счетчикам производительности и обычно указывают имя процесса, к которому относится счетчик.</span><span class="sxs-lookup"><span data-stu-id="0c866-317">Counter instance names are only applicable to some performance counters, and typically indicate the name of the process to which the count relates.</span></span> <span data-ttu-id="0c866-318">В данных телеметрии для каждого приложения вы увидите только счетчики для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="0c866-318">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="0c866-319">Например, вот как можно увидеть, какие счетчики доступны.</span><span class="sxs-lookup"><span data-stu-id="0c866-319">For example, to see what counters are available:</span></span>

![Счетчики производительности в аналитике Application Insights](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="0c866-321">Вот как можно получить диаграмму доступной памяти за выбранный период.</span><span class="sxs-lookup"><span data-stu-id="0c866-321">To get a chart of available memory over the selected period:</span></span>

![Временная диаграмма памяти в аналитике Application Insights](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="0c866-323">Как и другие данные телеметрии, данные **performanceCounters** также содержат столбец `cloud_RoleInstance`, указывающий удостоверение хост-компьютера, на котором выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="0c866-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host machine on which your app is running.</span></span> <span data-ttu-id="0c866-324">Например, вот как можно сравнить производительность приложения на разных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="0c866-324">For example, to compare the performance of your app on the different machines:</span></span>

![Производительность, сегментированная по экземпляру роли в аналитике Application Insights](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="0c866-326">Таблица исключений</span><span class="sxs-lookup"><span data-stu-id="0c866-326">Exceptions table</span></span>
<span data-ttu-id="0c866-327">В этой таблице доступны [исключения, выданные вашим приложением](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="0c866-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="0c866-328">Чтобы найти HTTP-запрос, обрабатываемый приложением при порождении исключения, выполните соединение по operation_Id.</span><span class="sxs-lookup"><span data-stu-id="0c866-328">To find the HTTP request that your app was handling when the exception was raised, join on operation_Id:</span></span>

![Соединение исключений с запросами по operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="0c866-330">Таблица временных параметров браузера</span><span class="sxs-lookup"><span data-stu-id="0c866-330">Browser timings table</span></span>
<span data-ttu-id="0c866-331">`browserTimings` показывает данные о загрузке страниц, собранных в браузерах пользователей.</span><span class="sxs-lookup"><span data-stu-id="0c866-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="0c866-332">Для просмотра этих метрик [настройте приложение для использования телеметрии на стороне клиента](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="0c866-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order to see these metrics.</span></span>

<span data-ttu-id="0c866-333">Схема включает в себя [метрики, указывающее длительность различных этапов загрузки страниц](app-insights-javascript.md#page-load-performance).</span><span class="sxs-lookup"><span data-stu-id="0c866-333">The schema includes [metrics indicating the lengths of different stages of the page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="0c866-334">(Они не указывает продолжительность чтения страниц пользователями.)</span><span class="sxs-lookup"><span data-stu-id="0c866-334">(They don’t indicate the length of time your users read a page.)</span></span>  

<span data-ttu-id="0c866-335">Отобразите популярность различных страниц и время загрузки каждой из них.</span><span class="sxs-lookup"><span data-stu-id="0c866-335">Show the popularities of different pages, and load times for each page:</span></span>

![Время загрузки страниц в аналитике](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="0c866-337">Таблица результатов тестов доступности</span><span class="sxs-lookup"><span data-stu-id="0c866-337">Availability results table</span></span>
<span data-ttu-id="0c866-338">`availabilityResults` показывает результаты ваших [веб-тестов](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="0c866-338">`availabilityResults` shows the results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="0c866-339">Каждое выполнение тестов в каком-либо расположении тестирования регистрируется отдельно.</span><span class="sxs-lookup"><span data-stu-id="0c866-339">Each run of your tests from each test location is reported separately.</span></span>

![Время загрузки страниц в аналитике](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="0c866-341">Таблица зависимостей</span><span class="sxs-lookup"><span data-stu-id="0c866-341">Dependencies table</span></span>
<span data-ttu-id="0c866-342">Содержит результаты вызовов вашего приложения, отправляемых к базам данных и интерфейсам REST API, а также других вызовов TrackDependency().</span><span class="sxs-lookup"><span data-stu-id="0c866-342">Contains results of calls that your app makes to databases and REST APIs, and other calls to TrackDependency().</span></span> <span data-ttu-id="0c866-343">Кроме того, содержит вызовы AJAX, выполненные из браузера.</span><span class="sxs-lookup"><span data-stu-id="0c866-343">Also includes AJAX calls made from the browser.</span></span>

<span data-ttu-id="0c866-344">Вызовы AJAX из браузера:</span><span class="sxs-lookup"><span data-stu-id="0c866-344">AJAX calls from the browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="0c866-345">Вызовы зависимостей от сервера:</span><span class="sxs-lookup"><span data-stu-id="0c866-345">Dependency calls from the server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="0c866-346">Для результатов зависимостей на стороне сервера всегда отображается `success==False`, если не установлен агент Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0c866-346">Server-side dependency results always show `success==False` if the Application Insights Agent is not installed.</span></span> <span data-ttu-id="0c866-347">Тем не менее прочие данные правильны.</span><span class="sxs-lookup"><span data-stu-id="0c866-347">However, the other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="0c866-348">Таблица трассировок</span><span class="sxs-lookup"><span data-stu-id="0c866-348">Traces table</span></span>
<span data-ttu-id="0c866-349">Содержит данные телеметрии, отправленные приложением с помощью TrackTrace() или [других платформ ведения журнала](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="0c866-349">Contains the telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="0c866-350">Видео</span><span class="sxs-lookup"><span data-stu-id="0c866-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="0c866-351">Расширенные запросы:</span><span class="sxs-lookup"><span data-stu-id="0c866-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="0c866-352">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0c866-352">Next steps</span></span>
* [<span data-ttu-id="0c866-353">Справочные материалы по аналитике</span><span class="sxs-lookup"><span data-stu-id="0c866-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="0c866-354">[Памятка для пользователей SQL](https://aka.ms/sql-analytics) содержит сопоставление наиболее распространенных идиом.</span><span class="sxs-lookup"><span data-stu-id="0c866-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates the most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
