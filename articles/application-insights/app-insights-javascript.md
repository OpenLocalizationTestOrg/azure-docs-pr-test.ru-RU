---
title: "aaaAzure Application Insights для JavaScript веб-приложений | Документы Microsoft"
description: "Получайте данные о количестве просмотров страницы и количестве сеансов, данные веб-клиента и отслеживайте закономерности использования. Выявляйте исключения и проблемы с производительностью на веб-страницах JavaScript."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="753b8-104">Application Insights для веб-страниц</span><span class="sxs-lookup"><span data-stu-id="753b8-104">Application Insights for web pages</span></span>
<span data-ttu-id="753b8-105">Сведения о производительности hello и использования веб-страницы или приложения.</span><span class="sxs-lookup"><span data-stu-id="753b8-105">Find out about hello performance and usage of your web page or app.</span></span> <span data-ttu-id="753b8-106">При добавлении [Application Insights](app-insights-overview.md) tooyour сценарий страницы, вы получаете времени загрузки страницы и AJAX вызовы, количеством и подробности исключения браузера и сбои AJAX, а также пользователей и число сеансов.</span><span class="sxs-lookup"><span data-stu-id="753b8-106">If you add [Application Insights](app-insights-overview.md) tooyour page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="753b8-107">Все эти данные можно разбить по страницам, версии клиентской ОС и браузера, географическому расположению и другим показателям.</span><span class="sxs-lookup"><span data-stu-id="753b8-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="753b8-108">Можно также настроить оповещения для определенного количества сбоев или медленной загрузки страниц.</span><span class="sxs-lookup"><span data-stu-id="753b8-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="753b8-109">И вставляя трассировки вызовов в коде JavaScript, можно отслеживать использования различных функций hello приложения веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="753b8-109">And by inserting trace calls in your JavaScript code, you can track how hello different features of your web page application are used.</span></span>

<span data-ttu-id="753b8-110">Application Insights можно использовать с любыми веб-страницами — просто добавьте небольшой фрагмент кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="753b8-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="753b8-111">Для веб-службы [Java](app-insights-java-get-started.md) или [ASP.NET](app-insights-asp-net.md) можно интегрировать данные телеметрии, полученные с сервера и клиентских компьютеров.</span><span class="sxs-lookup"><span data-stu-id="753b8-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![На сайте portal.azure.com откройте ресурс приложения и щелкните "Браузер".](./media/app-insights-javascript/03.png)

