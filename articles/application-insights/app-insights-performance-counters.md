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
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="9ec07-103">Системные счетчики производительности в Application Insights</span><span class="sxs-lookup"><span data-stu-id="9ec07-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="9ec07-104">В Windows предусмотрены самые разные [счетчики производительности](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters), которые отображают показатели использования ЦП, памяти, диска и сети.</span><span class="sxs-lookup"><span data-stu-id="9ec07-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="9ec07-105">Также вы можете определить собственные счетчики.</span><span class="sxs-lookup"><span data-stu-id="9ec07-105">You can also define your own.</span></span> <span data-ttu-id="9ec07-106">[Application Insights](app-insights-overview.md) можно показать счетчики производительности, если приложение работает под управлением служб IIS на локальный узел или виртуальную машину toowhich пользователь иметь административный доступ.</span><span class="sxs-lookup"><span data-stu-id="9ec07-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine toowhich you have administrative access.</span></span> <span data-ttu-id="9ec07-107">Hello диаграммы показывают hello ресурсы доступны tooyour работающего приложения, а также может помочь tooidentify балансировки нагрузки между экземплярами сервера.</span><span class="sxs-lookup"><span data-stu-id="9ec07-107">hello charts indicate hello resources available tooyour live application, and can help tooidentify unbalanced load between server instances.</span></span>

<span data-ttu-id="9ec07-108">Счетчики производительности отображаются в колонке hello серверов, которая содержит таблицу, которая сегментирует экземпляром сервера.</span><span class="sxs-lookup"><span data-stu-id="9ec07-108">Performance counters appear in hello Servers blade, which includes a table that segments by server instance.</span></span>

