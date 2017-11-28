---
title: "aaaMonitor и управления ими конвейеры данных — Azure | Документы Microsoft"
description: "Узнайте, как toouse Здравствуйте, мониторинг и управление toomonitor приложения и управлять фабриками данных Azure и конвейеры."
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
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a><span data-ttu-id="b2b99-103">Мониторинг и управление ими конвейеров фабрики данных Azure с помощью приложения hello мониторинг и управление</span><span class="sxs-lookup"><span data-stu-id="b2b99-103">Monitor and manage Azure Data Factory pipelines by using hello Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2b99-104">Использование портала Azure или Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2b99-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="b2b99-105">Использование приложения для мониторинга и управления</span><span class="sxs-lookup"><span data-stu-id="b2b99-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="b2b99-106">В этой статье описывается toouse мониторинг и управление toomonitor приложения hello, управления и отладки конвейеров фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="b2b99-106">This article describes how toouse hello Monitoring and Management app toomonitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="b2b99-107">Он также содержит сведения по как toocreate предупреждения tooget уведомления об ошибках.</span><span class="sxs-lookup"><span data-stu-id="b2b99-107">It also provides information on how toocreate alerts tooget notified on failures.</span></span> <span data-ttu-id="b2b99-108">Вы можете начать с помощью приложения hello за просмотром hello следующие видео:</span><span class="sxs-lookup"><span data-stu-id="b2b99-108">You can get started with using hello application by watching hello following video:</span></span>

> [!NOTE]
> <span data-ttu-id="b2b99-109">пользовательский интерфейс Hello показано hello видео может не соответствовать отображаемые на портале hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-109">hello user interface shown in hello video may not exactly match what you see in hello portal.</span></span> <span data-ttu-id="b2b99-110">Это немного старше, но основные понятия остаются hello же.</span><span class="sxs-lookup"><span data-stu-id="b2b99-110">It's slightly older, but concepts remain hello same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a><span data-ttu-id="b2b99-111">Запустите приложение hello мониторинг и управление</span><span class="sxs-lookup"><span data-stu-id="b2b99-111">Launch hello Monitoring and Management app</span></span>
<span data-ttu-id="b2b99-112">hello toolaunch монитора и приложение для управления, нажмите кнопку hello **отслеживать состо & Управление** плитки приветствия **фабрики данных** колонку для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="b2b99-112">toolaunch hello Monitor and Management app, click hello **Monitor & Manage** tile on hello **Data Factory** blade for your data factory.</span></span>

