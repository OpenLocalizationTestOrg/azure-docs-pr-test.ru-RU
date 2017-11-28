---
title: "Счетчики производительности в Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: 038d6e051be8112b9264e7efa6485965d11e32c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="aa0ac-103">Системные счетчики производительности в Application Insights</span><span class="sxs-lookup"><span data-stu-id="aa0ac-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="aa0ac-104">В Windows предусмотрены самые разные [счетчики производительности](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters), которые отображают показатели использования ЦП, памяти, диска и сети.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="aa0ac-105">Также вы можете определить собственные счетчики.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-105">You can also define your own.</span></span> <span data-ttu-id="aa0ac-106">[Application Insights](app-insights-overview.md) отображает эти счетчики производительности, если приложение запущено под управлением службы IIS на локальном узле или виртуальной машине, к которой у вас есть доступ с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine to which you have administrative access.</span></span> <span data-ttu-id="aa0ac-107">Диаграммы показывают, какие ресурсы доступны для запущенного приложения, а также позволяют обнаружить неравномерность в загрузке экземпляров сервера.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-107">The charts indicate the resources available to your live application, and can help to identify unbalanced load between server instances.</span></span>

<span data-ttu-id="aa0ac-108">Счетчики производительности отображаются в колонке "Серверы", где представлена таблица с разбивкой по экземплярам сервера.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-108">Performance counters appear in the Servers blade, which includes a table that segments by server instance.</span></span>

