---
title: "API Application Insights для пользовательских событий и метрик | Документация Майкрософт"
description: "Вставьте несколько строк кода в свое устройство или классическое приложение, на веб-страницу или в службу, чтобы отслеживать использование приложения и диагностировать неполадки."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: e94c50de51612243386d89c5e0b3178a4f9cbd38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="36d76-103">API Application Insights для пользовательских событий и метрик</span><span class="sxs-lookup"><span data-stu-id="36d76-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="36d76-104">Вставьте несколько строк кода в свое приложение, чтобы узнать, как пользователи его используют, или чтобы диагностировать неполадки.</span><span class="sxs-lookup"><span data-stu-id="36d76-104">Insert a few lines of code in your application to find out what users are doing with it, or to help diagnose issues.</span></span> <span data-ttu-id="36d76-105">Вы можете отправлять телеметрию из устройств и классических приложений, веб-клиентов и веб-серверов.</span><span class="sxs-lookup"><span data-stu-id="36d76-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="36d76-106">Используйте основной API телеметрии [Azure Application Insights](app-insights-overview.md), чтобы отправлять пользовательские события и метрики, а также собственные версии стандартной телеметрии.</span><span class="sxs-lookup"><span data-stu-id="36d76-106">Use the [Azure Application Insights](app-insights-overview.md) core telemetry API to send custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="36d76-107">Этот же API используется стандартными сборщиками данных Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36d76-107">This API is the same API that the standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="36d76-108">Сводные данные API</span><span class="sxs-lookup"><span data-stu-id="36d76-108">API summary</span></span>
<span data-ttu-id="36d76-109">Этот API используется на всех платформах, кроме некоторых небольших исключений.</span><span class="sxs-lookup"><span data-stu-id="36d76-109">The API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="36d76-110">Метод</span><span class="sxs-lookup"><span data-stu-id="36d76-110">Method</span></span> | <span data-ttu-id="36d76-111">Область использования</span><span class="sxs-lookup"><span data-stu-id="36d76-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="36d76-112">Страницы, экраны, колонки или формы.</span><span class="sxs-lookup"><span data-stu-id="36d76-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="36d76-113">Действия пользователя и другие события.</span><span class="sxs-lookup"><span data-stu-id="36d76-113">User actions and other events.</span></span> <span data-ttu-id="36d76-114">Используется для отслеживания поведения пользователя или мониторинга производительности.</span><span class="sxs-lookup"><span data-stu-id="36d76-114">Used to track user behavior or to monitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="36d76-115">Измерения производительности, не связанные с конкретными событиями, например, измерение длины очереди.</span><span class="sxs-lookup"><span data-stu-id="36d76-115">Performance measurements such as queue lengths not related to specific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="36d76-116">Регистрация исключений для диагностики.</span><span class="sxs-lookup"><span data-stu-id="36d76-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="36d76-117">Отслеживайте исключения, связанные с другими событиями, и изучайте трассировку стека.</span><span class="sxs-lookup"><span data-stu-id="36d76-117">Trace where they occur in relation to other events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="36d76-118">Регистрация частоты и длительности запросов к серверу для анализа производительности.</span><span class="sxs-lookup"><span data-stu-id="36d76-118">Logging the frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="36d76-119">Сообщения журналов диагностики.</span><span class="sxs-lookup"><span data-stu-id="36d76-119">Diagnostic log messages.</span></span> <span data-ttu-id="36d76-120">Можно также использовать журналы сторонних приложений.</span><span class="sxs-lookup"><span data-stu-id="36d76-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="36d76-121">Регистрация длительности и частоты вызовов внешних компонентов, от которых зависит приложение.</span><span class="sxs-lookup"><span data-stu-id="36d76-121">Logging the duration and frequency of calls to external components that your app depends on.</span></span> |

