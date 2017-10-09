---
title: "журналы трассировки aaaExplore .NET в Application Insights"
description: "Поиск журналов, созданных с помощью Trace, Log4Net или NLog."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="15488-103">Просмотр журналов трассировки .NET в Application Insights</span><span class="sxs-lookup"><span data-stu-id="15488-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="15488-104">При использовании NLog, log4Net или System.Diagnostic.Trace для диагностической трассировки в приложении ASP.NET, что журналы отправлено слишком[Azure Application Insights][start], где вы можете анализировать и поиска их.</span><span class="sxs-lookup"><span data-stu-id="15488-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent too[Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="15488-105">Журналы будут объединены с другими hello телеметрии, поступающих из своего приложения, чтобы вы могли определить hello трассировки, связанные с обслуживанием каждого пользовательского запроса и сопоставлять их с другими событиями и отчеты об исключениях.</span><span class="sxs-lookup"><span data-stu-id="15488-105">Your logs will be merged with hello other telemetry coming from your application, so that you can identify hello traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="15488-106">Требуется модуля записи журнала hello?</span><span class="sxs-lookup"><span data-stu-id="15488-106">Do you need hello log capture module?</span></span> <span data-ttu-id="15488-107">Это полезный адаптер для сторонних средств ведения журнала, но если вы еще не используете NLog, log4Net или System.Diagnostics.Trace, рассмотрите возможность вызова [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) напрямую.</span><span class="sxs-lookup"><span data-stu-id="15488-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="15488-108">Установка ведения журнала в приложении</span><span class="sxs-lookup"><span data-stu-id="15488-108">Install logging on your app</span></span>
<span data-ttu-id="15488-109">Установите выбранную платформу ведения журналов в своем проекте.</span><span class="sxs-lookup"><span data-stu-id="15488-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="15488-110">При этом должна появиться запись в файлах app.config или web.config.</span><span class="sxs-lookup"><span data-stu-id="15488-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="15488-111">Если вы используете System.Diagnostics.Trace, необходимо tooadd tooweb.config входа.</span><span class="sxs-lookup"><span data-stu-id="15488-111">If you're using System.Diagnostics.Trace, you need tooadd an entry tooweb.config:</span></span>

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a><span data-ttu-id="15488-112">Настройка журналов toocollect Application Insights</span><span class="sxs-lookup"><span data-stu-id="15488-112">Configure Application Insights toocollect logs</span></span>
<span data-ttu-id="15488-113">**[Добавление проекта Application Insights tooyour](app-insights-asp-net.md)**  Если вы еще не сделали, еще.</span><span class="sxs-lookup"><span data-stu-id="15488-113">**[Add Application Insights tooyour project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="15488-114">Вы увидите параметр tooinclude hello сборщика данных журнала.</span><span class="sxs-lookup"><span data-stu-id="15488-114">You'll see an option tooinclude hello log collector.</span></span>

<span data-ttu-id="15488-115">Или выберите **Настроить Application Insights** , щелкнув правой кнопкой мыши на своем проекте в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="15488-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="15488-116">Выберите параметр hello слишком**настройки сбора данных трассировки**.</span><span class="sxs-lookup"><span data-stu-id="15488-116">Select hello option too**Configure trace collection**.</span></span>

<span data-ttu-id="15488-117">*Вы не видите меню Application Insights или параметр для включения сборщика журналов?*</span><span class="sxs-lookup"><span data-stu-id="15488-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="15488-118">Попробуйте выполнить [Устранение неполадок](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="15488-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="15488-119">Ручная установка</span><span class="sxs-lookup"><span data-stu-id="15488-119">Manual installation</span></span>
<span data-ttu-id="15488-120">Используйте этот метод, если ваш тип проекта не поддерживается программой установки Application Insights hello (например Windows рабочего стола проект).</span><span class="sxs-lookup"><span data-stu-id="15488-120">Use this method if your project type isn't supported by hello Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="15488-121">Если планируется toouse log4Net или NLog, установите его в своем проекте.</span><span class="sxs-lookup"><span data-stu-id="15488-121">If you plan toouse log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="15488-122">В обозревателе решений щелкните правой кнопкой мыши ваш проект и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="15488-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="15488-123">Поиск Application Insights</span><span class="sxs-lookup"><span data-stu-id="15488-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="15488-124">Выберите соответствующий пакет hello - один из:</span><span class="sxs-lookup"><span data-stu-id="15488-124">Select hello appropriate package - one of:</span></span>

   * <span data-ttu-id="15488-125">Microsoft.ApplicationInsights.TraceListener (вызовы методов System.Diagnostics.Trace toocapture)</span><span class="sxs-lookup"><span data-stu-id="15488-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="15488-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource события)</span><span class="sxs-lookup"><span data-stu-id="15488-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource events)</span></span>
   * <span data-ttu-id="15488-127">Microsoft.ApplicationInsights.EtwListener (toocapture события трассировки событий Windows)</span><span class="sxs-lookup"><span data-stu-id="15488-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW events)</span></span>
   * <span data-ttu-id="15488-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="15488-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="15488-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="15488-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="15488-130">пакет NuGet Hello устанавливает необходимые сборки hello, а также изменяет web.config или app.config.</span><span class="sxs-lookup"><span data-stu-id="15488-130">hello NuGet package installs hello necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="15488-131">Вставка вызовов журнала диагностики</span><span class="sxs-lookup"><span data-stu-id="15488-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="15488-132">При использовании System.Diagnostics.Trace типичный вызов будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="15488-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="15488-133">если вы предпочитаете log4net или NLog:</span><span class="sxs-lookup"><span data-stu-id="15488-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="15488-134">Использование событий EventSource</span><span class="sxs-lookup"><span data-stu-id="15488-134">Using EventSource events</span></span>
<span data-ttu-id="15488-135">Можно настроить [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) tooApplication toobe отправки событий аналитики как трассировок.</span><span class="sxs-lookup"><span data-stu-id="15488-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="15488-136">Сначала установите hello `Microsoft.ApplicationInsights.EventSourceListener` пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="15488-136">First, install hello `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="15488-137">Затем измените `TelemetryModules` раздел hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) файла.</span><span class="sxs-lookup"><span data-stu-id="15488-137">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="15488-138">Для каждого источника можно задать следующие параметры hello.</span><span class="sxs-lookup"><span data-stu-id="15488-138">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="15488-139">`Name`Указывает имя hello hello EventSource toocollect.</span><span class="sxs-lookup"><span data-stu-id="15488-139">`Name` specifies hello name of hello EventSource toocollect.</span></span>
 * <span data-ttu-id="15488-140">`Level`Указывает hello toocollect уровня ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="15488-140">`Level` specifies hello logging level toocollect.</span></span> <span data-ttu-id="15488-141">Возможные значения: `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="15488-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="15488-142">`Keywords`(Необязательно) задает целочисленное значение hello toouse сочетания ключевых слов.</span><span class="sxs-lookup"><span data-stu-id="15488-142">`Keywords` (Optional) specifies hello integer value of keywords combinations toouse.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="15488-143">Использование событий DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="15488-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="15488-144">Можно настроить [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) tooApplication toobe отправки событий аналитики как трассировок.</span><span class="sxs-lookup"><span data-stu-id="15488-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="15488-145">Сначала установите hello [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="15488-145">First, install hello [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="15488-146">Затем измените hello `TelemetryModules` раздел hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) файла.</span><span class="sxs-lookup"><span data-stu-id="15488-146">Then edit hello `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="15488-147">Для каждого DiagnosticSource требуется tootrace, добавьте запись с hello `Name` toohello имя вашей DiagnosticSource набора атрибутов.</span><span class="sxs-lookup"><span data-stu-id="15488-147">For each DiagnosticSource you want tootrace, add an entry with hello `Name` attribute  set toohello name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="15488-148">Использование событий трассировки событий Windows</span><span class="sxs-lookup"><span data-stu-id="15488-148">Using ETW events</span></span>
<span data-ttu-id="15488-149">Вы можете настроить отправлен tooApplication аналитики как трассировки toobe события трассировки событий Windows.</span><span class="sxs-lookup"><span data-stu-id="15488-149">You can configure ETW events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="15488-150">Сначала установите hello `Microsoft.ApplicationInsights.EtwCollector` пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="15488-150">First, install hello `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="15488-151">Затем измените `TelemetryModules` раздел hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) файла.</span><span class="sxs-lookup"><span data-stu-id="15488-151">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="15488-152">События трассировки событий Windows могут собираться только в том случае, если hello процесс размещения hello SDK выполняется под идентификатором, который является членом группы «Пользователи журналов производительности» или Администраторы.</span><span class="sxs-lookup"><span data-stu-id="15488-152">ETW events can only be collected if hello process hosting hello SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="15488-153">Для каждого источника можно задать следующие параметры hello.</span><span class="sxs-lookup"><span data-stu-id="15488-153">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="15488-154">`ProviderName`— Имя hello toocollect поставщика трассировки событий Windows hello.</span><span class="sxs-lookup"><span data-stu-id="15488-154">`ProviderName` is hello name of hello ETW provider toocollect.</span></span>
 * <span data-ttu-id="15488-155">`ProviderGuid`Указывает hello GUID toocollect поставщика трассировки событий Windows hello, можно использовать вместо `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="15488-155">`ProviderGuid` specifies hello GUID of hello ETW provider toocollect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="15488-156">`Level`Задает hello toocollect уровня ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="15488-156">`Level` sets hello logging level toocollect.</span></span> <span data-ttu-id="15488-157">Возможные значения: `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="15488-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="15488-158">`Keywords`(Необязательно) задает hello целочисленное значение toouse сочетания ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="15488-158">`Keywords` (Optional) sets hello integer value of keyword combinations toouse.</span></span>

## <a name="using-hello-trace-api-directly"></a><span data-ttu-id="15488-159">Непосредственное использование hello трассировки API</span><span class="sxs-lookup"><span data-stu-id="15488-159">Using hello Trace API directly</span></span>
<span data-ttu-id="15488-160">API трассировки Application Insights hello можно вызывать напрямую.</span><span class="sxs-lookup"><span data-stu-id="15488-160">You can call hello Application Insights trace API directly.</span></span> <span data-ttu-id="15488-161">Этот API использовать адаптеры ведения журналов Hello.</span><span class="sxs-lookup"><span data-stu-id="15488-161">hello logging adapters use this API.</span></span>

<span data-ttu-id="15488-162">Например:</span><span class="sxs-lookup"><span data-stu-id="15488-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="15488-163">Преимуществом TrackTrace является относительно большие объемы данных можно поместить в сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="15488-163">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="15488-164">например данных POST.</span><span class="sxs-lookup"><span data-stu-id="15488-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="15488-165">Кроме того можно добавить сообщение tooyour уровня серьезности.</span><span class="sxs-lookup"><span data-stu-id="15488-165">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="15488-166">И, как и другие данные телеметрии, можно добавить значения свойств, которые используются toohelp фильтрации или поиска для разных наборов трассировок.</span><span class="sxs-lookup"><span data-stu-id="15488-166">And, like other telemetry, you can add property values that you can use toohelp filter or search for different sets of traces.</span></span> <span data-ttu-id="15488-167">Например:</span><span class="sxs-lookup"><span data-stu-id="15488-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="15488-168">Это позволит вам, в [поиска][diagnostic], tooeasily отфильтровать все сообщения hello уровня серьезности конкретного связанные tooa определенной базы данных.</span><span class="sxs-lookup"><span data-stu-id="15488-168">This would enable you, in [Search][diagnostic], tooeasily filter out all hello messages of a particular severity level relating tooa particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="15488-169">Просмотр журналов</span><span class="sxs-lookup"><span data-stu-id="15488-169">Explore your logs</span></span>
<span data-ttu-id="15488-170">Запустите приложение в режиме отладки или разверните его.</span><span class="sxs-lookup"><span data-stu-id="15488-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="15488-171">В колонке Общие сведения о приложении в [hello портале Application Insights][portal], выберите [поиска][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="15488-171">In your app's overview blade in [hello Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![В Application Insights выберите элемент «Поиск»](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![поиска](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="15488-174">Можно, например:</span><span class="sxs-lookup"><span data-stu-id="15488-174">You can, for example:</span></span>

* <span data-ttu-id="15488-175">фильтровать трассировки журнала или элементы с определенными свойствами;</span><span class="sxs-lookup"><span data-stu-id="15488-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="15488-176">просматривать подробные сведения конкретного элемента;</span><span class="sxs-lookup"><span data-stu-id="15488-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="15488-177">Найти другие телеметрии связанные toohello того же запроса пользователя (то есть с hello таким же идентификатором операции)</span><span class="sxs-lookup"><span data-stu-id="15488-177">Find other telemetry relating toohello same user request (that is, with hello same OperationId)</span></span>
* <span data-ttu-id="15488-178">Сохранить конфигурацию hello этой страницы в список избранного</span><span class="sxs-lookup"><span data-stu-id="15488-178">Save hello configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="15488-179">**Выборка.**</span><span class="sxs-lookup"><span data-stu-id="15488-179">**Sampling.**</span></span> <span data-ttu-id="15488-180">Если приложение отправляет большой объем данных, и вы используете hello пакет SDK Application Insights для ASP.NET версии 2.0.0-beta3 или более поздней версии, функция адаптивной выборки hello может работать и отправьте доля телеметрии.</span><span class="sxs-lookup"><span data-stu-id="15488-180">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="15488-181">Дополнительная информация о выборке.</span><span class="sxs-lookup"><span data-stu-id="15488-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="15488-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="15488-182">Next steps</span></span>
<span data-ttu-id="15488-183">[Диагностика ошибок и исключений в ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="15488-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="15488-184">[Дополнительная информация о службе поиска][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="15488-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="15488-185">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="15488-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="15488-186">Как это сделать в Java?</span><span class="sxs-lookup"><span data-stu-id="15488-186">How do I do this for Java?</span></span>
<span data-ttu-id="15488-187">Используйте hello [адаптеров журнала Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="15488-187">Use hello [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a><span data-ttu-id="15488-188">В контекстном меню проекта hello, нет возможности Application Insights</span><span class="sxs-lookup"><span data-stu-id="15488-188">There's no Application Insights option on hello project context menu</span></span>
* <span data-ttu-id="15488-189">Проверьте, установлены ли на этом компьютере средства Application Insights.</span><span class="sxs-lookup"><span data-stu-id="15488-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="15488-190">В меню "Сервис, расширения и обновления" Visual Studio найдите "Средства Application Insights".</span><span class="sxs-lookup"><span data-stu-id="15488-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="15488-191">Если он отсутствует в вкладку "установлено" hello, откройте вкладку hello в интерактивном режиме и установите его.</span><span class="sxs-lookup"><span data-stu-id="15488-191">If it isn't in hello Installed tab, open hello Online tab and install it.</span></span>
* <span data-ttu-id="15488-192">Возможно, этот тип проекта не поддерживается средствами Application Insights.</span><span class="sxs-lookup"><span data-stu-id="15488-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="15488-193">Используйте [установку вручную](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="15488-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a><span data-ttu-id="15488-194">Параметр адаптера не журнала в средстве настройки hello</span><span class="sxs-lookup"><span data-stu-id="15488-194">No log adapter option in hello configuration tool</span></span>
* <span data-ttu-id="15488-195">Вы должны платформы ведения журналов tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="15488-195">You need tooinstall hello logging framework first.</span></span>
* <span data-ttu-id="15488-196">Если вы используете System.Diagnostics.Trace, убедитесь, что это средство [настроено в `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="15488-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="15488-197">У вас есть hello последнюю версию Application Insights</span><span class="sxs-lookup"><span data-stu-id="15488-197">Have you got hello latest version of Application Insights?</span></span> <span data-ttu-id="15488-198">В Visual Studio **средства** меню, выберите **расширения и обновления**и откройте hello **обновления** вкладки. Если есть средства аналитические средства разработчика, щелкните tooupdate его.</span><span class="sxs-lookup"><span data-stu-id="15488-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open hello **Updates** tab. If Developer Analytics tools is there, click tooupdate it.</span></span>

### <span data-ttu-id="15488-199"><a name="emptykey"></a>Появляется сообщение об ошибке «ключ инструментирования не может быть пустым»</span><span class="sxs-lookup"><span data-stu-id="15488-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="15488-200">Похоже, вы установили hello, ведение журнала пакета Nuget адаптера без установки Application Insights.</span><span class="sxs-lookup"><span data-stu-id="15488-200">Looks like you installed hello logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="15488-201">В обозревателе решений щелкните правой кнопкой мыши `ApplicationInsights.config` и выберите **Обновить Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="15488-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="15488-202">Появится диалоговое окно, которое предлагает toosign в tooAzure и либо создать ресурс Application Insights или повторно использовать уже существующий.</span><span class="sxs-lookup"><span data-stu-id="15488-202">You'll get a dialog that invites you toosign in tooAzure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="15488-203">Это должно исправить проблему.</span><span class="sxs-lookup"><span data-stu-id="15488-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a><span data-ttu-id="15488-204">Я отображаются трассировки диагностики поиска, но не hello других событий</span><span class="sxs-lookup"><span data-stu-id="15488-204">I can see traces in diagnostic search, but not hello other events</span></span>
<span data-ttu-id="15488-205">Иногда может потребоваться время для всех hello события и запросы tooget через конвейер hello.</span><span class="sxs-lookup"><span data-stu-id="15488-205">It can sometimes take a while for all hello events and requests tooget through hello pipeline.</span></span>

### <span data-ttu-id="15488-206"><a name="limits"></a>Какой объем данных сохраняется?</span><span class="sxs-lookup"><span data-stu-id="15488-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="15488-207">Несколько факторов влияют на объем данных, хранящихся в hello.</span><span class="sxs-lookup"><span data-stu-id="15488-207">Several factors impact hello amount of data retained.</span></span> <span data-ttu-id="15488-208">В разделе hello [ограничения](app-insights-api-custom-events-metrics.md#limits) раздел страницы метрики hello клиента событий для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="15488-208">See hello [limits](app-insights-api-custom-events-metrics.md#limits) section of hello customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a><span data-ttu-id="15488-209">Я не вижу некоторые из записей журнала hello ожидаемых</span><span class="sxs-lookup"><span data-stu-id="15488-209">I'm not seeing some of hello log entries that I expect</span></span>
<span data-ttu-id="15488-210">Если приложение отправляет большой объем данных, и вы используете hello пакет SDK Application Insights для ASP.NET версии 2.0.0-beta3 или более поздней версии, функция адаптивной выборки hello может работать и отправьте доля телеметрии.</span><span class="sxs-lookup"><span data-stu-id="15488-210">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="15488-211">Дополнительная информация о выборке.</span><span class="sxs-lookup"><span data-stu-id="15488-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="15488-212"><a name="add"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="15488-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="15488-213">[Наблюдение за доступностью и скоростью реагирования веб-сайта][availability]</span><span class="sxs-lookup"><span data-stu-id="15488-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="15488-214">[Устранение неполадок][qna]</span><span class="sxs-lookup"><span data-stu-id="15488-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
