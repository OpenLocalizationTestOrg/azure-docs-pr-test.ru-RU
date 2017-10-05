---
title: "Отслеживание зависимостей в Azure Application Insights | Документация Майкрософт"
description: "Анализ использования, доступности и производительности локального приложения или веб-приложения Microsoft Azure с помощью Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 6e0b67ba98af27017901608dde4401600eb9957f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="e01b8-103">Настройка Application Insights: отслеживание зависимостей</span><span class="sxs-lookup"><span data-stu-id="e01b8-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="e01b8-104">*Зависимость* – это внешний компонент, который вызывается приложением.</span><span class="sxs-lookup"><span data-stu-id="e01b8-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="e01b8-105">Как правило, это служба, вызываемая с использованием HTTP, база данных или файловая система.</span><span class="sxs-lookup"><span data-stu-id="e01b8-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="e01b8-106">[Application Insights](app-insights-overview.md) измеряет время, в течение которого приложение ожидает зависимости, и определяет, как часто происходит сбой вызова зависимости.</span><span class="sxs-lookup"><span data-stu-id="e01b8-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="e01b8-107">Можно изучить определенные вызовы и установить их взаимосвязь с теми или иными запросами и исключениями.</span><span class="sxs-lookup"><span data-stu-id="e01b8-107">You can investigate specific calls, and relate them to requests and exceptions.</span></span>

