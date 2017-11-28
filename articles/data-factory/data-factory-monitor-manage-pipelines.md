---
title: "Мониторинг конвейеров и управление ими с помощью портала Azure и PowerShell | Документация Майкрософт"
description: "Сведения о том, как с помощью портала Azure и Azure PowerShell отслеживать состояние созданных конвейеров и фабрик данных Azure и управлять ими."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 61bb5379cd94dd00814e14420947e7783999ff0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-azure-portal-and-powershell"></a><span data-ttu-id="de636-103">Мониторинг конвейеров фабрики данных Azure и управление ими с помощью портала Azure и PowerShell</span><span class="sxs-lookup"><span data-stu-id="de636-103">Monitor and manage Azure Data Factory pipelines by using the Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="de636-104">Использование портала Azure или Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="de636-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="de636-105">Использование приложения для мониторинга и управления</span><span class="sxs-lookup"><span data-stu-id="de636-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="de636-106">Приложение для мониторинга и управления предоставляет улучшенную поддержку мониторинга и управления конвейерами данных и усовершенствованное устранение проблем.</span><span class="sxs-lookup"><span data-stu-id="de636-106">The monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="de636-107">Чтобы узнать больше об этом приложении, ознакомьтесь со статьей [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения для мониторинга и управления](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="de636-107">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="de636-108">В этой статье описываются мониторинг и отладка конвейеров, а также управление ими с помощью портала Azure и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de636-108">This article describes how to monitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="de636-109">В ней также приводятся инструкции по настройке оповещений в случае сбоев.</span><span class="sxs-lookup"><span data-stu-id="de636-109">The article also provides information on how to create alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="de636-110">Состояния конвейеров и действий</span><span class="sxs-lookup"><span data-stu-id="de636-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="de636-111">Используя портал Azure, можно делать следующее:</span><span class="sxs-lookup"><span data-stu-id="de636-111">By using the Azure portal, you can:</span></span>

* <span data-ttu-id="de636-112">представлять фабрику данных в виде схемы;</span><span class="sxs-lookup"><span data-stu-id="de636-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="de636-113">просматривать действия в конвейере;</span><span class="sxs-lookup"><span data-stu-id="de636-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="de636-114">просматривать входные и выходные наборы данных.</span><span class="sxs-lookup"><span data-stu-id="de636-114">View input and output datasets.</span></span>

<span data-ttu-id="de636-115">В этом разделе также содержатся сведения о переходе среза набора данных из одного состояния в другое.</span><span class="sxs-lookup"><span data-stu-id="de636-115">This section also describes how a dataset slice transitions from one state to another state.</span></span>   

