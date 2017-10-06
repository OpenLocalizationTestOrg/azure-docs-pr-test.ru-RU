---
title: "aaaDependency отслеживания в Azure Application Insights | Документы Microsoft"
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
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="b4d2e-103">Настройка Application Insights: отслеживание зависимостей</span><span class="sxs-lookup"><span data-stu-id="b4d2e-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="b4d2e-104">*Зависимость* – это внешний компонент, который вызывается приложением.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="b4d2e-105">Как правило, это служба, вызываемая с использованием HTTP, база данных или файловая система.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="b4d2e-106">[Application Insights](app-insights-overview.md) измеряет время, в течение которого приложение ожидает зависимости, и определяет, как часто происходит сбой вызова зависимости.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="b4d2e-107">Проверка конкретных вызовов и связывать их toorequests и исключения.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-107">You can investigate specific calls, and relate them toorequests and exceptions.</span></span>

![примеры диаграмм](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="b4d2e-109">монитор зависимостей out of box Hello в настоящее время отображает типы toothese вызовы зависимостей:</span><span class="sxs-lookup"><span data-stu-id="b4d2e-109">hello out-of-the-box dependency monitor currently reports calls toothese  types of dependencies:</span></span>

* <span data-ttu-id="b4d2e-110">сервер;</span><span class="sxs-lookup"><span data-stu-id="b4d2e-110">Server</span></span>
  * <span data-ttu-id="b4d2e-111">базы данных SQL;</span><span class="sxs-lookup"><span data-stu-id="b4d2e-111">SQL databases</span></span>
  * <span data-ttu-id="b4d2e-112">веб-службы и службы WCF ASP.NET, использующие привязки на основе HTTP;</span><span class="sxs-lookup"><span data-stu-id="b4d2e-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="b4d2e-113">локальные или удаленные HTTP-вызовы;</span><span class="sxs-lookup"><span data-stu-id="b4d2e-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="b4d2e-114">Azure Cosmos DB, таблица, хранилище BLOB-объектов и очередь.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="b4d2e-115">Веб-страницы</span><span class="sxs-lookup"><span data-stu-id="b4d2e-115">Web pages</span></span>
  * <span data-ttu-id="b4d2e-116">Вызовы AJAX</span><span class="sxs-lookup"><span data-stu-id="b4d2e-116">AJAX calls</span></span>

<span data-ttu-id="b4d2e-117">Мониторинг работает с помощью [инструментирования байт-кода](https://msdn.microsoft.com/library/z9z62c29.aspx) вокруг выбранных методов.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="b4d2e-118">Снижение производительности при этом сводится к минимуму.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="b4d2e-119">Можно также написать собственную SDK вызывает toomonitor другие зависимости, как в коде клиента и сервера hello, с помощью hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="b4d2e-119">You can also write your own SDK calls toomonitor other dependencies, both in hello client and server code, using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="b4d2e-120">Настройка мониторинга зависимостей</span><span class="sxs-lookup"><span data-stu-id="b4d2e-120">Set up dependency monitoring</span></span>
<span data-ttu-id="b4d2e-121">Сведения о частичных зависимостей собираются автоматически hello [пакет SDK Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="b4d2e-121">Partial dependency information is collected automatically by hello [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="b4d2e-122">tooget полные данные, установить соответствующий агент hello для сервера узла hello.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-122">tooget complete data, install hello appropriate agent for hello host server.</span></span>

| <span data-ttu-id="b4d2e-123">Платформа</span><span class="sxs-lookup"><span data-stu-id="b4d2e-123">Platform</span></span> | <span data-ttu-id="b4d2e-124">Установить</span><span class="sxs-lookup"><span data-stu-id="b4d2e-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="b4d2e-125">Сервер IIS</span><span class="sxs-lookup"><span data-stu-id="b4d2e-125">IIS Server</span></span> |<span data-ttu-id="b4d2e-126">Либо [установите монитор состояния на сервере](app-insights-monitor-performance-live-website-now.md) или [обновление вашего приложения too.NET framework 4.6 или более поздней версии](http://go.microsoft.com/fwlink/?LinkId=528259) и установить hello [пакет SDK Application Insights](app-insights-asp-net.md) в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application too.NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install hello [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="b4d2e-127">Веб-приложение Azure</span><span class="sxs-lookup"><span data-stu-id="b4d2e-127">Azure Web App</span></span> |<span data-ttu-id="b4d2e-128">На панели управления приложения web [Привет открыть колонку Application Insights в панели управления web app](app-insights-azure-web-apps.md) и выберите "установить" при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-128">In your web app control panel, [open hello Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="b4d2e-129">Облачная служба Azure</span><span class="sxs-lookup"><span data-stu-id="b4d2e-129">Azure Cloud Service</span></span> |<span data-ttu-id="b4d2e-130">[Используйте задачу при запуске](app-insights-cloudservices.md) или [установите платформу .NET Framework 4.6 или более поздней версии](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b4d2e-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-toofind-dependency-data"></a><span data-ttu-id="b4d2e-131">Где toofind зависимостей данных</span><span class="sxs-lookup"><span data-stu-id="b4d2e-131">Where toofind dependency data</span></span>
* <span data-ttu-id="b4d2e-132">[Схема сопоставления приложений](#application-map) наглядно представляет зависимости между приложением и смежными компонентами.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="b4d2e-133">[Колонки "Производительность", "Браузер" и "Сбой"](#performance-and-blades) отображают данные зависимостей сервера.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="b4d2e-134">[Колонка "Браузеры"](#ajax-calls) содержит вызовы AJAX из браузеров ваших пользователей.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="b4d2e-135">[Пролистайте от медленно или неудачных запросов](#diagnose-slow-requests) toocheck вызывает их зависимостей.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-135">[Click through from slow or failed requests](#diagnose-slow-requests) toocheck their dependency calls.</span></span>
* <span data-ttu-id="b4d2e-136">[Аналитика](#analytics) можно указывать данные, используемые tooquery зависимостей.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-136">[Analytics](#analytics) can be used tooquery dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="b4d2e-137">Схема сопоставления приложений</span><span class="sxs-lookup"><span data-stu-id="b4d2e-137">Application Map</span></span>
<span data-ttu-id="b4d2e-138">Схема сопоставления приложений выступает в качестве зависимости toodiscovering наглядные пособия между компонентами приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-138">Application Map acts as a visual aid toodiscovering dependencies between hello components of your application.</span></span> <span data-ttu-id="b4d2e-139">Оно создается автоматически на основе hello телеметрии из приложения.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-139">It is automatically generated from hello telemetry from your app.</span></span> <span data-ttu-id="b4d2e-140">Этот пример вызовы AJAX с помощью обозревателя скриптов hello и вызовы REST с сервера hello приложения tootwo внешние службы.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-140">This example shows AJAX calls from hello browser scripts and REST calls from hello server app tootwo external services.</span></span>

![Схема сопоставления приложений](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="b4d2e-142">**Переход от поля hello** toorelevant зависимостей и других диаграмм.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-142">**Navigate from hello boxes** toorelevant dependency and other charts.</span></span>
* <span data-ttu-id="b4d2e-143">**ПИН-кода hello карты** toohello [мониторинга](app-insights-dashboards.md), где он будет полностью функционален.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-143">**Pin hello map** toohello [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="b4d2e-144">[Подробнее](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="b4d2e-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="b4d2e-145">Колонки "Производительность" и "Сбой"</span><span class="sxs-lookup"><span data-stu-id="b4d2e-145">Performance and failure blades</span></span>
<span data-ttu-id="b4d2e-146">Колонка Hello производительности показывает продолжительность hello вызовов зависимостей, приложение hello server.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-146">hello performance blade shows hello duration of dependency calls made by hello server app.</span></span> <span data-ttu-id="b4d2e-147">Она содержит сводную диаграмму и таблицу, разбитую по вызовам.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-147">There's a summary chart and a table segmented by call.</span></span>

![Диаграммы зависимостей в колонке "Производительность"](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="b4d2e-149">Пролистайте hello сводных диаграмм или hello таблицы элементов toosearch необработанные вхождения этих вызовов.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-149">Click through hello summary charts or hello table items toosearch raw occurrences of these calls.</span></span>

![Экземпляры вызовов зависимостей](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="b4d2e-151">**Количествами не пройденных** отображаются на hello **сбоев** колонку.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-151">**Failure counts** are shown on hello **Failures** blade.</span></span> <span data-ttu-id="b4d2e-152">Сбой является любой код возврата, не находится в диапазоне 200 hello-399, или unknown.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-152">A failure is any return code that is not in hello range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="b4d2e-153">**100% failures?** (100 % сбоев?)</span><span class="sxs-lookup"><span data-stu-id="b4d2e-153">**100% failures?**</span></span> <span data-ttu-id="b4d2e-154">— вероятно, означает, что вы получаете только неполные данные зависимостей.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="b4d2e-155">Требуется слишком[настроить соответствующие tooyour платформы наблюдения зависимостей](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="b4d2e-155">You need too[set up dependency monitoring appropriate tooyour platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="b4d2e-156">Вызовы AJAX</span><span class="sxs-lookup"><span data-stu-id="b4d2e-156">AJAX Calls</span></span>
<span data-ttu-id="b4d2e-157">Hello браузеры колонке показывает продолжительность hello и частота сбоев AJAX вызывает из [JavaScript на веб-страницах](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="b4d2e-157">hello Browsers blade shows hello duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="b4d2e-158">Они отображаются как зависимости.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="b4d2e-159"><a name="diagnosis"></a> Диагностика медленных запросов</span><span class="sxs-lookup"><span data-stu-id="b4d2e-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="b4d2e-160">Каждое событие запрос связан с вызовы зависимостей hello, исключения и другие события, которые отслеживаются во время обработки приложения hello запроса.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-160">Each request event is associated with hello dependency calls, exceptions and other events that are tracked while your app is processing hello request.</span></span> <span data-ttu-id="b4d2e-161">Поэтому если некоторые запросы выполняются плохо, можно выяснить, является ли из-за tooslow ответов от зависимости.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-161">So if some requests are performing badly, you can find out whether it's due tooslow responses from a dependency.</span></span>

<span data-ttu-id="b4d2e-162">Давайте подробно рассмотрим подобный пример.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-toodependencies"></a><span data-ttu-id="b4d2e-163">Трассировка из toodependencies запросов</span><span class="sxs-lookup"><span data-stu-id="b4d2e-163">Tracing from requests toodependencies</span></span>
<span data-ttu-id="b4d2e-164">Откройте колонку производительности hello и посмотрите на сетку hello запросов:</span><span class="sxs-lookup"><span data-stu-id="b4d2e-164">Open hello Performance blade, and look at hello grid of requests:</span></span>

![Список запросов со средними значениями и их количеством](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="b4d2e-166">Основные Hello один занимает очень много времени.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-166">hello top one is taking very long.</span></span> <span data-ttu-id="b4d2e-167">Давайте посмотрим, если мы можно выяснить расходуется время hello.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-167">Let's see if we can find out where hello time is spent.</span></span>

<span data-ttu-id="b4d2e-168">Щелкните отдельный запрос событий toosee строки:</span><span class="sxs-lookup"><span data-stu-id="b4d2e-168">Click that row toosee individual request events:</span></span>

![Список вхождений запросов](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="b4d2e-170">Щелкните любой экземпляр tooinspect долго выполняющихся его дальнейшее и прокрутите вниз запроса связанных toothis вызовы удаленных зависимостей toohello:</span><span class="sxs-lookup"><span data-stu-id="b4d2e-170">Click any long-running instance tooinspect it further, and scroll down toohello remote dependency calls related toothis request:</span></span>

![Найти зависимости tooRemote вызовы, определите необычные длительность](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="b4d2e-172">Он будет выглядеть большинство hello время обслуживания, этот запрос, затраченное на вызов tooa локальной службы.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-172">It looks like most of hello time servicing this request was spent in a call tooa local service.</span></span>

<span data-ttu-id="b4d2e-173">Выберите Дополнительные сведения, tooget строки:</span><span class="sxs-lookup"><span data-stu-id="b4d2e-173">Select that row tooget more information:</span></span>

![Пролистайте, причиной hello tooidentify удаленных зависимостей](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="b4d2e-175">Похоже, именно здесь находится hello проблему.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-175">Looks like this is where hello problem is.</span></span> <span data-ttu-id="b4d2e-176">Мы детальные hello проблемы, так что теперь мы просто нужно toofind, почему этот вызов занимает так много времени.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-176">We've pinpointed hello problem, so now we just need toofind out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="b4d2e-177">Временная шкала запроса</span><span class="sxs-lookup"><span data-stu-id="b4d2e-177">Request timeline</span></span>
<span data-ttu-id="b4d2e-178">В другом случае вызов зависимости не имеет большую длительность.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="b4d2e-179">Но путем переключения toohello представлении временной шкалы, можно увидеть место возникновения задержки hello в нашей внутренней обработки:</span><span class="sxs-lookup"><span data-stu-id="b4d2e-179">But by switching toohello timeline view, we can see where hello delay occurred in our internal processing:</span></span>

![Найти зависимости tooRemote вызовы, определите необычные длительность](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="b4d2e-181">Похоже, что toobe большой разрыв после первого вызова зависимостей hello, поэтому мы следует обратить внимание на наши toosee код причины, т. е.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-181">There seems toobe a big gap after hello first dependency call, so we should look at our code toosee why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="b4d2e-182">Выполните профилирование активного сайта</span><span class="sxs-lookup"><span data-stu-id="b4d2e-182">Profile your live site</span></span>

<span data-ttu-id="b4d2e-183">Не знаете, где временем hello? Hello [профилировщик Application Insights](app-insights-profiler.md) трассировки HTTP вызывает динамическую сайта tooyour и показано, какие функции в коде заняло hello наибольшее время.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-183">No idea where hello time goes? hello [Application Insights profiler](app-insights-profiler.md) traces HTTP calls tooyour live site and shows you which functions in your code took hello longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="b4d2e-184">Failed requests (Неудачные запросы)</span><span class="sxs-lookup"><span data-stu-id="b4d2e-184">Failed requests</span></span>
<span data-ttu-id="b4d2e-185">Невыполненные запросы также могут быть связаны с toodependencies вызовов со сбоем.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-185">Failed requests might also be associated with failed calls toodependencies.</span></span> <span data-ttu-id="b4d2e-186">Опять же возможна детализация tootrack hello проблемы.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-186">Again, we can click through tootrack down hello problem.</span></span>

![Щелкните диаграмму hello неудачных запросов](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="b4d2e-188">Пролистайте tooan вхождения невыполненных запросов и просмотрите его связанные события.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-188">Click through tooan occurrence of a failed request, and look at its associated events.</span></span>

![Выберите тип запроса, щелкните hello экземпляр tooget tooa другое представление Здравствуйте же экземпляр, нажмите кнопку tooget сведения об исключении.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="b4d2e-190">Аналитика</span><span class="sxs-lookup"><span data-stu-id="b4d2e-190">Analytics</span></span>
<span data-ttu-id="b4d2e-191">Вы можете отслеживать зависимостей в hello [языка запросов анализа журналов](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="b4d2e-191">You can track dependencies in hello [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="b4d2e-192">Ниже приведены некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-192">Here are some examples.</span></span>

* <span data-ttu-id="b4d2e-193">Поиск неудачно завершенных вызовов зависимостей:</span><span class="sxs-lookup"><span data-stu-id="b4d2e-193">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="b4d2e-194">Поиск вызовов AJAX:</span><span class="sxs-lookup"><span data-stu-id="b4d2e-194">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="b4d2e-195">Поиск вызовов зависимостей, связанных с запросами:</span><span class="sxs-lookup"><span data-stu-id="b4d2e-195">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="b4d2e-196">Поиск вызовов AJAX, связанных с представлениями страницы:</span><span class="sxs-lookup"><span data-stu-id="b4d2e-196">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="b4d2e-197">Пользовательское отслеживание зависимостей</span><span class="sxs-lookup"><span data-stu-id="b4d2e-197">Custom dependency tracking</span></span>
<span data-ttu-id="b4d2e-198">стандартный модуль Отслеживание зависимостей Hello автоматически обнаруживает внешние зависимости, такие как базы данных и API-интерфейсов REST.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-198">hello standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="b4d2e-199">Однако может потребоваться некоторые дополнительные компоненты toobe исчислялся hello таким же способом.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-199">But you might want some additional components toobe treated in hello same way.</span></span>

<span data-ttu-id="b4d2e-200">Можно написать код, который отправляет сведения о зависимостях, с помощью hello же [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) используются стандартные модули hello.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-200">You can write code that sends dependency information, using hello same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by hello standard modules.</span></span>

<span data-ttu-id="b4d2e-201">Например при создании кода со сборкой, не написанного пользователем, удалось времени всех tooit hello вызовов toofind out какие вклад делает ответ tooyour времени.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-201">For example, if you build your code with an assembly that you didn't write yourself, you could time all hello calls tooit, toofind out what contribution it makes tooyour response times.</span></span> <span data-ttu-id="b4d2e-202">Отправить эти данные отображаются в форме диаграммы зависимости hello Application Insights toohave его с помощью `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-202">toohave this data displayed in hello dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

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

<span data-ttu-id="b4d2e-203">Tooswitch выключить модуля отслеживания стандартных зависимостей hello, удалить tooDependencyTrackingTelemetryModule ссылка hello в [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="b4d2e-203">If you want tooswitch off hello standard dependency tracking module, remove hello reference tooDependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b4d2e-204">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="b4d2e-204">Troubleshooting</span></span>
<span data-ttu-id="b4d2e-205">*Флаг успешной зависимости всегда показывает значение true или false.*</span><span class="sxs-lookup"><span data-stu-id="b4d2e-205">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="b4d2e-206">*SQL-запрос отображается не полностью.*</span><span class="sxs-lookup"><span data-stu-id="b4d2e-206">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="b4d2e-207">Обновите toohello последнюю версию пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-207">Upgrade toohello latest version of hello SDK.</span></span> <span data-ttu-id="b4d2e-208">Если используемая версия .NET меньше 4.6:</span><span class="sxs-lookup"><span data-stu-id="b4d2e-208">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="b4d2e-209">Узла IIS: установите [агент аналитики приложений](app-insights-monitor-performance-live-website-now.md) на серверах узла hello.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-209">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on hello host servers.</span></span>
  * <span data-ttu-id="b4d2e-210">Веб-приложение Azure: Откройте Application Insights в панели управления hello web app, а установите Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b4d2e-210">Azure web app: Open Application Insights tab in hello web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="b4d2e-211">Видео</span><span class="sxs-lookup"><span data-stu-id="b4d2e-211">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="b4d2e-212">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b4d2e-212">Next steps</span></span>
* [<span data-ttu-id="b4d2e-213">Исключения</span><span class="sxs-lookup"><span data-stu-id="b4d2e-213">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="b4d2e-214">Данные пользователей и страниц</span><span class="sxs-lookup"><span data-stu-id="b4d2e-214">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="b4d2e-215">Доступность</span><span class="sxs-lookup"><span data-stu-id="b4d2e-215">Availability</span></span>](app-insights-monitor-web-app-availability.md)