![примеры диаграмм](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="e01b8-109">Сейчас монитор зависимостей по умолчанию предоставляет отчеты о вызовах зависимостей таких типов:</span><span class="sxs-lookup"><span data-stu-id="e01b8-109">The out-of-the-box dependency monitor currently reports calls to these  types of dependencies:</span></span>

* <span data-ttu-id="e01b8-110">сервер;</span><span class="sxs-lookup"><span data-stu-id="e01b8-110">Server</span></span>
  * <span data-ttu-id="e01b8-111">базы данных SQL;</span><span class="sxs-lookup"><span data-stu-id="e01b8-111">SQL databases</span></span>
  * <span data-ttu-id="e01b8-112">веб-службы и службы WCF ASP.NET, использующие привязки на основе HTTP;</span><span class="sxs-lookup"><span data-stu-id="e01b8-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="e01b8-113">локальные или удаленные HTTP-вызовы;</span><span class="sxs-lookup"><span data-stu-id="e01b8-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="e01b8-114">Azure Cosmos DB, таблица, хранилище BLOB-объектов и очередь.</span><span class="sxs-lookup"><span data-stu-id="e01b8-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="e01b8-115">Веб-страницы</span><span class="sxs-lookup"><span data-stu-id="e01b8-115">Web pages</span></span>
  * <span data-ttu-id="e01b8-116">Вызовы AJAX</span><span class="sxs-lookup"><span data-stu-id="e01b8-116">AJAX calls</span></span>

<span data-ttu-id="e01b8-117">Мониторинг работает с помощью [инструментирования байт-кода](https://msdn.microsoft.com/library/z9z62c29.aspx) вокруг выбранных методов.</span><span class="sxs-lookup"><span data-stu-id="e01b8-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="e01b8-118">Снижение производительности при этом сводится к минимуму.</span><span class="sxs-lookup"><span data-stu-id="e01b8-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="e01b8-119">Можно также написать собственные вызовы пакета SDK для мониторинга других зависимостей (в клиентском и серверном коде) с помощью [API TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="e01b8-119">You can also write your own SDK calls to monitor other dependencies, both in the client and server code, using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="e01b8-120">Настройка мониторинга зависимостей</span><span class="sxs-lookup"><span data-stu-id="e01b8-120">Set up dependency monitoring</span></span>
<span data-ttu-id="e01b8-121">Неполные сведения о зависимостях собираются автоматически [пакетом SDK для Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="e01b8-121">Partial dependency information is collected automatically by the [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="e01b8-122">Чтобы получить полные данные, установите соответствующий агент для сервера узла.</span><span class="sxs-lookup"><span data-stu-id="e01b8-122">To get complete data, install the appropriate agent for the host server.</span></span>

| <span data-ttu-id="e01b8-123">платформа</span><span class="sxs-lookup"><span data-stu-id="e01b8-123">Platform</span></span> | <span data-ttu-id="e01b8-124">Установить</span><span class="sxs-lookup"><span data-stu-id="e01b8-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="e01b8-125">Сервер IIS</span><span class="sxs-lookup"><span data-stu-id="e01b8-125">IIS Server</span></span> |<span data-ttu-id="e01b8-126">[Установите монитор состояний на сервере](app-insights-monitor-performance-live-website-now.md) или [обновите свое приложение до .NET Framework 4.6 или более поздней версии](http://go.microsoft.com/fwlink/?LinkId=528259) и установите в нем [пакет SDK для Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="e01b8-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application to .NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install the [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="e01b8-127">Веб-приложение Azure</span><span class="sxs-lookup"><span data-stu-id="e01b8-127">Azure Web App</span></span> |<span data-ttu-id="e01b8-128">На панели управления веб-приложения [откройте колонку "Application Insights"](app-insights-azure-web-apps.md) и при появлении соответствующего запроса выберите "Установить".</span><span class="sxs-lookup"><span data-stu-id="e01b8-128">In your web app control panel, [open the Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="e01b8-129">Облачная служба Azure</span><span class="sxs-lookup"><span data-stu-id="e01b8-129">Azure Cloud Service</span></span> |<span data-ttu-id="e01b8-130">[Используйте задачу при запуске](app-insights-cloudservices.md) или [установите платформу .NET Framework 4.6 или более поздней версии](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e01b8-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-to-find-dependency-data"></a><span data-ttu-id="e01b8-131">Где найти данные зависимостей</span><span class="sxs-lookup"><span data-stu-id="e01b8-131">Where to find dependency data</span></span>
* <span data-ttu-id="e01b8-132">[Схема сопоставления приложений](#application-map) наглядно представляет зависимости между приложением и смежными компонентами.</span><span class="sxs-lookup"><span data-stu-id="e01b8-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="e01b8-133">[Колонки "Производительность", "Браузер" и "Сбой"](#performance-and-blades) отображают данные зависимостей сервера.</span><span class="sxs-lookup"><span data-stu-id="e01b8-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="e01b8-134">[Колонка "Браузеры"](#ajax-calls) содержит вызовы AJAX из браузеров ваших пользователей.</span><span class="sxs-lookup"><span data-stu-id="e01b8-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="e01b8-135">[Щелкните по очереди медленные или неудачно завершенные запросы](#diagnose-slow-requests), чтобы проверить из вызовы зависимостей.</span><span class="sxs-lookup"><span data-stu-id="e01b8-135">[Click through from slow or failed requests](#diagnose-slow-requests) to check their dependency calls.</span></span>
* <span data-ttu-id="e01b8-136">[Аналитику](#analytics) можно использовать для запроса данных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="e01b8-136">[Analytics](#analytics) can be used to query dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="e01b8-137">Схема сопоставления приложений</span><span class="sxs-lookup"><span data-stu-id="e01b8-137">Application Map</span></span>
<span data-ttu-id="e01b8-138">Схема сопоставления приложений — это визуальное средство, которое позволяет обнаруживать зависимости между компонентами приложения.</span><span class="sxs-lookup"><span data-stu-id="e01b8-138">Application Map acts as a visual aid to discovering dependencies between the components of your application.</span></span> <span data-ttu-id="e01b8-139">Она создается автоматически на основе данных телеметрии из приложения.</span><span class="sxs-lookup"><span data-stu-id="e01b8-139">It is automatically generated from the telemetry from your app.</span></span> <span data-ttu-id="e01b8-140">В этом примере показаны вызовы AJAX из сценариев браузера и вызовы REST из серверного приложения к двум внешним службам.</span><span class="sxs-lookup"><span data-stu-id="e01b8-140">This example shows AJAX calls from the browser scripts and REST calls from the server app to two external services.</span></span>

![Схема сопоставления приложений](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="e01b8-142">**Из полей перейдите** к соответствующей зависимости и другим диаграммам.</span><span class="sxs-lookup"><span data-stu-id="e01b8-142">**Navigate from the boxes** to relevant dependency and other charts.</span></span>
* <span data-ttu-id="e01b8-143">**Закрепите схему сопоставления** на [панели мониторинга](app-insights-dashboards.md), где она будет полностью функциональной.</span><span class="sxs-lookup"><span data-stu-id="e01b8-143">**Pin the map** to the [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="e01b8-144">[Подробнее](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="e01b8-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="e01b8-145">Колонки "Производительность" и "Сбой"</span><span class="sxs-lookup"><span data-stu-id="e01b8-145">Performance and failure blades</span></span>
<span data-ttu-id="e01b8-146">В колонке "Производительность" отображается длительность вызовов зависимостей, выполненных серверным приложением.</span><span class="sxs-lookup"><span data-stu-id="e01b8-146">The performance blade shows the duration of dependency calls made by the server app.</span></span> <span data-ttu-id="e01b8-147">Она содержит сводную диаграмму и таблицу, разбитую по вызовам.</span><span class="sxs-lookup"><span data-stu-id="e01b8-147">There's a summary chart and a table segmented by call.</span></span>

![Диаграммы зависимостей в колонке "Производительность"](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="e01b8-149">По очереди щелкните сводные диаграммы или элементы таблицы, чтобы найти необработанные экземпляры этих вызовов.</span><span class="sxs-lookup"><span data-stu-id="e01b8-149">Click through the summary charts or the table items to search raw occurrences of these calls.</span></span>

![Экземпляры вызовов зависимостей](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="e01b8-151">В колонке **Сбой** отображены **количества сбоев**.</span><span class="sxs-lookup"><span data-stu-id="e01b8-151">**Failure counts** are shown on the **Failures** blade.</span></span> <span data-ttu-id="e01b8-152">Сбоем является любой код возврата, который не попадает в диапазон 200–399 либо неизвестен.</span><span class="sxs-lookup"><span data-stu-id="e01b8-152">A failure is any return code that is not in the range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="e01b8-153">**100% failures?** (100 % сбоев?)</span><span class="sxs-lookup"><span data-stu-id="e01b8-153">**100% failures?**</span></span> <span data-ttu-id="e01b8-154">— вероятно, означает, что вы получаете только неполные данные зависимостей.</span><span class="sxs-lookup"><span data-stu-id="e01b8-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="e01b8-155">Необходимо [настроить мониторинг зависимостей в соответствии со своей платформой](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="e01b8-155">You need to [set up dependency monitoring appropriate to your platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="e01b8-156">Вызовы AJAX</span><span class="sxs-lookup"><span data-stu-id="e01b8-156">AJAX Calls</span></span>
<span data-ttu-id="e01b8-157">Колонка "Браузеры" отображает длительность и частоту сбоев вызовов AJAX из [JavaScript на веб-страницах](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="e01b8-157">The Browsers blade shows the duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="e01b8-158">Они отображаются как зависимости.</span><span class="sxs-lookup"><span data-stu-id="e01b8-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="e01b8-159"><a name="diagnosis"></a> Диагностика медленных запросов</span><span class="sxs-lookup"><span data-stu-id="e01b8-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="e01b8-160">Каждое событие запроса связано с вызовами зависимостей, исключениями и другими событиями, которые отслеживаются во время обработки запроса вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="e01b8-160">Each request event is associated with the dependency calls, exceptions and other events that are tracked while your app is processing the request.</span></span> <span data-ttu-id="e01b8-161">Поэтому, если какие-либо запросы завершаются неудачно, можно узнать, не является ли причиной этого медленный отклик зависимости.</span><span class="sxs-lookup"><span data-stu-id="e01b8-161">So if some requests are performing badly, you can find out whether it's due to slow responses from a dependency.</span></span>

<span data-ttu-id="e01b8-162">Давайте подробно рассмотрим подобный пример.</span><span class="sxs-lookup"><span data-stu-id="e01b8-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-to-dependencies"></a><span data-ttu-id="e01b8-163">Трассировка от запросов до зависимостей</span><span class="sxs-lookup"><span data-stu-id="e01b8-163">Tracing from requests to dependencies</span></span>
<span data-ttu-id="e01b8-164">Откройте колонку "Производительность" и посмотрите на сетку запросов.</span><span class="sxs-lookup"><span data-stu-id="e01b8-164">Open the Performance blade, and look at the grid of requests:</span></span>

![Список запросов со средними значениями и их количеством](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="e01b8-166">Получение ответа на верхний запрос заняло слишком много времени.</span><span class="sxs-lookup"><span data-stu-id="e01b8-166">The top one is taking very long.</span></span> <span data-ttu-id="e01b8-167">Стоит попытаться выяснить, на что потрачено время.</span><span class="sxs-lookup"><span data-stu-id="e01b8-167">Let's see if we can find out where the time is spent.</span></span>

<span data-ttu-id="e01b8-168">Щелкните эту строку, чтобы просмотреть события для отдельного запроса.</span><span class="sxs-lookup"><span data-stu-id="e01b8-168">Click that row to see individual request events:</span></span>

![Список вхождений запросов](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="e01b8-170">Щелкните любой длительный экземпляр, чтобы проверить его более детально, и прокрутите вниз до удаленных вызовов зависимостей, связанных с этим запросом.</span><span class="sxs-lookup"><span data-stu-id="e01b8-170">Click any long-running instance to inspect it further, and scroll down to the remote dependency calls related to this request:</span></span>

![Найдите вызовы удаленных зависимостей и определите необычную продолжительность.](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="e01b8-172">По-видимому, большую часть времени обработки этого запроса занял вызов локальной службы.</span><span class="sxs-lookup"><span data-stu-id="e01b8-172">It looks like most of the time servicing this request was spent in a call to a local service.</span></span>

<span data-ttu-id="e01b8-173">Выберите эту строку, чтобы получить дополнительную информацию.</span><span class="sxs-lookup"><span data-stu-id="e01b8-173">Select that row to get more information:</span></span>

![Щелкните эту удаленную зависимость, чтобы определить причину.](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="e01b8-175">Похоже, проблема именно в этом.</span><span class="sxs-lookup"><span data-stu-id="e01b8-175">Looks like this is where the problem is.</span></span> <span data-ttu-id="e01b8-176">Мы выявили проблему, так что теперь осталось выяснить, почему этот вызов занимает так много времени.</span><span class="sxs-lookup"><span data-stu-id="e01b8-176">We've pinpointed the problem, so now we just need to find out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="e01b8-177">Временная шкала запроса</span><span class="sxs-lookup"><span data-stu-id="e01b8-177">Request timeline</span></span>
<span data-ttu-id="e01b8-178">В другом случае вызов зависимости не имеет большую длительность.</span><span class="sxs-lookup"><span data-stu-id="e01b8-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="e01b8-179">Но, переключившись на представление временной шкалы, мы видим, где произошла задержка во время внутренней обработки.</span><span class="sxs-lookup"><span data-stu-id="e01b8-179">But by switching to the timeline view, we can see where the delay occurred in our internal processing:</span></span>

![Найдите вызовы удаленных зависимостей и определите необычную продолжительность.](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="e01b8-181">Похоже, большая задержка имела место после первого вызова зависимости, так что следует изучить наш код, чтобы узнать, почему это произошло.</span><span class="sxs-lookup"><span data-stu-id="e01b8-181">There seems to be a big gap after the first dependency call, so we should look at our code to see why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="e01b8-182">Выполните профилирование активного сайта</span><span class="sxs-lookup"><span data-stu-id="e01b8-182">Profile your live site</span></span>

<span data-ttu-id="e01b8-183">Не имеете представления, куда девается время?</span><span class="sxs-lookup"><span data-stu-id="e01b8-183">No idea where the time goes?</span></span> <span data-ttu-id="e01b8-184">[Профилировщик Application Insights](app-insights-profiler.md) отслеживает вызовы HTTP к активному веб-сайту и показывает, какие функции в коде выполнялись дольше всего.</span><span class="sxs-lookup"><span data-stu-id="e01b8-184">The [Application Insights profiler](app-insights-profiler.md) traces HTTP calls to your live site and shows you which functions in your code took the longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="e01b8-185">Failed requests (Неудачные запросы)</span><span class="sxs-lookup"><span data-stu-id="e01b8-185">Failed requests</span></span>
<span data-ttu-id="e01b8-186">Неудачно завершенные запросы также могут быть связаны с неудачными вызовами зависимостей.</span><span class="sxs-lookup"><span data-stu-id="e01b8-186">Failed requests might also be associated with failed calls to dependencies.</span></span> <span data-ttu-id="e01b8-187">Опять же, мы можем определить причину проблемы.</span><span class="sxs-lookup"><span data-stu-id="e01b8-187">Again, we can click through to track down the problem.</span></span>

![Щелкните диаграмму неудачных запросов.](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="e01b8-189">Щелкните экземпляр неудачно завершенного запроса и просмотрите связанные с ним события.</span><span class="sxs-lookup"><span data-stu-id="e01b8-189">Click through to an occurrence of a failed request, and look at its associated events.</span></span>

![Щелкните тип запроса, а затем его экземпляр, чтобы открыть этот же экземпляр в другом представлении. Щелкните его еще раз, чтобы просмотреть подробную информацию об исключении.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="e01b8-191">Аналитика</span><span class="sxs-lookup"><span data-stu-id="e01b8-191">Analytics</span></span>
<span data-ttu-id="e01b8-192">Вы можете отслеживать зависимости, используя [язык запросов Log Analytics](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="e01b8-192">You can track dependencies in the [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="e01b8-193">Ниже приведены некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="e01b8-193">Here are some examples.</span></span>

* <span data-ttu-id="e01b8-194">Поиск неудачно завершенных вызовов зависимостей:</span><span class="sxs-lookup"><span data-stu-id="e01b8-194">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="e01b8-195">Поиск вызовов AJAX:</span><span class="sxs-lookup"><span data-stu-id="e01b8-195">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="e01b8-196">Поиск вызовов зависимостей, связанных с запросами:</span><span class="sxs-lookup"><span data-stu-id="e01b8-196">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="e01b8-197">Поиск вызовов AJAX, связанных с представлениями страницы:</span><span class="sxs-lookup"><span data-stu-id="e01b8-197">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="e01b8-198">Пользовательское отслеживание зависимостей</span><span class="sxs-lookup"><span data-stu-id="e01b8-198">Custom dependency tracking</span></span>
<span data-ttu-id="e01b8-199">Стандартный модуль отслеживания зависимостей выявляет внешние зависимости, например базы данных и API REST, автоматически.</span><span class="sxs-lookup"><span data-stu-id="e01b8-199">The standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="e01b8-200">Однако при необходимости аналогичную обработку можно настроить и для других компонентов.</span><span class="sxs-lookup"><span data-stu-id="e01b8-200">But you might want some additional components to be treated in the same way.</span></span>

<span data-ttu-id="e01b8-201">Код, который отправляет сведения о зависимостях, можно написать с использованием того же интерфейса [API TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency) , что используется в стандартных модулях.</span><span class="sxs-lookup"><span data-stu-id="e01b8-201">You can write code that sends dependency information, using the same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by the standard modules.</span></span>

<span data-ttu-id="e01b8-202">Например, формируя код на основе готовой сборки, можно назначить время для всех вызовов этого кода и таким образом выяснить, как он влияет на время отклика вашей системы.</span><span class="sxs-lookup"><span data-stu-id="e01b8-202">For example, if you build your code with an assembly that you didn't write yourself, you could time all the calls to it, to find out what contribution it makes to your response times.</span></span> <span data-ttu-id="e01b8-203">Чтобы эти данные отображались в диаграммах зависимостей в Application Insights, используйте для их отправки командлет `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="e01b8-203">To have this data displayed in the dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

```C#

            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

<span data-ttu-id="e01b8-204">Чтобы отключить стандартный модуль отслеживания зависимостей, удалите ссылку на DependencyTrackingTelemetryModule в файле [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="e01b8-204">If you want to switch off the standard dependency tracking module, remove the reference to DependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e01b8-205">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="e01b8-205">Troubleshooting</span></span>
<span data-ttu-id="e01b8-206">*Флаг успешной зависимости всегда показывает значение true или false.*</span><span class="sxs-lookup"><span data-stu-id="e01b8-206">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="e01b8-207">*SQL-запрос отображается не полностью.*</span><span class="sxs-lookup"><span data-stu-id="e01b8-207">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="e01b8-208">Обновите пакет SDK до последней версии.</span><span class="sxs-lookup"><span data-stu-id="e01b8-208">Upgrade to the latest version of the SDK.</span></span> <span data-ttu-id="e01b8-209">Если используемая версия .NET меньше 4.6:</span><span class="sxs-lookup"><span data-stu-id="e01b8-209">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="e01b8-210">Узел IIS: установите [агент Application Insights](app-insights-monitor-performance-live-website-now.md) на серверах узлов.</span><span class="sxs-lookup"><span data-stu-id="e01b8-210">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on the host servers.</span></span>
  * <span data-ttu-id="e01b8-211">Веб-приложение Azure: откройте вкладку "Application Insights" на панели управления веб-приложения и установите Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e01b8-211">Azure web app: Open Application Insights tab in the web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="e01b8-212">Видео</span><span class="sxs-lookup"><span data-stu-id="e01b8-212">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="e01b8-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e01b8-213">Next steps</span></span>
* [<span data-ttu-id="e01b8-214">Исключения</span><span class="sxs-lookup"><span data-stu-id="e01b8-214">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="e01b8-215">Данные пользователей и страниц</span><span class="sxs-lookup"><span data-stu-id="e01b8-215">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="e01b8-216">Доступность</span><span class="sxs-lookup"><span data-stu-id="e01b8-216">Availability</span></span>](app-insights-monitor-web-app-availability.md)
