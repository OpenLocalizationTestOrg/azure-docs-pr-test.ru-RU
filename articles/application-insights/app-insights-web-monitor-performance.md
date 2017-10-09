---
title: "aaaMonitor состояния приложения и использования с помощью Application Insights"
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
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="47b58-104">Отслеживание производительности в веб-приложениях</span><span class="sxs-lookup"><span data-stu-id="47b58-104">Monitor performance in web applications</span></span>


<span data-ttu-id="47b58-105">Она позволяет удостовериться, что приложение работает с хорошей производительностью, и быстро выяснить, были ли сбои.</span><span class="sxs-lookup"><span data-stu-id="47b58-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="47b58-106">[Application Insights] [ start] сообщения о всех проблем производительности и исключений, а справки вы найдете и диагностировать hello основные причины.</span><span class="sxs-lookup"><span data-stu-id="47b58-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose hello root causes.</span></span>

<span data-ttu-id="47b58-107">Application Insights можно отслеживать веб-приложения и службы Java и ASP.NET, а также службы WCF.</span><span class="sxs-lookup"><span data-stu-id="47b58-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="47b58-108">Они могут размещаться локально, на виртуальных машинах, а также как веб-сайты Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="47b58-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="47b58-109">На стороне клиента hello Application Insights может занять телеметрии из веб-страниц и других устройств, включая iOS, Android и магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="47b58-109">On hello client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="47b58-110">Мы добавили новые возможности для поиска медленно выполняющихся страниц в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="47b58-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="47b58-111">Если у вас нет доступа к tooit, ее включить, настройку параметров предварительного просмотра с hello [предварительной версии](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="47b58-111">If you don't have access tooit, enable it by configuring your preview options with hello [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="47b58-112">Узнайте, как эти новые возможности в [поиска и устранения проблем производительности с hello интерактивного исследования производительности](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="47b58-112">Read about this new experience in [Find and fix performance bottlenecks with hello interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="47b58-113"><a name="setup"></a>Настройка мониторинга производительности</span><span class="sxs-lookup"><span data-stu-id="47b58-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="47b58-114">Если вы еще не добавили Application Insights tooyour проекта (то есть, если он не имеет ApplicationInsights.config), выберите один из следующих способов работы tooget:</span><span class="sxs-lookup"><span data-stu-id="47b58-114">If you haven't yet added Application Insights tooyour project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways tooget started:</span></span>

