---
title: "Метрики в Azure Application Insights aaaExploring | Документы Microsoft"
description: "Toointerpret диаграммах на метрики обозревателя, а также и колонок toocustomize обозревателя метрик."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="f01d8-103">Исследование метрик в Application Insights</span><span class="sxs-lookup"><span data-stu-id="f01d8-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="f01d8-104">Метрики в [Application Insights][start] — это измеренные значения и счетчики событий, которые передаются как данные телеметрии из приложения.</span><span class="sxs-lookup"><span data-stu-id="f01d8-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="f01d8-105">Они помогают обнаруживать проблемы производительности и отслеживать тенденции в использовании приложения.</span><span class="sxs-lookup"><span data-stu-id="f01d8-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="f01d8-106">Существует широкий спектр стандартных метрик, и можно также создавать собственные пользовательские метрики и события.</span><span class="sxs-lookup"><span data-stu-id="f01d8-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="f01d8-107">Метрики и счетчики событий отображаются в диаграммах агрегированных значений, например как сумма, среднее или количество.</span><span class="sxs-lookup"><span data-stu-id="f01d8-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="f01d8-108">Вот пример набора диаграмм:</span><span class="sxs-lookup"><span data-stu-id="f01d8-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="f01d8-109">Найти everywhere диаграммы метрик на портале Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="f01d8-109">You find metrics charts everywhere in hello Application Insights portal.</span></span> <span data-ttu-id="f01d8-110">В большинстве случаев они могут быть настроены и можно добавлять дополнительные диаграммы toohello колонку.</span><span class="sxs-lookup"><span data-stu-id="f01d8-110">In most cases, they can be customized, and you can add more charts toohello blade.</span></span> <span data-ttu-id="f01d8-111">Из колонки Обзор hello, щелкая toomore подробные диаграммы (которые имеют названия, такие как «Серверы»), или нажмите кнопку **обозревателя метрик** tooopen Новая колонка, где можно создавать настраиваемые диаграммы.</span><span class="sxs-lookup"><span data-stu-id="f01d8-111">From hello Overview blade, click through toomore detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** tooopen a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="f01d8-112">Диапазон времени</span><span class="sxs-lookup"><span data-stu-id="f01d8-112">Time range</span></span>
<span data-ttu-id="f01d8-113">Можно изменить диапазон времени, охватываемого hello диаграммы или сетки в любой колонке hello.</span><span class="sxs-lookup"><span data-stu-id="f01d8-113">You can change hello Time range covered by hello charts or grids on any blade.</span></span>

