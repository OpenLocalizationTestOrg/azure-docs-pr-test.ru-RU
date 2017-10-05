---
title: "Интеллектуальная диагностика изменений производительности веб-приложений в Azure Application Insights| Документы Майкрософт"
description: "Автоматическая диагностика пиков или шагов в данных телеметрии производительности из веб-приложения."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 5e53bc714d89bf6204681349e7890e0b8fbc7046
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="622d0-103">Диагностика внезапных изменений в телеметрии приложения</span><span class="sxs-lookup"><span data-stu-id="622d0-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="622d0-104">*Эта функция предоставляется в предварительной версии.*</span><span class="sxs-lookup"><span data-stu-id="622d0-104">*This feature is in preview.*</span></span>

<span data-ttu-id="622d0-105">Диагностируйте внезапные изменения производительности или использования веб-приложения одним щелчком мыши!</span><span class="sxs-lookup"><span data-stu-id="622d0-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="622d0-106">Функция интеллектуальной диагностики доступна при создании диаграммы времени в [Analytics](app-insights-analytics.md) в [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="622d0-106">The Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="622d0-107">При возникновении необычного отклонения от тенденций результатов, такого как пик или провал, интеллектуальная диагностика определяет шаблон измерений и связанные значения, которые могут объяснить такое изменение.</span><span class="sxs-lookup"><span data-stu-id="622d0-107">Wherever there is an unusual change from the trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain the change.</span></span> <span data-ttu-id="622d0-108">Это помогает быстро диагностировать проблему.</span><span class="sxs-lookup"><span data-stu-id="622d0-108">This helps you diagnose the problem quickly.</span></span> 

<span data-ttu-id="622d0-109">В этом примере интеллектуальная диагностика определила шаблон значений свойств, связанных с изменением, и выделила различие между результатами с таким шаблоном и без него:</span><span class="sxs-lookup"><span data-stu-id="622d0-109">In this example, Smart Diagnostics has identified a pattern of property values associated with the change, and highlights the difference between results with and without that pattern:</span></span>

