---
title: "Мониторинг конвейеров данных и управление ими в Azure | Документация Майкрософт"
description: "Узнайте, как отслеживать фабрики данных и конвейеры Azure и управлять ими с помощью приложения для мониторинга и управления."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: d5a2d1f3d85b8a2212326cfcfd0ba5d80356b769
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-monitoring-and-management-app"></a><span data-ttu-id="dba0e-103">Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения для мониторинга и управления</span><span class="sxs-lookup"><span data-stu-id="dba0e-103">Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dba0e-104">Использование портала Azure или Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dba0e-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="dba0e-105">Использование приложения для мониторинга и управления</span><span class="sxs-lookup"><span data-stu-id="dba0e-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="dba0e-106">В этой статье описывается, как с помощью приложения для мониторинга и управления отслеживать конвейеры фабрики данных, управлять ими и выполнять их отладку.</span><span class="sxs-lookup"><span data-stu-id="dba0e-106">This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="dba0e-107">В ней также приводятся инструкции по настройке оповещений в случае сбоев.</span><span class="sxs-lookup"><span data-stu-id="dba0e-107">It also provides information on how to create alerts to get notified on failures.</span></span> <span data-ttu-id="dba0e-108">Вы можете начать работу с приложением, посмотрев следующее видео:</span><span class="sxs-lookup"><span data-stu-id="dba0e-108">You can get started with using the application by watching the following video:</span></span>

> [!NOTE]
> <span data-ttu-id="dba0e-109">Пользовательский интерфейс, показанный в видео, может не соответствовать тому, который отображается на портале.</span><span class="sxs-lookup"><span data-stu-id="dba0e-109">The user interface shown in the video may not exactly match what you see in the portal.</span></span> <span data-ttu-id="dba0e-110">Он немного старше, но основные понятия остаются неизменными.</span><span class="sxs-lookup"><span data-stu-id="dba0e-110">It's slightly older, but concepts remain the same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-the-monitoring-and-management-app"></a><span data-ttu-id="dba0e-111">Запуск приложения для мониторинга и управления</span><span class="sxs-lookup"><span data-stu-id="dba0e-111">Launch the Monitoring and Management app</span></span>
<span data-ttu-id="dba0e-112">Чтобы открыть приложение для мониторинга и управления, щелкните элемент **Monitor & Manage** (Мониторинг и управление) в колонке **Фабрика данных** для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="dba0e-112">To launch the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.</span></span>

