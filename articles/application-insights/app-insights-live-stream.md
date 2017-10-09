---
title: "aaaLive поток метрики настраиваемых метрик и диагностики в Azure Application Insights | Документы Microsoft"
description: "Мониторинг веб-приложения в реальном времени с помощью пользовательских метрик и диагностика проблем с помощью динамического веб-канала сбоев, трассировок и событий."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="3bd9e-103">Live Metrics Stream: мониторинг и диагностика с задержкой в 1 секунду</span><span class="sxs-lookup"><span data-stu-id="3bd9e-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="3bd9e-104">Проверки подавать сигналы hello динамической, в рабочей среде веб-приложения с помощью динамический поток метрики из [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3bd9e-104">Probe hello beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="3bd9e-105">Выбор и фильтрация toowatch счетчики метрики и производительности в режиме реального времени, без tooyour любой телевизионными службы.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-105">Select and filter metrics and performance counters toowatch in real time, without any disturbance tooyour service.</span></span> <span data-ttu-id="3bd9e-106">Проверяйте трассировки стека на основе образцов неудавшихся запросов и исключений.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="3bd9e-107">Вместе с [Profiler](app-insights-profiler.md), [отладчиком моментальных снимков](app-insights-snapshot-debugger.md) и [тестированием производительности](app-insights-monitor-web-app-availability.md#performance-tests) Live Metrics Stream предоставляет эффективное средство диагностики веб-сайта, не вмешивающееся в его работу.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="3bd9e-108">С помощью Live Metrics Stream можно выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="3bd9e-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="3bd9e-109">Проверять выпущенное исправление, наблюдая за производительностью и числом сбоев.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="3bd9e-110">Посмотрите hello влияние тестирования нагрузки и диагностики проблем с live.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-110">Watch hello effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="3bd9e-111">Сосредоточиться на конкретный тест сеансов или отфильтровать известные проблемы, при выборе и фильтрации требуется toowatch метрики hello.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-111">Focus on particular test sessions or filter out known issues, by selecting and filtering hello metrics you want toowatch.</span></span>
* <span data-ttu-id="3bd9e-112">Получать трассировки исключений по мере того, как они возникают.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="3bd9e-113">Поэкспериментируйте с фильтрами toofind hello наиболее релевантных ключевых показателей эффективности.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-113">Experiment with filters toofind hello most relevant KPIs.</span></span>
* <span data-ttu-id="3bd9e-114">Отслеживать любые счетчики производительности Windows в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="3bd9e-115">Легко идентификации сервера, который испытывает проблемы и отфильтровать все hello/динамическая ключевого индикатора Производительности веб-канала toojust этого сервера.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-115">Easily identify a server that is having issues, and filter all hello KPI/live feed toojust that server.</span></span>

