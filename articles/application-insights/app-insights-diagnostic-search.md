---
title: "aaaUsing поиска в Azure Application Insights | Документы Microsoft"
description: "Поиск и фильтрация необработанных данных телеметрии, отправляемых веб-приложением."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="ec7f7-103">Поиск в Application Insights</span><span class="sxs-lookup"><span data-stu-id="ec7f7-103">Using Search in Application Insights</span></span>
<span data-ttu-id="ec7f7-104">Функция поиска [Application Insights](app-insights-overview.md) использовать toofind и исследовать телеметрии отдельные элементы, такие как представления страниц, исключения или веб-запросов.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use toofind and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="ec7f7-105">Также можно просматривать журнал трассировки и события, которые были закодированы.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="ec7f7-106">(Для более сложных запросов к данным используйте [Analytics](app-insights-analytics-tour.md).)</span><span class="sxs-lookup"><span data-stu-id="ec7f7-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="ec7f7-107">Как найти функцию поиска?</span><span class="sxs-lookup"><span data-stu-id="ec7f7-107">Where do you see Search?</span></span>
### <a name="in-hello-azure-portal"></a><span data-ttu-id="ec7f7-108">В hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ec7f7-108">In hello Azure portal</span></span>
<span data-ttu-id="ec7f7-109">Поиск диагностики можно открыть явно из колонки Обзор аналитики приложения hello приложения:</span><span class="sxs-lookup"><span data-stu-id="ec7f7-109">You can open diagnostic search explicitly from hello Application Insights Overview blade of your application:</span></span>