![Привет открыть колонку Обзор приложения hello портал Azure](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="f01d8-115">Если ожидаются некоторые данные, которые еще не отобразились, нажмите кнопку "Обновить".</span><span class="sxs-lookup"><span data-stu-id="f01d8-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="f01d8-116">Диаграммы обновления сами через промежутки времени, но интервалы приветствия больше времени для больших временных интервалов.</span><span class="sxs-lookup"><span data-stu-id="f01d8-116">Charts refresh themselves at intervals, but hello intervals are longer for larger time ranges.</span></span> <span data-ttu-id="f01d8-117">Он может занять некоторое время toocome данных через конвейер анализа hello фигуру на диаграмму.</span><span class="sxs-lookup"><span data-stu-id="f01d8-117">It can take a while for data toocome through hello analysis pipeline onto a chart.</span></span>

<span data-ttu-id="f01d8-118">toozoom в части диаграммы, перетащите его:</span><span class="sxs-lookup"><span data-stu-id="f01d8-118">toozoom into part of a chart, drag over it:</span></span>

![Перетащите часть диаграммы.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="f01d8-120">Щелкните toorestore кнопку отмены масштаб hello его.</span><span class="sxs-lookup"><span data-stu-id="f01d8-120">Click hello Undo Zoom button toorestore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="f01d8-121">Детализация и значения точек</span><span class="sxs-lookup"><span data-stu-id="f01d8-121">Granularity and point values</span></span>
<span data-ttu-id="f01d8-122">Наведите курсор мыши на данный момент над значениями hello toodisplay hello диаграммы метрик hello.</span><span class="sxs-lookup"><span data-stu-id="f01d8-122">Hover your mouse over hello chart toodisplay hello values of hello metrics at that point.</span></span>

![Наведите указатель мыши hello на диаграмме](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="f01d8-124">Суммарный Hello значение метрики hello в определенной точке за hello предшествующий интервала выборки.</span><span class="sxs-lookup"><span data-stu-id="f01d8-124">hello value of hello metric at a particular point is aggregated over hello preceding sampling interval.</span></span>

<span data-ttu-id="f01d8-125">интервал выборки Hello или «детализации» отображается вверху hello hello колонку.</span><span class="sxs-lookup"><span data-stu-id="f01d8-125">hello sampling interval or "granularity" is shown at hello top of hello blade.</span></span>

![заголовок колонки Hello.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="f01d8-127">Можно настроить гранулярность hello в колонке диапазон времени hello:</span><span class="sxs-lookup"><span data-stu-id="f01d8-127">You can adjust hello granularity in hello Time range blade:</span></span>

![заголовок колонки Hello.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="f01d8-129">Hello детализации доступны, зависят от выбранного диапазона времени hello.</span><span class="sxs-lookup"><span data-stu-id="f01d8-129">hello granularities available depend on hello time range you select.</span></span> <span data-ttu-id="f01d8-130">явные детализаций Hello являются гранулярности «automatic» toohello альтернативные варианты для hello временного диапазона.</span><span class="sxs-lookup"><span data-stu-id="f01d8-130">hello explicit granularities are alternatives toohello "automatic" granularity for hello time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="f01d8-131">Изменение диаграмм и сеток</span><span class="sxs-lookup"><span data-stu-id="f01d8-131">Editing charts and grids</span></span>
<span data-ttu-id="f01d8-132">tooadd Новая колонка toohello диаграммы:</span><span class="sxs-lookup"><span data-stu-id="f01d8-132">tooadd a new chart toohello blade:</span></span>

![В обозревателе метрик выберите "Добавить диаграмму"](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="f01d8-134">Выберите **изменить** на существующем или новом tooedit диаграммы что оно отображается:</span><span class="sxs-lookup"><span data-stu-id="f01d8-134">Select **Edit** on an existing or new chart tooedit what it shows:</span></span>

![Выберите одну или несколько метрик](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="f01d8-136">Более одной метрики можно отображать на диаграмме, хотя и существуют ограничения, о сочетаниях hello, которые могут быть отображены вместе.</span><span class="sxs-lookup"><span data-stu-id="f01d8-136">You can display more than one metric on a chart, though there are restrictions about hello combinations that can be displayed together.</span></span> <span data-ttu-id="f01d8-137">Как только выборе одной метрики, некоторые приветствия остальные отключены.</span><span class="sxs-lookup"><span data-stu-id="f01d8-137">As soon as you choose one metric, some of hello others are disabled.</span></span>

<span data-ttu-id="f01d8-138">Если в коде [настраиваемых метрик] [ track] в веб-приложения (вызовы tooTrackMetric и TrackEvent) они будут указаны здесь.</span><span class="sxs-lookup"><span data-stu-id="f01d8-138">If you coded [custom metrics][track] into your app (calls tooTrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="f01d8-139">Сегментация данных</span><span class="sxs-lookup"><span data-stu-id="f01d8-139">Segment your data</span></span>
<span data-ttu-id="f01d8-140">Вы можете разделить метрики, свойство — например, toocompare просмотров страниц клиентов с разными операционными системами.</span><span class="sxs-lookup"><span data-stu-id="f01d8-140">You can split a metric by property - for example, toocompare page views on clients with different operating systems.</span></span>

<span data-ttu-id="f01d8-141">Выбрать диаграммы или сетки, переключитесь на группирования и выберите свойство toogroup по:</span><span class="sxs-lookup"><span data-stu-id="f01d8-141">Select a chart or grid, switch on grouping and pick a property toogroup by:</span></span>

![Выберите "Объекты группировки", затем выберите свойство в списке "Группировать по"](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="f01d8-143">При использовании группирования hello типы областей и линейчатой диаграммы отображают с накоплением.</span><span class="sxs-lookup"><span data-stu-id="f01d8-143">When you use grouping, hello Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="f01d8-144">Такой подход удобно применять, где hello метод агрегирования является Sum.</span><span class="sxs-lookup"><span data-stu-id="f01d8-144">This is suitable where hello Aggregation method is Sum.</span></span> <span data-ttu-id="f01d8-145">Однако там, где используется тип агрегирования hello среднее, выбрать типы отображения hello линий или сетки.</span><span class="sxs-lookup"><span data-stu-id="f01d8-145">But where hello aggregation type is Average, choose hello Line or Grid display types.</span></span>
>
>

<span data-ttu-id="f01d8-146">Если в коде [настраиваемых метрик] [ track] в приложения и они включают значения свойств, вас могут tooselect hello свойство в списке hello.</span><span class="sxs-lookup"><span data-stu-id="f01d8-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able tooselect hello property in hello list.</span></span>

<span data-ttu-id="f01d8-147">Диаграмма hello слишком мал для сегментов данных?</span><span class="sxs-lookup"><span data-stu-id="f01d8-147">Is hello chart too small for segmented data?</span></span> <span data-ttu-id="f01d8-148">Измените ее высоту:</span><span class="sxs-lookup"><span data-stu-id="f01d8-148">Adjust its height:</span></span>

![Переместите ползунок hello](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="f01d8-150">Типы агрегата</span><span class="sxs-lookup"><span data-stu-id="f01d8-150">Aggregation types</span></span>
<span data-ttu-id="f01d8-151">условные обозначения Hello hello стороны по умолчанию обычно отображается значение hello статистическая обработка за период hello hello диаграммы.</span><span class="sxs-lookup"><span data-stu-id="f01d8-151">hello legend at hello side by default usually shows hello aggregated value over hello period of hello chart.</span></span> <span data-ttu-id="f01d8-152">При наведении указателя мыши на диаграмме hello hello значение показано на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="f01d8-152">If you hover over hello chart, it shows hello value at that point.</span></span>

<span data-ttu-id="f01d8-153">Каждой точке данных на диаграмме hello является hello значения данных, полученных в hello предыдущей выборки интервала или «детализации».</span><span class="sxs-lookup"><span data-stu-id="f01d8-153">Each data point on hello chart is an aggregate of hello data values received in hello preceding sampling interval or "granularity".</span></span> <span data-ttu-id="f01d8-154">Гранулярность Hello отображается hello верхней части колонки hello и зависит от hello общая шкала времени hello диаграммы.</span><span class="sxs-lookup"><span data-stu-id="f01d8-154">hello granularity is shown at hello top of hello blade, and varies with hello overall timescale of hello chart.</span></span>

<span data-ttu-id="f01d8-155">Метрики можно вычислять различными способами.</span><span class="sxs-lookup"><span data-stu-id="f01d8-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="f01d8-156">**Число** представляет собой число hello событий, полученных в интервале выборки hello.</span><span class="sxs-lookup"><span data-stu-id="f01d8-156">**Count** is a count of hello events received in hello sampling interval.</span></span> <span data-ttu-id="f01d8-157">Используется для событий, таких как запросы.</span><span class="sxs-lookup"><span data-stu-id="f01d8-157">It is used for events such as requests.</span></span> <span data-ttu-id="f01d8-158">Различные виды hello высотой диаграммы hello указывает вариации в hello скорость, с которой происходят hello.</span><span class="sxs-lookup"><span data-stu-id="f01d8-158">Variations in hello height of hello chart indicates variations in hello rate at which hello events occur.</span></span> <span data-ttu-id="f01d8-159">Но Обратите внимание, что числовое значение hello изменяется при изменении интервала выборки hello.</span><span class="sxs-lookup"><span data-stu-id="f01d8-159">But note that hello numeric value changes when you change hello sampling interval.</span></span>
* <span data-ttu-id="f01d8-160">**Сумма** складывает значения hello всех точек данных hello, полученные через интервал выборки hello, или период hello hello диаграммы.</span><span class="sxs-lookup"><span data-stu-id="f01d8-160">**Sum** adds up hello values of all hello data points received over hello sampling interval, or hello period of hello chart.</span></span>
* <span data-ttu-id="f01d8-161">**Среднее** разделяет hello сумма hello число точек данных, полученных через интервал приветствия.</span><span class="sxs-lookup"><span data-stu-id="f01d8-161">**Average** divides hello Sum by hello number of data points received over hello interval.</span></span>
* <span data-ttu-id="f01d8-162">**Уникальные** : использование счетчиков для подсчета количества пользователей и учетных записей.</span><span class="sxs-lookup"><span data-stu-id="f01d8-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="f01d8-163">За интервал выборки hello, или в течение периода hello hello диаграммы hello рисунке hello количество различных пользователей, в то время.</span><span class="sxs-lookup"><span data-stu-id="f01d8-163">Over hello sampling interval, or over hello period of hello chart, hello figure shows hello count of different users seen in that time.</span></span>
* <span data-ttu-id="f01d8-164">**%** — версии со значением каждого агрегата в процентах применяются только в сегментированных диаграммах.</span><span class="sxs-lookup"><span data-stu-id="f01d8-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="f01d8-165">всегда Hello общий суммирует too100% и hello диаграмма показывает относительный вклад hello всего различных компонентов.</span><span class="sxs-lookup"><span data-stu-id="f01d8-165">hello total always adds up too100%, and hello chart shows hello relative contribution of different components of a total.</span></span>

    ![Процентный агрегат](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a><span data-ttu-id="f01d8-167">Измените тип статистической обработки hello</span><span class="sxs-lookup"><span data-stu-id="f01d8-167">Change hello aggregation type</span></span>

![Изменение диаграммы hello, а затем выберите статистической обработки](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="f01d8-169">метод по умолчанию Hello для каждой метрики отображается при создании новой диаграммы или при отмене выбора все метрики:</span><span class="sxs-lookup"><span data-stu-id="f01d8-169">hello default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Отмените выбор значений по умолчанию hello toosee все метрики](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="f01d8-171">Закрепление оси Y</span><span class="sxs-lookup"><span data-stu-id="f01d8-171">Pin Y-axis</span></span> 
<span data-ttu-id="f01d8-172">По умолчанию на диаграмме отображается значений оси Y, начиная от нуля до максимального значения диапазона данных hello, toogive визуальное представление такта hello значений.</span><span class="sxs-lookup"><span data-stu-id="f01d8-172">By default a chart shows Y axis values starting from zero till maximum values in hello data range, toogive a visual representation of quantum of hello values.</span></span> <span data-ttu-id="f01d8-173">Но в некоторых случаях больше, чем может быть интересно toovisually такта hello проверять небольшие изменения в значения.</span><span class="sxs-lookup"><span data-stu-id="f01d8-173">But in some cases more than hello quantum it might be interesting toovisually inspect minor changes in values.</span></span> <span data-ttu-id="f01d8-174">Для настройки, таких как такое использование hello оси y диапазона редактирования функция toopin hello оси y минимального или максимального значения в нужном месте.</span><span class="sxs-lookup"><span data-stu-id="f01d8-174">For customizations like this use hello Y-axis range editing feature toopin hello Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="f01d8-175">Щелкните «Дополнительные параметры» флажок toobring копирование hello диапазон оси y параметры</span><span class="sxs-lookup"><span data-stu-id="f01d8-175">Click on "Advanced Settings" check box toobring up hello Y-axis range Settings</span></span>

![Щелкните "Дополнительные параметры", выберите "Настраиваемый диапазон" и укажите минимальное и максимальное значения.](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="f01d8-177">Фильтрация данных</span><span class="sxs-lookup"><span data-stu-id="f01d8-177">Filter your data</span></span>
<span data-ttu-id="f01d8-178">toosee просто hello метрики для выбранного набора значений свойств.</span><span class="sxs-lookup"><span data-stu-id="f01d8-178">toosee just hello metrics for a selected set of property values:</span></span>

![Щелкните "Фильтр", разверните свойство и проверьте некоторые значения](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="f01d8-180">Если не выбрать значения для конкретного свойства, он имеет hello таким же как при выборе их все: нет фильтра для этого свойства.</span><span class="sxs-lookup"><span data-stu-id="f01d8-180">If you don't select any values for a particular property, it's hello same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="f01d8-181">Обратите внимание hello подсчитывает событий вместе с каждого значения свойства.</span><span class="sxs-lookup"><span data-stu-id="f01d8-181">Notice hello counts of events alongside each property value.</span></span> <span data-ttu-id="f01d8-182">При выборе значения одного свойства hello подсчитывает наряду с другими значения настраиваются свойства.</span><span class="sxs-lookup"><span data-stu-id="f01d8-182">When you select values of one property, hello counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="f01d8-183">Фильтры применяются tooall hello диаграммы в колонке.</span><span class="sxs-lookup"><span data-stu-id="f01d8-183">Filters apply tooall hello charts on a blade.</span></span> <span data-ttu-id="f01d8-184">Если требуется, чтобы применить различные фильтры toodifferent диаграммы, создайте и сохраните колонках различных показателей.</span><span class="sxs-lookup"><span data-stu-id="f01d8-184">If you want different filters applied toodifferent charts, create and save different metrics blades.</span></span> <span data-ttu-id="f01d8-185">Если требуется, диаграммы с разных колонках toohello панели мониторинга, можно закрепить, чтобы можно было видеть их рядом друг с другом.</span><span class="sxs-lookup"><span data-stu-id="f01d8-185">If you want, you can pin charts from different blades toohello dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="f01d8-186">Исключение программ-роботов и веб-тест трафика</span><span class="sxs-lookup"><span data-stu-id="f01d8-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="f01d8-187">Использовать фильтр hello **реальный или искуственный трафик** и проверьте **реальные**.</span><span class="sxs-lookup"><span data-stu-id="f01d8-187">Use hello filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="f01d8-188">Также можно фильтровать по **источнику искусственного трафика**.</span><span class="sxs-lookup"><span data-stu-id="f01d8-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="tooadd-properties-toohello-filter-list"></a><span data-ttu-id="f01d8-189">Список фильтров toohello свойства tooadd</span><span class="sxs-lookup"><span data-stu-id="f01d8-189">tooadd properties toohello filter list</span></span>
<span data-ttu-id="f01d8-190">Вы хотите toofilter телеметрии на собственный выбор категории?</span><span class="sxs-lookup"><span data-stu-id="f01d8-190">Would you like toofilter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="f01d8-191">Например, вы распределили пользователей по различным категориям и хотели бы сегментировать данные по этим категориям.</span><span class="sxs-lookup"><span data-stu-id="f01d8-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="f01d8-192">[Создайте собственное свойство](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="f01d8-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="f01d8-193">Установите его в [инициализатора телеметрии](app-insights-api-custom-events-metrics.md#defaults) toohave, он отображается в все данные телеметрии - включая стандартной телеметрии hello отправленных различными модулями SDK.</span><span class="sxs-lookup"><span data-stu-id="f01d8-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) toohave it appear in all telemetry - including hello standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-hello-chart-type"></a><span data-ttu-id="f01d8-194">Изменить тип диаграммы hello</span><span class="sxs-lookup"><span data-stu-id="f01d8-194">Edit hello chart type</span></span>
<span data-ttu-id="f01d8-195">Обратите внимание, что можно переключаться между сетками и диаграммами.</span><span class="sxs-lookup"><span data-stu-id="f01d8-195">Notice that you can switch between grids and graphs:</span></span>

![Выберите сетку или диаграмму, затем выберите тип диаграммы](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="f01d8-197">Сохранение колонки метрик</span><span class="sxs-lookup"><span data-stu-id="f01d8-197">Save your metrics blade</span></span>
<span data-ttu-id="f01d8-198">После создания диаграммы ее можно сохранить в список избранного.</span><span class="sxs-lookup"><span data-stu-id="f01d8-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="f01d8-199">Можно ли tooshare его с другими членами группы, если вы используете учетную запись организации.</span><span class="sxs-lookup"><span data-stu-id="f01d8-199">You can choose whether tooshare it with other team members, if you use an organizational account.</span></span>

![Выберите "Избранное"](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="f01d8-201">toosee еще раз, в колонке hello **колонке Обзор перейдите toohello** и открыть Избранное:</span><span class="sxs-lookup"><span data-stu-id="f01d8-201">toosee hello blade again, **go toohello overview blade** and open Favorites:</span></span>

![В колонке Обзор hello выберите "Избранное"](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="f01d8-203">Если при сохранении относительный временной диапазон, колонке hello обновляется с последней метрики hello.</span><span class="sxs-lookup"><span data-stu-id="f01d8-203">If you chose Relative time range when you saved, hello blade will be updated with hello latest metrics.</span></span> <span data-ttu-id="f01d8-204">Если выбрана абсолютный временной диапазон, она будет отображаться hello и те же данные каждый раз.</span><span class="sxs-lookup"><span data-stu-id="f01d8-204">If you chose Absolute time range, it will show hello same data every time.</span></span>

## <a name="reset-hello-blade"></a><span data-ttu-id="f01d8-205">Сброс колонке hello</span><span class="sxs-lookup"><span data-stu-id="f01d8-205">Reset hello blade</span></span>
<span data-ttu-id="f01d8-206">Если изменить стоечный модуль, но затем хотелось бы tooget задней toohello исходного сохранен набор, просто щелкните сброса.</span><span class="sxs-lookup"><span data-stu-id="f01d8-206">If you edit a blade but then you'd like tooget back toohello original saved set, just click Reset.</span></span>

![В списке hello кнопки вверху hello метрика обозревателя](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="f01d8-208">Live Metrics Stream</span><span class="sxs-lookup"><span data-stu-id="f01d8-208">Live metrics stream</span></span>

<span data-ttu-id="f01d8-209">Чтобы получить мгновенное представление телеметрии, откройте [Live Stream](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="f01d8-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="f01d8-210">Большинство метрики занять tooappear несколько минут, из-за hello процесс статистической обработки.</span><span class="sxs-lookup"><span data-stu-id="f01d8-210">Most metrics take a few minutes tooappear, because of hello process of aggregation.</span></span> <span data-ttu-id="f01d8-211">В противоположность этому динамические метрики оптимизированы для отображения с малой задержкой.</span><span class="sxs-lookup"><span data-stu-id="f01d8-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="f01d8-212">Задание предупреждений</span><span class="sxs-lookup"><span data-stu-id="f01d8-212">Set alerts</span></span>
<span data-ttu-id="f01d8-213">уведомления по электронной почте о необычных значениях метрик, toobe добавить оповещение.</span><span class="sxs-lookup"><span data-stu-id="f01d8-213">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="f01d8-214">Вы можете Администраторы учетных записей электронной почты toohello для toosend hello или toospecific адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f01d8-214">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![В обозревателе метрик выберите последовательно «Правила предупреждений», «Добавить предупреждение»](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="f01d8-216">[Дополнительные сведения об оповещениях][alerts].</span><span class="sxs-lookup"><span data-stu-id="f01d8-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="f01d8-217">Непрерывный экспорт</span><span class="sxs-lookup"><span data-stu-id="f01d8-217">Continuous Export</span></span>
<span data-ttu-id="f01d8-218">Если необходимо постоянно экспортировать данные для внешней обработки, используйте [непрерывный экспорт](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="f01d8-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="f01d8-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="f01d8-219">Power BI</span></span>
<span data-ttu-id="f01d8-220">Если требуется более широких представлений данных, вы можете [Экспорт tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="f01d8-220">If you want even richer views of your data, you can [export tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="f01d8-221">Аналитика</span><span class="sxs-lookup"><span data-stu-id="f01d8-221">Analytics</span></span>
<span data-ttu-id="f01d8-222">[Аналитика](app-insights-analytics.md) является более гибким tooanalyze способом телеметрии на любом языке запросами.</span><span class="sxs-lookup"><span data-stu-id="f01d8-222">[Analytics](app-insights-analytics.md) is a more versatile way tooanalyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="f01d8-223">Используйте его, если хотите toocombine или вычислений Результаты метрик или выполнить глубоком изучении последних производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="f01d8-223">Use it if you want toocombine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="f01d8-224">В диаграмму показатель можно щелкнуть значок tooget hello Analytics непосредственно toohello эквивалентные аналитического запроса.</span><span class="sxs-lookup"><span data-stu-id="f01d8-224">From a metric chart, you can click hello Analytics icon tooget directly toohello equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f01d8-225">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f01d8-225">Troubleshooting</span></span>
<span data-ttu-id="f01d8-226">*Данные не отображаются на диаграмме.*</span><span class="sxs-lookup"><span data-stu-id="f01d8-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="f01d8-227">Фильтры применяются tooall hello диаграммы в колонке hello.</span><span class="sxs-lookup"><span data-stu-id="f01d8-227">Filters apply tooall hello charts on hello blade.</span></span> <span data-ttu-id="f01d8-228">Убедитесь, что, хотя объектами на одной диаграмме, не удалось установить фильтр, который исключает все данные hello на другом.</span><span class="sxs-lookup"><span data-stu-id="f01d8-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all hello data on another.</span></span>

    <span data-ttu-id="f01d8-229">Tooset различные фильтры на различных диаграммах, создайте их в разных колонках, сохраните их как отдельные "Избранное".</span><span class="sxs-lookup"><span data-stu-id="f01d8-229">If you want tooset different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="f01d8-230">Если требуется, можно закрепить их toohello панели мониторинга, чтобы можно было видеть их рядом друг с другом.</span><span class="sxs-lookup"><span data-stu-id="f01d8-230">If you want, you can pin them toohello dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="f01d8-231">Если диаграммы группируются по свойства, которое не определено на метрику hello, затем будет существовать ничего не на диаграмме hello.</span><span class="sxs-lookup"><span data-stu-id="f01d8-231">If you group a chart by a property that is not defined on hello metric, then there will be nothing on hello chart.</span></span> <span data-ttu-id="f01d8-232">Попробуйте убрать группировку или выберите другое свойство для группировки.</span><span class="sxs-lookup"><span data-stu-id="f01d8-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="f01d8-233">Данные о производительности (ЦП, скорость ввода-вывода и т. д.) доступны для веб-служб Java, классических приложений Windows, [веб-приложений и служб IIS, если установлен монитор состояния](app-insights-monitor-performance-live-website-now.md), а также [облачных служб Azure](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f01d8-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="f01d8-234">Такие данные для веб-сайтов Azure недоступны.</span><span class="sxs-lookup"><span data-stu-id="f01d8-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="f01d8-235">Видео</span><span class="sxs-lookup"><span data-stu-id="f01d8-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="f01d8-236">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f01d8-236">Next steps</span></span>
* [<span data-ttu-id="f01d8-237">Отслеживание использования Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f01d8-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="f01d8-238">Использование диагностического поиска</span><span class="sxs-lookup"><span data-stu-id="f01d8-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