![Мониторинг плитки на домашней странице hello фабрики данных](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="b2b99-114">Вы увидите мониторинг и управление приложение hello открыть в отдельном окне.</span><span class="sxs-lookup"><span data-stu-id="b2b99-114">You should see hello Monitoring and Management app open in a separate window.</span></span>  

![Приложение для мониторинга и управления](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="b2b99-116">При появлении этого веб-браузер hello застряла в «Авторизации...», снимите hello **блокировать сторонние файлы cookie и данным сайта** флажок--или он установлен, необходимо создать исключение для **login.microsoftonline.com** , а затем повторите попытку tooopen приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-116">If you see that hello web browser is stuck at "Authorizing...", clear hello **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try tooopen hello app again.</span></span>


<span data-ttu-id="b2b99-117">В списке действий Windows hello в средней области hello появится окно действия для каждого запуска действия.</span><span class="sxs-lookup"><span data-stu-id="b2b99-117">In hello Activity Windows list in hello middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="b2b99-118">Например при наличии toorun действие, запланированное hello каждый час на пять часов, см пять окон действий, связанных с пять срезы.</span><span class="sxs-lookup"><span data-stu-id="b2b99-118">For example, if you have hello activity scheduled toorun hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="b2b99-119">Если вы не видите окон действий в списке hello нижней hello, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="b2b99-119">If you don't see activity windows in hello list at hello bottom, do hello following:</span></span>
 
- <span data-ttu-id="b2b99-120">Обновление hello **время начала** и **время окончания** фильтров в верхнем toomatch hello hello запуска и завершения работы конвейера и нажмите кнопку hello **применить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b2b99-120">Update hello **start time** and **end time** filters at hello top toomatch hello start and end times of your pipeline, and then click hello **Apply** button.</span></span>  
- <span data-ttu-id="b2b99-121">Список действий Windows Hello не обновляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="b2b99-121">hello Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="b2b99-122">Щелкните hello **обновление** на инструментов hello в hello **действия Windows** списка.</span><span class="sxs-lookup"><span data-stu-id="b2b99-122">Click hello **Refresh** button on hello toolbar in hello **Activity Windows** list.</span></span>  

<span data-ttu-id="b2b99-123">При отсутствии tootest фабрики данных приложения следующие действия с, hello учебника: [копирования данных из хранилища больших двоичных объектов tooSQL базы данных с помощью фабрики данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b2b99-123">If you don't have a Data Factory application tootest these steps with, do hello tutorial: [copy data from Blob Storage tooSQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-hello-monitoring-and-management-app"></a><span data-ttu-id="b2b99-124">Понять, управление и мониторинг приложение hello</span><span class="sxs-lookup"><span data-stu-id="b2b99-124">Understand hello Monitoring and Management app</span></span>
<span data-ttu-id="b2b99-125">Есть три вкладки слева hello: **обозреватель ресурсов**, **представления мониторинга**, и **предупреждения**.</span><span class="sxs-lookup"><span data-stu-id="b2b99-125">There are three tabs on hello left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="b2b99-126">Первая вкладка Hello (**обозреватель ресурсов**) выбран по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b2b99-126">hello first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="b2b99-127">Обозреватель ресурсов</span><span class="sxs-lookup"><span data-stu-id="b2b99-127">Resource Explorer</span></span>
<span data-ttu-id="b2b99-128">Вы видите hello следующее:</span><span class="sxs-lookup"><span data-stu-id="b2b99-128">You see hello following:</span></span>

* <span data-ttu-id="b2b99-129">Обозреватель ресурсов Hello **представление в виде дерева** hello левой панели.</span><span class="sxs-lookup"><span data-stu-id="b2b99-129">hello Resource Explorer **tree view** in hello left pane.</span></span>
* <span data-ttu-id="b2b99-130">Hello **представление диаграммы** hello в в верхней части средней панели hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-130">hello **Diagram View** at hello top in hello middle pane.</span></span>
* <span data-ttu-id="b2b99-131">Hello **действия Windows** списке нижней hello в средней области hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-131">hello **Activity Windows** list at hello bottom in hello middle pane.</span></span>
* <span data-ttu-id="b2b99-132">Hello **свойства**, **действия окно обозревателя**, и **сценарий** вкладках в правой области hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-132">hello **Properties**, **Activity Window Explorer**, and **Script** tabs in hello right pane.</span></span>

<span data-ttu-id="b2b99-133">В обозревателе ресурсов можно просмотреть все ресурсы (конвейеры, наборы данных, связанных служб) в фабрике данных hello в виде дерева.</span><span class="sxs-lookup"><span data-stu-id="b2b99-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in hello data factory in a tree view.</span></span> <span data-ttu-id="b2b99-134">При выборе объекта в обозревателе ресурсов вы заметите следующее:</span><span class="sxs-lookup"><span data-stu-id="b2b99-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="b2b99-135">Hello связанные сущности, выделяется в представление диаграммы hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="b2b99-135">hello associated Data Factory entity is highlighted in hello Diagram View.</span></span>
* <span data-ttu-id="b2b99-136">[Связанные действия windows](data-factory-scheduling-and-execution.md) , выделяются в списке действий Windows hello нижней hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in hello Activity Windows list at hello bottom.</span></span>  
* <span data-ttu-id="b2b99-137">в окне свойств hello hello правой панели отображаются свойства Hello hello выбранного объекта.</span><span class="sxs-lookup"><span data-stu-id="b2b99-137">hello properties of hello selected object are shown in hello Properties window in hello right pane.</span></span>
* <span data-ttu-id="b2b99-138">Hello определения JSON hello выбранного объекта отображается, если это применимо.</span><span class="sxs-lookup"><span data-stu-id="b2b99-138">hello JSON definition of hello selected object is shown, if applicable.</span></span> <span data-ttu-id="b2b99-139">(например: связанная служба, набор данных или конвейер).</span><span class="sxs-lookup"><span data-stu-id="b2b99-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Обозреватель ресурсов](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="b2b99-141">В разделе hello [планирования и выполнения](data-factory-scheduling-and-execution.md) подробные Общие сведения о windows действия.</span><span class="sxs-lookup"><span data-stu-id="b2b99-141">See hello [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="b2b99-142">Представление схемы</span><span class="sxs-lookup"><span data-stu-id="b2b99-142">Diagram View</span></span>
<span data-ttu-id="b2b99-143">Hello фабрики данных представление схемы предоставляет единое toomonitor стекла и управление ими фабрику данных и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b2b99-143">hello Diagram View of a data factory provides a single pane of glass toomonitor and manage a data factory and its assets.</span></span> <span data-ttu-id="b2b99-144">При выборе сущности фабрики данных (dataset и конвейер) hello представление схемы:</span><span class="sxs-lookup"><span data-stu-id="b2b99-144">When you select a Data Factory entity (dataset/pipeline) in hello Diagram View:</span></span>

* <span data-ttu-id="b2b99-145">в древовидном представлении hello выбрана сущность фабрики данных Hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-145">hello data factory entity is selected in hello tree view.</span></span>
* <span data-ttu-id="b2b99-146">Hello связанные действия, который windows, выделяются в списке действий Windows hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-146">hello associated activity windows are highlighted in hello Activity Windows list.</span></span>
* <span data-ttu-id="b2b99-147">в окне свойств hello отображаются свойства Hello hello выбранного объекта.</span><span class="sxs-lookup"><span data-stu-id="b2b99-147">hello properties of hello selected object are shown in hello Properties window.</span></span>

<span data-ttu-id="b2b99-148">При включении конвейера hello (не в приостановленном состоянии), он отображается с зеленая линия:</span><span class="sxs-lookup"><span data-stu-id="b2b99-148">When hello pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Выполняющийся конвейер](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="b2b99-150">Можно приостановить, возобновить или завершить конвейера, выбрав его в представлении диаграммы hello и использование hello кнопок на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-150">You can pause, resume, or terminate a pipeline by selecting it in hello diagram view and using hello buttons on hello command bar.</span></span>

![Приостановить или возобновить на панели команд, hello](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="b2b99-152">Существуют три кнопки панели команд для конвейера hello в hello представление диаграммы.</span><span class="sxs-lookup"><span data-stu-id="b2b99-152">There are three command bar buttons for hello pipeline in hello Diagram View.</span></span> <span data-ttu-id="b2b99-153">Можно использовать hello вторая кнопка toopause hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="b2b99-153">You can use hello second button toopause hello pipeline.</span></span> <span data-ttu-id="b2b99-154">Приостановка не завершить hello, выполняемые действия и позволяет им продолжить toocompletion.</span><span class="sxs-lookup"><span data-stu-id="b2b99-154">Pausing doesn't terminate hello currently running activities and lets them proceed toocompletion.</span></span> <span data-ttu-id="b2b99-155">Третья кнопка Hello hello конвейера приостанавливает и прекращает работу своих существующих выполняемых действий.</span><span class="sxs-lookup"><span data-stu-id="b2b99-155">hello third button pauses hello pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="b2b99-156">Первая кнопка Hello возобновляет hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="b2b99-156">hello first button resumes hello pipeline.</span></span> <span data-ttu-id="b2b99-157">При приостановке конвейер hello цвет конвейера hello меняется.</span><span class="sxs-lookup"><span data-stu-id="b2b99-157">When your pipeline is paused, hello color of hello pipeline changes.</span></span> <span data-ttu-id="b2b99-158">Например приостановленного конвейера выглядит следующим образом в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="b2b99-158">For example, a paused pipeline looks like in hello following image:</span></span> 

![Приостановленный конвейер](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="b2b99-160">Можно выбрать несколько конвейеров два или более с помощью hello клавишу Ctrl.</span><span class="sxs-lookup"><span data-stu-id="b2b99-160">You can multi-select two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="b2b99-161">Можно использовать панель кнопок hello команда toopause или возобновления нескольких конвейеров одновременно.</span><span class="sxs-lookup"><span data-stu-id="b2b99-161">You can use hello command bar buttons toopause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="b2b99-162">Вы можете также щелкнуть правой кнопкой конвейера и выбрать параметры toosuspend, возобновлять или завершать работу конвейера.</span><span class="sxs-lookup"><span data-stu-id="b2b99-162">You can also right-click a pipeline and select options toosuspend, resume, or terminate a pipeline.</span></span> 

![Контекстное меню конвейера](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="b2b99-164">Нажмите кнопку hello **откройте конвейера** параметр toosee все hello действий в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-164">Click hello **Open pipeline** option toosee all hello activities in hello pipeline.</span></span> 

![Откройте меню конвейера](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="b2b99-166">Привет открыть конвейера, можно просмотреть все действия в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-166">In hello opened pipeline view, you see all activities in hello pipeline.</span></span> <span data-ttu-id="b2b99-167">В этом примере в конвейере существует только одно действие — действие копирования.</span><span class="sxs-lookup"><span data-stu-id="b2b99-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Открытый конвейер](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="b2b99-169">toogo резервное toohello предыдущего представления, щелкните имя фабрики данных hello в меню навигации hello верхней hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-169">toogo back toohello previous view, click hello data factory name in hello breadcrumb menu at hello top.</span></span>

<span data-ttu-id="b2b99-170">Hello конвейера при выборе выходной набор данных или при перемещении мыши над hello выходной набор данных, можно просмотреть действия Windows hello всплывающего окна для этого набора данных.</span><span class="sxs-lookup"><span data-stu-id="b2b99-170">In hello pipeline view, when you select an output dataset or when you move your mouse over hello output dataset, you see hello Activity Windows pop-up window for that dataset.</span></span>

![Всплывающее окно "Activity Windows" (Окна действий)](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="b2b99-172">Сведения об активности окна toosee можно щелкнуть для него hello **свойства** окно hello правой панели.</span><span class="sxs-lookup"><span data-stu-id="b2b99-172">You can click an activity window toosee details for it in hello **Properties** window in hello right pane.</span></span>

![Свойства окна действий](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="b2b99-174">В правой области hello переключение toohello **действия окно обозревателя** вкладке toosee Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="b2b99-174">In hello right pane, switch toohello **Activity Window Explorer** tab toosee more details.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="b2b99-176">Отображается также **разрешить переменные** для каждой попытки выполнения для действия в hello **попыток** раздела.</span><span class="sxs-lookup"><span data-stu-id="b2b99-176">You also see **resolved variables** for each run attempt for an activity in hello **Attempts** section.</span></span>

![Разрешенные переменные](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="b2b99-178">Переключение toohello **сценарий** вкладке toosee hello Определение сценария JSON для выбранного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-178">Switch toohello **Script** tab toosee hello JSON script definition for hello selected object.</span></span>   

![Вкладка "Скрипт"](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="b2b99-180">Окна действий можно просматривать в трех местах:</span><span class="sxs-lookup"><span data-stu-id="b2b99-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="b2b99-181">Hello окон действий во всплывающих окнах hello представление диаграммы (средняя панель).</span><span class="sxs-lookup"><span data-stu-id="b2b99-181">hello Activity Windows pop-up in hello Diagram View (middle pane).</span></span>
* <span data-ttu-id="b2b99-182">Hello окно обозревателя действие hello правой панели.</span><span class="sxs-lookup"><span data-stu-id="b2b99-182">hello Activity Window Explorer in hello right pane.</span></span>
* <span data-ttu-id="b2b99-183">Список действий Windows Hello hello нижней панели.</span><span class="sxs-lookup"><span data-stu-id="b2b99-183">hello Activity Windows list in hello bottom pane.</span></span>

<span data-ttu-id="b2b99-184">В всплывающих окон действий hello и действия окно обозревателя таблицу можно прокрутить toohello предыдущей недели и hello следующей неделе, используя hello стрелок влево и вправо.</span><span class="sxs-lookup"><span data-stu-id="b2b99-184">In hello Activity Windows pop-up and Activity Window Explorer, you can scroll toohello previous week and hello next week by using hello left and right arrows.</span></span>

![Кнопки со стрелками вправо и влево в "Activity Window Explorer" (Обозреватель окон действий)](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="b2b99-186">Внизу hello hello представление диаграммы, можно увидеть эти кнопки: увеличить масштаб, уменьшить масштаб, tooFit масштаба масштаб 100%, макет блокировки.</span><span class="sxs-lookup"><span data-stu-id="b2b99-186">At hello bottom of hello Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom tooFit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="b2b99-187">Hello **макета блокировки** кнопку предотвращает случайное перемещение таблиц и конвейеров в hello представление диаграммы.</span><span class="sxs-lookup"><span data-stu-id="b2b99-187">hello **Lock layout** button prevents you from accidentally moving tables and pipelines in hello Diagram View.</span></span> <span data-ttu-id="b2b99-188">Она включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b2b99-188">It's on by default.</span></span> <span data-ttu-id="b2b99-189">Можно отключить его и перемещать сущностей в схеме hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-189">You can turn it off and move entities around in hello diagram.</span></span> <span data-ttu-id="b2b99-190">При выключении этого параметра можно использовать hello последней кнопки tooautomatically позиции таблиц и конвейеров.</span><span class="sxs-lookup"><span data-stu-id="b2b99-190">When you turn it off, you can use hello last button tooautomatically position tables and pipelines.</span></span> <span data-ttu-id="b2b99-191">Также можно увеличить или уменьшить с помощью hello колесика мыши.</span><span class="sxs-lookup"><span data-stu-id="b2b99-191">You can also zoom in or out by using hello mouse wheel.</span></span>

![Команды изменения масштаба в представлении схемы](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="b2b99-193">Список "Activity Windows" (Окна действий)</span><span class="sxs-lookup"><span data-stu-id="b2b99-193">Activity Windows list</span></span>
<span data-ttu-id="b2b99-194">Список действий Windows Hello hello нижней части средней панели hello отображает все действия для hello набора данных, выбранного в hello обозреватель ресурсов или hello представление диаграммы.</span><span class="sxs-lookup"><span data-stu-id="b2b99-194">hello Activity Windows list at hello bottom of hello middle pane displays all activity windows for hello dataset that you selected in hello Resource Explorer or hello Diagram View.</span></span> <span data-ttu-id="b2b99-195">По умолчанию список hello — по убыванию, это означает, что вы видите окно последние действия hello вверху hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-195">By default, hello list is in descending order, which means that you see hello latest activity window at hello top.</span></span>

![Список "Activity Windows" (Окна действий)](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="b2b99-197">Этот список не обновляет автоматически, поэтому ее обновление используйте кнопку обновления hello на панели инструментов toomanually hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-197">This list doesn't refresh automatically, so use hello refresh button on hello toolbar toomanually refresh it.</span></span>  

<span data-ttu-id="b2b99-198">Действие windows может быть одним из следующих статусов hello:</span><span class="sxs-lookup"><span data-stu-id="b2b99-198">Activity windows can be in one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="b2b99-199">Состояние</span><span class="sxs-lookup"><span data-stu-id="b2b99-199">Status</span></span></th><th align="left"><span data-ttu-id="b2b99-200">Подсостояние</span><span class="sxs-lookup"><span data-stu-id="b2b99-200">Substatus</span></span></th><th align="left"><span data-ttu-id="b2b99-201">Описание</span><span class="sxs-lookup"><span data-stu-id="b2b99-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="b2b99-202">Waiting</span><span class="sxs-lookup"><span data-stu-id="b2b99-202">Waiting</span></span></td><td><span data-ttu-id="b2b99-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="b2b99-203">ScheduleTime</span></span></td><td><span data-ttu-id="b2b99-204">время Hello не входят в toorun окно действие hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-204">hello time hasn't come for hello activity window toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2b99-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="b2b99-205">DatasetDependencies</span></span></td><td><span data-ttu-id="b2b99-206">Hello восходящие зависимости не готовы.</span><span class="sxs-lookup"><span data-stu-id="b2b99-206">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2b99-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="b2b99-207">ComputeResources</span></span></td><td><span data-ttu-id="b2b99-208">Hello вычислительные ресурсы недоступны.</span><span class="sxs-lookup"><span data-stu-id="b2b99-208">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2b99-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="b2b99-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="b2b99-210">Все экземпляры действий hello заняты обработкой других окон действий.</span><span class="sxs-lookup"><span data-stu-id="b2b99-210">All hello activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2b99-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="b2b99-211">ActivityResume</span></span></td><td><span data-ttu-id="b2b99-212">Действие Hello приостановлено и не может работать windows действие hello, пока будет возобновлено.</span><span class="sxs-lookup"><span data-stu-id="b2b99-212">hello activity is paused and can't run hello activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2b99-213">Retry</span><span class="sxs-lookup"><span data-stu-id="b2b99-213">Retry</span></span></td><td><span data-ttu-id="b2b99-214">Повторная попытка выполнения операции Hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-214">hello activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2b99-215">Проверка</span><span class="sxs-lookup"><span data-stu-id="b2b99-215">Validation</span></span></td><td><span data-ttu-id="b2b99-216">Проверка еще не начата.</span><span class="sxs-lookup"><span data-stu-id="b2b99-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2b99-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="b2b99-217">ValidationRetry</span></span></td><td><span data-ttu-id="b2b99-218">Проверка выполняется повторная toobe ожидания.</span><span class="sxs-lookup"><span data-stu-id="b2b99-218">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="b2b99-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="b2b99-219">InProgress</span></span></td><td><span data-ttu-id="b2b99-220">Validating</span><span class="sxs-lookup"><span data-stu-id="b2b99-220">Validating</span></span></td><td><span data-ttu-id="b2b99-221">Проверка выполняется.</span><span class="sxs-lookup"><span data-stu-id="b2b99-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="b2b99-222">окно действия Hello обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="b2b99-222">hello activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="b2b99-223">Сбой</span><span class="sxs-lookup"><span data-stu-id="b2b99-223">Failed</span></span></td><td><span data-ttu-id="b2b99-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="b2b99-224">TimedOut</span></span></td><td><span data-ttu-id="b2b99-225">Выполнение действия Hello продолжалась дольше, чем допустимых с действия "hello".</span><span class="sxs-lookup"><span data-stu-id="b2b99-225">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2b99-226">Canceled</span><span class="sxs-lookup"><span data-stu-id="b2b99-226">Canceled</span></span></td><td><span data-ttu-id="b2b99-227">окно Hello действия была отменена пользователем.</span><span class="sxs-lookup"><span data-stu-id="b2b99-227">hello activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2b99-228">Проверка</span><span class="sxs-lookup"><span data-stu-id="b2b99-228">Validation</span></span></td><td><span data-ttu-id="b2b99-229">Сбой проверки.</span><span class="sxs-lookup"><span data-stu-id="b2b99-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="b2b99-230">окно действия Hello сбой toobe или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="b2b99-230">hello activity window failed toobe generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="b2b99-231">Ready</span><span class="sxs-lookup"><span data-stu-id="b2b99-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="b2b99-232">окно действия Hello готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="b2b99-232">hello activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2b99-233">Skipped</span><span class="sxs-lookup"><span data-stu-id="b2b99-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="b2b99-234">окно Hello действия не было обработано.</span><span class="sxs-lookup"><span data-stu-id="b2b99-234">hello activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b2b99-235">None</span><span class="sxs-lookup"><span data-stu-id="b2b99-235">None</span></span></td><td>-</td><td><span data-ttu-id="b2b99-236">В окне активности используется tooexist в другом состоянии, но был сброшен.</span><span class="sxs-lookup"><span data-stu-id="b2b99-236">An activity window used tooexist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="b2b99-237">Появляется при нажатии кнопки окна действия в списке hello, сведения о ней в hello **действия Проводник** или hello **свойства** окна на правом hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-237">When you click an activity window in hello list, you see details about it in hello **Activity Windows Explorer** or hello **Properties** window on hello right.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="b2b99-239">Обновление окон действий</span><span class="sxs-lookup"><span data-stu-id="b2b99-239">Refresh activity windows</span></span>
<span data-ttu-id="b2b99-240">Подробности Hello не обновляются автоматически, поэтому следует использовать hello обновления (hello второй) кнопки на панели списка toomanually обновления hello действия windows hello команд.</span><span class="sxs-lookup"><span data-stu-id="b2b99-240">hello details aren't automatically refreshed, so use hello refresh button (hello second button) on hello command bar toomanually refresh hello activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="b2b99-241">Окно "Свойства"</span><span class="sxs-lookup"><span data-stu-id="b2b99-241">Properties window</span></span>
<span data-ttu-id="b2b99-242">окно "Свойства" Hello находится в области справа hello приложение hello наблюдения и управления.</span><span class="sxs-lookup"><span data-stu-id="b2b99-242">hello Properties window is in hello right-most pane of hello Monitoring and Management app.</span></span>

![Окно "Свойства"](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="b2b99-244">Показать свойства для hello элемента, выбранного в hello обозреватель ресурсов (дерево), представление схемы или списка действий Windows.</span><span class="sxs-lookup"><span data-stu-id="b2b99-244">It displays properties for hello item that you selected in hello Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="b2b99-245">Activity Window Explorer</span><span class="sxs-lookup"><span data-stu-id="b2b99-245">Activity Window Explorer</span></span>
<span data-ttu-id="b2b99-246">Hello **действия окно обозревателя** окно находится в области справа hello приложение hello наблюдения и управления.</span><span class="sxs-lookup"><span data-stu-id="b2b99-246">hello **Activity Window Explorer** window is in hello right-most pane of hello Monitoring and Management app.</span></span> <span data-ttu-id="b2b99-247">Он отображает сведения о окно hello действия, выбранного в всплывающее окно действия Windows hello или список действий Windows hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-247">It displays details about hello activity window that you selected in hello Activity Windows pop-up window or hello Activity Windows list.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="b2b99-249">Окно tooanother действия можно перейти, щелкнув его в представлении календаря hello вверху hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-249">You can switch tooanother activity window by clicking it in hello calendar view at hello top.</span></span> <span data-ttu-id="b2b99-250">Можно также используйте кнопки со стрелками влево, Стрелка/вправо hello в windows действие hello top toosee из hello предыдущей недели или hello следующей неделе.</span><span class="sxs-lookup"><span data-stu-id="b2b99-250">You can also use hello left arrow/right arrow buttons at hello top toosee activity windows from hello previous week or hello next week.</span></span>

<span data-ttu-id="b2b99-251">Можно использовать кнопки панели инструментов hello в окно приветствия нижней панели toorerun hello действия или обновить информацию о hello hello панели.</span><span class="sxs-lookup"><span data-stu-id="b2b99-251">You can use hello toolbar buttons in hello bottom pane toorerun hello activity window or refresh hello details in hello pane.</span></span>

### <a name="script"></a><span data-ttu-id="b2b99-252">Скрипт</span><span class="sxs-lookup"><span data-stu-id="b2b99-252">Script</span></span>
<span data-ttu-id="b2b99-253">Можно использовать hello **сценарий** hello tooview вкладка Определение JSON hello выбранных сущностей фабрики данных (связанной службы, набор данных или конвейера).</span><span class="sxs-lookup"><span data-stu-id="b2b99-253">You can use hello **Script** tab tooview hello JSON definition of hello selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Вкладка "Скрипт"](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="b2b99-255">Использование системных представлений</span><span class="sxs-lookup"><span data-stu-id="b2b99-255">Use system views</span></span>
<span data-ttu-id="b2b99-256">Hello управление и мониторинг приложений включает в себя готовые системные представления (**последние действия windows**, **сбой действия windows**, **выполняющееся действие windows**), Разрешить windows tooview последних/сбой или выполняющееся действие для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="b2b99-256">hello Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you tooview recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="b2b99-257">Переключение toohello **представления мониторинга** вкладке слева hello, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="b2b99-257">Switch toohello **Monitoring Views** tab on hello left by clicking it.</span></span>

![Вкладка "Представления мониторинга"](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="b2b99-259">В настоящее время поддерживаются три системных представления.</span><span class="sxs-lookup"><span data-stu-id="b2b99-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="b2b99-260">Выберите параметр toosee Недавние действия windows, сбой операции windows или windows выполняющееся действие в список действий Windows hello (внизу hello hello средней панели).</span><span class="sxs-lookup"><span data-stu-id="b2b99-260">Select an option toosee recent activity windows, failed activity windows, or in-progress activity windows in hello Activity Windows list (at hello bottom of hello middle pane).</span></span>

<span data-ttu-id="b2b99-261">При выборе hello **последние действия windows** параметр, вы видите все недавние действия windows в порядке убывания hello **время последней попытки**.</span><span class="sxs-lookup"><span data-stu-id="b2b99-261">When you select hello **Recent activity windows** option, you see all recent activity windows in descending order of hello **last attempt time**.</span></span>

<span data-ttu-id="b2b99-262">Можно использовать hello **сбой действия windows** просмотра windows toosee не удалось выполнить действие в списке hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-262">You can use hello **Failed activity windows** view toosee all failed activity windows in hello list.</span></span> <span data-ttu-id="b2b99-263">Выберите окно отмененное действие в hello список toosee подробные сведения о нем в hello **свойства** окна или hello **действия окно обозревателя**.</span><span class="sxs-lookup"><span data-stu-id="b2b99-263">Select a failed activity window in hello list toosee details about it in hello **Properties** window or hello **Activity Window Explorer**.</span></span> <span data-ttu-id="b2b99-264">Можно также загрузить журналы для завершившегося ошибкой окна действия.</span><span class="sxs-lookup"><span data-stu-id="b2b99-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="b2b99-265">Сортировка и фильтрация окон действий</span><span class="sxs-lookup"><span data-stu-id="b2b99-265">Sort and filter activity windows</span></span>
<span data-ttu-id="b2b99-266">Изменение hello **время начала** и **время окончания** параметры в панели toofilter действия windows hello команд.</span><span class="sxs-lookup"><span data-stu-id="b2b99-266">Change hello **start time** and **end time** settings in hello command bar toofilter activity windows.</span></span> <span data-ttu-id="b2b99-267">После изменения hello время начала и время окончания выберите hello кнопку Далее toohello окончания времени toorefresh hello окон действий списка.</span><span class="sxs-lookup"><span data-stu-id="b2b99-267">After you change hello start time and end time, click hello button next toohello end time toorefresh hello Activity Windows list.</span></span>

![Время начала и окончания](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="b2b99-269">В настоящее время все значения времени приведены в формате UTC в приложение hello наблюдения и управления.</span><span class="sxs-lookup"><span data-stu-id="b2b99-269">Currently, all times are in UTC format in hello Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="b2b99-270">В hello **список действий Windows**, щелкните имя столбца hello (например: состояние).</span><span class="sxs-lookup"><span data-stu-id="b2b99-270">In hello **Activity Windows list**, click hello name of a column (for example: Status).</span></span>

![Меню столбца списка "Activity Windows" (Окна действий)](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="b2b99-272">Можно сделать hello следующее:</span><span class="sxs-lookup"><span data-stu-id="b2b99-272">You can do hello following:</span></span>

* <span data-ttu-id="b2b99-273">отсортировать по возрастанию;</span><span class="sxs-lookup"><span data-stu-id="b2b99-273">Sort in ascending order.</span></span>
* <span data-ttu-id="b2b99-274">отсортировать по убыванию;</span><span class="sxs-lookup"><span data-stu-id="b2b99-274">Sort in descending order.</span></span>
* <span data-ttu-id="b2b99-275">отфильтровать по одному или нескольким значениям ("Готово", "Ожидание" и т. д.).</span><span class="sxs-lookup"><span data-stu-id="b2b99-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="b2b99-276">При указании фильтр на столбце отображается кнопка фильтра hello включен для этого столбца, который указывает, что hello значения в столбце hello отфильтрованные значения.</span><span class="sxs-lookup"><span data-stu-id="b2b99-276">When you specify a filter on a column, you see hello filter button enabled for that column, which indicates that hello values in hello column are filtered values.</span></span>

![Применить фильтр к столбцу списка действий Windows hello](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="b2b99-278">Можно использовать hello и те же фильтры tooclear во всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="b2b99-278">You can use hello same pop-up window tooclear filters.</span></span> <span data-ttu-id="b2b99-279">tooclear все фильтры для списка действий Windows hello, нажмите кнопку Очистить фильтр hello hello панели команд.</span><span class="sxs-lookup"><span data-stu-id="b2b99-279">tooclear all filters for hello Activity Windows list, click hello clear filter button on hello command bar.</span></span>

![Очистить все фильтры для списка действий Windows hello](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="b2b99-281">Выполнение пакетных действий</span><span class="sxs-lookup"><span data-stu-id="b2b99-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="b2b99-282">Повторное выполнение выбранных окон действий</span><span class="sxs-lookup"><span data-stu-id="b2b99-282">Rerun selected activity windows</span></span>
<span data-ttu-id="b2b99-283">Выберите окно действия hello вниз для hello первой кнопке панели команд и выберите **повторить** / **повторно с проверенными в конвейере**.</span><span class="sxs-lookup"><span data-stu-id="b2b99-283">Select an activity window, click hello down arrow for hello first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="b2b99-284">При выборе hello **повторно с проверенными в конвейере** параметр, он перезапустит также все окна восходящего действия.</span><span class="sxs-lookup"><span data-stu-id="b2b99-284">When you select hello **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="b2b99-285">![Повторное выполнение окна действия](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="b2b99-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="b2b99-286">Также можно выбрать несколько окон действий в списке hello и снова запустите их на hello то же время.</span><span class="sxs-lookup"><span data-stu-id="b2b99-286">You can also select multiple activity windows in hello list and rerun them at hello same time.</span></span> <span data-ttu-id="b2b99-287">Может потребоваться toofilter действия windows на основе состояния hello (например: **сбой**)--и повторно запустите программу windows hello не удалось выполнить действия после исправления hello проблему, которая вызывает toofail windows hello действия.</span><span class="sxs-lookup"><span data-stu-id="b2b99-287">You might want toofilter activity windows based on hello status (for example: **Failed**)--and then rerun hello failed activity windows after correcting hello issue that causes hello activity windows toofail.</span></span> <span data-ttu-id="b2b99-288">См. в следующем разделе Дополнительные сведения о фильтрации windows действия в списке hello hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-288">See hello following section for details about filtering activity windows in hello list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="b2b99-289">Приостановка и возобновление нескольких конвейеров</span><span class="sxs-lookup"><span data-stu-id="b2b99-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="b2b99-290">Multiselect конвейеры два или более можно с помощью клавиши Ctrl hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-290">You can multiselect two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="b2b99-291">Можно использовать кнопки панели команд hello (который выделены hello красный прямоугольник в hello после изображения) toopause или возобновления их.</span><span class="sxs-lookup"><span data-stu-id="b2b99-291">You can use hello command bar buttons (which are highlighted in hello red rectangle in hello following image) toopause/resume them.</span></span>

![Приостановить или возобновить на панели команд, hello](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="b2b99-293">Создание оповещений</span><span class="sxs-lookup"><span data-stu-id="b2b99-293">Create alerts</span></span>
<span data-ttu-id="b2b99-294">Hello **оповещения** страница позволяет создать оповещение и Просмотр/изменение/Удаление оповещения.</span><span class="sxs-lookup"><span data-stu-id="b2b99-294">hello **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="b2b99-295">Можно также включить или отключить оповещение.</span><span class="sxs-lookup"><span data-stu-id="b2b99-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="b2b99-296">toosee Здравствуйте страницы оповещения, щелкните hello **оповещения** вкладки.</span><span class="sxs-lookup"><span data-stu-id="b2b99-296">toosee hello Alerts page, click hello **Alerts** tab.</span></span>

![Вкладка "Оповещения"](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a><span data-ttu-id="b2b99-298">toocreate оповещение</span><span class="sxs-lookup"><span data-stu-id="b2b99-298">toocreate an alert</span></span>
1. <span data-ttu-id="b2b99-299">Нажмите кнопку **добавить оповещение** tooadd оповещение.</span><span class="sxs-lookup"><span data-stu-id="b2b99-299">Click **Add Alert** tooadd an alert.</span></span> <span data-ttu-id="b2b99-300">Вы видите hello **сведения** страницы.</span><span class="sxs-lookup"><span data-stu-id="b2b99-300">You see hello **Details** page.</span></span>

    ![Создание оповещений — страница "Сведения"](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="b2b99-302">Укажите hello **имя** и **описание** hello предупреждение, а затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b2b99-302">Specify hello **Name** and **Description** for hello alert, and click **Next**.</span></span> <span data-ttu-id="b2b99-303">Вы увидите hello **фильтры** страницы.</span><span class="sxs-lookup"><span data-stu-id="b2b99-303">You should see hello **Filters** page.</span></span>

    ![Создание оповещений — страница "Фильтры"](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="b2b99-305">Выберите hello **событий**, **состояние**, и **подсостояния** (необязательно), которые должны toocreate служба фабрики данных для предупреждения и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b2b99-305">Select hello **event**, **status**, and **substatus** (optional) that you want toocreate a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="b2b99-306">Вы увидите hello **получателей** страницы.</span><span class="sxs-lookup"><span data-stu-id="b2b99-306">You should see hello **Recipients** page.</span></span>

    ![Создание оповещений — страница "Получатели"](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="b2b99-308">Выберите hello **по электронной почте администраторам подписки** параметра или ввести **дополнительная электронная почта администратора**и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="b2b99-308">Select hello **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="b2b99-309">Вы увидите предупреждение hello в списке hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-309">You should see hello alert in hello list.</span></span>

    ![Список "Оповещения"](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="b2b99-311">В списке оповещений hello кнопки hello, которые связаны с hello предупреждения tooedit/delete/включить или отключить предупреждение.</span><span class="sxs-lookup"><span data-stu-id="b2b99-311">In hello Alerts list, use hello buttons that are associated with hello alert tooedit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="b2b99-312">Событие, состояние и подсостояние</span><span class="sxs-lookup"><span data-stu-id="b2b99-312">Event/status/substatus</span></span>
<span data-ttu-id="b2b99-313">Hello следующей таблице приведен список hello доступные события и состояния (и Дополнительные сведения).</span><span class="sxs-lookup"><span data-stu-id="b2b99-313">hello following table provides hello list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="b2b99-314">Имя события</span><span class="sxs-lookup"><span data-stu-id="b2b99-314">Event name</span></span> | <span data-ttu-id="b2b99-315">Состояние</span><span class="sxs-lookup"><span data-stu-id="b2b99-315">Status</span></span> | <span data-ttu-id="b2b99-316">Подсостояние</span><span class="sxs-lookup"><span data-stu-id="b2b99-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2b99-317">Выполнение действия начато</span><span class="sxs-lookup"><span data-stu-id="b2b99-317">Activity Run Started</span></span> |<span data-ttu-id="b2b99-318">Started</span><span class="sxs-lookup"><span data-stu-id="b2b99-318">Started</span></span> |<span data-ttu-id="b2b99-319">Запуск</span><span class="sxs-lookup"><span data-stu-id="b2b99-319">Starting</span></span> |
| <span data-ttu-id="b2b99-320">Выполнение действия завершено</span><span class="sxs-lookup"><span data-stu-id="b2b99-320">Activity Run Finished</span></span> |<span data-ttu-id="b2b99-321">Успешно</span><span class="sxs-lookup"><span data-stu-id="b2b99-321">Succeeded</span></span> |<span data-ttu-id="b2b99-322">Успешно</span><span class="sxs-lookup"><span data-stu-id="b2b99-322">Succeeded</span></span> |
| <span data-ttu-id="b2b99-323">Выполнение действия завершено</span><span class="sxs-lookup"><span data-stu-id="b2b99-323">Activity Run Finished</span></span> |<span data-ttu-id="b2b99-324">Сбой</span><span class="sxs-lookup"><span data-stu-id="b2b99-324">Failed</span></span> |<span data-ttu-id="b2b99-325">Неудачное выделение ресурсов</span><span class="sxs-lookup"><span data-stu-id="b2b99-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="b2b99-326">Сбой при выполнении</span><span class="sxs-lookup"><span data-stu-id="b2b99-326">Failed Execution</span></span><br/><br/><span data-ttu-id="b2b99-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="b2b99-327">Timed Out</span></span><br/><br/><span data-ttu-id="b2b99-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="b2b99-328">Failed Validation</span></span><br/><br/><span data-ttu-id="b2b99-329">Abandoned</span><span class="sxs-lookup"><span data-stu-id="b2b99-329">Abandoned</span></span> |
| <span data-ttu-id="b2b99-330">Создание кластера HDI по запросу начато</span><span class="sxs-lookup"><span data-stu-id="b2b99-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="b2b99-331">Started</span><span class="sxs-lookup"><span data-stu-id="b2b99-331">Started</span></span> |-|
| <span data-ttu-id="b2b99-332">Кластер HDI по запросу успешно создан</span><span class="sxs-lookup"><span data-stu-id="b2b99-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="b2b99-333">Успешно</span><span class="sxs-lookup"><span data-stu-id="b2b99-333">Succeeded</span></span> |-|
| <span data-ttu-id="b2b99-334">Кластер HDI по запросу удален</span><span class="sxs-lookup"><span data-stu-id="b2b99-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="b2b99-335">Успешно</span><span class="sxs-lookup"><span data-stu-id="b2b99-335">Succeeded</span></span> |-|

### <a name="tooedit-delete-or-disable-an-alert"></a><span data-ttu-id="b2b99-336">tooedit, удалить или отключить оповещения</span><span class="sxs-lookup"><span data-stu-id="b2b99-336">tooedit, delete, or disable an alert</span></span>

<span data-ttu-id="b2b99-337">Используйте следующие tooedit кнопок (выделено красным цветом), delete или отключить оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="b2b99-337">Use hello following buttons (highlighted in red) tooedit, delete, or disable an alert.</span></span>

![Кнопки оповещений](./media/data-factory-monitor-manage-app/AlertButtons.png)
