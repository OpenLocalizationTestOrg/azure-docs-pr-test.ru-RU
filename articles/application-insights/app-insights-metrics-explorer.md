---
title: "Изучение метрик в Azure Application Insights | Документация Майкрософт"
description: "Способ интерпретации диаграмм в обозревателе метрик и настройки колонок обозревателя метрик."
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
ms.openlocfilehash: a13500284caab79bbe221060ccf3d925ffb1fab5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="19153-103">Исследование метрик в Application Insights</span><span class="sxs-lookup"><span data-stu-id="19153-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="19153-104">Метрики в [Application Insights][start] — это измеренные значения и счетчики событий, которые передаются как данные телеметрии из приложения.</span><span class="sxs-lookup"><span data-stu-id="19153-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="19153-105">Они помогают обнаруживать проблемы производительности и отслеживать тенденции в использовании приложения.</span><span class="sxs-lookup"><span data-stu-id="19153-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="19153-106">Существует широкий спектр стандартных метрик, и можно также создавать собственные пользовательские метрики и события.</span><span class="sxs-lookup"><span data-stu-id="19153-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="19153-107">Метрики и счетчики событий отображаются в диаграммах агрегированных значений, например как сумма, среднее или количество.</span><span class="sxs-lookup"><span data-stu-id="19153-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="19153-108">Вот пример набора диаграмм:</span><span class="sxs-lookup"><span data-stu-id="19153-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="19153-109">Диаграммы метрик повсеместно используются на портале Application Insights.</span><span class="sxs-lookup"><span data-stu-id="19153-109">You find metrics charts everywhere in the Application Insights portal.</span></span> <span data-ttu-id="19153-110">В большинстве случаев их можно настраивать, а также добавлять в колонку дополнительные диаграммы.</span><span class="sxs-lookup"><span data-stu-id="19153-110">In most cases, they can be customized, and you can add more charts to the blade.</span></span> <span data-ttu-id="19153-111">В колонке "Обзор" щелкните более подробные диаграммы (которые имеют заголовки, такие как "Сервер") или воспользуйтесь **обозревателем метрик**, чтобы открыть новую колонку, в которой можно создавать настраиваемые диаграммы.</span><span class="sxs-lookup"><span data-stu-id="19153-111">From the Overview blade, click through to more detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** to open a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="19153-112">Диапазон времени</span><span class="sxs-lookup"><span data-stu-id="19153-112">Time range</span></span>
<span data-ttu-id="19153-113">В любой колонке можно изменить диапазон времени, охватываемый диаграммами или сетками.</span><span class="sxs-lookup"><span data-stu-id="19153-113">You can change the Time range covered by the charts or grids on any blade.</span></span>

