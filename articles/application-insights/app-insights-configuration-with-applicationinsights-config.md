---
title: "ссылка aaaApplicationInsights.config - Azure | Документы Microsoft"
description: "Включение или отключение модулей сбора данных и добавление счетчиков производительности, а также других параметров."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="5c158-103">Настройка hello пакет SDK Application Insights с ApplicationInsights.config или XML-файла</span><span class="sxs-lookup"><span data-stu-id="5c158-103">Configuring hello Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="5c158-104">пакет SDK для Application Insights .NET Hello состоит из нескольких пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c158-104">hello Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="5c158-105">[Базовый пакет](http://www.nuget.org/packages/Microsoft.ApplicationInsights) предоставляет hello API для отправки телеметрии Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides hello API for sending telemetry to hello Application Insights.</span></span> <span data-ttu-id="5c158-106">[Дополнительные пакеты](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) предоставляют *модули* и *инициализаторы* телеметрии для автоматического отслеживания телеметрии вашего приложения и его контекста.</span><span class="sxs-lookup"><span data-stu-id="5c158-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="5c158-107">Перемещая hello файл конфигурации, можно включить или отключить модули телеметрии и инициализаторы и задать параметры для некоторых из них.</span><span class="sxs-lookup"><span data-stu-id="5c158-107">By adjusting hello configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="5c158-108">файл конфигурации Hello называется `ApplicationInsights.config` или `ApplicationInsights.xml`, в зависимости от типа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-108">hello configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on hello type of your application.</span></span> <span data-ttu-id="5c158-109">Она автоматически добавляется tooyour проекта при вы [установки большинства версий пакета SDK для hello][start].</span><span class="sxs-lookup"><span data-stu-id="5c158-109">It is automatically added tooyour project when you [install most versions of hello SDK][start].</span></span> <span data-ttu-id="5c158-110">Также добавляется tooa веб-приложения с [монитор состояния на сервере IIS][redfield], или при выборе аналитики приложения hello [расширения для веб-сайта Azure или виртуальной Машины](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="5c158-110">It is also added tooa web app by [Status Monitor on an IIS server][redfield], or when you select hello Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="5c158-111">Нет hello toocontrol эквивалентный файл [SDK веб-странице][client].</span><span class="sxs-lookup"><span data-stu-id="5c158-111">There isn't an equivalent file toocontrol hello [SDK in a web page][client].</span></span>

