---
title: "Панели мониторинга и навигация в Azure Application Insights | Документация Майкрософт"
description: "Создание представлений ключевых диаграмм и запросов APM."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9987f04e7e71df5fe10c8bc209a390cb940ec4f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="navigation-and-dashboards-in-the-application-insights-portal"></a><span data-ttu-id="20b8d-103">Навигация и панели мониторинга на портале Application Insights</span><span class="sxs-lookup"><span data-stu-id="20b8d-103">Navigation and Dashboards in the Application Insights portal</span></span>
<span data-ttu-id="20b8d-104">После [настройки Application Insights для проекта](app-insights-overview.md) данные телеметрии о производительности и использовании вашего приложения будут отображаться в ресурсе Application Insights на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="20b8d-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="20b8d-105">Поиск телеметрии</span><span class="sxs-lookup"><span data-stu-id="20b8d-105">Find your telemetry</span></span>
<span data-ttu-id="20b8d-106">Выполните вход на [портале Azure](https://portal.azure.com) и перейдите к ресурсу Application Insights, созданному для приложения.</span><span class="sxs-lookup"><span data-stu-id="20b8d-106">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the Application Insights resource that you created for your app.</span></span>

![Щелкните «Обзор», выберите «Application Insights», а затем свое приложение.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="20b8d-108">Колонка (страница) обзора приложения содержит основные метрики диагностики вашего приложения и предоставляет доступ к остальным функциям портала.</span><span class="sxs-lookup"><span data-stu-id="20b8d-108">The overview blade (page) for your app shows a summary of the key diagnostic metrics of your app, and is a gateway to the other features of the portal.</span></span>

![Основные маршруты для просмотра телеметрии](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="20b8d-110">Вы можете настроить любую диаграмму или сетку и закрепить ее на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="20b8d-110">You can customize any of the charts and grids and pin them to a dashboard.</span></span> <span data-ttu-id="20b8d-111">Таким образом можно объединить на центральной панели мониторинга ключевые данные телеметрии из разных приложений.</span><span class="sxs-lookup"><span data-stu-id="20b8d-111">That way, you can bring together the key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="20b8d-112">Панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="20b8d-112">Dashboards</span></span>
<span data-ttu-id="20b8d-113">Выполнив вход на [портал Microsoft Azure](https://portal.azure.com) , вы попадаете на панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="20b8d-113">The first thing you see after you sign in to the [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="20b8d-114">Здесь можно собрать самые нужные диаграммы из всех ресурсов Azure, в том числе данные телеметрии из [ Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20b8d-114">Here you can bring together the charts that are most important to you across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Настроенная панель мониторинга.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="20b8d-116">Чтобы **перейти к определенным ресурсам**, например к приложению в Application Insights, используйте панель слева.</span><span class="sxs-lookup"><span data-stu-id="20b8d-116">**Navigate to specific resources** such as your app in Application Insights: Use the left bar.</span></span>
2. <span data-ttu-id="20b8d-117">Чтобы **возвратиться на текущую панель мониторинга** или перейти в другие недавно открытые представления, используйте меню в верхнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="20b8d-117">**Return to the current dashboard**, or switch to other recent views: Use the drop-down menu at top left.</span></span>
3. <span data-ttu-id="20b8d-118">Чтобы **переключаться между панелями мониторинга**, воспользуйтесь меню возле заголовка панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="20b8d-118">**Switch dashboards**: Use the drop-down menu on the dashboard title</span></span>
4. <span data-ttu-id="20b8d-119">**Создавать и изменять панели мониторинга, а также использовать их совместно с другими пользователями** можно c помощью панели инструментов панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="20b8d-119">**Create, edit, and share dashboards** in the dashboard toolbar.</span></span>
5. <span data-ttu-id="20b8d-120">Чтобы **настроить панель мониторинга**, перемещайте, настраивайте и удаляйте плитки, наводя указатель мыши сначала на них, а потом на соответствующие значения в верхней панели.</span><span class="sxs-lookup"><span data-stu-id="20b8d-120">**Edit the dashboard**: Hover over a tile and then use its top bar to move, customize, or remove it.</span></span>

## <a name="add-to-a-dashboard"></a><span data-ttu-id="20b8d-121">Добавить на панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="20b8d-121">Add to a dashboard</span></span>
<span data-ttu-id="20b8d-122">Если вы просматриваете колонку или набор диаграмм, которая особенно интересна, закрепите ее копию на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="20b8d-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it to the dashboard.</span></span> <span data-ttu-id="20b8d-123">Вы увидите ее, когда в очередной раз откроете панель.</span><span class="sxs-lookup"><span data-stu-id="20b8d-123">You'll see it next time you return there.</span></span>

![Чтобы закрепить диаграмму, наведите на нее курсор мыши и нажмите кнопку "..." в заголовке.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="20b8d-125">Закрепите диаграмму на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="20b8d-125">Pin chart to dashboard.</span></span> <span data-ttu-id="20b8d-126">На панели мониторинга появится копия диаграммы.</span><span class="sxs-lookup"><span data-stu-id="20b8d-126">A copy of the chart appears on the dashboard.</span></span>
2. <span data-ttu-id="20b8d-127">Закрепите целую колонку на панели мониторинга — она отображается на панели мониторинга в виде плитки, которую можно щелкнуть.</span><span class="sxs-lookup"><span data-stu-id="20b8d-127">Pin the whole blade to the dashboard - it appears on the dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="20b8d-128">Щелкните клавишей мыши в левом верхнем углу, чтобы вернуться к текущей панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="20b8d-128">Click the top left corner to return to the current dashboard.</span></span> <span data-ttu-id="20b8d-129">Затем используйте раскрывающееся меню, чтобы вернуться в текущее представление.</span><span class="sxs-lookup"><span data-stu-id="20b8d-129">Then you can use the drop-down menu to return to the current view.</span></span>

<span data-ttu-id="20b8d-130">Обратите внимание, что диаграммы группируются в плитки и каждая плитка может содержать сразу несколько диаграмм.</span><span class="sxs-lookup"><span data-stu-id="20b8d-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="20b8d-131">Плитку можно закрепить на панели мониторинга целиком.</span><span class="sxs-lookup"><span data-stu-id="20b8d-131">You pin the whole tile to the dashboard.</span></span>

<span data-ttu-id="20b8d-132">Диаграмма обновляется автоматически с периодичностью, которая зависит от ее диапазона времени:</span><span class="sxs-lookup"><span data-stu-id="20b8d-132">The chart is automatically refreshed with a frequency that depends on the chart's time range:</span></span>

* <span data-ttu-id="20b8d-133">диапазон времени до 1 часа: обновление каждые 5 минут;</span><span class="sxs-lookup"><span data-stu-id="20b8d-133">Time range up to 1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="20b8d-134">диапазон времени от 1 до 24 часов: обновление каждые 15 минут;</span><span class="sxs-lookup"><span data-stu-id="20b8d-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="20b8d-135">диапазон времени более 24 часов: (диапазон времени)/60.</span><span class="sxs-lookup"><span data-stu-id="20b8d-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="20b8d-136">Закрепление любого запроса в аналитике</span><span class="sxs-lookup"><span data-stu-id="20b8d-136">Pin any query in Analytics</span></span>
<span data-ttu-id="20b8d-137">Вы также можете [закрепить диаграммы аналитики](app-insights-analytics-using.md#pin-to-dashboard) на [общей](#share-dashboards-with-your-team) панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="20b8d-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts to a [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="20b8d-138">Это позволяет добавлять диаграммы из любого произвольного запроса вместе со стандартными метриками.</span><span class="sxs-lookup"><span data-stu-id="20b8d-138">This allows you to add charts of any arbitrary query alongside the standard metrics.</span></span> 

<span data-ttu-id="20b8d-139">Результаты пересчитываются автоматически каждый час.</span><span class="sxs-lookup"><span data-stu-id="20b8d-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="20b8d-140">Чтобы пересчитать результаты немедленно, щелкните значок "Обновить" на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="20b8d-140">Click the Refresh icon on the chart to recalculate immediately.</span></span> <span data-ttu-id="20b8d-141">(При обновлении окна браузера результаты не пересчитываются.)</span><span class="sxs-lookup"><span data-stu-id="20b8d-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-the-dashboard"></a><span data-ttu-id="20b8d-142">Корректировка плитки на панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="20b8d-142">Adjust a tile on the dashboard</span></span>
<span data-ttu-id="20b8d-143">Плитку, закрепленную на панели мониторинга, можно скорректировать.</span><span class="sxs-lookup"><span data-stu-id="20b8d-143">Once a tile is on the dashboard, you can adjust it.</span></span>

![Наведите указатель мыши на диаграмму, чтобы ее изменить.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="20b8d-145">Добавить на плитку диаграмму.</span><span class="sxs-lookup"><span data-stu-id="20b8d-145">Add a chart to the tile.</span></span>
2. <span data-ttu-id="20b8d-146">Настроить метрику, параметры группировки и стиль (таблица, график) диаграммы.</span><span class="sxs-lookup"><span data-stu-id="20b8d-146">Set the metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="20b8d-147">Чтобы увеличить изображение, перетащите указатель мыши через диаграмму. Нажмите кнопку "Отменить" для сброса временного диапазона. Задайте свойства фильтра для диаграмм на плитке.</span><span class="sxs-lookup"><span data-stu-id="20b8d-147">Drag across the diagram to zoom in; click the undo button to reset the timespan; set filter properties for the charts on the tile.</span></span>
4. <span data-ttu-id="20b8d-148">Настроить название плитки.</span><span class="sxs-lookup"><span data-stu-id="20b8d-148">Set tile title.</span></span>

<span data-ttu-id="20b8d-149">Плитки, закрепленные из колонок обозревателя метрик, имеют больше параметров редактирования, чем плитки, закрепленные из колонки обзора.</span><span class="sxs-lookup"><span data-stu-id="20b8d-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="20b8d-150">На оригинальное название плитки ваши правки не влияют.</span><span class="sxs-lookup"><span data-stu-id="20b8d-150">The original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="20b8d-151">Переключение между панелями мониторинга</span><span class="sxs-lookup"><span data-stu-id="20b8d-151">Switch between dashboards</span></span>
<span data-ttu-id="20b8d-152">Можно сохранить несколько панелей мониторинга и переключаться между ними.</span><span class="sxs-lookup"><span data-stu-id="20b8d-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="20b8d-153">При закреплении диаграммы или колонки они добавляются к текущей панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="20b8d-153">When you pin a chart or blade, they're added to the current dashboard.</span></span>

![Для переключения между панелями мониторинга щелкните "Панель мониторинга" и выберите сохраненную панель мониторинга.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="20b8d-157">Например, у вас может быть одна панель мониторинга для отображения полного экрана в комнате команды, а другая — для общей разработки.</span><span class="sxs-lookup"><span data-stu-id="20b8d-157">For example, you might have one dashboard for displaying full screen in the team room, and another for general development.</span></span>

<span data-ttu-id="20b8d-158">На панели мониторинга появится колонка в виде элемента: щелкните его, чтобы перейти к колонке.</span><span class="sxs-lookup"><span data-stu-id="20b8d-158">On the dashboard, a blade appears as a tile: click it to go to the blade.</span></span> <span data-ttu-id="20b8d-159">Диаграмма реплицирует диаграмму в исходном расположении.</span><span class="sxs-lookup"><span data-stu-id="20b8d-159">A chart replicates the chart in its original location.</span></span>

![Щелкните плитку, чтобы открыть соответствующую ей колонку.](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="20b8d-161">Совместное использование панелей мониторинга</span><span class="sxs-lookup"><span data-stu-id="20b8d-161">Share dashboards</span></span>
<span data-ttu-id="20b8d-162">Создав панель мониторинга, вы можете предоставить к ней доступ другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="20b8d-162">When you've created a dashboard, you can share it with other users.</span></span>

![Щелкните общую папку в заголовке панели мониторинга.](./media/app-insights-dashboards/41.png)

<span data-ttu-id="20b8d-164">Дополнительные сведения о [ролях и контроле доступа](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="20b8d-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="20b8d-165">Навигация в приложении</span><span class="sxs-lookup"><span data-stu-id="20b8d-165">App navigation</span></span>
<span data-ttu-id="20b8d-166">Колонка "Обзор" — это шлюз для получения дополнительных сведений о приложении.</span><span class="sxs-lookup"><span data-stu-id="20b8d-166">The overview blade is the gateway to more information about your app.</span></span>

* <span data-ttu-id="20b8d-167">Щелкните **любую диаграмму или плитку**, чтобы просмотреть более подробные отображаемые сведения.</span><span class="sxs-lookup"><span data-stu-id="20b8d-167">**Any chart or tile** - Click any tile or chart to see more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="20b8d-168">Кнопки колонки "Обзор"</span><span class="sxs-lookup"><span data-stu-id="20b8d-168">Overview blade buttons</span></span>
![Панель навигации в верхней части колонки "Обзор"](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="20b8d-170">[**Обозреватель метрик**](app-insights-metrics-explorer.md) необходим, чтобы создавать собственные метрики производительности и использования.</span><span class="sxs-lookup"><span data-stu-id="20b8d-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="20b8d-171">[**Поиск**](app-insights-diagnostic-search.md) необходим, чтобы изучать определенные экземпляры таких событий, как запросы, исключения или трассировки журналов.</span><span class="sxs-lookup"><span data-stu-id="20b8d-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="20b8d-172">[**Аналитика**](app-insights-analytics.md) подойдет для эффективных запросов телеметрии.</span><span class="sxs-lookup"><span data-stu-id="20b8d-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="20b8d-173">**Диапазон времени** необходим для настройки диапазона, который отображается во всех диаграммах в колонке.</span><span class="sxs-lookup"><span data-stu-id="20b8d-173">**Time range** - Adjust the range displayed by all the charts on the blade.</span></span>
* <span data-ttu-id="20b8d-174">**Удалить.** Удалите ресурс Application Insights для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="20b8d-174">**Delete** - Delete the Application Insights resource for this app.</span></span> <span data-ttu-id="20b8d-175">Следует также удалить пакеты Application Insights из кода приложения или изменить [ключ инструментирования](app-insights-create-new-resource.md#copy-the-instrumentation-key) в приложении, чтобы направлять данные телеметрии на другой ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="20b8d-175">You should also either remove the Application Insights packages from your app code, or edit the [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app to direct telemetry to a different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="20b8d-176">Вкладка "Основное"</span><span class="sxs-lookup"><span data-stu-id="20b8d-176">Essentials tab</span></span>
* <span data-ttu-id="20b8d-177">[Ключ инструментирования](app-insights-create-new-resource.md#copy-the-instrumentation-key) определяет ресурс этого приложения.</span><span class="sxs-lookup"><span data-stu-id="20b8d-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="20b8d-178">Цены позволяют предоставить доступ к компонентам и установить ограничения объема.</span><span class="sxs-lookup"><span data-stu-id="20b8d-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="20b8d-179">Панель навигации приложения</span><span class="sxs-lookup"><span data-stu-id="20b8d-179">App navigation bar</span></span>
![Левая панель навигации](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="20b8d-181">**Обзор** позволяет вернуться к колонке обзора приложения.</span><span class="sxs-lookup"><span data-stu-id="20b8d-181">**Overview** - Return to the app overview blade.</span></span>
* <span data-ttu-id="20b8d-182">**Журнал действий** предоставляет доступ к оповещениям и административным событиям Azure.</span><span class="sxs-lookup"><span data-stu-id="20b8d-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="20b8d-183">[**Контроль доступа**](app-insights-resources-roles-access-control.md) предоставляет доступ к членам группы и другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="20b8d-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access to team members and others.</span></span>
* <span data-ttu-id="20b8d-184">[**Теги**](../azure-resource-manager/resource-group-using-tags.md) можно использовать для группирования приложения с другими приложениями.</span><span class="sxs-lookup"><span data-stu-id="20b8d-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags to group your app with others.</span></span>

<span data-ttu-id="20b8d-185">ИЗУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="20b8d-185">INVESTIGATE</span></span>

* <span data-ttu-id="20b8d-186">[**Схема сопоставления приложений**](app-insights-app-map.md) — это активная карта, на которой показаны компоненты приложения, основанные на сведениях о зависимостях.</span><span class="sxs-lookup"><span data-stu-id="20b8d-186">[**Application map**](app-insights-app-map.md) - Active map showing the components of your application, derived from the dependency information.</span></span>
* <span data-ttu-id="20b8d-187">[**Интеллектуальное обнаружение**](app-insights-proactive-diagnostics.md) предназначено для просмотра последних оповещений о производительности.</span><span class="sxs-lookup"><span data-stu-id="20b8d-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="20b8d-188">[**Динамический поток**](app-insights-live-stream.md) представляет собой фиксированный набор почти мгновенных метрик, полезных при отладке или развертывании новой сборки.</span><span class="sxs-lookup"><span data-stu-id="20b8d-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="20b8d-189">[**Доступность и веб-тесты**](app-insights-monitor-web-app-availability.md) позволяют регулярно отправлять запросы в веб-приложение со всего мира.*</span><span class="sxs-lookup"><span data-stu-id="20b8d-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests to your web app from around the world.*</span></span>
* <span data-ttu-id="20b8d-190">[**Сбои и производительность**](app-insights-web-monitor-performance.md) предназначены для проверки исключений, частоты сбоев и времени отклика на запросы приложения и из приложения к [зависимостям](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="20b8d-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests to your app and for requests from your app to [dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="20b8d-191">[**Производительность**](app-insights-web-monitor-performance.md) — это время отклика, время отклика зависимостей.</span><span class="sxs-lookup"><span data-stu-id="20b8d-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="20b8d-192">[Серверы](app-insights-web-monitor-performance.md) — счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="20b8d-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="20b8d-193">Доступны, если [установить монитор состояния](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="20b8d-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="20b8d-194">**Браузер** — производительность просмотра страниц и вызовов технологии AJAX.</span><span class="sxs-lookup"><span data-stu-id="20b8d-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="20b8d-195">Доступно, если [инструментировать веб-страницы](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="20b8d-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="20b8d-196">**Использование** — число просмотров страниц, пользователей и сеансов.</span><span class="sxs-lookup"><span data-stu-id="20b8d-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="20b8d-197">Доступно, если [инструментировать веб-страницы](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="20b8d-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="20b8d-198">НАСТРОЙКА</span><span class="sxs-lookup"><span data-stu-id="20b8d-198">CONFIGURE</span></span>

* <span data-ttu-id="20b8d-199">**Начало работы** — встроенное руководство.</span><span class="sxs-lookup"><span data-stu-id="20b8d-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="20b8d-200">**Свойства** — ключ инструментирования, идентификатор подписки и ресурса.</span><span class="sxs-lookup"><span data-stu-id="20b8d-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="20b8d-201">[Оповещения](app-insights-alerts.md) — конфигурация оповещений для метрик.</span><span class="sxs-lookup"><span data-stu-id="20b8d-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="20b8d-202">[Непрерывный экспорт](app-insights-export-telemetry.md) — настройка экспорта данных телеметрии в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="20b8d-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry to Azure storage.</span></span>
* <span data-ttu-id="20b8d-203">[Тестирование производительности](app-insights-monitor-web-app-availability.md#performance-tests) — настройка искусственной нагрузки на веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="20b8d-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="20b8d-204">[Квота и цены](app-insights-pricing.md) и [выборка приема](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="20b8d-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="20b8d-205">**Доступ к API** используется для создания [аннотаций к выпуску](app-insights-annotations.md) и для API доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="20b8d-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for the Data Access API.</span></span>
* <span data-ttu-id="20b8d-206">[**Рабочие элементы**](app-insights-diagnostic-search.md#create-work-item) подключаются к системе отслеживания работы, позволяющей создавать ошибки при проверке данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="20b8d-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect to a work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="20b8d-207">ПАРАМЕТРЫ</span><span class="sxs-lookup"><span data-stu-id="20b8d-207">SETTINGS</span></span>

* <span data-ttu-id="20b8d-208">[**Блокировки**](../azure-resource-manager/resource-group-lock-resources.md) позволяют блокировать ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="20b8d-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="20b8d-209">[**Сценарий автоматизации**](app-insights-powershell.md) — это экспорт определения ресурса Azure, позволяющий использовать его как шаблон для создания новых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="20b8d-209">[**Automation script**](app-insights-powershell.md) - export a definition of the Azure resource so that you can use it as a template to create new resources.</span></span>


## <a name="video"></a><span data-ttu-id="20b8d-210">Видео</span><span class="sxs-lookup"><span data-stu-id="20b8d-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="20b8d-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="20b8d-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="20b8d-212">Обозреватель метрик</span><span class="sxs-lookup"><span data-stu-id="20b8d-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="20b8d-213">Фильтрация и сегментирование метрик</span><span class="sxs-lookup"><span data-stu-id="20b8d-213">Filter and segment metrics</span></span> |![Пример поиска](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="20b8d-215">Поиск по журналу диагностики</span><span class="sxs-lookup"><span data-stu-id="20b8d-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="20b8d-216">Поиск и проверка событий, связанные события и создание ошибок</span><span class="sxs-lookup"><span data-stu-id="20b8d-216">Find and inspect events, related events, and create bugs</span></span> |![Пример поиска](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="20b8d-218">Аналитика в Application Insights</span><span class="sxs-lookup"><span data-stu-id="20b8d-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="20b8d-219">Эффективный язык запросов</span><span class="sxs-lookup"><span data-stu-id="20b8d-219">Powerful query language</span></span> |![Пример поиска](./media/app-insights-dashboards/63.png) |
