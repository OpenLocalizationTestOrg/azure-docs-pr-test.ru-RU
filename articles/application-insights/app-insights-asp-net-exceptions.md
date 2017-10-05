---
title: "Диагностика ошибок и исключений в веб-приложениях с помощью Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: 7eeacdc6677ccdebb1653e94a163ecb47090b7ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="c34c2-103">Диагностика исключений в веб-приложениях с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="c34c2-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="c34c2-104">Об исключениях активного веб-приложения сообщает [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c34c2-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="c34c2-105">Вы можете сопоставлять неудачно завершенные запросы с исключениями и другими событиями на клиенте и сервере, чтобы быстро выявлять причины неполадок.</span><span class="sxs-lookup"><span data-stu-id="c34c2-105">You can correlate failed requests with exceptions and other events at both the client and server, so that you can quickly diagnose the causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="c34c2-106">Настройка создания отчетов об исключениях</span><span class="sxs-lookup"><span data-stu-id="c34c2-106">Set up exception reporting</span></span>
* <span data-ttu-id="c34c2-107">Вот как можно настроить создание отчетов об исключениях серверного приложения.</span><span class="sxs-lookup"><span data-stu-id="c34c2-107">To have exceptions reported from your server app:</span></span>
  * <span data-ttu-id="c34c2-108">Запрограммируйте установку [пакета SDK для Application Insights](app-insights-asp-net.md) в приложении или:</span><span class="sxs-lookup"><span data-stu-id="c34c2-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="c34c2-109">веб-серверы IIS: запустите [агент Application Insights](app-insights-monitor-performance-live-website-now.md) либо</span><span class="sxs-lookup"><span data-stu-id="c34c2-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="c34c2-110">веб-приложения Azure: добавьте [расширение Application Insights](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c34c2-110">Azure web apps: Add the [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="c34c2-111">Веб-приложения Java: установите [агент Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="c34c2-111">Java web apps: Install the [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="c34c2-112">Добавьте [фрагмент кода JavaScript](app-insights-javascript.md) в веб-страницы для перехвата исключений браузера.</span><span class="sxs-lookup"><span data-stu-id="c34c2-112">Install the [JavaScript snippet](app-insights-javascript.md) in your web pages to catch browser exceptions.</span></span>
* <span data-ttu-id="c34c2-113">Для некоторых платформ приложений или заданных параметров необходимо выполнить дополнительные шаги, чтобы перехватывать дополнительные исключения:</span><span class="sxs-lookup"><span data-stu-id="c34c2-113">In some application frameworks or with some settings, you need to take some extra steps to catch more exceptions:</span></span>
  * <span data-ttu-id="c34c2-114">[веб-формы](#web-forms);</span><span class="sxs-lookup"><span data-stu-id="c34c2-114">[Web forms](#web-forms)</span></span>
  * <span data-ttu-id="c34c2-115">[MVC](#mvc);</span><span class="sxs-lookup"><span data-stu-id="c34c2-115">[MVC](#mvc)</span></span>
  * <span data-ttu-id="c34c2-116">[веб-API 1.*](#web-api-1);</span><span class="sxs-lookup"><span data-stu-id="c34c2-116">[Web API 1.*](#web-api-1)</span></span>
  * <span data-ttu-id="c34c2-117">[веб-API 2.*](#web-api-2);</span><span class="sxs-lookup"><span data-stu-id="c34c2-117">[Web API 2.*](#web-api-2)</span></span>
  * [<span data-ttu-id="c34c2-118">WCF</span><span class="sxs-lookup"><span data-stu-id="c34c2-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="c34c2-119">Диагностика исключений с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c34c2-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="c34c2-120">Откройте приложение в Visual Studio для отладки.</span><span class="sxs-lookup"><span data-stu-id="c34c2-120">Open the app solution in Visual Studio to help with debugging.</span></span>

<span data-ttu-id="c34c2-121">Запустите приложение на сервере или на компьютере разработки, нажав клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="c34c2-121">Run the app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="c34c2-122">Откройте окно поиска Application Insights в Visual Studio и настройте его для отображения событий из приложения.</span><span class="sxs-lookup"><span data-stu-id="c34c2-122">Open the Application Insights Search window in Visual Studio, and set it to display events from your app.</span></span> <span data-ttu-id="c34c2-123">Во время отладки это можно сделать, просто нажав кнопку Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c34c2-123">While you're debugging, you can do this just by clicking the Application Insights button.</span></span>

![Щелкните правой кнопкой мыши проект и последовательно выберите пункты "Application Insights" и "Открыть".](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="c34c2-125">Обратите внимание: отчет можно отфильтровать так, чтобы отображались только исключения.</span><span class="sxs-lookup"><span data-stu-id="c34c2-125">Notice that you can filter the report to show just exceptions.</span></span>

<span data-ttu-id="c34c2-126">*Исключения не отображаются? См. раздел [Запись исключений](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="c34c2-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="c34c2-127">Щелкните отчет об исключении, чтобы отобразить для него трассировку стека.</span><span class="sxs-lookup"><span data-stu-id="c34c2-127">Click an exception report to show its stack trace.</span></span>
<span data-ttu-id="c34c2-128">Щелкните ссылку на строку в трассировке стека, чтобы открыть соответствующий файл кода.</span><span class="sxs-lookup"><span data-stu-id="c34c2-128">Click a line reference in the stack trace, to open the relevant code file.</span></span>  

<span data-ttu-id="c34c2-129">В коде обратите внимание, что CodeLens показывает данные об исключениях.</span><span class="sxs-lookup"><span data-stu-id="c34c2-129">In the code, notice that CodeLens shows data about the exceptions:</span></span>

![Уведомление об исключениях CodeLens](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-the-azure-portal"></a><span data-ttu-id="c34c2-131">Диагностика сбоев с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="c34c2-131">Diagnosing failures using the Azure portal</span></span>
<span data-ttu-id="c34c2-132">В обзоре Application Insights в приложении на плитке "Сбои" показаны диаграммы исключений, ошибок HTTP-запросов и список URL-адресов запросов, наиболее часто вызывающих сбои.</span><span class="sxs-lookup"><span data-stu-id="c34c2-132">From the Application Insights overview of your app, the Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of the request URLs that cause the most frequent failures.</span></span>

![Последовательно выберите элементы "Параметры" и "Сбои".](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="c34c2-134">Щелкните один из типов исключений в списке, чтобы отобразить отдельные случаи исключения и просмотреть подробные сведения и трассировку стека.</span><span class="sxs-lookup"><span data-stu-id="c34c2-134">Click through one of the failed exception types in the list to get to individual occurrences of the exception, where you can see the details and stack trace:</span></span>

![Выберите экземпляр неудачно завершенного запроса и в разделе сведений об исключении перейдите к нужному экземпляру исключения.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="c34c2-136">**Кроме того**, можно начать со списка запросов и найти исключения, связанные с ними.</span><span class="sxs-lookup"><span data-stu-id="c34c2-136">**Alternatively,** you can start from the list of requests and find exceptions related to it.</span></span>

<span data-ttu-id="c34c2-137">*Исключения не отображаются? См. раздел [Запись исключений](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="c34c2-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="c34c2-138">Пользовательская трассировка и данные журналов</span><span class="sxs-lookup"><span data-stu-id="c34c2-138">Custom tracing and log data</span></span>
<span data-ttu-id="c34c2-139">Для получения диагностических данных своего приложения вставьте код для отправки собственных данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="c34c2-139">To get diagnostic data specific to your app, you can insert code to send your own telemetry data.</span></span> <span data-ttu-id="c34c2-140">Они отображаются в результатах диагностического поиска вместе с запросом, просмотром страницы и другими данными, которые собираются автоматически.</span><span class="sxs-lookup"><span data-stu-id="c34c2-140">This displayed in diagnostic search alongside the request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="c34c2-141">Доступно несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="c34c2-141">You have several options:</span></span>

* <span data-ttu-id="c34c2-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) обычно используется для мониторинга шаблонов использования, но отправляемые с его помощью данные также отображаются в разделе пользовательских событий диагностического поиска.</span><span class="sxs-lookup"><span data-stu-id="c34c2-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but the data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="c34c2-143">У событий есть имена и они могут содержать строковые свойства и числовые метрики, по которым можно [фильтровать результаты поиска диагностических данных](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="c34c2-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="c34c2-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) позволяет отправлять более длинные данные, например данные POST.</span><span class="sxs-lookup"><span data-stu-id="c34c2-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="c34c2-145">[TrackException()](#exceptions) отправляет трассировки стеков.</span><span class="sxs-lookup"><span data-stu-id="c34c2-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="c34c2-146">[Дополнительные сведения об исключениях](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="c34c2-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="c34c2-147">Если вы уже используете какую-либо платформу ведения журналов, например Log4Net или NLog, [эти журналы можно записывать](app-insights-asp-net-trace-logs.md) и включать в результаты поиска диагностических данных вместе с данными запросов и исключений.</span><span class="sxs-lookup"><span data-stu-id="c34c2-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="c34c2-148">Чтобы просмотреть эти события, откройте область [Поиск](app-insights-diagnostic-search.md), щелкните "Фильтр", а затем выберите пользовательское событие, трассировку и исключение.</span><span class="sxs-lookup"><span data-stu-id="c34c2-148">To see these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Детализация](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="c34c2-150">Если приложение генерирует много телеметрических данных, модуль адаптивной выборки автоматически сокращает объем отправляемых на портал данных, пересылая только репрезентативную часть событий.</span><span class="sxs-lookup"><span data-stu-id="c34c2-150">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="c34c2-151">События, составляющие часть той же операции, отбираются как группа, что позволяет перемещаться между связанными событиями.</span><span class="sxs-lookup"><span data-stu-id="c34c2-151">Events that are part of the same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="c34c2-152">Дополнительная информация о выборке.</span><span class="sxs-lookup"><span data-stu-id="c34c2-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-to-see-request-post-data"></a><span data-ttu-id="c34c2-153">Просмотр данных POST запроса</span><span class="sxs-lookup"><span data-stu-id="c34c2-153">How to see request POST data</span></span>
<span data-ttu-id="c34c2-154">Сведения о запросе не содержат данные, отправляемые в приложение в вызове метода POST.</span><span class="sxs-lookup"><span data-stu-id="c34c2-154">Request details don't include the data sent to your app in a POST call.</span></span> <span data-ttu-id="c34c2-155">Для внесения этих данных в отчет:</span><span class="sxs-lookup"><span data-stu-id="c34c2-155">To have this data reported:</span></span>

* <span data-ttu-id="c34c2-156">[Установите пакет SDK](app-insights-asp-net.md) в проект своего приложения.</span><span class="sxs-lookup"><span data-stu-id="c34c2-156">[Install the SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="c34c2-157">Вставьте в свое приложение код для вызова [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="c34c2-157">Insert code in your application to call [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="c34c2-158">Передайте данные POST в параметр сообщения.</span><span class="sxs-lookup"><span data-stu-id="c34c2-158">Send the POST data in the message parameter.</span></span> <span data-ttu-id="c34c2-159">На допустимый размер есть ограничение, поэтому следует пытаться передавать только самые необходимые данные.</span><span class="sxs-lookup"><span data-stu-id="c34c2-159">There is a limit to the permitted size, so you should try to send just the essential data.</span></span>
* <span data-ttu-id="c34c2-160">При исследовании неудачно завершенных запросов найдите связанные трассировки.</span><span class="sxs-lookup"><span data-stu-id="c34c2-160">When you investigate a failed request, find the associated traces.</span></span>  

![Детализация](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="c34c2-162"><a name="exceptions"></a> Запись исключений и связанных диагностических данных</span><span class="sxs-lookup"><span data-stu-id="c34c2-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="c34c2-163">Сначала вы не увидите на портале все исключения, которые приводят к сбоям в приложении.</span><span class="sxs-lookup"><span data-stu-id="c34c2-163">At first, you won't see in the portal all the exceptions that cause failures in your app.</span></span> <span data-ttu-id="c34c2-164">Вы увидите все исключения браузера (если на веб-страницах используется [пакет SDK для JavaScript](app-insights-javascript.md)).</span><span class="sxs-lookup"><span data-stu-id="c34c2-164">You'll see any browser exceptions (if you're using the [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="c34c2-165">Но большинство серверных исключений перехватываются IIS, и вам нужно написать небольшой код, чтобы увидеть их.</span><span class="sxs-lookup"><span data-stu-id="c34c2-165">But most server exceptions are caught by IIS and you have to write a bit of code to see them.</span></span>

<span data-ttu-id="c34c2-166">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="c34c2-166">You can:</span></span>

* <span data-ttu-id="c34c2-167">**Явно регистрировать исключения** путем вставки кода в обработчики исключений для регистрации исключений.</span><span class="sxs-lookup"><span data-stu-id="c34c2-167">**Log exceptions explicitly** by inserting code in exception handlers to report the exceptions.</span></span>
* <span data-ttu-id="c34c2-168">**Автоматически записывать исключения** путем настройки своей платформы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c34c2-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="c34c2-169">Для разных типов платформы необходимы различные дополнения.</span><span class="sxs-lookup"><span data-stu-id="c34c2-169">The necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="c34c2-170">Явная регистрация исключений</span><span class="sxs-lookup"><span data-stu-id="c34c2-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="c34c2-171">Самый простой способ — добавление в обработчик исключений вызова TrackException().</span><span class="sxs-lookup"><span data-stu-id="c34c2-171">The simplest way is to insert a call to TrackException() in an exception handler.</span></span>

<span data-ttu-id="c34c2-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="c34c2-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="c34c2-173">C#</span><span class="sxs-lookup"><span data-stu-id="c34c2-173">C#</span></span>

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

       // Send the exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="c34c2-174">VB</span><span class="sxs-lookup"><span data-stu-id="c34c2-174">VB</span></span>

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

      ' Send the exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="c34c2-175">Параметры свойств и значений не являются обязательными, но они удобны для [фильтрации и добавления](app-insights-diagnostic-search.md) дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="c34c2-175">The properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="c34c2-176">Например, если у вас есть приложение, которое запускает несколько игр, вы можете просматривать все отчеты об исключениях для каждой конкретной игры.</span><span class="sxs-lookup"><span data-stu-id="c34c2-176">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span></span> <span data-ttu-id="c34c2-177">Вы можете добавить в каждый словарь столько элементов, сколько вам нужно.</span><span class="sxs-lookup"><span data-stu-id="c34c2-177">You can add as many items as you like to each dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="c34c2-178">Исключения браузера</span><span class="sxs-lookup"><span data-stu-id="c34c2-178">Browser exceptions</span></span>
<span data-ttu-id="c34c2-179">Большинство исключений браузера регистрируются.</span><span class="sxs-lookup"><span data-stu-id="c34c2-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="c34c2-180">Если веб-страница содержит файлы сценариев из сети доставки содержимого или других доменов, убедитесь, что тег сценария содержит атрибут ```crossorigin="anonymous"```, а сервер отправляет [заголовки CORS](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="c34c2-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has the attribute ```crossorigin="anonymous"```,  and that the server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="c34c2-181">Это позволит вам извлекать трассировки стека и регистрировать необработанные исключения JavaScript из этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c34c2-181">This will allow you to get a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="c34c2-182">Веб-формы</span><span class="sxs-lookup"><span data-stu-id="c34c2-182">Web forms</span></span>
<span data-ttu-id="c34c2-183">Для веб-форм HTTP-модуль будет собирать исключения, если в CustomErrors не настроено перенаправление.</span><span class="sxs-lookup"><span data-stu-id="c34c2-183">For web forms, the HTTP Module will be able to collect the exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="c34c2-184">Однако при наличии активных перенаправлений добавьте следующие строки в функцию Application_Error в сценарий Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="c34c2-184">But if you have active redirects, add the following lines to the Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="c34c2-185">(Добавьте файл Global.asax, если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="c34c2-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="c34c2-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="c34c2-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="c34c2-187">MVC</span><span class="sxs-lookup"><span data-stu-id="c34c2-187">MVC</span></span>
<span data-ttu-id="c34c2-188">Если для конфигурации [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) установлено значение `Off`, исключения будут доступны для сбора в [HTTP-модуле](https://msdn.microsoft.com/library/ms178468.aspx).</span><span class="sxs-lookup"><span data-stu-id="c34c2-188">If the [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for the [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) to collect.</span></span> <span data-ttu-id="c34c2-189">Тем не менее, если это значение `RemoteOnly` (по умолчанию) или `On`, то исключение будет удалено и недоступно для автоматического сбора в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c34c2-189">However, if it is `RemoteOnly` (default), or `On`, then the exception will be cleared and not available for Application Insights to automatically collect.</span></span> <span data-ttu-id="c34c2-190">Эту ситуацию можно исправить, переопределив [класс System.Web.Mvc.HandleErrorAttribute](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx) и применив переопределенный класс, как показано для разных версий MVC ([источник на GitHub](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="c34c2-190">You can fix that by overriding the [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying the overridden class as shown for the different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

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
                //If customError is Off, then AI HTTPModule will report the exception
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

#### <a name="mvc-2"></a><span data-ttu-id="c34c2-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="c34c2-191">MVC 2</span></span>
<span data-ttu-id="c34c2-192">Замените атрибут HandleError новым атрибутом в контроллерах.</span><span class="sxs-lookup"><span data-stu-id="c34c2-192">Replace the HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="c34c2-193">Пример</span><span class="sxs-lookup"><span data-stu-id="c34c2-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="c34c2-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="c34c2-194">MVC 3</span></span>
<span data-ttu-id="c34c2-195">Зарегистрируйте `AiHandleErrorAttribute` в качестве глобального фильтра в Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="c34c2-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="c34c2-196">Пример</span><span class="sxs-lookup"><span data-stu-id="c34c2-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="c34c2-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="c34c2-197">MVC 4, MVC5</span></span>
<span data-ttu-id="c34c2-198">Зарегистрируйте AiHandleErrorAttribute в качестве глобального фильтра в FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="c34c2-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with the override to track unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="c34c2-199">Пример</span><span class="sxs-lookup"><span data-stu-id="c34c2-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="c34c2-200">Web API 1.x</span><span class="sxs-lookup"><span data-stu-id="c34c2-200">Web API 1.x</span></span>
<span data-ttu-id="c34c2-201">Переопределите System.Web.Http.Filters.ExceptionFilterAttribute:</span><span class="sxs-lookup"><span data-stu-id="c34c2-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

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

<span data-ttu-id="c34c2-202">Можно добавить этот переопределенный атрибут в нужные контроллеры или в конфигурации глобальных фильтров в классе WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="c34c2-202">You could add this overridden attribute to specific controllers, or add it to the global filter configuration in the WebApiConfig class:</span></span>

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

[<span data-ttu-id="c34c2-203">Пример</span><span class="sxs-lookup"><span data-stu-id="c34c2-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="c34c2-204">Существует несколько ситуаций, когда обработка фильтров исключений невозможна.</span><span class="sxs-lookup"><span data-stu-id="c34c2-204">There are a number of cases that the exception filters cannot handle.</span></span> <span data-ttu-id="c34c2-205">Например:</span><span class="sxs-lookup"><span data-stu-id="c34c2-205">For example:</span></span>

* <span data-ttu-id="c34c2-206">Исключения выброшены из конструкторов контроллеров.</span><span class="sxs-lookup"><span data-stu-id="c34c2-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="c34c2-207">Исключения выброшены из обработчиков сообщений.</span><span class="sxs-lookup"><span data-stu-id="c34c2-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="c34c2-208">Исключения выброшены при маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="c34c2-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="c34c2-209">Исключения выброшены при сериализации содержимого ответа.</span><span class="sxs-lookup"><span data-stu-id="c34c2-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="c34c2-210">Web API 2.x</span><span class="sxs-lookup"><span data-stu-id="c34c2-210">Web API 2.x</span></span>
<span data-ttu-id="c34c2-211">Добавьте реализацию IExceptionLogger:</span><span class="sxs-lookup"><span data-stu-id="c34c2-211">Add an implementation of IExceptionLogger:</span></span>

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

<span data-ttu-id="c34c2-212">Добавьте это в службы в WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="c34c2-212">Add this to the services in WebApiConfig:</span></span>

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
  <span data-ttu-id="c34c2-213">}</span><span class="sxs-lookup"><span data-stu-id="c34c2-213">}</span></span>

[<span data-ttu-id="c34c2-214">Пример</span><span class="sxs-lookup"><span data-stu-id="c34c2-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="c34c2-215">В качестве альтернативы можно выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="c34c2-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="c34c2-216">Замените только ExceptionHandler пользовательской реализацией IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="c34c2-216">Replace the only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="c34c2-217">Он вызывается, только когда платформа по-прежнему может выбирать ответное сообщение для отправки (но не после прерывания соединения для экземпляра)</span><span class="sxs-lookup"><span data-stu-id="c34c2-217">This is only called when the framework is still able to choose which response message to send (not when the connection is aborted for instance)</span></span>
2. <span data-ttu-id="c34c2-218">Фильтры исключений (как описано выше в разделе для контроллеров Web API 1.x) — не вызываются во всех случаях.</span><span class="sxs-lookup"><span data-stu-id="c34c2-218">Exception Filters (as described in the section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="c34c2-219">WCF</span><span class="sxs-lookup"><span data-stu-id="c34c2-219">WCF</span></span>
<span data-ttu-id="c34c2-220">Добавьте класс, который расширяет Attribute и реализует IErrorHandler и IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="c34c2-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

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

<span data-ttu-id="c34c2-221">Добавьте атрибут в реализации службы:</span><span class="sxs-lookup"><span data-stu-id="c34c2-221">Add the attribute to the service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="c34c2-222">Пример</span><span class="sxs-lookup"><span data-stu-id="c34c2-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="c34c2-223">Счетчики производительности исключений</span><span class="sxs-lookup"><span data-stu-id="c34c2-223">Exception performance counters</span></span>
<span data-ttu-id="c34c2-224">Если на сервере [установлен агент Application Insights](app-insights-monitor-performance-live-website-now.md), то можно получить диаграмму частоты исключений, вычисленной платформой .NET.</span><span class="sxs-lookup"><span data-stu-id="c34c2-224">If you have [installed the Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of the exceptions rate, measured by .NET.</span></span> <span data-ttu-id="c34c2-225">Она включает как обработанные, так и необработанные исключения .NET.</span><span class="sxs-lookup"><span data-stu-id="c34c2-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="c34c2-226">Откройте колонку обозревателя метрик, добавьте новую диаграмму и выберите счетчик **Частота исключений**в списке "Счетчики производительности".</span><span class="sxs-lookup"><span data-stu-id="c34c2-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="c34c2-227">Для вычисление частоты платформа .NET подсчитывает число исключений в интервале и делит его на длину интервала.</span><span class="sxs-lookup"><span data-stu-id="c34c2-227">The .NET framework calculates the rate by counting the number of exceptions in an interval and dividing by the length of the interval.</span></span>

<span data-ttu-id="c34c2-228">Обратите внимание, что она будет отличаться от значения счетчика Exceptions, вычисленного порталом Application Insights по количеству отчетов TrackException.</span><span class="sxs-lookup"><span data-stu-id="c34c2-228">Note that it will be different from the 'Exceptions' count calculated by the Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="c34c2-229">Интервалы выборки различаются, а пакет SDK не отправляет отчеты TrackException для всех обработанных и необработанных исключений.</span><span class="sxs-lookup"><span data-stu-id="c34c2-229">The sampling intervals are different, and the SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="c34c2-230">Видео</span><span class="sxs-lookup"><span data-stu-id="c34c2-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="c34c2-231">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c34c2-231">Next steps</span></span>
* [<span data-ttu-id="c34c2-232">Мониторинг вызовов REST, SQL и других вызовов зависимостей</span><span class="sxs-lookup"><span data-stu-id="c34c2-232">Monitor REST, SQL and other calls to dependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="c34c2-233">Мониторинг времени загрузки страниц, исключений браузера и вызовов AJAX</span><span class="sxs-lookup"><span data-stu-id="c34c2-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="c34c2-234">Мониторинг счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="c34c2-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