<span data-ttu-id="753b8-113">Вам потребуется подписка слишком[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="753b8-113">You need a subscription too[Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="753b8-114">Если у команды есть подписка организации, попросите владельца tooadd hello tooit вашей учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="753b8-114">If your team has an organizational subscription, ask hello owner tooadd your Microsoft Account tooit.</span></span> <span data-ttu-id="753b8-115">Разработка и использование в небольших масштабах не потребуют никаких денежных затрат.</span><span class="sxs-lookup"><span data-stu-id="753b8-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="753b8-116">Настройка Application Insights для веб-страницы</span><span class="sxs-lookup"><span data-stu-id="753b8-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="753b8-117">Добавьте hello загрузчика кода фрагмент tooyour веб-страницы, следующим образом.</span><span class="sxs-lookup"><span data-stu-id="753b8-117">Add hello loader code snippet tooyour web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="753b8-118">Открытие или создание ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="753b8-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="753b8-119">Hello ресурс Application Insights — которых отображаются данные о производительности и использования на странице.</span><span class="sxs-lookup"><span data-stu-id="753b8-119">hello Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="753b8-120">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="753b8-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="753b8-121">Если вы настроили мониторинг на стороне сервера приложения hello, уже имеют ресурса:</span><span class="sxs-lookup"><span data-stu-id="753b8-121">If you already set up monitoring for hello server side of your app, you already have a resource:</span></span>

![Последовательно выберите пункты «Обзор», «Службы для разработчиков» и «Application Insights».](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="753b8-123">Если ресурса у вас нет, создайте его.</span><span class="sxs-lookup"><span data-stu-id="753b8-123">If you don't have one, create it:</span></span>

![Последовательно выберите пункты «Создать», «Службы для разработчиков», «Application Insights»](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="753b8-125">*Уже появились вопросы?*</span><span class="sxs-lookup"><span data-stu-id="753b8-125">*Questions already?*</span></span> <span data-ttu-id="753b8-126">[Дополнительная информация о создании ресурса](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="753b8-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a><span data-ttu-id="753b8-127">Добавить скрипт tooyour hello пакет SDK для приложения или веб-страницы</span><span class="sxs-lookup"><span data-stu-id="753b8-127">Add hello SDK script tooyour app or web pages</span></span>
<span data-ttu-id="753b8-128">В быстром запуске получение hello скрипта для веб-страниц:</span><span class="sxs-lookup"><span data-stu-id="753b8-128">In Quick Start, get hello script for web pages:</span></span>

![В колонке обзор вашего приложения выберите Быстрый запуск, получить код toomonitor веб-страницы.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="753b8-131">Вставить скрипт hello непосредственно перед hello `</head>` тег каждой страницы, которую должна tootrack.</span><span class="sxs-lookup"><span data-stu-id="753b8-131">Insert hello script just before hello `</head>` tag of every page you want tootrack.</span></span> <span data-ttu-id="753b8-132">Если веб-сайт имеет главной страницы, можно поместить скрипт hello существует.</span><span class="sxs-lookup"><span data-stu-id="753b8-132">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="753b8-133">Например:</span><span class="sxs-lookup"><span data-stu-id="753b8-133">For example:</span></span>

* <span data-ttu-id="753b8-134">В проекте ASP.NET MVC разместите сценарий на странице `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="753b8-134">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="753b8-135">На сайте SharePoint, на панели управления hello, откройте [параметры сайта / Главная страница](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="753b8-135">In a SharePoint site, on hello control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="753b8-136">сценарий Hello содержит ключ инструментирования hello, указывающий ресурс Application Insights tooyour данных hello.</span><span class="sxs-lookup"><span data-stu-id="753b8-136">hello script contains hello instrumentation key that directs hello data tooyour Application Insights resource.</span></span> 

<span data-ttu-id="753b8-137">([Подробно hello скрипта. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="753b8-137">([Deeper explanation of hello script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="753b8-138">*(Если вы используете известную платформу веб-страницы, найдите адаптеры Application Insights. Например, [модуль AngularJS](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="753b8-138">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="753b8-139">Подробные сведения</span><span class="sxs-lookup"><span data-stu-id="753b8-139">Detailed configuration</span></span>
<span data-ttu-id="753b8-140">Вы можете задать несколько [параметров](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config), хотя в большинстве случаев это не требуется.</span><span class="sxs-lookup"><span data-stu-id="753b8-140">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="753b8-141">Например можно отключить или ограничить количество hello вызовов Ajax, регистрируемых в представление страницы (tooreduce трафик).</span><span class="sxs-lookup"><span data-stu-id="753b8-141">For example, you can disable or limit hello number of Ajax calls reported per page view (tooreduce traffic).</span></span> <span data-ttu-id="753b8-142">Или можно задать перемещения телеметрии toohave режим отладки быстро через конвейер hello не выполняется в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="753b8-142">Or you can set debug mode toohave telemetry move rapidly through hello pipeline without being batched.</span></span>

<span data-ttu-id="753b8-143">tooset эти параметры поиска для этой строки в фрагменте кода hello и добавьте после него больше элементов, разделенных запятыми:</span><span class="sxs-lookup"><span data-stu-id="753b8-143">tooset these parameters, look for this line in hello code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="753b8-144">Hello [доступных параметров](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) включают:</span><span class="sxs-lookup"><span data-stu-id="753b8-144">hello [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="753b8-145"><a name="run"></a>Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="753b8-145"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="753b8-146">Запуск веб-приложения, используйте его при toogenerate телеметрии и подождите несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="753b8-146">Run your web app, use it a while toogenerate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="753b8-147">Можно выполнить с помощью hello **F5** ключа на компьютере разработки или опубликовать его и позволяют пользователям работать с его.</span><span class="sxs-lookup"><span data-stu-id="753b8-147">You can either run it using hello **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="753b8-148">Toocheck hello телеметрии, веб-приложение отправляет tooApplication аналитики, используйте средства отладки в браузере (**F12** во многих браузерах).</span><span class="sxs-lookup"><span data-stu-id="753b8-148">If you want toocheck hello telemetry that a web app is sending tooApplication Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="753b8-149">Данные отправляются toodc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="753b8-149">Data is sent toodc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="753b8-150">Просмотр данных о производительности браузера</span><span class="sxs-lookup"><span data-stu-id="753b8-150">Explore your browser performance data</span></span>
<span data-ttu-id="753b8-151">Откройте hello tooshow колонке браузера собранные данные о производительности из браузеры пользователей.</span><span class="sxs-lookup"><span data-stu-id="753b8-151">Open hello Browser blade tooshow aggregated performance data from your users' browsers.</span></span>

![На сайте portal.azure.com откройте ресурс приложения и щелкните "Параметры", а затем "Браузер".](./media/app-insights-javascript/03.png)

<span data-ttu-id="753b8-153">*Еще нет данных? Нажмите кнопку **обновление** вверху hello страницы приветствия. По-прежнему нет данных? См. раздел [Устранение неполадок](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="753b8-153">*No data yet? Click **Refresh** at hello top of hello page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="753b8-154">панель обозревателя Hello — это [колонке обозревателя метрик](app-insights-metrics-explorer.md) с существующие фильтры и выбранные диаграммы.</span><span class="sxs-lookup"><span data-stu-id="753b8-154">hello Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="753b8-155">Диапазон времени hello, фильтры и конфигурации диаграммы можно изменить и сохранить результат hello в список избранного.</span><span class="sxs-lookup"><span data-stu-id="753b8-155">You can edit hello time range, filters, and chart configuration if you want, and save hello result as a favorite.</span></span> <span data-ttu-id="753b8-156">Нажмите кнопку **восстановить значения по умолчанию** tooget задней toohello исходной колонке конфигурации.</span><span class="sxs-lookup"><span data-stu-id="753b8-156">Click **Restore defaults** tooget back toohello original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="753b8-157">Производительность загрузки страниц</span><span class="sxs-lookup"><span data-stu-id="753b8-157">Page load performance</span></span>
<span data-ttu-id="753b8-158">Hello верхней является сегментированных диаграмму времени загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="753b8-158">At hello top is a segmented chart of page load times.</span></span> <span data-ttu-id="753b8-159">Общая высота Hello hello диаграммы представляет hello среднее время tooload и отображения страницы из приложения в браузерах пользователей.</span><span class="sxs-lookup"><span data-stu-id="753b8-159">hello total height of hello chart represents hello average time tooload and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="753b8-160">Hello время отсчитывается с, когда hello браузер отправляет первоначальный HTTP-запрос hello до всего синхронного нагрузки, будут обработаны события, включая макет и выполнение скриптов.</span><span class="sxs-lookup"><span data-stu-id="753b8-160">hello time is measured from when hello browser sends hello initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="753b8-161">Асинхронные задачи, такие как загрузка веб-частей из вызовов AJAX, не учитываются.</span><span class="sxs-lookup"><span data-stu-id="753b8-161">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="753b8-162">Диаграмма Hello делит время загрузки всего страницы приветствия на hello [стандартные затраты времени определено консорциумом W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="753b8-162">hello chart segments hello total page load time into hello [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="753b8-163">Обратите внимание, что hello *сетевых подключений* времени часто — ниже, чем предполагалось, так как среднее над всеми запросами с сервера toohello hello браузера.</span><span class="sxs-lookup"><span data-stu-id="753b8-163">Note that hello *network connect* time is often lower than you might expect, because it's an average over all requests from hello browser toohello server.</span></span> <span data-ttu-id="753b8-164">Множество отдельных запросов иметь время подключения 0, так как уже имеется сервер toohello активное соединение.</span><span class="sxs-lookup"><span data-stu-id="753b8-164">Many individual requests have a connect time of 0 because there is already an active connection toohello server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="753b8-165">Медленная загрузка</span><span class="sxs-lookup"><span data-stu-id="753b8-165">Slow loading?</span></span>
<span data-ttu-id="753b8-166">Медленная загрузка страниц — основная причина недовольства пользователей.</span><span class="sxs-lookup"><span data-stu-id="753b8-166">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="753b8-167">Если диаграмма hello указывает низкая скорость загрузки, это легко toodo некоторое исследование диагностики.</span><span class="sxs-lookup"><span data-stu-id="753b8-167">If hello chart indicates slow page loads, it's easy toodo some diagnostic research.</span></span>

<span data-ttu-id="753b8-168">Hello диаграмме показано среднее hello загружает все страницы в приложении.</span><span class="sxs-lookup"><span data-stu-id="753b8-168">hello chart shows hello average of all page loads in your app.</span></span> <span data-ttu-id="753b8-169">toosee, если проблема hello ограничены tooparticular страниц, внешний вид дальнейшей вниз колонку hello, где имеется сетки, разбитых на URL-адрес страницы:</span><span class="sxs-lookup"><span data-stu-id="753b8-169">toosee if hello problem is confined tooparticular pages, look further down hello blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="753b8-170">Обратите внимание, количество представления страниц hello и стандартное отклонение.</span><span class="sxs-lookup"><span data-stu-id="753b8-170">Notice hello page view count and standard deviation.</span></span> <span data-ttu-id="753b8-171">Количество страниц hello очень мала, затем hello проблема не влияет ли пользователи намного.</span><span class="sxs-lookup"><span data-stu-id="753b8-171">If hello page count is very low, then hello issue isn't affecting users much.</span></span> <span data-ttu-id="753b8-172">Высокий уровень стандартное отклонение (сопоставимых toohello среднее значение самого) указывает на большой объем различия между отдельные измерения.</span><span class="sxs-lookup"><span data-stu-id="753b8-172">A high standard deviation (comparable toohello average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="753b8-173">**Данные для отдельного URL-адреса и отдельного просмотра страницы.**</span><span class="sxs-lookup"><span data-stu-id="753b8-173">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="753b8-174">Щелкните любой toosee имя страницы панель диаграмм отфильтрованные просто toothat URL-адрес браузера; а затем на экземпляр представления страницы.</span><span class="sxs-lookup"><span data-stu-id="753b8-174">Click any page name toosee a blade of browser charts filtered just toothat URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="753b8-175">Нажмите кнопку `...` полный список свойств для данного события или проверить вызовы Ajax hello и связанные события.</span><span class="sxs-lookup"><span data-stu-id="753b8-175">Click `...` for a full list of properties for that event, or inspect hello Ajax calls and related events.</span></span> <span data-ttu-id="753b8-176">Привет, влияют на медленных вызовов Ajax общее время загрузки страницы, если они являются синхронными.</span><span class="sxs-lookup"><span data-stu-id="753b8-176">Slow Ajax calls affect hello overall page load time if they are synchronous.</span></span> <span data-ttu-id="753b8-177">Связанные события включают запросы серверов на hello же URL-адрес (Если вы настроили Application Insights на веб-сервере).</span><span class="sxs-lookup"><span data-stu-id="753b8-177">Related events include server requests for hello same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="753b8-178">**Производительность страниц со временем.**</span><span class="sxs-lookup"><span data-stu-id="753b8-178">**Page performance over time.**</span></span> <span data-ttu-id="753b8-179">В колонке браузеры hello измените hello время загрузки страницы сетки в toosee линии диаграммы при отсутствии пики в том:</span><span class="sxs-lookup"><span data-stu-id="753b8-179">Back at hello Browsers blade, change hello Page View Load Time grid into a line chart toosee if there were peaks at particular times:</span></span>

![Щелкните заголовок hello hello сетки и выберите новый тип диаграммы](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="753b8-181">**Сегментация по другим показателям.**</span><span class="sxs-lookup"><span data-stu-id="753b8-181">**Segment by other dimensions.**</span></span> <span data-ttu-id="753b8-182">Может быть страницы находятся медленнее tooload на конкретном отношении браузера, операционной системы клиента или пользователя?</span><span class="sxs-lookup"><span data-stu-id="753b8-182">Maybe your pages are slower tooload on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="753b8-183">Добавить новую диаграмму и поэкспериментировать с hello **Group by** измерения.</span><span class="sxs-lookup"><span data-stu-id="753b8-183">Add a new chart and experiment with hello **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="753b8-184">Производительность вызовов AJAX</span><span class="sxs-lookup"><span data-stu-id="753b8-184">AJAX Performance</span></span>
<span data-ttu-id="753b8-185">Убедитесь, что все вызовы AJAX на веб-страницах работают нормально.</span><span class="sxs-lookup"><span data-stu-id="753b8-185">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="753b8-186">Это часто используется toofill частей страницы асинхронно.</span><span class="sxs-lookup"><span data-stu-id="753b8-186">They are often used toofill parts of your page asynchronously.</span></span> <span data-ttu-id="753b8-187">Несмотря на то, что hello страницы целиком может загрузить незамедлительно, пользователям может быть надоело перед пустой веб-частей, Ожидание tooappear данных в них.</span><span class="sxs-lookup"><span data-stu-id="753b8-187">Although hello overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data tooappear in them.</span></span>

<span data-ttu-id="753b8-188">Вызовы AJAX на веб-странице отображаются в колонке браузеры hello как зависимости.</span><span class="sxs-lookup"><span data-stu-id="753b8-188">AJAX calls made from your web page are shown on hello Browsers blade as dependencies.</span></span>

<span data-ttu-id="753b8-189">Существует сводных диаграмм в верхней части колонки hello hello.</span><span class="sxs-lookup"><span data-stu-id="753b8-189">There are summary charts in hello upper part of hello blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="753b8-190">Подробные таблицы приводятся ниже:</span><span class="sxs-lookup"><span data-stu-id="753b8-190">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="753b8-191">Щелкните любую строку для получения подробной информации.</span><span class="sxs-lookup"><span data-stu-id="753b8-191">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="753b8-192">При удалении фильтра браузеры hello в колонке hello зависимостей AJAX и сервера включены в эти диаграммы.</span><span class="sxs-lookup"><span data-stu-id="753b8-192">If you delete hello Browsers filter on hello blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="753b8-193">Нажмите кнопку Восстановить значения по умолчанию фильтр tooreconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="753b8-193">Click Restore Defaults tooreconfigure hello filter.</span></span>
> 
> 

<span data-ttu-id="753b8-194">**toodrill в неудачные вызовы Ajax** прокрутите вниз по сетке сбоев toohello зависимостей и нажмите кнопку toosee конкретные экземпляры строк.</span><span class="sxs-lookup"><span data-stu-id="753b8-194">**toodrill into failed Ajax calls** scroll down toohello Dependency failures grid, and then click a row toosee specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="753b8-195">Щелкните `...` для hello полный телеметрии для вызова Ajax.</span><span class="sxs-lookup"><span data-stu-id="753b8-195">Click `...` for hello full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="753b8-196">Вызовы AJAX не регистрируются?</span><span class="sxs-lookup"><span data-stu-id="753b8-196">No Ajax calls reported?</span></span>
<span data-ttu-id="753b8-197">Вызовы AJAX включают все вызовы HTTP/HTTPS, выполненные из скрипта hello веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="753b8-197">Ajax calls include any HTTP/HTTPS  calls made from hello script of your web page.</span></span> <span data-ttu-id="753b8-198">Если вы не видите их сообщил, проверьте, что фрагмент кода hello не hello `disableAjaxTracking` или `maxAjaxCallsPerView` [параметры](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="753b8-198">If you don't see them reported, check that hello code snippet doesn't set hello `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="753b8-199">Исключения браузера</span><span class="sxs-lookup"><span data-stu-id="753b8-199">Browser exceptions</span></span>
<span data-ttu-id="753b8-200">В колонке браузеры hello является исключения Сводные диаграммы и сетки типов исключений дальнейшей вниз колонку hello.</span><span class="sxs-lookup"><span data-stu-id="753b8-200">On hello Browsers blade, there's an exceptions summary chart, and a grid of exception types further down hello blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="753b8-201">Если вы не видите исключения браузера, проверьте, этот фрагмент кода hello не hello `disableExceptionTracking` [параметр](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="753b8-201">If you don't see browser exceptions reported, check that hello code snippet doesn't set hello `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="753b8-202">Изучение отдельных событий просмотра страницы</span><span class="sxs-lookup"><span data-stu-id="753b8-202">Inspect individual page view events</span></span>

<span data-ttu-id="753b8-203">Обычно телеметрия просмотра страниц анализируется службой Application Insights, и вы видите только сводные отчеты со средними значениями для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="753b8-203">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="753b8-204">Однако в целях отладки можно также изучать отдельные события просмотра страниц.</span><span class="sxs-lookup"><span data-stu-id="753b8-204">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="753b8-205">В колонке диагностики поиска hello задайте фильтры tooPage представления.</span><span class="sxs-lookup"><span data-stu-id="753b8-205">In hello Diagnostic Search blade, set Filters tooPage View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="753b8-206">Выберите любое событие toosee более подробно.</span><span class="sxs-lookup"><span data-stu-id="753b8-206">Select any event toosee more detail.</span></span> <span data-ttu-id="753b8-207">Hello сведения на странице нажмите кнопку «...» toosee еще более подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="753b8-207">In hello details page, click "..." toosee even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="753b8-208">При использовании [поиска](app-insights-diagnostic-search.md), обратите внимание, наличие слова целиком toomatch: «О» и «Подробнее» о «About» не совпадают.</span><span class="sxs-lookup"><span data-stu-id="753b8-208">If you use [Search](app-insights-diagnostic-search.md), notice that you have toomatch whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="753b8-209">Можно также использовать hello мощные [языка запросов анализа журналов](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch страницы представления.</span><span class="sxs-lookup"><span data-stu-id="753b8-209">You can also use hello powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="753b8-210">Свойства просмотра страниц</span><span class="sxs-lookup"><span data-stu-id="753b8-210">Page view properties</span></span>
* <span data-ttu-id="753b8-211">**Длительность просмотра страницы**</span><span class="sxs-lookup"><span data-stu-id="753b8-211">**Page view duration**</span></span> 
  
  * <span data-ttu-id="753b8-212">По умолчанию hello он принимает tooload hello страница времени, toofull клиентом запроса загрузки (включая вспомогательные файлы, но исключая асинхронных задач, таких как вызовы Ajax).</span><span class="sxs-lookup"><span data-stu-id="753b8-212">By default, hello time it takes tooload hello page, from client request toofull load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="753b8-213">Если задать `overridePageViewDuration` в hello [конфигурация страницы](#detailed-configuration), сначала hello интервал между tooexecution запрос клиента из hello `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="753b8-213">If you set `overridePageViewDuration` in hello [page configuration](#detailed-configuration), hello interval between client request tooexecution of hello first `trackPageView`.</span></span> <span data-ttu-id="753b8-214">Если trackPageView перемещены из своего обычного положения после инициализации hello hello сценария, его отразят другое значение.</span><span class="sxs-lookup"><span data-stu-id="753b8-214">If you moved trackPageView from its usual position after hello initialization of hello script, it will reflect a different value.</span></span>
  * <span data-ttu-id="753b8-215">Если `overridePageViewDuration` и длительность, аргумент передан в hello `trackPageView()` вызова, то вместо него используется значение аргумента hello.</span><span class="sxs-lookup"><span data-stu-id="753b8-215">If `overridePageViewDuration` is set and a duration argument is provided in hello `trackPageView()` call, then hello argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="753b8-216">Настраиваемые счетчики страниц</span><span class="sxs-lookup"><span data-stu-id="753b8-216">Custom page counts</span></span>
<span data-ttu-id="753b8-217">По умолчанию количество страниц происходит каждый раз, когда загрузка новой страницы в браузер клиента hello.</span><span class="sxs-lookup"><span data-stu-id="753b8-217">By default, a page count occurs each time a new page loads into hello client browser.</span></span>  <span data-ttu-id="753b8-218">Однако при необходимости toocount дополнительная страница представления.</span><span class="sxs-lookup"><span data-stu-id="753b8-218">But you might want toocount additional page views.</span></span> <span data-ttu-id="753b8-219">Например страница может отобразить его содержимое во вкладках и требуется toocount страницей, когда пользователь hello переключает вкладки.</span><span class="sxs-lookup"><span data-stu-id="753b8-219">For example, a page might display its content in tabs and you want toocount a page when hello user switches tabs.</span></span> <span data-ttu-id="753b8-220">Или кода JavaScript на странице приветствия может загрузить новое содержимое без изменения URL-адрес браузера hello.</span><span class="sxs-lookup"><span data-stu-id="753b8-220">Or JavaScript code in hello page might load new content without changing hello browser's URL.</span></span>

<span data-ttu-id="753b8-221">В hello соответствующую точку в коде клиента, вставьте вызов JavaScript следующим образом:</span><span class="sxs-lookup"><span data-stu-id="753b8-221">Insert a JavaScript call like this at hello appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="753b8-222">имя страницы приветствия может содержать hello же символы URL-адрес, а любые после «#» или «?» игнорируется.</span><span class="sxs-lookup"><span data-stu-id="753b8-222">hello page name can contain hello same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="753b8-223">Отслеживание использования</span><span class="sxs-lookup"><span data-stu-id="753b8-223">Usage tracking</span></span>
<span data-ttu-id="753b8-224">Требуется toofind пользователей, выполнять с помощью приложения?</span><span class="sxs-lookup"><span data-stu-id="753b8-224">Want toofind out what your users do with your app?</span></span>

* [<span data-ttu-id="753b8-225">Дополнительные сведения об отслеживании использования</span><span class="sxs-lookup"><span data-stu-id="753b8-225">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="753b8-226">[Дополнительные сведения об API пользовательских событий и метрик](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="753b8-226">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="753b8-227"><a name="video"></a> Видео</span><span class="sxs-lookup"><span data-stu-id="753b8-227"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="753b8-228"><a name="next"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="753b8-228"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="753b8-229">Отслеживание использования</span><span class="sxs-lookup"><span data-stu-id="753b8-229">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="753b8-230">Пользовательские события и метрики</span><span class="sxs-lookup"><span data-stu-id="753b8-230">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="753b8-231">Сборка, измерение и обучение</span><span class="sxs-lookup"><span data-stu-id="753b8-231">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

