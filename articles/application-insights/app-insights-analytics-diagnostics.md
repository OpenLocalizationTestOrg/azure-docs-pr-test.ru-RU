---
title: "Диагностика aaaSmart web изменений производительности приложения в Azure Application Insights | Документы Microsoft"
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
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="ab4d3-103">Диагностика внезапных изменений в телеметрии приложения</span><span class="sxs-lookup"><span data-stu-id="ab4d3-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="ab4d3-104">*Эта функция предоставляется в предварительной версии.*</span><span class="sxs-lookup"><span data-stu-id="ab4d3-104">*This feature is in preview.*</span></span>

<span data-ttu-id="ab4d3-105">Диагностируйте внезапные изменения производительности или использования веб-приложения одним щелчком мыши!</span><span class="sxs-lookup"><span data-stu-id="ab4d3-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="ab4d3-106">Hello смарт-диагностики доступна каждый раз при создании временной диаграммы в [Analytics](app-insights-analytics.md) в [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab4d3-106">hello Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="ab4d3-107">Везде, где есть необычные изменение тренда hello результатов, например, пик или dip, смарт-диагностики обозначает шаблон измерений и связанных значений, которые могут объяснить hello изменений.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-107">Wherever there is an unusual change from hello trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain hello change.</span></span> <span data-ttu-id="ab4d3-108">Это поможет вам быстро диагностировать проблему hello.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-108">This helps you diagnose hello problem quickly.</span></span> 

<span data-ttu-id="ab4d3-109">В этом примере смарт-диагностики определил шаблон значения свойств, связанных с изменением hello и подчеркивает hello различие между результаты с использованием и без этого шаблона:</span><span class="sxs-lookup"><span data-stu-id="ab4d3-109">In this example, Smart Diagnostics has identified a pattern of property values associated with hello change, and highlights hello difference between results with and without that pattern:</span></span>

