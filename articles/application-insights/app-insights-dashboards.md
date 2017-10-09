---
title: "aaaDashboards и навигация в hello Azure Application Insights | Документы Microsoft"
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
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a><span data-ttu-id="99918-103">Навигации и панели мониторинга на портале Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="99918-103">Navigation and Dashboards in hello Application Insights portal</span></span>
<span data-ttu-id="99918-104">После того как вы [настроить Application Insights в проекте](app-insights-overview.md), данных телеметрии о производительности и использовании приложения будет отображаться в ресурс Application Insights проекта в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="99918-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in hello [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="99918-105">Поиск телеметрии</span><span class="sxs-lookup"><span data-stu-id="99918-105">Find your telemetry</span></span>
<span data-ttu-id="99918-106">Войдите в toohello [портал Azure](https://portal.azure.com) и перейдите в ресурс Application Insights toohello, который был создан для приложения.</span><span class="sxs-lookup"><span data-stu-id="99918-106">Sign in toohello [Azure portal](https://portal.azure.com) and navigate toohello Application Insights resource that you created for your app.</span></span>

![Щелкните «Обзор», выберите «Application Insights», а затем свое приложение.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="99918-108">Hello Обзор (страница) для вашего приложения со сводкой hello диагностики показатели приложения и, при необходимости является toohello шлюза другие функции hello портала.</span><span class="sxs-lookup"><span data-stu-id="99918-108">hello overview blade (page) for your app shows a summary of hello key diagnostic metrics of your app, and is a gateway toohello other features of hello portal.</span></span>

![Основная tooview маршруты телеметрии](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="99918-110">Можно настроить любой из hello диаграммы и таблицы и закрепить их tooa панель.</span><span class="sxs-lookup"><span data-stu-id="99918-110">You can customize any of hello charts and grids and pin them tooa dashboard.</span></span> <span data-ttu-id="99918-111">Таким образом, можно объединить hello ключа телеметрии из других приложений на центральной панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="99918-111">That way, you can bring together hello key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="99918-112">Панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="99918-112">Dashboards</span></span>
<span data-ttu-id="99918-113">Hello первое, что вы видите после входа в toohello [портал Microsoft Azure](https://portal.azure.com) является информационной панели.</span><span class="sxs-lookup"><span data-stu-id="99918-113">hello first thing you see after you sign in toohello [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="99918-114">Здесь можно объединить hello диаграммы, которые являются наиболее важных tooyou для всех ваших ресурсах Azure, включая данные телеметрии из [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99918-114">Here you can bring together hello charts that are most important tooyou across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Настроенная панель мониторинга.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="99918-116">**Перейдите ресурсы toospecific** таких как приложения в Application Insights: используйте hello левой панели.</span><span class="sxs-lookup"><span data-stu-id="99918-116">**Navigate toospecific resources** such as your app in Application Insights: Use hello left bar.</span></span>
2. <span data-ttu-id="99918-117">**Текущей панели мониторинга возвращаемого toohello**, или для переключения между представлениями последних tooother: используйте hello раскрывающееся меню в верхнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="99918-117">**Return toohello current dashboard**, or switch tooother recent views: Use hello drop-down menu at top left.</span></span>
3. <span data-ttu-id="99918-118">**Переключение панели мониторинга**: используйте hello раскрывающееся меню на заголовок панели мониторинга hello</span><span class="sxs-lookup"><span data-stu-id="99918-118">**Switch dashboards**: Use hello drop-down menu on hello dashboard title</span></span>
4. <span data-ttu-id="99918-119">**Создание, изменение и совместно использовать панели мониторинга** в панель инструментов панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="99918-119">**Create, edit, and share dashboards** in hello dashboard toolbar.</span></span>
5. <span data-ttu-id="99918-120">**Изменение панели мониторинга hello**: наведите указатель мыши на плитку, а затем используйте его верхней панели toomove, настроить или удалить его.</span><span class="sxs-lookup"><span data-stu-id="99918-120">**Edit hello dashboard**: Hover over a tile and then use its top bar toomove, customize, or remove it.</span></span>

## <a name="add-tooa-dashboard"></a><span data-ttu-id="99918-121">Добавить tooa панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="99918-121">Add tooa dashboard</span></span>
<span data-ttu-id="99918-122">Когда вы просматриваете колонке или набор диаграмм, особенно интересны, можно закрепить его копию toohello панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="99918-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it toohello dashboard.</span></span> <span data-ttu-id="99918-123">Вы увидите ее, когда в очередной раз откроете панель.</span><span class="sxs-lookup"><span data-stu-id="99918-123">You'll see it next time you return there.</span></span>

![toopin диаграмму, наведите на нее и нажмите кнопку «...» в заголовке hello.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="99918-125">Закрепить toodashboard диаграммы.</span><span class="sxs-lookup"><span data-stu-id="99918-125">Pin chart toodashboard.</span></span> <span data-ttu-id="99918-126">Копию hello диаграммы отображается на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="99918-126">A copy of hello chart appears on hello dashboard.</span></span>
2. <span data-ttu-id="99918-127">ПИН-кода hello всей колонке toohello - он откроется панель hello панели мониторинга как плитку, которую можно щелкнуть по.</span><span class="sxs-lookup"><span data-stu-id="99918-127">Pin hello whole blade toohello dashboard - it appears on hello dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="99918-128">Щелкните hello верхнего левого угла tooreturn toohello текущей панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="99918-128">Click hello top left corner tooreturn toohello current dashboard.</span></span> <span data-ttu-id="99918-129">Затем можно использовать текущее представление toohello tooreturn hello раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="99918-129">Then you can use hello drop-down menu tooreturn toohello current view.</span></span>

<span data-ttu-id="99918-130">Обратите внимание, что диаграммы группируются в плитки и каждая плитка может содержать сразу несколько диаграмм.</span><span class="sxs-lookup"><span data-stu-id="99918-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="99918-131">Можно закрепить панель toohello всей плитки приветствия.</span><span class="sxs-lookup"><span data-stu-id="99918-131">You pin hello whole tile toohello dashboard.</span></span>

<span data-ttu-id="99918-132">Hello диаграммы автоматически обновляются с частотой, от которого зависит hello диаграммы диапазон времени:</span><span class="sxs-lookup"><span data-stu-id="99918-132">hello chart is automatically refreshed with a frequency that depends on hello chart's time range:</span></span>

* <span data-ttu-id="99918-133">Временной диапазон копирование час too1: обновление каждые 5 минут</span><span class="sxs-lookup"><span data-stu-id="99918-133">Time range up too1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="99918-134">диапазон времени от 1 до 24 часов: обновление каждые 15 минут;</span><span class="sxs-lookup"><span data-stu-id="99918-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="99918-135">диапазон времени более 24 часов: (диапазон времени)/60.</span><span class="sxs-lookup"><span data-stu-id="99918-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="99918-136">Закрепление любого запроса в аналитике</span><span class="sxs-lookup"><span data-stu-id="99918-136">Pin any query in Analytics</span></span>
<span data-ttu-id="99918-137">Вы также можете [закрепить Analytics](app-insights-analytics-using.md#pin-to-dashboard) tooa диаграммы [общего](#share-dashboards-with-your-team) панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="99918-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts tooa [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="99918-138">Это позволяет tooadd диаграммы любого произвольного запроса вместе со стандартными показателями hello.</span><span class="sxs-lookup"><span data-stu-id="99918-138">This allows you tooadd charts of any arbitrary query alongside hello standard metrics.</span></span> 

<span data-ttu-id="99918-139">Результаты пересчитываются автоматически каждый час.</span><span class="sxs-lookup"><span data-stu-id="99918-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="99918-140">Щелкните значок обновления hello hello диаграммы toorecalculate немедленно.</span><span class="sxs-lookup"><span data-stu-id="99918-140">Click hello Refresh icon on hello chart toorecalculate immediately.</span></span> <span data-ttu-id="99918-141">(При обновлении окна браузера результаты не пересчитываются.)</span><span class="sxs-lookup"><span data-stu-id="99918-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-hello-dashboard"></a><span data-ttu-id="99918-142">Измените плитки на панели мониторинга hello</span><span class="sxs-lookup"><span data-stu-id="99918-142">Adjust a tile on hello dashboard</span></span>
<span data-ttu-id="99918-143">После плитки на панели мониторинга hello, ее можно изменить.</span><span class="sxs-lookup"><span data-stu-id="99918-143">Once a tile is on hello dashboard, you can adjust it.</span></span>

![Наведите указатель мыши на диаграмме в порядке tooedit его.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="99918-145">Добавление плитки toohello диаграммы.</span><span class="sxs-lookup"><span data-stu-id="99918-145">Add a chart toohello tile.</span></span>
2. <span data-ttu-id="99918-146">Задать метрику hello, измерения, группы и стиль диаграммы (таблицы, диаграммы).</span><span class="sxs-lookup"><span data-stu-id="99918-146">Set hello metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="99918-147">Выполните перетаскивание через toozoom hello схемы Нажмите кнопку timespan hello tooreset кнопка отмены hello; задать свойства фильтра для hello диаграммы на плитке приветствия.</span><span class="sxs-lookup"><span data-stu-id="99918-147">Drag across hello diagram toozoom in; click hello undo button tooreset hello timespan; set filter properties for hello charts on hello tile.</span></span>
4. <span data-ttu-id="99918-148">Настроить название плитки.</span><span class="sxs-lookup"><span data-stu-id="99918-148">Set tile title.</span></span>

<span data-ttu-id="99918-149">Плитки, закрепленные из колонок обозревателя метрик, имеют больше параметров редактирования, чем плитки, закрепленные из колонки обзора.</span><span class="sxs-lookup"><span data-stu-id="99918-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="99918-150">изменения, внесенные Hello исходного плитки, закрепленной не влияет.</span><span class="sxs-lookup"><span data-stu-id="99918-150">hello original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="99918-151">Переключение между панелями мониторинга</span><span class="sxs-lookup"><span data-stu-id="99918-151">Switch between dashboards</span></span>
<span data-ttu-id="99918-152">Можно сохранить несколько панелей мониторинга и переключаться между ними.</span><span class="sxs-lookup"><span data-stu-id="99918-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="99918-153">При закреплении диаграммы или колонки, они добавляются toohello текущей панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="99918-153">When you pin a chart or blade, they're added toohello current dashboard.</span></span>

![tooswitch между панелями мониторинга, щелкните панель мониторинга и выберите сохраненный панели мониторинга.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="99918-157">Например может потребоваться одна панель мониторинга для отображения полного экрана в комнате команды hello, а другой для общей разработки.</span><span class="sxs-lookup"><span data-stu-id="99918-157">For example, you might have one dashboard for displaying full screen in hello team room, and another for general development.</span></span>

<span data-ttu-id="99918-158">На панели мониторинга hello, панель отображается в виде плитки: нажмите кнопку toogo toohello колонку.</span><span class="sxs-lookup"><span data-stu-id="99918-158">On hello dashboard, a blade appears as a tile: click it toogo toohello blade.</span></span> <span data-ttu-id="99918-159">Диаграмма реплицирует hello диаграммы в его исходном месте.</span><span class="sxs-lookup"><span data-stu-id="99918-159">A chart replicates hello chart in its original location.</span></span>

![Нажмите кнопку колонки hello tooopen плитки, представляемой](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="99918-161">Совместное использование панелей мониторинга</span><span class="sxs-lookup"><span data-stu-id="99918-161">Share dashboards</span></span>
<span data-ttu-id="99918-162">Создав панель мониторинга, вы можете предоставить к ней доступ другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="99918-162">When you've created a dashboard, you can share it with other users.</span></span>

![В заголовке панели мониторинга hello выберите общий ресурс](./media/app-insights-dashboards/41.png)

<span data-ttu-id="99918-164">Дополнительные сведения о [ролях и контроле доступа](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="99918-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="99918-165">Навигация в приложении</span><span class="sxs-lookup"><span data-stu-id="99918-165">App navigation</span></span>
<span data-ttu-id="99918-166">Обзор колонке Hello — hello шлюза toomore информацию о приложении.</span><span class="sxs-lookup"><span data-stu-id="99918-166">hello overview blade is hello gateway toomore information about your app.</span></span>

* <span data-ttu-id="99918-167">**Все диаграммы или плитки** - щелкните одну из них или диаграммы toosee более подробные сведения о том, что он отображает.</span><span class="sxs-lookup"><span data-stu-id="99918-167">**Any chart or tile** - Click any tile or chart toosee more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="99918-168">Кнопки колонки "Обзор"</span><span class="sxs-lookup"><span data-stu-id="99918-168">Overview blade buttons</span></span>
![Панель навигации в верхней части колонки "Обзор"](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="99918-170">[**Обозреватель метрик**](app-insights-metrics-explorer.md) необходим, чтобы создавать собственные метрики производительности и использования.</span><span class="sxs-lookup"><span data-stu-id="99918-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="99918-171">[**Поиск**](app-insights-diagnostic-search.md) необходим, чтобы изучать определенные экземпляры таких событий, как запросы, исключения или трассировки журналов.</span><span class="sxs-lookup"><span data-stu-id="99918-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="99918-172">[**Аналитика**](app-insights-analytics.md) подойдет для эффективных запросов телеметрии.</span><span class="sxs-lookup"><span data-stu-id="99918-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="99918-173">**Временной диапазон** -настроить диапазон hello отобразить все диаграммы hello в колонке hello.</span><span class="sxs-lookup"><span data-stu-id="99918-173">**Time range** - Adjust hello range displayed by all hello charts on hello blade.</span></span>
* <span data-ttu-id="99918-174">**Удалить** -удаление ресурса Application Insights hello для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="99918-174">**Delete** - Delete hello Application Insights resource for this app.</span></span> <span data-ttu-id="99918-175">Следует также удалить hello Application Insights пакеты из кода вашего приложения либо изменить hello [ключ инструментирования](app-insights-create-new-resource.md#copy-the-instrumentation-key) в вашего приложения toodirect телеметрии tooa другой ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="99918-175">You should also either remove hello Application Insights packages from your app code, or edit hello [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app toodirect telemetry tooa different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="99918-176">Вкладка "Основное"</span><span class="sxs-lookup"><span data-stu-id="99918-176">Essentials tab</span></span>
* <span data-ttu-id="99918-177">[Ключ инструментирования](app-insights-create-new-resource.md#copy-the-instrumentation-key) определяет ресурс этого приложения.</span><span class="sxs-lookup"><span data-stu-id="99918-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="99918-178">Цены позволяют предоставить доступ к компонентам и установить ограничения объема.</span><span class="sxs-lookup"><span data-stu-id="99918-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="99918-179">Панель навигации приложения</span><span class="sxs-lookup"><span data-stu-id="99918-179">App navigation bar</span></span>
![Левая панель навигации](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="99918-181">**Общие сведения о** -колонка Обзор возвращаемого toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="99918-181">**Overview** - Return toohello app overview blade.</span></span>
* <span data-ttu-id="99918-182">**Журнал действий** предоставляет доступ к оповещениям и административным событиям Azure.</span><span class="sxs-lookup"><span data-stu-id="99918-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="99918-183">[**Контроль доступа** ](app-insights-resources-roles-access-control.md) -предоставляют доступ к членам tooteam и др.</span><span class="sxs-lookup"><span data-stu-id="99918-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access tooteam members and others.</span></span>
* <span data-ttu-id="99918-184">[**Теги** ](../azure-resource-manager/resource-group-using-tags.md) -используйте теги toogroup приложения с другими разделами.</span><span class="sxs-lookup"><span data-stu-id="99918-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags toogroup your app with others.</span></span>

<span data-ttu-id="99918-185">ИЗУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="99918-185">INVESTIGATE</span></span>

* <span data-ttu-id="99918-186">[**Сопоставления приложения** ](app-insights-app-map.md) -активная карта, показывающая hello компоненты приложения, производный от сведений о зависимостях hello.</span><span class="sxs-lookup"><span data-stu-id="99918-186">[**Application map**](app-insights-app-map.md) - Active map showing hello components of your application, derived from hello dependency information.</span></span>
* <span data-ttu-id="99918-187">[**Интеллектуальное обнаружение**](app-insights-proactive-diagnostics.md) предназначено для просмотра последних оповещений о производительности.</span><span class="sxs-lookup"><span data-stu-id="99918-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="99918-188">[**Динамический поток**](app-insights-live-stream.md) представляет собой фиксированный набор почти мгновенных метрик, полезных при отладке или развертывании новой сборки.</span><span class="sxs-lookup"><span data-stu-id="99918-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="99918-189">[**Доступность и веб-тесты** ](app-insights-monitor-web-app-availability.md) -Send обычных запросов tooyour веб-приложения из вокруг всем мире.* hello</span><span class="sxs-lookup"><span data-stu-id="99918-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests tooyour web app from around hello world.*</span></span>
* <span data-ttu-id="99918-190">[**Сбои, производительность** ](app-insights-web-monitor-performance.md) -исключений, сбоев и ответа время запросов tooyour приложения и для запросов в приложении слишком[зависимости](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="99918-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests tooyour app and for requests from your app too[dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="99918-191">[**Производительность**](app-insights-web-monitor-performance.md) — это время отклика, время отклика зависимостей.</span><span class="sxs-lookup"><span data-stu-id="99918-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="99918-192">[Серверы](app-insights-web-monitor-performance.md) — счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="99918-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="99918-193">Доступны, если [установить монитор состояния](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="99918-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="99918-194">**Браузер** — производительность просмотра страниц и вызовов технологии AJAX.</span><span class="sxs-lookup"><span data-stu-id="99918-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="99918-195">Доступно, если [инструментировать веб-страницы](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="99918-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="99918-196">**Использование** — число просмотров страниц, пользователей и сеансов.</span><span class="sxs-lookup"><span data-stu-id="99918-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="99918-197">Доступно, если [инструментировать веб-страницы](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="99918-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="99918-198">НАСТРОЙКА</span><span class="sxs-lookup"><span data-stu-id="99918-198">CONFIGURE</span></span>

* <span data-ttu-id="99918-199">**Начало работы** — встроенное руководство.</span><span class="sxs-lookup"><span data-stu-id="99918-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="99918-200">**Свойства** — ключ инструментирования, идентификатор подписки и ресурса.</span><span class="sxs-lookup"><span data-stu-id="99918-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="99918-201">[Оповещения](app-insights-alerts.md) — конфигурация оповещений для метрик.</span><span class="sxs-lookup"><span data-stu-id="99918-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="99918-202">[Непрерывный Экспорт](app-insights-export-telemetry.md) -настроить экспорт телеметрии tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="99918-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry tooAzure storage.</span></span>
* <span data-ttu-id="99918-203">[Тестирование производительности](app-insights-monitor-web-app-availability.md#performance-tests) — настройка искусственной нагрузки на веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="99918-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="99918-204">[Квота и цены](app-insights-pricing.md) и [выборка приема](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="99918-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="99918-205">**Доступ к API** -создать [выпуска заметки](app-insights-annotations.md) и для hello API-Интерфейс.</span><span class="sxs-lookup"><span data-stu-id="99918-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for hello Data Access API.</span></span>
* <span data-ttu-id="99918-206">[**Рабочие элементы** ](app-insights-diagnostic-search.md#create-work-item) -tooa работы системы отслеживания, чтобы ошибки при проверке телеметрии можно создавать подключения.</span><span class="sxs-lookup"><span data-stu-id="99918-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect tooa work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="99918-207">ПАРАМЕТРЫ</span><span class="sxs-lookup"><span data-stu-id="99918-207">SETTINGS</span></span>

* <span data-ttu-id="99918-208">[**Блокировки**](../azure-resource-manager/resource-group-lock-resources.md) позволяют блокировать ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="99918-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="99918-209">[**Сценарий автоматизации** ](app-insights-powershell.md) -экспортировать определение hello ресурсов Azure, чтобы ее можно использовать в качестве шаблона toocreate новые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="99918-209">[**Automation script**](app-insights-powershell.md) - export a definition of hello Azure resource so that you can use it as a template toocreate new resources.</span></span>


## <a name="video"></a><span data-ttu-id="99918-210">Видео</span><span class="sxs-lookup"><span data-stu-id="99918-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="99918-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="99918-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="99918-212">Обозреватель метрик</span><span class="sxs-lookup"><span data-stu-id="99918-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="99918-213">Фильтрация и сегментирование метрик</span><span class="sxs-lookup"><span data-stu-id="99918-213">Filter and segment metrics</span></span> |![Пример поиска](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="99918-215">Поиск по журналу диагностики</span><span class="sxs-lookup"><span data-stu-id="99918-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="99918-216">Поиск и проверка событий, связанные события и создание ошибок</span><span class="sxs-lookup"><span data-stu-id="99918-216">Find and inspect events, related events, and create bugs</span></span> |![Пример поиска](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="99918-218">Аналитика в Application Insights</span><span class="sxs-lookup"><span data-stu-id="99918-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="99918-219">Эффективный язык запросов</span><span class="sxs-lookup"><span data-stu-id="99918-219">Powerful query language</span></span> |![Пример поиска](./media/app-insights-dashboards/63.png) |
