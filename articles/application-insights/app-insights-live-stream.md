---
title: "Live Metrics Stream с пользовательскими метриками и диагностика в Azure Application Insights | Документы Майкрософт"
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
ms.openlocfilehash: 1eb2e0c467d4fb4cb263047caf58d36231578d9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="40522-103">Live Metrics Stream: мониторинг и диагностика с задержкой в 1 секунду</span><span class="sxs-lookup"><span data-stu-id="40522-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="40522-104">Держите руку на пульсе работы веб-приложения с помощью Live Metrics Stream в [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40522-104">Probe the beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="40522-105">Выбирайте и фильтруйте метрики и счетчики производительности для отслеживания в режиме реального времени, не нарушая работу служб.</span><span class="sxs-lookup"><span data-stu-id="40522-105">Select and filter metrics and performance counters to watch in real time, without any disturbance to your service.</span></span> <span data-ttu-id="40522-106">Проверяйте трассировки стека на основе образцов неудавшихся запросов и исключений.</span><span class="sxs-lookup"><span data-stu-id="40522-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="40522-107">Вместе с [Profiler](app-insights-profiler.md), [отладчиком моментальных снимков](app-insights-snapshot-debugger.md) и [тестированием производительности](app-insights-monitor-web-app-availability.md#performance-tests) Live Metrics Stream предоставляет эффективное средство диагностики веб-сайта, не вмешивающееся в его работу.</span><span class="sxs-lookup"><span data-stu-id="40522-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="40522-108">С помощью Live Metrics Stream можно выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="40522-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="40522-109">Проверять выпущенное исправление, наблюдая за производительностью и числом сбоев.</span><span class="sxs-lookup"><span data-stu-id="40522-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="40522-110">Наблюдать за результатом применения тестовых нагрузок и диагностировать проблемы в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="40522-110">Watch the effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="40522-111">Сосредотачиваться на определенных тестовых сеансах или отфильтровывать известные проблемы, выбирая и фильтруя метрики, подлежащие отслеживанию.</span><span class="sxs-lookup"><span data-stu-id="40522-111">Focus on particular test sessions or filter out known issues, by selecting and filtering the metrics you want to watch.</span></span>
* <span data-ttu-id="40522-112">Получать трассировки исключений по мере того, как они возникают.</span><span class="sxs-lookup"><span data-stu-id="40522-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="40522-113">Экспериментировать с фильтрами, чтобы найти наиболее важные ключевые показатели эффективности.</span><span class="sxs-lookup"><span data-stu-id="40522-113">Experiment with filters to find the most relevant KPIs.</span></span>
* <span data-ttu-id="40522-114">Отслеживать любые счетчики производительности Windows в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="40522-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="40522-115">Легко определить сервер, на котором возникают проблемы, и с помощью фильтра получить все КПЭ и динамические веб-каналы, относящиеся только к этому серверу.</span><span class="sxs-lookup"><span data-stu-id="40522-115">Easily identify a server that is having issues, and filter all the KPI/live feed to just that server.</span></span>