<span data-ttu-id="36d76-122">Вы можете [прикрепить свойства и метрики](#properties) к большинству этих вызовов телеметрии.</span><span class="sxs-lookup"><span data-stu-id="36d76-122">You can [attach properties and metrics](#properties) to most of these telemetry calls.</span></span>

## <span data-ttu-id="36d76-123"><a name="prep"></a>Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="36d76-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="36d76-124">Если у вас еще нет ссылки на пакет SDK Application Insights, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="36d76-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="36d76-125">Добавьте пакет SDK Application Insights в свой проект:</span><span class="sxs-lookup"><span data-stu-id="36d76-125">Add the Application Insights SDK to your project:</span></span>

  * [<span data-ttu-id="36d76-126">проект ASP.NET;</span><span class="sxs-lookup"><span data-stu-id="36d76-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="36d76-127">проект Java;</span><span class="sxs-lookup"><span data-stu-id="36d76-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="36d76-128">JavaScript на каждой веб-странице.</span><span class="sxs-lookup"><span data-stu-id="36d76-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="36d76-129">В программный код устройства или веб-сервера необходимо добавить:</span><span class="sxs-lookup"><span data-stu-id="36d76-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="36d76-130">*C#:* `using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="36d76-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="36d76-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="36d76-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="36d76-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="36d76-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="36d76-133">Создание экземпляра TelemetryClient</span><span class="sxs-lookup"><span data-stu-id="36d76-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="36d76-134">Создайте экземпляр `TelemetryClient` (за исключением JavaScript на веб-страницах).</span><span class="sxs-lookup"><span data-stu-id="36d76-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="36d76-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="36d76-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="36d76-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="36d76-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="36d76-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="36d76-138">Класс TelemetryClient является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="36d76-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="36d76-139">Рекомендуется использовать экземпляр TelemetryClient для каждого модуля приложения.</span><span class="sxs-lookup"><span data-stu-id="36d76-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="36d76-140">Например, у вас может быть один экземпляр TelemetryClient в веб-службе для отчетов о входящих HTTP-запросах, а другой в среднем классе для отчетов о событиях бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="36d76-140">For instance, you may have one TelemetryClient instance in your web service to report incoming HTTP requests, and another in a middleware class to report business logic events.</span></span> <span data-ttu-id="36d76-141">Можно задать свойства, например `TelemetryClient.Context.User.Id` для отслеживания пользователей и сеансов или `TelemetryClient.Context.Device.Id` для идентификации компьютера.</span><span class="sxs-lookup"><span data-stu-id="36d76-141">You can set properties such as `TelemetryClient.Context.User.Id` to track users and sessions, or `TelemetryClient.Context.Device.Id` to identify the machine.</span></span> <span data-ttu-id="36d76-142">Эти данные прикрепляются ко всем событиям, отправляемым экземпляром.</span><span class="sxs-lookup"><span data-stu-id="36d76-142">This information is attached to all events that the instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="36d76-143">TrackEvent (Отслеживание событий)</span><span class="sxs-lookup"><span data-stu-id="36d76-143">TrackEvent</span></span>
<span data-ttu-id="36d76-144">В Application Insights *пользовательское событие* — это точка данных, которую можно отобразить как суммарное значение в [обозревателе метрик](app-insights-metrics-explorer.md), а также как отдельные значения на вкладке [поиска по журналу диагностики](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="36d76-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="36d76-145">(Оно не связано с MVC и другими "событиями" платформы.)</span><span class="sxs-lookup"><span data-stu-id="36d76-145">(It isn't related to MVC or other framework "events.")</span></span>

<span data-ttu-id="36d76-146">Вставьте вызовы `TrackEvent` в код для подсчета различных событий:</span><span class="sxs-lookup"><span data-stu-id="36d76-146">Insert `TrackEvent` calls in your code to count various events.</span></span> <span data-ttu-id="36d76-147">как часто пользователи выбирают определенный компонент, как часто они достигают определенных целей, а также как часто возникают те или иные ошибки.</span><span class="sxs-lookup"><span data-stu-id="36d76-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="36d76-148">Например, отправляйте событие в игровом приложении при каждом выигрыше пользователя:</span><span class="sxs-lookup"><span data-stu-id="36d76-148">For example, in a game app, send an event whenever a user wins the game:</span></span>

<span data-ttu-id="36d76-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="36d76-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="36d76-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="36d76-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="36d76-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="36d76-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="36d76-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-the-microsoft-azure-portal"></a><span data-ttu-id="36d76-153">Просмотр событий на портале Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="36d76-153">View your events in the Microsoft Azure portal</span></span>
<span data-ttu-id="36d76-154">Чтобы увидеть число событий, откройте колонку [Обозреватель метрик](app-insights-metrics-explorer.md), добавьте новую диаграмму и выберите **События**.</span><span class="sxs-lookup"><span data-stu-id="36d76-154">To see a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Просмотр количества пользовательских событий](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="36d76-156">Чтобы сравнить количество различных событий, установите тип диаграммы **Сетка** и выполните группировку по имени события.</span><span class="sxs-lookup"><span data-stu-id="36d76-156">To compare the counts of different events, set the chart type to **Grid**, and group by event name:</span></span>

![Задание типа диаграммы и группировка](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="36d76-158">На сетке щелкните имя события, чтобы увидеть отдельные экземпляры данного события.</span><span class="sxs-lookup"><span data-stu-id="36d76-158">On the grid, click through an event name to see individual occurrences of that event.</span></span> <span data-ttu-id="36d76-159">Щелкните любое из них в списке, чтобы просмотреть подробные данные.</span><span class="sxs-lookup"><span data-stu-id="36d76-159">To see more detail - click any occurrence in the list.</span></span>

![Подробно просмотрите события](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="36d76-161">Чтобы сконцентрироваться на определенных событиях в функции поиска или в обозревателе метрик, задайте в фильтре колонки имена событий, которые вас интересуют.</span><span class="sxs-lookup"><span data-stu-id="36d76-161">To focus on specific events in either Search or Metrics Explorer, set the blade's filter to the event names that you're interested in:</span></span>

![Откройте "Фильтры", разверните пункт "Имя события" и выберите одно или несколько значений.](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="36d76-163">Пользовательские события в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="36d76-163">Custom events in Analytics</span></span>

<span data-ttu-id="36d76-164">Данные телеметрии доступны в таблице `customEvents` в [службе аналитики Application Insights](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="36d76-164">The telemetry is available in the `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="36d76-165">Каждая строка представляет собой вызов `trackEvent(..)` в приложении.</span><span class="sxs-lookup"><span data-stu-id="36d76-165">Each row represents a call to `trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="36d76-166">Если действует [выборка](app-insights-sampling.md), свойство itemCount имеет значение больше 1.</span><span class="sxs-lookup"><span data-stu-id="36d76-166">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="36d76-167">Например, itemCount==10 означает, что из 10 вызовов trackEvent() процесс выборки передал только один.</span><span class="sxs-lookup"><span data-stu-id="36d76-167">For example itemCount==10 means that of 10 calls to trackEvent(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="36d76-168">Поэтому, чтобы получить правильное количество пользовательских событий, следует использовать такой код, как `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="36d76-168">To get a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="36d76-169">TrackMetric (Отслеживание метрик)</span><span class="sxs-lookup"><span data-stu-id="36d76-169">TrackMetric</span></span>

<span data-ttu-id="36d76-170">Application Insights может создать диаграмму метрик, не привязанных к определенным событиям.</span><span class="sxs-lookup"><span data-stu-id="36d76-170">Application Insights can chart metrics that are not attached to particular events.</span></span> <span data-ttu-id="36d76-171">Например, можно отслеживать длину очереди через регулярные промежутки времени.</span><span class="sxs-lookup"><span data-stu-id="36d76-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="36d76-172">Благодаря метрикам отдельные измерения менее интересны, чем вариации и тенденции, и поэтому статистические диаграммы полезны.</span><span class="sxs-lookup"><span data-stu-id="36d76-172">With metrics, the individual measurements are of less interest than the variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="36d76-173">Для отправки метрик в Application Insights можно использовать API `TrackMetric(..)`.</span><span class="sxs-lookup"><span data-stu-id="36d76-173">In order to send metrics to Application Insights, you can use the `TrackMetric(..)` API.</span></span> <span data-ttu-id="36d76-174">Отправить метрику можно двумя способами.</span><span class="sxs-lookup"><span data-stu-id="36d76-174">There are two ways to send a metric:</span></span> 

* <span data-ttu-id="36d76-175">Отдельное значение.</span><span class="sxs-lookup"><span data-stu-id="36d76-175">Single value.</span></span> <span data-ttu-id="36d76-176">Каждый раз при выполнении измерения в приложении вы отправляете соответствующее значение в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36d76-176">Every time you perform a measurement in your application, you send the corresponding value to Application Insights.</span></span> <span data-ttu-id="36d76-177">Например, предположим, что имеется метрика, описывающая число элементов в контейнере.</span><span class="sxs-lookup"><span data-stu-id="36d76-177">For example, assume that you have a metric describing the number of items in a container.</span></span> <span data-ttu-id="36d76-178">В течение некоторого периода времени вы сначала помещаете три элемента в контейнер, а затем удаляете два элемента.</span><span class="sxs-lookup"><span data-stu-id="36d76-178">During a particular time period, you first put three items into the container and then you remove two items.</span></span> <span data-ttu-id="36d76-179">Соответственно, `TrackMetric` вызывается дважды: сначала передается значение `3`, а затем значение `-2`.</span><span class="sxs-lookup"><span data-stu-id="36d76-179">Accordingly, you would call `TrackMetric` twice: first passing the value `3` and then the value `-2`.</span></span> <span data-ttu-id="36d76-180">Application Insights сохраняет оба значения от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="36d76-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="36d76-181">Агрегирование.</span><span class="sxs-lookup"><span data-stu-id="36d76-181">Aggregation.</span></span> <span data-ttu-id="36d76-182">При работе с метриками отдельные измерения редко представляют интерес.</span><span class="sxs-lookup"><span data-stu-id="36d76-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="36d76-183">Вместо этого обычно важна сводка того, что произошло за определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="36d76-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="36d76-184">Такая сводка называется _агрегированием_.</span><span class="sxs-lookup"><span data-stu-id="36d76-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="36d76-185">В приведенном выше примере сумма агрегированной метрики за период времени равна `1`, а число значений метрики — `2`.</span><span class="sxs-lookup"><span data-stu-id="36d76-185">In the above example, the aggregate metric sum for that time period is `1` and the count of the metric values is `2`.</span></span> <span data-ttu-id="36d76-186">При использовании агрегирования `TrackMetric` вызывается только один раз для каждого периода времени и отправляются агрегированные значения.</span><span class="sxs-lookup"><span data-stu-id="36d76-186">When using the aggregation approach, you only invoke `TrackMetric` once per time period and send the aggregate values.</span></span> <span data-ttu-id="36d76-187">Это рекомендуемый подход, так как он может значительно снизить затраты и потери производительности благодаря отправке меньшего числа точек данных в Application Insights. При этом собирается вся важная информация.</span><span class="sxs-lookup"><span data-stu-id="36d76-187">This is the recommended approach since it can significantly reduce the cost and performance overhead by sending fewer data points to Application Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="36d76-188">Примеры:</span><span class="sxs-lookup"><span data-stu-id="36d76-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="36d76-189">Отдельные значения</span><span class="sxs-lookup"><span data-stu-id="36d76-189">Single values</span></span>

<span data-ttu-id="36d76-190">Отправка значения одной метрики</span><span class="sxs-lookup"><span data-stu-id="36d76-190">To send a single metric value:</span></span>

<span data-ttu-id="36d76-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="36d76-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="36d76-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="36d76-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="36d76-193">Агрегированные метрики</span><span class="sxs-lookup"><span data-stu-id="36d76-193">Aggregating metrics</span></span>

<span data-ttu-id="36d76-194">Рекомендуется агрегировать метрики перед их отправкой из приложения, чтобы уменьшить нагрузку на пропускную полосу, затраты и потери производительности.</span><span class="sxs-lookup"><span data-stu-id="36d76-194">It is recommended to aggregate metrics before sending them from your app, to reduce bandwidth, cost and to improve performance.</span></span>
<span data-ttu-id="36d76-195">Ниже представлен пример кода для агрегирования.</span><span class="sxs-lookup"><span data-stu-id="36d76-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="36d76-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-196">*C#*</span></span>

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends the aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of the aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap the current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute the actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct the metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="36d76-197">Пользовательские метрики в обозревателе метрик</span><span class="sxs-lookup"><span data-stu-id="36d76-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="36d76-198">Чтобы увидеть результаты, откройте обозреватель метрик и добавьте новую диаграмму.</span><span class="sxs-lookup"><span data-stu-id="36d76-198">To see the results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="36d76-199">Измените диаграмму, чтобы отобразить метрику.</span><span class="sxs-lookup"><span data-stu-id="36d76-199">Edit the chart to show your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="36d76-200">Пользовательская метрика может отобразиться в списке доступных метрик через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="36d76-200">Your custom metric might take several minutes to appear in the list of available metrics.</span></span>
>

![Добавьте новую диаграмму или выберите существующую, а в поле Custom (Пользовательские) выберите свою метрику](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="36d76-202">Настраиваемые метрики в аналитике</span><span class="sxs-lookup"><span data-stu-id="36d76-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="36d76-203">Данные телеметрии доступны в таблице `customMetrics` в [службе аналитики Application Insights](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="36d76-203">The telemetry is available in the `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="36d76-204">Каждая строка представляет собой вызов `trackMetric(..)` в приложении.</span><span class="sxs-lookup"><span data-stu-id="36d76-204">Each row represents a call to `trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="36d76-205">`valueSum` — это сумма измерений.</span><span class="sxs-lookup"><span data-stu-id="36d76-205">`valueSum` - This is the sum of the measurements.</span></span> <span data-ttu-id="36d76-206">Чтобы получить среднее значение, разделите текущее значение на значение `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="36d76-206">To get the mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="36d76-207">`valueCount` — число измерений, агрегированных в этот вызов `trackMetric(..)`.</span><span class="sxs-lookup"><span data-stu-id="36d76-207">`valueCount` - The number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="36d76-208">Просмотры страниц</span><span class="sxs-lookup"><span data-stu-id="36d76-208">Page views</span></span>
<span data-ttu-id="36d76-209">В устройстве или приложении веб-страницы телеметрия просмотров страницы отображается по умолчанию при загрузке каждого экрана или страницы.</span><span class="sxs-lookup"><span data-stu-id="36d76-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="36d76-210">Однако это можно изменить, чтобы отслеживать количество просмотров страницы в дополнительное или другое время.</span><span class="sxs-lookup"><span data-stu-id="36d76-210">But you can change that to track page views at additional or different times.</span></span> <span data-ttu-id="36d76-211">Например, в приложении, которое отображает вкладки или колонки, может потребоваться отслеживать страницу каждый раз, когда пользователь открывает новую колонку.</span><span class="sxs-lookup"><span data-stu-id="36d76-211">For example, in an app that displays tabs or blades, you might want to track a page whenever the user opens a new blade.</span></span>

![Область "Использование" в колонке "Обзор"](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="36d76-213">Данные о пользователе и сеансе отправляются в качестве свойств вместе с количеством просмотров страниц, поэтому диаграммы для пользователей и сеансов активируются при наличии телеметрии по количеству просмотров страницы.</span><span class="sxs-lookup"><span data-stu-id="36d76-213">User and session data is sent as properties along with page views, so the user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="36d76-214">Пользовательские данные о просмотре страницы</span><span class="sxs-lookup"><span data-stu-id="36d76-214">Custom page views</span></span>
<span data-ttu-id="36d76-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="36d76-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="36d76-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="36d76-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="36d76-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="36d76-218">Если у вас есть несколько вкладок на различных HTML-страницах, можно также указать URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="36d76-218">If you have several tabs within different HTML pages, you can specify the URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="36d76-219">Время просмотра страниц</span><span class="sxs-lookup"><span data-stu-id="36d76-219">Timing page views</span></span>
<span data-ttu-id="36d76-220">По умолчанию время, отображаемое как **Время загрузки страницы**, отсчитывается от момента отправки запроса браузером до вызова события загрузки страницы в браузере.</span><span class="sxs-lookup"><span data-stu-id="36d76-220">By default, the times reported as **Page view load time** are measured from when the browser sends the request, until the browser's page load event is called.</span></span>

<span data-ttu-id="36d76-221">Вместо этого вы можете выбрать один из таких вариантов:</span><span class="sxs-lookup"><span data-stu-id="36d76-221">Instead, you can either:</span></span>

* <span data-ttu-id="36d76-222">Задайте явную длительность вызова [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview): `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="36d76-222">Set an explicit duration in the [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="36d76-223">Используйте вызовы времени просмотра страницы `startTrackPage` и `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="36d76-223">Use the page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="36d76-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="36d76-224">*JavaScript*</span></span>

    // To start timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="36d76-225">...</span><span class="sxs-lookup"><span data-stu-id="36d76-225">...</span></span>

    // To stop timing and log the page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="36d76-226">Имя, используемое в качестве первого параметра, связывает вызовы start и stop.</span><span class="sxs-lookup"><span data-stu-id="36d76-226">The name that you use as the first parameter associates the start and stop calls.</span></span> <span data-ttu-id="36d76-227">По умолчанию используется имя текущей страницы.</span><span class="sxs-lookup"><span data-stu-id="36d76-227">It defaults to the current page name.</span></span>

<span data-ttu-id="36d76-228">Полученные длительности загрузки страниц, отображаемые в обозревателе метрик, являются производными интервала между вызовами start и stop.</span><span class="sxs-lookup"><span data-stu-id="36d76-228">The resulting page load durations displayed in Metrics Explorer are derived from the interval between the start and stop calls.</span></span> <span data-ttu-id="36d76-229">Выбор рассматриваемого интервала за вами.</span><span class="sxs-lookup"><span data-stu-id="36d76-229">It's up to you what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="36d76-230">Телеметрия страниц в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="36d76-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="36d76-231">В [службе аналитики](app-insights-analytics.md) две таблицы содержат данные по операциям в браузере.</span><span class="sxs-lookup"><span data-stu-id="36d76-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="36d76-232">Таблица `pageViews` содержит данные по URL-адресу и названию страницы.</span><span class="sxs-lookup"><span data-stu-id="36d76-232">The `pageViews` table contains data about the URL and page title</span></span>
* <span data-ttu-id="36d76-233">Таблица `browserTimings` содержит данные по производительности клиента, например время, затраченное на обработку входящих данных.</span><span class="sxs-lookup"><span data-stu-id="36d76-233">The `browserTimings` table contains data about client performance, such as the time taken to process the incoming data</span></span>

<span data-ttu-id="36d76-234">Чтобы узнать, сколько времени требуется браузеру на обработку различных страниц, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="36d76-234">To find how long the browser takes to process different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="36d76-235">Чтобы установить популярность различных браузеров, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="36d76-235">To discover the popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="36d76-236">Чтобы связать просмотры страниц с вызовами AJAX, выполните объединение с зависимостями:</span><span class="sxs-lookup"><span data-stu-id="36d76-236">To associate page views to AJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="36d76-237">TrackRequest (Отслеживание запросов)</span><span class="sxs-lookup"><span data-stu-id="36d76-237">TrackRequest</span></span>
<span data-ttu-id="36d76-238">TrackRequest используется в серверном пакете SDK, чтобы регистрировать HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="36d76-238">The server SDK uses TrackRequest to log HTTP requests.</span></span>

<span data-ttu-id="36d76-239">Его можно также вызвать самостоятельно, чтобы смодулировать запросы в контексте, в котором отсутствует выполняющийся модуль веб-службы.</span><span class="sxs-lookup"><span data-stu-id="36d76-239">You can also call it yourself if you want to simulate requests in a context where you don't have the web service module running.</span></span>

<span data-ttu-id="36d76-240">Мы рекомендуем отправлять телеметрию запроса, выступающего в качестве <a href="#operation-context">контекста операции</a>.</span><span class="sxs-lookup"><span data-stu-id="36d76-240">However, the recommended way to send request telemetry is where the request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="36d76-241">Контекст операции</span><span class="sxs-lookup"><span data-stu-id="36d76-241">Operation context</span></span>
<span data-ttu-id="36d76-242">Элементы телеметрии можно связать между собой, присвоив им общий идентификатор операции.</span><span class="sxs-lookup"><span data-stu-id="36d76-242">You can associate telemetry items together by attaching to them a common operation ID.</span></span> <span data-ttu-id="36d76-243">Стандартный модуль отслеживания запросов делает это для исключений и других событий, отправляемых во время обработки HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="36d76-243">The standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="36d76-244">В [службе поиска](app-insights-diagnostic-search.md) и [службе аналитики](app-insights-analytics.md) с помощью этого идентификатора можно легко найти все события, связанные с запросом.</span><span class="sxs-lookup"><span data-stu-id="36d76-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use the ID to easily find any events associated with the request.</span></span>

<span data-ttu-id="36d76-245">Самый простой способ задать этот идентификатор — установить контекст операции с помощью приведенного ниже шаблона.</span><span class="sxs-lookup"><span data-stu-id="36d76-245">The easiest way to set the ID is to set an operation context by using this pattern:</span></span>

<span data-ttu-id="36d76-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use the same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="36d76-247">Наряду с определением контекста операции `StartOperation` создает элемент телеметрии указанного вами типа</span><span class="sxs-lookup"><span data-stu-id="36d76-247">Along with setting an operation context, `StartOperation` creates a telemetry item of the type that you specify.</span></span> <span data-ttu-id="36d76-248">и отправляет его при удалении операции или при явном вызове `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="36d76-248">It sends the telemetry item when you dispose the operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="36d76-249">При использовании типа телеметрии `RequestTelemetry` ее длительность задается как временной интервал между запуском и остановкой.</span><span class="sxs-lookup"><span data-stu-id="36d76-249">If you use `RequestTelemetry` as the telemetry type, its duration is set to the timed interval between start and stop.</span></span>

<span data-ttu-id="36d76-250">Контексты операции не могут быть вложенными.</span><span class="sxs-lookup"><span data-stu-id="36d76-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="36d76-251">Если контекст операции уже существует, то его идентификатор связан со всеми вложенными элементами, включая элемент, созданный с помощью `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="36d76-251">If there is already an operation context, then its ID is associated with all the contained items, including the item created with `StartOperation`.</span></span>

<span data-ttu-id="36d76-252">В колонке поиска контекст операции используется для создания списка **связанных элементов**.</span><span class="sxs-lookup"><span data-stu-id="36d76-252">In Search, the operation context is used to create the **Related Items** list:</span></span>

![Связанные элементы](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="36d76-254">Дополнительные сведения об отслеживании пользовательских операций см. в разделе [application-insights-custom-operations-tracking.md].</span><span class="sxs-lookup"><span data-stu-id="36d76-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="36d76-255">Запросы в аналитике</span><span class="sxs-lookup"><span data-stu-id="36d76-255">Requests in Analytics</span></span> 

<span data-ttu-id="36d76-256">В [службе аналитики Application Insights](app-insights-analytics.md) запросы приводятся в таблице `requests`.</span><span class="sxs-lookup"><span data-stu-id="36d76-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in the `requests` table.</span></span>

<span data-ttu-id="36d76-257">Если действует [выборка](app-insights-sampling.md), свойство itemCount будет иметь значение больше 1.</span><span class="sxs-lookup"><span data-stu-id="36d76-257">If [sampling](app-insights-sampling.md) is in operation, the itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="36d76-258">Например, itemCount==10 означает, что из 10 вызовов trackRequest() процесс выборки передал только один.</span><span class="sxs-lookup"><span data-stu-id="36d76-258">For example itemCount==10 means that of 10 calls to trackRequest(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="36d76-259">Чтобы получить правильное число запросов и среднюю длительность, разбитую по именам запросов, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="36d76-259">To get a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="36d76-260">TrackException (Отслеживание исключений)</span><span class="sxs-lookup"><span data-stu-id="36d76-260">TrackException</span></span>
<span data-ttu-id="36d76-261">Отправляйте исключения в Application Insights, чтобы:</span><span class="sxs-lookup"><span data-stu-id="36d76-261">Send exceptions to Application Insights:</span></span>

* <span data-ttu-id="36d76-262">[определить их количество](app-insights-metrics-explorer.md) (для указания на частоту возникновения проблемы);</span><span class="sxs-lookup"><span data-stu-id="36d76-262">To [count them](app-insights-metrics-explorer.md), as an indication of the frequency of a problem.</span></span>
* <span data-ttu-id="36d76-263">[проверить отдельные значения.](app-insights-diagnostic-search.md)</span><span class="sxs-lookup"><span data-stu-id="36d76-263">To [examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="36d76-264">Отчеты содержат данные по трассировкам стеков.</span><span class="sxs-lookup"><span data-stu-id="36d76-264">The reports include the stack traces.</span></span>

<span data-ttu-id="36d76-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="36d76-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="36d76-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="36d76-267">Пакеты SDK перехватывают многие исключения автоматически, поэтому не всегда нужно явно вызвать метод TrackException.</span><span class="sxs-lookup"><span data-stu-id="36d76-267">The SDKs catch many exceptions automatically, so you don't always have to call TrackException explicitly.</span></span>

* <span data-ttu-id="36d76-268">ASP.NET: [написание кода для перехвата исключений](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="36d76-268">ASP.NET: [Write code to catch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="36d76-269">J2EE: [исключения перехватываются автоматически](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="36d76-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="36d76-270">JavaScript: исключения перехватываются автоматически.</span><span class="sxs-lookup"><span data-stu-id="36d76-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="36d76-271">Если вы хотите отключить автоматический сбор, добавьте строку в фрагмент кода, который вставляется на веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="36d76-271">If you want to disable automatic collection, add a line to the code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="36d76-272">Исключения в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="36d76-272">Exceptions in Analytics</span></span>

<span data-ttu-id="36d76-273">В [службе аналитики Application Insights](app-insights-analytics.md) исключения приводятся в таблице `exceptions`.</span><span class="sxs-lookup"><span data-stu-id="36d76-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in the `exceptions` table.</span></span>

<span data-ttu-id="36d76-274">Если действует [выборка](app-insights-sampling.md), свойство `itemCount` имеет значение больше 1.</span><span class="sxs-lookup"><span data-stu-id="36d76-274">If [sampling](app-insights-sampling.md) is in operation, the `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="36d76-275">Например, itemCount==10 означает, что из 10 вызовов trackException() процесс выборки передал только один.</span><span class="sxs-lookup"><span data-stu-id="36d76-275">For example itemCount==10 means that of 10 calls to trackException(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="36d76-276">Чтобы получить правильное число исключений, разбитое по типам исключений, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="36d76-276">To get a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="36d76-277">Большая часть важных сведений о стеке уже извлечена в отдельные переменные, однако вы можете разобрать структуру `details`, чтобы получить дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="36d76-277">Most of the important stack information is already extracted into separate variables, but you can pull apart the `details` structure to get more.</span></span> <span data-ttu-id="36d76-278">Так как это динамическая структура, результат следует привести к требуемому типу.</span><span class="sxs-lookup"><span data-stu-id="36d76-278">Since this structure is dynamic, you should cast the result to the type you expect.</span></span> <span data-ttu-id="36d76-279">Например:</span><span class="sxs-lookup"><span data-stu-id="36d76-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="36d76-280">Чтобы связать исключения с соответствующими запросами, используйте соединение:</span><span class="sxs-lookup"><span data-stu-id="36d76-280">To associate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="36d76-281">TrackTrace (Отслеживание трассировки)</span><span class="sxs-lookup"><span data-stu-id="36d76-281">TrackTrace</span></span>
<span data-ttu-id="36d76-282">Используйте TrackTrace для диагностики неполадок, отправляя навигационную цепочку в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36d76-282">Use TrackTrace to help diagnose problems by sending a "breadcrumb trail" to Application Insights.</span></span> <span data-ttu-id="36d76-283">Вы можете отправлять блоки диагностических данных и проверять их с помощью [поиска по журналу диагностики](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="36d76-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="36d76-284">[Адаптеры журнала](app-insights-asp-net-trace-logs.md) используют этот API для отправки журналов сторонних производителей на портал.</span><span class="sxs-lookup"><span data-stu-id="36d76-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API to send third-party logs to the portal.</span></span>

<span data-ttu-id="36d76-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="36d76-286">Вы можете выполнять поиск содержимого сообщения, но (в отличие от значений свойств) не можете фильтровать его.</span><span class="sxs-lookup"><span data-stu-id="36d76-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="36d76-287">Ограничения по размеру `message` гораздо выше, чем ограничение для свойств.</span><span class="sxs-lookup"><span data-stu-id="36d76-287">The size limit on `message` is much higher than the limit on properties.</span></span>
<span data-ttu-id="36d76-288">Преимуществом TrackTrace является возможность добавления в сообщения относительно длинных данных, </span><span class="sxs-lookup"><span data-stu-id="36d76-288">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="36d76-289">например данных POST.</span><span class="sxs-lookup"><span data-stu-id="36d76-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="36d76-290">Кроме того, вы можете настроить для сообщения уровень серьезности.</span><span class="sxs-lookup"><span data-stu-id="36d76-290">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="36d76-291">Как и для других данных телеметрии, вы можете добавлять значения свойства, используемые для фильтрации или поиска различных наборов трассировки.</span><span class="sxs-lookup"><span data-stu-id="36d76-291">And, like other telemetry, you can add property values to help you filter or search for different sets of traces.</span></span> <span data-ttu-id="36d76-292">Например:</span><span class="sxs-lookup"><span data-stu-id="36d76-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="36d76-293">В колонке [Поиск](app-insights-diagnostic-search.md) вы сможете легко отфильтровать все сообщения с определенной степенью серьезности, относящиеся к определенной базе данных.</span><span class="sxs-lookup"><span data-stu-id="36d76-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all the messages of a particular severity level that relate to a particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="36d76-294">Трассировки в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="36d76-294">Traces in Analytics</span></span>

<span data-ttu-id="36d76-295">В [службе аналитики Application Insights](app-insights-analytics.md) вызовы TrackTrace приводятся в таблице `traces`.</span><span class="sxs-lookup"><span data-stu-id="36d76-295">In [Application Insights Analytics](app-insights-analytics.md), calls to TrackTrace show up in the `traces` table.</span></span>

<span data-ttu-id="36d76-296">Если действует [выборка](app-insights-sampling.md), свойство itemCount имеет значение больше 1.</span><span class="sxs-lookup"><span data-stu-id="36d76-296">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="36d76-297">Например, itemCount==10 означает, что из 10 вызовов `trackTrace()` процесс выборки передал только один.</span><span class="sxs-lookup"><span data-stu-id="36d76-297">For example itemCount==10 means that of 10 calls to `trackTrace()`, the sampling process only transmitted one of them.</span></span> <span data-ttu-id="36d76-298">Чтобы получить правильное количество вызовов трассировки, следует использовать такой код, как `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="36d76-298">To get a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="36d76-299">TrackDependency (Отслеживание зависимостей)</span><span class="sxs-lookup"><span data-stu-id="36d76-299">TrackDependency</span></span>
<span data-ttu-id="36d76-300">Используйте вызов TrackDependency для отслеживания времени отклика и процента успешных попыток вызовов во внешнюю часть кода.</span><span class="sxs-lookup"><span data-stu-id="36d76-300">Use the TrackDependency call to track the response times and success rates of calls to an external piece of code.</span></span> <span data-ttu-id="36d76-301">Результаты отображаются в диаграммах зависимостей на портале.</span><span class="sxs-lookup"><span data-stu-id="36d76-301">The results appear in the dependency charts in the portal.</span></span>

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

<span data-ttu-id="36d76-302">Помните, что серверные пакеты SDK включают [модуль зависимостей](app-insights-asp-net-dependencies.md), который автоматически обнаруживает и отслеживает определенные вызовы зависимостей, например вызовы к базам данных и интерфейсам REST API.</span><span class="sxs-lookup"><span data-stu-id="36d76-302">Remember that the server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, to databases and REST APIs.</span></span> <span data-ttu-id="36d76-303">Для работы модуля необходимо установить агент на сервере.</span><span class="sxs-lookup"><span data-stu-id="36d76-303">You have to install an agent on your server to make the module work.</span></span> <span data-ttu-id="36d76-304">Используйте этот вызов, если необходимо отследить вызовы, которые не отслеживаются автоматически, или если вы не хотите устанавливать агент.</span><span class="sxs-lookup"><span data-stu-id="36d76-304">You use this call if you want to track calls that the automated tracking doesn't catch, or if you don't want to install the agent.</span></span>

<span data-ttu-id="36d76-305">Чтобы отключить стандартный модуль отслеживания зависимостей, измените файл [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) и удалите ссылку на `DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="36d76-305">To turn off the standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete the reference to `DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="36d76-306">Зависимости в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="36d76-306">Dependencies in Analytics</span></span>

<span data-ttu-id="36d76-307">В [службе аналитики Application Insights](app-insights-analytics.md) вызовы trackDependency приводятся в таблице `dependencies`.</span><span class="sxs-lookup"><span data-stu-id="36d76-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in the `dependencies` table.</span></span>

<span data-ttu-id="36d76-308">Если действует [выборка](app-insights-sampling.md), свойство itemCount имеет значение больше 1.</span><span class="sxs-lookup"><span data-stu-id="36d76-308">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="36d76-309">Например, itemCount==10 означает, что из 10 вызовов trackDependency() процесс выборки передал только один.</span><span class="sxs-lookup"><span data-stu-id="36d76-309">For example itemCount==10 means that of 10 calls to trackDependency(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="36d76-310">Чтобы получить правильное число зависимостей, разбитое по конечным компонентам, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="36d76-310">To get a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="36d76-311">Чтобы связать зависимости с соответствующими запросами, используйте соединение:</span><span class="sxs-lookup"><span data-stu-id="36d76-311">To associate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="36d76-312">Очистка данных</span><span class="sxs-lookup"><span data-stu-id="36d76-312">Flushing data</span></span>
<span data-ttu-id="36d76-313">Обычно пакет SDK отправляет данные в выбранный момент времени, чтобы свести влияние на пользователя к минимуму.</span><span class="sxs-lookup"><span data-stu-id="36d76-313">Normally, the SDK sends data at times chosen to minimize the impact on the user.</span></span> <span data-ttu-id="36d76-314">Однако в некоторых случаях может потребоваться очистить буфер, например, при использовании пакета SDK в приложении, которое завершает работу.</span><span class="sxs-lookup"><span data-stu-id="36d76-314">However, in some cases, you might want to flush the buffer--for example, if you are using the SDK in an application that shuts down.</span></span>

<span data-ttu-id="36d76-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="36d76-316">Обратите внимание, что для [канала телеметрии сервера](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/) эта функция является асинхронной.</span><span class="sxs-lookup"><span data-stu-id="36d76-316">Note that the function is asynchronous for the [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="36d76-317">Прошедшие проверку пользователи</span><span class="sxs-lookup"><span data-stu-id="36d76-317">Authenticated users</span></span>
<span data-ttu-id="36d76-318">В веб-приложении пользователи по умолчанию идентифицируются файлами cookie.</span><span class="sxs-lookup"><span data-stu-id="36d76-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="36d76-319">Пользователь может быть учтен более одного раза при доступе к приложению с другого компьютера или браузера либо при удалении файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="36d76-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="36d76-320">Если пользователи входят в ваше приложение, более точное их количество можно узнать, указав идентификатор пользователя, прошедшего аутентификацию, в коде браузера.</span><span class="sxs-lookup"><span data-stu-id="36d76-320">If users sign in to your app, you can get a more accurate count by setting the authenticated user ID in the browser code:</span></span>

<span data-ttu-id="36d76-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="36d76-321">*JavaScript*</span></span>

```JS
// Called when my app has identified the user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="36d76-322">Например, в веб-приложении MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="36d76-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="36d76-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="36d76-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="36d76-324">Нет необходимости использовать фактическое учетное имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="36d76-324">It isn't necessary to use the user's actual sign-in name.</span></span> <span data-ttu-id="36d76-325">Нужен только уникальный идентификатор этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="36d76-325">It only has to be an ID that is unique to that user.</span></span> <span data-ttu-id="36d76-326">В нем не должно быть пробелов или символов `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="36d76-326">It must not include spaces or any of the characters `,;=|`.</span></span>

<span data-ttu-id="36d76-327">Идентификатор пользователя также задается в файле cookie сеанса и отправляется на сервер.</span><span class="sxs-lookup"><span data-stu-id="36d76-327">The user ID is also set in a session cookie and sent to the server.</span></span> <span data-ttu-id="36d76-328">Если установлен серверный пакет SDK, идентификатор пользователя, прошедшего проверку подлинности, отправляется как часть свойств контекста телеметрии клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="36d76-328">If the server SDK is installed, the authenticated user ID is sent as part of the context properties of both client and server telemetry.</span></span> <span data-ttu-id="36d76-329">Затем можно выполнить фильтрацию и поиск.</span><span class="sxs-lookup"><span data-stu-id="36d76-329">You can then filter and search on it.</span></span>

<span data-ttu-id="36d76-330">Если приложение группирует пользователей по учетным записям, вы также можете передать идентификатор учетной записи (с аналогичными ограничениями знаков).</span><span class="sxs-lookup"><span data-stu-id="36d76-330">If your app groups users into accounts, you can also pass an identifier for the account (with the same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="36d76-331">В [обозревателе метрик](app-insights-metrics-explorer.md) можно создать диаграмму для отображения количества **пользователей, прошедших проверку подлинности**, а также **учетных записей пользователей**.</span><span class="sxs-lookup"><span data-stu-id="36d76-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="36d76-332">Кроме того, можно [выполнить поиск](app-insights-diagnostic-search.md) точек данных клиентов с определенными именами пользователей и учетными записями.</span><span class="sxs-lookup"><span data-stu-id="36d76-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="36d76-333"><a name="properties"></a>Фильтрация, поиск и сегментация данных с помощью свойств</span><span class="sxs-lookup"><span data-stu-id="36d76-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="36d76-334">Вы можете прикрепить свойства и результаты измерений к своим событиям, а также метрикам, просмотрам страниц, исключениям и другим данным телеметрии.</span><span class="sxs-lookup"><span data-stu-id="36d76-334">You can attach properties and measurements to your events (and also to metrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="36d76-335">*Свойства* — это строковые значения, которые можно использовать для фильтрации телеметрии в отчетах об использовании.</span><span class="sxs-lookup"><span data-stu-id="36d76-335">*Properties* are string values that you can use to filter your telemetry in the usage reports.</span></span> <span data-ttu-id="36d76-336">Например, если приложение содержит несколько игр, можно к каждому событию присоединять имя игры, чтобы видеть, какие игры наиболее популярны.</span><span class="sxs-lookup"><span data-stu-id="36d76-336">For example, if your app provides several games, you can attach the name of the game to each event so that you can see which games are more popular.</span></span>

<span data-ttu-id="36d76-337">В каждой строке может отображаться до 8192 событий.</span><span class="sxs-lookup"><span data-stu-id="36d76-337">There's a limit of 8192 on the string length.</span></span> <span data-ttu-id="36d76-338">(Если вы хотите отправлять большие блоки данных, используйте параметр сообщения [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="36d76-338">(If you want to send large chunks of data, use the message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="36d76-339">*Метрики* являются числовыми значениями, которые могут быть представлены в графическом виде.</span><span class="sxs-lookup"><span data-stu-id="36d76-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="36d76-340">Например, вам нужно будет посмотреть, постепенно ли увеличиваются зарабатываемые игроками очки.</span><span class="sxs-lookup"><span data-stu-id="36d76-340">For example, you might want to see if there's a gradual increase in the scores that your gamers achieve.</span></span> <span data-ttu-id="36d76-341">Графы можно сегментировать по свойствам, отправленным с событием, чтобы получать отдельные графы или набор граф для разных игр.</span><span class="sxs-lookup"><span data-stu-id="36d76-341">The graphs can be segmented by the properties that are sent with the event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="36d76-342">Чтобы значения метрик отображались правильно, они должны быть больше или равны 0.</span><span class="sxs-lookup"><span data-stu-id="36d76-342">For metric values to be correctly displayed, they should be greater than or equal to 0.</span></span>

<span data-ttu-id="36d76-343">Количество используемых [свойств, значений свойств и метрик ограничено](#limits) .</span><span class="sxs-lookup"><span data-stu-id="36d76-343">There are some [limits on the number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="36d76-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="36d76-344">*JavaScript*</span></span>

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


<span data-ttu-id="36d76-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="36d76-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="36d76-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="36d76-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="36d76-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="36d76-348">Постарайтесь не указывать в свойствах личные сведения.</span><span class="sxs-lookup"><span data-stu-id="36d76-348">Take care not to log personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="36d76-349">*При использовании метрик* откройте обозреватель метрик и выберите метрику из группы **Custom** (Пользовательские).</span><span class="sxs-lookup"><span data-stu-id="36d76-349">*If you used metrics*, open Metrics Explorer and select the metric from the **Custom** group:</span></span>

![Откройте обозреватель метрик, выделите диаграмму и выберите метрику](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="36d76-351">Если ваша метрика не отображается или заголовок **Custom** (Пользовательские) отсутствует, закройте колонку выбранной метрики и повторите попытку позже.</span><span class="sxs-lookup"><span data-stu-id="36d76-351">If your metric doesn't appear, or if the **Custom** heading isn't there, close the selection blade and try again later.</span></span> <span data-ttu-id="36d76-352">Иногда для вычисления метрик в конвейере может потребоваться час.</span><span class="sxs-lookup"><span data-stu-id="36d76-352">Metrics can sometimes take an hour to be aggregated through the pipeline.</span></span>

<span data-ttu-id="36d76-353">*При использовании свойств и метрик*сегментируйте метрики по свойствам:</span><span class="sxs-lookup"><span data-stu-id="36d76-353">*If you used properties and metrics*, segment the metric by the property:</span></span>

![Задайте группировку, а затем выберите свойство в списке "Группировать по"](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="36d76-355">*В колонке поиска по журналу диагностики*можно просматривать свойства и метрики, щелкая отдельные вхождения события.</span><span class="sxs-lookup"><span data-stu-id="36d76-355">*In Diagnostic Search*, you can view the properties and metrics of individual occurrences of an event.</span></span>

![Выберите экземпляр, а затем выберите "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="36d76-357">Используйте поле **поиска** для просмотра вхождений события с определенным значением свойства.</span><span class="sxs-lookup"><span data-stu-id="36d76-357">Use the **Search** field to see event occurrences that have a particular property value.</span></span>

![Введите слово в поле поиска](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="36d76-359">[Дополнительные сведения о выражениях поиска.](app-insights-diagnostic-search.md)</span><span class="sxs-lookup"><span data-stu-id="36d76-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-to-set-properties-and-metrics"></a><span data-ttu-id="36d76-360">Альтернативный способ настройки свойств и метрик</span><span class="sxs-lookup"><span data-stu-id="36d76-360">Alternative way to set properties and metrics</span></span>
<span data-ttu-id="36d76-361">Для удобства вы можете собирать параметры события в отдельный объект:</span><span class="sxs-lookup"><span data-stu-id="36d76-361">If it's more convenient, you can collect the parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="36d76-362">Не используйте один и тот же экземпляр элемента телеметрии (в этом примере `event`) для многократного вызова Track*().</span><span class="sxs-lookup"><span data-stu-id="36d76-362">Don't reuse the same telemetry item instance (`event` in this example) to call Track*() multiple times.</span></span> <span data-ttu-id="36d76-363">Это может привести к отправке телеметрии с неверной конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="36d76-363">This may cause telemetry to be sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="36d76-364">Пользовательские измерения и свойства в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="36d76-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="36d76-365">В [службе аналитики](app-insights-analytics.md) пользовательские метрики и свойства приводятся в атрибутах `customMeasurements` и `customDimensions` каждой записи телеметрии.</span><span class="sxs-lookup"><span data-stu-id="36d76-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in the `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="36d76-366">Например, если вы добавили свойство game в телеметрию запросов, следующий запрос подсчитывает число различных значений свойства game и показывает среднее значение пользовательской метрики score:</span><span class="sxs-lookup"><span data-stu-id="36d76-366">For example, if you have added a property named "game" to your request telemetry, this query counts the occurrences of different values of "game", and show the average of the custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="36d76-367">Обратите внимание на указанные ниже моменты.</span><span class="sxs-lookup"><span data-stu-id="36d76-367">Notice that:</span></span>

* <span data-ttu-id="36d76-368">При извлечении значения из JSON customDimensions или customMeasurements оно имеет динамический тип, поэтому его необходимо привести к `tostring` или `todouble`.</span><span class="sxs-lookup"><span data-stu-id="36d76-368">When you extract a value from the customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="36d76-369">С учетом возможности [выборки](app-insights-sampling.md) следует использовать `sum(itemCount)`, а не `count()`.</span><span class="sxs-lookup"><span data-stu-id="36d76-369">To take account of the possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="36d76-370"><a name="timed"></a> События времени</span><span class="sxs-lookup"><span data-stu-id="36d76-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="36d76-371">Иногда требуется отобразить на диаграмме продолжительность выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="36d76-371">Sometimes you want to chart how long it takes to perform an action.</span></span> <span data-ttu-id="36d76-372">Например, может потребоваться определить, сколько времени нужно пользователям для выбора решений в игре.</span><span class="sxs-lookup"><span data-stu-id="36d76-372">For example, you might want to know how long users take to consider choices in a game.</span></span> <span data-ttu-id="36d76-373">Для этого можно использовать параметр измерения.</span><span class="sxs-lookup"><span data-stu-id="36d76-373">You can use the measurement parameter for this.</span></span>

<span data-ttu-id="36d76-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform the timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send the event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="36d76-375"><a name="defaults"></a>Свойства по умолчанию для настраиваемой телеметрии</span><span class="sxs-lookup"><span data-stu-id="36d76-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="36d76-376">Если для некоторых создаваемых пользовательских событий требуется задать значения свойств по умолчанию, можно сделать это в экземпляре TelemetryClient.</span><span class="sxs-lookup"><span data-stu-id="36d76-376">If you want to set default property values for some of the custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="36d76-377">Они прикреплены к каждому элементу телеметрии, отправляемой из этого клиента.</span><span class="sxs-lookup"><span data-stu-id="36d76-377">They are attached to every telemetry item that's sent from that client.</span></span>

<span data-ttu-id="36d76-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="36d76-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="36d76-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="36d76-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="36d76-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="36d76-381">Вызовы отдельных данных телеметрии могут переопределить значения по умолчанию в словарях свойства.</span><span class="sxs-lookup"><span data-stu-id="36d76-381">Individual telemetry calls can override the default values in their property dictionaries.</span></span>

<span data-ttu-id="36d76-382">*Для веб-клиентов JavaScript*[используйте инициализаторы телеметрии JavaScript](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="36d76-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="36d76-383">*Чтобы добавить свойства для всей телеметрии*, включая данные из модулей стандартной коллекции, [реализуйте `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="36d76-383">*To add properties to all telemetry*, including the data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="36d76-384">Выборка, фильтрация и обработка данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="36d76-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="36d76-385">Для обработки телеметрии перед отправкой из пакета SDK можно написать код.</span><span class="sxs-lookup"><span data-stu-id="36d76-385">You can write code to process your telemetry before it's sent from the SDK.</span></span> <span data-ttu-id="36d76-386">Будут обрабатываться данные, отправляемые из модулей стандартной телеметрии, таких как коллекция запросов HTTP и коллекция зависимостей.</span><span class="sxs-lookup"><span data-stu-id="36d76-386">The processing includes data that's sent from the standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="36d76-387">[Добавьте свойства](app-insights-api-filtering-sampling.md#add-properties) в телеметрию, реализовав `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="36d76-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) to telemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="36d76-388">Например, можно добавить номера версий или значения, вычисленные на основе других свойств.</span><span class="sxs-lookup"><span data-stu-id="36d76-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="36d76-389">Используя [фильтрацию](app-insights-api-filtering-sampling.md#filtering), можно изменить или отменить телеметрию перед ее отправкой из пакета SDK. Для этого реализуйте `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="36d76-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from the SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="36d76-390">Вы сможете управлять тем, какие данные отправляются, а какие отклоняются. Однако при этом необходимо учитывать влияние на метрики.</span><span class="sxs-lookup"><span data-stu-id="36d76-390">You control what is sent or discarded, but you have to account for the effect on your metrics.</span></span> <span data-ttu-id="36d76-391">В зависимости от способа отклонения элементов можно потерять возможность перехода между связанными элементами.</span><span class="sxs-lookup"><span data-stu-id="36d76-391">Depending on how you discard items, you might lose the ability to navigate between related items.</span></span>

<span data-ttu-id="36d76-392">[Выборка](app-insights-api-filtering-sampling.md) представляет собой упакованное решение для сокращения объема данных, отправляемых из приложения на портал.</span><span class="sxs-lookup"><span data-stu-id="36d76-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution to reduce the volume of data that's sent from your app to the portal.</span></span> <span data-ttu-id="36d76-393">На отображаемые метрики выборка не влияет.</span><span class="sxs-lookup"><span data-stu-id="36d76-393">It does so without affecting the displayed metrics.</span></span> <span data-ttu-id="36d76-394">Возможность диагностировать проблемы путем перехода между связанными элементами, такими как исключения, запросы и просмотры страниц, также не затрагивается.</span><span class="sxs-lookup"><span data-stu-id="36d76-394">And it does so without affecting your ability to diagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="36d76-395">[Подробнее](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="36d76-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="36d76-396">Отключение телеметрии</span><span class="sxs-lookup"><span data-stu-id="36d76-396">Disabling telemetry</span></span>
<span data-ttu-id="36d76-397">Чтобы *динамически остановить и запустить* сбор и передачу данных телеметрии:</span><span class="sxs-lookup"><span data-stu-id="36d76-397">To *dynamically stop and start* the collection and transmission of telemetry:</span></span>

<span data-ttu-id="36d76-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="36d76-399">Чтобы *отключить выбранные стандартные сборщики*, например счетчики производительности, HTTP-запросы или зависимости, удалите или закомментируйте соответствующие строки в файле [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Это можно сделать, если вы, например, хотите отправить собственные данные TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="36d76-399">To *disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want to send your own TrackRequest data.</span></span>

## <span data-ttu-id="36d76-400"><a name="debug"></a>Режим разработчика</span><span class="sxs-lookup"><span data-stu-id="36d76-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="36d76-401">Во время отладки полезно передавать телеметрию через конвейер, чтобы результаты можно было увидеть немедленно.</span><span class="sxs-lookup"><span data-stu-id="36d76-401">During debugging, it's useful to have your telemetry expedited through the pipeline so that you can see results immediately.</span></span> <span data-ttu-id="36d76-402">Кроме того, вы можете получать дополнительные сообщения, которые помогают трассировать любые проблемы с телеметрией.</span><span class="sxs-lookup"><span data-stu-id="36d76-402">You also get additional messages that help you trace any problems with the telemetry.</span></span> <span data-ttu-id="36d76-403">Отключите этот режим в рабочей среде, так как он может замедлить работу приложения.</span><span class="sxs-lookup"><span data-stu-id="36d76-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="36d76-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="36d76-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="36d76-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="36d76-406"><a name="ikey"></a> Установка ключа инструментирования для выбранной пользовательской телеметрии</span><span class="sxs-lookup"><span data-stu-id="36d76-406"><a name="ikey"></a> Setting the instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="36d76-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="36d76-408"><a name="dynamic-ikey"></a> Динамический ключ инструментирования</span><span class="sxs-lookup"><span data-stu-id="36d76-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="36d76-409">Во избежание смешивания телеметрии из среды разработки, тестовой и рабочей среды вы можете [создавать отдельные ресурсы Application Insights](app-insights-create-new-resource.md) и менять их ключи в зависимости от среды.</span><span class="sxs-lookup"><span data-stu-id="36d76-409">To avoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on the environment.</span></span>

<span data-ttu-id="36d76-410">Вместо получения ключа инструментирования из файла конфигурации можно задать его в коде.</span><span class="sxs-lookup"><span data-stu-id="36d76-410">Instead of getting the instrumentation key from the configuration file, you can set it in your code.</span></span> <span data-ttu-id="36d76-411">Задайте ключ в методе инициализации, таком как global.aspx.cs, в службе ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="36d76-411">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="36d76-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="36d76-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="36d76-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="36d76-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="36d76-414">На веб-странице может потребоваться задать его, используя состояние веб-сервера, а не внедрить его в сценарий.</span><span class="sxs-lookup"><span data-stu-id="36d76-414">In webpages, you might want to set it from the web server's state, rather than coding it literally into the script.</span></span> <span data-ttu-id="36d76-415">Например, на веб-странице, созданной в приложении ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="36d76-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="36d76-416">*JavaScript в Razor*</span><span class="sxs-lookup"><span data-stu-id="36d76-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="36d76-417">Класс TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="36d76-417">TelemetryContext</span></span>
<span data-ttu-id="36d76-418">Экземпляр TelemetryClient включает свойство Context, содержащее несколько значений, которые отправляются вместе со всеми данными телеметрии.</span><span class="sxs-lookup"><span data-stu-id="36d76-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="36d76-419">Как правило, их задают модули стандартной телеметрии, но их также можно задать самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="36d76-419">They are normally set by the standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="36d76-420">Например:</span><span class="sxs-lookup"><span data-stu-id="36d76-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="36d76-421">Если задать эти значения самостоятельно, мы советуем удалить соответствующую строку из файла [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), чтобы не перепутать собственные значения и стандартные значения.</span><span class="sxs-lookup"><span data-stu-id="36d76-421">If you set any of these values yourself, consider removing the relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and the standard values don't get confused.</span></span>

* <span data-ttu-id="36d76-422">**Component:** приложение и его версия.</span><span class="sxs-lookup"><span data-stu-id="36d76-422">**Component**: The app and its version.</span></span>
* <span data-ttu-id="36d76-423">**Device:** данные об устройстве, на котором выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="36d76-423">**Device**: Data about the device where the app is running.</span></span> <span data-ttu-id="36d76-424">(В веб-приложениях это сервер или клиентское устройство, с которых отправляется телеметрия.)</span><span class="sxs-lookup"><span data-stu-id="36d76-424">(In web apps, this is the server or client device that the telemetry is sent from.)</span></span>
* <span data-ttu-id="36d76-425">**InstrumentationKey**: ресурс Application Insights в Azure, в котором отображается телеметрия.</span><span class="sxs-lookup"><span data-stu-id="36d76-425">**InstrumentationKey**: The Application Insights resource in Azure where the telemetry appear.</span></span> <span data-ttu-id="36d76-426">Обычно этот ресурс получают из файла ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="36d76-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="36d76-427">**Location:** географическое расположение устройства.</span><span class="sxs-lookup"><span data-stu-id="36d76-427">**Location**: The geographic location of the device.</span></span>
* <span data-ttu-id="36d76-428">**Operation:** текущий HTTP-запрос в веб-приложениях.</span><span class="sxs-lookup"><span data-stu-id="36d76-428">**Operation**: In web apps, the current HTTP request.</span></span> <span data-ttu-id="36d76-429">В приложениях других типов для этого значения можно задать значение "Группировать события совместно".</span><span class="sxs-lookup"><span data-stu-id="36d76-429">In other app types, you can set this to group events together.</span></span>
  * <span data-ttu-id="36d76-430">**Id:** созданное значение, которое сопоставляет различные события, чтобы при проверке любого события в поиске по журналу диагностики можно было найти связанные элементы.</span><span class="sxs-lookup"><span data-stu-id="36d76-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="36d76-431">**Name**: идентификатор, обычно URL-адрес HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="36d76-431">**Name**: An identifier, usually the URL of the HTTP request.</span></span>
  * <span data-ttu-id="36d76-432">**SyntheticSource:** если эта строка не пустая и не имеет значение null, она означает, что источник запроса был определен как программа-робот или веб-тест.</span><span class="sxs-lookup"><span data-stu-id="36d76-432">**SyntheticSource**: If not null or empty, a string that indicates that the source of the request has been identified as a robot or web test.</span></span> <span data-ttu-id="36d76-433">По умолчанию он исключается из вычислений в обозревателе метрик.</span><span class="sxs-lookup"><span data-stu-id="36d76-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="36d76-434">**Properties:** свойства, которые отправляются со всеми данными телеметрии.</span><span class="sxs-lookup"><span data-stu-id="36d76-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="36d76-435">Это значение можно переопределить в отдельных вызовах Track*.</span><span class="sxs-lookup"><span data-stu-id="36d76-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="36d76-436">**Session:** сеанс пользователя.</span><span class="sxs-lookup"><span data-stu-id="36d76-436">**Session**: The user's session.</span></span> <span data-ttu-id="36d76-437">Для Id задается созданное значение, которое изменяется, если пользователь был неактивным в течение некоторого времени.</span><span class="sxs-lookup"><span data-stu-id="36d76-437">The ID is set to a generated value, which is changed when the user has not been active for a while.</span></span>
* <span data-ttu-id="36d76-438">**User:** информация о пользователе.</span><span class="sxs-lookup"><span data-stu-id="36d76-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="36d76-439">Ограничения</span><span class="sxs-lookup"><span data-stu-id="36d76-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="36d76-440">Чтобы избежать превышения ограничения на скорость передачи данных, используйте [выборку](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="36d76-440">To avoid hitting the data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="36d76-441">Сведения о том, как определить, как долго хранятся данные, см. в статье [Сбор и хранение данных в Application Insights](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="36d76-441">To determine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="36d76-442">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="36d76-442">Reference docs</span></span>
* [<span data-ttu-id="36d76-443">Справочник по ASP.NET</span><span class="sxs-lookup"><span data-stu-id="36d76-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="36d76-444">Справочник по Java</span><span class="sxs-lookup"><span data-stu-id="36d76-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="36d76-445">Справочник по JavaScript</span><span class="sxs-lookup"><span data-stu-id="36d76-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="36d76-446">Android SDK</span><span class="sxs-lookup"><span data-stu-id="36d76-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="36d76-447">iOS SDK</span><span class="sxs-lookup"><span data-stu-id="36d76-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="36d76-448">Код пакета SDK</span><span class="sxs-lookup"><span data-stu-id="36d76-448">SDK code</span></span>
* [<span data-ttu-id="36d76-449">Базовый пакет SDK для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="36d76-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="36d76-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="36d76-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="36d76-451">Пакеты Windows Server</span><span class="sxs-lookup"><span data-stu-id="36d76-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="36d76-452">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="36d76-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="36d76-453">Пакет SDK для JavaScript</span><span class="sxs-lookup"><span data-stu-id="36d76-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="36d76-454">Все платформы</span><span class="sxs-lookup"><span data-stu-id="36d76-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="36d76-455">Вопросы</span><span class="sxs-lookup"><span data-stu-id="36d76-455">Questions</span></span>
* <span data-ttu-id="36d76-456">*Какие исключения могут создаваться при вызовах Track_()?*</span><span class="sxs-lookup"><span data-stu-id="36d76-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="36d76-457">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="36d76-457">None.</span></span> <span data-ttu-id="36d76-458">Вам не нужно помещать их в предложения try-catch.</span><span class="sxs-lookup"><span data-stu-id="36d76-458">You don't need to wrap them in try-catch clauses.</span></span> <span data-ttu-id="36d76-459">Если пакет SDK сталкивается с проблемами, он добавляет в журнал сообщения, которые отображаются в консоли отладки и, если сообщения проходят, — в поиске по журналу диагностики.</span><span class="sxs-lookup"><span data-stu-id="36d76-459">If the SDK encounters problems, it will log messages in the debug console output and--if the messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="36d76-460">*Существует ли REST API для получения данных из портала?*</span><span class="sxs-lookup"><span data-stu-id="36d76-460">*Is there a REST API to get data from the portal?*</span></span>

    <span data-ttu-id="36d76-461">Да, [API доступа к данным](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="36d76-461">Yes, the [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="36d76-462">К другим способам извлечения данных относятся [экспорт из Analytics в Power BI](app-insights-export-power-bi.md) и [непрерывный экспорт](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="36d76-462">Other ways to extract data include [export from Analytics to Power BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="36d76-463"><a name="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36d76-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="36d76-464">Поиск в Application Insights</span><span class="sxs-lookup"><span data-stu-id="36d76-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="36d76-465">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="36d76-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