![Счетчики производительности, отображаемые в Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="aa0ac-110">(Счетчики производительности недоступны для веб-приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="aa0ac-111">Но зато вы можете [отправить данные системы диагностики Azure в Application Insights](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="aa0ac-111">But you can [send Azure Diagnostics to Application Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="aa0ac-112">Просмотр счетчиков</span><span class="sxs-lookup"><span data-stu-id="aa0ac-112">View counters</span></span>
<span data-ttu-id="aa0ac-113">В колонке "Серверы" показывается стандартный набор счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-113">The Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="aa0ac-114">Чтобы увидеть другие счетчики, измените диаграммы в колонке "Серверы" или откройте новую колонку [Обозревателя метрик](app-insights-metrics-explorer.md) и добавьте в нее новые диаграммы.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-114">To see other counters, either edit the charts on the Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="aa0ac-115">При изменении диаграммы все доступные счетчики указываются в разделе метрик.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-115">The available counters are listed as metrics when you edit a chart.</span></span>

![Счетчики производительности, отображаемые в Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="aa0ac-117">Чтобы собрать в одном месте все важнейшие диаграммы, создайте [панель мониторинга](app-insights-dashboards.md) и закрепите на ней нужные диаграммы.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-117">To see all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them to it.</span></span>

## <a name="add-counters"></a><span data-ttu-id="aa0ac-118">Добавление счетчиков</span><span class="sxs-lookup"><span data-stu-id="aa0ac-118">Add counters</span></span>
<span data-ttu-id="aa0ac-119">Если нужный счетчик производительности не отображается в списке метрик, значит пакет SDK Application Insights не собирает сведения о нем на веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-119">If the performance counter you want isn't shown in the list of metrics, that's because the Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="aa0ac-120">Вы можете изменить настройки, чтобы разрешить сбор данных.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-120">You can configure it to do so.</span></span>

1. <span data-ttu-id="aa0ac-121">Чтобы получить список доступных счетчиков на сервер, выполните на сервере такую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="aa0ac-121">Find out what counters are available in your server by using this PowerShell command at the server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="aa0ac-122">(См. [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span><span class="sxs-lookup"><span data-stu-id="aa0ac-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="aa0ac-123">Откройте файл ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="aa0ac-124">Если вы добавили Application Insights в приложение во время разработки, отредактируйте файл ApplicationInsights.config в проекте и повторно разверните его на серверах.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-124">If you added Application Insights to your app during development, edit ApplicationInsights.config in your project, and then re-deploy it to your servers.</span></span>
   * <span data-ttu-id="aa0ac-125">Если монитор состояний использовался как инструментарий для веб-приложения во время выполнения, файл ApplicationInsights.config вы найдете в корневом каталоге приложения в IIS.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-125">If you used Status Monitor to instrument a web app at runtime, find ApplicationInsights.config in the root directory of the app in IIS.</span></span> <span data-ttu-id="aa0ac-126">Обновите его в этом расположении на каждом экземпляре сервера.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="aa0ac-127">Измените директиву сборщика данных производительности:</span><span class="sxs-lookup"><span data-stu-id="aa0ac-127">Edit the performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="aa0ac-128">Вы можете собирать показания как стандартных счетчиков, так и созданных вами самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="aa0ac-129">Например, стандартный счетчик `\Objects\Processes` доступен во всех системах Windows.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="aa0ac-130">Пример пользовательского счетчика, который можно реализовать в веб-службе: `\Sales(photo)\# Items Sold`.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="aa0ac-131">Используется формат `\Category(instance)\Counter"`, а для категорий без экземпляров — просто `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-131">The format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="aa0ac-132">`ReportAs` — обязательный параметр для счетчиков, имена которых не соответствуют маске `[a-zA-Z()/-_ \.]+`, т. е. содержат любые символы, не входящие в этот стандартный набор: буквы, круглые скобки, косую черту, дефис, символ подчеркивания, пробел и точку.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in the following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="aa0ac-133">При указании экземпляра он будет собираться в качестве измерения CounterInstanceName обнаруженной метрики.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of the reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="aa0ac-134">Сбор данных счетчиков производительности в коде</span><span class="sxs-lookup"><span data-stu-id="aa0ac-134">Collecting performance counters in code</span></span>
<span data-ttu-id="aa0ac-135">Чтобы собрать данные счетчиков производительности системы и передать их в Application Insights, можно использовать следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="aa0ac-135">To collect system performance counters and send them to Application Insights, you can adapt the snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="aa0ac-136">То же самое можно сделать с пользовательскими метриками, созданными вами:</span><span class="sxs-lookup"><span data-stu-id="aa0ac-136">Or you can do the same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="aa0ac-137">Счетчики производительности в службе аналитики</span><span class="sxs-lookup"><span data-stu-id="aa0ac-137">Performance counters in Analytics</span></span>
<span data-ttu-id="aa0ac-138">В [службе аналитики](app-insights-analytics.md) можно выполнять поиск отчетов по счетчикам производительности и отображать их.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="aa0ac-139">Схема **PerformanceCounters** предоставляет `category`, имя `counter` и имя `instance` каждого счетчика производительности.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-139">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="aa0ac-140">В данных телеметрии для каждого приложения вы увидите только счетчики для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-140">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="aa0ac-141">Например, вот как можно увидеть, какие счетчики доступны.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-141">For example, to see what counters are available:</span></span> 

![Счетчики производительности в аналитике Application Insights](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="aa0ac-143">(Экземпляр здесь обозначает экземпляр счетчика производительности, а не экземпляр роли или сервера.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-143">('Instance' here refers to the performance counter instance,  not the role or server machine instance.</span></span> <span data-ttu-id="aa0ac-144">Имя экземпляра счетчика производительности обычно разделяет такие счетчики, как загруженность процессора, по именам процессов или приложений.)</span><span class="sxs-lookup"><span data-stu-id="aa0ac-144">The performance counter instance name typically segments counters such as processor time by the name of the process or application.)</span></span>

<span data-ttu-id="aa0ac-145">Вот как можно получить диаграмму доступной памяти за последний период.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-145">To get a chart of available memory over the recent period:</span></span> 

![Временная диаграмма памяти в аналитике Application Insights](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="aa0ac-147">Как и другие данные телеметрии, данные **performanceCounters** также содержат столбец `cloud_RoleInstance`, который определяет экземпляр сервера, на котором выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host server instance on which your app is running.</span></span> <span data-ttu-id="aa0ac-148">Например, вот как можно сравнить производительность приложения на разных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-148">For example, to compare the performance of your app on the different machines:</span></span> 

![Производительность, сегментированная по экземпляру роли в аналитике Application Insights](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="aa0ac-150">ASP.NET и счетчики Application Insights</span><span class="sxs-lookup"><span data-stu-id="aa0ac-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="aa0ac-151">*Чем отличаются метрики "Частота исключений" и "Исключения"?*</span><span class="sxs-lookup"><span data-stu-id="aa0ac-151">*What's the difference between the Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="aa0ac-152">*Частота исключений* — это системный счетчик производительности.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="aa0ac-153">Среда CLR подсчитывает все обработанные и необработанные исключения и делит их общее количество в интервале выборки на продолжительность интервала.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-153">The CLR counts all the handled and unhandled exceptions that are thrown, and divides the total in a sampling interval by the length of the interval.</span></span> <span data-ttu-id="aa0ac-154">Пакет SDK Application Insights получает этот результат и отправляет его на портал.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-154">The Application Insights SDK collects this result and sends it to the portal.</span></span>
* <span data-ttu-id="aa0ac-155">*Исключения* — это количество отчетов TrackException, полученных порталом в интервале выборки диаграммы.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-155">*Exceptions* is a count of the TrackException reports received by the portal in the sampling interval of the chart.</span></span> <span data-ttu-id="aa0ac-156">Включает только обработанные исключения, в коде которых прописаны вызовы TrackException, и не включает [необработанные исключения](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="aa0ac-156">It includes only the handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="aa0ac-157">Оповещения</span><span class="sxs-lookup"><span data-stu-id="aa0ac-157">Alerts</span></span>
<span data-ttu-id="aa0ac-158">Как и для других метрик, вы можете [установить оповещение](app-insights-alerts.md), которое предупредит о выходе показаний счетчика производительности за установленные пределы.</span><span class="sxs-lookup"><span data-stu-id="aa0ac-158">Like other metrics, you can [set an alert](app-insights-alerts.md) to warn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="aa0ac-159">Откройте колонку "Оповещения" и щелкните "Добавить оповещение".</span><span class="sxs-lookup"><span data-stu-id="aa0ac-159">Open the Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="aa0ac-160"><a name="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aa0ac-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="aa0ac-161">Отслеживание зависимостей</span><span class="sxs-lookup"><span data-stu-id="aa0ac-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="aa0ac-162">Отслеживание исключений</span><span class="sxs-lookup"><span data-stu-id="aa0ac-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

