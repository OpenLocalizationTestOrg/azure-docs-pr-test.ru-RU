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
# <a name="filter-telemetry-in-your-java-web-app"></a>Фильтрация данных телеметрии в веб-приложении Java

Фильтры предоставляют способ tooselect hello телеметрии вашего [веб-приложение Java отправляет аналитики tooApplication](app-insights-java-get-started.md). Имеется несколько готовых фильтров, которые можно использовать. Можно также создать собственные пользовательские фильтры.

доступны следующие фильтры Hello out of box:

* уровень серьезности трассировки;
* определенные URL-адреса, ключевые слова или коды ответов;
* Быстрый ответ — то есть запросах toowhich tooquickly ответа приложения
* имена определенных событий.

> [!NOTE]
> Фильтры исказить hello метрик вашего приложения. Например можно решить, что в порядке toodiagnose замедление отклика, будут установлены фильтра toodiscard быстрого отклика. Однако следует иметь в виду hello среднего времени отклика сообщили Application Insights будет медленнее, чем скорость true hello, что счетчик hello запросов будет меньше, чем число реальные hello.
> Если это представляет собой проблему, то используйте [выборки](app-insights-sampling.md).

## <a name="setting-filters"></a>Задание фильтров

Добавьте в файл ApplicationInsights.xml раздел `TelemetryProcessors`, как в примере ниже.


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




[Проверять hello полный набор встроенных процессоров](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).

## <a name="built-in-filters"></a>Встроенные фильтры

### <a name="metric-telemetry-filter"></a>Фильтр телеметрии метрик

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* `NotNeeded` — разделенный запятыми список имен пользовательских метрик.


### <a name="page-view-telemetry-filter"></a>Фильтр телеметрии просмотров страницы

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* `DurationThresholdInMS`-Длительность ссылается время toohello tooload страницы приветствия. Если он установлен, то страницы, которые загружаются быстрее, чем это значение, не учитываются.
* `NotNeededNames` — разделенный запятыми список имен страниц.
* `NotNeededUrls` — разделенный запятыми список фрагментов URL-адресов. Например `"home"` отфильтровывает все страницы, которые имеют «Главная» в URL-АДРЕСЕ hello.


### <a name="request-telemetry-filter"></a>Фильтр телеметрии запросов


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a>Фильтр искусственных источников

Отфильтровывает все данные телеметрии, которые имеют значения в свойство SyntheticSource hello. К ним относятся запросы от программ-роботов, программ-обходчиков и тестов доступности.

Фильтрация данных телеметрии для всех запросов от искусственных источников:


```XML

           <Processor type="SyntheticSourceFilter" />
```

Фильтрация данных телеметрии для определенных запросов от искусственных источников:


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* `NotNeeded` — разделенный запятыми список имен искусственных источников.

### <a name="telemetry-event-filter"></a>Фильтр телеметрии событий

Фильтрует пользовательские события (добавленные в журнал с помощью [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* `NotNeededNames` — разделенный запятыми список имен событий.


### <a name="trace-telemetry-filter"></a>Фильтр телеметрии трассировок

Фильтрует трассировки журнала (добавленные в журнал с помощью [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) или [сборщика платформа ведения журналов](app-insights-java-trace-logs.md)).

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* Допустимые значения `FromSeverityLevel`:
 *  OFF — отфильтровывание ВСЕХ трассировок;
 *  TRACE — фильтрация отключена; уровень tooTrace Equals
 *  INFO — отфильтровывание уровня TRACE;
 *  WARN — отфильтровывание уровней TRACE и INFO;
 *  ERROR — отфильтровывание уровней WARN, INFO и TRACE;
 *  CRITICAL — отфильтровывание всех уровней, кроме уровня CRITICAL.


## <a name="custom-filters"></a>Настраиваемые фильтры

### <a name="1-code-your-filter"></a>1. Программирование фильтра

В коде создайте класс, реализующий `TelemetryProcessor`.

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


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a>2. Вызова фильтра, в файле конфигурации hello

В файле ApplicationInsights.xml:

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

## <a name="troubleshooting"></a>Устранение неполадок

*Мой фильтр не работает.*

* Убедитесь, что для параметров указаны допустимые значения. Например, значения длительности должны быть целыми числами. Недопустимые значения вызовет toobe фильтра hello игнорируются. Если пользовательский фильтр породит исключение из конструктора или метода set, он будет проигнорирован.

## <a name="next-steps"></a>Дальнейшие действия

* Использование [выборки](app-insights-sampling.md) — альтернативный метод, который не искажает метрики.