![Элемент "Мониторинг" на домашней странице фабрики данных](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="dba0e-114">Приложение для мониторинга и управления откроется в отдельном окне.</span><span class="sxs-lookup"><span data-stu-id="dba0e-114">You should see the Monitoring and Management app open in a separate window.</span></span>  

![Приложение для мониторинга и управления](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="dba0e-116">Если веб-браузер завис на действии "Авторизация...", то снимите флажок **Block third-party cookies and site data** (Блокировать сторонние файлы cookie и данные сайта). Либо оставьте флажок и создайте исключение для адреса **login.microsoftonline.com**, а затем попробуйте открыть приложение еще раз.</span><span class="sxs-lookup"><span data-stu-id="dba0e-116">If you see that the web browser is stuck at "Authorizing...", clear the **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try to open the app again.</span></span>


<span data-ttu-id="dba0e-117">В средней области списка "Activity Windows" (Окна действий) появится окно действия для каждого действия запуска.</span><span class="sxs-lookup"><span data-stu-id="dba0e-117">In the Activity Windows list in the middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="dba0e-118">Например, при наличии действия запланированного ежечасно в течение пяти часов, вы увидите пять окон действий, связанные с пятью срезами данных.</span><span class="sxs-lookup"><span data-stu-id="dba0e-118">For example, if you have the activity scheduled to run hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="dba0e-119">Если вы не видите окон действий внизу списка, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="dba0e-119">If you don't see activity windows in the list at the bottom, do the following:</span></span>
 
- <span data-ttu-id="dba0e-120">Обновите фильтры **время начала** и **время окончания** в верхней части, чтобы они соответствовали времени начала и окончания конвейера, а затем нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="dba0e-120">Update the **start time** and **end time** filters at the top to match the start and end times of your pipeline, and then click the **Apply** button.</span></span>  
- <span data-ttu-id="dba0e-121">Список "Activity Windows" (Окна действий) не обновляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="dba0e-121">The Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="dba0e-122">Нажмите кнопку **Обновить** на панели инструментов в списке **Activity Windows** (Окна действий).</span><span class="sxs-lookup"><span data-stu-id="dba0e-122">Click the **Refresh** button on the toolbar in the **Activity Windows** list.</span></span>  

<span data-ttu-id="dba0e-123">Если у вас нет приложения фабрики данных , чтобы протестировать эти действия, см. статью [Руководство. Копирование данных из хранилища BLOB-объектов Azure в базу данных SQL с помощью фабрики данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="dba0e-123">If you don't have a Data Factory application to test these steps with, do the tutorial: [copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-the-monitoring-and-management-app"></a><span data-ttu-id="dba0e-124">Общие сведения о приложении для мониторинга и управления</span><span class="sxs-lookup"><span data-stu-id="dba0e-124">Understand the Monitoring and Management app</span></span>
<span data-ttu-id="dba0e-125">В левой части находятся три вкладки (**Обозреватель ресурсов**, **Monitoring Views** (Представления мониторинга) и **Оповещения**).</span><span class="sxs-lookup"><span data-stu-id="dba0e-125">There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="dba0e-126">Первая вкладка (**Обозреватель ресурсов**) выбрана по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dba0e-126">The first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="dba0e-127">Обозреватель ресурсов</span><span class="sxs-lookup"><span data-stu-id="dba0e-127">Resource Explorer</span></span>
<span data-ttu-id="dba0e-128">Отображается следующее:</span><span class="sxs-lookup"><span data-stu-id="dba0e-128">You see the following:</span></span>

* <span data-ttu-id="dba0e-129">**представление в виде дерева** обозревателя ресурсов в левой области;</span><span class="sxs-lookup"><span data-stu-id="dba0e-129">The Resource Explorer **tree view** in the left pane.</span></span>
* <span data-ttu-id="dba0e-130">**Представление схемы** вверху средней области.</span><span class="sxs-lookup"><span data-stu-id="dba0e-130">The **Diagram View** at the top in the middle pane.</span></span>
* <span data-ttu-id="dba0e-131">список **Activity Windows** (Окна действий) внизу средней области;</span><span class="sxs-lookup"><span data-stu-id="dba0e-131">The **Activity Windows** list at the bottom in the middle pane.</span></span>
* <span data-ttu-id="dba0e-132">Вкладки **Свойства**, **Activity Window Explorer** (Обозреватель окон действий) и **Скрипт** в правой области.</span><span class="sxs-lookup"><span data-stu-id="dba0e-132">The **Properties**, **Activity Window Explorer**, and **Script** tabs in the right pane.</span></span>

<span data-ttu-id="dba0e-133">В обозревателе ресурсов все ресурсы (конвейеры, наборы данных, связанные службы) в фабрике данных отображаются в представлении в виде дерева.</span><span class="sxs-lookup"><span data-stu-id="dba0e-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view.</span></span> <span data-ttu-id="dba0e-134">При выборе объекта в обозревателе ресурсов вы заметите следующее:</span><span class="sxs-lookup"><span data-stu-id="dba0e-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="dba0e-135">связанная сущность фабрики данных выделена в представлении схемы;</span><span class="sxs-lookup"><span data-stu-id="dba0e-135">The associated Data Factory entity is highlighted in the Diagram View.</span></span>
* <span data-ttu-id="dba0e-136">[связанные окна действий](data-factory-scheduling-and-execution.md) выделены в списке "Activity Windows" (Окна действий) внизу;</span><span class="sxs-lookup"><span data-stu-id="dba0e-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.</span></span>  
* <span data-ttu-id="dba0e-137">свойства выбранного объекта отображаются в окне "Свойства" в правой области;</span><span class="sxs-lookup"><span data-stu-id="dba0e-137">The properties of the selected object are shown in the Properties window in the right pane.</span></span>
* <span data-ttu-id="dba0e-138">отображается определение JSON выбранного объекта, если это применимо</span><span class="sxs-lookup"><span data-stu-id="dba0e-138">The JSON definition of the selected object is shown, if applicable.</span></span> <span data-ttu-id="dba0e-139">(например: связанная служба, набор данных или конвейер).</span><span class="sxs-lookup"><span data-stu-id="dba0e-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Обозреватель ресурсов](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="dba0e-141">Дополнительные сведения об окнах действий см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="dba0e-141">See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="dba0e-142">Представление схемы</span><span class="sxs-lookup"><span data-stu-id="dba0e-142">Diagram View</span></span>
<span data-ttu-id="dba0e-143">Представление схемы позволяет отслеживать состояние фабрики данных и всех ее ресурсов, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="dba0e-143">The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets.</span></span> <span data-ttu-id="dba0e-144">При выборе сущности фабрики данных (набора данных или конвейера) в представлении схемы вы заметите следующее:</span><span class="sxs-lookup"><span data-stu-id="dba0e-144">When you select a Data Factory entity (dataset/pipeline) in the Diagram View:</span></span>

* <span data-ttu-id="dba0e-145">сущность фабрики данных выбрана в представлении в виде дерева;</span><span class="sxs-lookup"><span data-stu-id="dba0e-145">The data factory entity is selected in the tree view.</span></span>
* <span data-ttu-id="dba0e-146">связанные окна действий выделены в списке "Activity Windows" (Окна действий);</span><span class="sxs-lookup"><span data-stu-id="dba0e-146">The associated activity windows are highlighted in the Activity Windows list.</span></span>
* <span data-ttu-id="dba0e-147">свойства выбранного объекта отображаются в окне "Свойства".</span><span class="sxs-lookup"><span data-stu-id="dba0e-147">The properties of the selected object are shown in the Properties window.</span></span>

<span data-ttu-id="dba0e-148">Если конвейер включен (не находится в приостановленном состоянии), то он отображается с зеленой линией:</span><span class="sxs-lookup"><span data-stu-id="dba0e-148">When the pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Выполняющийся конвейер](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="dba0e-150">Конвейер можно приостановить, возобновить или завершить, выбрав его в представлении схемы, а также с помощью кнопок на панели команд.</span><span class="sxs-lookup"><span data-stu-id="dba0e-150">You can pause, resume, or terminate a pipeline by selecting it in the diagram view and using the buttons on the command bar.</span></span>

![Приостановка или возобновление на панели команд](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="dba0e-152">В представлении схемы для конвейера доступны три кнопки панели команд.</span><span class="sxs-lookup"><span data-stu-id="dba0e-152">There are three command bar buttons for the pipeline in the Diagram View.</span></span> <span data-ttu-id="dba0e-153">Вторая кнопка используется для приостановки конвейера.</span><span class="sxs-lookup"><span data-stu-id="dba0e-153">You can use the second button to pause the pipeline.</span></span> <span data-ttu-id="dba0e-154">Во время приостановки текущие выполняющиеся действия не останавливаются, а завершаются до конца.</span><span class="sxs-lookup"><span data-stu-id="dba0e-154">Pausing doesn't terminate the currently running activities and lets them proceed to completion.</span></span> <span data-ttu-id="dba0e-155">Третья кнопка используется для приостановки конвейера и завершения текущих выполняющихся действий.</span><span class="sxs-lookup"><span data-stu-id="dba0e-155">The third button pauses the pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="dba0e-156">Первая кнопка позволяет возобновить работу конвейера.</span><span class="sxs-lookup"><span data-stu-id="dba0e-156">The first button resumes the pipeline.</span></span> <span data-ttu-id="dba0e-157">Если конвейер приостановлен, его цвет меняется:</span><span class="sxs-lookup"><span data-stu-id="dba0e-157">When your pipeline is paused, the color of the pipeline changes.</span></span> <span data-ttu-id="dba0e-158">Например, приостановленный конвейер выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dba0e-158">For example, a paused pipeline looks like in the following image:</span></span> 

![Приостановленный конвейер](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="dba0e-160">С помощью клавиши Ctrl можно выбрать два конвейера или более.</span><span class="sxs-lookup"><span data-stu-id="dba0e-160">You can multi-select two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="dba0e-161">С помощью кнопок панели команд можно приостанавливать или возобновлять работу нескольких конвейеров одновременно.</span><span class="sxs-lookup"><span data-stu-id="dba0e-161">You can use the command bar buttons to pause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="dba0e-162">Кроме того, можно щелкнуть конвейер правой кнопкой мыши и выбрать параметры, чтобы приостановить, возобновить или завершить его работу.</span><span class="sxs-lookup"><span data-stu-id="dba0e-162">You can also right-click a pipeline and select options to suspend, resume, or terminate a pipeline.</span></span> 

![Контекстное меню конвейера](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="dba0e-164">Выберите параметр **Открыть конвейер**, чтобы просмотреть все действия в конвейере.</span><span class="sxs-lookup"><span data-stu-id="dba0e-164">Click the **Open pipeline** option to see all the activities in the pipeline.</span></span> 

![Откройте меню конвейера](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="dba0e-166">В открывшемся представлении конвейера вы увидите все действия в конвейере.</span><span class="sxs-lookup"><span data-stu-id="dba0e-166">In the opened pipeline view, you see all activities in the pipeline.</span></span> <span data-ttu-id="dba0e-167">В этом примере в конвейере существует только одно действие — действие копирования.</span><span class="sxs-lookup"><span data-stu-id="dba0e-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Открытый конвейер](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="dba0e-169">Чтобы перейти к предыдущему представлению, щелкните имя фабрики данных в меню навигации вверху.</span><span class="sxs-lookup"><span data-stu-id="dba0e-169">To go back to the previous view, click the data factory name in the breadcrumb menu at the top.</span></span>

<span data-ttu-id="dba0e-170">При щелчке выходного набора данных или наведении на него указателя мыши в представлении конвейера отобразится всплывающее окно "Activity Windows" (Окна действий) для этого набора данных.</span><span class="sxs-lookup"><span data-stu-id="dba0e-170">In the pipeline view, when you select an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.</span></span>

![Всплывающее окно "Activity Windows" (Окна действий)](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="dba0e-172">Щелкните окно действий, чтобы просмотреть сведения о нем в окне **Свойства** в правой области.</span><span class="sxs-lookup"><span data-stu-id="dba0e-172">You can click an activity window to see details for it in the **Properties** window in the right pane.</span></span>

![Свойства окна действий](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="dba0e-174">Чтобы просмотреть дополнительные сведения, в правой области перейдите на вкладку **Activity Window Explorer** (Обозреватель окон действий).</span><span class="sxs-lookup"><span data-stu-id="dba0e-174">In the right pane, switch to the **Activity Window Explorer** tab to see more details.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="dba0e-176">Вы также увидите **разрешенные переменные** для каждой попытки запуска действия в разделе **Попытки**.</span><span class="sxs-lookup"><span data-stu-id="dba0e-176">You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.</span></span>

![Разрешенные переменные](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="dba0e-178">Перейдите на вкладку **Скрипт** , чтобы просмотреть определение скриптов JSON для выбранного объекта.</span><span class="sxs-lookup"><span data-stu-id="dba0e-178">Switch to the **Script** tab to see the JSON script definition for the selected object.</span></span>   

![Вкладка "Скрипт"](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="dba0e-180">Окна действий можно просматривать в трех местах:</span><span class="sxs-lookup"><span data-stu-id="dba0e-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="dba0e-181">всплывающее окно "Activity Windows" (Окна действий) в представлении схемы (средняя область);</span><span class="sxs-lookup"><span data-stu-id="dba0e-181">The Activity Windows pop-up in the Diagram View (middle pane).</span></span>
* <span data-ttu-id="dba0e-182">"Activity Window Explorer" (Обозреватель окон действий) в правой области;</span><span class="sxs-lookup"><span data-stu-id="dba0e-182">The Activity Window Explorer in the right pane.</span></span>
* <span data-ttu-id="dba0e-183">список "Activity Windows" (Окна действий) в нижней области.</span><span class="sxs-lookup"><span data-stu-id="dba0e-183">The Activity Windows list in the bottom pane.</span></span>

<span data-ttu-id="dba0e-184">Во всплывающем окне "Activity Windows" (Окна действий) и на вкладке "Activity Window Explorer" (Обозреватель окон действий) можно перейти к прошлой и следующей неделям, используя кнопки со стрелками влево и вправо.</span><span class="sxs-lookup"><span data-stu-id="dba0e-184">In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.</span></span>

![Кнопки со стрелками вправо и влево в "Activity Window Explorer" (Обозреватель окон действий)](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="dba0e-186">В нижней части представления схемы находятся такие кнопки: увеличение и уменьшение масштаба, выбор 100-процентного масштаба, масштаба по размеру и блокировки структуры схемы.</span><span class="sxs-lookup"><span data-stu-id="dba0e-186">At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="dba0e-187">Кнопка **блокировки структуры** позволяет предотвратить случайное перемещение таблиц и конвейеров в представлении схемы.</span><span class="sxs-lookup"><span data-stu-id="dba0e-187">The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View.</span></span> <span data-ttu-id="dba0e-188">Она включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dba0e-188">It's on by default.</span></span> <span data-ttu-id="dba0e-189">Ее можно отключить и перемещать объекты в рамках схемы.</span><span class="sxs-lookup"><span data-stu-id="dba0e-189">You can turn it off and move entities around in the diagram.</span></span> <span data-ttu-id="dba0e-190">Если кнопка отключена, то для автоматического размещения таблиц и конвейеров можно использовать последнюю кнопку.</span><span class="sxs-lookup"><span data-stu-id="dba0e-190">When you turn it off, you can use the last button to automatically position tables and pipelines.</span></span> <span data-ttu-id="dba0e-191">Также можно увеличить или уменьшить масштаб с помощью колесика мыши.</span><span class="sxs-lookup"><span data-stu-id="dba0e-191">You can also zoom in or out by using the mouse wheel.</span></span>

![Команды изменения масштаба в представлении схемы](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="dba0e-193">Список "Activity Windows" (Окна действий)</span><span class="sxs-lookup"><span data-stu-id="dba0e-193">Activity Windows list</span></span>
<span data-ttu-id="dba0e-194">В списке "Activity Windows" (Окна действий) в нижней части средней области отображаются все окна действий для набора данных, выбранного в обозревателе ресурсов или представлении схемы.</span><span class="sxs-lookup"><span data-stu-id="dba0e-194">The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View.</span></span> <span data-ttu-id="dba0e-195">По умолчанию список отсортирован по убыванию. Это значит, что в его верхней части находится самое последнее окно действий.</span><span class="sxs-lookup"><span data-stu-id="dba0e-195">By default, the list is in descending order, which means that you see the latest activity window at the top.</span></span>

![Список "Activity Windows" (Окна действий)](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="dba0e-197">Этот список не обновляется автоматически, поэтому воспользуйтесь кнопкой "Обновить" на панели инструментов, чтобы обновить его вручную.</span><span class="sxs-lookup"><span data-stu-id="dba0e-197">This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.</span></span>  

<span data-ttu-id="dba0e-198">Окна действий могут находиться в одном из указанных ниже состояний.</span><span class="sxs-lookup"><span data-stu-id="dba0e-198">Activity windows can be in one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="dba0e-199">Состояние</span><span class="sxs-lookup"><span data-stu-id="dba0e-199">Status</span></span></th><th align="left"><span data-ttu-id="dba0e-200">Подсостояние</span><span class="sxs-lookup"><span data-stu-id="dba0e-200">Substatus</span></span></th><th align="left"><span data-ttu-id="dba0e-201">Описание</span><span class="sxs-lookup"><span data-stu-id="dba0e-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="dba0e-202">Waiting</span><span class="sxs-lookup"><span data-stu-id="dba0e-202">Waiting</span></span></td><td><span data-ttu-id="dba0e-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="dba0e-203">ScheduleTime</span></span></td><td><span data-ttu-id="dba0e-204">Время выполнения окна действий еще не наступило.</span><span class="sxs-lookup"><span data-stu-id="dba0e-204">The time hasn't come for the activity window to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="dba0e-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="dba0e-205">DatasetDependencies</span></span></td><td><span data-ttu-id="dba0e-206">Восходящие зависимости не готовы.</span><span class="sxs-lookup"><span data-stu-id="dba0e-206">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="dba0e-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="dba0e-207">ComputeResources</span></span></td><td><span data-ttu-id="dba0e-208">Вычислительные ресурсы недоступны.</span><span class="sxs-lookup"><span data-stu-id="dba0e-208">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="dba0e-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="dba0e-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="dba0e-210">Все экземпляры действия заняты выполнением других окон действий.</span><span class="sxs-lookup"><span data-stu-id="dba0e-210">All the activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="dba0e-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="dba0e-211">ActivityResume</span></span></td><td><span data-ttu-id="dba0e-212">Действие приостановлено, и до его возобновления выполнение окон действий недоступно.</span><span class="sxs-lookup"><span data-stu-id="dba0e-212">The activity is paused and can't run the activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="dba0e-213">Retry</span><span class="sxs-lookup"><span data-stu-id="dba0e-213">Retry</span></span></td><td><span data-ttu-id="dba0e-214">Действие выполняется повторно.</span><span class="sxs-lookup"><span data-stu-id="dba0e-214">The activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="dba0e-215">Проверка</span><span class="sxs-lookup"><span data-stu-id="dba0e-215">Validation</span></span></td><td><span data-ttu-id="dba0e-216">Проверка еще не начата.</span><span class="sxs-lookup"><span data-stu-id="dba0e-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="dba0e-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="dba0e-217">ValidationRetry</span></span></td><td><span data-ttu-id="dba0e-218">Ожидание повторения проверки.</span><span class="sxs-lookup"><span data-stu-id="dba0e-218">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="dba0e-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="dba0e-219">InProgress</span></span></td><td><span data-ttu-id="dba0e-220">Validating</span><span class="sxs-lookup"><span data-stu-id="dba0e-220">Validating</span></span></td><td><span data-ttu-id="dba0e-221">Проверка выполняется.</span><span class="sxs-lookup"><span data-stu-id="dba0e-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="dba0e-222">Выполняется обработка окна действия.</span><span class="sxs-lookup"><span data-stu-id="dba0e-222">The activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="dba0e-223">Сбой</span><span class="sxs-lookup"><span data-stu-id="dba0e-223">Failed</span></span></td><td><span data-ttu-id="dba0e-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="dba0e-224">TimedOut</span></span></td><td><span data-ttu-id="dba0e-225">Выполнение действия заняло больше времени, чем разрешено для данного действия.</span><span class="sxs-lookup"><span data-stu-id="dba0e-225">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="dba0e-226">Canceled</span><span class="sxs-lookup"><span data-stu-id="dba0e-226">Canceled</span></span></td><td><span data-ttu-id="dba0e-227">Окно действий отменено пользователем.</span><span class="sxs-lookup"><span data-stu-id="dba0e-227">The activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="dba0e-228">Проверка</span><span class="sxs-lookup"><span data-stu-id="dba0e-228">Validation</span></span></td><td><span data-ttu-id="dba0e-229">Сбой проверки.</span><span class="sxs-lookup"><span data-stu-id="dba0e-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="dba0e-230">Не удалось создать или проверить окно действий.</span><span class="sxs-lookup"><span data-stu-id="dba0e-230">The activity window failed to be generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="dba0e-231">Ready</span><span class="sxs-lookup"><span data-stu-id="dba0e-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="dba0e-232">Окно действия готово к использованию.</span><span class="sxs-lookup"><span data-stu-id="dba0e-232">The activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="dba0e-233">Skipped</span><span class="sxs-lookup"><span data-stu-id="dba0e-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="dba0e-234">Окно действий не обработано.</span><span class="sxs-lookup"><span data-stu-id="dba0e-234">The activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="dba0e-235">Без блокировки</span><span class="sxs-lookup"><span data-stu-id="dba0e-235">None</span></span></td><td>-</td><td><span data-ttu-id="dba0e-236">Окно действий, которое ранее существовало с другим состоянием, но было сброшено.</span><span class="sxs-lookup"><span data-stu-id="dba0e-236">An activity window used to exist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="dba0e-237">При выборе окна действий в списке вы увидите сведения о нем на вкладке **Activity Windows Explorer** (Обозреватель окон действий) или в окне **Свойства** справа.</span><span class="sxs-lookup"><span data-stu-id="dba0e-237">When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="dba0e-239">Обновление окон действий</span><span class="sxs-lookup"><span data-stu-id="dba0e-239">Refresh activity windows</span></span>
<span data-ttu-id="dba0e-240">Данные не обновляются автоматически, поэтому воспользуйтесь кнопкой "Обновить" (вторая по счету) на панели команд, чтобы обновить список окон действий вручную.</span><span class="sxs-lookup"><span data-stu-id="dba0e-240">The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="dba0e-241">Окно "Свойства"</span><span class="sxs-lookup"><span data-stu-id="dba0e-241">Properties window</span></span>
<span data-ttu-id="dba0e-242">Окно "Свойства" доступно в правой области приложения по мониторингу и управлению.</span><span class="sxs-lookup"><span data-stu-id="dba0e-242">The Properties window is in the right-most pane of the Monitoring and Management app.</span></span>

![Окно "Свойства"](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="dba0e-244">В нем отображаются свойства элемента, выбранного в обозревателе ресурсов (в представлении в виде дерева), представлении схемы или списке "Activity Windows" (Окна действий).</span><span class="sxs-lookup"><span data-stu-id="dba0e-244">It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="dba0e-245">Activity Window Explorer</span><span class="sxs-lookup"><span data-stu-id="dba0e-245">Activity Window Explorer</span></span>
<span data-ttu-id="dba0e-246">Окно **Activity Window Explorer** (Обозреватель окон действий) находится в правой области приложения для мониторинга и управления.</span><span class="sxs-lookup"><span data-stu-id="dba0e-246">The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app.</span></span> <span data-ttu-id="dba0e-247">В нем отображаются сведения об окне действий, выбранном во всплывающем окне или списке Activity Windows (Окна действий).</span><span class="sxs-lookup"><span data-stu-id="dba0e-247">It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="dba0e-249">Вы можете переключиться между окнами действий, щелкнув нужное окно в представлении календаря в верхней части.</span><span class="sxs-lookup"><span data-stu-id="dba0e-249">You can switch to another activity window by clicking it in the calendar view at the top.</span></span> <span data-ttu-id="dba0e-250">Чтобы просмотреть окна действий за прошлую или следующую неделю, используйте кнопки со стрелками влево и вправо в верхней части.</span><span class="sxs-lookup"><span data-stu-id="dba0e-250">You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.</span></span>

<span data-ttu-id="dba0e-251">Чтобы повторно выполнить окно действий или обновить сведения, используйте кнопки панели инструментов в нижней области.</span><span class="sxs-lookup"><span data-stu-id="dba0e-251">You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.</span></span>

### <a name="script"></a><span data-ttu-id="dba0e-252">Скрипт</span><span class="sxs-lookup"><span data-stu-id="dba0e-252">Script</span></span>
<span data-ttu-id="dba0e-253">Откройте вкладку **Скрипт**, чтобы просмотреть определение JSON выбранной сущности фабрики данных (связанную службу, набор данных или конвейер).</span><span class="sxs-lookup"><span data-stu-id="dba0e-253">You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Вкладка "Скрипт"](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="dba0e-255">Использование системных представлений</span><span class="sxs-lookup"><span data-stu-id="dba0e-255">Use system views</span></span>
<span data-ttu-id="dba0e-256">Приложение для мониторинга и управления содержит встроенные системные представления (**Recent activity windows** (Последние окна действий), **Failed activity windows** (Ошибки окон действий), **In-Progress activity windows** (Выполняющиеся окна действий)), которые позволяют просматривать последние, завершившиеся ошибкой или выполняющиеся окна действий для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="dba0e-256">The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="dba0e-257">В левой части откройте вкладку **Monitoring Views** (Представления мониторинга), щелкнув ее.</span><span class="sxs-lookup"><span data-stu-id="dba0e-257">Switch to the **Monitoring Views** tab on the left by clicking it.</span></span>

![Вкладка "Представления мониторинга"](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="dba0e-259">В настоящее время поддерживаются три системных представления.</span><span class="sxs-lookup"><span data-stu-id="dba0e-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="dba0e-260">Выберите, какие именно окна будут отображаться в списке "Activity Windows" (Окна действий) (в нижней части средней области) — последние, завершившиеся ошибкой или выполняющиеся.</span><span class="sxs-lookup"><span data-stu-id="dba0e-260">Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).</span></span>

<span data-ttu-id="dba0e-261">При выборе варианта **Recent activity windows** (Последние окна действий) будут отображены все последние окна действий в порядке убывания по **времени последней попытки**.</span><span class="sxs-lookup"><span data-stu-id="dba0e-261">When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.</span></span>

<span data-ttu-id="dba0e-262">В представлении **Failed activity windows** (Ошибки окон действий) в списке отображаются все завершившиеся ошибкой окна действий.</span><span class="sxs-lookup"><span data-stu-id="dba0e-262">You can use the **Failed activity windows** view to see all failed activity windows in the list.</span></span> <span data-ttu-id="dba0e-263">Выберите в списке окно действий, завершившееся ошибкой, чтобы просмотреть подробные сведения о нем в окне **Свойства** или в **Activity Window Explorer** (Обозреватель окон действий).</span><span class="sxs-lookup"><span data-stu-id="dba0e-263">Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**.</span></span> <span data-ttu-id="dba0e-264">Можно также загрузить журналы для завершившегося ошибкой окна действия.</span><span class="sxs-lookup"><span data-stu-id="dba0e-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="dba0e-265">Сортировка и фильтрация окон действий</span><span class="sxs-lookup"><span data-stu-id="dba0e-265">Sort and filter activity windows</span></span>
<span data-ttu-id="dba0e-266">Чтобы отфильтровать окна действий, измените значение параметров **Время начала** и **Время окончания** в командной строке.</span><span class="sxs-lookup"><span data-stu-id="dba0e-266">Change the **start time** and **end time** settings in the command bar to filter activity windows.</span></span> <span data-ttu-id="dba0e-267">После изменения времени начала и окончания нажмите кнопку рядом с параметром "Время окончания", чтобы обновить список "Activity Windows" (Окна действий).</span><span class="sxs-lookup"><span data-stu-id="dba0e-267">After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.</span></span>

![Время начала и окончания](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="dba0e-269">Сейчас в приложении для мониторинга и управления все значения времени указываются в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="dba0e-269">Currently, all times are in UTC format in the Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="dba0e-270">В **списке окон действий**щелкните имя столбца (например, "Состояние").</span><span class="sxs-lookup"><span data-stu-id="dba0e-270">In the **Activity Windows list**, click the name of a column (for example: Status).</span></span>

![Меню столбца списка "Activity Windows" (Окна действий)](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="dba0e-272">Можно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="dba0e-272">You can do the following:</span></span>

* <span data-ttu-id="dba0e-273">отсортировать по возрастанию;</span><span class="sxs-lookup"><span data-stu-id="dba0e-273">Sort in ascending order.</span></span>
* <span data-ttu-id="dba0e-274">отсортировать по убыванию;</span><span class="sxs-lookup"><span data-stu-id="dba0e-274">Sort in descending order.</span></span>
* <span data-ttu-id="dba0e-275">отфильтровать по одному или нескольким значениям ("Готово", "Ожидание" и т. д.).</span><span class="sxs-lookup"><span data-stu-id="dba0e-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="dba0e-276">После выбора фильтра в столбце активируется кнопка "Фильтр", указывающая, что значения в столбце являются отфильтрованными.</span><span class="sxs-lookup"><span data-stu-id="dba0e-276">When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.</span></span>

![Фильтр в столбце списка "Activity Windows" (Окна действий)](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="dba0e-278">Чтобы очистить фильтры, можно использовать то же самое всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="dba0e-278">You can use the same pop-up window to clear filters.</span></span> <span data-ttu-id="dba0e-279">Чтобы очистить все фильтры для списка "Activity Windows" (Окна действий), нажмите кнопку очистки фильтров на панели команд.</span><span class="sxs-lookup"><span data-stu-id="dba0e-279">To clear all filters for the Activity Windows list, click the clear filter button on the command bar.</span></span>

![Очистка всех фильтров для списка "Activity Windows" (Окна действий)](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="dba0e-281">Выполнение пакетных действий</span><span class="sxs-lookup"><span data-stu-id="dba0e-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="dba0e-282">Повторное выполнение выбранных окон действий</span><span class="sxs-lookup"><span data-stu-id="dba0e-282">Rerun selected activity windows</span></span>
<span data-ttu-id="dba0e-283">Выберите окно действий, нажмите кнопку со стрелкой вниз (первая кнопка на панели команд) и выберите **Выполнить снова** или  / **Rerun with upstream in pipeline** (Повторно выполнить с параметром UpstreamInPipeline).</span><span class="sxs-lookup"><span data-stu-id="dba0e-283">Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="dba0e-284">При выборе варианта **Rerun with upstream in pipeline** (Повторно выполнить с параметром UpstreamInPipeline) также будут выполнены все вышестоящие окна действий.</span><span class="sxs-lookup"><span data-stu-id="dba0e-284">When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="dba0e-285">![Повторное выполнение окна действия](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="dba0e-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="dba0e-286">Кроме того, в списке можно выбрать несколько окон действий и повторно выполнить сразу все эти окна.</span><span class="sxs-lookup"><span data-stu-id="dba0e-286">You can also select multiple activity windows in the list and rerun them at the same time.</span></span> <span data-ttu-id="dba0e-287">Вы можете отфильтровать окна действий на основе состояния (например, **Сбой**), а после устранения причины сбоя выполнить окна действий повторно.</span><span class="sxs-lookup"><span data-stu-id="dba0e-287">You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail.</span></span> <span data-ttu-id="dba0e-288">Дополнительные сведения о фильтрации окон действий см. в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="dba0e-288">See the following section for details about filtering activity windows in the list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="dba0e-289">Приостановка и возобновление нескольких конвейеров</span><span class="sxs-lookup"><span data-stu-id="dba0e-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="dba0e-290">С помощью клавиши Ctrl можно выбрать два конвейера или более.</span><span class="sxs-lookup"><span data-stu-id="dba0e-290">You can multiselect two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="dba0e-291">Чтобы приостановить или возобновить все эти конвейеры, можно воспользоваться кнопками на панели команд (на следующем снимке экрана выделены красным прямоугольником).</span><span class="sxs-lookup"><span data-stu-id="dba0e-291">You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.</span></span>

![Приостановка или возобновление на панели команд](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="dba0e-293">Создание оповещений</span><span class="sxs-lookup"><span data-stu-id="dba0e-293">Create alerts</span></span>
<span data-ttu-id="dba0e-294">На странице **Оповещения** можно создать оповещение, а также просмотреть, изменить или удалить имеющиеся оповещения.</span><span class="sxs-lookup"><span data-stu-id="dba0e-294">The **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="dba0e-295">Можно также включить или отключить оповещение.</span><span class="sxs-lookup"><span data-stu-id="dba0e-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="dba0e-296">Щелкните вкладку **Оповещения**, чтобы открыть страницу оповещений.</span><span class="sxs-lookup"><span data-stu-id="dba0e-296">To see the Alerts page, click the **Alerts** tab.</span></span>

![Вкладка "Оповещения"](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="to-create-an-alert"></a><span data-ttu-id="dba0e-298">Создание оповещения</span><span class="sxs-lookup"><span data-stu-id="dba0e-298">To create an alert</span></span>
1. <span data-ttu-id="dba0e-299">Чтобы добавить оповещение, нажмите кнопку **Добавить оповещение** .</span><span class="sxs-lookup"><span data-stu-id="dba0e-299">Click **Add Alert** to add an alert.</span></span> <span data-ttu-id="dba0e-300">Отобразится страница **Подробности**.</span><span class="sxs-lookup"><span data-stu-id="dba0e-300">You see the **Details** page.</span></span>

    ![Создание оповещений — страница "Сведения"](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="dba0e-302">Укажите **имя** и введите **описание** оповещения в соответствующих полях, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dba0e-302">Specify the **Name** and **Description** for the alert, and click **Next**.</span></span> <span data-ttu-id="dba0e-303">Должна открыться страница **Фильтры** .</span><span class="sxs-lookup"><span data-stu-id="dba0e-303">You should see the **Filters** page.</span></span>

    ![Создание оповещений — страница "Фильтры"](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="dba0e-305">Выберите **событие**, **состояние** и **подсостояние** (необязательно), о которых служба фабрики данных должна выводить оповещение, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="dba0e-305">Select the **event**, **status**, and **substatus** (optional) that you want to create a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="dba0e-306">Откроется страница **Получатели** .</span><span class="sxs-lookup"><span data-stu-id="dba0e-306">You should see the **Recipients** page.</span></span>

    ![Создание оповещений — страница "Получатели"](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="dba0e-308">Выберите параметр **Email subscription admins** (Администраторы подписки электронной почты) и (или) укажите значение параметра **Дополнительный адрес электронной почты администратора**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="dba0e-308">Select the **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="dba0e-309">Оповещение должно появиться в списке.</span><span class="sxs-lookup"><span data-stu-id="dba0e-309">You should see the alert in the list.</span></span>

    ![Список "Оповещения"](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="dba0e-311">В списке "Оповещения" используйте связанные с оповещением кнопки, чтобы изменить, удалить, включить или отключить оповещение.</span><span class="sxs-lookup"><span data-stu-id="dba0e-311">In the Alerts list, use the buttons that are associated with the alert to edit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="dba0e-312">Событие, состояние и подсостояние</span><span class="sxs-lookup"><span data-stu-id="dba0e-312">Event/status/substatus</span></span>
<span data-ttu-id="dba0e-313">В приведенной далее таблице содержится список возможных событий и состояний (и подсостояний).</span><span class="sxs-lookup"><span data-stu-id="dba0e-313">The following table provides the list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="dba0e-314">Имя события</span><span class="sxs-lookup"><span data-stu-id="dba0e-314">Event name</span></span> | <span data-ttu-id="dba0e-315">Состояние</span><span class="sxs-lookup"><span data-stu-id="dba0e-315">Status</span></span> | <span data-ttu-id="dba0e-316">Подсостояние</span><span class="sxs-lookup"><span data-stu-id="dba0e-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dba0e-317">Выполнение действия начато</span><span class="sxs-lookup"><span data-stu-id="dba0e-317">Activity Run Started</span></span> |<span data-ttu-id="dba0e-318">Started</span><span class="sxs-lookup"><span data-stu-id="dba0e-318">Started</span></span> |<span data-ttu-id="dba0e-319">Запуск</span><span class="sxs-lookup"><span data-stu-id="dba0e-319">Starting</span></span> |
| <span data-ttu-id="dba0e-320">Выполнение действия завершено</span><span class="sxs-lookup"><span data-stu-id="dba0e-320">Activity Run Finished</span></span> |<span data-ttu-id="dba0e-321">Успешно</span><span class="sxs-lookup"><span data-stu-id="dba0e-321">Succeeded</span></span> |<span data-ttu-id="dba0e-322">Успешно</span><span class="sxs-lookup"><span data-stu-id="dba0e-322">Succeeded</span></span> |
| <span data-ttu-id="dba0e-323">Выполнение действия завершено</span><span class="sxs-lookup"><span data-stu-id="dba0e-323">Activity Run Finished</span></span> |<span data-ttu-id="dba0e-324">Сбой</span><span class="sxs-lookup"><span data-stu-id="dba0e-324">Failed</span></span> |<span data-ttu-id="dba0e-325">Неудачное выделение ресурсов</span><span class="sxs-lookup"><span data-stu-id="dba0e-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="dba0e-326">Сбой при выполнении</span><span class="sxs-lookup"><span data-stu-id="dba0e-326">Failed Execution</span></span><br/><br/><span data-ttu-id="dba0e-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="dba0e-327">Timed Out</span></span><br/><br/><span data-ttu-id="dba0e-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="dba0e-328">Failed Validation</span></span><br/><br/><span data-ttu-id="dba0e-329">Abandoned</span><span class="sxs-lookup"><span data-stu-id="dba0e-329">Abandoned</span></span> |
| <span data-ttu-id="dba0e-330">Создание кластера HDI по запросу начато</span><span class="sxs-lookup"><span data-stu-id="dba0e-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="dba0e-331">Started</span><span class="sxs-lookup"><span data-stu-id="dba0e-331">Started</span></span> |-|
| <span data-ttu-id="dba0e-332">Кластер HDI по запросу успешно создан</span><span class="sxs-lookup"><span data-stu-id="dba0e-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="dba0e-333">Успешно</span><span class="sxs-lookup"><span data-stu-id="dba0e-333">Succeeded</span></span> |-|
| <span data-ttu-id="dba0e-334">Кластер HDI по запросу удален</span><span class="sxs-lookup"><span data-stu-id="dba0e-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="dba0e-335">Успешно</span><span class="sxs-lookup"><span data-stu-id="dba0e-335">Succeeded</span></span> |-|

### <a name="to-edit-delete-or-disable-an-alert"></a><span data-ttu-id="dba0e-336">Изменение, удаление или отключение оповещения</span><span class="sxs-lookup"><span data-stu-id="dba0e-336">To edit, delete, or disable an alert</span></span>

<span data-ttu-id="dba0e-337">Используйте следующие кнопки (выделены красным цветом), чтобы изменить, удалить или отключить оповещение.</span><span class="sxs-lookup"><span data-stu-id="dba0e-337">Use the following buttons (highlighted in red) to edit, delete, or disable an alert.</span></span>

![Кнопки оповещений](./media/data-factory-monitor-manage-app/AlertButtons.png)