![Откройте поиск по журналу диагностики](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="ec7f7-111">Она также открывается при щелчке некоторых диаграмм и элементов сетки.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="ec7f7-112">В этом случае его фильтров предварительно задан toofocus на hello тип выбранного элемента.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-112">In this case, its filters are pre-set toofocus on hello type of item you selected.</span></span> 

<span data-ttu-id="ec7f7-113">Например в колонке Обзор hello, представляет собой линейчатую диаграмму, запросов, относящихся к времени ответа.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-113">For example, on hello Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="ec7f7-114">Переходите toosee диапазон производительности список отдельных запросов, время отклика диапазоном.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-114">Click through a performance range toosee a list of individual requests in that response time range:</span></span>

![Выбор производительности запроса](./media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="ec7f7-116">основной текст Hello диагностики поиска является список элементов телеметрии - запросов сервера страница представления, пользовательские события, которые были закодированы и т. д.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-116">hello main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="ec7f7-117">Hello вверху списка hello является Сводка диаграмма, отображающая счетчики событий со временем.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-117">At hello top of hello list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="ec7f7-118">Нажмите кнопку обновления tooget новые события.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-118">Click Refresh tooget new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="ec7f7-119">В Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ec7f7-119">In Visual Studio</span></span>

<span data-ttu-id="ec7f7-120">В Visual Studio также есть окно поиска по Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="ec7f7-121">Это может пригодиться для отображения телеметрии события, создаваемые приложением hello, который выполняется отладка.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-121">It's most useful for displaying telemetry events generated by hello application that you're debugging.</span></span> <span data-ttu-id="ec7f7-122">Однако также можно показать hello события, полученные от опубликованного приложения в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-122">But it can also show hello events collected from your published app at hello Azure portal.</span></span>

<span data-ttu-id="ec7f7-123">Откройте окно поиска hello в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ec7f7-123">Open hello Search window in Visual Studio:</span></span>

![Как открыть окно "Поиск по Application Insights" в Visual Studio](./media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="ec7f7-125">окно поиска Hello имеет аналогичные функции toohello веб-портала.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-125">hello Search window has features similar toohello web portal:</span></span>

![Окно "Поиск по Application Insights" в Visual Studio](./media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="ec7f7-127">Вкладка операции отслеживания Hello отображается при открытии запроса или вид страницы.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-127">hello Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="ec7f7-128">"Операция" — это последовательность событий, связанный с tooa одного запроса или страницы представления.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-128">An 'operation' is a sequence of events that is associated with tooa single request or page view.</span></span> <span data-ttu-id="ec7f7-129">В одну операцию могут входить, например, вызовы зависимостей, исключения, журналы трассировки и пользовательские события.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="ec7f7-130">на вкладке выводятся операции отслеживания Hello графически hello времени и продолжительности эти события в представлении запроса или страница toohello отношения.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-130">hello Track Operation tab shows graphically hello timing and duration of these events in relation toohello request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="ec7f7-131">Проверка отдельных элементов</span><span class="sxs-lookup"><span data-stu-id="ec7f7-131">Inspect individual items</span></span>
<span data-ttu-id="ec7f7-132">Выберите все поля ключа toosee элемента телеметрии и связанных элементов.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-132">Select any telemetry item toosee key fields and related items.</span></span> <span data-ttu-id="ec7f7-133">Toosee hello полный набор полей, нажмите кнопку «...».</span><span class="sxs-lookup"><span data-stu-id="ec7f7-133">If you want toosee hello full set of fields, click "...".</span></span> 

![Щелкните новый рабочий элемент, изменить поля hello и нажмите кнопку ОК.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="ec7f7-135">Фильтрация по типам событий</span><span class="sxs-lookup"><span data-stu-id="ec7f7-135">Filter event types</span></span>
<span data-ttu-id="ec7f7-136">Откройте колонку hello фильтр и выберите типы событий hello, вы хотите toosee.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-136">Open hello Filter blade and choose hello event types you want toosee.</span></span> <span data-ttu-id="ec7f7-137">(Если более поздней версии, нужно фильтры hello toorestore, с которыми вы открыли колонке hello, щелкните Reset).</span><span class="sxs-lookup"><span data-stu-id="ec7f7-137">(If, later, you want toorestore hello filters with which you opened hello blade, click Reset.)</span></span>

![Щелкните "Фильтр" и укажите типы элементов телеметрии](./media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="ec7f7-139">Ниже приведены типы событий Hello.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-139">hello event types are:</span></span>

* <span data-ttu-id="ec7f7-140">**Трассировка**  -  [журналы диагностики](app-insights-asp-net-trace-logs.md), в том числе TrackTrace, log4Net, NLog и вызовы System.Diagnostic.Trace.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="ec7f7-141">**Запрос** — HTTP-запросы, полученные серверным приложением, включая страницы, скрипты, изображения, файлы стилей и данные.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="ec7f7-142">Эти события — это используемые toocreate hello запроса и ответа Обзор диаграммы.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-142">These events are used toocreate hello request and response overview charts.</span></span>
* <span data-ttu-id="ec7f7-143">**Представление страницы** - [телеметрии, отправленные клиентом веб-hello](app-insights-javascript.md), используемые toocreate страницы Просмотр отчетов.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-143">**Page View** - [Telemetry sent by hello web client](app-insights-javascript.md), used toocreate page view reports.</span></span> 
* <span data-ttu-id="ec7f7-144">**Пользовательское событие** — Если было введено tooTrackEvent() вызывает в порядке слишком[наблюдение за использованием](app-insights-api-custom-events-metrics.md), их можно найти здесь.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-144">**Custom Event** - If you inserted calls tooTrackEvent() in order too[monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="ec7f7-145">**Исключение** - неперехваченных [исключения в hello server](app-insights-asp-net-exceptions.md)и те, которые войдите, используя TrackException().</span><span class="sxs-lookup"><span data-stu-id="ec7f7-145">**Exception** - Uncaught [exceptions in hello server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="ec7f7-146">**Зависимости** - [вызовы из приложения сервера](app-insights-asp-net-dependencies.md) tooother служб, например API-интерфейс REST или баз данных, а также вызовы AJAX с вашей [клиентский код](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="ec7f7-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) tooother services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="ec7f7-147">**Доступность** — результаты [тестов доступности](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="ec7f7-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="ec7f7-148">Фильтрация на основе значений свойств</span><span class="sxs-lookup"><span data-stu-id="ec7f7-148">Filter on property values</span></span>
<span data-ttu-id="ec7f7-149">Можно отфильтровать такие события на hello значения их свойств.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-149">You can filter events on hello values of their properties.</span></span> <span data-ttu-id="ec7f7-150">Hello доступные свойства зависят от выбранных типов событий hello.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-150">hello available properties depend on hello event types you selected.</span></span> 

<span data-ttu-id="ec7f7-151">Например, можно выбрать запросы с определенным кодом ответа.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-151">For example, pick out requests with a specific response code.</span></span> 

![Разверните свойство и выберите значение](./media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="ec7f7-153">Выбор значения конкретного свойства не имеет тот же эффект, как выбор всех значений hello.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-153">Choosing no values of a particular property has hello same effect as choosing all values.</span></span> <span data-ttu-id="ec7f7-154">Фильтрация по этому свойству будет отключена.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="ec7f7-155">Сужение области поиска</span><span class="sxs-lookup"><span data-stu-id="ec7f7-155">Narrow your search</span></span>
<span data-ttu-id="ec7f7-156">Обратите внимание, что этот hello подсчитывает toohello справа от значения фильтра hello показывать число вхождений существует в текущем наборе отфильтрованные hello.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-156">Notice that hello counts toohello right of hello filter values show how many occurrences there are in hello current filtered set.</span></span> 

<span data-ttu-id="ec7f7-157">В этом примере ясно, что этот запрос «Rpt/сотрудники» hello приводит большинство ошибок hello "500":</span><span class="sxs-lookup"><span data-stu-id="ec7f7-157">In this example, it's clear that hello 'Rpt/Employees' request results in most of hello '500' errors:</span></span>

![Разверните свойство и выберите значение](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a><span data-ttu-id="ec7f7-159">Найти события с hello одного свойства</span><span class="sxs-lookup"><span data-stu-id="ec7f7-159">Find events with hello same property</span></span>
<span data-ttu-id="ec7f7-160">Найти Здравствуйте, все элементы, которые hello же значение свойства:</span><span class="sxs-lookup"><span data-stu-id="ec7f7-160">Find all hello items with hello same property value:</span></span>

![Щелкните правой кнопкой мыши свойство](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a><span data-ttu-id="ec7f7-162">Поиск данных hello</span><span class="sxs-lookup"><span data-stu-id="ec7f7-162">Search hello data</span></span>

> [!NOTE]
> <span data-ttu-id="ec7f7-163">toowrite более сложные запросы, откройте [ **Analytics** ](app-insights-analytics-tour.md) из hello верхней части колонки поиска hello.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-163">toowrite more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from hello top of hello Search blade.</span></span>
> 

<span data-ttu-id="ec7f7-164">Можно выполнить поиск условия в любом hello значений свойств.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-164">You can search for terms in any of hello property values.</span></span> <span data-ttu-id="ec7f7-165">Это особенно полезно, если вы написали [пользовательские события](app-insights-api-custom-events-metrics.md) со значениями свойств.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="ec7f7-166">Может потребоваться tooset диапазон времени, как поиск на короткий период, выполняются быстрее.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-166">You might want tooset a time range, as searches over a shorter range are faster.</span></span> 

![Откройте поиск по журналу диагностики](./media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="ec7f7-168">Выполните поиск по полным словам, а не по подстрокам.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="ec7f7-169">Используйте кавычки tooenclose специальные символы.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-169">Use quotation marks tooenclose special characters.</span></span>

| <span data-ttu-id="ec7f7-170">string</span><span class="sxs-lookup"><span data-stu-id="ec7f7-170">string</span></span> | <span data-ttu-id="ec7f7-171">*не* найдена по словам</span><span class="sxs-lookup"><span data-stu-id="ec7f7-171">is *not* found by</span></span> | <span data-ttu-id="ec7f7-172">но найдена по словам</span><span class="sxs-lookup"><span data-stu-id="ec7f7-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec7f7-173">HomeController.About</span><span class="sxs-lookup"><span data-stu-id="ec7f7-173">HomeController.About</span></span> |<span data-ttu-id="ec7f7-174">home</span><span class="sxs-lookup"><span data-stu-id="ec7f7-174">home</span></span><br/><span data-ttu-id="ec7f7-175">controller</span><span class="sxs-lookup"><span data-stu-id="ec7f7-175">controller</span></span><br/><span data-ttu-id="ec7f7-176">out</span><span class="sxs-lookup"><span data-stu-id="ec7f7-176">out</span></span> | <span data-ttu-id="ec7f7-177">homecontroller</span><span class="sxs-lookup"><span data-stu-id="ec7f7-177">homecontroller</span></span><br/><span data-ttu-id="ec7f7-178">about</span><span class="sxs-lookup"><span data-stu-id="ec7f7-178">about</span></span><br/><span data-ttu-id="ec7f7-179">"homecontroller.about"</span><span class="sxs-lookup"><span data-stu-id="ec7f7-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="ec7f7-180">США</span><span class="sxs-lookup"><span data-stu-id="ec7f7-180">United States</span></span>|<span data-ttu-id="ec7f7-181">Сое</span><span class="sxs-lookup"><span data-stu-id="ec7f7-181">Uni</span></span><br/><span data-ttu-id="ec7f7-182">диненные</span><span class="sxs-lookup"><span data-stu-id="ec7f7-182">ted</span></span>|<span data-ttu-id="ec7f7-183">соединенные</span><span class="sxs-lookup"><span data-stu-id="ec7f7-183">united</span></span><br/><span data-ttu-id="ec7f7-184">штаты</span><span class="sxs-lookup"><span data-stu-id="ec7f7-184">states</span></span><br/><span data-ttu-id="ec7f7-185">соединенные AND штаты</span><span class="sxs-lookup"><span data-stu-id="ec7f7-185">united AND states</span></span><br/><span data-ttu-id="ec7f7-186">"соединенные штаты"</span><span class="sxs-lookup"><span data-stu-id="ec7f7-186">"united states"</span></span>

<span data-ttu-id="ec7f7-187">Ниже приведены hello выражения поиска, которые можно использовать.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-187">Here are hello search expressions you can use:</span></span>

| <span data-ttu-id="ec7f7-188">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="ec7f7-188">Sample query</span></span> | <span data-ttu-id="ec7f7-189">Результат</span><span class="sxs-lookup"><span data-stu-id="ec7f7-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="ec7f7-190">Найти все события за период времени hello, поля которых есть слово hello «apple»</span><span class="sxs-lookup"><span data-stu-id="ec7f7-190">Find all events in hello time range whose fields include hello word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="ec7f7-191">Поиск событий, содержащих оба слова.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-191">Find events that contain both words.</span></span> <span data-ttu-id="ec7f7-192">Используйте "AND" заглавными буквами, а не "and".</span><span class="sxs-lookup"><span data-stu-id="ec7f7-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="ec7f7-193">Поиск событий, содержащих любое из этих слов.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-193">Find events that contain either word.</span></span> <span data-ttu-id="ec7f7-194">Используйте «OR» заглавными буквами, а не «or».</span><span class="sxs-lookup"><span data-stu-id="ec7f7-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="ec7f7-195">Короткая форма.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="ec7f7-196">Найти события, содержащие одно слово, но не hello других.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-196">Find events that contain one word but not hello other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="ec7f7-197">Выборка</span><span class="sxs-lookup"><span data-stu-id="ec7f7-197">Sampling</span></span>
<span data-ttu-id="ec7f7-198">Если приложение создает большой объем данных телеметрии (при использовании hello 2.0.0-beta3 версии пакета SDK для ASP.NET или более поздней версии), модуль адаптивной выборки hello автоматически уменьшает hello тома, отправляемое toohello портала, отправляя репрезентативной часть событий.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-198">If your app generates a lot of telemetry (and you are using hello ASP.NET SDK version 2.0.0-beta3 or later), hello adaptive sampling module automatically reduces hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="ec7f7-199">Тем не менее события, которые связанные toohello того же запроса или отмену выбора как группой, чтобы могли перемещаться между связанными событиями.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-199">However, events that are related toohello same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="ec7f7-200">[Дополнительная информация о выборке](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="ec7f7-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="ec7f7-201">Создание рабочего элемента</span><span class="sxs-lookup"><span data-stu-id="ec7f7-201">Create work item</span></span>
<span data-ttu-id="ec7f7-202">Можно создать ошибку в GitHub или Visual Studio Team Services с подробными сведениями hello из любого элемента телеметрии.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-202">You can create a bug in GitHub or Visual Studio Team Services with hello details from any telemetry item.</span></span> 

![Щелкните новый рабочий элемент, изменить поля hello и нажмите кнопку ОК.](./media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="ec7f7-204">Hello при первом запуске этого будет предложено tooconfigure tooyour ссылку Team Services учетной записи и проекта.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-204">hello first time you do this, you are asked tooconfigure a link tooyour Team Services account and project.</span></span>

![Введите URL-адрес hello сервера Team Services и имя проекта hello и нажмите авторизовать](./media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="ec7f7-206">(Можно также настроить ссылку hello в колонке hello рабочих элементов.)</span><span class="sxs-lookup"><span data-stu-id="ec7f7-206">(You can also configure hello link on hello Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="ec7f7-207">Сохранение результатов поиска</span><span class="sxs-lookup"><span data-stu-id="ec7f7-207">Save your search</span></span>
<span data-ttu-id="ec7f7-208">При установке все фильтры hello hello поиска можно сохранить в список избранного.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-208">When you've set all hello filters you want, you can save hello search as a favorite.</span></span> <span data-ttu-id="ec7f7-209">Если вы работаете в учетную запись организации, можно ли tooshare его с другими членами команды.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-209">If you work in an organizational account, you can choose whether tooshare it with other team members.</span></span>

![Щелкните Избранное hello имя набора и нажмите кнопку Сохранить](./media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="ec7f7-211">Поиск hello toosee еще раз, **колонке Обзор перейдите toohello** и открыть Избранное:</span><span class="sxs-lookup"><span data-stu-id="ec7f7-211">toosee hello search again, **go toohello overview blade** and open Favorites:</span></span>

![Плитка "Избранное"](./media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="ec7f7-213">Если вы сохранили относительный временной диапазон, повторно открыть колонку hello имеет hello последние данные.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-213">If you saved with Relative time range, hello re-opened blade has hello latest data.</span></span> <span data-ttu-id="ec7f7-214">Если вы сохранили с диапазоном абсолютное время, вы увидите hello и те же данные каждый раз.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-214">If you saved with Absolute time range, you see hello same data every time.</span></span> <span data-ttu-id="ec7f7-215">(Если «Relative» не поддерживается при необходимости toosave Избранное, выберите диапазон времени в заголовке hello и задать диапазон времени, не настраиваемого диапазона).</span><span class="sxs-lookup"><span data-stu-id="ec7f7-215">(If 'Relative' isn't available when you want toosave a favorite, click Time Range in hello header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-tooapplication-insights"></a><span data-ttu-id="ec7f7-216">Отправлять дополнительные данные телеметрии tooApplication аналитики</span><span class="sxs-lookup"><span data-stu-id="ec7f7-216">Send more telemetry tooApplication Insights</span></span>
<span data-ttu-id="ec7f7-217">В телеметрии toohello out of box сложения отправленных пакет SDK Application Insights вы можете:</span><span class="sxs-lookup"><span data-stu-id="ec7f7-217">In addition toohello out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="ec7f7-218">Выполнять трасcировку журналов, используя избранную платформу ведения журнала в [.NET](app-insights-asp-net-trace-logs.md) или [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ec7f7-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="ec7f7-219">Благодаря этому можно будет выполнить поиск в журнале трассировки и сопоставить результаты с просмотрами страниц, исключениями и другими событиями.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="ec7f7-220">[Написание кода](app-insights-api-custom-events-metrics.md) toosend пользовательских событий, представления страниц и исключения.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-220">[Write code](app-insights-api-custom-events-metrics.md) toosend custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="ec7f7-221">[Узнайте, каким образом ведет журнал toosend и пользовательского телеметрии tooApplication аналитики](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ec7f7-221">[Learn how toosend logs and custom telemetry tooApplication Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <span data-ttu-id="ec7f7-222"><a name="questions"></a>Вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="ec7f7-222"><a name="questions"></a>Q & A</span></span>
### <span data-ttu-id="ec7f7-223"><a name="limits"></a>Какой объем данных сохраняется?</span><span class="sxs-lookup"><span data-stu-id="ec7f7-223"><a name="limits"></a>How much data is retained?</span></span>

<span data-ttu-id="ec7f7-224">В разделе hello [Сводная таблица ограничений](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="ec7f7-224">See hello [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="ec7f7-225">Как просмотреть данные POST в запросах к серверу?</span><span class="sxs-lookup"><span data-stu-id="ec7f7-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="ec7f7-226">Мы не заносить в журнал данные POST hello автоматически, но можно использовать [TrackTrace или журнала вызовов](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ec7f7-226">We don't log hello POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="ec7f7-227">Поместите hello ОТПРАВЛЕННЫХ данных в параметре сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-227">Put hello POST data in hello message parameter.</span></span> <span data-ttu-id="ec7f7-228">Невозможно применить фильтр сообщений hello в hello таким же, каким образом можно применить фильтр свойств, но ограничение размера hello длиннее.</span><span class="sxs-lookup"><span data-stu-id="ec7f7-228">You can't filter on hello message in hello same way you can filter on properties, but hello size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="ec7f7-229">Видео</span><span class="sxs-lookup"><span data-stu-id="ec7f7-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <span data-ttu-id="ec7f7-230"><a name="add"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec7f7-230"><a name="add"></a>Next steps</span></span>
* [<span data-ttu-id="ec7f7-231">Создание сложных запросов в Analytics</span><span class="sxs-lookup"><span data-stu-id="ec7f7-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="ec7f7-232">Отправить журналы настроенной телеметрии и tooApplication аналитики</span><span class="sxs-lookup"><span data-stu-id="ec7f7-232">Send logs and custom telemetry tooApplication Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="ec7f7-233">Наблюдение за доступностью и скоростью реагирования веб-сайта</span><span class="sxs-lookup"><span data-stu-id="ec7f7-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="ec7f7-234">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="ec7f7-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