![Пример результатов диагностики аналитики](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="622d0-111">Диагностика изменений данных</span><span class="sxs-lookup"><span data-stu-id="622d0-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="622d0-112">Выполните запрос в Analytics и отрисуйте его в виде диаграммы времени.</span><span class="sxs-lookup"><span data-stu-id="622d0-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="622d0-113">Щелкните любой из выделенных пиков, если он имеется.</span><span class="sxs-lookup"><span data-stu-id="622d0-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![пик](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="622d0-115">Функция диагностики тратит несколько секунд на выявление шаблона.</span><span class="sxs-lookup"><span data-stu-id="622d0-115">Diagnostics takes a few seconds to discover a pattern.</span></span>

3. <span data-ttu-id="622d0-116">На вкладке результатов диагностики отображается шаблон, который может выяснить неоднородность данных.</span><span class="sxs-lookup"><span data-stu-id="622d0-116">The Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="622d0-118">В тексте отображаются значения измерений, коррелирующих с изменением.</span><span class="sxs-lookup"><span data-stu-id="622d0-118">The text shows the dimension values that appear to correlate with the shift.</span></span> <span data-ttu-id="622d0-119">В этом примере оно связано с конкретным запросом и конкретной версией браузера.</span><span class="sxs-lookup"><span data-stu-id="622d0-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="622d0-120">Обратите внимание на два компонента диаграммы, у которых фильтр имеет значение true и false.</span><span class="sxs-lookup"><span data-stu-id="622d0-120">Notice also the two components of the chart, with the filter true and false.</span></span> <span data-ttu-id="622d0-121">Компонент со значением false показывает тренд без изменений.</span><span class="sxs-lookup"><span data-stu-id="622d0-121">The false component shows an unchanged trend.</span></span> <span data-ttu-id="622d0-122">Другими словами, результаты телеметрии не изменяются, если исключить проблемное сочетание измерений, выявленное функцией диагностики.</span><span class="sxs-lookup"><span data-stu-id="622d0-122">In other words, there is no change in the telemetry results, if we exclude the problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="622d0-123">Результаты в этом сочетании, напротив, показывают резкое изменение в выделенной области исследования.</span><span class="sxs-lookup"><span data-stu-id="622d0-123">By contrast, the results within that combination do show a dramatic change within the highlighted area of investigation.</span></span> <span data-ttu-id="622d0-124">Это указывает, что функция диагностики обнаружила сочетание свойств, описывающих изменение.</span><span class="sxs-lookup"><span data-stu-id="622d0-124">This shows that Diagnostics has found a combination of properties that explains the change.</span></span>

4.  <span data-ttu-id="622d0-125">Если шаблон сложный, нужно навести указатель мыши на элемент **Показать все** для просмотра измерений.</span><span class="sxs-lookup"><span data-stu-id="622d0-125">If the pattern is complex, you need to hover over **Show all** to see the dimensions.</span></span>

    ![показать все](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="622d0-127">Если функция диагностики не обнаруживает довольно значимый шаблон, отображается страница "Нет результатов".</span><span class="sxs-lookup"><span data-stu-id="622d0-127">In case Diagnostics finds no significant pattern to notify about, the ‘no results’ page will be presented.</span></span> <span data-ttu-id="622d0-128">На этом этапе запрос можно изменить.</span><span class="sxs-lookup"><span data-stu-id="622d0-128">At this point, you may change your query.</span></span> <span data-ttu-id="622d0-129">Например, можно сузить диапазон времени и группирование в запросе аналитики для дальнейшего анализа и потенциально лучших результатов.</span><span class="sxs-lookup"><span data-stu-id="622d0-129">For example, you could narrow the time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="622d0-130">Теперь, зная, что некоторая страница вашего веб-сайта вызывает проблемы в определенном браузере, вы можете перейти сразу к проблемной странице и изучить недавние изменения.</span><span class="sxs-lookup"><span data-stu-id="622d0-130">Armed with the knowledge that a particular page of your website has a problem on a particular browser, you can now go straight to the problem page, and investigate recent changes.</span></span>

## <a name="try-the-demo"></a><span data-ttu-id="622d0-131">Пробное использование демоверсии</span><span class="sxs-lookup"><span data-stu-id="622d0-131">Try the demo</span></span>

<span data-ttu-id="622d0-132">[Щелкните здесь, чтобы просмотреть демонстрацию](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) с образцом данных.</span><span class="sxs-lookup"><span data-stu-id="622d0-132">[Click here to see a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="622d0-133">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="622d0-133">How it works</span></span>

<span data-ttu-id="622d0-134">Интеллектуальная диагностика использует расширенный алгоритм машинного обучения без учителя на основе операции [DiffPatterns](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="622d0-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on the [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="622d0-135">Она ищет шаблоны-кандидаты, которые могут объяснить изменение данных.</span><span class="sxs-lookup"><span data-stu-id="622d0-135">It looks for candidate patterns that might explain the data change.</span></span> <span data-ttu-id="622d0-136">Она анализирует влияние каждого кандидата на метрику и показывает шаблон, который наиболее точно соответствует изменению.</span><span class="sxs-lookup"><span data-stu-id="622d0-136">It analyses the impact of each candidate on the metric, and shows the pattern that best correlates with the change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="622d0-137">Нет точек диагностики?</span><span class="sxs-lookup"><span data-stu-id="622d0-137">No diagnostic points?</span></span>

<span data-ttu-id="622d0-138">Интеллектуальная диагностика работает только при соблюдении следующих условий:</span><span class="sxs-lookup"><span data-stu-id="622d0-138">Smart Diagnostics only works when the following criteria are satisfied:</span></span>

 * <span data-ttu-id="622d0-139">Включен параметр интеллектуальной диагностики.</span><span class="sxs-lookup"><span data-stu-id="622d0-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="622d0-140">Он находится в меню значка "Параметры" в Analytics.</span><span class="sxs-lookup"><span data-stu-id="622d0-140">Look under the Settings icon in Analytics.</span></span>
 * <span data-ttu-id="622d0-141">Выбран параметр интеллектуальной диагностики в параметрах Analytics.</span><span class="sxs-lookup"><span data-stu-id="622d0-141">The Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="622d0-142">Ось времени: ось X диаграммы должна иметь тип `datetime`.</span><span class="sxs-lookup"><span data-stu-id="622d0-142">Time axis: The X-axis of the chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="622d0-143">График или диаграмма с областями: диагностика работает только для этих типов диаграмм.</span><span class="sxs-lookup"><span data-stu-id="622d0-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="622d0-144">Используйте `| render timechart` или `| render areachart` в конце запроса либо выберите "График" или "Диаграмма с областями" в раскрывающемся списке выбора.</span><span class="sxs-lookup"><span data-stu-id="622d0-144">Use `| render timechart` or `| render areachart` at the end of your query; or select Line or Area Chart from the drop-down selector.</span></span>
 * <span data-ttu-id="622d0-145">Неоднородность: в данных должна присутствовать значительная неоднородность.</span><span class="sxs-lookup"><span data-stu-id="622d0-145">Discontinuity: There must be a significant discontinuity in the data.</span></span>
 * <span data-ttu-id="622d0-146">Достаточное число точек для анализа.</span><span class="sxs-lookup"><span data-stu-id="622d0-146">Sufficient points to analyze.</span></span>
 * <span data-ttu-id="622d0-147">Не более одного предложения итоговых значений в запросе.</span><span class="sxs-lookup"><span data-stu-id="622d0-147">No more than one summarize clause in the query.</span></span>
 * <span data-ttu-id="622d0-148">Отсутствие предложения проекта, содержащего определение имени, перед предложением итоговых значений.</span><span class="sxs-lookup"><span data-stu-id="622d0-148">No project clause that contains a name definition before the summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="622d0-149">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="622d0-149">Related articles</span></span>

 * [<span data-ttu-id="622d0-150">Руководство по аналитике</span><span class="sxs-lookup"><span data-stu-id="622d0-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="622d0-151">[Интеллектуальное обнаружение](app-insights-proactive-diagnostics.md) автоматически оповещает вас о проблемах с производительностью.</span><span class="sxs-lookup"><span data-stu-id="622d0-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you to performance issues.</span></span>