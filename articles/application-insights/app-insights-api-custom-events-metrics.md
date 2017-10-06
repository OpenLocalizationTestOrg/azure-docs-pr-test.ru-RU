---
title: "aaaApplication аналитики API пользовательские события и метрики | Документы Microsoft"
description: "Вставить несколько строк кода в tootrack устройства или классического приложения, веб-страницы или службы, использование и диагностировать проблемы."
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
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="b61cc-103">API Application Insights для пользовательских событий и метрик</span><span class="sxs-lookup"><span data-stu-id="b61cc-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="b61cc-104">Вставить несколько строк кода в ваш приложения toofind out действиями пользователей с ним или toohelp диагностировать проблемы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-104">Insert a few lines of code in your application toofind out what users are doing with it, or toohelp diagnose issues.</span></span> <span data-ttu-id="b61cc-105">Вы можете отправлять телеметрию из устройств и классических приложений, веб-клиентов и веб-серверов.</span><span class="sxs-lookup"><span data-stu-id="b61cc-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="b61cc-106">Используйте hello [Azure Application Insights](app-insights-overview.md) основной API телеметрии toosend пользовательские события и метрики и версий стандартной телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b61cc-106">Use hello [Azure Application Insights](app-insights-overview.md) core telemetry API toosend custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="b61cc-107">Этот API является hello же API-Интерфейсом этого стандарта hello, используемое сборщики данных Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b61cc-107">This API is hello same API that hello standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="b61cc-108">Сводные данные API</span><span class="sxs-lookup"><span data-stu-id="b61cc-108">API summary</span></span>
<span data-ttu-id="b61cc-109">Hello API единообразно для всех платформ, помимо несколько небольшие вариации.</span><span class="sxs-lookup"><span data-stu-id="b61cc-109">hello API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="b61cc-110">Метод</span><span class="sxs-lookup"><span data-stu-id="b61cc-110">Method</span></span> | <span data-ttu-id="b61cc-111">Область использования</span><span class="sxs-lookup"><span data-stu-id="b61cc-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="b61cc-112">Страницы, экраны, колонки или формы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="b61cc-113">Действия пользователя и другие события.</span><span class="sxs-lookup"><span data-stu-id="b61cc-113">User actions and other events.</span></span> <span data-ttu-id="b61cc-114">Использовать поведение или toomonitor производительности tootrack пользователя.</span><span class="sxs-lookup"><span data-stu-id="b61cc-114">Used tootrack user behavior or toomonitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="b61cc-115">Показатели производительности, такие как длина очереди не события, связанные с toospecific.</span><span class="sxs-lookup"><span data-stu-id="b61cc-115">Performance measurements such as queue lengths not related toospecific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="b61cc-116">Регистрация исключений для диагностики.</span><span class="sxs-lookup"><span data-stu-id="b61cc-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="b61cc-117">Трассировки, где они происходят в отношение tooother события и трассировки стека.</span><span class="sxs-lookup"><span data-stu-id="b61cc-117">Trace where they occur in relation tooother events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="b61cc-118">Ведение журнала hello частота и длительность запросов к серверу для анализа производительности.</span><span class="sxs-lookup"><span data-stu-id="b61cc-118">Logging hello frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="b61cc-119">Сообщения журналов диагностики.</span><span class="sxs-lookup"><span data-stu-id="b61cc-119">Diagnostic log messages.</span></span> <span data-ttu-id="b61cc-120">Можно также использовать журналы сторонних приложений.</span><span class="sxs-lookup"><span data-stu-id="b61cc-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="b61cc-121">Длительность hello ведения журнала и частоты вызовов tooexternal компонентов, от которых зависит приложение.</span><span class="sxs-lookup"><span data-stu-id="b61cc-121">Logging hello duration and frequency of calls tooexternal components that your app depends on.</span></span> |