<span data-ttu-id="3bd9e-116">[![Видео, посвященное Live Metrics Stream](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="3bd9e-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="3bd9e-117">Динамический поток метрики в настоящее время доступен для приложений ASP.NET, выполняющихся в локальной среде или в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in hello Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="3bd9e-118">Начало работы</span><span class="sxs-lookup"><span data-stu-id="3bd9e-118">Get started</span></span>

1. <span data-ttu-id="3bd9e-119">Если вы еще не [установили Application Insights](app-insights-asp-net.md) в своем веб-приложении ASP.NET или [приложении Windows Server](app-insights-windows-services.md), сделайте это сейчас.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="3bd9e-120">**Последнюю версию обновления toohello** пакета Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-120">**Update toohello latest version** of hello Application Insights package.</span></span> <span data-ttu-id="3bd9e-121">В Visual Studio щелкните проект правой кнопкой мыши и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="3bd9e-122">Откройте hello **обновления** установите флажок **включить предварительный выпуск**и выбрать все пакеты Microsoft.ApplicationInsights.* hello.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-122">Open hello **Updates** tab, check **Include prerelease**, and select all hello Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="3bd9e-123">Разверните приложение заново.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-123">Redeploy your app.</span></span>

3. <span data-ttu-id="3bd9e-124">В hello [портал Azure](https://portal.azure.com), откройте hello ресурс Application Insights для своего приложения, а затем обновляющегося потока.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-124">In hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="3bd9e-125">[Канал управления безопасного hello](#secure-the-control-channel) Если конфиденциальные данные, например имена клиентов можно использовать в фильтры.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-125">[Secure hello control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![В колонке Обзор hello щелкните обновляющегося потока](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="3bd9e-127">Данные отсутствуют?</span><span class="sxs-lookup"><span data-stu-id="3bd9e-127">No data?</span></span> <span data-ttu-id="3bd9e-128">Проверьте брандмауэр сервера</span><span class="sxs-lookup"><span data-stu-id="3bd9e-128">Check your server firewall</span></span>

<span data-ttu-id="3bd9e-129">Проверьте hello [исходящие порты для потоковой трансляции метрики](app-insights-ip-addresses.md#outgoing-ports) открыты в брандмауэре hello серверов.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-129">Check hello [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in hello firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="3bd9e-130">Чем Live Metrics Stream отличается от обозревателя метрик и службы аналитики?</span><span class="sxs-lookup"><span data-stu-id="3bd9e-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="3bd9e-131">Live Stream</span><span class="sxs-lookup"><span data-stu-id="3bd9e-131">Live Stream</span></span> | <span data-ttu-id="3bd9e-132">Обозреватель метрик и служба аналитики</span><span class="sxs-lookup"><span data-stu-id="3bd9e-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="3bd9e-133">Задержка</span><span class="sxs-lookup"><span data-stu-id="3bd9e-133">Latency</span></span>|<span data-ttu-id="3bd9e-134">Данные отображаются в течение одной секунды</span><span class="sxs-lookup"><span data-stu-id="3bd9e-134">Data displayed within one second</span></span>|<span data-ttu-id="3bd9e-135">Агрегирование выполняется в течение нескольких минут</span><span class="sxs-lookup"><span data-stu-id="3bd9e-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="3bd9e-136">Нет сохранения</span><span class="sxs-lookup"><span data-stu-id="3bd9e-136">No retention</span></span>|<span data-ttu-id="3bd9e-137">Данные хранятся на диаграмме hello, и затем удаляется</span><span class="sxs-lookup"><span data-stu-id="3bd9e-137">Data persists while it's on hello chart, and is then discarded</span></span>|[<span data-ttu-id="3bd9e-138">Данные сохраняются 90 дней</span><span class="sxs-lookup"><span data-stu-id="3bd9e-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="3bd9e-139">По запросу</span><span class="sxs-lookup"><span data-stu-id="3bd9e-139">On demand</span></span>|<span data-ttu-id="3bd9e-140">Данные передаются, пока открыта служба Live Metrics</span><span class="sxs-lookup"><span data-stu-id="3bd9e-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="3bd9e-141">Данные отправляются в том случае, когда hello SDK установлен и включен</span><span class="sxs-lookup"><span data-stu-id="3bd9e-141">Data is sent whenever hello SDK is installed and enabled</span></span>|
|<span data-ttu-id="3bd9e-142">Free</span><span class="sxs-lookup"><span data-stu-id="3bd9e-142">Free</span></span>|<span data-ttu-id="3bd9e-143">Плата за данные Live Stream не взимается</span><span class="sxs-lookup"><span data-stu-id="3bd9e-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="3bd9e-144">Тема слишком[цены](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="3bd9e-144">Subject too[pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="3bd9e-145">Выборка</span><span class="sxs-lookup"><span data-stu-id="3bd9e-145">Sampling</span></span>|<span data-ttu-id="3bd9e-146">Передаются все выбранные метрики и счетчики.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="3bd9e-147">Производится выборка сбоев и трассировок стека.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="3bd9e-148">TelemetryProcessors не применяются.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="3bd9e-149">Может производиться [выборка](app-insights-api-filtering-sampling.md) событий.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="3bd9e-150">Канал управления</span><span class="sxs-lookup"><span data-stu-id="3bd9e-150">Control channel</span></span>|<span data-ttu-id="3bd9e-151">Сигналы управления фильтра, отправляются toohello SDK.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-151">Filter control signals are sent toohello SDK.</span></span> <span data-ttu-id="3bd9e-152">Рекомендуется [защитить этот канал](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="3bd9e-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="3bd9e-153">Связь является односторонней, toohello портала</span><span class="sxs-lookup"><span data-stu-id="3bd9e-153">Communication is one-way, toohello portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="3bd9e-154">Выбор и фильтрация метрик</span><span class="sxs-lookup"><span data-stu-id="3bd9e-154">Select and filter your metrics</span></span>

<span data-ttu-id="3bd9e-155">(На классическом приложений ASP.NET с помощью hello новейшую версию пакета SDK.)</span><span class="sxs-lookup"><span data-stu-id="3bd9e-155">(Available on classic ASP.NET apps with hello latest SDK.)</span></span>

<span data-ttu-id="3bd9e-156">Вы можете отслеживать пользовательские ключевого индикатора Производительности динамической путем применения фильтров произвольный на любой телеметрии Application Insights с портала hello.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from hello portal.</span></span> <span data-ttu-id="3bd9e-157">Щелкните элемент управления фильтром hello, показывающий, когда вы указатель любой hello диаграмм.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-157">Click hello filter control that shows when you mouse-over any of hello charts.</span></span> <span data-ttu-id="3bd9e-158">Следующая диаграмма Hello отображения на диаграмме пользовательского запроса счетчик ключевого показателя Эффективности с фильтры для атрибутов URL-адрес и длительность.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-158">hello following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="3bd9e-159">Проверьте фильтры с hello Предварительный просмотр потока раздел, описывающий динамического канала телеметрии, которая соответствует критериям hello, заданные в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-159">Validate your filters with hello Stream Preview section that shows a live feed of telemetry that matches hello criteria you have specified at any point in time.</span></span> 

![Пользовательский КПЭ запросов](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="3bd9e-161">Вы можете отслеживать не только количество.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="3bd9e-162">Hello параметры зависят от типа hello потока, который может быть любой телеметрии Application Insights: запросы, зависимости, исключения, трассировок, события или метрик.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-162">hello options depend on hello type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="3bd9e-163">Поток может передавать и ваше [пользовательское измерение](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="3bd9e-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Параметры значения](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="3bd9e-165">В дополнение к этому tooApplication телеметрии аналитики также можно отслеживать любого счетчика производительности Windows, выбрав, параметры потока hello и указав имя hello счетчика производительности "hello".</span><span class="sxs-lookup"><span data-stu-id="3bd9e-165">In addition tooApplication Insights telemetry, you can also monitor any Windows performance counter by selecting that from hello stream options, and providing hello name of hello performance counter.</span></span>

<span data-ttu-id="3bd9e-166">Динамические метрики объединяются дважды: локально на каждом сервере, а затем на всех серверах.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="3bd9e-167">По умолчанию hello в одном, используя другие параметры hello соответствующих раскрывающихся списков можно изменить.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-167">You can change hello default at either by selecting other options in hello respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="3bd9e-168">Пример данных телеметрии: пользовательские события динамической диагностики</span><span class="sxs-lookup"><span data-stu-id="3bd9e-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="3bd9e-169">По умолчанию hello динамического канала событий показаны примеры запросов с ошибками и вызовы зависимостей, исключения, события и трассировки.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-169">By default, hello live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="3bd9e-170">Щелкните hello значок toosee hello применения отбора в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-170">Click hello filter icon toosee hello applied criteria at any point in time.</span></span> 

![Динамический веб-канал по умолчанию](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="3bd9e-172">Как с метриками, можно указать любой произвольный критерии tooany типов телеметрии Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-172">As with metrics, you can specify any arbitrary criteria tooany of hello Application Insights telemetry types.</span></span> <span data-ttu-id="3bd9e-173">В этом примере мы выбираем конкретные сбои запросов, трассировки и события.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="3bd9e-174">Мы также выбираем все исключения и сбои зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-174">We are also selecting all exceptions and dependency failures.</span></span>

![Пользовательский динамический веб-канал](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="3bd9e-176">Примечание: В настоящее время в критериях исключения на уровне сообщений, используйте сообщение hello внешней исключения.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-176">Note: Currently, for Exception message-based criteria, use hello outermost exception message.</span></span> <span data-ttu-id="3bd9e-177">В предыдущих примере hello toofilter out hello критической исключение с сообщением внутреннее исключение (следующим hello «<--» разделитель) «hello client отключен».</span><span class="sxs-lookup"><span data-stu-id="3bd9e-177">In hello preceding example, toofilter out hello benign exception with inner exception message (follows hello "<--" delimiter) "hello client disconnected."</span></span> <span data-ttu-id="3bd9e-178">использовался критерий "Message not-contains "Error reading request content"" (Сообщение не содержит "Ошибка при чтении содержимого запроса").</span><span class="sxs-lookup"><span data-stu-id="3bd9e-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="3bd9e-179">В разделе hello сведения об элементе в hello live веб-канала, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-179">See hello details of an item in hello live feed by clicking it.</span></span> <span data-ttu-id="3bd9e-180">Вы можете приостановить hello веб-канала либо нажав **приостановить** просто прокрутку вниз или при выборе пункта меню.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-180">You can pause hello feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="3bd9e-181">Динамического канала будет возобновлена после прокрутки начало обратной toohello или щелкнув hello счетчик элементов, собранные во время оно было приостановлено.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-181">Live feed will resume after you scroll back toohello top, or by clicking hello counter of items collected while it was paused.</span></span>

![Выборка динамических ошибок](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="3bd9e-183">Фильтрация по экземпляру сервера</span><span class="sxs-lookup"><span data-stu-id="3bd9e-183">Filter by server instance</span></span>

<span data-ttu-id="3bd9e-184">Если вы хотите toomonitor экземпляр роли сервера, можно отфильтровать сервером.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-184">If you want toomonitor a particular server role instance, you can filter by server.</span></span>

![Выборка динамических ошибок](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="3bd9e-186">Требования к пакетам SDK</span><span class="sxs-lookup"><span data-stu-id="3bd9e-186">SDK Requirements</span></span>
<span data-ttu-id="3bd9e-187">Пользовательские метрики и события Live Metrics Stream доступны при использовании версии 2.4.0-beta2 или более новой версии [пакета SDK для Application Insights для веб-приложений](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="3bd9e-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="3bd9e-188">Помните, параметр «Включить предварительный выпуск» tooselect из диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-188">Remember tooselect "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-hello-control-channel"></a><span data-ttu-id="3bd9e-189">Безопасный канал управления hello</span><span class="sxs-lookup"><span data-stu-id="3bd9e-189">Secure hello control channel</span></span>
<span data-ttu-id="3bd9e-190">Hello настраиваемые фильтры заданных критериев отправляются назад toohello компонент Live метрики hello пакет SDK Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-190">hello custom filters criteria you specify are sent back toohello Live Metrics component in hello Application Insights SDK.</span></span> <span data-ttu-id="3bd9e-191">Hello фильтры могут содержать конфиденциальные сведения, например кодов клиента.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-191">hello filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="3bd9e-192">Можно сделать канала hello secure секретным ключом API Кроме toohello ключ инструментирования.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-192">You can make hello channel secure with a secret API key in addition toohello instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="3bd9e-193">Создание ключа API</span><span class="sxs-lookup"><span data-stu-id="3bd9e-193">Create an API Key</span></span>

![Создание ключа API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a><span data-ttu-id="3bd9e-195">Добавление ключа tooConfiguration API</span><span class="sxs-lookup"><span data-stu-id="3bd9e-195">Add API key tooConfiguration</span></span>
<span data-ttu-id="3bd9e-196">Добавьте в файл applicationinsights.config hello, hello AuthenticationApiKey toohello QuickPulseTelemetryModule.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-196">In hello applicationinsights.config file, add hello AuthenticationApiKey toohello QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="3bd9e-197">Или в коде, задайте его в hello QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="3bd9e-197">Or in code, set it on hello QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="3bd9e-198">Однако если распознавать и доверять всем hello подключенных серверов, можно попробовать hello настраиваемые фильтры без канала с проверкой подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-198">However, if you recognize and trust all hello connected servers, you can try hello custom filters without hello authenticated channel.</span></span> <span data-ttu-id="3bd9e-199">Эта возможность доступна в течение шести месяцев.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-199">This option is available for six months.</span></span> <span data-ttu-id="3bd9e-200">Это переопределение требуется после каждого создания сеанса или подключения нового сервера.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-200">This override is required once every new session, or when a new server comes online.</span></span>

![Параметры аутентификации Live Metrics](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="3bd9e-202">Настоятельно рекомендуется установить канал с проверкой подлинности hello перед вводом потенциально конфиденциальных данных, например CustomerID в критериях фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-202">We strongly recommend that you set up hello authenticated channel before entering potentially sensitive information like CustomerID in hello filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="3bd9e-203">Создание нагрузки для тестирования производительности</span><span class="sxs-lookup"><span data-stu-id="3bd9e-203">Generating a performance test load</span></span>

<span data-ttu-id="3bd9e-204">Влияние hello toowatch загрузки увеличить, используйте hello теста производительности колонку.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-204">If you want toowatch hello effect of a load increase, use hello Performance Test blade.</span></span> <span data-ttu-id="3bd9e-205">В ней имитируются одновременные запросы от нескольких пользователей.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="3bd9e-206">Его можно запустить либо «ручные тесты» (ping тесты) одного URL-адреса, или он может выполнять [многоэтапной веб-теста производительности](app-insights-monitor-web-app-availability.md#multi-step-web-tests) отправлять (в hello таким же способом, как доступности тестирования).</span><span class="sxs-lookup"><span data-stu-id="3bd9e-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in hello same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="3bd9e-207">После создания теста производительности hello, откройте тест hello и hello колонке обновляющегося потока в отдельных окнах.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-207">After you create hello performance test, open hello test and hello Live Stream blade in separate windows.</span></span> <span data-ttu-id="3bd9e-208">Можно увидеть при запуске теста производительности и контрольных значений обновляющегося потока в hello hello из очереди одновременно.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-208">You can see when hello queued performance test starts, and watch live stream at hello same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="3bd9e-209">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="3bd9e-209">Troubleshooting</span></span>

<span data-ttu-id="3bd9e-210">Данные отсутствуют?</span><span class="sxs-lookup"><span data-stu-id="3bd9e-210">No data?</span></span> <span data-ttu-id="3bd9e-211">Если приложение находится в защищенной сети: Live Metrics Stream использует IP-адреса, отличающиеся IP-адресов другой телеметрии Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="3bd9e-212">Убедитесь, что [эти IP-адреса](app-insights-ip-addresses.md) открыты в брандмауэре.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="3bd9e-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3bd9e-213">Next steps</span></span>
* [<span data-ttu-id="3bd9e-214">Отслеживание использования Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3bd9e-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="3bd9e-215">Использование диагностического поиска</span><span class="sxs-lookup"><span data-stu-id="3bd9e-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="3bd9e-216">Профилировщик</span><span class="sxs-lookup"><span data-stu-id="3bd9e-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="3bd9e-217">Отладчик моментальных снимков</span><span class="sxs-lookup"><span data-stu-id="3bd9e-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
