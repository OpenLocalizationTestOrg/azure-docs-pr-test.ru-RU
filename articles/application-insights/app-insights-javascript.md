---
title: "Azure Application Insights и веб-приложения JavaScript | Документация Майкрософт"
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
ms.openlocfilehash: 4e8a77e3644bb726d1b8e2050dab61893ccfa3c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="5e720-104">Application Insights для веб-страниц</span><span class="sxs-lookup"><span data-stu-id="5e720-104">Application Insights for web pages</span></span>
<span data-ttu-id="5e720-105">Узнайте о производительности и использовании своей веб-страницы или приложения.</span><span class="sxs-lookup"><span data-stu-id="5e720-105">Find out about the performance and usage of your web page or app.</span></span> <span data-ttu-id="5e720-106">Если добавить [Application Insights](app-insights-overview.md) в скрипт страницы, вы узнаете время загрузки страницы и вызовов AJAX, сведения об исключениях браузера, ошибках AJAX и их количестве, а также количество пользователей и сеансов.</span><span class="sxs-lookup"><span data-stu-id="5e720-106">If you add [Application Insights](app-insights-overview.md) to your page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="5e720-107">Все эти данные можно разбить по страницам, версии клиентской ОС и браузера, географическому расположению и другим показателям.</span><span class="sxs-lookup"><span data-stu-id="5e720-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="5e720-108">Можно также настроить оповещения для определенного количества сбоев или медленной загрузки страниц.</span><span class="sxs-lookup"><span data-stu-id="5e720-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="5e720-109">Кроме того, вставив вызовы трассировки в код JavaScript, вы можете отслеживать использование различных функций приложения веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="5e720-109">And by inserting trace calls in your JavaScript code, you can track how the different features of your web page application are used.</span></span>

<span data-ttu-id="5e720-110">Application Insights можно использовать с любыми веб-страницами — просто добавьте небольшой фрагмент кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5e720-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="5e720-111">Для веб-службы [Java](app-insights-java-get-started.md) или [ASP.NET](app-insights-asp-net.md) можно интегрировать данные телеметрии, полученные с сервера и клиентских компьютеров.</span><span class="sxs-lookup"><span data-stu-id="5e720-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![На сайте portal.azure.com откройте ресурс приложения и щелкните "Браузер".](./media/app-insights-javascript/03.png)