![Пример результатов диагностики аналитики](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="ab4d3-111">Диагностика изменений данных</span><span class="sxs-lookup"><span data-stu-id="ab4d3-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="ab4d3-112">Выполните запрос в Analytics и отрисуйте его в виде диаграммы времени.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="ab4d3-113">Щелкните любой из выделенных пиков, если он имеется.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![пик](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="ab4d3-115">Диагностика занимает несколько секунд toodiscover шаблон.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-115">Diagnostics takes a few seconds toodiscover a pattern.</span></span>

3. <span data-ttu-id="ab4d3-116">Hello результатов диагностики вкладке отображается шаблон, которые могут помочь выяснить разрыв в данных.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-116">hello Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="ab4d3-118">текст Hello указывает hello значения измерений, которые появляются toocorrelate с hello shift.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-118">hello text shows hello dimension values that appear toocorrelate with hello shift.</span></span> <span data-ttu-id="ab4d3-119">В этом примере оно связано с конкретным запросом и конкретной версией браузера.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="ab4d3-120">Следует также обратить внимание hello двух компонентов hello диаграммы, с hello фильтра true и false.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-120">Notice also hello two components of hello chart, with hello filter true and false.</span></span> <span data-ttu-id="ab4d3-121">компонент false Hello показывает тренд без изменений.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-121">hello false component shows an unchanged trend.</span></span> <span data-ttu-id="ab4d3-122">Другими словами нет изменений в результатах телеметрии hello, если мы исключить hello проблемный сочетаниями измерений, которые определил диагностики.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-122">In other words, there is no change in hello telemetry results, if we exclude hello problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="ab4d3-123">В отличие от этого результаты hello в комбинации показывают требуются значительные изменения в пределах области выделены hello расследования.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-123">By contrast, hello results within that combination do show a dramatic change within hello highlighted area of investigation.</span></span> <span data-ttu-id="ab4d3-124">Показывает, что диагностики обнаружил сочетания свойств с объяснением hello изменений.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-124">This shows that Diagnostics has found a combination of properties that explains hello change.</span></span>

4.  <span data-ttu-id="ab4d3-125">Если шаблон hello является сложным, требуется toohover по сравнению с **Показать все** toosee hello измерений.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-125">If hello pattern is complex, you need toohover over **Show all** toosee hello dimensions.</span></span>

    ![показать все](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="ab4d3-127">В случае, если Диагностика находит не toonotify значительные шаблон о hello, откроется страница «нет результатов».</span><span class="sxs-lookup"><span data-stu-id="ab4d3-127">In case Diagnostics finds no significant pattern toonotify about, hello ‘no results’ page will be presented.</span></span> <span data-ttu-id="ab4d3-128">На этом этапе запрос можно изменить.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-128">At this point, you may change your query.</span></span> <span data-ttu-id="ab4d3-129">Например может сузить диапазон времени hello и группирования в запросе Analytics для дальнейшего анализа и потенциально более точные результаты.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-129">For example, you could narrow hello time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="ab4d3-130">Используя знания hello, что на одной странице веб-сайте возникла проблема в браузере, определенного, позволяют теперь переход на страницу прямой toohello проблему и изучить последние изменения.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-130">Armed with hello knowledge that a particular page of your website has a problem on a particular browser, you can now go straight toohello problem page, and investigate recent changes.</span></span>

## <a name="try-hello-demo"></a><span data-ttu-id="ab4d3-131">Повторите Демонстрация hello</span><span class="sxs-lookup"><span data-stu-id="ab4d3-131">Try hello demo</span></span>

<span data-ttu-id="ab4d3-132">[Щелкните здесь, toosee Демонстрация](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) над образцом данных.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-132">[Click here toosee a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="ab4d3-133">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="ab4d3-133">How it works</span></span>

<span data-ttu-id="ab4d3-134">Смарт-диагностики используется алгоритм Дополнительно незащищенных машинного обучения, основании hello [DiffPatterns](app-insights-analytics-reference.md) операции.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on hello [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="ab4d3-135">Выполняет поиск вероятные шаблоны, которые могут объяснить hello изменения данных.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-135">It looks for candidate patterns that might explain hello data change.</span></span> <span data-ttu-id="ab4d3-136">Анализирует hello влияние каждого кандидата на метрику hello и показан шаблон hello, лучше всего сопоставлены hello изменений.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-136">It analyses hello impact of each candidate on hello metric, and shows hello pattern that best correlates with hello change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="ab4d3-137">Нет точек диагностики?</span><span class="sxs-lookup"><span data-stu-id="ab4d3-137">No diagnostic points?</span></span>

<span data-ttu-id="ab4d3-138">Смарт-диагностики работает только в том случае, когда выполняются следующие условия hello:</span><span class="sxs-lookup"><span data-stu-id="ab4d3-138">Smart Diagnostics only works when hello following criteria are satisfied:</span></span>

 * <span data-ttu-id="ab4d3-139">Включен параметр интеллектуальной диагностики.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="ab4d3-140">Найдите под значком параметров hello в аналитике.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-140">Look under hello Settings icon in Analytics.</span></span>
 * <span data-ttu-id="ab4d3-141">выбран Hello параметр смарт-диагностики в параметрах Analytics.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-141">hello Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="ab4d3-142">Ось времени: hello оси x диаграммы hello должен иметь тип `datetime`.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-142">Time axis: hello X-axis of hello chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="ab4d3-143">График или диаграмма с областями: диагностика работает только для этих типов диаграмм.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="ab4d3-144">Используйте `| render timechart` или `| render areachart` в конце hello запроса; или выберите из раскрывающегося списка выбора hello линии или области диаграммы.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-144">Use `| render timechart` or `| render areachart` at hello end of your query; or select Line or Area Chart from hello drop-down selector.</span></span>
 * <span data-ttu-id="ab4d3-145">Разрыв: Необходимо значительный разрыв в данных hello.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-145">Discontinuity: There must be a significant discontinuity in hello data.</span></span>
 * <span data-ttu-id="ab4d3-146">Достаточно tooanalyze точек.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-146">Sufficient points tooanalyze.</span></span>
 * <span data-ttu-id="ab4d3-147">Не более одного обобщить предложение в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-147">No more than one summarize clause in hello query.</span></span>
 * <span data-ttu-id="ab4d3-148">Без предложения проекта, содержащего определение имени перед hello суммировать предложения.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-148">No project clause that contains a name definition before hello summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="ab4d3-149">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="ab4d3-149">Related articles</span></span>

 * [<span data-ttu-id="ab4d3-150">Руководство по аналитике</span><span class="sxs-lookup"><span data-stu-id="ab4d3-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="ab4d3-151">[Смарт-обнаружение](app-insights-proactive-diagnostics.md) автоматически оповещает пользователя tooperformance проблемы.</span><span class="sxs-lookup"><span data-stu-id="ab4d3-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you tooperformance issues.</span></span>
