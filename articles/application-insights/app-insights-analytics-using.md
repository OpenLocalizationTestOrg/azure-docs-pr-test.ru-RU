---
title: "aaaUsing аналитика - hello мощное средство аналитики приложений Azure | Документы Microsoft"
description: "С помощью hello Analytics hello мощное средство диагностики поиска средство аналитики приложений. "
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
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="31e10-103">Использование аналитики в Application Insights</span><span class="sxs-lookup"><span data-stu-id="31e10-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="31e10-104">[Аналитика](app-insights-analytics.md) — мощное средство поиска функция hello [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="31e10-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="31e10-105">На этих страницах описан язык запросов Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="31e10-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="31e10-106">**[Вводное видео hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="31e10-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="31e10-107">**[Испытайте аналитика на нашем смоделированные данные](https://analytics.applicationinsights.io/demo)**  Если ваше приложение еще не отправляет данные tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="31e10-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="31e10-108">Открытие аналитики</span><span class="sxs-lookup"><span data-stu-id="31e10-108">Open Analytics</span></span>
<span data-ttu-id="31e10-109">В домашнем ресурсе вашего приложения в Application Insights щелкните "Аналитика".</span><span class="sxs-lookup"><span data-stu-id="31e10-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![На сайте portal.azure.com откройте ресурс Application Insights и щелкните "Аналитика".](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="31e10-111">Hello встроенного учебник дает некоторые сведения о возможностях.</span><span class="sxs-lookup"><span data-stu-id="31e10-111">hello inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="31e10-112">Смотрите [исчерпывающий обзор здесь](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="31e10-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="31e10-113">Запрос данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="31e10-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="31e10-114">Напишите запрос</span><span class="sxs-lookup"><span data-stu-id="31e10-114">Write a query</span></span>
![Отображение схемы](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="31e10-116">Начать с именами hello какой-либо таблицы hello в списке слева hello (или hello [диапазон](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) или [объединение](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) операторы).</span><span class="sxs-lookup"><span data-stu-id="31e10-116">Begin with hello names of any of hello tables listed on hello left (or hello [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="31e10-117">Используйте `|` toocreate в конвейер [операторы](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="31e10-117">Use `|` toocreate a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="31e10-118">IntelliSense предлагает операторы hello и элементы hello выражений, которые можно использовать.</span><span class="sxs-lookup"><span data-stu-id="31e10-118">IntelliSense prompts you with hello operators and hello expression elements that you can use.</span></span> <span data-ttu-id="31e10-119">Щелкните значок сведений hello (или нажмите клавиши CTRL + ПРОБЕЛ) tooget подробное описание и примеры toouse каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="31e10-119">Click hello information icon (or press CTRL+Space) tooget a longer description and examples of how toouse each element.</span></span>

<span data-ttu-id="31e10-120">В разделе hello [обзор языка Analytics](app-insights-analytics-tour.md) и [Справочник по языку](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="31e10-120">See hello [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="31e10-121">Выполнение запроса</span><span class="sxs-lookup"><span data-stu-id="31e10-121">Run a query</span></span>
![Выполнение запроса](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="31e10-123">В запросе можно использовать только однократные разрывы строк.</span><span class="sxs-lookup"><span data-stu-id="31e10-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="31e10-124">Поместите курсор hello внутри или в конце hello hello запроса, который должен toorun.</span><span class="sxs-lookup"><span data-stu-id="31e10-124">Put hello cursor inside or at hello end of hello query you want toorun.</span></span>
3. <span data-ttu-id="31e10-125">Проверьте hello диапазон времени запроса.</span><span class="sxs-lookup"><span data-stu-id="31e10-125">Check hello time range of your query.</span></span> <span data-ttu-id="31e10-126">(Его можно изменить или переопределить, добавив в запрос собственное предложение [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html).)</span><span class="sxs-lookup"><span data-stu-id="31e10-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="31e10-127">Нажмите кнопку Go toorun hello запрос.</span><span class="sxs-lookup"><span data-stu-id="31e10-127">Click Go toorun hello query.</span></span>
4. <span data-ttu-id="31e10-128">Не помещайте в запрос пустые строки.</span><span class="sxs-lookup"><span data-stu-id="31e10-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="31e10-129">На одной вкладке запроса можно хранить несколько отдельных запросов, разделив их пустыми строками.</span><span class="sxs-lookup"><span data-stu-id="31e10-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="31e10-130">Выполняется только hello запроса с курсором hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-130">Only hello query that has hello cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="31e10-131">Сохранение запроса</span><span class="sxs-lookup"><span data-stu-id="31e10-131">Save a query</span></span>
![Сохранение запроса](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="31e10-133">Сохраните текущий файл запрос hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-133">Save hello current query file.</span></span>
2. <span data-ttu-id="31e10-134">Откройте сохраненный файл запроса.</span><span class="sxs-lookup"><span data-stu-id="31e10-134">Open a saved query file.</span></span>
3. <span data-ttu-id="31e10-135">Создайте новый файл запроса.</span><span class="sxs-lookup"><span data-stu-id="31e10-135">Create a new query file.</span></span>

## <a name="see-hello-details"></a><span data-ttu-id="31e10-136">Просмотреть сведения о hello</span><span class="sxs-lookup"><span data-stu-id="31e10-136">See hello details</span></span>
<span data-ttu-id="31e10-137">Разверните любую строку в toosee результаты hello его полный список свойств.</span><span class="sxs-lookup"><span data-stu-id="31e10-137">Expand any row in hello results toosee its complete list of properties.</span></span> <span data-ttu-id="31e10-138">Далее можно развернуть любое свойство, например со структурированными значениями -, пользовательские измерения или стек hello в исключение.</span><span class="sxs-lookup"><span data-stu-id="31e10-138">You can further expand any property that is a structured value - for example, custom dimensions, or hello stack listing in an exception.</span></span>

![Развертывание строки](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a><span data-ttu-id="31e10-140">Упорядочить результаты hello</span><span class="sxs-lookup"><span data-stu-id="31e10-140">Arrange hello results</span></span>
<span data-ttu-id="31e10-141">Можно сортировать, фильтровать, разбиение на страницы и группы hello результаты, возвращаемые из запроса.</span><span class="sxs-lookup"><span data-stu-id="31e10-141">You can sort, filter, paginate, and group hello results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="31e10-142">Сортировка, Группировка и фильтрация в браузере hello не повторно выполнить запрос.</span><span class="sxs-lookup"><span data-stu-id="31e10-142">Sorting, grouping, and filtering in hello browser don't re-run your query.</span></span> <span data-ttu-id="31e10-143">Они только изменить hello результаты, возвращенные последнего запроса.</span><span class="sxs-lookup"><span data-stu-id="31e10-143">They only rearrange hello results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="31e10-144">tooperform этих задач в сервере hello, прежде чем hello результатов, написать собственный запрос с hello [сортировки](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [суммировать](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) и [где](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) операторы.</span><span class="sxs-lookup"><span data-stu-id="31e10-144">tooperform these tasks in hello server before hello results are returned, write your query with hello [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="31e10-145">Выбрать столбцы hello и как toosee, перетащите toorearrange заголовки столбцов, а также изменить размер столбцов, перетаскивая их границы.</span><span class="sxs-lookup"><span data-stu-id="31e10-145">Pick hello columns you'd like toosee, drag column headers toorearrange them, and resize columns by dragging their borders.</span></span>

![Упорядочивание столбцов](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="31e10-147">Сортировка и фильтрация элементов</span><span class="sxs-lookup"><span data-stu-id="31e10-147">Sort and filter items</span></span>
<span data-ttu-id="31e10-148">Результаты сортировки, щелкнув hello заголовка столбца.</span><span class="sxs-lookup"><span data-stu-id="31e10-148">Sort your results by clicking hello head of a column.</span></span> <span data-ttu-id="31e10-149">Снова щелкните toosort hello другим способом, а нажмите кнопку в третий раз toorevert toohello исходный порядок возвращаемые запросом.</span><span class="sxs-lookup"><span data-stu-id="31e10-149">Click again toosort hello other way, and click a third time toorevert toohello original ordering returned by your query.</span></span>

<span data-ttu-id="31e10-150">Используйте значок toonarrow hello фильтр поиска.</span><span class="sxs-lookup"><span data-stu-id="31e10-150">Use hello filter icon toonarrow your search.</span></span>

![Сортировка и фильтрация столбцов](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="31e10-152">Группирование элементов</span><span class="sxs-lookup"><span data-stu-id="31e10-152">Group items</span></span>
<span data-ttu-id="31e10-153">toosort по нескольким столбцам, используют группирование.</span><span class="sxs-lookup"><span data-stu-id="31e10-153">toosort by more than one column, use grouping.</span></span> <span data-ttu-id="31e10-154">Сначала ее включить, а затем перетащите заголовки столбцов в пространство hello над таблицей hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-154">First enable it, and then drag column headers into hello space above hello table.</span></span>

![Группа](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="31e10-156">Если некоторые результаты отсутствуют</span><span class="sxs-lookup"><span data-stu-id="31e10-156">Missing some results?</span></span>

<span data-ttu-id="31e10-157">Если вы считаете, что вы не видите все ожидаемые результаты hello, существует несколько возможных причин.</span><span class="sxs-lookup"><span data-stu-id="31e10-157">If you think you're not seeing all hello results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="31e10-158">**Фильтр диапазона времени**.</span><span class="sxs-lookup"><span data-stu-id="31e10-158">**Time range filter**.</span></span> <span data-ttu-id="31e10-159">По умолчанию вы увидите только результаты из hello последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="31e10-159">By default, you will only see results from hello last 24 hours.</span></span> <span data-ttu-id="31e10-160">Нет автоматический фильтр, который ограничивает диапазон hello результатов, которые извлекаются из исходных таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-160">There is an automatic filter that limits hello range of results that are retrieved from hello source tables.</span></span> 

    <span data-ttu-id="31e10-161">Тем не менее, можно изменить диапазон времени hello фильтра с помощью раскрывающегося меню hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-161">However, you can change hello time range filter by using hello drop-down menu.</span></span>

    <span data-ttu-id="31e10-162">Или можно переопределить hello автоматическое изменение диапазона, включая свою собственную [ `where  ... timestamp ...` предложение](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) в свой запрос.</span><span class="sxs-lookup"><span data-stu-id="31e10-162">Or you can override hello automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="31e10-163">Например:</span><span class="sxs-lookup"><span data-stu-id="31e10-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="31e10-164">**Ограничение результатов**.</span><span class="sxs-lookup"><span data-stu-id="31e10-164">**Results limit**.</span></span> <span data-ttu-id="31e10-165">Ограничено 10 тысяч строк на hello результаты, возвращаемые из портала hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-165">There's a limit of about 10k rows on hello results returned from hello portal.</span></span> <span data-ttu-id="31e10-166">Предупреждение показывает, переходе превышении hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-166">A warning shows if you go over hello limit.</span></span> <span data-ttu-id="31e10-167">В этом случае Сортировка результатов в таблице hello не всегда показывают все hello фактические первой или последней результаты.</span><span class="sxs-lookup"><span data-stu-id="31e10-167">If that happens, sorting your results in hello table won't always show you all hello actual first or last results.</span></span> 

    <span data-ttu-id="31e10-168">Это ограничение hello попадание tooavoid рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="31e10-168">It's good practice tooavoid hitting hello limit.</span></span> <span data-ttu-id="31e10-169">Использовать фильтр по диапазону времени hello, или использовать операторы, такие как:</span><span class="sxs-lookup"><span data-stu-id="31e10-169">Use hello time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="31e10-170">top 100 by timestamp;</span><span class="sxs-lookup"><span data-stu-id="31e10-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="31e10-171">take 100;</span><span class="sxs-lookup"><span data-stu-id="31e10-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="31e10-172">summarize </span><span class="sxs-lookup"><span data-stu-id="31e10-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="31e10-173">where timestamp > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="31e10-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="31e10-174">(Требуется более 10 тысяч строк?</span><span class="sxs-lookup"><span data-stu-id="31e10-174">(Want more than 10k rows?</span></span> <span data-ttu-id="31e10-175">Рассмотрите возможность использования [непрерывного экспорта](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="31e10-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="31e10-176">Аналитика предназначена для анализа, а не получения необработанных данных.)</span><span class="sxs-lookup"><span data-stu-id="31e10-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="31e10-177">Схемы</span><span class="sxs-lookup"><span data-stu-id="31e10-177">Diagrams</span></span>
<span data-ttu-id="31e10-178">Выберите тип диаграммы, которую вы хотите hello:</span><span class="sxs-lookup"><span data-stu-id="31e10-178">Select hello type of diagram you'd like:</span></span>

![Выберите тип диаграммы](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="31e10-180">Если имеется несколько столбцов типов правой hello, вы можете hello x и оси y и столбец измерения toosplit hello результаты по.</span><span class="sxs-lookup"><span data-stu-id="31e10-180">If you have several columns of hello right types, you can choose hello x and y axes, and a column of dimensions toosplit hello results by.</span></span>

<span data-ttu-id="31e10-181">По умолчанию изначально результаты отображаются в виде таблицы и диаграммы hello выбрать вручную.</span><span class="sxs-lookup"><span data-stu-id="31e10-181">By default, results are initially displayed as a table, and you select hello diagram manually.</span></span> <span data-ttu-id="31e10-182">Но вы можете использовать hello [визуализации директива](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) конце hello запроса tooselect диаграмму.</span><span class="sxs-lookup"><span data-stu-id="31e10-182">But you can use hello [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at hello end of a query tooselect a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="31e10-183">Диагностика аналитики</span><span class="sxs-lookup"><span data-stu-id="31e10-183">Analytics diagnostics</span></span>


<span data-ttu-id="31e10-184">На timechart Если неожиданный всплеск или этапа в данных, может появиться точки выделенной строке hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on hello line.</span></span> <span data-ttu-id="31e10-185">Это означает, что аналитика диагностики определил сочетания свойств, которые отфильтровать hello внезапные изменения.</span><span class="sxs-lookup"><span data-stu-id="31e10-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out hello sudden change.</span></span> <span data-ttu-id="31e10-186">Дополнительные сведения о фильтрации hello и toosee hello отфильтрованной версии нажмите кнопку tooget точки hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-186">Click hello point tooget more detail on hello filter, and toosee hello filtered version.</span></span> <span data-ttu-id="31e10-187">Это может помочь определить, какие изменения вызвало hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-187">This may help you identify what caused hello change.</span></span> 

[<span data-ttu-id="31e10-188">Диагностика внезапных изменений в телеметрии приложения</span><span class="sxs-lookup"><span data-stu-id="31e10-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Диагностика аналитики](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a><span data-ttu-id="31e10-190">Toodashboard ПИН-кода</span><span class="sxs-lookup"><span data-stu-id="31e10-190">Pin toodashboard</span></span>
<span data-ttu-id="31e10-191">Вы можете закрепить tooone схему или таблицу из вашего [общих панелей мониторинга](app-insights-dashboards.md) -просто щелкните hello ПИН-код.</span><span class="sxs-lookup"><span data-stu-id="31e10-191">You can pin a diagram or table tooone of your [shared dashboards](app-insights-dashboards.md) - just click hello pin.</span></span> <span data-ttu-id="31e10-192">(Может потребоваться слишком[обновления приложения тарифного пакета](app-insights-pricing.md) tooturn эту функцию.)</span><span class="sxs-lookup"><span data-stu-id="31e10-192">(You might need too[upgrade your app's pricing package](app-insights-pricing.md) tooturn on this feature.)</span></span> 

![Нажмите кнопку hello ПИН-кода](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="31e10-194">Это означает, что при сборке toohelp панели мониторинга, мониторинг производительности hello или использования веб-служб, можно включить довольно сложными analysis рядом с hello другие показатели.</span><span class="sxs-lookup"><span data-stu-id="31e10-194">This means that, when you put together a dashboard toohelp you monitor hello performance or usage of your web services, you can include quite complex analysis alongside hello other metrics.</span></span> 

<span data-ttu-id="31e10-195">Можно закрепить панель мониторинга toohello таблицы, если у него есть четыре или меньшее число столбцов.</span><span class="sxs-lookup"><span data-stu-id="31e10-195">You can pin a table toohello dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="31e10-196">Отображаются только hello первые семь строк.</span><span class="sxs-lookup"><span data-stu-id="31e10-196">Only hello top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="31e10-197">Обновление панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="31e10-197">Dashboard refresh</span></span>
<span data-ttu-id="31e10-198">мониторинга toohello Hello закрепить диаграммы автоматически обновляются примерно каждые часов повторным запуском запроса hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-198">hello chart pinned toohello dashboard is refreshed automatically by re-running hello query approximately every hours.</span></span> <span data-ttu-id="31e10-199">Кроме того, можно нажать кнопку обновления hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-199">You can also click hello Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="31e10-200">Автоматические упрощения</span><span class="sxs-lookup"><span data-stu-id="31e10-200">Automatic simplifications</span></span>

<span data-ttu-id="31e10-201">Определенные упрощения, примененные tooa диаграммы, когда вы Закрепить панель мониторинга tooa.</span><span class="sxs-lookup"><span data-stu-id="31e10-201">Certain simplifications are applied tooa chart when you pin it tooa dashboard.</span></span>

<span data-ttu-id="31e10-202">**Ограничение времени:** запросы, ограничивают выбор toohello за последние 14 дней.</span><span class="sxs-lookup"><span data-stu-id="31e10-202">**Time restriction:** Queries are automatically limited toohello past 14 days.</span></span> <span data-ttu-id="31e10-203">Hello эффект hello же, как если запрос включает `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="31e10-203">hello effect is hello same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="31e10-204">**Ограничение на количество ячеек:** Если отобразить диаграмму, которая содержит много дискретных ячейки (обычно линейчатую диаграмму), меньше заполненных ячеек автоматически группируются в одном «другие» hello ячейки.</span><span class="sxs-lookup"><span data-stu-id="31e10-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), hello less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="31e10-205">Например, запрос</span><span class="sxs-lookup"><span data-stu-id="31e10-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="31e10-206">в аналитике выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="31e10-206">looks like this in Analytics:</span></span>

![Диаграмма с длинным "хвостом"](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="31e10-208">Однако при закреплении его tooa панели мониторинга, он выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="31e10-208">but when you pin it tooa dashboard, it looks like this:</span></span>

![Диаграмма с ограниченным количеством ячеек](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a><span data-ttu-id="31e10-210">Экспортировать tooExcel</span><span class="sxs-lookup"><span data-stu-id="31e10-210">Export tooExcel</span></span>
<span data-ttu-id="31e10-211">После выполнения запроса можно скачать CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="31e10-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="31e10-212">Щелкните **"Экспорт", Excel**.</span><span class="sxs-lookup"><span data-stu-id="31e10-212">Click **Export,  Excel**.</span></span>

## <a name="export-toopower-bi"></a><span data-ttu-id="31e10-213">Экспорт tooPower бизнес-Аналитики</span><span class="sxs-lookup"><span data-stu-id="31e10-213">Export tooPower BI</span></span>
<span data-ttu-id="31e10-214">Поместите курсор hello в запросе и выберите **экспорта Power BI**.</span><span class="sxs-lookup"><span data-stu-id="31e10-214">Put hello cursor in a query and choose **Export, Power BI**.</span></span>

![Экспорт из Analytics tooPower бизнес-Аналитики](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="31e10-216">При выполнении запроса hello в Power BI</span><span class="sxs-lookup"><span data-stu-id="31e10-216">You run hello query in Power BI.</span></span> <span data-ttu-id="31e10-217">Может быть задана toorefresh по расписанию.</span><span class="sxs-lookup"><span data-stu-id="31e10-217">You can set it toorefresh on a schedule.</span></span>

<span data-ttu-id="31e10-218">С помощью Power BI вы можете создавать панели мониторинга, объединяющие данные из разных источников.</span><span class="sxs-lookup"><span data-stu-id="31e10-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="31e10-219">Дополнительные сведения об экспорте tooPower бизнес-Аналитики</span><span class="sxs-lookup"><span data-stu-id="31e10-219">Learn more about export tooPower BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="31e10-220">Прямая ссылка</span><span class="sxs-lookup"><span data-stu-id="31e10-220">Deep link</span></span>

<span data-ttu-id="31e10-221">Получить ссылку в разделе **Экспорт общей ссылки** следует отправить tooanother пользователя.</span><span class="sxs-lookup"><span data-stu-id="31e10-221">Get a link under **Export, Share link** that you can send tooanother user.</span></span> <span data-ttu-id="31e10-222">Предоставляемый пользователем hello [группы ресурсов tooyour доступ](app-insights-resources-roles-access-control.md), hello запрос будет открываться в hello Analytics пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="31e10-222">Provided hello user has [access tooyour resource group](app-insights-resources-roles-access-control.md), hello query will open in hello Analytics UI.</span></span>

<span data-ttu-id="31e10-223">(В ссылке hello hello текст запроса появляется после «? q =», сжимаются gzip и в кодировке base-64.</span><span class="sxs-lookup"><span data-stu-id="31e10-223">(In hello link, hello query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="31e10-224">Можно написать код toogenerate прямые ссылки необходимо указать toousers.</span><span class="sxs-lookup"><span data-stu-id="31e10-224">You could write code toogenerate deep links that you provide toousers.</span></span> <span data-ttu-id="31e10-225">Однако рекомендуется использовать hello toorun способом Analytics из кода можно с помощью hello [API-интерфейса REST](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="31e10-225">However, hello recommended way toorun Analytics from code is by using hello [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="31e10-226">Служба автоматизации</span><span class="sxs-lookup"><span data-stu-id="31e10-226">Automation</span></span>

<span data-ttu-id="31e10-227">Используйте hello [REST API-Интерфейс](https://dev.applicationinsights.io/) toorun аналитические запросы.</span><span class="sxs-lookup"><span data-stu-id="31e10-227">Use hello  [Data Access REST API](https://dev.applicationinsights.io/) toorun Analytics queries.</span></span> <span data-ttu-id="31e10-228">[Пример](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (использование PowerShell):</span><span class="sxs-lookup"><span data-stu-id="31e10-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="31e10-229">В отличие от hello Analytics пользовательского интерфейса hello API-интерфейса REST автоматически не добавляются все запросы tooyour ограничение отметки времени.</span><span class="sxs-lookup"><span data-stu-id="31e10-229">Unlike hello Analytics UI, hello REST API does not automatically add any timestamp limitation tooyour queries.</span></span> <span data-ttu-id="31e10-230">Помните tooadd собственные-предложения where, tooavoid получения огромный ответов.</span><span class="sxs-lookup"><span data-stu-id="31e10-230">Remember tooadd your own where-clause, tooavoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="31e10-231">Импорт данных</span><span class="sxs-lookup"><span data-stu-id="31e10-231">Import data</span></span>

<span data-ttu-id="31e10-232">Можно импортировать данные из CSV-файла.</span><span class="sxs-lookup"><span data-stu-id="31e10-232">You can import data from a CSV file.</span></span> <span data-ttu-id="31e10-233">Типичным использованием является tooimport статические данные, можно присоединить с таблицами, с помощью телеметрии.</span><span class="sxs-lookup"><span data-stu-id="31e10-233">A typical usage is tooimport static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="31e10-234">Например в случае прошедших проверку подлинности пользователей в телеметрии скрытый идентификатор или псевдоним, можно импортировать таблицу, которая сопоставляет имена tooreal псевдонимы.</span><span class="sxs-lookup"><span data-stu-id="31e10-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases tooreal names.</span></span> <span data-ttu-id="31e10-235">В результате соединения hello телеметрии запроса, можно определить пользователей, их реальные имена в отчетах аналитики hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-235">By performing a join on hello request telemetry, you can identify users by their real names in hello Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="31e10-236">Определение схемы данных</span><span class="sxs-lookup"><span data-stu-id="31e10-236">Define your data schema</span></span>

1. <span data-ttu-id="31e10-237">Щелкните **Параметры** (в верхнем левом углу) и выберите **Источники данных**.</span><span class="sxs-lookup"><span data-stu-id="31e10-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="31e10-238">Добавление источника данных, следуя инструкциям hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-238">Add a data source, following hello instructions.</span></span> <span data-ttu-id="31e10-239">Вы являетесь задаваемые toosupply образец hello данных, который должен содержать по крайней мере 10 строк.</span><span class="sxs-lookup"><span data-stu-id="31e10-239">You are asked toosupply a sample of hello data, which should include at least ten rows.</span></span> <span data-ttu-id="31e10-240">Исправьте схему hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-240">You then correct hello schema.</span></span>

<span data-ttu-id="31e10-241">Определяет источник данных, который затем можно будет использовать tooimport отдельных таблиц.</span><span class="sxs-lookup"><span data-stu-id="31e10-241">This defines a data source, which you can then use tooimport individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="31e10-242">Импорт таблицы</span><span class="sxs-lookup"><span data-stu-id="31e10-242">Import a table</span></span>

1. <span data-ttu-id="31e10-243">Откройте определение источника данных из списка hello.</span><span class="sxs-lookup"><span data-stu-id="31e10-243">Open your data source definition from hello list.</span></span>
2. <span data-ttu-id="31e10-244">Нажмите кнопку «Отправить» и следуйте hello инструкции tooupload hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="31e10-244">Click "Upload" and follow hello instructions tooupload hello table.</span></span> <span data-ttu-id="31e10-245">Это включает в себя tooa вызова интерфейса API REST, и в этом случае легко tooautomate.</span><span class="sxs-lookup"><span data-stu-id="31e10-245">This involves a call tooa REST API, and so it is easy tooautomate.</span></span> 

<span data-ttu-id="31e10-246">Таблица теперь доступна для использования в запросах аналитики.</span><span class="sxs-lookup"><span data-stu-id="31e10-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="31e10-247">Она будет отображаться в Аналитике.</span><span class="sxs-lookup"><span data-stu-id="31e10-247">It will appear in Analytics</span></span> 

### <a name="use-hello-table"></a><span data-ttu-id="31e10-248">Используйте таблицу hello</span><span class="sxs-lookup"><span data-stu-id="31e10-248">Use hello table</span></span>

<span data-ttu-id="31e10-249">Предположим, что определение источника данных называется `usermap` и содержит два поля, `realName` и `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="31e10-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="31e10-250">Hello `requests` таблица также содержит поле с именем `user_AuthenticatedId`, поэтому его легко toojoin их:</span><span class="sxs-lookup"><span data-stu-id="31e10-250">hello `requests` table also has a field named `user_AuthenticatedId`, so it's easy toojoin them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="31e10-251">Hello результирующая таблица запросов имеет дополнительный столбец, `realName`.</span><span class="sxs-lookup"><span data-stu-id="31e10-251">hello resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="31e10-252">Импорт из LogStash</span><span class="sxs-lookup"><span data-stu-id="31e10-252">Import from LogStash</span></span>

<span data-ttu-id="31e10-253">Если вы используете [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), можно использовать tooquery аналитика журналов.</span><span class="sxs-lookup"><span data-stu-id="31e10-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics tooquery your logs.</span></span> <span data-ttu-id="31e10-254">Используйте hello [подключаемого модуля, который передает данные в Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="31e10-254">Use hello [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="31e10-255">Видео</span><span class="sxs-lookup"><span data-stu-id="31e10-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