<span data-ttu-id="5c158-112">В этом документе описаны разделы hello, отображаемые в конфигурации hello файла, как они управляют компонентами hello hello SDK, и какие пакеты NuGet загрузки этих компонентов.</span><span class="sxs-lookup"><span data-stu-id="5c158-112">This document describes hello sections you see in hello configuration file, how they control hello components of hello SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="5c158-113">Модули телеметрии (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="5c158-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="5c158-114">Каждый модуль телеметрии собирает конкретного типа данных и использует hello основных данных hello toosend API.</span><span class="sxs-lookup"><span data-stu-id="5c158-114">Each telemetry module collects a specific type of data and uses hello core API toosend hello data.</span></span> <span data-ttu-id="5c158-115">Hello модули устанавливаются различные пакеты NuGet, которые также добавить требуемые строки toohello hello config-файла.</span><span class="sxs-lookup"><span data-stu-id="5c158-115">hello modules are installed by different NuGet packages, which also add hello required lines toohello .config file.</span></span>

<span data-ttu-id="5c158-116">Есть такой узел в файле конфигурации hello для каждого модуля.</span><span class="sxs-lookup"><span data-stu-id="5c158-116">There's a node in hello configuration file for each module.</span></span> <span data-ttu-id="5c158-117">toodisable модуля, удалите узел hello или закомментируйте его.</span><span class="sxs-lookup"><span data-stu-id="5c158-117">toodisable a module, delete hello node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="5c158-118">Отслеживание зависимостей</span><span class="sxs-lookup"><span data-stu-id="5c158-118">Dependency Tracking</span></span>
<span data-ttu-id="5c158-119">[Отслеживание зависимостей](app-insights-asp-net-dependencies.md) собирает данные телеметрии об обращениях приложение делает toodatabases и внешних служб и баз данных.</span><span class="sxs-lookup"><span data-stu-id="5c158-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes toodatabases and external services and databases.</span></span> <span data-ttu-id="5c158-120">tooallow toowork этот модуль на сервере IIS, необходимо слишком[установите монитор состояния][redfield].</span><span class="sxs-lookup"><span data-stu-id="5c158-120">tooallow this module toowork in an IIS server, you need too[install Status Monitor][redfield].</span></span> <span data-ttu-id="5c158-121">toouse его в веб-приложениях Azure или на виртуальных машинах, [выберите расширение Application Insights hello](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="5c158-121">toouse it in Azure web apps or VMs, [select hello Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="5c158-122">Можно также написать собственную слежения кода с помощью hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="5c158-122">You can also write your own dependency tracking code using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="5c158-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .</span><span class="sxs-lookup"><span data-stu-id="5c158-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="5c158-124">Сборщик данных производительности</span><span class="sxs-lookup"><span data-stu-id="5c158-124">Performance collector</span></span>
<span data-ttu-id="5c158-125">[Собирает данные счетчиков производительности системы](app-insights-performance-counters.md), например ЦП, памяти и сетевой нагрузки из установок IIS.</span><span class="sxs-lookup"><span data-stu-id="5c158-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="5c158-126">Можно указать, какие счетчики toocollect, включая счетчики производительности, которые вы настроили самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="5c158-126">You can specify which counters toocollect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="5c158-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .</span><span class="sxs-lookup"><span data-stu-id="5c158-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="5c158-128">Телеметрия диагностики Application Insights</span><span class="sxs-lookup"><span data-stu-id="5c158-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="5c158-129">Hello `DiagnosticsTelemetryModule` сообщает об ошибках в hello сам код инструментирования Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5c158-129">hello `DiagnosticsTelemetryModule` reports errors in hello Application Insights instrumentation code itself.</span></span> <span data-ttu-id="5c158-130">Например если код hello не может получить доступ к счетчики производительности или `ITelemetryInitializer` приводит к возникновению исключения.</span><span class="sxs-lookup"><span data-stu-id="5c158-130">For example, if hello code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="5c158-131">Отслеживается этим модулем телеметрии трассировки отображается в hello [диагностики поиска][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="5c158-131">Trace telemetry tracked by this module appears in hello [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="5c158-132">Отправляет toodc.services.vsallin.net диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="5c158-132">Sends diagnostic data toodc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="5c158-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="5c158-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="5c158-134">При установке этого пакета только файл ApplicationInsights.config hello не создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="5c158-134">If you only install this package, hello ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="5c158-135">Режим разработчика</span><span class="sxs-lookup"><span data-stu-id="5c158-135">Developer Mode</span></span>
<span data-ttu-id="5c158-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`принудительно вызывает hello Application Insights `TelemetryChannel` toosend немедленно, данных телеметрии одного элемента за раз, когда отладчик находится присоединенного toohello процесс приложения.</span><span class="sxs-lookup"><span data-stu-id="5c158-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces hello Application Insights `TelemetryChannel` toosend data immediately, one telemetry item at a time, when a debugger is attached toohello application process.</span></span> <span data-ttu-id="5c158-137">Это уменьшает hello промежуток времени между hello момент, когда приложение отслеживает телеметрии и когда он появится на портале Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-137">This reduces hello amount of time between hello moment when your application tracks telemetry and when it appears on hello Application Insights portal.</span></span> <span data-ttu-id="5c158-138">Это вызывает значительную нагрузку на процессор и пропускную способность сети.</span><span class="sxs-lookup"><span data-stu-id="5c158-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="5c158-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) </span><span class="sxs-lookup"><span data-stu-id="5c158-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="5c158-140">Отслеживание веб-запросов</span><span class="sxs-lookup"><span data-stu-id="5c158-140">Web Request Tracking</span></span>
<span data-ttu-id="5c158-141">Отчеты hello [время и результат код ответа](app-insights-asp-net.md) HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="5c158-141">Reports hello [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="5c158-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) </span><span class="sxs-lookup"><span data-stu-id="5c158-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="5c158-143">Отслеживание исключений</span><span class="sxs-lookup"><span data-stu-id="5c158-143">Exception tracking</span></span>
<span data-ttu-id="5c158-144">`ExceptionTrackingTelemetryModule` отслеживает количество необработанных исключений в вашем веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="5c158-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="5c158-145">Ознакомьтесь со статьей [Ошибки и исключения][exceptions].</span><span class="sxs-lookup"><span data-stu-id="5c158-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="5c158-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) </span><span class="sxs-lookup"><span data-stu-id="5c158-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="5c158-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` отслеживает [незамеченные исключения задач](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c158-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="5c158-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` отслеживает необработанные исключения для рабочих ролей, служб Windows и консольных приложений.</span><span class="sxs-lookup"><span data-stu-id="5c158-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="5c158-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .</span><span class="sxs-lookup"><span data-stu-id="5c158-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="5c158-150">Отслеживание EventSource</span><span class="sxs-lookup"><span data-stu-id="5c158-150">EventSource Tracking</span></span>
<span data-ttu-id="5c158-151">`EventSourceTelemetryModule`позволяет tooconfigure toobe события EventSource отправлен tooApplication аналитики как трассировок.</span><span class="sxs-lookup"><span data-stu-id="5c158-151">`EventSourceTelemetryModule` allows you tooconfigure EventSource events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="5c158-152">Сведения об отслеживании событий EventSource см. в разделе [Использование событий EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="5c158-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="5c158-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="5c158-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="5c158-154">Трассировка событий Windows</span><span class="sxs-lookup"><span data-stu-id="5c158-154">ETW Event Tracking</span></span>
<span data-ttu-id="5c158-155">`EtwCollectorTelemetryModule`позволяет tooconfigure события из переданного tooApplication аналитики в качестве трассировки toobe поставщиков трассировки событий Windows.</span><span class="sxs-lookup"><span data-stu-id="5c158-155">`EtwCollectorTelemetryModule` allows you tooconfigure events from ETW providers toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="5c158-156">Сведения об отслеживании событий трассировки событий Windows см. в разделе [Использование событий трассировки событий Windows](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="5c158-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="5c158-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="5c158-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="5c158-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="5c158-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="5c158-159">пакет Microsoft.ApplicationInsights Hello предоставляет hello [основные API](https://msdn.microsoft.com/library/mt420197.aspx) из пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-159">hello Microsoft.ApplicationInsights package provides hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) of hello SDK.</span></span> <span data-ttu-id="5c158-160">Hello другие модули телеметрии этот метод следует использовать, и вы также можете [toodefine использовать собственные телеметрии](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="5c158-160">hello other telemetry modules use this, and you can also [use it toodefine your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="5c158-161">Нет записей в файле ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="5c158-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="5c158-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="5c158-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="5c158-163">Если просто установить этот пакет NuGet, CONFIG-файл не создается.</span><span class="sxs-lookup"><span data-stu-id="5c158-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="5c158-164">Канал телеметрии</span><span class="sxs-lookup"><span data-stu-id="5c158-164">Telemetry Channel</span></span>
<span data-ttu-id="5c158-165">Hello телеметрии канала управляет буферизацией и передачу данных телеметрии toohello служба Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5c158-165">hello telemetry channel manages buffering and transmission of telemetry toohello Application Insights service.</span></span>

* <span data-ttu-id="5c158-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`— hello канал по умолчанию для служб.</span><span class="sxs-lookup"><span data-stu-id="5c158-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is hello default channel for services.</span></span> <span data-ttu-id="5c158-167">Он создает буфер данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="5c158-167">It buffers data in memory.</span></span>
* <span data-ttu-id="5c158-168">`Microsoft.ApplicationInsights.PersistenceChannel` — альтернатива для консольных приложений.</span><span class="sxs-lookup"><span data-stu-id="5c158-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="5c158-169">Он может сэкономить любое хранилище данных unflushed toopersistent при закрывает приложение и отправит его при запуске приложение hello, еще раз.</span><span class="sxs-lookup"><span data-stu-id="5c158-169">It can save any unflushed data toopersistent storage when your app closes down, and will send it when hello app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="5c158-170">Инициализаторы телеметрии (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="5c158-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="5c158-171">Инициализаторы телеметрии задают свойства контекста, которые отправляются вместе с каждым элементом телеметрии.</span><span class="sxs-lookup"><span data-stu-id="5c158-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="5c158-172">Вы можете [написать собственные инициализаторы](app-insights-api-filtering-sampling.md#add-properties) tooset свойства контекста.</span><span class="sxs-lookup"><span data-stu-id="5c158-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) tooset context properties.</span></span>

<span data-ttu-id="5c158-173">Стандартная инициализаторы Hello установлено либо hello пакетов WindowsServer NuGet или веб:</span><span class="sxs-lookup"><span data-stu-id="5c158-173">hello standard initializers are all set either by hello Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="5c158-174">`AccountIdTelemetryInitializer`Задает свойство AccountId hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-174">`AccountIdTelemetryInitializer` sets hello AccountId property.</span></span>
* <span data-ttu-id="5c158-175">`AuthenticatedUserIdTelemetryInitializer`Задает свойство AuthenticatedUserId hello как набор с hello JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="5c158-175">`AuthenticatedUserIdTelemetryInitializer` sets hello AuthenticatedUserId property as set by hello JavaScript SDK.</span></span>
* <span data-ttu-id="5c158-176">`AzureRoleEnvironmentTelemetryInitializer`обновления hello `RoleName` и `RoleInstance` свойства hello `Device` контекст для всех элементов телеметрии с помощью данных, извлеченных из среды выполнения Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-176">`AzureRoleEnvironmentTelemetryInitializer` updates hello `RoleName` and `RoleInstance` properties of hello `Device` context for all telemetry items with information extracted from hello Azure runtime environment.</span></span>
* <span data-ttu-id="5c158-177">`BuildInfoConfigComponentVersionTelemetryInitializer`обновления hello `Version` свойство hello `Component` контекст для всех элементов телеметрии со значением hello, извлеченным из hello `BuildInfo.config` файл создан с помощью MS Build.</span><span class="sxs-lookup"><span data-stu-id="5c158-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates hello `Version` property of hello `Component` context for all telemetry items with hello value extracted from hello `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="5c158-178">`ClientIpHeaderTelemetryInitializer`обновления `Ip` свойство hello `Location` контекст всех элементов телеметрии на основании hello `X-Forwarded-For` заголовок HTTP запроса hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of hello `Location` context of all telemetry items based on hello `X-Forwarded-For` HTTP header of hello request.</span></span>
* <span data-ttu-id="5c158-179">`DeviceTelemetryInitializer`следующие свойства объекта hello hello обновления `Device` контекст для всех элементов телеметрии.</span><span class="sxs-lookup"><span data-stu-id="5c158-179">`DeviceTelemetryInitializer` updates hello following properties of hello `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="5c158-180">`Type`задано слишком «PC»</span><span class="sxs-lookup"><span data-stu-id="5c158-180">`Type` is set too"PC"</span></span>
  * <span data-ttu-id="5c158-181">`Id`имеет значение toohello доменное имя компьютера hello, где работает веб-приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-181">`Id` is set toohello domain name of hello computer where hello web application is running.</span></span>
  * <span data-ttu-id="5c158-182">`OemName`имеет значение toohello значение, извлеченное из hello `Win32_ComputerSystem.Manufacturer` поля с помощью инструментария WMI.</span><span class="sxs-lookup"><span data-stu-id="5c158-182">`OemName` is set toohello value extracted from hello `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="5c158-183">`Model`имеет значение toohello значение, извлеченное из hello `Win32_ComputerSystem.Model` поля с помощью инструментария WMI.</span><span class="sxs-lookup"><span data-stu-id="5c158-183">`Model` is set toohello value extracted from hello `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="5c158-184">`NetworkType`имеет значение toohello значение, извлеченное из hello `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="5c158-184">`NetworkType` is set toohello value extracted from hello `NetworkInterface`.</span></span>
  * <span data-ttu-id="5c158-185">`Language`задается имя toohello hello `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="5c158-185">`Language` is set toohello name of hello `CurrentCulture`.</span></span>
* <span data-ttu-id="5c158-186">`DomainNameRoleInstanceTelemetryInitializer`обновления hello `RoleInstance` свойство hello `Device` контекст для всех элементов телеметрии с доменным именем hello hello компьютера, где выполняется веб-приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-186">`DomainNameRoleInstanceTelemetryInitializer` updates hello `RoleInstance` property of hello `Device` context for all telemetry items with hello domain name of hello computer where hello web application is running.</span></span>
* <span data-ttu-id="5c158-187">`OperationNameTelemetryInitializer`обновления hello `Name` свойство hello `RequestTelemetry` и hello `Name` свойство hello `Operation` контекст всех элементов телеметрии зависимости от метода hello HTTP, а также имена hello вызванный tooprocess контроллера и действия ASP.NET MVC запрос.</span><span class="sxs-lookup"><span data-stu-id="5c158-187">`OperationNameTelemetryInitializer` updates hello `Name` property of hello `RequestTelemetry` and hello `Name` property of hello `Operation` context of all telemetry items based on hello HTTP method, as well as names of ASP.NET MVC controller and action invoked tooprocess hello request.</span></span>
* <span data-ttu-id="5c158-188">`OperationIdTelemetryInitializer`или `OperationCorrelationTelemetryInitializer` обновления hello `Operation.Id` контекстное свойство всех элементов телеметрии отслеживаются во время обработки запроса с hello автоматически создается `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="5c158-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates hello `Operation.Id` context property of all telemetry items tracked while handling a request with hello automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="5c158-189">`SessionTelemetryInitializer`обновления hello `Id` свойство hello `Session` контекст для всех элементов телеметрии с значение, извлеченное из hello `ai_session` cookie созданные hello код инструментирования ApplicationInsights JavaScript, выполняются в браузере пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-189">`SessionTelemetryInitializer` updates hello `Id` property of hello `Session` context for all telemetry items with value extracted from hello `ai_session` cookie generated by hello ApplicationInsights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="5c158-190">`SyntheticTelemetryInitializer`или `SyntheticUserAgentTelemetryInitializer` обновления hello `User`, `Session` и `Operation` контекстов свойств всех элементов телеметрии отслеживаются при обработке запроса от искусственного источника, например доступности тестирования или выполните поиск программ-роботов ядра.</span><span class="sxs-lookup"><span data-stu-id="5c158-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates hello `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="5c158-191">По умолчанию [обозреватель метрик](app-insights-metrics-explorer.md) не отображает данные телеметрии искусственных источников.</span><span class="sxs-lookup"><span data-stu-id="5c158-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="5c158-192">Hello `<Filters>` задать определение свойств запросов на hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-192">hello `<Filters>` set identifying properties of hello requests.</span></span>
* <span data-ttu-id="5c158-193">`UserAgentTelemetryInitializer`обновления hello `UserAgent` свойство hello `User` контекст всех элементов телеметрии на основании hello `User-Agent` заголовок HTTP запроса hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-193">`UserAgentTelemetryInitializer` updates hello `UserAgent` property of hello `User` context of all telemetry items based on hello `User-Agent` HTTP header of hello request.</span></span>
* <span data-ttu-id="5c158-194">`UserTelemetryInitializer`обновления hello `Id` и `AcquisitionDate` свойства `User` контекст для всех элементов телеметрии со значения, извлеченные из hello `ai_user` куки-файл, созданный код инструментирования Application Insights JavaScript hello, выполняемый в hello браузер пользователя.</span><span class="sxs-lookup"><span data-stu-id="5c158-194">`UserTelemetryInitializer` updates hello `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from hello `ai_user` cookie generated by hello Application Insights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="5c158-195">`WebTestTelemetryInitializer`для HTTP-запросы, поставляемые с наборами hello идентификатор пользователя, идентификатор сеанса и свойства источника искусственных [тестов доступности](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="5c158-195">`WebTestTelemetryInitializer` sets hello user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="5c158-196">Hello `<Filters>` задать определение свойств запросов на hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-196">hello `<Filters>` set identifying properties of hello requests.</span></span>

<span data-ttu-id="5c158-197">Для приложений .NET, работающих в Service Fabric, можно включить hello `Microsoft.ApplicationInsights.ServiceFabric` пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c158-197">For .NET applications running in Service Fabric, you can include hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="5c158-198">Этот пакет включает в себя `FabricTelemetryInitializer`, который добавляет элементы tootelemetry свойств Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5c158-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties tootelemetry items.</span></span> <span data-ttu-id="5c158-199">Дополнительные сведения см. в разделе hello [странице GitHub](https://go.microsoft.com/fwlink/?linkid=848457) о свойствах hello, добавленные в этот пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c158-199">For more information, see hello [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about hello properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="5c158-200">Обработчики данных телеметрии (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="5c158-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="5c158-201">Процессоры телеметрии можно фильтровать и изменения каждого элемента телеметрии непосредственно перед отправкой с портала toohello hello SDK.</span><span class="sxs-lookup"><span data-stu-id="5c158-201">Telemetry processors can filter and modify each telemetry item just before it is sent from hello SDK toohello portal.</span></span>

<span data-ttu-id="5c158-202">Вы можете [написать собственные обработчики данных телеметрии](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="5c158-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="5c158-203">Обработчик адаптивной выборки телеметрии (начиная с версии 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="5c158-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="5c158-204">Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5c158-204">This is enabled by default.</span></span> <span data-ttu-id="5c158-205">Если приложение отправляет слишком много телеметрических данных, обработчик удаляет часть из них.</span><span class="sxs-lookup"><span data-stu-id="5c158-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="5c158-206">параметр Hello предоставляет цели hello, Здравствуйте, алгоритм пытается tooachieve.</span><span class="sxs-lookup"><span data-stu-id="5c158-206">hello parameter provides hello target that hello algorithm tries tooachieve.</span></span> <span data-ttu-id="5c158-207">Каждый экземпляр hello работы пакета SDK для независимо друг от друга, поэтому если сервер находится в кластере из нескольких компьютеров, hello фактический объем телеметрии будут умножены соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="5c158-207">Each instance of hello SDK works independently, so if your server is a cluster of several machines, hello actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="5c158-208">[Дополнительная информация о выборке](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="5c158-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="5c158-209">Обработчик выборки телеметрии с фиксированной частотой (начиная с версии 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="5c158-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="5c158-210">Также имеется стандартный [обработчик выборочной телеметрии](app-insights-api-filtering-sampling.md) (начиная с версии 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="5c158-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="5c158-211">Параметры канала (Java)</span><span class="sxs-lookup"><span data-stu-id="5c158-211">Channel parameters (Java)</span></span>
<span data-ttu-id="5c158-212">Эти параметры влияют как следует хранить и очистка hello данные телеметрии, которые она собирает hello Java SDK.</span><span class="sxs-lookup"><span data-stu-id="5c158-212">These parameters affect how hello Java SDK should store and flush hello telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="5c158-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="5c158-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="5c158-214">количество элементов телеметрии, которые могут храниться в хранилище в памяти hello SDK Hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-214">hello number of telemetry items that can be stored in hello SDK's in-memory storage.</span></span> <span data-ttu-id="5c158-215">При достижении этого количества буфера телеметрии hello -, hello телеметрии элементы передаются серверу toohello Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5c158-215">When this number is reached, hello telemetry buffer is flushed - that is, hello telemetry items are sent toohello Application Insights server.</span></span>

* <span data-ttu-id="5c158-216">Мин. значение: 1.</span><span class="sxs-lookup"><span data-stu-id="5c158-216">Min: 1</span></span>
* <span data-ttu-id="5c158-217">Макс. значение: 1000.</span><span class="sxs-lookup"><span data-stu-id="5c158-217">Max: 1000</span></span>
* <span data-ttu-id="5c158-218">Значение по умолчанию: 500.</span><span class="sxs-lookup"><span data-stu-id="5c158-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="5c158-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="5c158-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="5c158-220">Определяет, как часто hello данные, хранящиеся в хранилище в памяти hello должна быть сброшены (отправленных tooApplication аналитики).</span><span class="sxs-lookup"><span data-stu-id="5c158-220">Determines how often hello data that is stored in hello in-memory storage should be flushed (sent tooApplication Insights).</span></span>

* <span data-ttu-id="5c158-221">Мин. значение: 1.</span><span class="sxs-lookup"><span data-stu-id="5c158-221">Min: 1</span></span>
* <span data-ttu-id="5c158-222">Макс. значение: 300.</span><span class="sxs-lookup"><span data-stu-id="5c158-222">Max: 300</span></span>
* <span data-ttu-id="5c158-223">Значение по умолчанию: 5.</span><span class="sxs-lookup"><span data-stu-id="5c158-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="5c158-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="5c158-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="5c158-225">Определяет hello максимальный размер в Мегабайтах, который выделяется toohello постоянное хранилище на локальном диске hello.</span><span class="sxs-lookup"><span data-stu-id="5c158-225">Determines hello maximum size in MB that is allotted toohello persistent storage on hello local disk.</span></span> <span data-ttu-id="5c158-226">Это хранилище используется для сохранения элементов телеметрии, сбой конечной точки Application Insights toohello toobe передачи.</span><span class="sxs-lookup"><span data-stu-id="5c158-226">This storage is used for persisting telemetry items that failed toobe transmitted toohello Application Insights endpoint.</span></span> <span data-ttu-id="5c158-227">При выполнении размер хранилища hello новые элементы данных телеметрии, будут отменены.</span><span class="sxs-lookup"><span data-stu-id="5c158-227">When hello storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="5c158-228">Мин. значение: 1.</span><span class="sxs-lookup"><span data-stu-id="5c158-228">Min: 1</span></span>
* <span data-ttu-id="5c158-229">Макс. значение: 100.</span><span class="sxs-lookup"><span data-stu-id="5c158-229">Max: 100</span></span>
* <span data-ttu-id="5c158-230">Значение по умолчанию: 10.</span><span class="sxs-lookup"><span data-stu-id="5c158-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="5c158-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="5c158-231">InstrumentationKey</span></span>
<span data-ttu-id="5c158-232">Определяет ресурс Application Insights hello, в котором отображается данных.</span><span class="sxs-lookup"><span data-stu-id="5c158-232">This determines hello Application Insights resource in which your data appears.</span></span> <span data-ttu-id="5c158-233">Обычно создается отдельный ресурс с отдельным ключом инструментирования для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="5c158-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="5c158-234">Если нужно tooset hello ключ динамически — например, если требуется toosend результаты из ресурсов приложения toodifferent - можно опустить hello ключ из файла конфигурации hello и установите его в коде.</span><span class="sxs-lookup"><span data-stu-id="5c158-234">If you want tooset hello key dynamically - for example if you want toosend results from your application toodifferent resources - you can omit hello key from hello configuration file, and set it in code instead.</span></span>

<span data-ttu-id="5c158-235">ключ hello tooset для всех экземпляров TelemetryClient, включая модули стандартной телеметрии, настройте раздел hello TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="5c158-235">tooset hello key for all instances of TelemetryClient, including standard telemetry modules, set hello key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="5c158-236">Задайте ключ в методе инициализации, таком как global.aspx.cs, в службе ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="5c158-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="5c158-237">Если необходимо просто toosend определенный набор событий tooa различных ресурсов, можно задать ключ hello для конкретных TelemetryClient:</span><span class="sxs-lookup"><span data-stu-id="5c158-237">If you just want toosend a specific set of events tooa different resource, you can set hello key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="5c158-238">новый ключ tooget [Создание ресурса на портале Application Insights hello][new].</span><span class="sxs-lookup"><span data-stu-id="5c158-238">tooget a new key, [create a new resource in hello Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c158-239">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c158-239">Next steps</span></span>
<span data-ttu-id="5c158-240">[Дополнительные сведения об hello API][api].</span><span class="sxs-lookup"><span data-stu-id="5c158-240">[Learn more about hello API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
