---
title: "Фильтрация данных телеметрии Azure Application Insights в веб-приложении Java | Документация Майкрософт"
description: "Уменьшите трафик телеметрии с помощью фильтрации событий, которые не нужно отслеживать."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 5f6d6d4ad590b85810c42e9f9520850024c5446a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="d79da-103">Фильтрация данных телеметрии в веб-приложении Java</span><span class="sxs-lookup"><span data-stu-id="d79da-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="d79da-104">Фильтры позволяют выбрать данные телеметрии, которые [веб-приложение Java отправляет в Application Insights](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d79da-104">Filters provide a way to select the telemetry that your [Java web app sends to Application Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="d79da-105">Имеется несколько готовых фильтров, которые можно использовать. Можно также создать собственные пользовательские фильтры.</span><span class="sxs-lookup"><span data-stu-id="d79da-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="d79da-106">В готовых фильтры используется следующее:</span><span class="sxs-lookup"><span data-stu-id="d79da-106">The out-of-the-box filters include:</span></span>

* <span data-ttu-id="d79da-107">уровень серьезности трассировки;</span><span class="sxs-lookup"><span data-stu-id="d79da-107">Trace severity level</span></span>
* <span data-ttu-id="d79da-108">определенные URL-адреса, ключевые слова или коды ответов;</span><span class="sxs-lookup"><span data-stu-id="d79da-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="d79da-109">быстрые ответы — запросы, на которые приложение отвечает быстро;</span><span class="sxs-lookup"><span data-stu-id="d79da-109">Fast responses - that is, requests to which your app responded to quickly</span></span>
* <span data-ttu-id="d79da-110">имена определенных событий.</span><span class="sxs-lookup"><span data-stu-id="d79da-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="d79da-111">Фильтры искажают значения метрик приложения.</span><span class="sxs-lookup"><span data-stu-id="d79da-111">Filters skew the metrics of your app.</span></span> <span data-ttu-id="d79da-112">Например, вы можете задать фильтр для отклонения небольших значений времени ответа, чтобы диагностировать медленные ответы.</span><span class="sxs-lookup"><span data-stu-id="d79da-112">For example, you might decide that, in order to diagnose slow responses, you will set a filter to discard fast response times.</span></span> <span data-ttu-id="d79da-113">Однако необходимо иметь в виду, что в этом случае среднее время ответа, отображаемое Application Insights, будет медленнее, а количество запросов — меньше, чем на самом деле.</span><span class="sxs-lookup"><span data-stu-id="d79da-113">But you must be aware that the average response times reported by Application Insights will then be slower than the true speed, and the count of requests will be smaller than the real count.</span></span>
> <span data-ttu-id="d79da-114">Если это представляет собой проблему, то используйте [выборки](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="d79da-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="d79da-115">Задание фильтров</span><span class="sxs-lookup"><span data-stu-id="d79da-115">Setting filters</span></span>

<span data-ttu-id="d79da-116">Добавьте в файл ApplicationInsights.xml раздел `TelemetryProcessors`, как в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="d79da-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


```XML

    <ApplicationInsights>
      <TelemetryProcessors>

        <BuiltInProcessors>
           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="100"/>
                  <Add name="NotNeededResponseCodes" value="200-400"/>
           </Processor>

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="100"/>
                  <Add name="NotNeededNames" value="home,index"/>
                  <Add name="NotNeededUrls" value=".jpg,.css"/>
           </Processor>

           <Processor type="TelemetryEventFilter">
                  <!-- Names of events we don't want to see -->
                  <Add name="NotNeededNames" value="Start,Stop,Pause"/>
           </Processor>

           <!-- Exclude telemetry from availability tests and bots -->
           <Processor type="SyntheticSourceFilter">
                <!-- Optional: specify which synthetic sources,
                     comma-separated
                     - default is all synthetics -->
                <Add name="NotNeededSources" value="Application Insights Availability Monitoring,BingPreview"
           </Processor>

        </BuiltInProcessors>

        <CustomProcessors>
          <Processor type="com.fabrikam.MyFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>

      </TelemetryProcessors>
    </ApplicationInsights>

```




<span data-ttu-id="d79da-117">[Просмотрите полный набор встроенных обработчиков](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="d79da-117">[Inspect the full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="d79da-118">Встроенные фильтры</span><span class="sxs-lookup"><span data-stu-id="d79da-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="d79da-119">Фильтр телеметрии метрик</span><span class="sxs-lookup"><span data-stu-id="d79da-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="d79da-120">`NotNeeded` — разделенный запятыми список имен пользовательских метрик.</span><span class="sxs-lookup"><span data-stu-id="d79da-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="d79da-121">Фильтр телеметрии просмотров страницы</span><span class="sxs-lookup"><span data-stu-id="d79da-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="d79da-122">`DurationThresholdInMS` — длительность означает время, необходимое для загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="d79da-122">`DurationThresholdInMS` - Duration refers to the time taken to load the page.</span></span> <span data-ttu-id="d79da-123">Если он установлен, то страницы, которые загружаются быстрее, чем это значение, не учитываются.</span><span class="sxs-lookup"><span data-stu-id="d79da-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="d79da-124">`NotNeededNames` — разделенный запятыми список имен страниц.</span><span class="sxs-lookup"><span data-stu-id="d79da-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="d79da-125">`NotNeededUrls` — разделенный запятыми список фрагментов URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="d79da-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="d79da-126">Например, `"home"` отфильтровывает все страницы, которые содержат в URL-адресе слово "home".</span><span class="sxs-lookup"><span data-stu-id="d79da-126">For example, `"home"` filters out all pages that have "home" in the URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="d79da-127">Фильтр телеметрии запросов</span><span class="sxs-lookup"><span data-stu-id="d79da-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="d79da-128">Фильтр искусственных источников</span><span class="sxs-lookup"><span data-stu-id="d79da-128">Synthetic Source filter</span></span>

<span data-ttu-id="d79da-129">Отфильтровывает все данные телеметрии, имеющие значение в свойстве SyntheticSource.</span><span class="sxs-lookup"><span data-stu-id="d79da-129">Filters out all telemetry that have values in the SyntheticSource property.</span></span> <span data-ttu-id="d79da-130">К ним относятся запросы от программ-роботов, программ-обходчиков и тестов доступности.</span><span class="sxs-lookup"><span data-stu-id="d79da-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="d79da-131">Фильтрация данных телеметрии для всех запросов от искусственных источников:</span><span class="sxs-lookup"><span data-stu-id="d79da-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="d79da-132">Фильтрация данных телеметрии для определенных запросов от искусственных источников:</span><span class="sxs-lookup"><span data-stu-id="d79da-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="d79da-133">`NotNeeded` — разделенный запятыми список имен искусственных источников.</span><span class="sxs-lookup"><span data-stu-id="d79da-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="d79da-134">Фильтр телеметрии событий</span><span class="sxs-lookup"><span data-stu-id="d79da-134">Telemetry Event filter</span></span>

<span data-ttu-id="d79da-135">Фильтрует пользовательские события (добавленные в журнал с помощью [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="d79da-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="d79da-136">`NotNeededNames` — разделенный запятыми список имен событий.</span><span class="sxs-lookup"><span data-stu-id="d79da-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="d79da-137">Фильтр телеметрии трассировок</span><span class="sxs-lookup"><span data-stu-id="d79da-137">Trace Telemetry filter</span></span>

<span data-ttu-id="d79da-138">Фильтрует трассировки журнала (добавленные в журнал с помощью [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) или [сборщика платформа ведения журналов](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="d79da-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="d79da-139">Допустимые значения `FromSeverityLevel`:</span><span class="sxs-lookup"><span data-stu-id="d79da-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="d79da-140">OFF — отфильтровывание ВСЕХ трассировок;</span><span class="sxs-lookup"><span data-stu-id="d79da-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="d79da-141">TRACE — фильтрация отключена;</span><span class="sxs-lookup"><span data-stu-id="d79da-141">TRACE           - No filtering.</span></span> <span data-ttu-id="d79da-142">соответствует уровню трассировки (TRACE);</span><span class="sxs-lookup"><span data-stu-id="d79da-142">equals to Trace level</span></span>
 *  <span data-ttu-id="d79da-143">INFO — отфильтровывание уровня TRACE;</span><span class="sxs-lookup"><span data-stu-id="d79da-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="d79da-144">WARN — отфильтровывание уровней TRACE и INFO;</span><span class="sxs-lookup"><span data-stu-id="d79da-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="d79da-145">ERROR — отфильтровывание уровней WARN, INFO и TRACE;</span><span class="sxs-lookup"><span data-stu-id="d79da-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="d79da-146">CRITICAL — отфильтровывание всех уровней, кроме уровня CRITICAL.</span><span class="sxs-lookup"><span data-stu-id="d79da-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="d79da-147">Настраиваемые фильтры</span><span class="sxs-lookup"><span data-stu-id="d79da-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="d79da-148">1. Программирование фильтра</span><span class="sxs-lookup"><span data-stu-id="d79da-148">1. Code your filter</span></span>

<span data-ttu-id="d79da-149">В коде создайте класс, реализующий `TelemetryProcessor`.</span><span class="sxs-lookup"><span data-stu-id="d79da-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required to support the filter.*/
       private final String successful;

       /* Initializers for the parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry to be sent.
          Return false to discard it.
          Return true to allow other processors to inspect it. */
       @Override
       public boolean process(Telemetry telemetry) {
        if (telemetry == null) { return true; }
        if (telemetry instanceof RequestTelemetry)
        {
            RequestTelemetry requestTelemetry = (RequestTelemetry)telemetry;
            return request.getSuccess() == successful;
        }
        return true;
       }
    }

```


### <a name="2-invoke-your-filter-in-the-configuration-file"></a><span data-ttu-id="d79da-150">2) Вызов фильтра в файле конфигурации</span><span class="sxs-lookup"><span data-stu-id="d79da-150">2. Invoke your filter in the configuration file</span></span>

<span data-ttu-id="d79da-151">В файле ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="d79da-151">In ApplicationInsights.xml:</span></span>

```XML


    <ApplicationInsights>
      <TelemetryProcessors>
        <CustomProcessors>
          <Processor type="com.fabrikam.SuccessFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>
      </TelemetryProcessors>
    </ApplicationInsights>

```

## <a name="troubleshooting"></a><span data-ttu-id="d79da-152">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="d79da-152">Troubleshooting</span></span>

<span data-ttu-id="d79da-153">*Мой фильтр не работает.*</span><span class="sxs-lookup"><span data-stu-id="d79da-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="d79da-154">Убедитесь, что для параметров указаны допустимые значения.</span><span class="sxs-lookup"><span data-stu-id="d79da-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="d79da-155">Например, значения длительности должны быть целыми числами.</span><span class="sxs-lookup"><span data-stu-id="d79da-155">For example, durations should be integers.</span></span> <span data-ttu-id="d79da-156">Недопустимые значения приведут к тому, что фильтр будет проигнорирован.</span><span class="sxs-lookup"><span data-stu-id="d79da-156">Invalid values will cause the filter to be ignored.</span></span> <span data-ttu-id="d79da-157">Если пользовательский фильтр породит исключение из конструктора или метода set, он будет проигнорирован.</span><span class="sxs-lookup"><span data-stu-id="d79da-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d79da-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d79da-158">Next steps</span></span>

* <span data-ttu-id="d79da-159">Использование [выборки](app-insights-sampling.md) — альтернативный метод, который не искажает метрики.</span><span class="sxs-lookup"><span data-stu-id="d79da-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
