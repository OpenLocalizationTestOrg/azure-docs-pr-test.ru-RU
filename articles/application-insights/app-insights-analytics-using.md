---
title: "Использование аналитики — мощного инструмента поиска Azure Application Insights | Документация Майкрософт"
description: "Использование аналитики — эффективного инструмента поиска по журналу диагностики Application Insights. "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9f7c1744db52b1c2f374fd5655e2c66b5f61bacf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="ed4b3-103">Использование аналитики в Application Insights</span><span class="sxs-lookup"><span data-stu-id="ed4b3-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="ed4b3-104">[Аналитика](app-insights-analytics.md) — это мощный инструмент поиска [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed4b3-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="ed4b3-105">На этих страницах описан язык запросов Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="ed4b3-106">**[Просмотрите видео с вводной информацией](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="ed4b3-107">**[Протестируйте аналитику на смоделированных данных](https://analytics.applicationinsights.io/demo)**, если ваше приложение еще не отправляет данные в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="ed4b3-108">Открытие аналитики</span><span class="sxs-lookup"><span data-stu-id="ed4b3-108">Open Analytics</span></span>
<span data-ttu-id="ed4b3-109">В домашнем ресурсе вашего приложения в Application Insights щелкните "Аналитика".</span><span class="sxs-lookup"><span data-stu-id="ed4b3-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![На сайте portal.azure.com откройте ресурс Application Insights и щелкните "Аналитика".](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="ed4b3-111">Во встроенном руководстве представлены некоторые сведения о доступных возможностях.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-111">The inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="ed4b3-112">Смотрите [исчерпывающий обзор здесь](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="ed4b3-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="ed4b3-113">Запрос данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="ed4b3-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="ed4b3-114">Напишите запрос</span><span class="sxs-lookup"><span data-stu-id="ed4b3-114">Write a query</span></span>
![Отображение схемы](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="ed4b3-116">Начните с имен таблиц, перечисленных в левой части окна (либо с операторов [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) или [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html)).</span><span class="sxs-lookup"><span data-stu-id="ed4b3-116">Begin with the names of any of the tables listed on the left (or the [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="ed4b3-117">Используйте `|` для создания конвейера [операторов](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="ed4b3-117">Use `|` to create a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="ed4b3-118">IntelliSense подскажет вам операторы и элементы выражений, которые можно использовать.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-118">IntelliSense prompts you with the operators and the expression elements that you can use.</span></span> <span data-ttu-id="ed4b3-119">Щелкните значок сведений (или нажмите клавиши CTRL+ПРОБЕЛ), чтобы получить более подробное описание и примеры использования каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-119">Click the information icon (or press CTRL+Space) to get a longer description and examples of how to use each element.</span></span>

<span data-ttu-id="ed4b3-120">Ознакомьтесь с [обзором языка аналитики](app-insights-analytics-tour.md) и [справочником по языку](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ed4b3-120">See the [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="ed4b3-121">Выполнение запроса</span><span class="sxs-lookup"><span data-stu-id="ed4b3-121">Run a query</span></span>
![Выполнение запроса](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="ed4b3-123">В запросе можно использовать только однократные разрывы строк.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="ed4b3-124">Поместите курсор внутри или в конце запроса, который необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-124">Put the cursor inside or at the end of the query you want to run.</span></span>
3. <span data-ttu-id="ed4b3-125">Проверьте диапазон времени своего запроса.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-125">Check the time range of your query.</span></span> <span data-ttu-id="ed4b3-126">(Его можно изменить или переопределить, добавив в запрос собственное предложение [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html).)</span><span class="sxs-lookup"><span data-stu-id="ed4b3-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="ed4b3-127">Щелкните "Начать", чтобы выполнить запрос.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-127">Click Go to run the query.</span></span>
4. <span data-ttu-id="ed4b3-128">Не помещайте в запрос пустые строки.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="ed4b3-129">На одной вкладке запроса можно хранить несколько отдельных запросов, разделив их пустыми строками.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="ed4b3-130">Выполняется только запрос с курсором.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-130">Only the query that has the cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="ed4b3-131">Сохранение запроса</span><span class="sxs-lookup"><span data-stu-id="ed4b3-131">Save a query</span></span>
![Сохранение запроса](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="ed4b3-133">Сохраните файл текущего запроса.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-133">Save the current query file.</span></span>
2. <span data-ttu-id="ed4b3-134">Откройте сохраненный файл запроса.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-134">Open a saved query file.</span></span>
3. <span data-ttu-id="ed4b3-135">Создайте новый файл запроса.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-135">Create a new query file.</span></span>

## <a name="see-the-details"></a><span data-ttu-id="ed4b3-136">Просмотр подробных сведений</span><span class="sxs-lookup"><span data-stu-id="ed4b3-136">See the details</span></span>
<span data-ttu-id="ed4b3-137">Чтобы просмотреть полный список свойств какой-либо строки, разверните ее в результатах.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-137">Expand any row in the results to see its complete list of properties.</span></span> <span data-ttu-id="ed4b3-138">Можно также развернуть любое свойство, которое представляет собой структурированное значение, например пользовательские измерения или список стеков в исключении.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-138">You can further expand any property that is a structured value - for example, custom dimensions, or the stack listing in an exception.</span></span>

![Развертывание строки](./media/app-insights-analytics-using/070.png)

## <a name="arrange-the-results"></a><span data-ttu-id="ed4b3-140">Упорядочение результатов</span><span class="sxs-lookup"><span data-stu-id="ed4b3-140">Arrange the results</span></span>
<span data-ttu-id="ed4b3-141">Результаты, возвращаемые из запроса, можно сортировать, фильтровать, разбивать на страницы и группировать.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-141">You can sort, filter, paginate, and group the results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="ed4b3-142">При сортировке, группировании и фильтрации в браузере запрос не выполняется повторно.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-142">Sorting, grouping, and filtering in the browser don't re-run your query.</span></span> <span data-ttu-id="ed4b3-143">При этом только переупорядочиваются результаты, возвращенные последним запросом.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-143">They only rearrange the results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="ed4b3-144">Чтобы выполнить эти задачи на сервере до возвращения результатов, создайте запрос с операторами [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) и [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html).</span><span class="sxs-lookup"><span data-stu-id="ed4b3-144">To perform these tasks in the server before the results are returned, write your query with the [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="ed4b3-145">Выберите столбцы, которые необходимо просмотреть. Чтобы переупорядочить столбцы, необходимо перетащить их заголовки, а чтобы изменить их размер — перетащить их границы.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-145">Pick the columns you'd like to see, drag column headers to rearrange them, and resize columns by dragging their borders.</span></span>

![Упорядочивание столбцов](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="ed4b3-147">Сортировка и фильтрация элементов</span><span class="sxs-lookup"><span data-stu-id="ed4b3-147">Sort and filter items</span></span>
<span data-ttu-id="ed4b3-148">Чтобы отсортировать результаты, щелкните заголовок столбца.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-148">Sort your results by clicking the head of a column.</span></span> <span data-ttu-id="ed4b3-149">Щелкните еще раз, чтобы отсортировать в другом направлении, и третий раз, чтобы восстановить исходный порядок, возвращенный запросом.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-149">Click again to sort the other way, and click a third time to revert to the original ordering returned by your query.</span></span>

<span data-ttu-id="ed4b3-150">С помощью значка фильтра можно сузить область поиска.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-150">Use the filter icon to narrow your search.</span></span>

![Сортировка и фильтрация столбцов](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="ed4b3-152">Группирование элементов</span><span class="sxs-lookup"><span data-stu-id="ed4b3-152">Group items</span></span>
<span data-ttu-id="ed4b3-153">Чтобы отсортировать по нескольким столбцам, можно использовать группирование.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-153">To sort by more than one column, use grouping.</span></span> <span data-ttu-id="ed4b3-154">Сначала активируйте эту функцию, а затем перетащите заголовки столбцов в область над таблицей.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-154">First enable it, and then drag column headers into the space above the table.</span></span>

![Группа](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="ed4b3-156">Если некоторые результаты отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ed4b3-156">Missing some results?</span></span>

<span data-ttu-id="ed4b3-157">Если вы считаете, что отображены не все ожидаемые результаты, этому может быть несколько причин.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-157">If you think you're not seeing all the results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="ed4b3-158">**Фильтр диапазона времени**.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-158">**Time range filter**.</span></span> <span data-ttu-id="ed4b3-159">По умолчанию вы увидите только результаты за последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-159">By default, you will only see results from the last 24 hours.</span></span> <span data-ttu-id="ed4b3-160">Существует автоматический фильтр, который ограничивает диапазон результатов, полученных из исходных таблиц.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-160">There is an automatic filter that limits the range of results that are retrieved from the source tables.</span></span> 

    <span data-ttu-id="ed4b3-161">Тем не менее можно изменить фильтр диапазона времени, воспользовавшись раскрывающимся меню.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-161">However, you can change the time range filter by using the drop-down menu.</span></span>

    <span data-ttu-id="ed4b3-162">Или можно переопределить автоматический диапазон, добавив в запрос собственное [предложение `where  ... timestamp ...`](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html).</span><span class="sxs-lookup"><span data-stu-id="ed4b3-162">Or you can override the automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="ed4b3-163">Например:</span><span class="sxs-lookup"><span data-stu-id="ed4b3-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="ed4b3-164">**Ограничение результатов**.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-164">**Results limit**.</span></span> <span data-ttu-id="ed4b3-165">В результатах, возвращаемых с портала, есть ограничение в 10 тысяч строк.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-165">There's a limit of about 10k rows on the results returned from the portal.</span></span> <span data-ttu-id="ed4b3-166">Если вы превысите его, появится предупреждение.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-166">A warning shows if you go over the limit.</span></span> <span data-ttu-id="ed4b3-167">В этом случае при сортировке результатов в таблице не всегда будут представлены все первые или последние результаты.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-167">If that happens, sorting your results in the table won't always show you all the actual first or last results.</span></span> 

    <span data-ttu-id="ed4b3-168">Рекомендуется избегать превышения ограничения.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-168">It's good practice to avoid hitting the limit.</span></span> <span data-ttu-id="ed4b3-169">Используйте фильтр диапазона времени или операторы, в том числе следующие:</span><span class="sxs-lookup"><span data-stu-id="ed4b3-169">Use the time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="ed4b3-170">top 100 by timestamp;</span><span class="sxs-lookup"><span data-stu-id="ed4b3-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="ed4b3-171">take 100;</span><span class="sxs-lookup"><span data-stu-id="ed4b3-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="ed4b3-172">summarize </span><span class="sxs-lookup"><span data-stu-id="ed4b3-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="ed4b3-173">where timestamp > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="ed4b3-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="ed4b3-174">(Требуется более 10 тысяч строк?</span><span class="sxs-lookup"><span data-stu-id="ed4b3-174">(Want more than 10k rows?</span></span> <span data-ttu-id="ed4b3-175">Рассмотрите возможность использования [непрерывного экспорта](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="ed4b3-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="ed4b3-176">Аналитика предназначена для анализа, а не получения необработанных данных.)</span><span class="sxs-lookup"><span data-stu-id="ed4b3-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="ed4b3-177">Схемы</span><span class="sxs-lookup"><span data-stu-id="ed4b3-177">Diagrams</span></span>
<span data-ttu-id="ed4b3-178">Выберите тип схемы, которая вам нужна:</span><span class="sxs-lookup"><span data-stu-id="ed4b3-178">Select the type of diagram you'd like:</span></span>

![Выберите тип диаграммы](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="ed4b3-180">Если у вас несколько столбцов правильных типов, можно выбрать оси X и Y, а также столбец измерений, чтобы разделить по ним результаты.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-180">If you have several columns of the right types, you can choose the x and y axes, and a column of dimensions to split the results by.</span></span>

<span data-ttu-id="ed4b3-181">По умолчанию результаты изначально отображаются в виде таблицы, а схему вы выбираете вручную.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-181">By default, results are initially displayed as a table, and you select the diagram manually.</span></span> <span data-ttu-id="ed4b3-182">В конце запроса можно также использовать [директиву render](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) , чтобы выбрать диаграмму.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-182">But you can use the [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at the end of a query to select a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="ed4b3-183">Диагностика аналитики</span><span class="sxs-lookup"><span data-stu-id="ed4b3-183">Analytics diagnostics</span></span>


<span data-ttu-id="ed4b3-184">Если на временной диаграмме есть внезапный пик или шаг в данных, то вы можете видеть на линии выделенную точку.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on the line.</span></span> <span data-ttu-id="ed4b3-185">Это указывает на то, что диагностика аналитики выявила сочетание свойств, которое отфильтровывает внезапные изменения.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out the sudden change.</span></span> <span data-ttu-id="ed4b3-186">Щелкните данную точку, чтобы узнать больше о фильтре и просмотреть отфильтрованную версию.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-186">Click the point to get more detail on the filter, and to see the filtered version.</span></span> <span data-ttu-id="ed4b3-187">Эти сведения могут помочь определить причину изменения.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-187">This may help you identify what caused the change.</span></span> 

[<span data-ttu-id="ed4b3-188">Диагностика внезапных изменений в телеметрии приложения</span><span class="sxs-lookup"><span data-stu-id="ed4b3-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Диагностика аналитики](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-to-dashboard"></a><span data-ttu-id="ed4b3-190">Закрепление на панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="ed4b3-190">Pin to dashboard</span></span>
<span data-ttu-id="ed4b3-191">Вы можете закрепить диаграмму или таблицу на одной из [общих панелей мониторинга](app-insights-dashboards.md). Для этого просто щелкните значок булавки.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-191">You can pin a diagram or table to one of your [shared dashboards](app-insights-dashboards.md) - just click the pin.</span></span> <span data-ttu-id="ed4b3-192">(Для включения этой функции может потребоваться [обновить ценовой пакет приложения](app-insights-pricing.md).)</span><span class="sxs-lookup"><span data-stu-id="ed4b3-192">(You might need to [upgrade your app's pricing package](app-insights-pricing.md) to turn on this feature.)</span></span> 

![Щелкните значок булавки](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="ed4b3-194">Это означает, что при сборке панели мониторинга для отслеживания производительности или использования веб-служб наряду с другими метриками можно включить довольно сложный анализ.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-194">This means that, when you put together a dashboard to help you monitor the performance or usage of your web services, you can include quite complex analysis alongside the other metrics.</span></span> 

<span data-ttu-id="ed4b3-195">Если таблица содержит четыре столбца или меньше, вы можете закрепить ее на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-195">You can pin a table to the dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="ed4b3-196">Отображаются только семь верхних строк.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-196">Only the top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="ed4b3-197">Обновление панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="ed4b3-197">Dashboard refresh</span></span>
<span data-ttu-id="ed4b3-198">Диаграмма, закрепленная на панели мониторинга, обновляется автоматически при повторном выполнении запроса приблизительно каждые два часа.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-198">The chart pinned to the dashboard is refreshed automatically by re-running the query approximately every hours.</span></span> <span data-ttu-id="ed4b3-199">Вы также можете нажать кнопку "Обновить".</span><span class="sxs-lookup"><span data-stu-id="ed4b3-199">You can also click the Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="ed4b3-200">Автоматические упрощения</span><span class="sxs-lookup"><span data-stu-id="ed4b3-200">Automatic simplifications</span></span>

<span data-ttu-id="ed4b3-201">При закреплении на панели мониторинга к диаграмме применяются определенные упрощения.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-201">Certain simplifications are applied to a chart when you pin it to a dashboard.</span></span>

<span data-ttu-id="ed4b3-202">**Ограничение времени:** автоматически отображаются запросы только за последние 14 дней.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-202">**Time restriction:** Queries are automatically limited to the past 14 days.</span></span> <span data-ttu-id="ed4b3-203">Тот же эффект достигается добавлением в запрос `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-203">The effect is the same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="ed4b3-204">**Ограничение количества ячеек:** если отображается диаграмма, содержащая много отдельных ячеек (как правило, линейчатая диаграмма), менее заполненные ячейки автоматически группируются в одну ячейку под названием "Другие".</span><span class="sxs-lookup"><span data-stu-id="ed4b3-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), the less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="ed4b3-205">Например, запрос</span><span class="sxs-lookup"><span data-stu-id="ed4b3-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="ed4b3-206">в аналитике выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ed4b3-206">looks like this in Analytics:</span></span>

![Диаграмма с длинным "хвостом"](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="ed4b3-208">Но если закрепить его на панели мониторинга, он будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="ed4b3-208">but when you pin it to a dashboard, it looks like this:</span></span>

![Диаграмма с ограниченным количеством ячеек](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-to-excel"></a><span data-ttu-id="ed4b3-210">Экспорт в Excel</span><span class="sxs-lookup"><span data-stu-id="ed4b3-210">Export to Excel</span></span>
<span data-ttu-id="ed4b3-211">После выполнения запроса можно скачать CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="ed4b3-212">Щелкните **"Экспорт", Excel**.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-212">Click **Export,  Excel**.</span></span>

## <a name="export-to-power-bi"></a><span data-ttu-id="ed4b3-213">Экспорт в Power BI</span><span class="sxs-lookup"><span data-stu-id="ed4b3-213">Export to Power BI</span></span>
<span data-ttu-id="ed4b3-214">Поместите курсор в запрос и выберите **"Экспорт", Power BI**.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-214">Put the cursor in a query and choose **Export, Power BI**.</span></span>

![Экспорт из Log Analytics в Power BI](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="ed4b3-216">Выполните запрос в Power BI.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-216">You run the query in Power BI.</span></span> <span data-ttu-id="ed4b3-217">Вы можете задать обновление запроса по расписанию.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-217">You can set it to refresh on a schedule.</span></span>

<span data-ttu-id="ed4b3-218">С помощью Power BI вы можете создавать панели мониторинга, объединяющие данные из разных источников.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="ed4b3-219">Использование данных Application Insights в Power BI</span><span class="sxs-lookup"><span data-stu-id="ed4b3-219">Learn more about export to Power BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="ed4b3-220">Прямая ссылка</span><span class="sxs-lookup"><span data-stu-id="ed4b3-220">Deep link</span></span>

<span data-ttu-id="ed4b3-221">Получите ссылку в разделе **"Экспорт", "Поделиться ссылкой"**, которую можно отправить другому пользователю.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-221">Get a link under **Export, Share link** that you can send to another user.</span></span> <span data-ttu-id="ed4b3-222">Если у пользователя есть [доступ к группе ресурсов](app-insights-resources-roles-access-control.md), запрос откроется в пользовательском интерфейсе раздела аналитики.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-222">Provided the user has [access to your resource group](app-insights-resources-roles-access-control.md), the query will open in the Analytics UI.</span></span>

<span data-ttu-id="ed4b3-223">(В ссылке текст запроса в формате GZIP и в кодировке Base-64 отображается после "?q=".</span><span class="sxs-lookup"><span data-stu-id="ed4b3-223">(In the link, the query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="ed4b3-224">Вы можете написать код, чтобы создать прямые ссылки, которые можно предоставить пользователям.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-224">You could write code to generate deep links that you provide to users.</span></span> <span data-ttu-id="ed4b3-225">Тем не менее, мы рекомендуем запускать аналитику из кода с помощью [REST API](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="ed4b3-225">However, the recommended way to run Analytics from code is by using the [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="ed4b3-226">Служба автоматизации</span><span class="sxs-lookup"><span data-stu-id="ed4b3-226">Automation</span></span>

<span data-ttu-id="ed4b3-227">Используйте [REST API доступа к данным](https://dev.applicationinsights.io/) для выполнения запросов аналитики.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-227">Use the  [Data Access REST API](https://dev.applicationinsights.io/) to run Analytics queries.</span></span> <span data-ttu-id="ed4b3-228">[Пример](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (использование PowerShell):</span><span class="sxs-lookup"><span data-stu-id="ed4b3-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="ed4b3-229">В отличие от пользовательского интерфейса аналитики REST API не добавляет ограничения по меткам времени для запросов автоматически.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-229">Unlike the Analytics UI, the REST API does not automatically add any timestamp limitation to your queries.</span></span> <span data-ttu-id="ed4b3-230">Чтобы не получать объемные ответы, обязательно добавляйте собственные предложения where.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-230">Remember to add your own where-clause, to avoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="ed4b3-231">Импорт данных</span><span class="sxs-lookup"><span data-stu-id="ed4b3-231">Import data</span></span>

<span data-ttu-id="ed4b3-232">Можно импортировать данные из CSV-файла.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-232">You can import data from a CSV file.</span></span> <span data-ttu-id="ed4b3-233">Обычно это используется для импорта статических данных, которые можно объединить с таблицами из данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-233">A typical usage is to import static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="ed4b3-234">Например, если аутентифицированные пользователи идентифицируются в данных телеметрии по псевдониму или скрываемому идентификатору, то можно импортировать таблицу, которая позволяет сопоставить псевдонимы с настоящими именами.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases to real names.</span></span> <span data-ttu-id="ed4b3-235">В результате объединения данных телеметрии запросов пользователей в отчетах аналитики можно будет идентифицировать по их настоящим именам.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-235">By performing a join on the request telemetry, you can identify users by their real names in the Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="ed4b3-236">Определение схемы данных</span><span class="sxs-lookup"><span data-stu-id="ed4b3-236">Define your data schema</span></span>

1. <span data-ttu-id="ed4b3-237">Щелкните **Параметры** (в верхнем левом углу) и выберите **Источники данных**.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="ed4b3-238">Добавьте источник данных, следуя инструкциям.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-238">Add a data source, following the instructions.</span></span> <span data-ttu-id="ed4b3-239">Вам будет предложено указать пример данных, который должен содержать по крайней мере десять строк.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-239">You are asked to supply a sample of the data, which should include at least ten rows.</span></span> <span data-ttu-id="ed4b3-240">После этого можно исправить схему.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-240">You then correct the schema.</span></span>

<span data-ttu-id="ed4b3-241">Она определяет источник данных, который затем можно будет использовать для импорта отдельных таблиц.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-241">This defines a data source, which you can then use to import individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="ed4b3-242">Импорт таблицы</span><span class="sxs-lookup"><span data-stu-id="ed4b3-242">Import a table</span></span>

1. <span data-ttu-id="ed4b3-243">Откройте определение источника данных из списка.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-243">Open your data source definition from the list.</span></span>
2. <span data-ttu-id="ed4b3-244">Щелкните "Отправить" и следуйте инструкциям по передаче таблицы.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-244">Click "Upload" and follow the instructions to upload the table.</span></span> <span data-ttu-id="ed4b3-245">Данный процесс подразумевает вызов REST API, поэтому этот его очень легко автоматизировать.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-245">This involves a call to a REST API, and so it is easy to automate.</span></span> 

<span data-ttu-id="ed4b3-246">Таблица теперь доступна для использования в запросах аналитики.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="ed4b3-247">Она будет отображаться в Аналитике.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-247">It will appear in Analytics</span></span> 

### <a name="use-the-table"></a><span data-ttu-id="ed4b3-248">Использование таблицы</span><span class="sxs-lookup"><span data-stu-id="ed4b3-248">Use the table</span></span>

<span data-ttu-id="ed4b3-249">Предположим, что определение источника данных называется `usermap` и содержит два поля, `realName` и `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="ed4b3-250">В таблице `requests` также есть поле `user_AuthenticatedId`, так что их легко объединить.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-250">The `requests` table also has a field named `user_AuthenticatedId`, so it's easy to join them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="ed4b3-251">Результирующая таблица запросов содержит дополнительный столбец, `realName`.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-251">The resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="ed4b3-252">Импорт из LogStash</span><span class="sxs-lookup"><span data-stu-id="ed4b3-252">Import from LogStash</span></span>

<span data-ttu-id="ed4b3-253">Если вы используете [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), то можете использовать Аналитику для запроса журналов.</span><span class="sxs-lookup"><span data-stu-id="ed4b3-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics to query your logs.</span></span> <span data-ttu-id="ed4b3-254">Используйте [подключаемый модуль, который передает данные в Аналитику](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="ed4b3-254">Use the [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="ed4b3-255">Видео</span><span class="sxs-lookup"><span data-stu-id="ed4b3-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