![Счетчики производительности, отображаемые в Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="9ec07-110">(Счетчики производительности недоступны для веб-приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="9ec07-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="9ec07-111">Но вы можете [отправки диагностики Azure Insights tooApplication](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="9ec07-111">But you can [send Azure Diagnostics tooApplication Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="9ec07-112">Просмотр счетчиков</span><span class="sxs-lookup"><span data-stu-id="9ec07-112">View counters</span></span>
<span data-ttu-id="9ec07-113">Серверы колонке Hello показан набор по умолчанию счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="9ec07-113">hello Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="9ec07-114">toosee другие счетчики изменить hello диаграмм, в колонке серверы hello, или откройте новое [обозревателя метрик](app-insights-metrics-explorer.md) колонки и добавление новых диаграмм.</span><span class="sxs-lookup"><span data-stu-id="9ec07-114">toosee other counters, either edit hello charts on hello Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="9ec07-115">Доступные счетчики Hello, перечислены как метрики при редактировании диаграммы.</span><span class="sxs-lookup"><span data-stu-id="9ec07-115">hello available counters are listed as metrics when you edit a chart.</span></span>

![Счетчики производительности, отображаемые в Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="9ec07-117">создать все чаще диаграммы в одном месте toosee [мониторинга](app-insights-dashboards.md) и закреплять их tooit.</span><span class="sxs-lookup"><span data-stu-id="9ec07-117">toosee all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them tooit.</span></span>

## <a name="add-counters"></a><span data-ttu-id="9ec07-118">Добавление счетчиков</span><span class="sxs-lookup"><span data-stu-id="9ec07-118">Add counters</span></span>
<span data-ttu-id="9ec07-119">Если hello счетчиков производительности, которые вы хотите не отображаются в списке hello метрик, так как пакет SDK Application Insights hello не сбор в веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="9ec07-119">If hello performance counter you want isn't shown in hello list of metrics, that's because hello Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="9ec07-120">Можно настроить его toodo таким образом.</span><span class="sxs-lookup"><span data-stu-id="9ec07-120">You can configure it toodo so.</span></span>

1. <span data-ttu-id="9ec07-121">Узнайте, какие счетчики доступны на сервере с помощью этой команды PowerShell на сервере hello:</span><span class="sxs-lookup"><span data-stu-id="9ec07-121">Find out what counters are available in your server by using this PowerShell command at hello server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="9ec07-122">(См. [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span><span class="sxs-lookup"><span data-stu-id="9ec07-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="9ec07-123">Откройте файл ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="9ec07-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="9ec07-124">Если вы добавили Application Insights tooyour приложения во время разработки, измените файл ApplicationInsights.config в проекте и повторно развернуть серверы tooyour.</span><span class="sxs-lookup"><span data-stu-id="9ec07-124">If you added Application Insights tooyour app during development, edit ApplicationInsights.config in your project, and then re-deploy it tooyour servers.</span></span>
   * <span data-ttu-id="9ec07-125">Если вы использовали tooinstrument монитор состояния веб-приложения во время выполнения, найти файл ApplicationInsights.config в корневой каталог hello приложение hello в службах IIS.</span><span class="sxs-lookup"><span data-stu-id="9ec07-125">If you used Status Monitor tooinstrument a web app at runtime, find ApplicationInsights.config in hello root directory of hello app in IIS.</span></span> <span data-ttu-id="9ec07-126">Обновите его в этом расположении на каждом экземпляре сервера.</span><span class="sxs-lookup"><span data-stu-id="9ec07-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="9ec07-127">Изменение hello производительности сборщика директивы:</span><span class="sxs-lookup"><span data-stu-id="9ec07-127">Edit hello performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="9ec07-128">Вы можете собирать показания как стандартных счетчиков, так и созданных вами самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="9ec07-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="9ec07-129">Например, стандартный счетчик `\Objects\Processes` доступен во всех системах Windows.</span><span class="sxs-lookup"><span data-stu-id="9ec07-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="9ec07-130">Пример пользовательского счетчика, который можно реализовать в веб-службе: `\Sales(photo)\# Items Sold`.</span><span class="sxs-lookup"><span data-stu-id="9ec07-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="9ec07-131">Формат Hello `\Category(instance)\Counter"`, или категорий, которые не имеют экземпляров, просто `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="9ec07-131">hello format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="9ec07-132">`ReportAs`требуется для имен счетчиков, которые не соответствуют `[a-zA-Z()/-_ \.]+` -то есть, они содержат символы, которые не находятся в следующих наборов hello: буквы в круглые скобки, косой черты, дефиса, подчеркивания, пространство, точка.</span><span class="sxs-lookup"><span data-stu-id="9ec07-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in hello following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="9ec07-133">При указании экземпляра он соберет указываемая метрика измерения «CounterInstanceName» из hello.</span><span class="sxs-lookup"><span data-stu-id="9ec07-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of hello reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="9ec07-134">Сбор данных счетчиков производительности в коде</span><span class="sxs-lookup"><span data-stu-id="9ec07-134">Collecting performance counters in code</span></span>
<span data-ttu-id="9ec07-135">производительность системы toocollect счетчиков и отправлять их tooApplication аналитики, вы можете адаптировать в приведенном ниже фрагменте hello:</span><span class="sxs-lookup"><span data-stu-id="9ec07-135">toocollect system performance counters and send them tooApplication Insights, you can adapt hello snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="9ec07-136">Или можно сделать то же самое с настраиваемых метрик, которые вы создали hello:</span><span class="sxs-lookup"><span data-stu-id="9ec07-136">Or you can do hello same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="9ec07-137">Счетчики производительности в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="9ec07-137">Performance counters in Analytics</span></span>
<span data-ttu-id="9ec07-138">В [службе аналитики](app-insights-analytics.md) можно выполнять поиск отчетов по счетчикам производительности и отображать их.</span><span class="sxs-lookup"><span data-stu-id="9ec07-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="9ec07-139">Hello **performanceCounters** схема предоставляет hello `category`, `counter` имя, и `instance` имя каждого счетчика производительности.</span><span class="sxs-lookup"><span data-stu-id="9ec07-139">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="9ec07-140">Hello данные телеметрии для каждого приложения вы увидите только hello счетчики для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="9ec07-140">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="9ec07-141">Например, toosee какие счетчики доступны:</span><span class="sxs-lookup"><span data-stu-id="9ec07-141">For example, toosee what counters are available:</span></span> 

![Счетчики производительности в аналитике Application Insights](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="9ec07-143">(Здесь «Instance» ссылается экземпляр счетчика производительности toohello, не hello роли или машины экземпляра сервера.</span><span class="sxs-lookup"><span data-stu-id="9ec07-143">('Instance' here refers toohello performance counter instance,  not hello role or server machine instance.</span></span> <span data-ttu-id="9ec07-144">Имя экземпляра счетчика производительности Hello обычно сегменты счетчиков, например процессорного времени, именем hello hello процесс или приложение.)</span><span class="sxs-lookup"><span data-stu-id="9ec07-144">hello performance counter instance name typically segments counters such as processor time by hello name of hello process or application.)</span></span>

<span data-ttu-id="9ec07-145">tooget диаграммы доступной памяти за последний период hello:</span><span class="sxs-lookup"><span data-stu-id="9ec07-145">tooget a chart of available memory over hello recent period:</span></span> 

![Временная диаграмма памяти в аналитике Application Insights](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="9ec07-147">Как и другие данные телеметрии **performanceCounters** также есть столбец `cloud_RoleInstance` указывает удостоверение hello hello экземпляр основного сервера, на котором выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="9ec07-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host server instance on which your app is running.</span></span> <span data-ttu-id="9ec07-148">Например toocompare hello производительности приложения на разных компьютерах hello:</span><span class="sxs-lookup"><span data-stu-id="9ec07-148">For example, toocompare hello performance of your app on hello different machines:</span></span> 

![Производительность, сегментированная по экземпляру роли в аналитике Application Insights](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="9ec07-150">ASP.NET и счетчики Application Insights</span><span class="sxs-lookup"><span data-stu-id="9ec07-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="9ec07-151">*Что такое hello различие между скорость исключение hello и метрики, исключения*</span><span class="sxs-lookup"><span data-stu-id="9ec07-151">*What's hello difference between hello Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="9ec07-152">*Частота исключений* — это системный счетчик производительности.</span><span class="sxs-lookup"><span data-stu-id="9ec07-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="9ec07-153">Hello CLR подсчитывает все обрабатываются hello и необработанные исключения, которые были созданы и делит общий hello в интервале выборки hello продолжительность интервала hello.</span><span class="sxs-lookup"><span data-stu-id="9ec07-153">hello CLR counts all hello handled and unhandled exceptions that are thrown, and divides hello total in a sampling interval by hello length of hello interval.</span></span> <span data-ttu-id="9ec07-154">пакет SDK для Application Insights Hello собирает этот результат и отправляет их toohello портала.</span><span class="sxs-lookup"><span data-stu-id="9ec07-154">hello Application Insights SDK collects this result and sends it toohello portal.</span></span>
* <span data-ttu-id="9ec07-155">*Исключения* представляет собой число hello TrackException отчеты, полученных портала hello в интервале выборки hello hello диаграммы.</span><span class="sxs-lookup"><span data-stu-id="9ec07-155">*Exceptions* is a count of hello TrackException reports received by hello portal in hello sampling interval of hello chart.</span></span> <span data-ttu-id="9ec07-156">Он включает только hello обработанных исключений, где вы написали TrackException вызывает в коде, а не включает все [необработанные исключения](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="9ec07-156">It includes only hello handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="9ec07-157">Оповещения</span><span class="sxs-lookup"><span data-stu-id="9ec07-157">Alerts</span></span>
<span data-ttu-id="9ec07-158">Как и другие показатели, вы можете [настроить оповещение](app-insights-alerts.md) toowarn, если счетчик производительности выйдет за пределы ограничения указывается.</span><span class="sxs-lookup"><span data-stu-id="9ec07-158">Like other metrics, you can [set an alert](app-insights-alerts.md) toowarn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="9ec07-159">Откройте колонку оповещения hello и нажмите кнопку Добавить оповещение.</span><span class="sxs-lookup"><span data-stu-id="9ec07-159">Open hello Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="9ec07-160"><a name="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9ec07-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="9ec07-161">Отслеживание зависимостей</span><span class="sxs-lookup"><span data-stu-id="9ec07-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="9ec07-162">Отслеживание исключений</span><span class="sxs-lookup"><span data-stu-id="9ec07-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

