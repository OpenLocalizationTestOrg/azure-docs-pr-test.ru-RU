---
title: "счетчики aaaPerformance в Application Insights | Документы Microsoft"
description: "Мониторинг системных и пользовательских счетчиков производительности .NET в Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a>Системные счетчики производительности в Application Insights
В Windows предусмотрены самые разные [счетчики производительности](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters), которые отображают показатели использования ЦП, памяти, диска и сети. Также вы можете определить собственные счетчики. [Application Insights](app-insights-overview.md) можно показать счетчики производительности, если приложение работает под управлением служб IIS на локальный узел или виртуальную машину toowhich пользователь иметь административный доступ. Hello диаграммы показывают hello ресурсы доступны tooyour работающего приложения, а также может помочь tooidentify балансировки нагрузки между экземплярами сервера.

Счетчики производительности отображаются в колонке hello серверов, которая содержит таблицу, которая сегментирует экземпляром сервера.

![Счетчики производительности, отображаемые в Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

(Счетчики производительности недоступны для веб-приложений Azure. Но вы можете [отправки диагностики Azure Insights tooApplication](app-insights-azure-diagnostics.md).)

## <a name="view-counters"></a>Просмотр счетчиков
Серверы колонке Hello показан набор по умолчанию счетчики производительности. 

toosee другие счетчики изменить hello диаграмм, в колонке серверы hello, или откройте новое [обозревателя метрик](app-insights-metrics-explorer.md) колонки и добавление новых диаграмм. 

Доступные счетчики Hello, перечислены как метрики при редактировании диаграммы.

![Счетчики производительности, отображаемые в Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

создать все чаще диаграммы в одном месте toosee [мониторинга](app-insights-dashboards.md) и закреплять их tooit.

## <a name="add-counters"></a>Добавление счетчиков
Если hello счетчиков производительности, которые вы хотите не отображаются в списке hello метрик, так как пакет SDK Application Insights hello не сбор в веб-сервере. Можно настроить его toodo таким образом.

1. Узнайте, какие счетчики доступны на сервере с помощью этой команды PowerShell на сервере hello:
   
    `Get-Counter -ListSet *`
   
    (См. [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)
2. Откройте файл ApplicationInsights.config.
   
   * Если вы добавили Application Insights tooyour приложения во время разработки, измените файл ApplicationInsights.config в проекте и повторно развернуть серверы tooyour.
   * Если вы использовали tooinstrument монитор состояния веб-приложения во время выполнения, найти файл ApplicationInsights.config в корневой каталог hello приложение hello в службах IIS. Обновите его в этом расположении на каждом экземпляре сервера.
3. Изменение hello производительности сборщика директивы:
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

Вы можете собирать показания как стандартных счетчиков, так и созданных вами самостоятельно. Например, стандартный счетчик `\Objects\Processes` доступен во всех системах Windows. Пример пользовательского счетчика, который можно реализовать в веб-службе: `\Sales(photo)\# Items Sold`. 

Формат Hello `\Category(instance)\Counter"`, или категорий, которые не имеют экземпляров, просто `\Category\Counter`.

`ReportAs`требуется для имен счетчиков, которые не соответствуют `[a-zA-Z()/-_ \.]+` -то есть, они содержат символы, которые не находятся в следующих наборов hello: буквы в круглые скобки, косой черты, дефиса, подчеркивания, пространство, точка.

При указании экземпляра он соберет указываемая метрика измерения «CounterInstanceName» из hello.

### <a name="collecting-performance-counters-in-code"></a>Сбор данных счетчиков производительности в коде
производительность системы toocollect счетчиков и отправлять их tooApplication аналитики, вы можете адаптировать в приведенном ниже фрагменте hello:


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

Или можно сделать то же самое с настраиваемых метрик, которые вы создали hello:

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a>Счетчики производительности в службе аналитики
В [службе аналитики](app-insights-analytics.md) можно выполнять поиск отчетов по счетчикам производительности и отображать их.

Hello **performanceCounters** схема предоставляет hello `category`, `counter` имя, и `instance` имя каждого счетчика производительности.  Hello данные телеметрии для каждого приложения вы увидите только hello счетчики для этого приложения. Например, toosee какие счетчики доступны: 

![Счетчики производительности в аналитике Application Insights](./media/app-insights-performance-counters/analytics-performance-counters.png)

(Здесь «Instance» ссылается экземпляр счетчика производительности toohello, не hello роли или машины экземпляра сервера. Имя экземпляра счетчика производительности Hello обычно сегменты счетчиков, например процессорного времени, именем hello hello процесс или приложение.)

tooget диаграммы доступной памяти за последний период hello: 

![Временная диаграмма памяти в аналитике Application Insights](./media/app-insights-performance-counters/analytics-available-memory.png)

Как и другие данные телеметрии **performanceCounters** также есть столбец `cloud_RoleInstance` указывает удостоверение hello hello экземпляр основного сервера, на котором выполняется приложение. Например toocompare hello производительности приложения на разных компьютерах hello: 

![Производительность, сегментированная по экземпляру роли в аналитике Application Insights](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a>ASP.NET и счетчики Application Insights
*Что такое hello различие между скорость исключение hello и метрики, исключения*

* *Частота исключений* — это системный счетчик производительности. Hello CLR подсчитывает все обрабатываются hello и необработанные исключения, которые были созданы и делит общий hello в интервале выборки hello продолжительность интервала hello. пакет SDK для Application Insights Hello собирает этот результат и отправляет их toohello портала.
* *Исключения* представляет собой число hello TrackException отчеты, полученных портала hello в интервале выборки hello hello диаграммы. Он включает только hello обработанных исключений, где вы написали TrackException вызывает в коде, а не включает все [необработанные исключения](app-insights-asp-net-exceptions.md). 

## <a name="alerts"></a>Оповещения
Как и другие показатели, вы можете [настроить оповещение](app-insights-alerts.md) toowarn, если счетчик производительности выйдет за пределы ограничения указывается. Откройте колонку оповещения hello и нажмите кнопку Добавить оповещение.

## <a name="next"></a>Дальнейшие действия
* [Отслеживание зависимостей](app-insights-asp-net-dependencies.md)
* [Отслеживание исключений](app-insights-asp-net-exceptions.md)