<span data-ttu-id="40522-116">[![Видео, посвященное Live Metrics Stream](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="40522-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="40522-117">Служба Live Metrics Stream в настоящее время доступна для приложений ASP.NET, работающих в локальной среде или облаке.</span><span class="sxs-lookup"><span data-stu-id="40522-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in the Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="40522-118">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="40522-118">Get started</span></span>

1. <span data-ttu-id="40522-119">Если вы еще не [установили Application Insights](app-insights-asp-net.md) в своем веб-приложении ASP.NET или [приложении Windows Server](app-insights-windows-services.md), сделайте это сейчас.</span><span class="sxs-lookup"><span data-stu-id="40522-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="40522-120">**Выполните обновление до последней версии** пакета Application Insights.</span><span class="sxs-lookup"><span data-stu-id="40522-120">**Update to the latest version** of the Application Insights package.</span></span> <span data-ttu-id="40522-121">В Visual Studio щелкните проект правой кнопкой мыши и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="40522-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="40522-122">Откройте вкладку **Обновления**, установите флажок **Включить предварительные выпуски** и выберите все пакеты Microsoft.ApplicationInsights.*.</span><span class="sxs-lookup"><span data-stu-id="40522-122">Open the **Updates** tab, check **Include prerelease**, and select all the Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="40522-123">Разверните приложение заново.</span><span class="sxs-lookup"><span data-stu-id="40522-123">Redeploy your app.</span></span>

3. <span data-ttu-id="40522-124">На [портале Azure](https://portal.azure.com) откройте ресурс Application Insights для своего приложения, а затем откройте Live Stream.</span><span class="sxs-lookup"><span data-stu-id="40522-124">In the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="40522-125">[Защитите канал управления](#secure-the-control-channel), если в фильтрах могут использоваться конфиденциальные данные, например имена клиентов.</span><span class="sxs-lookup"><span data-stu-id="40522-125">[Secure the control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![В колонке обзора щелкните Live Stream (Динамический поток).](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="40522-127">Данные отсутствуют?</span><span class="sxs-lookup"><span data-stu-id="40522-127">No data?</span></span> <span data-ttu-id="40522-128">Проверьте брандмауэр сервера</span><span class="sxs-lookup"><span data-stu-id="40522-128">Check your server firewall</span></span>

<span data-ttu-id="40522-129">Убедитесь в том, что [исходящие порты для Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) открыты в брандмауэре ваших серверов.</span><span class="sxs-lookup"><span data-stu-id="40522-129">Check the [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in the firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="40522-130">Чем Live Metrics Stream отличается от обозревателя метрик и службы аналитики?</span><span class="sxs-lookup"><span data-stu-id="40522-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="40522-131">Live Stream</span><span class="sxs-lookup"><span data-stu-id="40522-131">Live Stream</span></span> | <span data-ttu-id="40522-132">Обозреватель метрик и служба аналитики</span><span class="sxs-lookup"><span data-stu-id="40522-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="40522-133">Задержка</span><span class="sxs-lookup"><span data-stu-id="40522-133">Latency</span></span>|<span data-ttu-id="40522-134">Данные отображаются в течение одной секунды</span><span class="sxs-lookup"><span data-stu-id="40522-134">Data displayed within one second</span></span>|<span data-ttu-id="40522-135">Агрегирование выполняется в течение нескольких минут</span><span class="sxs-lookup"><span data-stu-id="40522-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="40522-136">Нет сохранения</span><span class="sxs-lookup"><span data-stu-id="40522-136">No retention</span></span>|<span data-ttu-id="40522-137">Данные сохраняются, только пока они отображаются на диаграмме, а затем удаляются.</span><span class="sxs-lookup"><span data-stu-id="40522-137">Data persists while it's on the chart, and is then discarded</span></span>|[<span data-ttu-id="40522-138">Данные сохраняются 90 дней</span><span class="sxs-lookup"><span data-stu-id="40522-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="40522-139">По запросу</span><span class="sxs-lookup"><span data-stu-id="40522-139">On demand</span></span>|<span data-ttu-id="40522-140">Данные передаются, пока открыта служба Live Metrics</span><span class="sxs-lookup"><span data-stu-id="40522-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="40522-141">Данные отправляются, когда пакет SDK установлен и включен</span><span class="sxs-lookup"><span data-stu-id="40522-141">Data is sent whenever the SDK is installed and enabled</span></span>|
|<span data-ttu-id="40522-142">Free</span><span class="sxs-lookup"><span data-stu-id="40522-142">Free</span></span>|<span data-ttu-id="40522-143">Плата за данные Live Stream не взимается</span><span class="sxs-lookup"><span data-stu-id="40522-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="40522-144">Действуют [расценки](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="40522-144">Subject to [pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="40522-145">Выборка</span><span class="sxs-lookup"><span data-stu-id="40522-145">Sampling</span></span>|<span data-ttu-id="40522-146">Передаются все выбранные метрики и счетчики.</span><span class="sxs-lookup"><span data-stu-id="40522-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="40522-147">Производится выборка сбоев и трассировок стека.</span><span class="sxs-lookup"><span data-stu-id="40522-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="40522-148">TelemetryProcessors не применяются.</span><span class="sxs-lookup"><span data-stu-id="40522-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="40522-149">Может производиться [выборка](app-insights-api-filtering-sampling.md) событий.</span><span class="sxs-lookup"><span data-stu-id="40522-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="40522-150">Канал управления</span><span class="sxs-lookup"><span data-stu-id="40522-150">Control channel</span></span>|<span data-ttu-id="40522-151">В пакет SDK отправляются управляющие сигналы фильтрации.</span><span class="sxs-lookup"><span data-stu-id="40522-151">Filter control signals are sent to the SDK.</span></span> <span data-ttu-id="40522-152">Рекомендуется [защитить этот канал](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="40522-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="40522-153">Взаимодействие является односторонним (в сторону портала)</span><span class="sxs-lookup"><span data-stu-id="40522-153">Communication is one-way, to the portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="40522-154">Выбор и фильтрация метрик</span><span class="sxs-lookup"><span data-stu-id="40522-154">Select and filter your metrics</span></span>

<span data-ttu-id="40522-155">(Доступно для классических приложений ASP.NET с последней версией пакета SDK.)</span><span class="sxs-lookup"><span data-stu-id="40522-155">(Available on classic ASP.NET apps with the latest SDK.)</span></span>

<span data-ttu-id="40522-156">Можно отслеживать пользовательский КПЭ в реальном времени, применяя произвольные фильтры к любым данным телеметрии Application Insights на портале.</span><span class="sxs-lookup"><span data-stu-id="40522-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from the portal.</span></span> <span data-ttu-id="40522-157">Щелкните элемент управления фильтром, появляющийся при наведении указателя мыши на любую диаграмму.</span><span class="sxs-lookup"><span data-stu-id="40522-157">Click the filter control that shows when you mouse-over any of the charts.</span></span> <span data-ttu-id="40522-158">На диаграмме ниже показан пользовательский КПЭ числа запросов с фильтрами по для атрибутам URL-адреса и длительности.</span><span class="sxs-lookup"><span data-stu-id="40522-158">The following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="40522-159">Проверьте результат фильтрации в разделе "Просмотр потока", в котором отображается динамический веб-канал телеметрии, соответствующей критериям, которые можно указать в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="40522-159">Validate your filters with the Stream Preview section that shows a live feed of telemetry that matches the criteria you have specified at any point in time.</span></span> 

![Пользовательский КПЭ запросов](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="40522-161">Вы можете отслеживать не только количество.</span><span class="sxs-lookup"><span data-stu-id="40522-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="40522-162">Параметры зависят от типа потока. Он может передавать любые данные телеметрии Application Insights: запросы, зависимости, исключения, трассировки, события или метрики.</span><span class="sxs-lookup"><span data-stu-id="40522-162">The options depend on the type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="40522-163">Поток может передавать и ваше [пользовательское измерение](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="40522-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Параметры значения](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="40522-165">Помимо телеметрии Application Insights, можно также отслеживать любой счетчик производительности Windows, выбрав его в параметрах потока и указав имя счетчика производительности.</span><span class="sxs-lookup"><span data-stu-id="40522-165">In addition to Application Insights telemetry, you can also monitor any Windows performance counter by selecting that from the stream options, and providing the name of the performance counter.</span></span>

<span data-ttu-id="40522-166">Динамические метрики объединяются дважды: локально на каждом сервере, а затем на всех серверах.</span><span class="sxs-lookup"><span data-stu-id="40522-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="40522-167">Можно изменить режим по умолчанию для обоих случаев, выбрав другие параметры в соответствующих раскрывающихся списках.</span><span class="sxs-lookup"><span data-stu-id="40522-167">You can change the default at either by selecting other options in the respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="40522-168">Пример данных телеметрии: пользовательские события динамической диагностики</span><span class="sxs-lookup"><span data-stu-id="40522-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="40522-169">По умолчанию динамический веб-канал событий отображает примеры завершившихся сбоем запросов и вызовов зависимостей, исключений, событий и трассировок.</span><span class="sxs-lookup"><span data-stu-id="40522-169">By default, the live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="40522-170">Щелкните значок фильтра, чтобы просмотреть действующие критерии в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="40522-170">Click the filter icon to see the applied criteria at any point in time.</span></span> 

![Динамический веб-канал по умолчанию](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="40522-172">Как и для метрик, можно указать любые произвольные критерии для любого типа данных телеметрии Application Insights.</span><span class="sxs-lookup"><span data-stu-id="40522-172">As with metrics, you can specify any arbitrary criteria to any of the Application Insights telemetry types.</span></span> <span data-ttu-id="40522-173">В этом примере мы выбираем конкретные сбои запросов, трассировки и события.</span><span class="sxs-lookup"><span data-stu-id="40522-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="40522-174">Мы также выбираем все исключения и сбои зависимостей.</span><span class="sxs-lookup"><span data-stu-id="40522-174">We are also selecting all exceptions and dependency failures.</span></span>

![Пользовательский динамический веб-канал](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="40522-176">Примечание. В настоящее время для критериев на основе сообщений об исключениях используйте сообщение о внешнем исключении.</span><span class="sxs-lookup"><span data-stu-id="40522-176">Note: Currently, for Exception message-based criteria, use the outermost exception message.</span></span> <span data-ttu-id="40522-177">В предыдущем примере, чтобы отфильтровать неопасные исключения с сообщением о внутреннем исключении (после разделителя "<--") "Клиент отключен",</span><span class="sxs-lookup"><span data-stu-id="40522-177">In the preceding example, to filter out the benign exception with inner exception message (follows the "<--" delimiter) "The client disconnected."</span></span> <span data-ttu-id="40522-178">использовался критерий "Message not-contains "Error reading request content"" (Сообщение не содержит "Ошибка при чтении содержимого запроса").</span><span class="sxs-lookup"><span data-stu-id="40522-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="40522-179">Просмотрите сведения об элементе динамического веб-канала, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="40522-179">See the details of an item in the live feed by clicking it.</span></span> <span data-ttu-id="40522-180">Можно приостановить веб-канал, щелкнув **Приостановить**, прокрутив вниз или щелкнув элемент.</span><span class="sxs-lookup"><span data-stu-id="40522-180">You can pause the feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="40522-181">Работа динамического веб-канала возобновится, когда вы прокрутите его обратно до начала или щелкните счетчик элементов, собранных во время приостановки.</span><span class="sxs-lookup"><span data-stu-id="40522-181">Live feed will resume after you scroll back to the top, or by clicking the counter of items collected while it was paused.</span></span>

![Выборка динамических ошибок](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="40522-183">Фильтрация по экземпляру сервера</span><span class="sxs-lookup"><span data-stu-id="40522-183">Filter by server instance</span></span>

<span data-ttu-id="40522-184">Если требуется отслеживать определенный экземпляр роли сервера, можно применить фильтрацию по серверу.</span><span class="sxs-lookup"><span data-stu-id="40522-184">If you want to monitor a particular server role instance, you can filter by server.</span></span>

![Выборка динамических ошибок](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="40522-186">Требования к пакетам SDK</span><span class="sxs-lookup"><span data-stu-id="40522-186">SDK Requirements</span></span>
<span data-ttu-id="40522-187">Пользовательские метрики и события Live Metrics Stream доступны при использовании версии 2.4.0-beta2 или более новой версии [пакета SDK для Application Insights для веб-приложений](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="40522-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="40522-188">Не забудьте выбрать параметр "Включить предварительные выпуски" в диспетчере пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="40522-188">Remember to select "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-the-control-channel"></a><span data-ttu-id="40522-189">Защита канала управления</span><span class="sxs-lookup"><span data-stu-id="40522-189">Secure the control channel</span></span>
<span data-ttu-id="40522-190">Указываемые вами пользовательские критерии фильтра передаются в компонент Live Metrics в пакете SDK для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="40522-190">The custom filters criteria you specify are sent back to the Live Metrics component in the Application Insights SDK.</span></span> <span data-ttu-id="40522-191">Фильтры могут содержать конфиденциальные сведения, например идентификаторы клиентов.</span><span class="sxs-lookup"><span data-stu-id="40522-191">The filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="40522-192">Помимо ключа инструментирования, канал для их передачи можно защитить секретным ключом API.</span><span class="sxs-lookup"><span data-stu-id="40522-192">You can make the channel secure with a secret API key in addition to the instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="40522-193">Создание ключа API</span><span class="sxs-lookup"><span data-stu-id="40522-193">Create an API Key</span></span>

![Создание ключа API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-to-configuration"></a><span data-ttu-id="40522-195">Добавление ключа API в конфигурацию</span><span class="sxs-lookup"><span data-stu-id="40522-195">Add API key to Configuration</span></span>
<span data-ttu-id="40522-196">В файле applicationinsights.config добавьте AuthenticationApiKey в QuickPulseTelemetryModule.</span><span class="sxs-lookup"><span data-stu-id="40522-196">In the applicationinsights.config file, add the AuthenticationApiKey to the QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="40522-197">Или задайте его в коде для QuickPulseTelemetryModule.</span><span class="sxs-lookup"><span data-stu-id="40522-197">Or in code, set it on the QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="40522-198">Однако, если все подключенные серверы опознаны и надежны, можно использовать настраиваемые фильтры без аутентифицированного канала.</span><span class="sxs-lookup"><span data-stu-id="40522-198">However, if you recognize and trust all the connected servers, you can try the custom filters without the authenticated channel.</span></span> <span data-ttu-id="40522-199">Эта возможность доступна в течение шести месяцев.</span><span class="sxs-lookup"><span data-stu-id="40522-199">This option is available for six months.</span></span> <span data-ttu-id="40522-200">Это переопределение требуется после каждого создания сеанса или подключения нового сервера.</span><span class="sxs-lookup"><span data-stu-id="40522-200">This override is required once every new session, or when a new server comes online.</span></span>

![Параметры аутентификации Live Metrics](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="40522-202">Настоятельно рекомендуется установить аутентифицированный канал перед вводом в критерии фильтра потенциально конфиденциальной информации, например идентификатора клиента.</span><span class="sxs-lookup"><span data-stu-id="40522-202">We strongly recommend that you set up the authenticated channel before entering potentially sensitive information like CustomerID in the filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="40522-203">Создание нагрузки для тестирования производительности</span><span class="sxs-lookup"><span data-stu-id="40522-203">Generating a performance test load</span></span>

<span data-ttu-id="40522-204">Если необходимо отследить результат повышения нагрузки, используйте колонку "Тест производительности".</span><span class="sxs-lookup"><span data-stu-id="40522-204">If you want to watch the effect of a load increase, use the Performance Test blade.</span></span> <span data-ttu-id="40522-205">В ней имитируются одновременные запросы от нескольких пользователей.</span><span class="sxs-lookup"><span data-stu-id="40522-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="40522-206">Можно выполнить "ручные тесты" (проверку связи) для отдельного URL-адреса или [многоэтапный веб-тест производительности](app-insights-monitor-web-app-availability.md#multi-step-web-tests), который добавляется так же, как тест доступности.</span><span class="sxs-lookup"><span data-stu-id="40522-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in the same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="40522-207">После создания теста производительности откройте его и колонку Live Stream в отдельных окнах.</span><span class="sxs-lookup"><span data-stu-id="40522-207">After you create the performance test, open the test and the Live Stream blade in separate windows.</span></span> <span data-ttu-id="40522-208">Вы сможете увидеть, когда начнется тест производительности, поставленный в очередь, одновременно наблюдая за динамическим потоком.</span><span class="sxs-lookup"><span data-stu-id="40522-208">You can see when the queued performance test starts, and watch live stream at the same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="40522-209">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="40522-209">Troubleshooting</span></span>

<span data-ttu-id="40522-210">Данные отсутствуют?</span><span class="sxs-lookup"><span data-stu-id="40522-210">No data?</span></span> <span data-ttu-id="40522-211">Если приложение находится в защищенной сети: Live Metrics Stream использует IP-адреса, отличающиеся IP-адресов другой телеметрии Application Insights.</span><span class="sxs-lookup"><span data-stu-id="40522-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="40522-212">Убедитесь, что [эти IP-адреса](app-insights-ip-addresses.md) открыты в брандмауэре.</span><span class="sxs-lookup"><span data-stu-id="40522-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="40522-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="40522-213">Next steps</span></span>
* [<span data-ttu-id="40522-214">Отслеживание использования Application Insights.</span><span class="sxs-lookup"><span data-stu-id="40522-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="40522-215">Использование диагностического поиска</span><span class="sxs-lookup"><span data-stu-id="40522-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="40522-216">Профилировщик</span><span class="sxs-lookup"><span data-stu-id="40522-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="40522-217">Отладчик моментальных снимков</span><span class="sxs-lookup"><span data-stu-id="40522-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
