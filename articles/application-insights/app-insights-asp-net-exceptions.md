---
title: "aaaDiagnose сбои и исключения в веб-приложений с помощью Azure Application Insights | Документы Microsoft"
description: "Регистрируйте исключения приложений ASP.NET и телеметрию запросов."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="1805c-103">Диагностика исключений в веб-приложениях с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="1805c-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="1805c-104">Об исключениях активного веб-приложения сообщает [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1805c-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="1805c-105">Вы можете соотнести неудачных запросов с исключениями и других событий на сервер и клиент hello, чтобы быстро найти причину причины hello.</span><span class="sxs-lookup"><span data-stu-id="1805c-105">You can correlate failed requests with exceptions and other events at both hello client and server, so that you can quickly diagnose hello causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="1805c-106">Настройка создания отчетов об исключениях</span><span class="sxs-lookup"><span data-stu-id="1805c-106">Set up exception reporting</span></span>
* <span data-ttu-id="1805c-107">исключения toohave, полученные от сервера приложения.</span><span class="sxs-lookup"><span data-stu-id="1805c-107">toohave exceptions reported from your server app:</span></span>
  * <span data-ttu-id="1805c-108">Запрограммируйте установку [пакета SDK для Application Insights](app-insights-asp-net.md) в приложении или:</span><span class="sxs-lookup"><span data-stu-id="1805c-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="1805c-109">веб-серверы IIS: запустите [агент Application Insights](app-insights-monitor-performance-live-website-now.md) либо</span><span class="sxs-lookup"><span data-stu-id="1805c-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="1805c-110">Веб-приложениях Azure: добавить hello [расширение Application Insights](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="1805c-110">Azure web apps: Add hello [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="1805c-111">Веб-приложений Java: hello установки [агента Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="1805c-111">Java web apps: Install hello [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="1805c-112">Установка hello [фрагмент JavaScript](app-insights-javascript.md) в свои исключения браузера toocatch веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="1805c-112">Install hello [JavaScript snippet](app-insights-javascript.md) in your web pages toocatch browser exceptions.</span></span>
* <span data-ttu-id="1805c-113">Некоторые платформы приложений или некоторые параметры, необходимые tootake toocatch некоторые дополнительные шаги дополнительные исключения:</span><span class="sxs-lookup"><span data-stu-id="1805c-113">In some application frameworks or with some settings, you need tootake some extra steps toocatch more exceptions:</span></span>
  * <span data-ttu-id="1805c-114">[веб-формы](#web-forms);</span><span class="sxs-lookup"><span data-stu-id="1805c-114">[Web forms](#web-forms)</span></span>
  * <span data-ttu-id="1805c-115">[MVC](#mvc);</span><span class="sxs-lookup"><span data-stu-id="1805c-115">[MVC](#mvc)</span></span>
  * <span data-ttu-id="1805c-116">[веб-API 1.*](#web-api-1);</span><span class="sxs-lookup"><span data-stu-id="1805c-116">[Web API 1.*](#web-api-1)</span></span>
  * <span data-ttu-id="1805c-117">[веб-API 2.*](#web-api-2);</span><span class="sxs-lookup"><span data-stu-id="1805c-117">[Web API 2.*](#web-api-2)</span></span>
  * [<span data-ttu-id="1805c-118">WCF</span><span class="sxs-lookup"><span data-stu-id="1805c-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="1805c-119">Диагностика исключений с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1805c-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="1805c-120">Откройте решение для приложения hello в Visual Studio toohelp в процессе отладки.</span><span class="sxs-lookup"><span data-stu-id="1805c-120">Open hello app solution in Visual Studio toohelp with debugging.</span></span>

<span data-ttu-id="1805c-121">Запустите приложение hello на сервере или на компьютере разработки, нажав клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="1805c-121">Run hello app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="1805c-122">Откройте окно hello поиска Application Insights в Visual Studio и задать для него toodisplay события из приложения.</span><span class="sxs-lookup"><span data-stu-id="1805c-122">Open hello Application Insights Search window in Visual Studio, and set it toodisplay events from your app.</span></span> <span data-ttu-id="1805c-123">Во время отладки, это можно сделать, просто нажав кнопку hello Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1805c-123">While you're debugging, you can do this just by clicking hello Application Insights button.</span></span>

![Щелкните правой кнопкой мыши проект hello и Application Insights, нажмите кнопку Открыть.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="1805c-125">Обратите внимание, что hello отчетов tooshow просто исключения можно фильтровать.</span><span class="sxs-lookup"><span data-stu-id="1805c-125">Notice that you can filter hello report tooshow just exceptions.</span></span>

<span data-ttu-id="1805c-126">*Исключения не отображаются? См. раздел [Запись исключений](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="1805c-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="1805c-127">Щелкните отчет исключение tooshow трассировку стека.</span><span class="sxs-lookup"><span data-stu-id="1805c-127">Click an exception report tooshow its stack trace.</span></span>
<span data-ttu-id="1805c-128">Щелкните Справочник по строке в трассировке стека hello, соответствующий код файла tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="1805c-128">Click a line reference in hello stack trace, tooopen hello relevant code file.</span></span>  

<span data-ttu-id="1805c-129">В коде hello Обратите внимание, что CodeLens показывает данные об исключениях hello:</span><span class="sxs-lookup"><span data-stu-id="1805c-129">In hello code, notice that CodeLens shows data about hello exceptions:</span></span>

![Уведомление об исключениях CodeLens](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a><span data-ttu-id="1805c-131">Диагностика ошибок с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="1805c-131">Diagnosing failures using hello Azure portal</span></span>
<span data-ttu-id="1805c-132">Из Application Insights hello Общие сведения о приложении Плитка сбоев hello отображает диаграммы для исключения и невыполненных запросов HTTP, вместе со списком hello запроса URL-адреса, которые наиболее частые ошибки hello.</span><span class="sxs-lookup"><span data-stu-id="1805c-132">From hello Application Insights overview of your app, hello Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of hello request URLs that cause hello most frequent failures.</span></span>

![Последовательно выберите элементы "Параметры" и "Сбои".](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="1805c-134">Щелкните по одной из hello сбой типов исключений в tooget tooindividual hello список вхождений hello исключения, где можно подробно рассмотреть hello и трассировка стека:</span><span class="sxs-lookup"><span data-stu-id="1805c-134">Click through one of hello failed exception types in hello list tooget tooindividual occurrences of hello exception, where you can see hello details and stack trace:</span></span>

![Выберите экземпляр невыполненных запросов, а также в разделе сведения об исключении, получить tooinstances hello исключения.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="1805c-136">**Кроме того** можно запустить из списка hello запросов и найти связанные tooit исключения.</span><span class="sxs-lookup"><span data-stu-id="1805c-136">**Alternatively,** you can start from hello list of requests and find exceptions related tooit.</span></span>

<span data-ttu-id="1805c-137">*Исключения не отображаются? См. раздел [Запись исключений](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="1805c-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="1805c-138">Пользовательская трассировка и данные журналов</span><span class="sxs-lookup"><span data-stu-id="1805c-138">Custom tracing and log data</span></span>
<span data-ttu-id="1805c-139">приложение конкретных tooyour tooget диагностических данных, можно вставить код toosend данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="1805c-139">tooget diagnostic data specific tooyour app, you can insert code toosend your own telemetry data.</span></span> <span data-ttu-id="1805c-140">Это отображаются при поиске диагностики наряду с hello запрос представления страницы и другие данные, автоматически сохраняются.</span><span class="sxs-lookup"><span data-stu-id="1805c-140">This displayed in diagnostic search alongside hello request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="1805c-141">Доступно несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="1805c-141">You have several options:</span></span>

* <span data-ttu-id="1805c-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) обычно используется для наблюдения за шаблонов использования, но также отправляет данных отображается под пользовательские события диагностики поиска hello.</span><span class="sxs-lookup"><span data-stu-id="1805c-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but hello data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="1805c-143">У событий есть имена и они могут содержать строковые свойства и числовые метрики, по которым можно [фильтровать результаты поиска диагностических данных](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="1805c-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="1805c-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) позволяет отправлять более длинные данные, например данные POST.</span><span class="sxs-lookup"><span data-stu-id="1805c-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="1805c-145">[TrackException()](#exceptions) отправляет трассировки стеков.</span><span class="sxs-lookup"><span data-stu-id="1805c-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="1805c-146">[Дополнительные сведения об исключениях](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="1805c-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="1805c-147">Если вы уже используете какую-либо платформу ведения журналов, например Log4Net или NLog, [эти журналы можно записывать](app-insights-asp-net-trace-logs.md) и включать в результаты поиска диагностических данных вместе с данными запросов и исключений.</span><span class="sxs-lookup"><span data-stu-id="1805c-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="1805c-148">Откройте эти события toosee [поиска](app-insights-diagnostic-search.md)откройте фильтра и нажмите кнопку Custom Event, трассировку или исключения.</span><span class="sxs-lookup"><span data-stu-id="1805c-148">toosee these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Детализация](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="1805c-150">Если приложение создает большой объем данных телеметрии, модуль адаптивной выборки hello автоматически уменьшит hello тома, отправляемое toohello портала, отправляя репрезентативной часть событий.</span><span class="sxs-lookup"><span data-stu-id="1805c-150">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="1805c-151">События, которые являются частью hello одной операции будет иметь или отмену выбора как группу, так что можно перемещаться между связанными событиями.</span><span class="sxs-lookup"><span data-stu-id="1805c-151">Events that are part of hello same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="1805c-152">Дополнительная информация о выборке.</span><span class="sxs-lookup"><span data-stu-id="1805c-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a><span data-ttu-id="1805c-153">Способ toosee запроса данные POST</span><span class="sxs-lookup"><span data-stu-id="1805c-153">How toosee request POST data</span></span>
<span data-ttu-id="1805c-154">Сведения о запросе не включайте hello данные, отправляемые tooyour приложения в вызове процедуры POST.</span><span class="sxs-lookup"><span data-stu-id="1805c-154">Request details don't include hello data sent tooyour app in a POST call.</span></span> <span data-ttu-id="1805c-155">toohave эти данные, определенные как:</span><span class="sxs-lookup"><span data-stu-id="1805c-155">toohave this data reported:</span></span>

* <span data-ttu-id="1805c-156">[Установка пакета SDK для hello](app-insights-asp-net.md) в проекте приложения.</span><span class="sxs-lookup"><span data-stu-id="1805c-156">[Install hello SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="1805c-157">Вставьте код в вашего приложения toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="1805c-157">Insert code in your application toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="1805c-158">Отправьте данные POST hello в параметре сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="1805c-158">Send hello POST data in hello message parameter.</span></span> <span data-ttu-id="1805c-159">Нет toohello допускается ограничение на размер, поэтому попробуйте toosend hello только необходимые данные.</span><span class="sxs-lookup"><span data-stu-id="1805c-159">There is a limit toohello permitted size, so you should try toosend just hello essential data.</span></span>
* <span data-ttu-id="1805c-160">При исследовании невыполненных запросов, найти связанные hello трассировок.</span><span class="sxs-lookup"><span data-stu-id="1805c-160">When you investigate a failed request, find hello associated traces.</span></span>  

![Детализация](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="1805c-162"><a name="exceptions"></a> Запись исключений и связанных диагностических данных</span><span class="sxs-lookup"><span data-stu-id="1805c-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="1805c-163">Сначала вы не увидите hello портале все исключения hello, привести к сбою приложения.</span><span class="sxs-lookup"><span data-stu-id="1805c-163">At first, you won't see in hello portal all hello exceptions that cause failures in your app.</span></span> <span data-ttu-id="1805c-164">Вы увидите все исключения браузера (Если вы используете hello [JavaScript SDK](app-insights-javascript.md) на веб-страницах).</span><span class="sxs-lookup"><span data-stu-id="1805c-164">You'll see any browser exceptions (if you're using hello [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="1805c-165">Но большинство server исключения перехватываются службами IIS и у вас есть немного кода toosee toowrite их.</span><span class="sxs-lookup"><span data-stu-id="1805c-165">But most server exceptions are caught by IIS and you have toowrite a bit of code toosee them.</span></span>

<span data-ttu-id="1805c-166">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="1805c-166">You can:</span></span>

* <span data-ttu-id="1805c-167">**Явно журнала исключений** путем вставки кода в tooreport hello исключение обработчиков исключений.</span><span class="sxs-lookup"><span data-stu-id="1805c-167">**Log exceptions explicitly** by inserting code in exception handlers tooreport hello exceptions.</span></span>
* <span data-ttu-id="1805c-168">**Автоматически записывать исключения** путем настройки своей платформы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1805c-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="1805c-169">Hello необходимых дополнений отличаются для разных типов framework.</span><span class="sxs-lookup"><span data-stu-id="1805c-169">hello necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="1805c-170">Явная регистрация исключений</span><span class="sxs-lookup"><span data-stu-id="1805c-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="1805c-171">Hello простым способом является tooinsert tooTrackException() вызов в обработчике исключений.</span><span class="sxs-lookup"><span data-stu-id="1805c-171">hello simplest way is tooinsert a call tooTrackException() in an exception handler.</span></span>

<span data-ttu-id="1805c-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1805c-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="1805c-173">C#</span><span class="sxs-lookup"><span data-stu-id="1805c-173">C#</span></span>

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="1805c-174">VB</span><span class="sxs-lookup"><span data-stu-id="1805c-174">VB</span></span>

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="1805c-175">Hello свойства и значения параметров не являются обязательными, но они полезны для [фильтрацию и добавление](app-insights-diagnostic-search.md) дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="1805c-175">hello properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="1805c-176">Например если у вас есть приложение, которое можно запустить несколько игр, можно найти все hello исключение отчеты связанные tooa конкретной игры.</span><span class="sxs-lookup"><span data-stu-id="1805c-176">For example, if you have an app that can run several games, you could find all hello exception reports related tooa particular game.</span></span> <span data-ttu-id="1805c-177">Можно добавить столько элементов, так как tooeach словарь.</span><span class="sxs-lookup"><span data-stu-id="1805c-177">You can add as many items as you like tooeach dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="1805c-178">Исключения браузера</span><span class="sxs-lookup"><span data-stu-id="1805c-178">Browser exceptions</span></span>
<span data-ttu-id="1805c-179">Большинство исключений браузера регистрируются.</span><span class="sxs-lookup"><span data-stu-id="1805c-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="1805c-180">Если веб-страница содержит файлы скриптов из сети доставки содержимого или других доменов, убедитесь в скрипт содержит атрибут hello ```crossorigin="anonymous"```, и отправляет этот сервер hello [заголовки CORS](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="1805c-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has hello attribute ```crossorigin="anonymous"```,  and that hello server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="1805c-181">Это позволит вам tooget трассировку стека и сведения для необработанных исключений JavaScript из этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1805c-181">This will allow you tooget a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="1805c-182">Веб-формы</span><span class="sxs-lookup"><span data-stu-id="1805c-182">Web forms</span></span>
<span data-ttu-id="1805c-183">Для веб-формы hello HTTP-модуль будет может toocollect hello исключений при переадресации, не настроены CustomErrors.</span><span class="sxs-lookup"><span data-stu-id="1805c-183">For web forms, hello HTTP Module will be able toocollect hello exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="1805c-184">Но при наличии активных переадресации, добавить следующие функции Application_Error строки toohello в Global.asax.cs hello.</span><span class="sxs-lookup"><span data-stu-id="1805c-184">But if you have active redirects, add hello following lines toohello Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="1805c-185">(Добавьте файл Global.asax, если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="1805c-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="1805c-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="1805c-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="1805c-187">MVC</span><span class="sxs-lookup"><span data-stu-id="1805c-187">MVC</span></span>
<span data-ttu-id="1805c-188">Если hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) конфигурация `Off`, то исключения будут доступны для hello [HTTP-модуля](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span><span class="sxs-lookup"><span data-stu-id="1805c-188">If hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for hello [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span></span> <span data-ttu-id="1805c-189">Тем не менее если это `RemoteOnly` (по умолчанию), или `On`, hello исключение будет очищено и недоступно для Application Insights tooautomatically сбора.</span><span class="sxs-lookup"><span data-stu-id="1805c-189">However, if it is `RemoteOnly` (default), or `On`, then hello exception will be cleared and not available for Application Insights tooautomatically collect.</span></span> <span data-ttu-id="1805c-190">Можно исправить, путем переопределения hello [класса System.Web.Mvc.HandleErrorAttribute](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)и применение hello переопределении класса, как показано для hello разные MVC версии ниже ([github источника](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="1805c-190">You can fix that by overriding hello [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying hello overridden class as shown for hello different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a><span data-ttu-id="1805c-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="1805c-191">MVC 2</span></span>
<span data-ttu-id="1805c-192">Замените на новый атрибут в контроллерах атрибут HandleError hello.</span><span class="sxs-lookup"><span data-stu-id="1805c-192">Replace hello HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="1805c-193">Пример</span><span class="sxs-lookup"><span data-stu-id="1805c-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="1805c-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="1805c-194">MVC 3</span></span>
<span data-ttu-id="1805c-195">Зарегистрируйте `AiHandleErrorAttribute` в качестве глобального фильтра в Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="1805c-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="1805c-196">Пример</span><span class="sxs-lookup"><span data-stu-id="1805c-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="1805c-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="1805c-197">MVC 4, MVC5</span></span>
<span data-ttu-id="1805c-198">Зарегистрируйте AiHandleErrorAttribute в качестве глобального фильтра в FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="1805c-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="1805c-199">Пример</span><span class="sxs-lookup"><span data-stu-id="1805c-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="1805c-200">Web API 1.x</span><span class="sxs-lookup"><span data-stu-id="1805c-200">Web API 1.x</span></span>
<span data-ttu-id="1805c-201">Переопределите System.Web.Http.Filters.ExceptionFilterAttribute:</span><span class="sxs-lookup"><span data-stu-id="1805c-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

<span data-ttu-id="1805c-202">Можно добавить этот атрибут переопределенный toospecific контроллеры, или добавить глобальный фильтр конфигурации toohello класса WebApiConfig hello:</span><span class="sxs-lookup"><span data-stu-id="1805c-202">You could add this overridden attribute toospecific controllers, or add it toohello global filter configuration in hello WebApiConfig class:</span></span>

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[<span data-ttu-id="1805c-203">Пример</span><span class="sxs-lookup"><span data-stu-id="1805c-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="1805c-204">Существует несколько вариантов, не может обрабатывать hello фильтры исключений.</span><span class="sxs-lookup"><span data-stu-id="1805c-204">There are a number of cases that hello exception filters cannot handle.</span></span> <span data-ttu-id="1805c-205">Например:</span><span class="sxs-lookup"><span data-stu-id="1805c-205">For example:</span></span>

* <span data-ttu-id="1805c-206">Исключения выброшены из конструкторов контроллеров.</span><span class="sxs-lookup"><span data-stu-id="1805c-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="1805c-207">Исключения выброшены из обработчиков сообщений.</span><span class="sxs-lookup"><span data-stu-id="1805c-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="1805c-208">Исключения выброшены при маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="1805c-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="1805c-209">Исключения выброшены при сериализации содержимого ответа.</span><span class="sxs-lookup"><span data-stu-id="1805c-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="1805c-210">Web API 2.x</span><span class="sxs-lookup"><span data-stu-id="1805c-210">Web API 2.x</span></span>
<span data-ttu-id="1805c-211">Добавьте реализацию IExceptionLogger:</span><span class="sxs-lookup"><span data-stu-id="1805c-211">Add an implementation of IExceptionLogger:</span></span>

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

<span data-ttu-id="1805c-212">При добавлении этой службы toohello WebApiConfig.</span><span class="sxs-lookup"><span data-stu-id="1805c-212">Add this toohello services in WebApiConfig:</span></span>

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  <span data-ttu-id="1805c-213">}</span><span class="sxs-lookup"><span data-stu-id="1805c-213">}</span></span>

[<span data-ttu-id="1805c-214">Пример</span><span class="sxs-lookup"><span data-stu-id="1805c-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="1805c-215">В качестве альтернативы можно выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="1805c-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="1805c-216">Замените hello только ExceptionHandler на собственную реализацию IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="1805c-216">Replace hello only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="1805c-217">Это только вызывается, когда инфраструктура hello это все еще может toochoose какой ответ сообщений toosend (не при прерывании hello соединения для экземпляра)</span><span class="sxs-lookup"><span data-stu-id="1805c-217">This is only called when hello framework is still able toochoose which response message toosend (not when hello connection is aborted for instance)</span></span>
2. <span data-ttu-id="1805c-218">Не вызывается во всех случаях фильтры исключений (как описано в разделе hello контроллерах веб-API 1.x выше).</span><span class="sxs-lookup"><span data-stu-id="1805c-218">Exception Filters (as described in hello section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="1805c-219">WCF</span><span class="sxs-lookup"><span data-stu-id="1805c-219">WCF</span></span>
<span data-ttu-id="1805c-220">Добавьте класс, который расширяет Attribute и реализует IErrorHandler и IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="1805c-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

<span data-ttu-id="1805c-221">Добавьте hello атрибут toohello службы реализации:</span><span class="sxs-lookup"><span data-stu-id="1805c-221">Add hello attribute toohello service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="1805c-222">Пример</span><span class="sxs-lookup"><span data-stu-id="1805c-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="1805c-223">Счетчики производительности исключений</span><span class="sxs-lookup"><span data-stu-id="1805c-223">Exception performance counters</span></span>
<span data-ttu-id="1805c-224">Если у вас есть [установлен агент аналитики приложений hello](app-insights-monitor-performance-live-website-now.md) на сервере, вы можете получить диаграмму скорости исключения hello, измеренное .NET.</span><span class="sxs-lookup"><span data-stu-id="1805c-224">If you have [installed hello Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of hello exceptions rate, measured by .NET.</span></span> <span data-ttu-id="1805c-225">Она включает как обработанные, так и необработанные исключения .NET.</span><span class="sxs-lookup"><span data-stu-id="1805c-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="1805c-226">Откройте колонку обозревателя метрик, добавьте новую диаграмму и выберите счетчик **Частота исключений**в списке "Счетчики производительности".</span><span class="sxs-lookup"><span data-stu-id="1805c-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="1805c-227">Hello .NET framework вычисляет скорость hello путем подсчета hello число исключений в интервал hello продолжительность интервала hello.</span><span class="sxs-lookup"><span data-stu-id="1805c-227">hello .NET framework calculates hello rate by counting hello number of exceptions in an interval and dividing by hello length of hello interval.</span></span>

<span data-ttu-id="1805c-228">Обратите внимание, что он будет отличаться от вычислены порталом Application Insights hello TrackException отчеты по инвентаризации число исключений «hello».</span><span class="sxs-lookup"><span data-stu-id="1805c-228">Note that it will be different from hello 'Exceptions' count calculated by hello Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="1805c-229">интервалов выборки Hello различаются, а hello SDK не отправляет отчеты TrackException для обработанные и необработанные исключения.</span><span class="sxs-lookup"><span data-stu-id="1805c-229">hello sampling intervals are different, and hello SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="1805c-230">Видео</span><span class="sxs-lookup"><span data-stu-id="1805c-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="1805c-231">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1805c-231">Next steps</span></span>
* [<span data-ttu-id="1805c-232">Мониторинг REST, SQL и другие вызовы toodependencies</span><span class="sxs-lookup"><span data-stu-id="1805c-232">Monitor REST, SQL and other calls toodependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="1805c-233">Мониторинг времени загрузки страниц, исключений браузера и вызовов AJAX</span><span class="sxs-lookup"><span data-stu-id="1805c-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="1805c-234">Мониторинг счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="1805c-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
