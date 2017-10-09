---
title: "aaaFilter телеметрии Azure Application Insights в веб-приложения Java | Документы Microsoft"
description: "Уменьшить трафик телеметрии, отфильтровывая hello событий не требуется toomonitor."
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
ms.openlocfilehash: 95713e11d5f86472777c67e4e7f3177fbf2cd0b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="f008d-103">Фильтрация данных телеметрии в веб-приложении Java</span><span class="sxs-lookup"><span data-stu-id="f008d-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="f008d-104">Фильтры предоставляют способ tooselect hello телеметрии вашего [веб-приложение Java отправляет аналитики tooApplication](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f008d-104">Filters provide a way tooselect hello telemetry that your [Java web app sends tooApplication Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="f008d-105">Имеется несколько готовых фильтров, которые можно использовать. Можно также создать собственные пользовательские фильтры.</span><span class="sxs-lookup"><span data-stu-id="f008d-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="f008d-106">доступны следующие фильтры Hello out of box:</span><span class="sxs-lookup"><span data-stu-id="f008d-106">hello out-of-the-box filters include:</span></span>

* <span data-ttu-id="f008d-107">уровень серьезности трассировки;</span><span class="sxs-lookup"><span data-stu-id="f008d-107">Trace severity level</span></span>
* <span data-ttu-id="f008d-108">определенные URL-адреса, ключевые слова или коды ответов;</span><span class="sxs-lookup"><span data-stu-id="f008d-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="f008d-109">Быстрый ответ — то есть запросах toowhich tooquickly ответа приложения</span><span class="sxs-lookup"><span data-stu-id="f008d-109">Fast responses - that is, requests toowhich your app responded tooquickly</span></span>
* <span data-ttu-id="f008d-110">имена определенных событий.</span><span class="sxs-lookup"><span data-stu-id="f008d-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="f008d-111">Фильтры исказить hello метрик вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f008d-111">Filters skew hello metrics of your app.</span></span> <span data-ttu-id="f008d-112">Например можно решить, что в порядке toodiagnose замедление отклика, будут установлены фильтра toodiscard быстрого отклика.</span><span class="sxs-lookup"><span data-stu-id="f008d-112">For example, you might decide that, in order toodiagnose slow responses, you will set a filter toodiscard fast response times.</span></span> <span data-ttu-id="f008d-113">Однако следует иметь в виду hello среднего времени отклика сообщили Application Insights будет медленнее, чем скорость true hello, что счетчик hello запросов будет меньше, чем число реальные hello.</span><span class="sxs-lookup"><span data-stu-id="f008d-113">But you must be aware that hello average response times reported by Application Insights will then be slower than hello true speed, and hello count of requests will be smaller than hello real count.</span></span>
> <span data-ttu-id="f008d-114">Если это представляет собой проблему, то используйте [выборки](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="f008d-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="f008d-115">Задание фильтров</span><span class="sxs-lookup"><span data-stu-id="f008d-115">Setting filters</span></span>

<span data-ttu-id="f008d-116">Добавьте в файл ApplicationInsights.xml раздел `TelemetryProcessors`, как в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="f008d-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


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
                  <!-- Names of events we don't want toosee -->
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




<span data-ttu-id="f008d-117">[Проверять hello полный набор встроенных процессоров](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="f008d-117">[Inspect hello full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="f008d-118">Встроенные фильтры</span><span class="sxs-lookup"><span data-stu-id="f008d-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="f008d-119">Фильтр телеметрии метрик</span><span class="sxs-lookup"><span data-stu-id="f008d-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="f008d-120">`NotNeeded` — разделенный запятыми список имен пользовательских метрик.</span><span class="sxs-lookup"><span data-stu-id="f008d-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="f008d-121">Фильтр телеметрии просмотров страницы</span><span class="sxs-lookup"><span data-stu-id="f008d-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="f008d-122">`DurationThresholdInMS`-Длительность ссылается время toohello tooload страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="f008d-122">`DurationThresholdInMS` - Duration refers toohello time taken tooload hello page.</span></span> <span data-ttu-id="f008d-123">Если он установлен, то страницы, которые загружаются быстрее, чем это значение, не учитываются.</span><span class="sxs-lookup"><span data-stu-id="f008d-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="f008d-124">`NotNeededNames` — разделенный запятыми список имен страниц.</span><span class="sxs-lookup"><span data-stu-id="f008d-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="f008d-125">`NotNeededUrls` — разделенный запятыми список фрагментов URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="f008d-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="f008d-126">Например `"home"` отфильтровывает все страницы, которые имеют «Главная» в URL-АДРЕСЕ hello.</span><span class="sxs-lookup"><span data-stu-id="f008d-126">For example, `"home"` filters out all pages that have "home" in hello URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="f008d-127">Фильтр телеметрии запросов</span><span class="sxs-lookup"><span data-stu-id="f008d-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="f008d-128">Фильтр искусственных источников</span><span class="sxs-lookup"><span data-stu-id="f008d-128">Synthetic Source filter</span></span>

<span data-ttu-id="f008d-129">Отфильтровывает все данные телеметрии, которые имеют значения в свойство SyntheticSource hello.</span><span class="sxs-lookup"><span data-stu-id="f008d-129">Filters out all telemetry that have values in hello SyntheticSource property.</span></span> <span data-ttu-id="f008d-130">К ним относятся запросы от программ-роботов, программ-обходчиков и тестов доступности.</span><span class="sxs-lookup"><span data-stu-id="f008d-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="f008d-131">Фильтрация данных телеметрии для всех запросов от искусственных источников:</span><span class="sxs-lookup"><span data-stu-id="f008d-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="f008d-132">Фильтрация данных телеметрии для определенных запросов от искусственных источников:</span><span class="sxs-lookup"><span data-stu-id="f008d-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="f008d-133">`NotNeeded` — разделенный запятыми список имен искусственных источников.</span><span class="sxs-lookup"><span data-stu-id="f008d-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="f008d-134">Фильтр телеметрии событий</span><span class="sxs-lookup"><span data-stu-id="f008d-134">Telemetry Event filter</span></span>

<span data-ttu-id="f008d-135">Фильтрует пользовательские события (добавленные в журнал с помощью [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="f008d-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="f008d-136">`NotNeededNames` — разделенный запятыми список имен событий.</span><span class="sxs-lookup"><span data-stu-id="f008d-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="f008d-137">Фильтр телеметрии трассировок</span><span class="sxs-lookup"><span data-stu-id="f008d-137">Trace Telemetry filter</span></span>

<span data-ttu-id="f008d-138">Фильтрует трассировки журнала (добавленные в журнал с помощью [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) или [сборщика платформа ведения журналов](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="f008d-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="f008d-139">Допустимые значения `FromSeverityLevel`:</span><span class="sxs-lookup"><span data-stu-id="f008d-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="f008d-140">OFF — отфильтровывание ВСЕХ трассировок;</span><span class="sxs-lookup"><span data-stu-id="f008d-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="f008d-141">TRACE — фильтрация отключена;</span><span class="sxs-lookup"><span data-stu-id="f008d-141">TRACE           - No filtering.</span></span> <span data-ttu-id="f008d-142">уровень tooTrace Equals</span><span class="sxs-lookup"><span data-stu-id="f008d-142">equals tooTrace level</span></span>
 *  <span data-ttu-id="f008d-143">INFO — отфильтровывание уровня TRACE;</span><span class="sxs-lookup"><span data-stu-id="f008d-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="f008d-144">WARN — отфильтровывание уровней TRACE и INFO;</span><span class="sxs-lookup"><span data-stu-id="f008d-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="f008d-145">ERROR — отфильтровывание уровней WARN, INFO и TRACE;</span><span class="sxs-lookup"><span data-stu-id="f008d-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="f008d-146">CRITICAL — отфильтровывание всех уровней, кроме уровня CRITICAL.</span><span class="sxs-lookup"><span data-stu-id="f008d-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="f008d-147">Настраиваемые фильтры</span><span class="sxs-lookup"><span data-stu-id="f008d-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="f008d-148">1. Программирование фильтра</span><span class="sxs-lookup"><span data-stu-id="f008d-148">1. Code your filter</span></span>

<span data-ttu-id="f008d-149">В коде создайте класс, реализующий `TelemetryProcessor`.</span><span class="sxs-lookup"><span data-stu-id="f008d-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required toosupport hello filter.*/
       private final String successful;

       /* Initializers for hello parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry toobe sent.
          Return false toodiscard it.
          Return true tooallow other processors tooinspect it. */
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


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a><span data-ttu-id="f008d-150">2. Вызова фильтра, в файле конфигурации hello</span><span class="sxs-lookup"><span data-stu-id="f008d-150">2. Invoke your filter in hello configuration file</span></span>

<span data-ttu-id="f008d-151">В файле ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="f008d-151">In ApplicationInsights.xml:</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="f008d-152">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f008d-152">Troubleshooting</span></span>

<span data-ttu-id="f008d-153">*Мой фильтр не работает.*</span><span class="sxs-lookup"><span data-stu-id="f008d-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="f008d-154">Убедитесь, что для параметров указаны допустимые значения.</span><span class="sxs-lookup"><span data-stu-id="f008d-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="f008d-155">Например, значения длительности должны быть целыми числами.</span><span class="sxs-lookup"><span data-stu-id="f008d-155">For example, durations should be integers.</span></span> <span data-ttu-id="f008d-156">Недопустимые значения вызовет toobe фильтра hello игнорируются.</span><span class="sxs-lookup"><span data-stu-id="f008d-156">Invalid values will cause hello filter toobe ignored.</span></span> <span data-ttu-id="f008d-157">Если пользовательский фильтр породит исключение из конструктора или метода set, он будет проигнорирован.</span><span class="sxs-lookup"><span data-stu-id="f008d-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f008d-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f008d-158">Next steps</span></span>

* <span data-ttu-id="f008d-159">Использование [выборки](app-insights-sampling.md) — альтернативный метод, который не искажает метрики.</span><span class="sxs-lookup"><span data-stu-id="f008d-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