![Откройте колонку обзора приложения на портале Azure](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="19153-115">Если ожидаются некоторые данные, которые еще не отобразились, нажмите кнопку "Обновить".</span><span class="sxs-lookup"><span data-stu-id="19153-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="19153-116">Диаграммы самостоятельно обновляются через определенные интервалы, однако интервалы становятся длиннее при использовании более крупных временных отрезков.</span><span class="sxs-lookup"><span data-stu-id="19153-116">Charts refresh themselves at intervals, but the intervals are longer for larger time ranges.</span></span> <span data-ttu-id="19153-117">Может потребоваться некоторое время, чтобы данные были переданы через конвейер анализа в диаграмму.</span><span class="sxs-lookup"><span data-stu-id="19153-117">It can take a while for data to come through the analysis pipeline onto a chart.</span></span>

<span data-ttu-id="19153-118">Чтобы увеличить часть диаграммы, перетащите ее:</span><span class="sxs-lookup"><span data-stu-id="19153-118">To zoom into part of a chart, drag over it:</span></span>

![Перетащите часть диаграммы.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="19153-120">Чтобы восстановить первоначальный масштаб, нажмите кнопку Undo Zoom (Отменить изменение масштаба).</span><span class="sxs-lookup"><span data-stu-id="19153-120">Click the Undo Zoom button to restore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="19153-121">Детализация и значения точек</span><span class="sxs-lookup"><span data-stu-id="19153-121">Granularity and point values</span></span>
<span data-ttu-id="19153-122">Наведите указатель мыши на диаграммы для отображения значений метрик в той точке.</span><span class="sxs-lookup"><span data-stu-id="19153-122">Hover your mouse over the chart to display the values of the metrics at that point.</span></span>

![Наведите указатель мыши на диаграмму](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="19153-124">Значение метрики в определенной точке определяется как результат статистического вычисления за предыдущий интервал выборки.</span><span class="sxs-lookup"><span data-stu-id="19153-124">The value of the metric at a particular point is aggregated over the preceding sampling interval.</span></span>

<span data-ttu-id="19153-125">Интервал выборки, или «степень детализации», отображается в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="19153-125">The sampling interval or "granularity" is shown at the top of the blade.</span></span>

![Заголовок колонки.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="19153-127">Степень детализации можно настроить в колонке временного диапазона:</span><span class="sxs-lookup"><span data-stu-id="19153-127">You can adjust the granularity in the Time range blade:</span></span>

![Заголовок колонки.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="19153-129">Доступные степени детализации зависят от выбранного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="19153-129">The granularities available depend on the time range you select.</span></span> <span data-ttu-id="19153-130">Вместо автоматической степени детализации для интервала времени можно выбрать явную степень детализации.</span><span class="sxs-lookup"><span data-stu-id="19153-130">The explicit granularities are alternatives to the "automatic" granularity for the time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="19153-131">Изменение диаграмм и сеток</span><span class="sxs-lookup"><span data-stu-id="19153-131">Editing charts and grids</span></span>
<span data-ttu-id="19153-132">Добавление новой диаграммы в колонку:</span><span class="sxs-lookup"><span data-stu-id="19153-132">To add a new chart to the blade:</span></span>

![В обозревателе метрик выберите "Добавить диаграмму"](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="19153-134">Вы можете **изменить** существующую или создать новую диаграмму для редактирования отображаемых данных.</span><span class="sxs-lookup"><span data-stu-id="19153-134">Select **Edit** on an existing or new chart to edit what it shows:</span></span>

![Выберите одну или несколько метрик](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="19153-136">Можно отобразить более одной метрики на диаграмме, хотя существуют ограничения по сочетаниям, которые могут отображаться одновременно.</span><span class="sxs-lookup"><span data-stu-id="19153-136">You can display more than one metric on a chart, though there are restrictions about the combinations that can be displayed together.</span></span> <span data-ttu-id="19153-137">Когда выбрана одна метрика, некоторые другие становятся недоступными.</span><span class="sxs-lookup"><span data-stu-id="19153-137">As soon as you choose one metric, some of the others are disabled.</span></span>

<span data-ttu-id="19153-138">Если [пользовательские метрики][track] были добавлены в код приложения (вызовы TrackMetric и TrackEvent), то они будут перечислены здесь.</span><span class="sxs-lookup"><span data-stu-id="19153-138">If you coded [custom metrics][track] into your app (calls to TrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="19153-139">Сегментация данных</span><span class="sxs-lookup"><span data-stu-id="19153-139">Segment your data</span></span>
<span data-ttu-id="19153-140">Можно разделить метрику по свойствам — например, для сравнения просмотров страниц на клиентах с разными операционными системами.</span><span class="sxs-lookup"><span data-stu-id="19153-140">You can split a metric by property - for example, to compare page views on clients with different operating systems.</span></span>

<span data-ttu-id="19153-141">Выберите диаграмму или сетку, переключитесь на группировку и выберите свойство для группировки:</span><span class="sxs-lookup"><span data-stu-id="19153-141">Select a chart or grid, switch on grouping and pick a property to group by:</span></span>

![Выберите "Объекты группировки", затем выберите свойство в списке "Группировать по"](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="19153-143">При использовании группирования диаграммы с областями и линейчатые диаграммы отображают данные с накоплением.</span><span class="sxs-lookup"><span data-stu-id="19153-143">When you use grouping, the Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="19153-144">Это удобно, когда методом агрегирования является "Сумма".</span><span class="sxs-lookup"><span data-stu-id="19153-144">This is suitable where the Aggregation method is Sum.</span></span> <span data-ttu-id="19153-145">Но если методом агрегирования является "Среднее", выберите отображение линий или сетки.</span><span class="sxs-lookup"><span data-stu-id="19153-145">But where the aggregation type is Average, choose the Line or Grid display types.</span></span>
>
>

<span data-ttu-id="19153-146">Если [пользовательские метрики][track] были добавлены в код приложения и включают значения свойств, то в списке можно будет выбрать соответствующее свойство.</span><span class="sxs-lookup"><span data-stu-id="19153-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able to select the property in the list.</span></span>

<span data-ttu-id="19153-147">Диаграмма слишком мала для сегментации данных?</span><span class="sxs-lookup"><span data-stu-id="19153-147">Is the chart too small for segmented data?</span></span> <span data-ttu-id="19153-148">Измените ее высоту:</span><span class="sxs-lookup"><span data-stu-id="19153-148">Adjust its height:</span></span>

![Отрегулируйте положение ползунка](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="19153-150">Типы агрегата</span><span class="sxs-lookup"><span data-stu-id="19153-150">Aggregation types</span></span>
<span data-ttu-id="19153-151">В условных обозначениях сбоку по умолчанию отображается значение, вычисленное для периода диаграммы.</span><span class="sxs-lookup"><span data-stu-id="19153-151">The legend at the side by default usually shows the aggregated value over the period of the chart.</span></span> <span data-ttu-id="19153-152">При наведении указателя мыши на какую-либо точку диаграммы отображается значение в этой точке.</span><span class="sxs-lookup"><span data-stu-id="19153-152">If you hover over the chart, it shows the value at that point.</span></span>

<span data-ttu-id="19153-153">Каждая точка данных на диаграмме вычисляется на основе значений данных, полученных на предыдущем интервале выборки (степени детализации).</span><span class="sxs-lookup"><span data-stu-id="19153-153">Each data point on the chart is an aggregate of the data values received in the preceding sampling interval or "granularity".</span></span> <span data-ttu-id="19153-154">Степень детализации отображается в верхней части колонки и зависит от общей шкалы времени диаграммы.</span><span class="sxs-lookup"><span data-stu-id="19153-154">The granularity is shown at the top of the blade, and varies with the overall timescale of the chart.</span></span>

<span data-ttu-id="19153-155">Метрики можно вычислять различными способами.</span><span class="sxs-lookup"><span data-stu-id="19153-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="19153-156">**Count** — счетчик событий, полученных в интервале выборки.</span><span class="sxs-lookup"><span data-stu-id="19153-156">**Count** is a count of the events received in the sampling interval.</span></span> <span data-ttu-id="19153-157">Используется для событий, таких как запросы.</span><span class="sxs-lookup"><span data-stu-id="19153-157">It is used for events such as requests.</span></span> <span data-ttu-id="19153-158">Изменения высоты диаграммы указывают на изменения частоты, с которой происходят события.</span><span class="sxs-lookup"><span data-stu-id="19153-158">Variations in the height of the chart indicates variations in the rate at which the events occur.</span></span> <span data-ttu-id="19153-159">Но обратите внимание, что числовое значение изменяется при изменении интервала выборки.</span><span class="sxs-lookup"><span data-stu-id="19153-159">But note that the numeric value changes when you change the sampling interval.</span></span>
* <span data-ttu-id="19153-160">**Сумма** : суммирование значений всех точек данных, полученных в течение интервала выборки (периода диаграммы).</span><span class="sxs-lookup"><span data-stu-id="19153-160">**Sum** adds up the values of all the data points received over the sampling interval, or the period of the chart.</span></span>
* <span data-ttu-id="19153-161">**Среднее** : деление значения "Сумма" на количество точек данных, полученных в течение интервала.</span><span class="sxs-lookup"><span data-stu-id="19153-161">**Average** divides the Sum by the number of data points received over the interval.</span></span>
* <span data-ttu-id="19153-162">**Уникальные** : использование счетчиков для подсчета количества пользователей и учетных записей.</span><span class="sxs-lookup"><span data-stu-id="19153-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="19153-163">На рисунке показано количество различных пользователей, обнаруженных в течение интервала выборки (периода диаграммы).</span><span class="sxs-lookup"><span data-stu-id="19153-163">Over the sampling interval, or over the period of the chart, the figure shows the count of different users seen in that time.</span></span>
* <span data-ttu-id="19153-164">**%** — версии со значением каждого агрегата в процентах применяются только в сегментированных диаграммах.</span><span class="sxs-lookup"><span data-stu-id="19153-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="19153-165">Общее значение всегда равно 100 %, а на диаграмме отображается относительный вклад каждого компонента.</span><span class="sxs-lookup"><span data-stu-id="19153-165">The total always adds up to 100%, and the chart shows the relative contribution of different components of a total.</span></span>

    ![Процентный агрегат](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-the-aggregation-type"></a><span data-ttu-id="19153-167">Изменение типа агрегата</span><span class="sxs-lookup"><span data-stu-id="19153-167">Change the aggregation type</span></span>

![Измените диаграмму, а затем выберите агрегат](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="19153-169">При создании диаграммы или при отмене выбора всех метрик отображается метод по умолчанию для каждой метрики.</span><span class="sxs-lookup"><span data-stu-id="19153-169">The default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Отмените выбор всех метрик, чтобы отобразить значения по умолчанию.](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="19153-171">Закрепление оси Y</span><span class="sxs-lookup"><span data-stu-id="19153-171">Pin Y-axis</span></span> 
<span data-ttu-id="19153-172">По умолчанию на диаграмме отображаются значения оси Y от нуля до максимального значения в диапазоне данных, чтобы наглядно представить квант времени значений.</span><span class="sxs-lookup"><span data-stu-id="19153-172">By default a chart shows Y axis values starting from zero till maximum values in the data range, to give a visual representation of quantum of the values.</span></span> <span data-ttu-id="19153-173">Но в некоторых случаях незначительные изменения в значениях могут представлять больший интерес для исследования, чем весь квант времени.</span><span class="sxs-lookup"><span data-stu-id="19153-173">But in some cases more than the quantum it might be interesting to visually inspect minor changes in values.</span></span> <span data-ttu-id="19153-174">Для подобных настроек используется функция изменения диапазона оси Y, позволяющая закрепить ее минимальное или максимальное значение в нужном месте.</span><span class="sxs-lookup"><span data-stu-id="19153-174">For customizations like this use the Y-axis range editing feature to pin the Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="19153-175">Установите флажок "Дополнительные параметры", чтобы открыть параметры диапазона оси Y.</span><span class="sxs-lookup"><span data-stu-id="19153-175">Click on "Advanced Settings" check box to bring up the Y-axis range Settings</span></span>

![Щелкните "Дополнительные параметры", выберите "Настраиваемый диапазон" и укажите минимальное и максимальное значения.](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="19153-177">Фильтрация данных</span><span class="sxs-lookup"><span data-stu-id="19153-177">Filter your data</span></span>
<span data-ttu-id="19153-178">Просмотр метрик только для выбранного набора значений свойства</span><span class="sxs-lookup"><span data-stu-id="19153-178">To see just the metrics for a selected set of property values:</span></span>

![Щелкните "Фильтр", разверните свойство и проверьте некоторые значения](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="19153-180">Если не выбирать какие-либо значения для конкретного свойства, это будет аналогично выбору их всех: нет фильтра по этому свойству.</span><span class="sxs-lookup"><span data-stu-id="19153-180">If you don't select any values for a particular property, it's the same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="19153-181">Обратите внимание на счетчики событий рядом с каждым значением свойства.</span><span class="sxs-lookup"><span data-stu-id="19153-181">Notice the counts of events alongside each property value.</span></span> <span data-ttu-id="19153-182">При выборе значений одного свойства счетчики, находящиеся рядом со значениями других свойств, корректируются.</span><span class="sxs-lookup"><span data-stu-id="19153-182">When you select values of one property, the counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="19153-183">Фильтры применяются ко всем диаграммам в колонке.</span><span class="sxs-lookup"><span data-stu-id="19153-183">Filters apply to all the charts on a blade.</span></span> <span data-ttu-id="19153-184">Если требуется применить разные фильтры к различным диаграммам, отдельно создайте и сохраните соответствующие колонки метрик.</span><span class="sxs-lookup"><span data-stu-id="19153-184">If you want different filters applied to different charts, create and save different metrics blades.</span></span> <span data-ttu-id="19153-185">Если необходимо, вы можете закрепить диаграммы из разных колонок на панели мониторинга, чтобы их можно было видеть вместе.</span><span class="sxs-lookup"><span data-stu-id="19153-185">If you want, you can pin charts from different blades to the dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="19153-186">Исключение программ-роботов и веб-тест трафика</span><span class="sxs-lookup"><span data-stu-id="19153-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="19153-187">Используйте фильтр **Реальный или искусственный трафик** и установите флажок **Реальный**.</span><span class="sxs-lookup"><span data-stu-id="19153-187">Use the filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="19153-188">Также можно фильтровать по **источнику искусственного трафика**.</span><span class="sxs-lookup"><span data-stu-id="19153-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="to-add-properties-to-the-filter-list"></a><span data-ttu-id="19153-189">Добавление свойств в список фильтров</span><span class="sxs-lookup"><span data-stu-id="19153-189">To add properties to the filter list</span></span>
<span data-ttu-id="19153-190">Вам необходимо фильтровать данные телеметрии по выбранным вами категориям?</span><span class="sxs-lookup"><span data-stu-id="19153-190">Would you like to filter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="19153-191">Например, вы распределили пользователей по различным категориям и хотели бы сегментировать данные по этим категориям.</span><span class="sxs-lookup"><span data-stu-id="19153-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="19153-192">[Создайте собственное свойство](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="19153-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="19153-193">Задайте его в [инициализаторе телеметрии](app-insights-api-custom-events-metrics.md#defaults) , чтобы оно было включено во все данные телеметрии, включая стандартные данные телеметрии, отправляемые различными модулями SDK.</span><span class="sxs-lookup"><span data-stu-id="19153-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) to have it appear in all telemetry - including the standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-the-chart-type"></a><span data-ttu-id="19153-194">Изменение типа диаграммы</span><span class="sxs-lookup"><span data-stu-id="19153-194">Edit the chart type</span></span>
<span data-ttu-id="19153-195">Обратите внимание, что можно переключаться между сетками и диаграммами.</span><span class="sxs-lookup"><span data-stu-id="19153-195">Notice that you can switch between grids and graphs:</span></span>

![Выберите сетку или диаграмму, затем выберите тип диаграммы](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="19153-197">Сохранение колонки метрик</span><span class="sxs-lookup"><span data-stu-id="19153-197">Save your metrics blade</span></span>
<span data-ttu-id="19153-198">После создания диаграммы ее можно сохранить в список избранного.</span><span class="sxs-lookup"><span data-stu-id="19153-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="19153-199">При использовании учетной записи организации можно выбрать, будут ли другие члены команды иметь к ней доступ.</span><span class="sxs-lookup"><span data-stu-id="19153-199">You can choose whether to share it with other team members, if you use an organizational account.</span></span>

![Выберите "Избранное"](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="19153-201">Чтобы снова увидеть эту колонку, **перейдите в колонку "Обзор"** и откройте "Избранное":</span><span class="sxs-lookup"><span data-stu-id="19153-201">To see the blade again, **go to the overview blade** and open Favorites:</span></span>

![В колонке "Обзор" выберите "Избранное"](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="19153-203">Если выбрать относительный диапазон времени при сохранении, колонка будет обновлена с использованием последних метрик.</span><span class="sxs-lookup"><span data-stu-id="19153-203">If you chose Relative time range when you saved, the blade will be updated with the latest metrics.</span></span> <span data-ttu-id="19153-204">Если выбрать абсолютного диапазона времени, каждый раз будут отображаться те же данные.</span><span class="sxs-lookup"><span data-stu-id="19153-204">If you chose Absolute time range, it will show the same data every time.</span></span>

## <a name="reset-the-blade"></a><span data-ttu-id="19153-205">Сброс настроек колонки</span><span class="sxs-lookup"><span data-stu-id="19153-205">Reset the blade</span></span>
<span data-ttu-id="19153-206">Если после изменения колонки требуется вернуться к исходному  сохраненному набору параметров, просто нажмите кнопку сброса.</span><span class="sxs-lookup"><span data-stu-id="19153-206">If you edit a blade but then you'd like to get back to the original saved set, just click Reset.</span></span>

![В кнопках верхней части обозревателя метрик](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="19153-208">Live Metrics Stream</span><span class="sxs-lookup"><span data-stu-id="19153-208">Live metrics stream</span></span>

<span data-ttu-id="19153-209">Чтобы получить мгновенное представление телеметрии, откройте [Live Stream](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="19153-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="19153-210">Отображение большинства метрик занимает несколько минут из-за процесса агрегирования.</span><span class="sxs-lookup"><span data-stu-id="19153-210">Most metrics take a few minutes to appear, because of the process of aggregation.</span></span> <span data-ttu-id="19153-211">В противоположность этому динамические метрики оптимизированы для отображения с малой задержкой.</span><span class="sxs-lookup"><span data-stu-id="19153-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="19153-212">Задание предупреждений</span><span class="sxs-lookup"><span data-stu-id="19153-212">Set alerts</span></span>
<span data-ttu-id="19153-213">Чтобы получать уведомления по электронной почте о нетипичных значениях любой метрики, добавьте предупреждение.</span><span class="sxs-lookup"><span data-stu-id="19153-213">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="19153-214">Можно выбрать отправку либо по электронной почте администраторам учетной записи, либо на указанный электронный адрес.</span><span class="sxs-lookup"><span data-stu-id="19153-214">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![В обозревателе метрик выберите последовательно «Правила предупреждений», «Добавить предупреждение»](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="19153-216">[Дополнительные сведения об оповещениях][alerts].</span><span class="sxs-lookup"><span data-stu-id="19153-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="19153-217">Непрерывный экспорт</span><span class="sxs-lookup"><span data-stu-id="19153-217">Continuous Export</span></span>
<span data-ttu-id="19153-218">Если необходимо постоянно экспортировать данные для внешней обработки, используйте [непрерывный экспорт](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="19153-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="19153-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="19153-219">Power BI</span></span>
<span data-ttu-id="19153-220">Если вам нужны представления данных с еще большими возможностями, данные можно [экспортировать в Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="19153-220">If you want even richer views of your data, you can [export to Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="19153-221">Аналитика</span><span class="sxs-lookup"><span data-stu-id="19153-221">Analytics</span></span>
<span data-ttu-id="19153-222">[Аналитика](app-insights-analytics.md) является более гибким способом анализа телеметрии с помощью мощного языка запросов.</span><span class="sxs-lookup"><span data-stu-id="19153-222">[Analytics](app-insights-analytics.md) is a more versatile way to analyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="19153-223">Используйте ее, если требуется объединить или вычислить результаты метрик либо тщательно изучить последние данные производительности приложения.</span><span class="sxs-lookup"><span data-stu-id="19153-223">Use it if you want to combine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="19153-224">На диаграмме с метриками можно щелкнуть значок "Аналитика", чтобы перейти непосредственно к эквивалентному запросу "Аналитика".</span><span class="sxs-lookup"><span data-stu-id="19153-224">From a metric chart, you can click the Analytics icon to get directly to the equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="19153-225">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="19153-225">Troubleshooting</span></span>
<span data-ttu-id="19153-226">*Данные не отображаются на диаграмме.*</span><span class="sxs-lookup"><span data-stu-id="19153-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="19153-227">Фильтры применяются ко всем диаграммам в колонке.</span><span class="sxs-lookup"><span data-stu-id="19153-227">Filters apply to all the charts on the blade.</span></span> <span data-ttu-id="19153-228">Убедитесь, что, рассматривая какую-либо диаграмму, вы не задали фильтр, исключающий все данные на другой диаграмме.</span><span class="sxs-lookup"><span data-stu-id="19153-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all the data on another.</span></span>

    <span data-ttu-id="19153-229">Если вы хотите задать разные фильтры для различных диаграмм, создайте их на разных колонках и по отдельности сохраните в избранное.</span><span class="sxs-lookup"><span data-stu-id="19153-229">If you want to set different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="19153-230">Если необходимо, вы можете закрепить их на панели мониторинга, чтобы их можно было видеть вместе.</span><span class="sxs-lookup"><span data-stu-id="19153-230">If you want, you can pin them to the dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="19153-231">Если сгруппировать диаграмму по свойству, которое не определено в метрике, то на диаграмме ничего не отобразится.</span><span class="sxs-lookup"><span data-stu-id="19153-231">If you group a chart by a property that is not defined on the metric, then there will be nothing on the chart.</span></span> <span data-ttu-id="19153-232">Попробуйте убрать группировку или выберите другое свойство для группировки.</span><span class="sxs-lookup"><span data-stu-id="19153-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="19153-233">Данные о производительности (ЦП, скорость ввода-вывода и т. д.) доступны для веб-служб Java, классических приложений Windows, [веб-приложений и служб IIS, если установлен монитор состояния](app-insights-monitor-performance-live-website-now.md), а также [облачных служб Azure](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="19153-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="19153-234">Такие данные для веб-сайтов Azure недоступны.</span><span class="sxs-lookup"><span data-stu-id="19153-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="19153-235">Видео</span><span class="sxs-lookup"><span data-stu-id="19153-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="19153-236">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="19153-236">Next steps</span></span>
* [<span data-ttu-id="19153-237">Отслеживание использования Application Insights.</span><span class="sxs-lookup"><span data-stu-id="19153-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="19153-238">Использование диагностического поиска</span><span class="sxs-lookup"><span data-stu-id="19153-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