<span data-ttu-id="b61cc-122">Вы можете [присоедините свойства и метрики](#properties) toomost этих вызовов телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b61cc-122">You can [attach properties and metrics](#properties) toomost of these telemetry calls.</span></span>

## <span data-ttu-id="b61cc-123"><a name="prep"></a>Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="b61cc-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="b61cc-124">Если у вас еще нет ссылки на пакет SDK Application Insights, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="b61cc-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="b61cc-125">Добавьте проект tooyour hello пакет SDK Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b61cc-125">Add hello Application Insights SDK tooyour project:</span></span>

  * [<span data-ttu-id="b61cc-126">проект ASP.NET;</span><span class="sxs-lookup"><span data-stu-id="b61cc-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="b61cc-127">проект Java;</span><span class="sxs-lookup"><span data-stu-id="b61cc-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="b61cc-128">JavaScript на каждой веб-странице.</span><span class="sxs-lookup"><span data-stu-id="b61cc-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="b61cc-129">В программный код устройства или веб-сервера необходимо добавить:</span><span class="sxs-lookup"><span data-stu-id="b61cc-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="b61cc-130">*C#:* `using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="b61cc-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="b61cc-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="b61cc-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="b61cc-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="b61cc-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="b61cc-133">Создание экземпляра TelemetryClient</span><span class="sxs-lookup"><span data-stu-id="b61cc-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="b61cc-134">Создайте экземпляр `TelemetryClient` (за исключением JavaScript на веб-страницах).</span><span class="sxs-lookup"><span data-stu-id="b61cc-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="b61cc-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="b61cc-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b61cc-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="b61cc-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="b61cc-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="b61cc-138">Класс TelemetryClient является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="b61cc-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="b61cc-139">Рекомендуется использовать экземпляр TelemetryClient для каждого модуля приложения.</span><span class="sxs-lookup"><span data-stu-id="b61cc-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="b61cc-140">Для экземпляра может иметь один экземпляр TelemetryClient в web service tooreport входящих HTTP-запросы, а другой в по промежуточного слоя класс tooreport бизнес-логики событий.</span><span class="sxs-lookup"><span data-stu-id="b61cc-140">For instance, you may have one TelemetryClient instance in your web service tooreport incoming HTTP requests, and another in a middleware class tooreport business logic events.</span></span> <span data-ttu-id="b61cc-141">Например, можно задать свойства `TelemetryClient.Context.User.Id` tootrack пользователей и сеансов, или `TelemetryClient.Context.Device.Id` tooidentify hello машины.</span><span class="sxs-lookup"><span data-stu-id="b61cc-141">You can set properties such as `TelemetryClient.Context.User.Id` tootrack users and sessions, or `TelemetryClient.Context.Device.Id` tooidentify hello machine.</span></span> <span data-ttu-id="b61cc-142">Эта информация является tooall присоединенные события, которые hello отправляет экземпляра.</span><span class="sxs-lookup"><span data-stu-id="b61cc-142">This information is attached tooall events that hello instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="b61cc-143">TrackEvent (Отслеживание событий)</span><span class="sxs-lookup"><span data-stu-id="b61cc-143">TrackEvent</span></span>
<span data-ttu-id="b61cc-144">В Application Insights *пользовательское событие* — это точка данных, которую можно отобразить как суммарное значение в [обозревателе метрик](app-insights-metrics-explorer.md), а также как отдельные значения на вкладке [поиска по журналу диагностики](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b61cc-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="b61cc-145">(Это не связанных tooMVC или других framework» событий.»)</span><span class="sxs-lookup"><span data-stu-id="b61cc-145">(It isn't related tooMVC or other framework "events.")</span></span>

<span data-ttu-id="b61cc-146">Вставить `TrackEvent` вызывает в ваш код toocount различных событий.</span><span class="sxs-lookup"><span data-stu-id="b61cc-146">Insert `TrackEvent` calls in your code toocount various events.</span></span> <span data-ttu-id="b61cc-147">как часто пользователи выбирают определенный компонент, как часто они достигают определенных целей, а также как часто возникают те или иные ошибки.</span><span class="sxs-lookup"><span data-stu-id="b61cc-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="b61cc-148">Например в приложении игрового отправьте событие, когда пользователь wins игры hello:</span><span class="sxs-lookup"><span data-stu-id="b61cc-148">For example, in a game app, send an event whenever a user wins hello game:</span></span>

<span data-ttu-id="b61cc-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b61cc-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="b61cc-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="b61cc-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b61cc-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="b61cc-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="b61cc-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a><span data-ttu-id="b61cc-153">Просмотр событий в портал Microsoft Azure hello</span><span class="sxs-lookup"><span data-stu-id="b61cc-153">View your events in hello Microsoft Azure portal</span></span>
<span data-ttu-id="b61cc-154">Откройте toosee число событий, [обозревателя метрик](app-insights-metrics-explorer.md) , добавить новую диаграмму и, при необходимости выберите **события**.</span><span class="sxs-lookup"><span data-stu-id="b61cc-154">toosee a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Просмотр количества пользовательских событий](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="b61cc-156">счетчики hello toocompare различных событий установите тип диаграммы hello слишком**сетки**и группы, имя события:</span><span class="sxs-lookup"><span data-stu-id="b61cc-156">toocompare hello counts of different events, set hello chart type too**Grid**, and group by event name:</span></span>

![Выберите тип диаграммы hello и группирование](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="b61cc-158">В сетке hello, щелкая событий имя toosee отдельные копии этого события.</span><span class="sxs-lookup"><span data-stu-id="b61cc-158">On hello grid, click through an event name toosee individual occurrences of that event.</span></span> <span data-ttu-id="b61cc-159">toosee более подробно описывается - щелкните любое событие, в списке hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-159">toosee more detail - click any occurrence in hello list.</span></span>

![Детализация hello события](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="b61cc-161">toofocus на определенные события в поиска или обозревателя метрик набор hello колонке фильтра toohello имена событий вы заинтересованы в:</span><span class="sxs-lookup"><span data-stu-id="b61cc-161">toofocus on specific events in either Search or Metrics Explorer, set hello blade's filter toohello event names that you're interested in:</span></span>

![Откройте "Фильтры", разверните пункт "Имя события" и выберите одно или несколько значений.](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="b61cc-163">Пользовательские события в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="b61cc-163">Custom events in Analytics</span></span>

<span data-ttu-id="b61cc-164">Hello телеметрии доступен в hello `customEvents` в таблицу [приложения аналитика Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="b61cc-164">hello telemetry is available in hello `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="b61cc-165">Каждая строка представляет вызов слишком`trackEvent(..)` в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="b61cc-165">Each row represents a call too`trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="b61cc-166">Если [выборки](app-insights-sampling.md) находится в операции, свойство itemCount hello показывает значение больше 1.</span><span class="sxs-lookup"><span data-stu-id="b61cc-166">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="b61cc-167">Для примера itemCount == 10 означает, что из tootrackEvent() 10 вызовов hello выборки процесса передаются только один из них.</span><span class="sxs-lookup"><span data-stu-id="b61cc-167">For example itemCount==10 means that of 10 calls tootrackEvent(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="b61cc-168">tooget правильное число пользовательских событий, следует использовать таким образом использовать код, например `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-168">tooget a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="b61cc-169">TrackMetric (Отслеживание метрик)</span><span class="sxs-lookup"><span data-stu-id="b61cc-169">TrackMetric</span></span>

<span data-ttu-id="b61cc-170">Application Insights можно диаграммы метрик, которые не являются tooparticular присоединенные события.</span><span class="sxs-lookup"><span data-stu-id="b61cc-170">Application Insights can chart metrics that are not attached tooparticular events.</span></span> <span data-ttu-id="b61cc-171">Например, можно отслеживать длину очереди через регулярные промежутки времени.</span><span class="sxs-lookup"><span data-stu-id="b61cc-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="b61cc-172">Метрики hello отдельные измерения представляют интерес, меньше, чем hello вариантов и трендов и поэтому статистические диаграммы могут применяться.</span><span class="sxs-lookup"><span data-stu-id="b61cc-172">With metrics, hello individual measurements are of less interest than hello variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="b61cc-173">Порядок toosend метрики аналитики tooApplication, можете воспользоваться hello `TrackMetric(..)` API.</span><span class="sxs-lookup"><span data-stu-id="b61cc-173">In order toosend metrics tooApplication Insights, you can use hello `TrackMetric(..)` API.</span></span> <span data-ttu-id="b61cc-174">Существует два способа toosend метрики:</span><span class="sxs-lookup"><span data-stu-id="b61cc-174">There are two ways toosend a metric:</span></span> 

* <span data-ttu-id="b61cc-175">Отдельное значение.</span><span class="sxs-lookup"><span data-stu-id="b61cc-175">Single value.</span></span> <span data-ttu-id="b61cc-176">Каждый раз при выполнении измерения в приложении, следует отправить соответствующее значение hello tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="b61cc-176">Every time you perform a measurement in your application, you send hello corresponding value tooApplication Insights.</span></span> <span data-ttu-id="b61cc-177">Например пусть метрики, описывающие hello количество элементов в контейнере.</span><span class="sxs-lookup"><span data-stu-id="b61cc-177">For example, assume that you have a metric describing hello number of items in a container.</span></span> <span data-ttu-id="b61cc-178">Во время конкретного периода времени Вначале переведите трех элементов в контейнере hello и затем удалите два элемента.</span><span class="sxs-lookup"><span data-stu-id="b61cc-178">During a particular time period, you first put three items into hello container and then you remove two items.</span></span> <span data-ttu-id="b61cc-179">Соответственно, вызовите `TrackMetric` дважды: сначала при передаче значения hello `3` и затем hello значение `-2`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-179">Accordingly, you would call `TrackMetric` twice: first passing hello value `3` and then hello value `-2`.</span></span> <span data-ttu-id="b61cc-180">Application Insights сохраняет оба значения от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="b61cc-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="b61cc-181">Агрегирование.</span><span class="sxs-lookup"><span data-stu-id="b61cc-181">Aggregation.</span></span> <span data-ttu-id="b61cc-182">При работе с метриками отдельные измерения редко представляют интерес.</span><span class="sxs-lookup"><span data-stu-id="b61cc-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="b61cc-183">Вместо этого обычно важна сводка того, что произошло за определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="b61cc-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="b61cc-184">Такая сводка называется _агрегированием_.</span><span class="sxs-lookup"><span data-stu-id="b61cc-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="b61cc-185">В приведенном выше примере hello, является статистическим выражением суммы метрики hello для этого периода времени `1` и число hello значения метрики hello `2`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-185">In hello above example, hello aggregate metric sum for that time period is `1` and hello count of hello metric values is `2`.</span></span> <span data-ttu-id="b61cc-186">При использовании подхода hello статистической обработки, можно вызвать только `TrackMetric` один раз за время периода и отправить hello статистические значения.</span><span class="sxs-lookup"><span data-stu-id="b61cc-186">When using hello aggregation approach, you only invoke `TrackMetric` once per time period and send hello aggregate values.</span></span> <span data-ttu-id="b61cc-187">Это рекомендованный подход, поскольку он может значительно снизить стоимость hello и производительности издержки, отправляя меньшее количество данных указывает tooApplication аналитики, при сборе вся необходимая информация по-прежнему hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-187">This is hello recommended approach since it can significantly reduce hello cost and performance overhead by sending fewer data points tooApplication Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="b61cc-188">Примеры:</span><span class="sxs-lookup"><span data-stu-id="b61cc-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="b61cc-189">Отдельные значения</span><span class="sxs-lookup"><span data-stu-id="b61cc-189">Single values</span></span>

<span data-ttu-id="b61cc-190">toosend одиночное значение метрики:</span><span class="sxs-lookup"><span data-stu-id="b61cc-190">toosend a single metric value:</span></span>

<span data-ttu-id="b61cc-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b61cc-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="b61cc-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="b61cc-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="b61cc-193">Агрегированные метрики</span><span class="sxs-lookup"><span data-stu-id="b61cc-193">Aggregating metrics</span></span>

<span data-ttu-id="b61cc-194">Рекомендуется перед их отправкой из вашего приложения, tooreduce пропускной способности, производительности, стоимости и tooimprove tooaggregate метрики.</span><span class="sxs-lookup"><span data-stu-id="b61cc-194">It is recommended tooaggregate metrics before sending them from your app, tooreduce bandwidth, cost and tooimprove performance.</span></span>
<span data-ttu-id="b61cc-195">Ниже представлен пример кода для агрегирования.</span><span class="sxs-lookup"><span data-stu-id="b61cc-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="b61cc-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-196">*C#*</span></span>

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
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
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
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
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

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="b61cc-197">Пользовательские метрики в обозревателе метрик</span><span class="sxs-lookup"><span data-stu-id="b61cc-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="b61cc-198">результаты toosee hello, откройте обозреватель метрик и добавить новую диаграмму.</span><span class="sxs-lookup"><span data-stu-id="b61cc-198">toosee hello results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="b61cc-199">Изменение диаграммы tooshow hello вашей метрики.</span><span class="sxs-lookup"><span data-stu-id="b61cc-199">Edit hello chart tooshow your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="b61cc-200">В списке доступных метрик hello вашей пользовательской метрики может занять несколько минут tooappear.</span><span class="sxs-lookup"><span data-stu-id="b61cc-200">Your custom metric might take several minutes tooappear in hello list of available metrics.</span></span>
>

![Добавьте новую диаграмму или выберите существующую, а в поле Custom (Пользовательские) выберите свою метрику](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="b61cc-202">Настраиваемые метрики в аналитике</span><span class="sxs-lookup"><span data-stu-id="b61cc-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="b61cc-203">Hello телеметрии доступен в hello `customMetrics` в таблицу [приложения аналитика Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="b61cc-203">hello telemetry is available in hello `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="b61cc-204">Каждая строка представляет вызов слишком`trackMetric(..)` в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="b61cc-204">Each row represents a call too`trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="b61cc-205">`valueSum`— Это сумма hello hello измерений.</span><span class="sxs-lookup"><span data-stu-id="b61cc-205">`valueSum` - This is hello sum of hello measurements.</span></span> <span data-ttu-id="b61cc-206">Среднее значение hello tooget, деление на `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-206">tooget hello mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="b61cc-207">`valueCount`-hello число измерений, которые были сведены в это `trackMetric(..)` вызова.</span><span class="sxs-lookup"><span data-stu-id="b61cc-207">`valueCount` - hello number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="b61cc-208">Просмотры страниц</span><span class="sxs-lookup"><span data-stu-id="b61cc-208">Page views</span></span>
<span data-ttu-id="b61cc-209">В устройстве или приложении веб-страницы телеметрия просмотров страницы отображается по умолчанию при загрузке каждого экрана или страницы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="b61cc-210">Однако можно изменить, представления страниц tootrack время дополнительные или другие.</span><span class="sxs-lookup"><span data-stu-id="b61cc-210">But you can change that tootrack page views at additional or different times.</span></span> <span data-ttu-id="b61cc-211">Например приложение, которое отображает вкладки или колонок, может потребоваться tootrack страницы всякий раз, когда пользователь hello открывается новая колонка.</span><span class="sxs-lookup"><span data-stu-id="b61cc-211">For example, in an app that displays tabs or blades, you might want tootrack a page whenever hello user opens a new blade.</span></span>

![Область "Использование" в колонке "Обзор"](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="b61cc-213">Данные пользователя и сеанса отправляется как свойства вместе с просмотров страниц, поэтому hello пользователей и сеансов диаграммы поступать в активном состоянии при отсутствии телеметрии просмотров страниц.</span><span class="sxs-lookup"><span data-stu-id="b61cc-213">User and session data is sent as properties along with page views, so hello user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="b61cc-214">Пользовательские данные о просмотре страницы</span><span class="sxs-lookup"><span data-stu-id="b61cc-214">Custom page views</span></span>
<span data-ttu-id="b61cc-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b61cc-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="b61cc-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="b61cc-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b61cc-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="b61cc-218">При наличии нескольких вкладок в разных HTML-страницы, можно указать URL-адрес hello слишком:</span><span class="sxs-lookup"><span data-stu-id="b61cc-218">If you have several tabs within different HTML pages, you can specify hello URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="b61cc-219">Время просмотра страниц</span><span class="sxs-lookup"><span data-stu-id="b61cc-219">Timing page views</span></span>
<span data-ttu-id="b61cc-220">По умолчанию hello раз отмечено как **время загрузки страницы** отсчитываются от при hello браузер отправляет запрос hello, пока не будет вызван события загрузки страницы браузера hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-220">By default, hello times reported as **Page view load time** are measured from when hello browser sends hello request, until hello browser's page load event is called.</span></span>

<span data-ttu-id="b61cc-221">Вместо этого вы можете выбрать один из таких вариантов:</span><span class="sxs-lookup"><span data-stu-id="b61cc-221">Instead, you can either:</span></span>

* <span data-ttu-id="b61cc-222">Задать явные длительность в hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) вызова: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-222">Set an explicit duration in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="b61cc-223">Использовать вызовы времени представление страницы приветствия `startTrackPage` и `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-223">Use hello page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="b61cc-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b61cc-224">*JavaScript*</span></span>

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="b61cc-225">...</span><span class="sxs-lookup"><span data-stu-id="b61cc-225">...</span></span>

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="b61cc-226">Здравствуйте, имя, которое используется как первый параметр hello связывает hello запуска и остановки вызовы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-226">hello name that you use as hello first parameter associates hello start and stop calls.</span></span> <span data-ttu-id="b61cc-227">По умолчанию toohello имени текущей страницы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-227">It defaults toohello current page name.</span></span>

<span data-ttu-id="b61cc-228">Hello длительности, отображаемых в обозревателе метрик являются производными от hello интервал между hello полученный загрузки страницы, запускать и останавливать вызовов.</span><span class="sxs-lookup"><span data-stu-id="b61cc-228">hello resulting page load durations displayed in Metrics Explorer are derived from hello interval between hello start and stop calls.</span></span> <span data-ttu-id="b61cc-229">Он работает tooyou какие интервал фактически времени.</span><span class="sxs-lookup"><span data-stu-id="b61cc-229">It's up tooyou what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="b61cc-230">Телеметрия страниц в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="b61cc-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="b61cc-231">В [службе аналитики](app-insights-analytics.md) две таблицы содержат данные по операциям в браузере.</span><span class="sxs-lookup"><span data-stu-id="b61cc-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="b61cc-232">Hello `pageViews` таблица содержит данные о hello URL-адрес и заголовок страницы</span><span class="sxs-lookup"><span data-stu-id="b61cc-232">hello `pageViews` table contains data about hello URL and page title</span></span>
* <span data-ttu-id="b61cc-233">Hello `browserTimings` таблице содержатся данные о производительности клиента, такие как время, затраченное tooprocess hello hello входящих данных</span><span class="sxs-lookup"><span data-stu-id="b61cc-233">hello `browserTimings` table contains data about client performance, such as hello time taken tooprocess hello incoming data</span></span>

<span data-ttu-id="b61cc-234">toofind как долго браузера hello принимает tooprocess различные страницы:</span><span class="sxs-lookup"><span data-stu-id="b61cc-234">toofind how long hello browser takes tooprocess different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="b61cc-235">toodiscover popularities hello различных браузеров:</span><span class="sxs-lookup"><span data-stu-id="b61cc-235">toodiscover hello popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="b61cc-236">tooassociate представления tooAJAX обращениями к страницам, соединения с зависимостями:</span><span class="sxs-lookup"><span data-stu-id="b61cc-236">tooassociate page views tooAJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="b61cc-237">TrackRequest (Отслеживание запросов)</span><span class="sxs-lookup"><span data-stu-id="b61cc-237">TrackRequest</span></span>
<span data-ttu-id="b61cc-238">сервер Hello SDK использует TrackRequest toolog HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="b61cc-238">hello server SDK uses TrackRequest toolog HTTP requests.</span></span>

<span data-ttu-id="b61cc-239">Можно также вызвать ее самостоятельно Если требуется toosimulate запросы в контексте, где отсутствует служба модуля hello web работает.</span><span class="sxs-lookup"><span data-stu-id="b61cc-239">You can also call it yourself if you want toosimulate requests in a context where you don't have hello web service module running.</span></span>

<span data-ttu-id="b61cc-240">Однако рекомендуется использовать hello телеметрии запроса toosend способом — где hello запрос выступает в качестве <a href="#operation-context">контекст операции</a>.</span><span class="sxs-lookup"><span data-stu-id="b61cc-240">However, hello recommended way toosend request telemetry is where hello request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="b61cc-241">Контекст операции</span><span class="sxs-lookup"><span data-stu-id="b61cc-241">Operation context</span></span>
<span data-ttu-id="b61cc-242">Можно связать элементы телеметрии путем присоединения toothem общие идентификатором операции.</span><span class="sxs-lookup"><span data-stu-id="b61cc-242">You can associate telemetry items together by attaching toothem a common operation ID.</span></span> <span data-ttu-id="b61cc-243">стандартный модуль отслеживания запроса Hello делает это для исключения и другие события, которые отправляются во время обработки HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="b61cc-243">hello standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="b61cc-244">В [поиска](app-insights-diagnostic-search.md) и [Analytics](app-insights-analytics.md), можно использовать поиск tooeasily идентификатор hello все события, связанные с запросом hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use hello ID tooeasily find any events associated with hello request.</span></span>

<span data-ttu-id="b61cc-245">Hello простым способом tooset hello идентификатор — tooset контекст операции с помощью этого шаблона:</span><span class="sxs-lookup"><span data-stu-id="b61cc-245">hello easiest way tooset hello ID is tooset an operation context by using this pattern:</span></span>

<span data-ttu-id="b61cc-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="b61cc-247">Вместе с установкой контекст операции `StartOperation` создает элемент телеметрии указанного типа hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-247">Along with setting an operation context, `StartOperation` creates a telemetry item of hello type that you specify.</span></span> <span data-ttu-id="b61cc-248">Он отправляет данные телеметрии hello элементов при реализации операции hello, или если явным образом вызвать `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-248">It sends hello telemetry item when you dispose hello operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="b61cc-249">Если вы используете `RequestTelemetry` как тип телеметрии hello, его длительность устанавливается интервал toohello истекло время ожидания между start и stop.</span><span class="sxs-lookup"><span data-stu-id="b61cc-249">If you use `RequestTelemetry` as hello telemetry type, its duration is set toohello timed interval between start and stop.</span></span>

<span data-ttu-id="b61cc-250">Контексты операции не могут быть вложенными.</span><span class="sxs-lookup"><span data-stu-id="b61cc-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="b61cc-251">Если уже контекст операции, то его идентификатор связан с все hello содержатся элементы, включая hello элемент, созданный с `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-251">If there is already an operation context, then its ID is associated with all hello contained items, including hello item created with `StartOperation`.</span></span>

<span data-ttu-id="b61cc-252">В поле поиска контекст операции hello — hello используется toocreate **связанные элементы** списка:</span><span class="sxs-lookup"><span data-stu-id="b61cc-252">In Search, hello operation context is used toocreate hello **Related Items** list:</span></span>

![Связанные элементы](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="b61cc-254">Дополнительные сведения об отслеживании пользовательских операций см. в разделе [application-insights-custom-operations-tracking.md].</span><span class="sxs-lookup"><span data-stu-id="b61cc-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="b61cc-255">Запросы в аналитике</span><span class="sxs-lookup"><span data-stu-id="b61cc-255">Requests in Analytics</span></span> 

<span data-ttu-id="b61cc-256">В [приложения аналитика Analytics](app-insights-analytics.md), запрашивает Показать вверх в hello `requests` таблицы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in hello `requests` table.</span></span>

<span data-ttu-id="b61cc-257">Если [выборки](app-insights-sampling.md) — в операции, свойство itemCount hello покажет значение больше 1.</span><span class="sxs-lookup"><span data-stu-id="b61cc-257">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="b61cc-258">Для примера itemCount == 10 означает, что из tootrackRequest() 10 вызовов hello выборки процесса передаются только один из них.</span><span class="sxs-lookup"><span data-stu-id="b61cc-258">For example itemCount==10 means that of 10 calls tootrackRequest(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="b61cc-259">tooget правильного числа запросов, а Средняя длительность, разбитых на имена запроса, можно использовать следующий код:</span><span class="sxs-lookup"><span data-stu-id="b61cc-259">tooget a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="b61cc-260">TrackException (Отслеживание исключений)</span><span class="sxs-lookup"><span data-stu-id="b61cc-260">TrackException</span></span>
<span data-ttu-id="b61cc-261">Отправьте аналитики tooApplication исключения:</span><span class="sxs-lookup"><span data-stu-id="b61cc-261">Send exceptions tooApplication Insights:</span></span>

* <span data-ttu-id="b61cc-262">слишком[их](app-insights-metrics-explorer.md), как показатель частоты hello проблемы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-262">too[count them](app-insights-metrics-explorer.md), as an indication of hello frequency of a problem.</span></span>
* <span data-ttu-id="b61cc-263">слишком[проверьте отдельные копии](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b61cc-263">too[examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="b61cc-264">Hello отчеты включают hello трассировки стека.</span><span class="sxs-lookup"><span data-stu-id="b61cc-264">hello reports include hello stack traces.</span></span>

<span data-ttu-id="b61cc-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="b61cc-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b61cc-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="b61cc-267">пакеты SDK Hello перехватывать исключения, многие автоматически, поэтому не всегда нужно toocall TrackException явным образом.</span><span class="sxs-lookup"><span data-stu-id="b61cc-267">hello SDKs catch many exceptions automatically, so you don't always have toocall TrackException explicitly.</span></span>

* <span data-ttu-id="b61cc-268">ASP.NET: [писать код исключения toocatch](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="b61cc-268">ASP.NET: [Write code toocatch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="b61cc-269">J2EE: [исключения перехватываются автоматически](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="b61cc-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="b61cc-270">JavaScript: исключения перехватываются автоматически.</span><span class="sxs-lookup"><span data-stu-id="b61cc-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="b61cc-271">Если вы хотите toodisable автоматический сбор сведений, добавьте фрагмента кода toohello строки, которые можно вставить в веб-страницы:</span><span class="sxs-lookup"><span data-stu-id="b61cc-271">If you want toodisable automatic collection, add a line toohello code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="b61cc-272">Исключения в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="b61cc-272">Exceptions in Analytics</span></span>

<span data-ttu-id="b61cc-273">В [приложения аналитика Analytics](app-insights-analytics.md), отображаются в hello исключения `exceptions` таблицы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in hello `exceptions` table.</span></span>

<span data-ttu-id="b61cc-274">Если [выборки](app-insights-sampling.md) — в операции hello `itemCount` свойств отображается значение больше 1.</span><span class="sxs-lookup"><span data-stu-id="b61cc-274">If [sampling](app-insights-sampling.md) is in operation, hello `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="b61cc-275">Для примера itemCount == 10 означает, что из tootrackException() 10 вызовов hello выборки процесса передаются только один из них.</span><span class="sxs-lookup"><span data-stu-id="b61cc-275">For example itemCount==10 means that of 10 calls tootrackException(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="b61cc-276">tooget правильное число исключений, разбитых на тип исключения, можно использовать следующий код:</span><span class="sxs-lookup"><span data-stu-id="b61cc-276">tooget a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="b61cc-277">Большинство важных сведений стека уже извлеченные в отдельные переменные, но вы можете извлечь друг от друга hello hello `details` дополнительные tooget структуры.</span><span class="sxs-lookup"><span data-stu-id="b61cc-277">Most of hello important stack information is already extracted into separate variables, but you can pull apart hello `details` structure tooget more.</span></span> <span data-ttu-id="b61cc-278">Так как эта структура является динамическим, необходимо привести тип результата toohello hello, ожидаемых.</span><span class="sxs-lookup"><span data-stu-id="b61cc-278">Since this structure is dynamic, you should cast hello result toohello type you expect.</span></span> <span data-ttu-id="b61cc-279">Например:</span><span class="sxs-lookup"><span data-stu-id="b61cc-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="b61cc-280">исключения tooassociate с их связанные запросы соединения:</span><span class="sxs-lookup"><span data-stu-id="b61cc-280">tooassociate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="b61cc-281">TrackTrace (Отслеживание трассировки)</span><span class="sxs-lookup"><span data-stu-id="b61cc-281">TrackTrace</span></span>
<span data-ttu-id="b61cc-282">Используйте TrackTrace toohelp диагностики проблем, отправляя tooApplication «цепочка навигации» дополнительная информация.</span><span class="sxs-lookup"><span data-stu-id="b61cc-282">Use TrackTrace toohelp diagnose problems by sending a "breadcrumb trail" tooApplication Insights.</span></span> <span data-ttu-id="b61cc-283">Вы можете отправлять блоки диагностических данных и проверять их с помощью [поиска по журналу диагностики](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b61cc-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="b61cc-284">[Журнал адаптеров](app-insights-asp-net-trace-logs.md) использовать этот портал toohello журналы сторонних toosend API.</span><span class="sxs-lookup"><span data-stu-id="b61cc-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API toosend third-party logs toohello portal.</span></span>

<span data-ttu-id="b61cc-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="b61cc-286">Вы можете выполнять поиск содержимого сообщения, но (в отличие от значений свойств) не можете фильтровать его.</span><span class="sxs-lookup"><span data-stu-id="b61cc-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="b61cc-287">ограничения на размер Hello `message` гораздо выше, чем максимально hello свойства.</span><span class="sxs-lookup"><span data-stu-id="b61cc-287">hello size limit on `message` is much higher than hello limit on properties.</span></span>
<span data-ttu-id="b61cc-288">Преимуществом TrackTrace является относительно большие объемы данных можно поместить в сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-288">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="b61cc-289">например данных POST.</span><span class="sxs-lookup"><span data-stu-id="b61cc-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="b61cc-290">Кроме того можно добавить сообщение tooyour уровня серьезности.</span><span class="sxs-lookup"><span data-stu-id="b61cc-290">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="b61cc-291">И, как и другие данные телеметрии, вы можете добавить toohelp значения свойств, фильтровать или поиска для разных наборов трассировок.</span><span class="sxs-lookup"><span data-stu-id="b61cc-291">And, like other telemetry, you can add property values toohelp you filter or search for different sets of traces.</span></span> <span data-ttu-id="b61cc-292">Например:</span><span class="sxs-lookup"><span data-stu-id="b61cc-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="b61cc-293">В [поиска](app-insights-diagnostic-search.md), можно затем легко отфильтровать все сообщения hello уровня серьезности конкретного, относящиеся tooa определенной базы данных.</span><span class="sxs-lookup"><span data-stu-id="b61cc-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all hello messages of a particular severity level that relate tooa particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="b61cc-294">Трассировки в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="b61cc-294">Traces in Analytics</span></span>

<span data-ttu-id="b61cc-295">В [приложения аналитика Analytics](app-insights-analytics.md), звонит tooTrackTrace Показать hello `traces` таблицы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-295">In [Application Insights Analytics](app-insights-analytics.md), calls tooTrackTrace show up in hello `traces` table.</span></span>

<span data-ttu-id="b61cc-296">Если [выборки](app-insights-sampling.md) находится в операции, свойство itemCount hello показывает значение больше 1.</span><span class="sxs-lookup"><span data-stu-id="b61cc-296">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="b61cc-297">Для примера itemCount == 10 означает, что 10 вызывает слишком`trackTrace()`, процесс выборки hello передаются только в одной из них.</span><span class="sxs-lookup"><span data-stu-id="b61cc-297">For example itemCount==10 means that of 10 calls too`trackTrace()`, hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="b61cc-298">tooget правильного числа вызовов трассировки, следует использовать таким образом кода например `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-298">tooget a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="b61cc-299">TrackDependency (Отслеживание зависимостей)</span><span class="sxs-lookup"><span data-stu-id="b61cc-299">TrackDependency</span></span>
<span data-ttu-id="b61cc-300">Используйте hello TrackDependency вызовите tootrack hello отклика и частоты успешных вызовов tooan внешним фрагментам кода.</span><span class="sxs-lookup"><span data-stu-id="b61cc-300">Use hello TrackDependency call tootrack hello response times and success rates of calls tooan external piece of code.</span></span> <span data-ttu-id="b61cc-301">Hello результаты отображаются в форме диаграммы зависимости hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="b61cc-301">hello results appear in hello dependency charts in hello portal.</span></span>

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

<span data-ttu-id="b61cc-302">Помните, сервера hello, пакеты SDK включают [зависимостей модуля](app-insights-asp-net-dependencies.md) , обнаруживает и отслеживает определенные вызовы зависимостей автоматически — например, toodatabases и API-интерфейсов REST.</span><span class="sxs-lookup"><span data-stu-id="b61cc-302">Remember that hello server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, toodatabases and REST APIs.</span></span> <span data-ttu-id="b61cc-303">У вас есть tooinstall агент на модуле hello server toomake работы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-303">You have tooinstall an agent on your server toomake hello module work.</span></span> <span data-ttu-id="b61cc-304">Используйте этот вызов не перехватывать вызовы tootrack, hello автоматического отслеживания, или если вы не хотите tooinstall hello агента.</span><span class="sxs-lookup"><span data-stu-id="b61cc-304">You use this call if you want tootrack calls that hello automated tracking doesn't catch, or if you don't want tooinstall hello agent.</span></span>

<span data-ttu-id="b61cc-305">изменить tooturn off hello стандартного модуля Отслеживание зависимостей, [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) и удалить ссылку hello слишком`DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-305">tooturn off hello standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete hello reference too`DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="b61cc-306">Зависимости в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="b61cc-306">Dependencies in Analytics</span></span>

<span data-ttu-id="b61cc-307">В [приложения аналитика Analytics](app-insights-analytics.md), trackDependency вызовы отображаются в hello `dependencies` таблицы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in hello `dependencies` table.</span></span>

<span data-ttu-id="b61cc-308">Если [выборки](app-insights-sampling.md) находится в операции, свойство itemCount hello показывает значение больше 1.</span><span class="sxs-lookup"><span data-stu-id="b61cc-308">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="b61cc-309">Для примера itemCount == 10 означает, что из tootrackDependency() 10 вызовов hello выборки процесса передаются только один из них.</span><span class="sxs-lookup"><span data-stu-id="b61cc-309">For example itemCount==10 means that of 10 calls tootrackDependency(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="b61cc-310">tooget правильное количество зависимостей, разбитых на целевого компонента, можно использовать следующий код:</span><span class="sxs-lookup"><span data-stu-id="b61cc-310">tooget a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="b61cc-311">зависимости tooassociate с их связанные запросы соединения:</span><span class="sxs-lookup"><span data-stu-id="b61cc-311">tooassociate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="b61cc-312">Очистка данных</span><span class="sxs-lookup"><span data-stu-id="b61cc-312">Flushing data</span></span>
<span data-ttu-id="b61cc-313">Как правило hello SDK отправляет данные, в некоторых случаях выбрана toominimize hello влияние на пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-313">Normally, hello SDK sends data at times chosen toominimize hello impact on hello user.</span></span> <span data-ttu-id="b61cc-314">Однако в некоторых случаях может потребоваться tooflush hello буфера — например, при использовании hello SDK в приложении, которое завершает работу.</span><span class="sxs-lookup"><span data-stu-id="b61cc-314">However, in some cases, you might want tooflush hello buffer--for example, if you are using hello SDK in an application that shuts down.</span></span>

<span data-ttu-id="b61cc-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="b61cc-316">Обратите внимание, что функции hello асинхронной для hello [телеметрии канала сервера](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="b61cc-316">Note that hello function is asynchronous for hello [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="b61cc-317">Прошедшие проверку пользователи</span><span class="sxs-lookup"><span data-stu-id="b61cc-317">Authenticated users</span></span>
<span data-ttu-id="b61cc-318">В веб-приложении пользователи по умолчанию идентифицируются файлами cookie.</span><span class="sxs-lookup"><span data-stu-id="b61cc-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="b61cc-319">Пользователь может быть учтен более одного раза при доступе к приложению с другого компьютера или браузера либо при удалении файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="b61cc-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="b61cc-320">Если пользователи входят в приложении tooyour, можно получить более точный подсчет, установив идентификатор пользователя с проверкой подлинности hello в коде hello браузера:</span><span class="sxs-lookup"><span data-stu-id="b61cc-320">If users sign in tooyour app, you can get a more accurate count by setting hello authenticated user ID in hello browser code:</span></span>

<span data-ttu-id="b61cc-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b61cc-321">*JavaScript*</span></span>

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="b61cc-322">Например, в веб-приложении MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b61cc-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="b61cc-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="b61cc-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="b61cc-324">Это не значит необходимые toouse hello фактическое учетное имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="b61cc-324">It isn't necessary toouse hello user's actual sign-in name.</span></span> <span data-ttu-id="b61cc-325">Он имеет только toobe идентификатор, уникальный toothat пользователя.</span><span class="sxs-lookup"><span data-stu-id="b61cc-325">It only has toobe an ID that is unique toothat user.</span></span> <span data-ttu-id="b61cc-326">Он не должен содержать пробелы или знаки hello `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-326">It must not include spaces or any of hello characters `,;=|`.</span></span>

<span data-ttu-id="b61cc-327">Идентификатор пользователя Hello также задать в файле cookie сеанса и отправки toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="b61cc-327">hello user ID is also set in a session cookie and sent toohello server.</span></span> <span data-ttu-id="b61cc-328">Если установлен SDK сервера hello, hello проверку подлинности пользователя, которого код отправляется как часть свойств контекста hello телеметрии клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="b61cc-328">If hello server SDK is installed, hello authenticated user ID is sent as part of hello context properties of both client and server telemetry.</span></span> <span data-ttu-id="b61cc-329">Затем можно выполнить фильтрацию и поиск.</span><span class="sxs-lookup"><span data-stu-id="b61cc-329">You can then filter and search on it.</span></span>

<span data-ttu-id="b61cc-330">Приложения в учетные записи групп пользователей можно также передать идентификатор учетной записи hello (с hello же ограничения на символы).</span><span class="sxs-lookup"><span data-stu-id="b61cc-330">If your app groups users into accounts, you can also pass an identifier for hello account (with hello same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="b61cc-331">В [обозревателе метрик](app-insights-metrics-explorer.md) можно создать диаграмму для отображения количества **пользователей, прошедших проверку подлинности**, а также **учетных записей пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b61cc-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="b61cc-332">Кроме того, можно [выполнить поиск](app-insights-diagnostic-search.md) точек данных клиентов с определенными именами пользователей и учетными записями.</span><span class="sxs-lookup"><span data-stu-id="b61cc-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="b61cc-333"><a name="properties"></a>Фильтрация, поиск и сегментация данных с помощью свойств</span><span class="sxs-lookup"><span data-stu-id="b61cc-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="b61cc-334">Можно присоединить измерениях и свойства tooyour событий (и также toometrics, представления страниц, исключения и другие данные телеметрии).</span><span class="sxs-lookup"><span data-stu-id="b61cc-334">You can attach properties and measurements tooyour events (and also toometrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="b61cc-335">*Свойства* представляют собой строковые значения, которые используются toofilter телеметрии в отчетах об использовании hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-335">*Properties* are string values that you can use toofilter your telemetry in hello usage reports.</span></span> <span data-ttu-id="b61cc-336">Например если ваше приложение предоставляет несколько игр, можно присоединить hello имя события игры tooeach hello, можно увидеть, какие игры популярные.</span><span class="sxs-lookup"><span data-stu-id="b61cc-336">For example, if your app provides several games, you can attach hello name of hello game tooeach event so that you can see which games are more popular.</span></span>

<span data-ttu-id="b61cc-337">Имеется ограничение в 8192 hello длина строки.</span><span class="sxs-lookup"><span data-stu-id="b61cc-337">There's a limit of 8192 on hello string length.</span></span> <span data-ttu-id="b61cc-338">(Если вы хотите toosend больших объемов данных, используйте параметр сообщение hello [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="b61cc-338">(If you want toosend large chunks of data, use hello message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="b61cc-339">*Метрики* являются числовыми значениями, которые могут быть представлены в графическом виде.</span><span class="sxs-lookup"><span data-stu-id="b61cc-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="b61cc-340">Например может потребоваться toosee при наличии постепенное увеличение hello оценки, которые достижения вашего игр.</span><span class="sxs-lookup"><span data-stu-id="b61cc-340">For example, you might want toosee if there's a gradual increase in hello scores that your gamers achieve.</span></span> <span data-ttu-id="b61cc-341">Hello диаграмм сегментации отдельные свойства, которые отправляются с событием hello, чтобы вы могли получить приветствия или с накоплением графики для различных игр.</span><span class="sxs-lookup"><span data-stu-id="b61cc-341">hello graphs can be segmented by hello properties that are sent with hello event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="b61cc-342">Для значения метрики toobe правильно отображается они должны быть больше или равно too0.</span><span class="sxs-lookup"><span data-stu-id="b61cc-342">For metric values toobe correctly displayed, they should be greater than or equal too0.</span></span>

<span data-ttu-id="b61cc-343">Некоторые [ограничения на число свойств, значений свойств и показатели hello](#limits) , который можно использовать.</span><span class="sxs-lookup"><span data-stu-id="b61cc-343">There are some [limits on hello number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="b61cc-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b61cc-344">*JavaScript*</span></span>

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


<span data-ttu-id="b61cc-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="b61cc-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b61cc-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="b61cc-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="b61cc-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="b61cc-348">Будьте внимательны toolog не личные сведения в свойствах.</span><span class="sxs-lookup"><span data-stu-id="b61cc-348">Take care not toolog personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="b61cc-349">*При использовании метрик*выберите hello метрики из hello, откройте обозреватель метрик **настраиваемый** группы:</span><span class="sxs-lookup"><span data-stu-id="b61cc-349">*If you used metrics*, open Metrics Explorer and select hello metric from hello **Custom** group:</span></span>

![Откройте обозреватель метрик, диаграммы выберите hello и выберите метрики hello](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="b61cc-351">Если ваш метрики отсутствует или hello **настраиваемый** заголовок колонки выбора закрыть hello не существует и повторите попытку позже.</span><span class="sxs-lookup"><span data-stu-id="b61cc-351">If your metric doesn't appear, or if hello **Custom** heading isn't there, close hello selection blade and try again later.</span></span> <span data-ttu-id="b61cc-352">Метрики иногда может занять один час toobe статистическую обработку через конвейер hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-352">Metrics can sometimes take an hour toobe aggregated through hello pipeline.</span></span>

<span data-ttu-id="b61cc-353">*При использовании свойств и метрики*, сегмент метрика hello свойством hello:</span><span class="sxs-lookup"><span data-stu-id="b61cc-353">*If you used properties and metrics*, segment hello metric by hello property:</span></span>

![Задать группирования, а затем выберите свойство hello в списке Group by](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="b61cc-355">*В поиске диагностики*, можно просмотреть свойства hello и метриках отдельные вхождения события.</span><span class="sxs-lookup"><span data-stu-id="b61cc-355">*In Diagnostic Search*, you can view hello properties and metrics of individual occurrences of an event.</span></span>

![Выберите экземпляр, а затем выберите "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="b61cc-357">Используйте hello **поиска** поле toosee вхождений событий, имеющих определенное значение свойства.</span><span class="sxs-lookup"><span data-stu-id="b61cc-357">Use hello **Search** field toosee event occurrences that have a particular property value.</span></span>

![Введите слово в поле поиска](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="b61cc-359">[Дополнительные сведения о выражениях поиска.](app-insights-diagnostic-search.md)</span><span class="sxs-lookup"><span data-stu-id="b61cc-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-tooset-properties-and-metrics"></a><span data-ttu-id="b61cc-360">Альтернативный способ tooset свойства и метрики</span><span class="sxs-lookup"><span data-stu-id="b61cc-360">Alternative way tooset properties and metrics</span></span>
<span data-ttu-id="b61cc-361">Если он является более удобным, можно собирать параметров hello события в отдельном объекте:</span><span class="sxs-lookup"><span data-stu-id="b61cc-361">If it's more convenient, you can collect hello parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="b61cc-362">Не используйте hello того же экземпляра элемента телеметрии (`event` в этом примере) toocall Track*() несколько раз.</span><span class="sxs-lookup"><span data-stu-id="b61cc-362">Don't reuse hello same telemetry item instance (`event` in this example) toocall Track*() multiple times.</span></span> <span data-ttu-id="b61cc-363">Это может привести к toobe телеметрии, отправленные с неправильной конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="b61cc-363">This may cause telemetry toobe sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="b61cc-364">Пользовательские измерения и свойства в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="b61cc-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="b61cc-365">В [Analytics](app-insights-analytics.md), настраиваемых метрик и свойства отображаются в hello `customMeasurements` и `customDimensions` атрибуты каждой записи телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b61cc-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in hello `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="b61cc-366">Например при добавлении свойства с именем «игры» tooyour телеметрии запроса этот запрос подсчитывающей hello различных значений «игра» и Показать среднее hello hello пользовательские метрики «оценка»:</span><span class="sxs-lookup"><span data-stu-id="b61cc-366">For example, if you have added a property named "game" tooyour request telemetry, this query counts hello occurrences of different values of "game", and show hello average of hello custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="b61cc-367">Обратите внимание на указанные ниже моменты.</span><span class="sxs-lookup"><span data-stu-id="b61cc-367">Notice that:</span></span>

* <span data-ttu-id="b61cc-368">При извлечении значения из hello customDimensions или customMeasurements JSON имеет динамический тип и поэтому необходимо привести `tostring` или `todouble`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-368">When you extract a value from hello customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="b61cc-369">Учетная запись tootake вероятность hello [выборки](app-insights-sampling.md), следует использовать `sum(itemCount)`, а не `count()`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-369">tootake account of hello possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="b61cc-370"><a name="timed"></a> События времени</span><span class="sxs-lookup"><span data-stu-id="b61cc-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="b61cc-371">Иногда требуется toochart понадобившееся tooperform действие.</span><span class="sxs-lookup"><span data-stu-id="b61cc-371">Sometimes you want toochart how long it takes tooperform an action.</span></span> <span data-ttu-id="b61cc-372">Например, может потребоваться tooknow как долго выполнять пользователи tooconsider вариантов в игру.</span><span class="sxs-lookup"><span data-stu-id="b61cc-372">For example, you might want tooknow how long users take tooconsider choices in a game.</span></span> <span data-ttu-id="b61cc-373">Для этого можно использовать параметр измерения hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-373">You can use hello measurement parameter for this.</span></span>

<span data-ttu-id="b61cc-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="b61cc-375"><a name="defaults"></a>Свойства по умолчанию для настраиваемой телеметрии</span><span class="sxs-lookup"><span data-stu-id="b61cc-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="b61cc-376">Если требуется tooset значения свойств по умолчанию для некоторых hello пользовательских событий, которые пишутся, можно установить их на экземпляр TelemetryClient.</span><span class="sxs-lookup"><span data-stu-id="b61cc-376">If you want tooset default property values for some of hello custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="b61cc-377">Они представляют подключенных tooevery телеметрии элементов, отправляемых с клиента.</span><span class="sxs-lookup"><span data-stu-id="b61cc-377">They are attached tooevery telemetry item that's sent from that client.</span></span>

<span data-ttu-id="b61cc-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="b61cc-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b61cc-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="b61cc-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="b61cc-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="b61cc-381">Вызовы отдельных телеметрии можно переопределить значения по умолчанию hello в словарях их свойства.</span><span class="sxs-lookup"><span data-stu-id="b61cc-381">Individual telemetry calls can override hello default values in their property dictionaries.</span></span>

<span data-ttu-id="b61cc-382">*Для веб-клиентов JavaScript*[используйте инициализаторы телеметрии JavaScript](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="b61cc-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="b61cc-383">*Данные телеметрии tooall свойства tooadd*, включая hello данные из стандартной коллекции модулей, [реализовать `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="b61cc-383">*tooadd properties tooall telemetry*, including hello data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="b61cc-384">Выборка, фильтрация и обработка данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="b61cc-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="b61cc-385">Можно написать код tooprocess телеметрии перед отправкой из пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-385">You can write code tooprocess your telemetry before it's sent from hello SDK.</span></span> <span data-ttu-id="b61cc-386">Обработка Hello включает в себя данные, отправленные из модулей стандартной телеметрии hello, например коллекции запроса HTTP и коллекция зависимостей.</span><span class="sxs-lookup"><span data-stu-id="b61cc-386">hello processing includes data that's sent from hello standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="b61cc-387">[Добавить свойства](app-insights-api-filtering-sampling.md#add-properties) tootelemetry путем реализации `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) tootelemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="b61cc-388">Например, можно добавить номера версий или значения, вычисленные на основе других свойств.</span><span class="sxs-lookup"><span data-stu-id="b61cc-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="b61cc-389">[Фильтрация](app-insights-api-filtering-sampling.md#filtering) можно изменить или отменить телеметрии перед отправкой из пакета SDK для hello путем реализации `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="b61cc-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from hello SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="b61cc-390">Управлять что отправлено или удалены, но у tooaccount для hello влияет на показатели.</span><span class="sxs-lookup"><span data-stu-id="b61cc-390">You control what is sent or discarded, but you have tooaccount for hello effect on your metrics.</span></span> <span data-ttu-id="b61cc-391">В зависимости от того, каким образом удалить элементы то можно потерять toonavigate возможность hello между связанных элементов.</span><span class="sxs-lookup"><span data-stu-id="b61cc-391">Depending on how you discard items, you might lose hello ability toonavigate between related items.</span></span>

<span data-ttu-id="b61cc-392">[Выборка](app-insights-api-filtering-sampling.md) является упакованных решения tooreduce hello объем данных, передаваемых через портал toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="b61cc-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution tooreduce hello volume of data that's sent from your app toohello portal.</span></span> <span data-ttu-id="b61cc-393">Это происходит не затрагивая hello отображаются метрики.</span><span class="sxs-lookup"><span data-stu-id="b61cc-393">It does so without affecting hello displayed metrics.</span></span> <span data-ttu-id="b61cc-394">И это делается без влияния на ваши возможности toodiagnose проблемы с помощью перехода между элементами, такими как исключения, запросы и представления страницы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-394">And it does so without affecting your ability toodiagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="b61cc-395">[Подробнее](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="b61cc-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="b61cc-396">Отключение телеметрии</span><span class="sxs-lookup"><span data-stu-id="b61cc-396">Disabling telemetry</span></span>
<span data-ttu-id="b61cc-397">слишком*динамически остановить и запустить* hello сбор и передача данных телеметрии:</span><span class="sxs-lookup"><span data-stu-id="b61cc-397">too*dynamically stop and start* hello collection and transmission of telemetry:</span></span>

<span data-ttu-id="b61cc-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="b61cc-399">слишком*отключить выбранный Стандартная сборщики*— например, счетчики производительности, HTTP-запросы или зависимости — удалите или закомментируйте hello соответствующих строк в [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Это можно сделать, например, если требуется toosend TrackRequest данных.</span><span class="sxs-lookup"><span data-stu-id="b61cc-399">too*disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <span data-ttu-id="b61cc-400"><a name="debug"></a>Режим разработчика</span><span class="sxs-lookup"><span data-stu-id="b61cc-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="b61cc-401">Во время отладки, бывает полезно toohave телеметрии ускорено через конвейер hello, так что можно сразу же увидеть результаты.</span><span class="sxs-lookup"><span data-stu-id="b61cc-401">During debugging, it's useful toohave your telemetry expedited through hello pipeline so that you can see results immediately.</span></span> <span data-ttu-id="b61cc-402">Можно также получить дополнительные сообщения, которые помогают трассировку проблемах, связанных с телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-402">You also get additional messages that help you trace any problems with hello telemetry.</span></span> <span data-ttu-id="b61cc-403">Отключите этот режим в рабочей среде, так как он может замедлить работу приложения.</span><span class="sxs-lookup"><span data-stu-id="b61cc-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="b61cc-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="b61cc-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b61cc-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="b61cc-406"><a name="ikey"></a>Задание ключа hello инструментирования для выбранного пользовательского телеметрии</span><span class="sxs-lookup"><span data-stu-id="b61cc-406"><a name="ikey"></a> Setting hello instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="b61cc-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="b61cc-408"><a name="dynamic-ikey"></a> Динамический ключ инструментирования</span><span class="sxs-lookup"><span data-stu-id="b61cc-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="b61cc-409">Смешивание копирование телеметрии из разработки, тестирования и рабочих средах tooavoid вы можете [создать отдельные ресурсы Application Insights](app-insights-create-new-resource.md) и изменить свои ключи, в зависимости от среды hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-409">tooavoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on hello environment.</span></span>

<span data-ttu-id="b61cc-410">Вместо получения hello ключ инструментирования из файла конфигурации hello, можно задать в коде.</span><span class="sxs-lookup"><span data-stu-id="b61cc-410">Instead of getting hello instrumentation key from hello configuration file, you can set it in your code.</span></span> <span data-ttu-id="b61cc-411">Установите раздел hello в метод инициализации, например global.aspx.cs в службы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b61cc-411">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="b61cc-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="b61cc-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="b61cc-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b61cc-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="b61cc-414">Веб-страницы, может потребоваться tooset его из hello веб-сервере состояния, а не кодирование буквально в сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-414">In webpages, you might want tooset it from hello web server's state, rather than coding it literally into hello script.</span></span> <span data-ttu-id="b61cc-415">Например, на веб-странице, созданной в приложении ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b61cc-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="b61cc-416">*JavaScript в Razor*</span><span class="sxs-lookup"><span data-stu-id="b61cc-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="b61cc-417">Класс TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="b61cc-417">TelemetryContext</span></span>
<span data-ttu-id="b61cc-418">Экземпляр TelemetryClient включает свойство Context, содержащее несколько значений, которые отправляются вместе со всеми данными телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b61cc-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="b61cc-419">Обычно задаются модулями стандартной телеметрии hello, но можно также установить их самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="b61cc-419">They are normally set by hello standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="b61cc-420">Например:</span><span class="sxs-lookup"><span data-stu-id="b61cc-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="b61cc-421">Если установить эти значения самостоятельно, рассмотрите возможность удаления hello соответствующую строку из [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), чтобы не перепутать значения и hello стандартных значений.</span><span class="sxs-lookup"><span data-stu-id="b61cc-421">If you set any of these values yourself, consider removing hello relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and hello standard values don't get confused.</span></span>

* <span data-ttu-id="b61cc-422">**Компонент**: hello приложения и его версии.</span><span class="sxs-lookup"><span data-stu-id="b61cc-422">**Component**: hello app and its version.</span></span>
* <span data-ttu-id="b61cc-423">**Устройство**: данные об устройстве hello, где выполняется приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-423">**Device**: Data about hello device where hello app is running.</span></span> <span data-ttu-id="b61cc-424">(В веб-приложениях это hello сервере или клиентском устройстве, которые отправляются данные телеметрии hello.)</span><span class="sxs-lookup"><span data-stu-id="b61cc-424">(In web apps, this is hello server or client device that hello telemetry is sent from.)</span></span>
* <span data-ttu-id="b61cc-425">**InstrumentationKey**: hello ресурс Application Insights в Azure, в которой отображаются данные телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-425">**InstrumentationKey**: hello Application Insights resource in Azure where hello telemetry appear.</span></span> <span data-ttu-id="b61cc-426">Обычно этот ресурс получают из файла ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="b61cc-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="b61cc-427">**Расположение**: hello географическое расположение устройств hello.</span><span class="sxs-lookup"><span data-stu-id="b61cc-427">**Location**: hello geographic location of hello device.</span></span>
* <span data-ttu-id="b61cc-428">**Операция**: В веб-приложениях hello текущего HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="b61cc-428">**Operation**: In web apps, hello current HTTP request.</span></span> <span data-ttu-id="b61cc-429">В других типов приложений можно задать этот toogroup событий друг с другом.</span><span class="sxs-lookup"><span data-stu-id="b61cc-429">In other app types, you can set this toogroup events together.</span></span>
  * <span data-ttu-id="b61cc-430">**Id:** созданное значение, которое сопоставляет различные события, чтобы при проверке любого события в поиске по журналу диагностики можно было найти связанные элементы.</span><span class="sxs-lookup"><span data-stu-id="b61cc-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="b61cc-431">**Имя**: идентификатор, обычно hello URL-адрес hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="b61cc-431">**Name**: An identifier, usually hello URL of hello HTTP request.</span></span>
  * <span data-ttu-id="b61cc-432">**SyntheticSource**: Если не null или пустым, строка, указывающая источник hello hello запроса было определено как робот или веб-теста.</span><span class="sxs-lookup"><span data-stu-id="b61cc-432">**SyntheticSource**: If not null or empty, a string that indicates that hello source of hello request has been identified as a robot or web test.</span></span> <span data-ttu-id="b61cc-433">По умолчанию он исключается из вычислений в обозревателе метрик.</span><span class="sxs-lookup"><span data-stu-id="b61cc-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="b61cc-434">**Properties:** свойства, которые отправляются со всеми данными телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b61cc-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="b61cc-435">Это значение можно переопределить в отдельных вызовах Track*.</span><span class="sxs-lookup"><span data-stu-id="b61cc-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="b61cc-436">**Сеанс**: hello пользовательского сеанса.</span><span class="sxs-lookup"><span data-stu-id="b61cc-436">**Session**: hello user's session.</span></span> <span data-ttu-id="b61cc-437">Идентификатор Hello задан tooa создается значение, которое меняется, когда пользователь hello не было активных некоторое время.</span><span class="sxs-lookup"><span data-stu-id="b61cc-437">hello ID is set tooa generated value, which is changed when hello user has not been active for a while.</span></span>
* <span data-ttu-id="b61cc-438">**User:** информация о пользователе.</span><span class="sxs-lookup"><span data-stu-id="b61cc-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="b61cc-439">Ограничения</span><span class="sxs-lookup"><span data-stu-id="b61cc-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="b61cc-440">попадание ограничение частоты данных hello, используйте tooavoid [выборки](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="b61cc-440">tooavoid hitting hello data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="b61cc-441">toodetermine содержится много данных, в статье [хранение данных и конфиденциальности](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="b61cc-441">toodetermine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="b61cc-442">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="b61cc-442">Reference docs</span></span>
* [<span data-ttu-id="b61cc-443">Справочник по ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b61cc-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="b61cc-444">Справочник по Java</span><span class="sxs-lookup"><span data-stu-id="b61cc-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="b61cc-445">Справочник по JavaScript</span><span class="sxs-lookup"><span data-stu-id="b61cc-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="b61cc-446">Android SDK</span><span class="sxs-lookup"><span data-stu-id="b61cc-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="b61cc-447">iOS SDK</span><span class="sxs-lookup"><span data-stu-id="b61cc-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="b61cc-448">Код пакета SDK</span><span class="sxs-lookup"><span data-stu-id="b61cc-448">SDK code</span></span>
* [<span data-ttu-id="b61cc-449">Базовый пакет SDK для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b61cc-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="b61cc-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="b61cc-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="b61cc-451">Пакеты Windows Server</span><span class="sxs-lookup"><span data-stu-id="b61cc-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="b61cc-452">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="b61cc-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="b61cc-453">Пакет SDK для JavaScript</span><span class="sxs-lookup"><span data-stu-id="b61cc-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="b61cc-454">Все платформы</span><span class="sxs-lookup"><span data-stu-id="b61cc-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="b61cc-455">Вопросы</span><span class="sxs-lookup"><span data-stu-id="b61cc-455">Questions</span></span>
* <span data-ttu-id="b61cc-456">*Какие исключения могут создаваться при вызовах Track_()?*</span><span class="sxs-lookup"><span data-stu-id="b61cc-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="b61cc-457">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="b61cc-457">None.</span></span> <span data-ttu-id="b61cc-458">Не требуется toowrap их в конструкции try-catch.</span><span class="sxs-lookup"><span data-stu-id="b61cc-458">You don't need toowrap them in try-catch clauses.</span></span> <span data-ttu-id="b61cc-459">Если пакет SDK для hello сталкивается с проблемами, он сообщения в журнал в выходных данных консоли отладки hello и — если hello сообщения поступают через--диагностики поиска.</span><span class="sxs-lookup"><span data-stu-id="b61cc-459">If hello SDK encounters problems, it will log messages in hello debug console output and--if hello messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="b61cc-460">*Есть ли tooget данных API-интерфейса REST с hello портала?*</span><span class="sxs-lookup"><span data-stu-id="b61cc-460">*Is there a REST API tooget data from hello portal?*</span></span>

    <span data-ttu-id="b61cc-461">Да, hello [API доступа к данным](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="b61cc-461">Yes, hello [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="b61cc-462">Другие способы tooextract данные включают [Экспорт из Analytics tooPower BI](app-insights-export-power-bi.md) и [непрерывный Экспорт](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="b61cc-462">Other ways tooextract data include [export from Analytics tooPower BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="b61cc-463"><a name="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b61cc-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="b61cc-464">Поиск в Application Insights</span><span class="sxs-lookup"><span data-stu-id="b61cc-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="b61cc-465">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="b61cc-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


