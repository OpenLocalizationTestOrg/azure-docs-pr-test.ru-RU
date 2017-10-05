---
title: "Отслеживание работоспособности и использования приложения с помощью Application Insights"
description: "Приступая к работе с Application Insights. Анализ использования, доступности и производительности локальных приложений или веб-приложений Microsoft Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 5b7b1f4a53cd2624ee8e2ab684ba6ba63252674f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="0955d-104">Отслеживание производительности в веб-приложениях</span><span class="sxs-lookup"><span data-stu-id="0955d-104">Monitor performance in web applications</span></span>


<span data-ttu-id="0955d-105">Она позволяет удостовериться, что приложение работает с хорошей производительностью, и быстро выяснить, были ли сбои.</span><span class="sxs-lookup"><span data-stu-id="0955d-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="0955d-106">[Application Insights][start] сообщает о любых проблемах с производительностью и исключениях, помогая выявлять и диагностировать их причины.</span><span class="sxs-lookup"><span data-stu-id="0955d-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose the root causes.</span></span>

<span data-ttu-id="0955d-107">Application Insights можно отслеживать веб-приложения и службы Java и ASP.NET, а также службы WCF.</span><span class="sxs-lookup"><span data-stu-id="0955d-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="0955d-108">Они могут размещаться локально, на виртуальных машинах, а также как веб-сайты Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0955d-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="0955d-109">На стороне клиента Application Insights может извлекать телеметрию с веб-страниц и разнообразных устройств, включая приложения для iOS, Android и Магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="0955d-109">On the client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="0955d-110">Мы добавили новые возможности для поиска медленно выполняющихся страниц в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="0955d-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="0955d-111">Если у вас нет доступа к ним, включите их, настроив параметры предварительной версии с помощью [колонки предварительной версии](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="0955d-111">If you don't have access to it, enable it by configuring your preview options with the [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="0955d-112">Об этих новых возможностях можно прочитать в разделе [Поиск и устранение узких мест производительности с помощью интерактивного исследования производительности](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="0955d-112">Read about this new experience in [Find and fix performance bottlenecks with the interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="0955d-113"><a name="setup"></a>Настройка мониторинга производительности</span><span class="sxs-lookup"><span data-stu-id="0955d-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="0955d-114">Если вы еще не добавили Application Insights в проект (т. е. если в нем нет файла ApplicationInsights.config), вы можете приступить к работе с этой службой одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="0955d-114">If you haven't yet added Application Insights to your project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways to get started:</span></span>

* [<span data-ttu-id="0955d-115">Веб-приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0955d-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="0955d-116">Добавление мониторинга исключений</span><span class="sxs-lookup"><span data-stu-id="0955d-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="0955d-117">Добавление мониторинга зависимостей</span><span class="sxs-lookup"><span data-stu-id="0955d-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="0955d-118">Веб-приложения J2EE</span><span class="sxs-lookup"><span data-stu-id="0955d-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="0955d-119">Добавление мониторинга зависимостей</span><span class="sxs-lookup"><span data-stu-id="0955d-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="0955d-120"><a name="view"></a>Просмотр метрик производительности</span><span class="sxs-lookup"><span data-stu-id="0955d-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="0955d-121">На [портале Azure](https://portal.azure.com)перейдите к ресурсу Application Insights, настроенному для приложения.</span><span class="sxs-lookup"><span data-stu-id="0955d-121">In [the Azure portal](https://portal.azure.com), browse to the Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="0955d-122">В колонке "Обзор" отображаются основные данные производительности:</span><span class="sxs-lookup"><span data-stu-id="0955d-122">The overview blade shows basic performance data:</span></span>

<span data-ttu-id="0955d-123">Щелкните любую диаграмму, чтобы увидеть результаты более подробно и за больший период.</span><span class="sxs-lookup"><span data-stu-id="0955d-123">Click any chart to see more detail, and to see results for a longer period.</span></span> <span data-ttu-id="0955d-124">Например, щелкните плитку "Запросы" и выберите временной диапазон.</span><span class="sxs-lookup"><span data-stu-id="0955d-124">For example, click the Requests tile and then select a time range:</span></span>

![Щелкните плитки, чтобы увидеть подробные данные, и выберите временной диапазон](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="0955d-126">Щелкните диаграмму, чтобы выбрать, какие метрики отображать, а также добавить новую диаграмму и выбрать метрики для нее.</span><span class="sxs-lookup"><span data-stu-id="0955d-126">Click a chart to choose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Щелкните график, чтобы выбрать метрики](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="0955d-128">**Отмените выбор всех метрик** , чтобы увидеть полный набор доступных метрик.</span><span class="sxs-lookup"><span data-stu-id="0955d-128">**Uncheck all the metrics** to see the full selection that is available.</span></span> <span data-ttu-id="0955d-129">Метрики разделены на группы: если выбран один из элементов группы, отображаются только метрики этой группы.</span><span class="sxs-lookup"><span data-stu-id="0955d-129">The metrics fall into groups; when any member of a group is selected, only the other members of that group appear.</span></span>

## <span data-ttu-id="0955d-130"><a name="metrics"></a>Что все это означает?</span><span class="sxs-lookup"><span data-stu-id="0955d-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="0955d-131">Плитки и отчеты о производительности</span><span class="sxs-lookup"><span data-stu-id="0955d-131">Performance tiles and reports</span></span>
<span data-ttu-id="0955d-132">Имеются различные метрики производительности, которые можно получить.</span><span class="sxs-lookup"><span data-stu-id="0955d-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="0955d-133">Начнем с тех, которые отображаются в колонке приложения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0955d-133">Let's start with those that appear by default on the application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="0955d-134">Requests (Запросы)</span><span class="sxs-lookup"><span data-stu-id="0955d-134">Requests</span></span>
<span data-ttu-id="0955d-135">Это число HTTP-запросов, полученных за указанный период.</span><span class="sxs-lookup"><span data-stu-id="0955d-135">The number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="0955d-136">Сравните это значение с результатами в других отчетах, чтобы узнать, как ведет себя приложение при изменении нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0955d-136">Compare this with the results on other reports to see how your app behaves as the load varies.</span></span>

<span data-ttu-id="0955d-137">HTTP-запросы включают в себя все запросы GET и POST для страниц, данных и изображений.</span><span class="sxs-lookup"><span data-stu-id="0955d-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="0955d-138">Чтобы просмотреть счетчики для конкретных URL-адресов, щелкните плитку.</span><span class="sxs-lookup"><span data-stu-id="0955d-138">Click on the tile to get counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="0955d-139">Average response time (Среднее время ответа)</span><span class="sxs-lookup"><span data-stu-id="0955d-139">Average response time</span></span>
<span data-ttu-id="0955d-140">Это время от поступления веб-запроса в приложение до возвращения ответа.</span><span class="sxs-lookup"><span data-stu-id="0955d-140">Measures the time between a web request entering your application and the response being returned.</span></span>

<span data-ttu-id="0955d-141">Точки показывают скользящее среднее.</span><span class="sxs-lookup"><span data-stu-id="0955d-141">The points show a moving average.</span></span> <span data-ttu-id="0955d-142">Если запросов много, для некоторых из них значения могут отклоняться от среднего, но при этом на графике не будет явных пиков или провалов.</span><span class="sxs-lookup"><span data-stu-id="0955d-142">If there are a lot of requests, there might be some that deviate from the average without an obvious peak or dip in the graph.</span></span>

<span data-ttu-id="0955d-143">Обращайте внимание на необычные пики.</span><span class="sxs-lookup"><span data-stu-id="0955d-143">Look for unusual peaks.</span></span> <span data-ttu-id="0955d-144">Как правило, время ответа растет с увеличением числа запросов.</span><span class="sxs-lookup"><span data-stu-id="0955d-144">In general, expect response time to rise with a rise in requests.</span></span> <span data-ttu-id="0955d-145">Если этот рост непропорционален, возможно, приложение исчерпало какой-либо ресурс, например ЦП или емкость используемой службы.</span><span class="sxs-lookup"><span data-stu-id="0955d-145">If the rise is disproportionate, your app might be hitting a resource limit such as CPU or the capacity of a service it uses.</span></span>

<span data-ttu-id="0955d-146">Чтобы просмотреть значения для конкретных URL-адресов, щелкните плитку.</span><span class="sxs-lookup"><span data-stu-id="0955d-146">Click the tile to get times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="0955d-147">Slowest requests (Самые медленные запросы)</span><span class="sxs-lookup"><span data-stu-id="0955d-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="0955d-148">Показывает, какие запросы могут потребовать оптимизации производительности.</span><span class="sxs-lookup"><span data-stu-id="0955d-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="0955d-149">Failed requests (Неудачные запросы)</span><span class="sxs-lookup"><span data-stu-id="0955d-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="0955d-150">Это счетчик запросов, которые вызвали не перехваченные исключения.</span><span class="sxs-lookup"><span data-stu-id="0955d-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="0955d-151">Чтобы просмотреть подробные сведения о конкретных сбоях, щелкните плитку. Чтобы просмотреть подробные сведения об отдельном запросе, выберите его.</span><span class="sxs-lookup"><span data-stu-id="0955d-151">Click the tile to see the details of specific failures, and select an individual request to see its detail.</span></span> 

<span data-ttu-id="0955d-152">Для детального изучения доступна только репрезентативная выборка сбоев.</span><span class="sxs-lookup"><span data-stu-id="0955d-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="0955d-153">Другие метрики</span><span class="sxs-lookup"><span data-stu-id="0955d-153">Other metrics</span></span>
<span data-ttu-id="0955d-154">Чтобы увидеть, какие еще метрики доступны, щелкните график и снимите все флажки метрик.</span><span class="sxs-lookup"><span data-stu-id="0955d-154">To see what other metrics you can display, click a graph, and then deselect all the metrics to see the full available set.</span></span> <span data-ttu-id="0955d-155">Чтобы просмотреть определение конкретной метрики, щелкните значок (i).</span><span class="sxs-lookup"><span data-stu-id="0955d-155">Click (i) to see each metric's definition.</span></span>

![Снимите все флажки, чтобы увидеть полный набор метрик](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="0955d-157">Выбор любой метрики отключит остальные, и они не будут отображаться на этой диаграмме.</span><span class="sxs-lookup"><span data-stu-id="0955d-157">Selecting any metric disables the others that can't appear on the same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="0955d-158">Задайте предупреждения</span><span class="sxs-lookup"><span data-stu-id="0955d-158">Set alerts</span></span>
<span data-ttu-id="0955d-159">Чтобы получать уведомления по электронной почте о нетипичных значениях любой метрики, добавьте предупреждение.</span><span class="sxs-lookup"><span data-stu-id="0955d-159">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="0955d-160">Можно выбрать отправку либо по электронной почте администраторам учетной записи, либо на указанный электронный адрес.</span><span class="sxs-lookup"><span data-stu-id="0955d-160">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="0955d-161">Выбирайте ресурс прежде других свойств.</span><span class="sxs-lookup"><span data-stu-id="0955d-161">Set the resource before the other properties.</span></span> <span data-ttu-id="0955d-162">Не выбирайте ресурсы webtest, если нужно задать предупреждения метрик производительности или использования.</span><span class="sxs-lookup"><span data-stu-id="0955d-162">Don't choose the webtest resources if you want to set alerts on performance or usage metrics.</span></span>

<span data-ttu-id="0955d-163">Аккуратно указывайте единицы измерения для пороговых значений.</span><span class="sxs-lookup"><span data-stu-id="0955d-163">Be careful to note the units in which you're asked to enter the threshold value.</span></span>

<span data-ttu-id="0955d-164">*Отсутствует кнопка «Добавить оповещение».*</span><span class="sxs-lookup"><span data-stu-id="0955d-164">*I don't see the Add Alert button.*</span></span> <span data-ttu-id="0955d-165">Вы используете учетную запись группы с доступом только для чтения?</span><span class="sxs-lookup"><span data-stu-id="0955d-165">- Is this a group account to which you have read-only access?</span></span> <span data-ttu-id="0955d-166">Обратитесь к администратору учетной записи.</span><span class="sxs-lookup"><span data-stu-id="0955d-166">Check with the account administrator.</span></span>

## <span data-ttu-id="0955d-167"><a name="diagnosis"></a>Диагностические проблемы</span><span class="sxs-lookup"><span data-stu-id="0955d-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="0955d-168">Вот некоторые советы по выявлению и диагностике проблем с производительностью:</span><span class="sxs-lookup"><span data-stu-id="0955d-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="0955d-169">настройте [веб-тесты][availability], чтобы получать оповещения, когда веб-сайт выходит из строя либо отвечает неправильно или медленно;</span><span class="sxs-lookup"><span data-stu-id="0955d-169">Set up [web tests][availability] to be alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="0955d-170">сравните число запросов с другими метриками, чтобы узнать, не связаны ли сбои или медленный ответ с нагрузкой;</span><span class="sxs-lookup"><span data-stu-id="0955d-170">Compare the Request count with other metrics to see if failures or slow response are related to load.</span></span>
* <span data-ttu-id="0955d-171">[вставьте в код инструкции трассировки и выполняйте поиск по ним][diagnostic], чтобы упростить выявление проблем.</span><span class="sxs-lookup"><span data-stu-id="0955d-171">[Insert and search trace statements][diagnostic] in your code to help pinpoint problems.</span></span>
* <span data-ttu-id="0955d-172">Отслеживайте работу веб-приложения с помощью [Live Metrics Stream][livestream].</span><span class="sxs-lookup"><span data-stu-id="0955d-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="0955d-173">Запишите состояние приложения .NET с помощью [отладчика моментальных снимков][snapshot].</span><span class="sxs-lookup"><span data-stu-id="0955d-173">Capture the state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="0955d-174">Поиск и устранение узких мест производительности с помощью интерактивного исследования производительности</span><span class="sxs-lookup"><span data-stu-id="0955d-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="0955d-175">Вы можете использовать новую функцию интерактивного исследования производительности Application Insights для обнаружения областей веб-приложения, которые снижают общую производительность.</span><span class="sxs-lookup"><span data-stu-id="0955d-175">You can use the new Application Insights interactive performance investigation to locate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="0955d-176">Вы можете быстро найти определенные страницы, снижающие производительность, и использовать [средство профилирования](app-insights-profiler.md), чтобы проверить наличие корреляции между ними.</span><span class="sxs-lookup"><span data-stu-id="0955d-176">You can quickly find specific pages that are slowing down, and use the [Profiling tool](app-insights-profiler.md) to see if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="0955d-177">Создание списка медленно выполняющихся страниц</span><span class="sxs-lookup"><span data-stu-id="0955d-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="0955d-178">Чтобы найти проблемы с производительностью, прежде всего необходимо получить список медленно выполняющихся страниц.</span><span class="sxs-lookup"><span data-stu-id="0955d-178">The first step for finding performance issues is to get a list of the slow responding pages.</span></span> <span data-ttu-id="0955d-179">Приведенный ниже снимок экрана демонстрирует использование колонки "Производительность" для получения списка потенциальных страниц для дальнейшего анализа.</span><span class="sxs-lookup"><span data-stu-id="0955d-179">The screen shot below demonstrates using the Performance blade to get a list of potential pages to investigate further.</span></span> <span data-ttu-id="0955d-180">На этой странице вы можете легко увидеть, что задержка времени отклика приложения произошла приблизительно в 18:00, а затем еще раз — приблизительно в 22:00.</span><span class="sxs-lookup"><span data-stu-id="0955d-180">You can quickly see from this page that there was a slow-down in the response time of the app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="0955d-181">Также вы увидите, что во время операции получения сведений о клиенте выполнялись долго выполняющиеся операции со средним временем отклика 507,05 мс.</span><span class="sxs-lookup"><span data-stu-id="0955d-181">You can also see that the GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Интерактивная производительность Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="0955d-183">Просмотр определенных страниц</span><span class="sxs-lookup"><span data-stu-id="0955d-183">Drill down on specific pages</span></span>

<span data-ttu-id="0955d-184">Получив моментальный снимок производительности приложения, можно получить дополнительные сведения о медленно выполняющихся операциях.</span><span class="sxs-lookup"><span data-stu-id="0955d-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="0955d-185">Щелкните любую операцию в списке, чтобы увидеть подробные сведения, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="0955d-185">Click on any operation in the list to see the details as shown below.</span></span> <span data-ttu-id="0955d-186">На диаграмме можно увидеть, была ли производительность основана на зависимости.</span><span class="sxs-lookup"><span data-stu-id="0955d-186">From the chart you can see if the performance was based on a dependency.</span></span> <span data-ttu-id="0955d-187">Также можно увидеть, у скольких пользователей было различное время отклика.</span><span class="sxs-lookup"><span data-stu-id="0955d-187">You can also see how many users experienced the various response times.</span></span> 

![Колонка "Операции" в Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="0955d-189">Просмотр данных для определенного периода времени</span><span class="sxs-lookup"><span data-stu-id="0955d-189">Drill down on a specific time period</span></span>

<span data-ttu-id="0955d-190">Определив точки во времени для исследования, углубитесь еще больше, чтобы рассмотреть определенные операции, которые могли вызвать снижение производительности.</span><span class="sxs-lookup"><span data-stu-id="0955d-190">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="0955d-191">Щелкнув определенную точку во времени, вы получите подробности о странице, как это показано ниже.</span><span class="sxs-lookup"><span data-stu-id="0955d-191">When you click on a specific point in time you get the details of the page as shown below.</span></span> <span data-ttu-id="0955d-192">В примере ниже можно увидеть операции для данного периода времени, а также коды ответа сервера и длительность операции.</span><span class="sxs-lookup"><span data-stu-id="0955d-192">In the example below you can see the operations listed for a given time period along with the server response codes and the operation duration.</span></span> <span data-ttu-id="0955d-193">Также имеется URL-адрес для открытия рабочего элемента TFS, если необходимо отправить эти сведения команде разработчиков.</span><span class="sxs-lookup"><span data-stu-id="0955d-193">You also have the url for opening a TFS work item if you need to send this information to your development team.</span></span>

![Временной срез Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="0955d-195">Просмотр подробных сведений об определенной операции</span><span class="sxs-lookup"><span data-stu-id="0955d-195">Drill down on a specific operation</span></span>

<span data-ttu-id="0955d-196">Определив точки во времени для исследования, углубитесь еще больше, чтобы рассмотреть определенные операции, которые могли вызвать снижение производительности.</span><span class="sxs-lookup"><span data-stu-id="0955d-196">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="0955d-197">Щелкните операцию в списке, чтобы просмотреть подробности о ней, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="0955d-197">Click on an operation from the list to see the details of the operation as shown below.</span></span> <span data-ttu-id="0955d-198">В этом примере видно, что произошел сбой операции и Application Insights предоставила сведения об исключении, которое выдало приложение.</span><span class="sxs-lookup"><span data-stu-id="0955d-198">In this example you can see that the operation failed, and Application Insights has provided the details of the exception the application threw.</span></span> <span data-ttu-id="0955d-199">Опять же, вы можете легко создать рабочий элемент TFS из этой колонки.</span><span class="sxs-lookup"><span data-stu-id="0955d-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Колонка "Операции" в Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="0955d-201"><a name="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0955d-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="0955d-202">[Веб-тесты][availability] — настройте отправку веб-запросов к приложению через равные интервалы из разных точек мира.</span><span class="sxs-lookup"><span data-stu-id="0955d-202">[Web tests][availability] - Have web requests sent to your application at regular intervals from around the world.</span></span>

<span data-ttu-id="0955d-203">[Сбор данных трассировки диагностики и поиск по ним][diagnostic] — добавьте вызовы трассировки и анализируйте результаты для выявления проблем.</span><span class="sxs-lookup"><span data-stu-id="0955d-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through the results to pinpoint issues.</span></span>

<span data-ttu-id="0955d-204">[Отслеживание использования][usage] — получайте информацию о том, как люди используют ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="0955d-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="0955d-205">[Устранение неполадок][qna] — вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="0955d-205">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



