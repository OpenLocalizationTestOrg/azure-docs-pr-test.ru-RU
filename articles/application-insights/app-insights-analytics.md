---
title: "aaaAnalytics - hello мощное средство аналитики приложений Azure | Документы Microsoft"
description: "Обзор аналитики hello мощное средство диагностики поиска средство аналитики приложений. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="f92df-103">Аналитика в Application Insights</span><span class="sxs-lookup"><span data-stu-id="f92df-103">Analytics in Application Insights</span></span>
<span data-ttu-id="f92df-104">[Аналитика](app-insights-analytics.md) — мощное средство поиска функция hello [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f92df-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="f92df-105">На этих страницах описан язык запросов Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f92df-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="f92df-106">**[Вводное видео hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="f92df-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="f92df-107">**[Испытайте аналитика на нашем смоделированные данные](https://analytics.applicationinsights.io/demo)**  Если ваше приложение еще не отправляет данные tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="f92df-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="f92df-108">**[SQL-пользователей Памятка](https://aka.ms/sql-analytics)**  преобразует наиболее общих идиом hello.</span><span class="sxs-lookup"><span data-stu-id="f92df-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>
* <span data-ttu-id="f92df-109">**[Справочник по языку](app-insights-analytics-reference.md)**  узнать, как все toouse hello мощные функции hello язык запросов для анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="f92df-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how toouse all hello powerful features of hello Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="f92df-110">Запросы в аналитике</span><span class="sxs-lookup"><span data-stu-id="f92df-110">Queries in Analytics</span></span>
<span data-ttu-id="f92df-111">Типичный запрос содержит *исходную* таблицу и ряд *операторов*, разделенных `|`.</span><span class="sxs-lookup"><span data-stu-id="f92df-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="f92df-112">Например давайте выясним какое время дня гражданами hello Hyderabad повторите наш веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f92df-112">For example, let's find out what time of day hello citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="f92df-113">А пока что мы посмотрим, какие коды результатов возвращаются tootheir HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="f92df-113">And while we're there, let's see what result codes are returned tootheir HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="f92df-114">Мы количество IP-адресов для различных клиентов, сгруппировать их по часам hello hello дня по hello за последние 7 дней.</span><span class="sxs-lookup"><span data-stu-id="f92df-114">We count distinct client IP addresses, grouping them by hello hour of hello day over hello past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="f92df-115">результаты tooget за пределами hello предыдущие 24 часа, либо явным образом включить «timestamp» в запросе либо используйте hello время диапазона раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="f92df-115">tooget results outside hello previous 24h, either include 'timestamp' explicitly in your query, or use hello time range drop-down menu.</span></span>
>

<span data-ttu-id="f92df-116">Позволяет отобразить результаты hello с hello линейчатой диаграммы презентации, выбрав toostack результаты hello коды ответа:</span><span class="sxs-lookup"><span data-stu-id="f92df-116">Let's display hello results with hello bar chart presentation, choosing toostack hello results from different response codes:</span></span>

![Выберите линейчатую диаграмму, оси x и y, а затем сегментацию.](./media/app-insights-analytics/020.png)

<span data-ttu-id="f92df-118">Похоже, в Хайдерабаде наше приложение наиболее популярно в обеденное время и время отхода ко сну.</span><span class="sxs-lookup"><span data-stu-id="f92df-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="f92df-119">(И нам следует изучить эти 500 кодов.)</span><span class="sxs-lookup"><span data-stu-id="f92df-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="f92df-120">Кроме того, существуют сложные статистические операции.</span><span class="sxs-lookup"><span data-stu-id="f92df-120">There are also powerful statistical operations:</span></span>

![Результаты статистического запроса](./media/app-insights-analytics/025.png)

<span data-ttu-id="f92df-122">язык Hello имеет множество функций привлекательным:</span><span class="sxs-lookup"><span data-stu-id="f92df-122">hello language has many attractive features:</span></span>


* <span data-ttu-id="f92df-123">[Фильтрация](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) необработанных данных телеметрии приложения по любым полям, включая пользовательские свойства и метрики.</span><span class="sxs-lookup"><span data-stu-id="f92df-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="f92df-124">[Соединение](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) нескольких таблиц — соотношение запросов с просмотрами страниц, вызовами зависимостей, исключениями и трассировками журнала.</span><span class="sxs-lookup"><span data-stu-id="f92df-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="f92df-125">Сложные статистические [агрегаты](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="f92df-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="f92df-126">Столь же мощных, как SQL, но гораздо проще для сложных запросов: вместо вложенных инструкций передать hello данные из одного toohello простые операции рядом.</span><span class="sxs-lookup"><span data-stu-id="f92df-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe hello data from one elementary operation toohello next.</span></span>
* <span data-ttu-id="f92df-127">Мгновенные яркие визуализации.</span><span class="sxs-lookup"><span data-stu-id="f92df-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="f92df-128">[ПИН-код диаграммы панели мониторинга tooAzure](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="f92df-128">[Pin charts tooAzure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="f92df-129">[Экспорт tooPower запросов BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="f92df-129">[Export queries tooPower BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="f92df-130">Отсутствует [API-интерфейса REST](https://dev.applicationinsights.io/) можно использовать запросы toorun программными средствами, например из Powershell.</span><span class="sxs-lookup"><span data-stu-id="f92df-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use toorun queries programmatically, for example from Powershell.</span></span>


## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="f92df-131">Подключение к данным tooyour Application Insights</span><span class="sxs-lookup"><span data-stu-id="f92df-131">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="f92df-132">Откройте аналитику в [колонке "Обзор"](app-insights-dashboards.md) приложения в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f92df-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![На сайте portal.azure.com откройте ресурс Application Insights и щелкните "Аналитика".](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="f92df-134">Видео</span><span class="sxs-lookup"><span data-stu-id="f92df-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="f92df-135">Примеры запросов</span><span class="sxs-lookup"><span data-stu-id="f92df-135">Query examples</span></span>

<span data-ttu-id="f92df-136">Повторите эти пошаговые руководства tooillustrate hello степень аналитика с помощью:</span><span class="sxs-lookup"><span data-stu-id="f92df-136">Try these walkthroughs tooillustrate hello power of using Analytics:</span></span>

 *  [<span data-ttu-id="f92df-137">Автоматическая диагностика пиков и пропуска шагов в контексте длительности запросов.</span><span class="sxs-lookup"><span data-stu-id="f92df-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="f92df-138">Анализ снижения производительности путем анализа временных рядов.</span><span class="sxs-lookup"><span data-stu-id="f92df-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="f92df-139">Анализ сбоев приложения с помощью функций autocluster и diffpatterns.</span><span class="sxs-lookup"><span data-stu-id="f92df-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="f92df-140">Расширенное определение формы путем анализа временных рядов.</span><span class="sxs-lookup"><span data-stu-id="f92df-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="f92df-141">С помощью скользящего окна операций tooanalyze приложения об использовании (скользящий MAU/DAU и т. д)</span><span class="sxs-lookup"><span data-stu-id="f92df-141">Using sliding window operations tooanalyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="f92df-142">[Обнаружение нарушений в работе службы на основе анализа журналов отладки](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) и соответствующая запись блога [здесь](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span><span class="sxs-lookup"><span data-stu-id="f92df-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="f92df-143">[Профилирование производительности приложений с помощью простых журналов отладки](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) и соответствующая запись блога [здесь](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/).</span><span class="sxs-lookup"><span data-stu-id="f92df-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="f92df-144">[Измерение длительности hello для каждого шага в потоке кода с помощью простого отладочный журналы](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) и соответствующие записи блога [здесь](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="f92df-144">[Measuring hello duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="f92df-145">[Анализ параллелизма с помощью простых журналов отладки](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) и соответствующая запись блога [здесь](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/).</span><span class="sxs-lookup"><span data-stu-id="f92df-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="f92df-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f92df-146">Next steps</span></span>
* <span data-ttu-id="f92df-147">Мы рекомендуем начать с hello [обзор языка](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="f92df-147">We recommend you start with hello [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="f92df-148">Дополнительные сведения об [использовании аналитики](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="f92df-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="f92df-149">[Справочник по языку](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f92df-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
