---
title: "aaaApplication карты в Azure Application Insights | Документы Microsoft"
description: "Визуальное представление hello зависимостей между компонентами приложения с меткой оповещения и ключевые показатели эффективности."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="2d9d3-103">Схема сопоставления приложений в Application Insights</span><span class="sxs-lookup"><span data-stu-id="2d9d3-103">Application Map in Application Insights</span></span>
<span data-ttu-id="2d9d3-104">В [Azure Application Insights](app-insights-overview.md), карта приложения — это визуальное расположение hello отношения зависимости компонентов приложения.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of hello dependency relationships of your application components.</span></span> <span data-ttu-id="2d9d3-105">Каждый компонент показаны ключевые показатели эффективности например toohelp загрузки, производительности, ошибок и предупреждений, обнаружение любой компонент вызывает проблемы с производительностью или сбоя.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-105">Each component shows KPIs such as load, performance, failures, and alerts, toohelp you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="2d9d3-106">Можно щелкнуть из любого компонента toomore подробные диагностики, таких как события Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-106">You can click through from any component toomore detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="2d9d3-107">Если приложение использует службы Azure, можно также щелкнуть по диагностике tooAzure, например рекомендаций помощник по настройке ядра базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-107">If your app uses Azure services, you can also click through tooAzure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="2d9d3-108">Как и другие диаграммы можно закрепить toohello карты приложения Azure панели мониторинга, где будут обладать полной функциональностью.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-108">Like other charts, you can pin an application map toohello Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-hello-application-map"></a><span data-ttu-id="2d9d3-109">Привет открыть приложение карты</span><span class="sxs-lookup"><span data-stu-id="2d9d3-109">Open hello application map</span></span>
<span data-ttu-id="2d9d3-110">Откройте hello карты из колонки Обзор hello для приложения:</span><span class="sxs-lookup"><span data-stu-id="2d9d3-110">Open hello map from hello overview blade for your application:</span></span>

![Открытие схемы сопоставления приложений](./media/app-insights-app-map/01.png)

![Схема сопоставления приложений](./media/app-insights-app-map/02.png)

<span data-ttu-id="2d9d3-113">Hello карте показаны.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-113">hello map shows:</span></span>

* <span data-ttu-id="2d9d3-114">Тесты доступности</span><span class="sxs-lookup"><span data-stu-id="2d9d3-114">Availability tests</span></span>
* <span data-ttu-id="2d9d3-115">Клиентский компонент (просматривается с hello JavaScript SDK)</span><span class="sxs-lookup"><span data-stu-id="2d9d3-115">Client-side component (monitored with hello JavaScript SDK)</span></span>
* <span data-ttu-id="2d9d3-116">компонент на стороне сервера;</span><span class="sxs-lookup"><span data-stu-id="2d9d3-116">Server-side component</span></span>
* <span data-ttu-id="2d9d3-117">Зависимости hello клиентские и серверные компоненты</span><span class="sxs-lookup"><span data-stu-id="2d9d3-117">Dependencies of hello client and server components</span></span>

<span data-ttu-id="2d9d3-118">Можно разворачивать и сворачивать группы ссылок зависимостей:</span><span class="sxs-lookup"><span data-stu-id="2d9d3-118">You can expand and collapse dependency link groups:</span></span>

![Свертывание](./media/app-insights-app-map/03.png)

<span data-ttu-id="2d9d3-120">Если есть большое количество однотипных зависимостей (например, SQL, HTTP и пр.), они могут группироваться.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![Сгруппированные зависимости](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="2d9d3-122">Выявление проблем</span><span class="sxs-lookup"><span data-stu-id="2d9d3-122">Spot problems</span></span>
<span data-ttu-id="2d9d3-123">Каждый узел имеет соответствующие производительности показатели, такие как hello скорости загрузки, производительности и сбоя для этого компонента.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-123">Each node has relevant performance indicators, such as hello load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="2d9d3-124">Предупреждающие значки указывают на возможные проблемы.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="2d9d3-125">Оранжевое предупреждение означает сбои в запросах, представлении страниц или вызовах зависимостей.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="2d9d3-126">Красное предупреждение указывает на риск сбоя с вероятностью более 5 %.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="2d9d3-127">Если вы хотите tooadjust эти пороговые значения, откройте параметры.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-127">If you want tooadjust these thresholds, open Options.</span></span>

![Значки, указывающие на сбои](./media/app-insights-app-map/04.png)

<span data-ttu-id="2d9d3-129">Тут же отображаются активные оповещения:</span><span class="sxs-lookup"><span data-stu-id="2d9d3-129">Active alerts also show up:</span></span> 

![Активные оповещения](./media/app-insights-app-map/05.png)

<span data-ttu-id="2d9d3-131">При использовании SQL Azure вы увидите соответствующий значок, информирующий о наличии рекомендаций по улучшению производительности.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Рекомендации Azure](./media/app-insights-app-map/06.png)