<span data-ttu-id="5e720-113">Вам понадобится подписка [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="5e720-113">You need a subscription to [Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="5e720-114">Если у вашей группы есть подписка организации, попросите владельца подписки добавить в нее вашу учетную запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5e720-114">If your team has an organizational subscription, ask the owner to add your Microsoft Account to it.</span></span> <span data-ttu-id="5e720-115">Разработка и использование в небольших масштабах не потребуют никаких денежных затрат.</span><span class="sxs-lookup"><span data-stu-id="5e720-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="5e720-116">Настройка Application Insights для веб-страницы</span><span class="sxs-lookup"><span data-stu-id="5e720-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="5e720-117">Добавьте фрагмент кода загрузчика на веб-страницы, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5e720-117">Add the loader code snippet to your web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="5e720-118">Открытие или создание ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="5e720-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="5e720-119">Ресурс Application Insights — это место, где отображаются данные о производительности и об использовании страницы.</span><span class="sxs-lookup"><span data-stu-id="5e720-119">The Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="5e720-120">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5e720-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="5e720-121">Если вы уже настроили мониторинг приложения на стороне сервера, то у вас уже есть ресурс.</span><span class="sxs-lookup"><span data-stu-id="5e720-121">If you already set up monitoring for the server side of your app, you already have a resource:</span></span>

![Последовательно выберите пункты «Обзор», «Службы для разработчиков» и «Application Insights».](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="5e720-123">Если ресурса у вас нет, создайте его.</span><span class="sxs-lookup"><span data-stu-id="5e720-123">If you don't have one, create it:</span></span>

![Последовательно выберите пункты «Создать», «Службы для разработчиков», «Application Insights»](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="5e720-125">*Уже появились вопросы?*</span><span class="sxs-lookup"><span data-stu-id="5e720-125">*Questions already?*</span></span> <span data-ttu-id="5e720-126">[Дополнительная информация о создании ресурса](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="5e720-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-the-sdk-script-to-your-app-or-web-pages"></a><span data-ttu-id="5e720-127">Добавление сценария пакета SDK в приложение или на веб-страницу</span><span class="sxs-lookup"><span data-stu-id="5e720-127">Add the SDK script to your app or web pages</span></span>
<span data-ttu-id="5e720-128">В разделе «Быстрый запуск» получите сценарий для веб-страниц:</span><span class="sxs-lookup"><span data-stu-id="5e720-128">In Quick Start, get the script for web pages:</span></span>

![В колонке обзора приложения последовательно выберите элементы «Быстрый запуск», «Получить код для мониторинга моих веб-страниц».](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="5e720-131">Вставьте сценарий непосредственно перед тегом `</head>` каждой страницы, которую вы хотите отслеживать. Если на вашем веб-сайте есть главная страница, можно разместить сценарий на ней.</span><span class="sxs-lookup"><span data-stu-id="5e720-131">Insert the script just before the `</head>` tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="5e720-132">Например:</span><span class="sxs-lookup"><span data-stu-id="5e720-132">For example:</span></span>

* <span data-ttu-id="5e720-133">В проекте ASP.NET MVC разместите сценарий на странице `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="5e720-133">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="5e720-134">На сайте SharePoint на панели управления откройте [Параметры сайта/Главная страница](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="5e720-134">In a SharePoint site, on the control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="5e720-135">Сценарий содержит ключ инструментирования, который направляет данные к ресурсу Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5e720-135">The script contains the instrumentation key that directs the data to your Application Insights resource.</span></span> 

<span data-ttu-id="5e720-136">([Подробное объяснение сценария.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="5e720-136">([Deeper explanation of the script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="5e720-137">*(Если вы используете известную платформу веб-страницы, найдите адаптеры Application Insights. Например, [модуль AngularJS](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="5e720-137">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="5e720-138">Подробные сведения</span><span class="sxs-lookup"><span data-stu-id="5e720-138">Detailed configuration</span></span>
<span data-ttu-id="5e720-139">Вы можете задать несколько [параметров](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config), хотя в большинстве случаев это не требуется.</span><span class="sxs-lookup"><span data-stu-id="5e720-139">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="5e720-140">Например, можно отключить или ограничить количество вызовов AJAX, регистрируемых при каждом просмотре страницы (чтобы уменьшить трафик).</span><span class="sxs-lookup"><span data-stu-id="5e720-140">For example, you can disable or limit the number of Ajax calls reported per page view (to reduce traffic).</span></span> <span data-ttu-id="5e720-141">Или можно задать режим отладки, чтобы быстрее пропустить данные телеметрии через конвейер, не выполняя пакетные операции.</span><span class="sxs-lookup"><span data-stu-id="5e720-141">Or you can set debug mode to have telemetry move rapidly through the pipeline without being batched.</span></span>

<span data-ttu-id="5e720-142">Чтобы задать эти параметры, найдите следующую строку в фрагменте кода и добавьте после нее несколько элементов, разделенных запятой:</span><span class="sxs-lookup"><span data-stu-id="5e720-142">To set these parameters, look for this line in the code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="5e720-143">[Доступные параметры](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) включают:</span><span class="sxs-lookup"><span data-stu-id="5e720-143">The [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember to remove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, to reduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up to execution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="5e720-144"><a name="run"></a>Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="5e720-144"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="5e720-145">Запустите веб-приложение, используйте его в течение непродолжительного времени для формирования телеметрии и подождите несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="5e720-145">Run your web app, use it a while to generate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="5e720-146">Вы также можете запустить приложение на компьютере, на котором ведется разработка, нажав клавишу **F5**, или опубликовать и позволить пользователям его использовать.</span><span class="sxs-lookup"><span data-stu-id="5e720-146">You can either run it using the **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="5e720-147">Если вам надо проверить телеметрию, отправляемую веб-приложением в Application Insights, используйте инструменты отладки браузера (во многих браузерах это можно сделать нажатием клавиши**F12** ).</span><span class="sxs-lookup"><span data-stu-id="5e720-147">If you want to check the telemetry that a web app is sending to Application Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="5e720-148">Данные отправляются по адресу dc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="5e720-148">Data is sent to dc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="5e720-149">Просмотр данных о производительности браузера</span><span class="sxs-lookup"><span data-stu-id="5e720-149">Explore your browser performance data</span></span>
<span data-ttu-id="5e720-150">Откройте колонку "Браузер", чтобы отобразить сводные данные о производительности, поступающие из браузеров пользователей.</span><span class="sxs-lookup"><span data-stu-id="5e720-150">Open the Browser blade to show aggregated performance data from your users' browsers.</span></span>

![На сайте portal.azure.com откройте ресурс приложения и щелкните "Параметры", а затем "Браузер".](./media/app-insights-javascript/03.png)

<span data-ttu-id="5e720-152">*Еще нет данных? Щелкните **Обновить** в верхней части страницы. По-прежнему нет данных? См. раздел [Устранение неполадок](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="5e720-152">*No data yet? Click **Refresh** at the top of the page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="5e720-153">Колонка "Браузер" — это [колонка обозревателя метрик](app-insights-metrics-explorer.md) с предустановленными фильтрами и предварительно выбранными параметрами диаграмм.</span><span class="sxs-lookup"><span data-stu-id="5e720-153">The Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="5e720-154">При необходимости можно изменить диапазон времени, фильтры и конфигурацию диаграмм и сохранить результат в избранном.</span><span class="sxs-lookup"><span data-stu-id="5e720-154">You can edit the time range, filters, and chart configuration if you want, and save the result as a favorite.</span></span> <span data-ttu-id="5e720-155">Щелкните **Восстановить значения по умолчанию**, чтобы вернуться к исходной конфигурации колонки.</span><span class="sxs-lookup"><span data-stu-id="5e720-155">Click **Restore defaults** to get back to the original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="5e720-156">Производительность загрузки страниц</span><span class="sxs-lookup"><span data-stu-id="5e720-156">Page load performance</span></span>
<span data-ttu-id="5e720-157">Вверху экрана отображается сегментированная диаграмма времени загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="5e720-157">At the top is a segmented chart of page load times.</span></span> <span data-ttu-id="5e720-158">Общая высота диаграммы представляет среднее время загрузки и отображения страниц приложения в браузерах пользователей.</span><span class="sxs-lookup"><span data-stu-id="5e720-158">The total height of the chart represents the average time to load and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="5e720-159">Время отсчитывается от момента, когда браузер отправляет первоначальный запрос HTTP, до момента, когда завершается обработка всех синхронных событий загрузки, включая макет и выполняющиеся сценарии.</span><span class="sxs-lookup"><span data-stu-id="5e720-159">The time is measured from when the browser sends the initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="5e720-160">Асинхронные задачи, такие как загрузка веб-частей из вызовов AJAX, не учитываются.</span><span class="sxs-lookup"><span data-stu-id="5e720-160">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="5e720-161">На этой диаграмме общее время загрузки страницы разбито на [стандартные отрезки времени, определенные консорциумом W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="5e720-161">The chart segments the total page load time into the [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="5e720-162">Обратите внимание, что значение времени *подключения к сети* часто меньше ожидаемого, так как это среднее значение по всем запросам из браузера на сервер.</span><span class="sxs-lookup"><span data-stu-id="5e720-162">Note that the *network connect* time is often lower than you might expect, because it's an average over all requests from the browser to the server.</span></span> <span data-ttu-id="5e720-163">Для множества отдельных запросов значение времени подключения — «0» из-за наличия активного подключения к серверу.</span><span class="sxs-lookup"><span data-stu-id="5e720-163">Many individual requests have a connect time of 0 because there is already an active connection to the server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="5e720-164">Медленная загрузка</span><span class="sxs-lookup"><span data-stu-id="5e720-164">Slow loading?</span></span>
<span data-ttu-id="5e720-165">Медленная загрузка страниц — основная причина недовольства пользователей.</span><span class="sxs-lookup"><span data-stu-id="5e720-165">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="5e720-166">Если диаграмма показывает, что страницы загружаются медленно, вы можете выполнить ряд простых диагностических исследований.</span><span class="sxs-lookup"><span data-stu-id="5e720-166">If the chart indicates slow page loads, it's easy to do some diagnostic research.</span></span>

<span data-ttu-id="5e720-167">На диаграмме показано среднее время загрузки всех страниц в приложении.</span><span class="sxs-lookup"><span data-stu-id="5e720-167">The chart shows the average of all page loads in your app.</span></span> <span data-ttu-id="5e720-168">Чтобы узнать, связана ли проблема с определенными страницами, найдите в колонке таблицу, где данные разбиты по URL-адресам страниц:</span><span class="sxs-lookup"><span data-stu-id="5e720-168">To see if the problem is confined to particular pages, look further down the blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="5e720-169">Обратите внимание на количество просмотров страниц и стандартное отклонение.</span><span class="sxs-lookup"><span data-stu-id="5e720-169">Notice the page view count and standard deviation.</span></span> <span data-ttu-id="5e720-170">Если страниц очень мало, проблема не доставляет пользователям особых неудобств.</span><span class="sxs-lookup"><span data-stu-id="5e720-170">If the page count is very low, then the issue isn't affecting users much.</span></span> <span data-ttu-id="5e720-171">Высокий уровень стандартного отклонения (относительно среднего уровня) указывает на большие различия между отдельными измерениями.</span><span class="sxs-lookup"><span data-stu-id="5e720-171">A high standard deviation (comparable to the average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="5e720-172">**Данные для отдельного URL-адреса и отдельного просмотра страницы.**</span><span class="sxs-lookup"><span data-stu-id="5e720-172">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="5e720-173">Щелкните имя любой страницы, чтобы отобразить колонку диаграмм браузера, отфильтрованных только для этого URL-адреса. То же самое можно сделать для экземпляра представления страницы.</span><span class="sxs-lookup"><span data-stu-id="5e720-173">Click any page name to see a blade of browser charts filtered just to that URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="5e720-174">Щелкните `...`, чтобы увидеть полный список свойств для данного события или проверить вызовы AJAX и связанные события.</span><span class="sxs-lookup"><span data-stu-id="5e720-174">Click `...` for a full list of properties for that event, or inspect the Ajax calls and related events.</span></span> <span data-ttu-id="5e720-175">Медленные вызовы AJAX влияют на общее время загрузки страницы, если они выполняются синхронно.</span><span class="sxs-lookup"><span data-stu-id="5e720-175">Slow Ajax calls affect the overall page load time if they are synchronous.</span></span> <span data-ttu-id="5e720-176">К связанным событиям относятся запросы сервера для того же URL-адреса (если вы настроили Application Insights на веб-сервере).</span><span class="sxs-lookup"><span data-stu-id="5e720-176">Related events include server requests for the same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="5e720-177">**Производительность страниц со временем.**</span><span class="sxs-lookup"><span data-stu-id="5e720-177">**Page performance over time.**</span></span> <span data-ttu-id="5e720-178">Вернитесь в колонку "Браузеры" и вместо таблицы "Время загрузки страницы" выберите график, на котором отображаются пиковые значения в определенное время:</span><span class="sxs-lookup"><span data-stu-id="5e720-178">Back at the Browsers blade, change the Page View Load Time grid into a line chart to see if there were peaks at particular times:</span></span>

![Щелкните заголовок таблицы и выберите новый тип диаграммы.](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="5e720-180">**Сегментация по другим показателям.**</span><span class="sxs-lookup"><span data-stu-id="5e720-180">**Segment by other dimensions.**</span></span> <span data-ttu-id="5e720-181">Возможно, загрузка страниц происходит медленнее в конкретном браузере, клиентской ОС или расположении пользователя?</span><span class="sxs-lookup"><span data-stu-id="5e720-181">Maybe your pages are slower to load on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="5e720-182">Добавьте новую диаграмму и поэкспериментируйте с параметром **Группировать по** .</span><span class="sxs-lookup"><span data-stu-id="5e720-182">Add a new chart and experiment with the **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="5e720-183">Производительность вызовов AJAX</span><span class="sxs-lookup"><span data-stu-id="5e720-183">AJAX Performance</span></span>
<span data-ttu-id="5e720-184">Убедитесь, что все вызовы AJAX на веб-страницах работают нормально.</span><span class="sxs-lookup"><span data-stu-id="5e720-184">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="5e720-185">Они часто используются для асинхронного заполнения частей страницы.</span><span class="sxs-lookup"><span data-stu-id="5e720-185">They are often used to fill parts of your page asynchronously.</span></span> <span data-ttu-id="5e720-186">Иногда вся страница загружается быстро, но остаются пустые веб-части, данные в которых отображаются не сразу. Естественно, это вызывает раздражение пользователей.</span><span class="sxs-lookup"><span data-stu-id="5e720-186">Although the overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data to appear in them.</span></span>

<span data-ttu-id="5e720-187">Вызовы AJAX, выполняемые с веб-страницы, отображаются в колонке "Браузеры" как зависимости.</span><span class="sxs-lookup"><span data-stu-id="5e720-187">AJAX calls made from your web page are shown on the Browsers blade as dependencies.</span></span>

<span data-ttu-id="5e720-188">В верхней части колонки есть сводные диаграммы:</span><span class="sxs-lookup"><span data-stu-id="5e720-188">There are summary charts in the upper part of the blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="5e720-189">Подробные таблицы приводятся ниже:</span><span class="sxs-lookup"><span data-stu-id="5e720-189">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="5e720-190">Щелкните любую строку для получения подробной информации.</span><span class="sxs-lookup"><span data-stu-id="5e720-190">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="5e720-191">Если удалить фильтр "Браузеры" в колонке, зависимости сервера и зависимости AJAX будут включены в эти диаграммы.</span><span class="sxs-lookup"><span data-stu-id="5e720-191">If you delete the Browsers filter on the blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="5e720-192">Чтобы повторно настроить фильтр, щелкните "Восстановить значения по умолчанию".</span><span class="sxs-lookup"><span data-stu-id="5e720-192">Click Restore Defaults to reconfigure the filter.</span></span>
> 
> 

<span data-ttu-id="5e720-193">**Для быстрого анализа вызовов AJAX, завершившихся сбоем**, прокрутите вниз до таблицы сбоев зависимостей и щелкните строку, чтобы просмотреть конкретные экземпляры.</span><span class="sxs-lookup"><span data-stu-id="5e720-193">**To drill into failed Ajax calls** scroll down to the Dependency failures grid, and then click a row to see specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="5e720-194">Щелкните `...`, чтобы получить полные данные телеметрии для вызова AJAX.</span><span class="sxs-lookup"><span data-stu-id="5e720-194">Click `...` for the full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="5e720-195">Вызовы AJAX не регистрируются?</span><span class="sxs-lookup"><span data-stu-id="5e720-195">No Ajax calls reported?</span></span>
<span data-ttu-id="5e720-196">Вызовы AJAX включают все вызовы HTTP/HTTPS из сценария веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="5e720-196">Ajax calls include any HTTP/HTTPS  calls made from the script of your web page.</span></span> <span data-ttu-id="5e720-197">Если они не регистрируются, проверьте, не заданы ли во фрагменте кода [параметры](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableAjaxTracking` или `maxAjaxCallsPerView`.</span><span class="sxs-lookup"><span data-stu-id="5e720-197">If you don't see them reported, check that the code snippet doesn't set the `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="5e720-198">Исключения браузера</span><span class="sxs-lookup"><span data-stu-id="5e720-198">Browser exceptions</span></span>
<span data-ttu-id="5e720-199">В нижней части колонке "Браузеры" есть сводная диаграмма исключений и таблица типов исключений.</span><span class="sxs-lookup"><span data-stu-id="5e720-199">On the Browsers blade, there's an exceptions summary chart, and a grid of exception types further down the blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="5e720-200">Если исключения браузера не регистрируются, проверьте, не задан ли во фрагменте кода [параметр](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableExceptionTracking`.</span><span class="sxs-lookup"><span data-stu-id="5e720-200">If you don't see browser exceptions reported, check that the code snippet doesn't set the `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="5e720-201">Изучение отдельных событий просмотра страницы</span><span class="sxs-lookup"><span data-stu-id="5e720-201">Inspect individual page view events</span></span>

<span data-ttu-id="5e720-202">Обычно телеметрия просмотра страниц анализируется службой Application Insights, и вы видите только сводные отчеты со средними значениями для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="5e720-202">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="5e720-203">Однако в целях отладки можно также изучать отдельные события просмотра страниц.</span><span class="sxs-lookup"><span data-stu-id="5e720-203">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="5e720-204">В колонке Diagnostic Search (Поиск данных диагностики) в разделе Filter (Фильтр) установите флажок Page View (Просмотр страниц).</span><span class="sxs-lookup"><span data-stu-id="5e720-204">In the Diagnostic Search blade, set Filters to Page View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="5e720-205">Выберите любое событие, чтобы просмотреть подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="5e720-205">Select any event to see more detail.</span></span> <span data-ttu-id="5e720-206">На странице сведений нажмите кнопку «...», чтобы открыть еще более подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="5e720-206">In the details page, click "..." to see even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="5e720-207">Если вы используете [Поиск](app-insights-diagnostic-search.md), обратите внимание, что вы должны сопоставлять слова целиком: "Пр" и "о" не соответствуют "Про".</span><span class="sxs-lookup"><span data-stu-id="5e720-207">If you use [Search](app-insights-diagnostic-search.md), notice that you have to match whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="5e720-208">Кроме того, для поиска просмотров страницы можно использовать [язык запросов Log Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table).</span><span class="sxs-lookup"><span data-stu-id="5e720-208">You can also use the powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) to search page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="5e720-209">Свойства просмотра страниц</span><span class="sxs-lookup"><span data-stu-id="5e720-209">Page view properties</span></span>
* <span data-ttu-id="5e720-210">**Длительность просмотра страницы**</span><span class="sxs-lookup"><span data-stu-id="5e720-210">**Page view duration**</span></span> 
  
  * <span data-ttu-id="5e720-211">По умолчанию время, необходимое для загрузки страницы, от запроса клиента до полной загрузки (включая вспомогательные файлы, но за исключением асинхронных задач, таких как вызовы Ajax).</span><span class="sxs-lookup"><span data-stu-id="5e720-211">By default, the time it takes to load the page, from client request to full load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="5e720-212">Если в `overridePageViewDuration`конфигурации страницы[ указано значение ](#detailed-configuration), это интервал между запросом клиента и выполнением первого `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="5e720-212">If you set `overridePageViewDuration` in the [page configuration](#detailed-configuration), the interval between client request to execution of the first `trackPageView`.</span></span> <span data-ttu-id="5e720-213">Если после инициализации сценария trackPageView вы переместили его из обычного положения, значение будет иным.</span><span class="sxs-lookup"><span data-stu-id="5e720-213">If you moved trackPageView from its usual position after the initialization of the script, it will reflect a different value.</span></span>
  * <span data-ttu-id="5e720-214">Если задано значение `overridePageViewDuration` и указан аргумент длительности в вызове `trackPageView()`, будет использовано значение аргумента.</span><span class="sxs-lookup"><span data-stu-id="5e720-214">If `overridePageViewDuration` is set and a duration argument is provided in the `trackPageView()` call, then the argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="5e720-215">Настраиваемые счетчики страниц</span><span class="sxs-lookup"><span data-stu-id="5e720-215">Custom page counts</span></span>
<span data-ttu-id="5e720-216">По умолчанию счетчик страницы увеличивается на единицу каждый раз, когда страница загружается в клиентском браузере.</span><span class="sxs-lookup"><span data-stu-id="5e720-216">By default, a page count occurs each time a new page loads into the client browser.</span></span>  <span data-ttu-id="5e720-217">Однако вам может потребоваться подсчитать дополнительные просмотры страницы.</span><span class="sxs-lookup"><span data-stu-id="5e720-217">But you might want to count additional page views.</span></span> <span data-ttu-id="5e720-218">Например, если содержимое страницы разбито на вкладки, возможно, вы захотите, чтобы счетчик увеличивался на единицу при каждом переключении между ними.</span><span class="sxs-lookup"><span data-stu-id="5e720-218">For example, a page might display its content in tabs and you want to count a page when the user switches tabs.</span></span> <span data-ttu-id="5e720-219">Другой пример — ситуация, когда код JavaScript на странице загружает новое содержимое, но URL-адрес в браузере при этом не меняется.</span><span class="sxs-lookup"><span data-stu-id="5e720-219">Or JavaScript code in the page might load new content without changing the browser's URL.</span></span>

<span data-ttu-id="5e720-220">Вставьте в соответствующем месте клиентского кода вызов JavaScript наподобие следующего:</span><span class="sxs-lookup"><span data-stu-id="5e720-220">Insert a JavaScript call like this at the appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="5e720-221">Имя страницы может содержать те же знаки, что и URL-адрес, но все знаки после "#" или "?" игнорируются.</span><span class="sxs-lookup"><span data-stu-id="5e720-221">The page name can contain the same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="5e720-222">Отслеживание использования</span><span class="sxs-lookup"><span data-stu-id="5e720-222">Usage tracking</span></span>
<span data-ttu-id="5e720-223">Хотите узнать, что пользователи делают в вашем приложении?</span><span class="sxs-lookup"><span data-stu-id="5e720-223">Want to find out what your users do with your app?</span></span>

* [<span data-ttu-id="5e720-224">Дополнительные сведения об отслеживании использования</span><span class="sxs-lookup"><span data-stu-id="5e720-224">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="5e720-225">[Дополнительные сведения об API пользовательских событий и метрик](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="5e720-225">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="5e720-226"><a name="video"></a> Видео</span><span class="sxs-lookup"><span data-stu-id="5e720-226"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="5e720-227"><a name="next"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e720-227"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="5e720-228">Отслеживание использования</span><span class="sxs-lookup"><span data-stu-id="5e720-228">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="5e720-229">Пользовательские события и метрики</span><span class="sxs-lookup"><span data-stu-id="5e720-229">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="5e720-230">Сборка, измерение и обучение</span><span class="sxs-lookup"><span data-stu-id="5e720-230">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