### <a name="navigate-to-your-data-factory"></a><span data-ttu-id="de636-116">Переход к фабрике данных</span><span class="sxs-lookup"><span data-stu-id="de636-116">Navigate to your data factory</span></span>
1. <span data-ttu-id="de636-117">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de636-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="de636-118">Щелкните колонку **Фабрики данных** в меню слева.</span><span class="sxs-lookup"><span data-stu-id="de636-118">Click **Data factories** on the menu on the left.</span></span> <span data-ttu-id="de636-119">Если вы ее не видите, выберите **Больше служб** и щелкните **Фабрики данных** в категории **Аналитика**.</span><span class="sxs-lookup"><span data-stu-id="de636-119">If you don't see it, click **More services >**, and then click **Data factories** under the **INTELLIGENCE + ANALYTICS** category.</span></span>

   !["Просмотреть все" -> "Фабрики данных"](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="de636-121">В колонке **Фабрики данных** выберите фабрику данных, которая вас интересует.</span><span class="sxs-lookup"><span data-stu-id="de636-121">On the **Data factories** blade, select the data factory that you're interested in.</span></span>

    ![Выбор фабрики данных](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="de636-123">После этого откроется домашняя страница фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="de636-123">You should see the home page for the data factory.</span></span>

   ![Колонка "Фабрика данных"](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="de636-125">Представление фабрики данных в виде схемы</span><span class="sxs-lookup"><span data-stu-id="de636-125">Diagram view of your data factory</span></span>
<span data-ttu-id="de636-126">Представление **схемы** позволяет отслеживать состояние фабрики данных и всех ее ресурсов, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="de636-126">The **Diagram** view of a data factory provides a single pane of glass to monitor and manage the data factory and its assets.</span></span> <span data-ttu-id="de636-127">Щелкните **Схема** на домашней странице фабрики данных, чтобы представить ее в виде **схемы**.</span><span class="sxs-lookup"><span data-stu-id="de636-127">To see the **Diagram** view of your data factory, click **Diagram** on the home page for the data factory.</span></span>

![Представление схемы](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="de636-129">Вы можете увеличивать и уменьшать масштаб, выбирать 100%-ный масштаб или масштаб по размеру, блокировать структуру схемы и автоматически размещать конвейеры и наборы данных.</span><span class="sxs-lookup"><span data-stu-id="de636-129">You can zoom in, zoom out, zoom to fit, zoom to 100%, lock the layout of the diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="de636-130">Кроме того, можно отображать сведения из журнала преобразований данных (выделение восходящих и нисходящих элементов).</span><span class="sxs-lookup"><span data-stu-id="de636-130">You can also see the data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="de636-131">Действия в конвейере</span><span class="sxs-lookup"><span data-stu-id="de636-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="de636-132">Щелкните конвейер правой кнопкой мыши и выберите **Открыть конвейер**. Отобразятся все действия, а также входные и выходные наборы данных.</span><span class="sxs-lookup"><span data-stu-id="de636-132">Right-click the pipeline, and then click **Open pipeline** to see all activities in the pipeline, along with input and output datasets for the activities.</span></span> <span data-ttu-id="de636-133">Эта функция удобна, когда конвейер состоит из нескольких действий, а вы хотите понять структуру взаимосвязей во всем конвейере.</span><span class="sxs-lookup"><span data-stu-id="de636-133">This feature is useful when your pipeline includes more than one activity and you want to understand the operational lineage of a single pipeline.</span></span>

    ![Откройте меню конвейера](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="de636-135">В приведенном ниже примере используется действие копирования в конвейере с входными и выходными данными.</span><span class="sxs-lookup"><span data-stu-id="de636-135">In the following example, you see a copy activity in the pipeline with an input and an output.</span></span> 

    ![Действия в конвейере](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="de636-137">Чтобы вернуться на домашнюю страницу фабрики данных, щелкните ссылку **Фабрика данных** в строке навигации в левом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="de636-137">You can navigate back to the home page of the data factory by clicking the **Data factory** link in the breadcrumb at the top-left corner.</span></span>

    ![Возврат к фабрике данных](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-the-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="de636-139">Просмотр состояния действий в конвейере</span><span class="sxs-lookup"><span data-stu-id="de636-139">View the state of each activity inside a pipeline</span></span>
<span data-ttu-id="de636-140">Вы можете просмотреть текущее состояние отдельного действия, отобразив состояние любого созданного им набора данных.</span><span class="sxs-lookup"><span data-stu-id="de636-140">You can view the current state of an activity by viewing the status of any of the datasets that are produced by the activity.</span></span>

<span data-ttu-id="de636-141">Чтобы отобразить все срезы, созданные в рамках отдельных циклов выполнения действия в конвейере, дважды щелкните **OutputBlobTable** в представлении **Схема**.</span><span class="sxs-lookup"><span data-stu-id="de636-141">By double-clicking the **OutputBlobTable** in the **Diagram**, you can see all the slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="de636-142">Как видите, действие копирования успешно выполнялось последние восемь часов и создало срезы в состоянии **Готово**.</span><span class="sxs-lookup"><span data-stu-id="de636-142">You can see that the copy activity ran successfully for the last eight hours and produced the slices in the **Ready** state.</span></span>  

![Состояние конвейера](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="de636-144">Срезы наборов данных в фабрике данных могут находиться в одном из следующих состояний:</span><span class="sxs-lookup"><span data-stu-id="de636-144">The dataset slices in the data factory can have one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="de636-145">Состояние</span><span class="sxs-lookup"><span data-stu-id="de636-145">State</span></span></th><th align="left"><span data-ttu-id="de636-146">Подсостояние</span><span class="sxs-lookup"><span data-stu-id="de636-146">Substate</span></span></th><th align="left"><span data-ttu-id="de636-147">Описание</span><span class="sxs-lookup"><span data-stu-id="de636-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="de636-148">Waiting</span><span class="sxs-lookup"><span data-stu-id="de636-148">Waiting</span></span></td><td><span data-ttu-id="de636-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="de636-149">ScheduleTime</span></span></td><td><span data-ttu-id="de636-150">Время для выполнения среза еще не пришло.</span><span class="sxs-lookup"><span data-stu-id="de636-150">The time hasn't come for the slice to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de636-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="de636-151">DatasetDependencies</span></span></td><td><span data-ttu-id="de636-152">Восходящие зависимости не готовы.</span><span class="sxs-lookup"><span data-stu-id="de636-152">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de636-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="de636-153">ComputeResources</span></span></td><td><span data-ttu-id="de636-154">Вычислительные ресурсы недоступны.</span><span class="sxs-lookup"><span data-stu-id="de636-154">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de636-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="de636-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="de636-156">Все экземпляры действия заняты выполнением других срезов.</span><span class="sxs-lookup"><span data-stu-id="de636-156">All the activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de636-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="de636-157">ActivityResume</span></span></td><td><span data-ttu-id="de636-158">Действие приостановлено, и до его возобновления выполнять срезы нельзя.</span><span class="sxs-lookup"><span data-stu-id="de636-158">The activity is paused and can't run the slices until the activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de636-159">Retry</span><span class="sxs-lookup"><span data-stu-id="de636-159">Retry</span></span></td><td><span data-ttu-id="de636-160">Действие выполняется повторно.</span><span class="sxs-lookup"><span data-stu-id="de636-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de636-161">Проверка</span><span class="sxs-lookup"><span data-stu-id="de636-161">Validation</span></span></td><td><span data-ttu-id="de636-162">Проверка еще не начата.</span><span class="sxs-lookup"><span data-stu-id="de636-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de636-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="de636-163">ValidationRetry</span></span></td><td><span data-ttu-id="de636-164">Ожидание повторения проверки.</span><span class="sxs-lookup"><span data-stu-id="de636-164">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="de636-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="de636-165">InProgress</span></span></td><td><span data-ttu-id="de636-166">Validating</span><span class="sxs-lookup"><span data-stu-id="de636-166">Validating</span></span></td><td><span data-ttu-id="de636-167">Проверка выполняется.</span><span class="sxs-lookup"><span data-stu-id="de636-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="de636-168">Срез обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="de636-168">The slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="de636-169">Сбой</span><span class="sxs-lookup"><span data-stu-id="de636-169">Failed</span></span></td><td><span data-ttu-id="de636-170">TimedOut</span><span class="sxs-lookup"><span data-stu-id="de636-170">TimedOut</span></span></td><td><span data-ttu-id="de636-171">Выполнение действия заняло больше времени, чем разрешено для данного действия.</span><span class="sxs-lookup"><span data-stu-id="de636-171">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de636-172">Canceled</span><span class="sxs-lookup"><span data-stu-id="de636-172">Canceled</span></span></td><td><span data-ttu-id="de636-173">Срез был отменен пользователем.</span><span class="sxs-lookup"><span data-stu-id="de636-173">The slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de636-174">Проверка</span><span class="sxs-lookup"><span data-stu-id="de636-174">Validation</span></span></td><td><span data-ttu-id="de636-175">Сбой проверки.</span><span class="sxs-lookup"><span data-stu-id="de636-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="de636-176">Не удалось создать и/или проверить срез.</span><span class="sxs-lookup"><span data-stu-id="de636-176">The slice failed to be generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="de636-177">Ready</span><span class="sxs-lookup"><span data-stu-id="de636-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="de636-178">Срез готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="de636-178">The slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de636-179">Skipped</span><span class="sxs-lookup"><span data-stu-id="de636-179">Skipped</span></span></td><td><span data-ttu-id="de636-180">None</span><span class="sxs-lookup"><span data-stu-id="de636-180">None</span></span></td><td><span data-ttu-id="de636-181">Срез не обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="de636-181">The slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="de636-182">None</span><span class="sxs-lookup"><span data-stu-id="de636-182">None</span></span></td><td>-</td><td><span data-ttu-id="de636-183">Срез, который ранее существовал с другим состоянием, но был сброшен.</span><span class="sxs-lookup"><span data-stu-id="de636-183">A slice used to exist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="de636-184">Чтобы просмотреть сведения о срезе, щелкните запись среза в колонке **Последние обновленные срезы**.</span><span class="sxs-lookup"><span data-stu-id="de636-184">You can view the details about a slice by clicking a slice entry on the **Recently Updated Slices** blade.</span></span>

![Сведения о срезе](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="de636-186">Если срез выполнялся несколько раз, вы увидите несколько строк в списке **Выполнения действий** .</span><span class="sxs-lookup"><span data-stu-id="de636-186">If the slice has been executed multiple times, you see multiple rows in the **Activity runs** list.</span></span> <span data-ttu-id="de636-187">Чтобы просмотреть сведения о выполнении действия, щелкните запись цикла в списке **Циклы выполнения действия** .</span><span class="sxs-lookup"><span data-stu-id="de636-187">You can view details about an activity run by clicking the run entry in the **Activity runs** list.</span></span> <span data-ttu-id="de636-188">Отобразятся все файлы журналов и сообщения об ошибках, если таковые были.</span><span class="sxs-lookup"><span data-stu-id="de636-188">The list shows all the log files, along with an error message if there is one.</span></span> <span data-ttu-id="de636-189">Эта функция удобна для просмотра и обработки файлов журналов непосредственно из фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="de636-189">This feature is useful to view and debug logs without having to leave your data factory.</span></span>

![СВЕДЕНИЯ О ВЫПОЛНЕННОМ ДЕЙСТВИИ](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="de636-191">Если срез не находится в состоянии **Готово**, вы можете увидеть восходящие срезы, которые не находятся в состоянии готовности и блокируют выполнение текущего среза в списке **Неготовые восходящие срезы**.</span><span class="sxs-lookup"><span data-stu-id="de636-191">If the slice isn't in the **Ready** state, you can see the upstream slices that aren't ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="de636-192">Эта функция удобна для просмотра восходящих зависимостей, если срез находится в состоянии **Ожидание**.</span><span class="sxs-lookup"><span data-stu-id="de636-192">This feature is useful when your slice is in **Waiting** state and you want to understand the upstream dependencies that the slice is waiting on.</span></span>

![Неготовые восходящие срезы](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="de636-194">Схема состояний наборов данных</span><span class="sxs-lookup"><span data-stu-id="de636-194">Dataset state diagram</span></span>
<span data-ttu-id="de636-195">После развертывания фабрики данных и определения периода активности конвейера срезы наборов данных переходят из одного состояния в другое.</span><span class="sxs-lookup"><span data-stu-id="de636-195">After you deploy a data factory and the pipelines have a valid active period, the dataset slices transition from one state to another.</span></span> <span data-ttu-id="de636-196">В настоящее время переходы между состояниями выполняются в соответствии со следующей схемой:</span><span class="sxs-lookup"><span data-stu-id="de636-196">Currently, the slice status follows the following state diagram:</span></span>

![Схема состояний](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="de636-198">Поток переходов между состояниями выглядит так: "Ожидание" -> "Выполняется" или "Выполняется (проверка)" -> "Готово" или "Сбой".</span><span class="sxs-lookup"><span data-stu-id="de636-198">The dataset state transition flow in data factory is the following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="de636-199">Изначально срезы находятся в состоянии **Ожидание**, ожидая, что предварительные условия будут соблюдены до выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="de636-199">The slice starts in a **Waiting** state, waiting for preconditions to be met before it executes.</span></span> <span data-ttu-id="de636-200">Затем начинается выполнение действия, и срез переходит в состояние **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="de636-200">Then, the activity starts executing, and the slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="de636-201">Выполнение действия может завершиться успешно или с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="de636-201">The activity execution might succeed or fail.</span></span> <span data-ttu-id="de636-202">В зависимости от того, как завершится действие, срез перейдет в состояние **Готово** или **Сбой**.</span><span class="sxs-lookup"><span data-stu-id="de636-202">The slice is marked as **Ready** or **Failed**, based on the result of the execution.</span></span>

<span data-ttu-id="de636-203">Вы можете сбросить состояние среза **Готово** или **Сбой** обратно в состояние **Ожидание**.</span><span class="sxs-lookup"><span data-stu-id="de636-203">You can reset the slice to go back from the **Ready** or **Failed** state to the **Waiting** state.</span></span> <span data-ttu-id="de636-204">Вы также можете установить для среза флажок **Пропустить** — действие со срезом не выполняется, и срез не обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="de636-204">You can also mark the slice state to **Skip**, which prevents the activity from executing and not processing the slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="de636-205">Приостановка и возобновление работы конвейеров</span><span class="sxs-lookup"><span data-stu-id="de636-205">Pause and resume pipelines</span></span>
<span data-ttu-id="de636-206">Управлять конвейерами можно с помощью Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="de636-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="de636-207">Например, вы можете приостановить и возобновить работу конвейеров, используя командлеты Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de636-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="de636-208">Представление схемы не поддерживает приостановку и возобновление конвейеров.</span><span class="sxs-lookup"><span data-stu-id="de636-208">The diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="de636-209">Если вы хотите использовать пользовательский интерфейс, используйте приложение для мониторинга и управления.</span><span class="sxs-lookup"><span data-stu-id="de636-209">If you want to use an user interface, use the monitoring and managing application.</span></span> <span data-ttu-id="de636-210">Чтобы узнать больше об этом приложении, ознакомьтесь со статьей [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения для мониторинга и управления](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="de636-210">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="de636-211">Вы можете приостановить работу конвейеров с помощью командлета PowerShell **Suspend-AzureRmDataFactoryPipeline**.</span><span class="sxs-lookup"><span data-stu-id="de636-211">You can pause/suspend pipelines by using the **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="de636-212">Этот командлет полезен, если не требуется запускать конвейеры до устранения проблемы.</span><span class="sxs-lookup"><span data-stu-id="de636-212">This cmdlet is useful when you don’t want to run your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="de636-213">Например:</span><span class="sxs-lookup"><span data-stu-id="de636-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="de636-214">Устранив проблему в конвейере, возобновите его работу. Для этого выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="de636-214">After the issue has been fixed with the pipeline, you can resume the suspended pipeline by running the following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="de636-215">Например:</span><span class="sxs-lookup"><span data-stu-id="de636-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="de636-216">Отладка конвейеров</span><span class="sxs-lookup"><span data-stu-id="de636-216">Debug pipelines</span></span>
<span data-ttu-id="de636-217">Фабрика данных Azure предоставляет широкие возможности отладки и устранения неполадок с конвейерами с помощью портала Azure и Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de636-217">Azure Data Factory provides rich capabilities for you to debug and troubleshoot pipelines by using the Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="de636-218">Примечание. Гораздо проще устранять ошибки и проблемы с помощью приложения для мониторинга и управления.</span><span class="sxs-lookup"><span data-stu-id="de636-218">[!NOTE} It is much easier to troubleshot errors using the Monitoring & Management App.</span></span> <span data-ttu-id="de636-219">Чтобы узнать больше об этом приложении, ознакомьтесь со статьей [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения для мониторинга и управления](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="de636-219">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="de636-220">Поиск ошибок в конвейере</span><span class="sxs-lookup"><span data-stu-id="de636-220">Find errors in a pipeline</span></span>
<span data-ttu-id="de636-221">Если при выполнении действия в конвейере происходит сбой, созданный конвейером набор данных будет находиться в состоянии "Ошибка".</span><span class="sxs-lookup"><span data-stu-id="de636-221">If the activity run fails in a pipeline, the dataset that is produced by the pipeline is in an error state because of the failure.</span></span> <span data-ttu-id="de636-222">Вы можете устранить неполадки или выполнить отладку в фабрике данных Azure, используя следующие методы.</span><span class="sxs-lookup"><span data-stu-id="de636-222">You can debug and troubleshoot errors in Azure Data Factory by using the following methods.</span></span>

#### <a name="use-the-azure-portal-to-debug-an-error"></a><span data-ttu-id="de636-223">Отладка ошибок с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="de636-223">Use the Azure portal to debug an error</span></span>
1. <span data-ttu-id="de636-224">В колонке **Таблица** щелкните проблемный срез с **состоянием** **Сбой**.</span><span class="sxs-lookup"><span data-stu-id="de636-224">On the **Table** blade, click the problem slice that has the **Status** set to **Failed**.</span></span>

   ![Колонка "Таблица" с проблемным срезом](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="de636-226">В колонке **Срез данных** щелкните цикл выполнения действия, который завершился ошибкой.</span><span class="sxs-lookup"><span data-stu-id="de636-226">On the **Data slice** blade, click the activity run that failed.</span></span>

   ![Срез данных с ошибкой](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="de636-228">В колонке **Подробности о выполнении операции** вы можете скачать файлы, связанные с обработкой HDInsight.</span><span class="sxs-lookup"><span data-stu-id="de636-228">On the **Activity run details** blade, you can download the files that are associated with the HDInsight processing.</span></span> <span data-ttu-id="de636-229">Чтобы скачать файл журнала ошибок c подробными сведениями об ошибке, щелкните **Скачать** в строке журнала Status/stderr.</span><span class="sxs-lookup"><span data-stu-id="de636-229">Click **Download** for Status/stderr to download the error log file that contains details about the error.</span></span>

   ![Колонка "Сведения о циклах выполнения действия" с ошибкой](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-to-debug-an-error"></a><span data-ttu-id="de636-231">Отладка ошибок с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="de636-231">Use PowerShell to debug an error</span></span>
1. <span data-ttu-id="de636-232">Запустите **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="de636-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="de636-233">Выполните команду **Get-AzureRmDataFactorySlice**, чтобы просмотреть срезы и их состояние.</span><span class="sxs-lookup"><span data-stu-id="de636-233">Run the **Get-AzureRmDataFactorySlice** command to see the slices and their statuses.</span></span> <span data-ttu-id="de636-234">Вы должны увидеть срез с состоянием **Сбой**.</span><span class="sxs-lookup"><span data-stu-id="de636-234">You should see a slice with the status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="de636-235">Например:</span><span class="sxs-lookup"><span data-stu-id="de636-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="de636-236">Замените **StartDateTime** на время запуска конвейера.</span><span class="sxs-lookup"><span data-stu-id="de636-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="de636-237">Теперь запустите командлет **Get-AzureRmDataFactoryRun**, чтобы получить подробные сведения о выполненном для среза действии.</span><span class="sxs-lookup"><span data-stu-id="de636-237">Now, run the **Get-AzureRmDataFactoryRun** cmdlet to get details about the activity run for the slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="de636-238">Например:</span><span class="sxs-lookup"><span data-stu-id="de636-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="de636-239">В качестве значения StartDateTime укажите время начала для проблемного (содержащего ошибку) среза, которое вы отметили на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="de636-239">The value of StartDateTime is the start time for the error/problem slice that you noted from the previous step.</span></span> <span data-ttu-id="de636-240">Значение даты-времени необходимо заключить в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="de636-240">The date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="de636-241">Вы должны увидеть выходные данные с подробными сведениями об ошибке, аналогичные следующим:</span><span class="sxs-lookup"><span data-stu-id="de636-241">You should see output with details about the error that is similar to the following:</span></span>

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. <span data-ttu-id="de636-242">Вы можете выполнить командлет **Save-AzureRmDataFactoryLog** с идентификатором, который отображается в результате команд, и скачать файлы журналов, используя параметр **-DownloadLogsoption** командлета.</span><span class="sxs-lookup"><span data-stu-id="de636-242">You can run the **Save-AzureRmDataFactoryLog** cmdlet with the Id value that you see from the output, and download the log files by using the **-DownloadLogsoption** for the cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="de636-243">Повторная обработка проблемных срезов в конвейере</span><span class="sxs-lookup"><span data-stu-id="de636-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de636-244">Использование приложения для мониторинга и управления облегчает устранение ошибок и перезапуск неудачных срезов.</span><span class="sxs-lookup"><span data-stu-id="de636-244">It's easier to troubleshoot errors and rerun failed slices by using the Monitoring & Management App.</span></span> <span data-ttu-id="de636-245">Чтобы узнать больше об этом приложении, ознакомьтесь со статьей [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения для мониторинга и управления](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="de636-245">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-the-azure-portal"></a><span data-ttu-id="de636-246">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="de636-246">Use the Azure portal</span></span>
<span data-ttu-id="de636-247">После устранения неполадок и отладки ошибок в конвейере можно повторно обработать срез с ошибками. Для этого выберите срез и на панели команд нажмите кнопку **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="de636-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating to the error slice and clicking the **Run** button on the command bar.</span></span>

![Повторная обработка среза](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="de636-249">Если срез не прошел проверку из-за ошибки политики (например, данные недоступны), вы можете исправить ошибку и повторно выполнить проверку, нажав на панели команд кнопку **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="de636-249">In case the slice has failed validation because of a policy failure (for example, if data isn't available), you can fix the failure and validate again by clicking the **Validate** button on the command bar.</span></span>

![Исправление ошибок и проверка](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="de636-251">Использование Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="de636-251">Use Azure PowerShell</span></span>
<span data-ttu-id="de636-252">Вы можете повторно обработать проблемные срезы, используя командлет **Set-AzureRmDataFactorySliceStatus**.</span><span class="sxs-lookup"><span data-stu-id="de636-252">You can rerun failures by using the **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="de636-253">Синтаксис и другие сведения об этом командлете см. в соответствующем разделе статьи [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx).</span><span class="sxs-lookup"><span data-stu-id="de636-253">See the [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about the cmdlet.</span></span>

<span data-ttu-id="de636-254">**Пример**</span><span class="sxs-lookup"><span data-stu-id="de636-254">**Example:**</span></span>

<span data-ttu-id="de636-255">В следующем примере состояние всех срезов в таблице DAWikiAggregatedData в фабрике данных WikiADF меняется на Waiting.</span><span class="sxs-lookup"><span data-stu-id="de636-255">The following example sets the status of all slices for the table 'DAWikiAggregatedData' to 'Waiting' in the Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="de636-256">Для UpdateType задано значение UpstreamInPipeline. Это означает, что состояние каждого среза в таблице и всех зависимых (восходящих) таблиц переходит в состояние Waiting.</span><span class="sxs-lookup"><span data-stu-id="de636-256">The 'UpdateType' is set to 'UpstreamInPipeline', which means that statuses of each slice for the table and all the dependent (upstream) tables are set to 'Waiting'.</span></span> <span data-ttu-id="de636-257">Этот параметр может иметь еще одно значение — Individual.</span><span class="sxs-lookup"><span data-stu-id="de636-257">The other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="de636-258">Создание оповещений</span><span class="sxs-lookup"><span data-stu-id="de636-258">Create alerts</span></span>
<span data-ttu-id="de636-259">Azure регистрирует пользовательские события, когда ресурс Azure (например, фабрика данных) создается, обновляется или удаляется.</span><span class="sxs-lookup"><span data-stu-id="de636-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="de636-260">Вы можете создавать оповещения об этих событиях.</span><span class="sxs-lookup"><span data-stu-id="de636-260">You can create alerts on these events.</span></span> <span data-ttu-id="de636-261">Фабрика данных позволяет собирать различные метрики и создавать по ним оповещения.</span><span class="sxs-lookup"><span data-stu-id="de636-261">You can use Data Factory to capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="de636-262">Мы советуем использовать события для наблюдения в режиме реального времени, а метрики — для статистических целей.</span><span class="sxs-lookup"><span data-stu-id="de636-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="de636-263">Оповещения о событиях</span><span class="sxs-lookup"><span data-stu-id="de636-263">Alerts on events</span></span>
<span data-ttu-id="de636-264">События Azure позволяют получить представление о том, что происходит в ресурсах Azure.</span><span class="sxs-lookup"><span data-stu-id="de636-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="de636-265">При использовании фабрики данных Azure события создаются, когда:</span><span class="sxs-lookup"><span data-stu-id="de636-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="de636-266">фабрика данных создается, обновляется или удаляется;</span><span class="sxs-lookup"><span data-stu-id="de636-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="de636-267">запускается или завершается обработка данных (цикл выполнения);</span><span class="sxs-lookup"><span data-stu-id="de636-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="de636-268">создается и удаляется кластер HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="de636-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="de636-269">Вы можете создавать оповещения в этих пользовательских событиях и настраивать их для отправки уведомлений по электронной почте администраторам и соадминистраторам подписки.</span><span class="sxs-lookup"><span data-stu-id="de636-269">You can create alerts on these user events and configure them to send email notifications to the administrator and coadministrators of the subscription.</span></span> <span data-ttu-id="de636-270">Кроме того, вы можете указать дополнительные адреса электронной почты пользователей, которые должны получать уведомления по электронной почте при выполнении определенных условий.</span><span class="sxs-lookup"><span data-stu-id="de636-270">In addition, you can specify additional email addresses of users who need to receive email notifications when the conditions are met.</span></span> <span data-ttu-id="de636-271">Эта функция удобна, когда нужно получать уведомления о сбоях, но не требуется постоянно отслеживать состояние фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="de636-271">This feature is useful when you want to get notified on failures and don’t want to continuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="de636-272">В настоящее время портал не отображает оповещения о событиях.</span><span class="sxs-lookup"><span data-stu-id="de636-272">Currently, the portal doesn't show alerts on events.</span></span> <span data-ttu-id="de636-273">Используйте [приложение по мониторингу и управлению](data-factory-monitor-manage-app.md) для просмотра всех оповещений.</span><span class="sxs-lookup"><span data-stu-id="de636-273">Use the [Monitoring and Management app](data-factory-monitor-manage-app.md) to see all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="de636-274">Задание определения оповещения</span><span class="sxs-lookup"><span data-stu-id="de636-274">Specify an alert definition</span></span>
<span data-ttu-id="de636-275">Чтобы задать определение оповещения, создайте файл JSON, описывающий операции, о которых вы хотите получать оповещения.</span><span class="sxs-lookup"><span data-stu-id="de636-275">To specify an alert definition, you create a JSON file that describes the operations that you want to be alerted on.</span></span> <span data-ttu-id="de636-276">В следующем примере отправляется электронное уведомление об операции RunFinished.</span><span class="sxs-lookup"><span data-stu-id="de636-276">In the following example, the alert sends an email notification for the RunFinished operation.</span></span> <span data-ttu-id="de636-277">Другими словами, оно отправляется в случае завершения цикла выполнения действия в фабрике данных со сбоем (состояние = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="de636-277">To be specific, an email notification is sent when a run in the data factory has completed and the run has failed (Status = FailedExecution).</span></span>

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of the data slices for the Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

<span data-ttu-id="de636-278">Вы можете удалить **subStatus** в определении JSON, если не хотите получать оповещение при конкретном сбое.</span><span class="sxs-lookup"><span data-stu-id="de636-278">You can remove **subStatus** from the JSON definition if you don’t want to be alerted on a specific failure.</span></span>

<span data-ttu-id="de636-279">Этот пример устанавливает оповещение для всех фабрик данных в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="de636-279">This example sets up the alert for all data factories in your subscription.</span></span> <span data-ttu-id="de636-280">Если вам необходимо установить оповещение для определенной фабрики данных, можно указать ее значение **resourceUri** в **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="de636-280">If you want the alert to be set up for a particular data factory, you can specify data factory **resourceUri** in the **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="de636-281">Список возможных операций и состояний (а также дополнительных состояний) см. в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="de636-281">The following table provides the list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="de636-282">Имя операции</span><span class="sxs-lookup"><span data-stu-id="de636-282">Operation name</span></span> | <span data-ttu-id="de636-283">Состояние</span><span class="sxs-lookup"><span data-stu-id="de636-283">Status</span></span> | <span data-ttu-id="de636-284">Подсостояние</span><span class="sxs-lookup"><span data-stu-id="de636-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de636-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="de636-285">RunStarted</span></span> |<span data-ttu-id="de636-286">Started</span><span class="sxs-lookup"><span data-stu-id="de636-286">Started</span></span> |<span data-ttu-id="de636-287">Starting</span><span class="sxs-lookup"><span data-stu-id="de636-287">Starting</span></span> |
| <span data-ttu-id="de636-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="de636-288">RunFinished</span></span> |<span data-ttu-id="de636-289">Failed / Succeeded</span><span class="sxs-lookup"><span data-stu-id="de636-289">Failed / Succeeded</span></span> |<span data-ttu-id="de636-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="de636-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="de636-291">Succeeded</span><span class="sxs-lookup"><span data-stu-id="de636-291">Succeeded</span></span><br/><br/><span data-ttu-id="de636-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="de636-292">FailedExecution</span></span><br/><br/><span data-ttu-id="de636-293">TimedOut</span><span class="sxs-lookup"><span data-stu-id="de636-293">TimedOut</span></span><br/><br/><span data-ttu-id="de636-294"><Canceled</span><span class="sxs-lookup"><span data-stu-id="de636-294"><Canceled</span></span><br/><br/><span data-ttu-id="de636-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="de636-295">FailedValidation</span></span><br/><br/><span data-ttu-id="de636-296">Abandoned</span><span class="sxs-lookup"><span data-stu-id="de636-296">Abandoned</span></span> |
| <span data-ttu-id="de636-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="de636-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="de636-298">Started</span><span class="sxs-lookup"><span data-stu-id="de636-298">Started</span></span> | |
| <span data-ttu-id="de636-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="de636-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="de636-300">Успешно</span><span class="sxs-lookup"><span data-stu-id="de636-300">Succeeded</span></span> | |
| <span data-ttu-id="de636-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="de636-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="de636-302">Успешно</span><span class="sxs-lookup"><span data-stu-id="de636-302">Succeeded</span></span> | |

<span data-ttu-id="de636-303">Дополнительные сведения об элементах JSON, используемых в примере, см. в статье о том, как [создать правило оповещения](https://msdn.microsoft.com/library/azure/dn510366.aspx).</span><span class="sxs-lookup"><span data-stu-id="de636-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about the JSON elements that are used in the example.</span></span>

#### <a name="deploy-the-alert"></a><span data-ttu-id="de636-304">Развертывание оповещения</span><span class="sxs-lookup"><span data-stu-id="de636-304">Deploy the alert</span></span>
<span data-ttu-id="de636-305">Для развертывания оповещения используйте командлет Azure PowerShell **New-AzureRmResourceGroupDeployment**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="de636-305">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="de636-306">После успешного завершения развертывания группы ресурсов вы увидите следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="de636-306">After the resource group deployment has finished successfully, you see the following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - The StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts to remove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> <span data-ttu-id="de636-307">Можно использовать REST API [Создать правило оповещения](https://msdn.microsoft.com/library/azure/dn510366.aspx) для создания правила оповещения.</span><span class="sxs-lookup"><span data-stu-id="de636-307">You can use the [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API to create an alert rule.</span></span> <span data-ttu-id="de636-308">Полезные данные JSON аналогичны JSON в примере.</span><span class="sxs-lookup"><span data-stu-id="de636-308">The JSON payload is similar to the JSON example.</span></span>  


#### <a name="retrieve-the-list-of-azure-resource-group-deployments"></a><span data-ttu-id="de636-309">Получение списка развертываний групп ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="de636-309">Retrieve the list of Azure resource group deployments</span></span>
<span data-ttu-id="de636-310">Чтобы получить список развертываний групп ресурсов Azure, используйте командлет **Get-AzureRmResourceGroupDeployment**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="de636-310">To retrieve the list of deployed Azure resource group deployments, use the cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="de636-311">Устранение неполадок пользовательских событий</span><span class="sxs-lookup"><span data-stu-id="de636-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="de636-312">Вы можете просмотреть все созданные события, щелкнув плитку **Метрики и операции**.</span><span class="sxs-lookup"><span data-stu-id="de636-312">You can see all the events that are generated after clicking the **Metrics and operations** tile.</span></span>

    ![Элемент "Метрики и операции"](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="de636-314">Щелкните плитку **События** для просмотра событий.</span><span class="sxs-lookup"><span data-stu-id="de636-314">Click the **Events** tile to see the events.</span></span>

    ![Плитки "События"](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="de636-316">В колонке **События** можно просмотреть подробные сведения о событиях, фильтровать их и т. д.</span><span class="sxs-lookup"><span data-stu-id="de636-316">On the **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Колонка "События"](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="de636-318">В списке операций выберите **операцию**, которая вызывает ошибку.</span><span class="sxs-lookup"><span data-stu-id="de636-318">Click an **Operation** in the operations list that causes an error.</span></span>

    ![Выберите операцию](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="de636-320">Щелкните событие **ошибки**, чтобы просмотреть сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="de636-320">Click an **Error** event to see details about the error.</span></span>

    ![Ошибка события](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="de636-322">Сведения о командлетах PowerShell, которые можно использовать для добавления, получения и удаления предупреждений, см. в статье о [командлетах Azure Insight](https://msdn.microsoft.com/library/mt282452.aspx).</span><span class="sxs-lookup"><span data-stu-id="de636-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use to add, get, or remove alerts.</span></span> <span data-ttu-id="de636-323">Далее приведено несколько примеров использования командлета **Get-AlertRule**:</span><span class="sxs-lookup"><span data-stu-id="de636-323">Here are a few examples of using the **Get-AlertRule** cmdlet:</span></span>

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of the data slices for the Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

<span data-ttu-id="de636-324">Выполните следующие команды get-help, чтобы просмотреть сведения и примеры для командлета Get-AlertRule.</span><span class="sxs-lookup"><span data-stu-id="de636-324">Run the following get-help commands to see details and examples for the Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="de636-325">Если события-триггеры отображаются в колонке на портале, но вы не получаете электронных уведомлений, убедитесь, что ваш адрес электронной почты может получать сообщения от внешних отправителей.</span><span class="sxs-lookup"><span data-stu-id="de636-325">If you see the alert generation events on the portal blade but you don't receive email notifications, check whether the email address that is specified is set to receive emails from external senders.</span></span> <span data-ttu-id="de636-326">Получение оповещений может быть заблокировано в параметрах электронной почты.</span><span class="sxs-lookup"><span data-stu-id="de636-326">The alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="de636-327">Оповещения по метрикам</span><span class="sxs-lookup"><span data-stu-id="de636-327">Alerts on metrics</span></span>
<span data-ttu-id="de636-328">Фабрика данных позволяет собирать различные метрики и создавать по ним оповещения.</span><span class="sxs-lookup"><span data-stu-id="de636-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="de636-329">Вы можете отслеживать и создавать оповещения по следующим метрикам срезов в фабрике данных:</span><span class="sxs-lookup"><span data-stu-id="de636-329">You can monitor and create alerts on the following metrics for the slices in your data factory:</span></span>

* <span data-ttu-id="de636-330">**циклы выполнения со сбоем**;</span><span class="sxs-lookup"><span data-stu-id="de636-330">**Failed Runs**</span></span>
* <span data-ttu-id="de636-331">**успешные циклы выполнения**.</span><span class="sxs-lookup"><span data-stu-id="de636-331">**Successful Runs**</span></span>

<span data-ttu-id="de636-332">Эти метрики позволяют получать общее представление обо всех успешных и проблемных циклах в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="de636-332">These metrics are useful and help you to get an overview of overall failed and successful runs in the data factory.</span></span> <span data-ttu-id="de636-333">Метрики создаются при каждом цикле выполнения действия со срезом.</span><span class="sxs-lookup"><span data-stu-id="de636-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="de636-334">Все созданные за час метрики собираются и передаются в вашу учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="de636-334">At the beginning of the hour, these metrics are aggregated and pushed to your storage account.</span></span> <span data-ttu-id="de636-335">Чтобы включить метрики, необходимо настроить учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="de636-335">To enable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="de636-336">Включить метрики</span><span class="sxs-lookup"><span data-stu-id="de636-336">Enable metrics</span></span>
<span data-ttu-id="de636-337">Чтобы включить метрики, в колонке **Фабрика данных** выберите следующее:</span><span class="sxs-lookup"><span data-stu-id="de636-337">To enable metrics, click the following from the **Data Factory** blade:</span></span>

<span data-ttu-id="de636-338">**Мониторинг** > **Метрика** > **Параметры диагностики** > **Диагностика**</span><span class="sxs-lookup"><span data-stu-id="de636-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Ссылка диагностики](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="de636-340">В колонке **Диагностика** щелкните **Вкл.**, выберите учетную запись хранения и щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="de636-340">On the **Diagnostics** blade, click **On**, select the storage account, and click **Save**.</span></span>

![Выноска "Диагностика"](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="de636-342">Так как метрики агрегируются ежечасно, между сохранением и отображением метрик в колонке **Мониторинг** может пройти час.</span><span class="sxs-lookup"><span data-stu-id="de636-342">It might take up to one hour for the metrics to be visible on the **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="de636-343">Настройка оповещений по метрикам</span><span class="sxs-lookup"><span data-stu-id="de636-343">Set up an alert on metrics</span></span>
<span data-ttu-id="de636-344">Щелкните плитку **Метрики фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="de636-344">Click the **Data Factory metrics** tile:</span></span>

![Элемент "Метрики фабрики данных"](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="de636-346">В колонке **Метрика** щелкните **+ Add alert** (+ Добавить оповещение) на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="de636-346">On the **Metric** blade, click **+ Add alert** on the toolbar.</span></span>
<span data-ttu-id="de636-347">![Колонка "Метрики фабрики данных", добавление оповещения](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="de636-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="de636-348">На странице **Добавление правила оповещения** сделайте следующее и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="de636-348">On the **Add an alert rule** page, do the following steps, and click **OK**.</span></span>

* <span data-ttu-id="de636-349">Введите имя для оповещения (например, оповещение о сбое).</span><span class="sxs-lookup"><span data-stu-id="de636-349">Enter a name for the alert (example: "failed alert").</span></span>
* <span data-ttu-id="de636-350">Введите описание для оповещения (например, отправка сообщения при сбое).</span><span class="sxs-lookup"><span data-stu-id="de636-350">Enter a description for the alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="de636-351">Выберите метрику (неудачные и успешные выполнения).</span><span class="sxs-lookup"><span data-stu-id="de636-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="de636-352">Укажите условие и пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="de636-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="de636-353">Укажите период времени.</span><span class="sxs-lookup"><span data-stu-id="de636-353">Specify the period of time.</span></span>
* <span data-ttu-id="de636-354">Укажите, кому следует отправлять сообщение (владельцам, участникам или читателям).</span><span class="sxs-lookup"><span data-stu-id="de636-354">Specify whether an email should be sent to owners, contributors, and readers.</span></span>

![Колонка "Метрики фабрики данных", добавление правила оповещения](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="de636-356">После успешного добавления правила оповещения колонка закрывается и в колонке **Метрика** появляется новое оповещение.</span><span class="sxs-lookup"><span data-stu-id="de636-356">After the alert rule is added successfully, the blade closes and you see the new alert on the **Metric** blade.</span></span>

![Колонка "Метрики фабрики данных", добавление нового оповещения](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="de636-358">В плитке **Правила оповещений** также появится количество оповещений.</span><span class="sxs-lookup"><span data-stu-id="de636-358">You should also see the number of alerts in the **Alert rules** tile.</span></span> <span data-ttu-id="de636-359">Щелкните плитку **Правила оповещений**.</span><span class="sxs-lookup"><span data-stu-id="de636-359">Click the **Alert rules** tile.</span></span>

![Колонка "Метрики фабрики данных", правила оповещения](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="de636-361">В колонке **Правила оповещений** можно увидеть все имеющиеся оповещения.</span><span class="sxs-lookup"><span data-stu-id="de636-361">On the **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="de636-362">Чтобы добавить оповещение, нажмите кнопку **Добавить оповещение** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="de636-362">To add an alert, click **Add alert** on the toolbar.</span></span>

![Колонка "Правила оповещения"](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="de636-364">Оповещения</span><span class="sxs-lookup"><span data-stu-id="de636-364">Alert notifications</span></span>
<span data-ttu-id="de636-365">После возникновения условия, по которому срабатывает правило оповещения, вы будете получать соответствующее электронное уведомление о том, что оповещение активировано.</span><span class="sxs-lookup"><span data-stu-id="de636-365">After the alert rule matches the condition, you should get an email that says the alert is activated.</span></span> <span data-ttu-id="de636-366">После устранения условия (т. е. оно больше не соответствует правилу оповещения) вы получите электронное уведомление о том, что причина оповещения устранена.</span><span class="sxs-lookup"><span data-stu-id="de636-366">After the issue is resolved and the alert condition doesn’t match anymore, you get an email that says the alert is resolved.</span></span>

<span data-ttu-id="de636-367">Такое поведение отличается от ситуации, когда уведомление отправляется по каждому сбою, соответствующему правилу оповещения.</span><span class="sxs-lookup"><span data-stu-id="de636-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="de636-368">Развертывание оповещений с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="de636-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="de636-369">Вы можете развернуть оповещения по метрикам так же, как и по событиям.</span><span class="sxs-lookup"><span data-stu-id="de636-369">You can deploy alerts for metrics the same way that you do for events.</span></span>

<span data-ttu-id="de636-370">**Определение оповещения**</span><span class="sxs-lookup"><span data-stu-id="de636-370">**Alert definition**</span></span>

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

<span data-ttu-id="de636-371">Замените *subscriptionId*, *resourceGroupName* и *dataFactoryName* в примере на соответствующие значения.</span><span class="sxs-lookup"><span data-stu-id="de636-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in the sample with appropriate values.</span></span>

<span data-ttu-id="de636-372">*metricName* на данный момент поддерживает два значения:</span><span class="sxs-lookup"><span data-stu-id="de636-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="de636-373">FailedRuns и</span><span class="sxs-lookup"><span data-stu-id="de636-373">FailedRuns</span></span>
* <span data-ttu-id="de636-374">SuccessfulRuns.</span><span class="sxs-lookup"><span data-stu-id="de636-374">SuccessfulRuns</span></span>

<span data-ttu-id="de636-375">**Развертывание оповещения**</span><span class="sxs-lookup"><span data-stu-id="de636-375">**Deploy the alert**</span></span>

<span data-ttu-id="de636-376">Для развертывания оповещения используйте командлет Azure PowerShell **New-AzureRmResourceGroupDeployment**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="de636-376">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="de636-377">В случае успешного развертывания вы увидите следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="de636-377">You should see following message after a successful deployment:</span></span>

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

<span data-ttu-id="de636-378">Вы также можете использовать командлет **Add-AlertRule**, чтобы развернуть правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="de636-378">You can also use the **Add-AlertRule** cmdlet to deploy an alert rule.</span></span> <span data-ttu-id="de636-379">Дополнительные сведения и примеры см. в документации [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx).</span><span class="sxs-lookup"><span data-stu-id="de636-379">See the [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-to-a-different-resource-group-or-subscription"></a><span data-ttu-id="de636-380">Перемещение фабрики данных в другую группу ресурсов или подписку</span><span class="sxs-lookup"><span data-stu-id="de636-380">Move a data factory to a different resource group or subscription</span></span>
<span data-ttu-id="de636-381">Фабрику данных можно переместить в другую группу ресурсов или подписку, воспользовавшись кнопкой **Переместить** в командной строке на домашней странице фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="de636-381">You can move a data factory to a different resource group or a different subscription by using the **Move** command bar button on the home page of your data factory.</span></span>

![Перемещение фабрики данных](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="de636-383">Вместе с фабрикой данных можно переместить все связанные ресурсы (например, связанные с ней оповещения).</span><span class="sxs-lookup"><span data-stu-id="de636-383">You can also move any related resources (such as alerts that are associated with the data factory), along with the data factory.</span></span>

![Диалоговое окно "Перемещение ресурсов"](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