<span data-ttu-id="2d9d3-133">Щелкните любой значок tooget Дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="2d9d3-133">Click any icon tooget more details:</span></span>

![Рекомендации Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="2d9d3-135">Просмотр данных диагностики</span><span class="sxs-lookup"><span data-stu-id="2d9d3-135">Diagnostic click through</span></span>
<span data-ttu-id="2d9d3-136">Каждый из узлов hello на карте hello предлагает целевой Повтор дополнительной информации для диагностики.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-136">Each of hello nodes on hello map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="2d9d3-137">Hello параметры зависят от типа hello hello узла.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-137">hello options vary depending on hello type of hello node.</span></span>

![Параметры сервера](./media/app-insights-app-map/09.png)

<span data-ttu-id="2d9d3-139">Для компонентов, которые размещены в Azure hello варианты toothem прямых ссылок.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-139">For components that are hosted in Azure, hello options include direct links toothem.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="2d9d3-140">Фильтры и диапазон времени</span><span class="sxs-lookup"><span data-stu-id="2d9d3-140">Filters and time range</span></span>
<span data-ttu-id="2d9d3-141">По умолчанию hello карты перечислены все доступные для выбранного диапазона времени hello данные hello.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-141">By default, hello map summarizes all hello data available for hello chosen time range.</span></span> <span data-ttu-id="2d9d3-142">Но можно использовать имена tooinclude только определенной операции или зависимости.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-142">But you can filter it tooinclude only specific operation names or dependencies.</span></span>

* <span data-ttu-id="2d9d3-143">Имя операции: сюда входят запросы просмотров страниц и запросы сервера.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="2d9d3-144">Этот параметр показывает карты hello hello ключевого показателя Эффективности на узле стороне сервера или клиента hello hello выбран только для операций.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-144">With this option, hello map shows hello KPI on hello server/client-side node for hello selected operations only.</span></span> <span data-ttu-id="2d9d3-145">Он показывает зависимости hello, вызывается в контексте hello этих конкретных операций.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-145">It shows hello dependencies called in hello context of those specific operations.</span></span>
* <span data-ttu-id="2d9d3-146">Базовое имя зависимостей: hello AJAX браузера зависимости и зависимости на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-146">Dependency base name: This includes hello AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="2d9d3-147">Если вы сообщаете телеметрии пользовательскую зависимость с hello TrackDependency API, они также отображаются здесь.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-147">If you report custom dependency telemetry with hello TrackDependency API, they also appear here.</span></span> <span data-ttu-id="2d9d3-148">Вы можете выбрать tooshow hello зависимости на карте hello.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-148">You can select hello dependencies tooshow on hello map.</span></span> <span data-ttu-id="2d9d3-149">В настоящее время этот выбор фильтрует hello серверных запросов или представлений hello страницы на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-149">Currently this selection does not filter hello server-side requests, or hello client-side page views.</span></span>

![Настройка фильтров](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="2d9d3-151">Сохранение фильтров</span><span class="sxs-lookup"><span data-stu-id="2d9d3-151">Save filters</span></span>
<span data-ttu-id="2d9d3-152">Примененные фильтры hello toosave ПИН-кода hello отфильтрованное представление на [мониторинга](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="2d9d3-152">toosave hello filters you have applied, pin hello filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Toodashboard ПИН-кода](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="2d9d3-154">Область ошибок</span><span class="sxs-lookup"><span data-stu-id="2d9d3-154">Error pane</span></span>
<span data-ttu-id="2d9d3-155">Если щелкнуть узел в карте hello, ошибка панель отображается правой стороны hello суммирования сбоев для этого узла.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-155">When you click a node in hello map, an error pane is displayed on hello right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="2d9d3-156">Сбои группируются сначала по идентификатору операции, затем — по идентификатору проблемы.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Область ошибок](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="2d9d3-158">Щелкнув сбоя принимает экземпляра последним toohello об этой ошибке.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-158">Clicking on a failure takes you toohello most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="2d9d3-159">Работоспособность ресурса</span><span class="sxs-lookup"><span data-stu-id="2d9d3-159">Resource health</span></span>
<span data-ttu-id="2d9d3-160">Для некоторых типов ресурсов исправности ресурсов отображается в верхней hello hello Ошибка области.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-160">For some resource types, resource health is displayed at hello top of hello error pane.</span></span> <span data-ttu-id="2d9d3-161">Например при щелчке узла SQL покажет hello работоспособности базы данных и все оповещения, которые сработавшими триггерами.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-161">For example, clicking a SQL node will show hello database health and any alerts that have fired.</span></span>

![Работоспособность ресурса](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="2d9d3-163">Можно щелкнуть hello метрики ресурсов имя tooview стандартные общие сведения для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-163">You can click hello resource name tooview standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="2d9d3-164">Комплексная схема сопоставления приложений системы</span><span class="sxs-lookup"><span data-stu-id="2d9d3-164">End-to-end system app maps</span></span>

<span data-ttu-id="2d9d3-165">*Требуется пакет SDK версии 2.3 или выше.*</span><span class="sxs-lookup"><span data-stu-id="2d9d3-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="2d9d3-166">Если приложение имеет несколько компонентов - например, внутренняя служба Кроме toohello веб-приложения — то можно показать их все на один интегрированного приложения карты.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-166">If your application has several components - for example, a back-end service in addition toohello web app - then you can show them all on one integrated app map.</span></span>

![Настройка фильтров](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="2d9d3-168">карта приложения Hello выполняется поиск узлов сервера, выполнив любой HTTP-обращениях зависимостей между серверами с hello установлен пакет SDK для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-168">hello app map finds server nodes by following any HTTP dependency calls made between servers with hello Application Insights SDK installed.</span></span> <span data-ttu-id="2d9d3-169">Каждый ресурс Application Insights предполагается, что toocontain одного сервера.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-169">Each Application Insights resource is assumed toocontain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="2d9d3-170">Карта приложений с несколькими ролями (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="2d9d3-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="2d9d3-171">Hello Предварительный просмотр приложения с несколькими ролями карты позволяет вам карты приложения hello toouse с несколькими серверами, отправка данных toohello того же ресурса Application Insights и ключ инструментирования.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-171">hello preview multi-role app map feature allows you toouse hello app map with multiple servers sending data toohello same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="2d9d3-172">Серверы в карте hello разделены свойством cloud_RoleName hello элементов телеметрии.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-172">Servers in hello map are segmented by hello cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="2d9d3-173">Задать *карты несколькими ролями приложения* слишком*на* из hello tooenable колонке предварительные версии этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-173">Set *Multi-role Application Map* too*On* from hello Previews blade tooenable this configuration.</span></span>

<span data-ttu-id="2d9d3-174">Этот подход может оказаться целесообразным в приложении службы micro или в других сценариях, где искомые события toocorrelate на нескольких серверах в пределах одного ресурса Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-174">This approach may be desired in a micro-services application, or in other scenarios where you want toocorrelate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="2d9d3-175">Видео</span><span class="sxs-lookup"><span data-stu-id="2d9d3-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="2d9d3-176">Отзыв</span><span class="sxs-lookup"><span data-stu-id="2d9d3-176">Feedback</span></span>
<span data-ttu-id="2d9d3-177">Оставьте отзыв через параметр портала отзыва hello.</span><span class="sxs-lookup"><span data-stu-id="2d9d3-177">Please provide feedback through hello portal feedback option.</span></span>

![Изображение MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="2d9d3-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2d9d3-179">Next steps</span></span>

* [<span data-ttu-id="2d9d3-180">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="2d9d3-180">Azure portal</span></span>](https://portal.azure.com)