* [<span data-ttu-id="47b58-115">Веб-приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="47b58-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="47b58-116">Добавление мониторинга исключений</span><span class="sxs-lookup"><span data-stu-id="47b58-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="47b58-117">Добавление мониторинга зависимостей</span><span class="sxs-lookup"><span data-stu-id="47b58-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="47b58-118">Веб-приложения J2EE</span><span class="sxs-lookup"><span data-stu-id="47b58-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="47b58-119">Добавление мониторинга зависимостей</span><span class="sxs-lookup"><span data-stu-id="47b58-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="47b58-120"><a name="view"></a>Просмотр метрик производительности</span><span class="sxs-lookup"><span data-stu-id="47b58-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="47b58-121">В [hello портал Azure](https://portal.azure.com), найдите ресурс Application Insights toohello, который настроен для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="47b58-121">In [hello Azure portal](https://portal.azure.com), browse toohello Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="47b58-122">Обзор колонке Hello отображаются основные данные:</span><span class="sxs-lookup"><span data-stu-id="47b58-122">hello overview blade shows basic performance data:</span></span>

<span data-ttu-id="47b58-123">Щелкните любой toosee диаграммы более подробные сведения и toosee результаты на более длительный период.</span><span class="sxs-lookup"><span data-stu-id="47b58-123">Click any chart toosee more detail, and toosee results for a longer period.</span></span> <span data-ttu-id="47b58-124">Например, щелкните плитку hello запросов, а затем выберите диапазон времени:</span><span class="sxs-lookup"><span data-stu-id="47b58-124">For example, click hello Requests tile and then select a time range:</span></span>

![Перемещаться по данным toomore и выберите диапазон времени](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="47b58-126">Щелкните toochoose диаграммы какие метрики, он отображается, или добавить новую диаграмму и выберите его метрики:</span><span class="sxs-lookup"><span data-stu-id="47b58-126">Click a chart toochoose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Выберите метрики toochoose графа](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="47b58-128">**Снимите все показатели hello** полное выделение hello toosee, которая доступна.</span><span class="sxs-lookup"><span data-stu-id="47b58-128">**Uncheck all hello metrics** toosee hello full selection that is available.</span></span> <span data-ttu-id="47b58-129">метрики Hello делятся на группы; При выборе любого члена группы только hello других членов этой группы отображаются.</span><span class="sxs-lookup"><span data-stu-id="47b58-129">hello metrics fall into groups; when any member of a group is selected, only hello other members of that group appear.</span></span>

## <span data-ttu-id="47b58-130"><a name="metrics"></a>Что все это означает?</span><span class="sxs-lookup"><span data-stu-id="47b58-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="47b58-131">Плитки и отчеты о производительности</span><span class="sxs-lookup"><span data-stu-id="47b58-131">Performance tiles and reports</span></span>
<span data-ttu-id="47b58-132">Имеются различные метрики производительности, которые можно получить.</span><span class="sxs-lookup"><span data-stu-id="47b58-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="47b58-133">Давайте начнем с тех, которые отображаются по умолчанию в колонке приложения hello.</span><span class="sxs-lookup"><span data-stu-id="47b58-133">Let's start with those that appear by default on hello application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="47b58-134">Запросы</span><span class="sxs-lookup"><span data-stu-id="47b58-134">Requests</span></span>
<span data-ttu-id="47b58-135">Hello количество HTTP-запросов, полученных в течение указанного периода.</span><span class="sxs-lookup"><span data-stu-id="47b58-135">hello number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="47b58-136">Сравните это с результатами hello на другие отчеты toosee, как приложение ведет себя как загрузка hello меняется.</span><span class="sxs-lookup"><span data-stu-id="47b58-136">Compare this with hello results on other reports toosee how your app behaves as hello load varies.</span></span>

<span data-ttu-id="47b58-137">HTTP-запросы включают в себя все запросы GET и POST для страниц, данных и изображений.</span><span class="sxs-lookup"><span data-stu-id="47b58-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="47b58-138">Щелкните на подсчете tooget плитки приветствия для конкретного URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="47b58-138">Click on hello tile tooget counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="47b58-139">Среднее время ответа</span><span class="sxs-lookup"><span data-stu-id="47b58-139">Average response time</span></span>
<span data-ttu-id="47b58-140">Меры hello время между ввода, возвращаемых приложения и hello ответа веб-запроса.</span><span class="sxs-lookup"><span data-stu-id="47b58-140">Measures hello time between a web request entering your application and hello response being returned.</span></span>

<span data-ttu-id="47b58-141">Hello точек Показать скользящее среднее.</span><span class="sxs-lookup"><span data-stu-id="47b58-141">hello points show a moving average.</span></span> <span data-ttu-id="47b58-142">Если имеется много запросов, может возникнуть некоторые, может отличаться от среднего hello без очевидным пиковых нагрузок или оказываются в hello graph.</span><span class="sxs-lookup"><span data-stu-id="47b58-142">If there are a lot of requests, there might be some that deviate from hello average without an obvious peak or dip in hello graph.</span></span>

<span data-ttu-id="47b58-143">Обращайте внимание на необычные пики.</span><span class="sxs-lookup"><span data-stu-id="47b58-143">Look for unusual peaks.</span></span> <span data-ttu-id="47b58-144">Средняя toorise времени ответа с уделять запросов.</span><span class="sxs-lookup"><span data-stu-id="47b58-144">In general, expect response time toorise with a rise in requests.</span></span> <span data-ttu-id="47b58-145">В случае неограниченного уделять hello приложения может попадание ограничение ресурсов, таких как мощность Процессора и hello службы, используемые в нем.</span><span class="sxs-lookup"><span data-stu-id="47b58-145">If hello rise is disproportionate, your app might be hitting a resource limit such as CPU or hello capacity of a service it uses.</span></span>

<span data-ttu-id="47b58-146">Щелкните раз tooget hello плитки для конкретного URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="47b58-146">Click hello tile tooget times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="47b58-147">Slowest requests (Самые медленные запросы)</span><span class="sxs-lookup"><span data-stu-id="47b58-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="47b58-148">Показывает, какие запросы могут потребовать оптимизации производительности.</span><span class="sxs-lookup"><span data-stu-id="47b58-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="47b58-149">Failed requests (Неудачные запросы)</span><span class="sxs-lookup"><span data-stu-id="47b58-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="47b58-150">Это счетчик запросов, которые вызвали не перехваченные исключения.</span><span class="sxs-lookup"><span data-stu-id="47b58-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="47b58-151">Щелкните hello плитки toosee hello подробные сведения о конкретных ошибок и выберите его подробности toosee отдельный запрос.</span><span class="sxs-lookup"><span data-stu-id="47b58-151">Click hello tile toosee hello details of specific failures, and select an individual request toosee its detail.</span></span> 

<span data-ttu-id="47b58-152">Для детального изучения доступна только репрезентативная выборка сбоев.</span><span class="sxs-lookup"><span data-stu-id="47b58-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="47b58-153">Другие метрики</span><span class="sxs-lookup"><span data-stu-id="47b58-153">Other metrics</span></span>
<span data-ttu-id="47b58-154">toosee других метриках отображения, щелкните график и затем отмените выбор всех hello метрики toosee hello все доступные набора.</span><span class="sxs-lookup"><span data-stu-id="47b58-154">toosee what other metrics you can display, click a graph, and then deselect all hello metrics toosee hello full available set.</span></span> <span data-ttu-id="47b58-155">Нажмите кнопку (i) toosee определения каждой метрики.</span><span class="sxs-lookup"><span data-stu-id="47b58-155">Click (i) toosee each metric's definition.</span></span>

![Отмените выбор всех показателей toosee hello всего набора](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="47b58-157">Здравствуйте, при выборе любой hello метрики отключает другим пользователям, которые не могут присутствовать на одной диаграмме.</span><span class="sxs-lookup"><span data-stu-id="47b58-157">Selecting any metric disables hello others that can't appear on hello same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="47b58-158">Задание предупреждений</span><span class="sxs-lookup"><span data-stu-id="47b58-158">Set alerts</span></span>
<span data-ttu-id="47b58-159">уведомления по электронной почте о необычных значениях метрик, toobe добавить оповещение.</span><span class="sxs-lookup"><span data-stu-id="47b58-159">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="47b58-160">Вы можете Администраторы учетных записей электронной почты toohello для toosend hello или toospecific адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="47b58-160">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="47b58-161">Задайте другие свойства ресурса hello перед hello.</span><span class="sxs-lookup"><span data-stu-id="47b58-161">Set hello resource before hello other properties.</span></span> <span data-ttu-id="47b58-162">Не следует выбирать ресурсы webtest hello Если tooset оповещения на производительность или метрики использования.</span><span class="sxs-lookup"><span data-stu-id="47b58-162">Don't choose hello webtest resources if you want tooset alerts on performance or usage metrics.</span></span>

<span data-ttu-id="47b58-163">Быть тщательно toonote hello единиц, в которых в ответ на вопрос tooenter hello пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="47b58-163">Be careful toonote hello units in which you're asked tooenter hello threshold value.</span></span>

<span data-ttu-id="47b58-164">*Я не вижу hello кнопки "добавить оповещение".*</span><span class="sxs-lookup"><span data-stu-id="47b58-164">*I don't see hello Add Alert button.*</span></span> <span data-ttu-id="47b58-165">-Это toowhich учетной записи группы, у вас есть доступ только для чтения?</span><span class="sxs-lookup"><span data-stu-id="47b58-165">- Is this a group account toowhich you have read-only access?</span></span> <span data-ttu-id="47b58-166">Обратитесь к администратору учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="47b58-166">Check with hello account administrator.</span></span>

## <span data-ttu-id="47b58-167"><a name="diagnosis"></a>Диагностические проблемы</span><span class="sxs-lookup"><span data-stu-id="47b58-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="47b58-168">Вот некоторые советы по выявлению и диагностике проблем с производительностью:</span><span class="sxs-lookup"><span data-stu-id="47b58-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="47b58-169">Настройка [веб-тестов] [ availability] toobe оповещение, если веб-узел выходит из строя или отвечает неправильно или медленно.</span><span class="sxs-lookup"><span data-stu-id="47b58-169">Set up [web tests][availability] toobe alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="47b58-170">Сравнение hello количество запросов с toosee других метрик на предмет ошибок или медленный ответ связанные tooload.</span><span class="sxs-lookup"><span data-stu-id="47b58-170">Compare hello Request count with other metrics toosee if failures or slow response are related tooload.</span></span>
* <span data-ttu-id="47b58-171">[Вставка и поиск операторов трассировки] [ diagnostic] в ваш код toohelp выявить проблемы.</span><span class="sxs-lookup"><span data-stu-id="47b58-171">[Insert and search trace statements][diagnostic] in your code toohelp pinpoint problems.</span></span>
* <span data-ttu-id="47b58-172">Отслеживайте работу веб-приложения с помощью [Live Metrics Stream][livestream].</span><span class="sxs-lookup"><span data-stu-id="47b58-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="47b58-173">Записать состояние hello приложения .net с [отладчик моментального снимка][snapshot].</span><span class="sxs-lookup"><span data-stu-id="47b58-173">Capture hello state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="47b58-174">Поиск и устранение узких мест производительности с помощью интерактивного исследования производительности</span><span class="sxs-lookup"><span data-stu-id="47b58-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="47b58-175">Можно использовать hello новый Application Insights производительности интерактивного исследования toolocate областей веб-приложения с замедление работы общую производительность.</span><span class="sxs-lookup"><span data-stu-id="47b58-175">You can use hello new Application Insights interactive performance investigation toolocate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="47b58-176">Можно быстро найти конкретные страницы замедляют работу и использовать hello [средство профилирования](app-insights-profiler.md) toosee при наличии корреляцию между ними.</span><span class="sxs-lookup"><span data-stu-id="47b58-176">You can quickly find specific pages that are slowing down, and use hello [Profiling tool](app-insights-profiler.md) toosee if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="47b58-177">Создание списка медленно выполняющихся страниц</span><span class="sxs-lookup"><span data-stu-id="47b58-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="47b58-178">Первый шаг Hello для поиска проблем с производительностью — tooget список hello медленно отвечать на запросы страниц.</span><span class="sxs-lookup"><span data-stu-id="47b58-178">hello first step for finding performance issues is tooget a list of hello slow responding pages.</span></span> <span data-ttu-id="47b58-179">Привет, показанную ниже демонстрируется использование hello производительности колонке tooget список потенциальных tooinvestigate страниц дальнейшей.</span><span class="sxs-lookup"><span data-stu-id="47b58-179">hello screen shot below demonstrates using hello Performance blade tooget a list of potential pages tooinvestigate further.</span></span> <span data-ttu-id="47b58-180">Быстро видно на этой странице, было slow-down hello время ответа приложения hello в приблизительно 6:00, а затем в приблизительно 22: 00.</span><span class="sxs-lookup"><span data-stu-id="47b58-180">You can quickly see from this page that there was a slow-down in hello response time of hello app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="47b58-181">Также вы увидите, что операции сведения о клиенте GET hello имеет некоторые длительные операции с Медиана: время отклика 507.05 время в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="47b58-181">You can also see that hello GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Интерактивная производительность Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="47b58-183">Просмотр определенных страниц</span><span class="sxs-lookup"><span data-stu-id="47b58-183">Drill down on specific pages</span></span>

<span data-ttu-id="47b58-184">Получив моментальный снимок производительности приложения, можно получить дополнительные сведения о медленно выполняющихся операциях.</span><span class="sxs-lookup"><span data-stu-id="47b58-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="47b58-185">Щелкните любой операции в toosee hello список hello сведения, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="47b58-185">Click on any operation in hello list toosee hello details as shown below.</span></span> <span data-ttu-id="47b58-186">Hello диаграммы можно увидеть, если производительность hello был основан на зависимость.</span><span class="sxs-lookup"><span data-stu-id="47b58-186">From hello chart you can see if hello performance was based on a dependency.</span></span> <span data-ttu-id="47b58-187">Также видно сколько hello опытным пользователям различные времени ответа.</span><span class="sxs-lookup"><span data-stu-id="47b58-187">You can also see how many users experienced hello various response times.</span></span> 

![Колонка "Операции" в Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="47b58-189">Просмотр данных для определенного периода времени</span><span class="sxs-lookup"><span data-stu-id="47b58-189">Drill down on a specific time period</span></span>

<span data-ttu-id="47b58-190">После идентификации определенного момента времени tooinvestigate детализации и даже дальнейших toolook на hello определенных операций, которые могли привести slow-down производительности hello.</span><span class="sxs-lookup"><span data-stu-id="47b58-190">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="47b58-191">При нажатии кнопки на определенный момент времени можно получить сведения о hello страницы приветствия, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="47b58-191">When you click on a specific point in time you get hello details of hello page as shown below.</span></span> <span data-ttu-id="47b58-192">В hello пример ниже, вы увидите hello операции, перечисленные для определенного периода времени вместе с кодами ответа сервера hello и продолжительность операции hello.</span><span class="sxs-lookup"><span data-stu-id="47b58-192">In hello example below you can see hello operations listed for a given time period along with hello server response codes and hello operation duration.</span></span> <span data-ttu-id="47b58-193">Также имеется hello URL-адрес для открытия рабочего элемента TFS, если вам требуется toosend этой команды разработки сведения tooyour.</span><span class="sxs-lookup"><span data-stu-id="47b58-193">You also have hello url for opening a TFS work item if you need toosend this information tooyour development team.</span></span>

![Временной срез Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="47b58-195">Просмотр подробных сведений об определенной операции</span><span class="sxs-lookup"><span data-stu-id="47b58-195">Drill down on a specific operation</span></span>

<span data-ttu-id="47b58-196">После идентификации определенного момента времени tooinvestigate детализации и даже дальнейших toolook на hello определенных операций, которые могли привести slow-down производительности hello.</span><span class="sxs-lookup"><span data-stu-id="47b58-196">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="47b58-197">Щелкните операцию на основе сведений hello toosee списка hello hello операции, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="47b58-197">Click on an operation from hello list toosee hello details of hello operation as shown below.</span></span> <span data-ttu-id="47b58-198">В этом примере видно, что не удалось выполнить операцию hello и Application Insights предоставленные hello подробные сведения о hello приложение hello исключение вызвало.</span><span class="sxs-lookup"><span data-stu-id="47b58-198">In this example you can see that hello operation failed, and Application Insights has provided hello details of hello exception hello application threw.</span></span> <span data-ttu-id="47b58-199">Опять же, вы можете легко создать рабочий элемент TFS из этой колонки.</span><span class="sxs-lookup"><span data-stu-id="47b58-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Колонка "Операции" в Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="47b58-201"><a name="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47b58-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="47b58-202">[Веб-тестов] [ availability] -веб-запросов отправки tooyour приложения с регулярными интервалами из вокруг Здравствуй, мир.</span><span class="sxs-lookup"><span data-stu-id="47b58-202">[Web tests][availability] - Have web requests sent tooyour application at regular intervals from around hello world.</span></span>

<span data-ttu-id="47b58-203">[Записать и искать трассировки диагностики] [ diagnostic] — Вставка трассировки вызовов и анализировать проблемы toopinpoint результаты hello.</span><span class="sxs-lookup"><span data-stu-id="47b58-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through hello results toopinpoint issues.</span></span>

<span data-ttu-id="47b58-204">[Отслеживание использования][usage] — получайте информацию о том, как люди используют ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="47b58-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="47b58-205">[Устранение неполадок][qna] — вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="47b58-205">[Troubleshooting][qna] - and Q & A</span></span>



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



