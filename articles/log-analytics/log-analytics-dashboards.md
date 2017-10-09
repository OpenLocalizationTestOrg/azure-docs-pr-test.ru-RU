---
title: "aaaCreate настраиваемую панель мониторинга в службе анализа журналов Azure | Документы Microsoft"
description: "Это руководство поможет вам понять, как панели мониторинга службы анализа журналов можно визуализации всех ваших запросов поиска журналов, предоставляя один дисторсии tooview вашей среде."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="91f89-103">Создание пользовательской панели мониторинга для Log Analytics</span><span class="sxs-lookup"><span data-stu-id="91f89-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="91f89-104">Если обновленный toohello рабочей области [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то нельзя создать новые панели мониторинга или изменение существующих панелей мониторинга.</span><span class="sxs-lookup"><span data-stu-id="91f89-104">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="91f89-105">Это руководство поможет вам понять, как панели мониторинга службы анализа журналов можно визуализации всех ваших запросов поиска журналов, предоставляя один дисторсии tooview вашей среде.</span><span class="sxs-lookup"><span data-stu-id="91f89-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens tooview your environment.</span></span>

![Пример панели мониторинга](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="91f89-107">Все hello настраиваемых панелей мониторинга, созданные на портале OMS hello, также доступны в hello мобильные приложения OMS.</span><span class="sxs-lookup"><span data-stu-id="91f89-107">All hello custom dashboards that you create in hello OMS portal are also available in hello OMS Mobile App.</span></span> <span data-ttu-id="91f89-108">См. следующие страницы, Дополнительные сведения о приложениях hello hello.</span><span class="sxs-lookup"><span data-stu-id="91f89-108">See hello following pages for more information about hello apps.</span></span>

* [<span data-ttu-id="91f89-109">OMS мобильного приложения из магазина Microsoft hello</span><span class="sxs-lookup"><span data-stu-id="91f89-109">OMS mobile app from hello Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="91f89-110">Мобильное приложение OMS в Apple iTunes</span><span class="sxs-lookup"><span data-stu-id="91f89-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![панель мониторинга на мобильном устройстве](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="91f89-112">Создание панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="91f89-112">How do I create my dashboard?</span></span>
<span data-ttu-id="91f89-113">toobegin toohello последовательно выберите «Обзор» OMS.</span><span class="sxs-lookup"><span data-stu-id="91f89-113">toobegin, go toohello OMS Overview page.</span></span> <span data-ttu-id="91f89-114">Вы увидите hello **Моя панель мониторинга** плитки слева hello.</span><span class="sxs-lookup"><span data-stu-id="91f89-114">You'll see hello **My Dashboard** tile on hello left.</span></span> <span data-ttu-id="91f89-115">Щелкните его toodrill вниз на информационную панель.</span><span class="sxs-lookup"><span data-stu-id="91f89-115">Click it toodrill down into your dashboard.</span></span>

![Обзор](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="91f89-117">Добавление плитки</span><span class="sxs-lookup"><span data-stu-id="91f89-117">Adding a tile</span></span>
<span data-ttu-id="91f89-118">В разделе панелей мониторинга сведения на плитках берутся из сохраненных запросов поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="91f89-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="91f89-119">В службе OMS есть много уже готовых запросов поиска журналов, поэтому вы сможете сразу приступить к созданию панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="91f89-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="91f89-120">Используйте hello описанных ниже действий, характеризующих как toobegin.</span><span class="sxs-lookup"><span data-stu-id="91f89-120">Use hello following steps that outline how toobegin.</span></span>

<span data-ttu-id="91f89-121">В hello Моя панель мониторинга представления, щелкните **Настройка** tooenter режим настройки.</span><span class="sxs-lookup"><span data-stu-id="91f89-121">In hello My Dashboard view, simply click **Customize** tooenter customize mode.</span></span>

![Инструкция в виде рисунков](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="91f89-123">Откроется hello правой части страницы приветствия Hello панель показывает все рабочую область сохраненных запросов поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="91f89-123">hello panel that opens on hello right side of hello page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="91f89-124">toovisualize сохраненный журнал поиска как плитку, наведите указатель мыши на сохраненные условия поиска и нажмите кнопку hello **, а также** символов.</span><span class="sxs-lookup"><span data-stu-id="91f89-124">toovisualize a saved log search as a tile,  hover over a saved search and then click hello **plus** symbol.</span></span>

![Добавление плиток 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="91f89-126">При нажатии кнопки hello **, а также** symbol, новая Плитка отображается в hello представление Моя панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="91f89-126">When you click hello **plus** symbol, a new tile appears in hello My Dashboard view.</span></span>

![Добавление плиток 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="91f89-128">Изменение плитки</span><span class="sxs-lookup"><span data-stu-id="91f89-128">Edit a tile</span></span>
<span data-ttu-id="91f89-129">В hello Моя панель мониторинга представления, щелкните **Настройка** tooenter режим настройки.</span><span class="sxs-lookup"><span data-stu-id="91f89-129">In hello My Dashboard view, simply click  **Customize** tooenter customize mode.</span></span> <span data-ttu-id="91f89-130">Щелкните плитку hello требуется tooedit.</span><span class="sxs-lookup"><span data-stu-id="91f89-130">Click hello tile you want tooedit.</span></span> <span data-ttu-id="91f89-131">Правая панель Hello изменения tooedit и обеспечивает выбор вариантов:</span><span class="sxs-lookup"><span data-stu-id="91f89-131">hello right panel changes tooedit, and gives a selection of options:</span></span>

![Изменение плитки](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Изменение плитки](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="91f89-134">Визуализация плиток</span><span class="sxs-lookup"><span data-stu-id="91f89-134">Tile visualizations</span></span>
<span data-ttu-id="91f89-135">Существует три вида toochoose визуализации плитки из:</span><span class="sxs-lookup"><span data-stu-id="91f89-135">There are three kinds of tile visualizations toochoose from:</span></span>

| <span data-ttu-id="91f89-136">тип диаграммы</span><span class="sxs-lookup"><span data-stu-id="91f89-136">chart type</span></span> | <span data-ttu-id="91f89-137">назначение</span><span class="sxs-lookup"><span data-stu-id="91f89-137">what it does</span></span> |
| --- | --- |
| ![Линейчатая диаграмма](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="91f89-139">Отображает временную шкалу результатов сохраненного поиска по журналу в виде линейчатой диаграммы или списка результатов по полям (зависит от того, сортирует ли поиск по журналу найденные результаты по полям).</span><span class="sxs-lookup"><span data-stu-id="91f89-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![метрика](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="91f89-141">На ней показывается число, которое означает, сколько раз был найден элемент по запросу поиска журнала.</span><span class="sxs-lookup"><span data-stu-id="91f89-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="91f89-142">Плитки с метрикой позволяют tooset пороговое значение, которое будет выделяться плитки приветствия при достижении порога hello.</span><span class="sxs-lookup"><span data-stu-id="91f89-142">Metric tiles allow you tooset a threshold that will highlight hello tile when hello threshold is reached.</span></span> |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="91f89-144">Отображает временную шкалу совпадения результатов сохраненного поиска по журналу со значениями в виде графика.</span><span class="sxs-lookup"><span data-stu-id="91f89-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="91f89-145">Пороговое значение</span><span class="sxs-lookup"><span data-stu-id="91f89-145">Threshold</span></span>
<span data-ttu-id="91f89-146">Пороговое значение можно создать на плитки с помощью hello визуализацию в виде метрики.</span><span class="sxs-lookup"><span data-stu-id="91f89-146">You can create a threshold on a tile using hello Metric visualization.</span></span> <span data-ttu-id="91f89-147">Выберите toocreate пороговое значение на плитке приветствия.</span><span class="sxs-lookup"><span data-stu-id="91f89-147">Select on toocreate a threshold value on hello tile.</span></span> <span data-ttu-id="91f89-148">Выберите ли toohighlight hello карточки при hello значение — выше или ниже порогового значения выбранного hello, задайте пороговое значение hello ниже.</span><span class="sxs-lookup"><span data-stu-id="91f89-148">Choose whether toohighlight hello tile when hello value is over or under hello chosen threshold, then set hello threshold value below.</span></span>

## <a name="organizing-hello-dashboard"></a><span data-ttu-id="91f89-149">Упорядочение панели мониторинга hello</span><span class="sxs-lookup"><span data-stu-id="91f89-149">Organizing hello dashboard</span></span>
<span data-ttu-id="91f89-150">tooorganize перейдите toohello Моя панель мониторинга представления панели мониторинга и нажмите кнопку **Настройка** tooenter режим настройки.</span><span class="sxs-lookup"><span data-stu-id="91f89-150">tooorganize your dashboard, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="91f89-151">Щелкните и перетащите плитку hello нужны toomove и переместите его toowhere требуется вашей toobe плитки.</span><span class="sxs-lookup"><span data-stu-id="91f89-151">Click and drag hello tile you want toomove, and move it toowhere you want your tile toobe.</span></span>

![Упорядочение панели мониторинга](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="91f89-153">Удаление плитки</span><span class="sxs-lookup"><span data-stu-id="91f89-153">Remove a tile</span></span>
<span data-ttu-id="91f89-154">tooremove плитки, перейдите в представление toohello Моя панель мониторинга и нажмите кнопку **Настройка** tooenter режим настройки.</span><span class="sxs-lookup"><span data-stu-id="91f89-154">tooremove a tile, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="91f89-155">Плитка приветствия выберите tooremove и нажмите на правой панели hello выберите **удалить плитку**.</span><span class="sxs-lookup"><span data-stu-id="91f89-155">Select hello tile you want tooremove, then on hello right panel select **Remove Tile**.</span></span>

![Удаление плитки](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="91f89-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="91f89-157">Next steps</span></span>
* <span data-ttu-id="91f89-158">Создание [оповещения](log-analytics-alerts.md) в уведомлениях toogenerate анализа журналов и tooremediate проблем.</span><span class="sxs-lookup"><span data-stu-id="91f89-158">Create [alerts](log-analytics-alerts.md) in Log Analytics toogenerate notifications and tooremediate problems.</span></span>
