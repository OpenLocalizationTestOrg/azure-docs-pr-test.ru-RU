---
title: "aaaMonitor и управлять конвейеров с помощью PowerShell и hello портал Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure и Azure PowerShell toomonitor и управлять фабриками данных Azure hello и конвейеры, созданных."
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
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a><span data-ttu-id="d601e-103">Мониторинг и управление ими конвейеров фабрики данных Azure с помощью портала Azure hello и PowerShell</span><span class="sxs-lookup"><span data-stu-id="d601e-103">Monitor and manage Azure Data Factory pipelines by using hello Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d601e-104">Использование портала Azure или Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d601e-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="d601e-105">Использование приложения для мониторинга и управления</span><span class="sxs-lookup"><span data-stu-id="d601e-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="d601e-106">Управление и мониторинг приложения Hello предоставляет улучшенную поддержку мониторинг и управление конвейеры данных и устранение проблем.</span><span class="sxs-lookup"><span data-stu-id="d601e-106">hello monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="d601e-107">Дополнительные сведения об использовании приложения hello см. в разделе [мониторинг и управление ими конвейеров фабрики данных с помощью приложения hello мониторинг и управление](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="d601e-107">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="d601e-108">В этой статье описывается toomonitor, управлять и отлаживать конвейеров с помощью портала Azure и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d601e-108">This article describes how toomonitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="d601e-109">Hello и содержатся рекомендации о предоставлении toocreate предупреждения и получить уведомление о сбоях.</span><span class="sxs-lookup"><span data-stu-id="d601e-109">hello article also provides information on how toocreate alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="d601e-110">Состояния конвейеров и действий</span><span class="sxs-lookup"><span data-stu-id="d601e-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="d601e-111">С помощью hello портал Azure, вы можете:</span><span class="sxs-lookup"><span data-stu-id="d601e-111">By using hello Azure portal, you can:</span></span>

* <span data-ttu-id="d601e-112">представлять фабрику данных в виде схемы;</span><span class="sxs-lookup"><span data-stu-id="d601e-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="d601e-113">просматривать действия в конвейере;</span><span class="sxs-lookup"><span data-stu-id="d601e-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="d601e-114">просматривать входные и выходные наборы данных.</span><span class="sxs-lookup"><span data-stu-id="d601e-114">View input and output datasets.</span></span>

<span data-ttu-id="d601e-115">В этом разделе также описываются переходы среза набора данных из одного состояния tooanother состояния.</span><span class="sxs-lookup"><span data-stu-id="d601e-115">This section also describes how a dataset slice transitions from one state tooanother state.</span></span>   

### <a name="navigate-tooyour-data-factory"></a><span data-ttu-id="d601e-116">Перейдите tooyour фабрики данных</span><span class="sxs-lookup"><span data-stu-id="d601e-116">Navigate tooyour data factory</span></span>
1. <span data-ttu-id="d601e-117">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d601e-117">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d601e-118">Нажмите кнопку **фабрик данных** hello меню слева hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-118">Click **Data factories** on hello menu on hello left.</span></span> <span data-ttu-id="d601e-119">Если вы не видите его, нажмите кнопку **дополнительные службы >**, а затем нажмите кнопку **фабрик данных** под hello **АНАЛИТИКИ + АНАЛИТИКА** категории.</span><span class="sxs-lookup"><span data-stu-id="d601e-119">If you don't see it, click **More services >**, and then click **Data factories** under hello **INTELLIGENCE + ANALYTICS** category.</span></span>

   !["Просмотреть все" -> "Фабрики данных"](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="d601e-121">На hello **фабрик данных** колонки, выберите hello фабрики данных, который вас интересует.</span><span class="sxs-lookup"><span data-stu-id="d601e-121">On hello **Data factories** blade, select hello data factory that you're interested in.</span></span>

    ![Выбор фабрики данных](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="d601e-123">Вы увидите домашнюю страницу приветствия для фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-123">You should see hello home page for hello data factory.</span></span>

   ![Колонка "Фабрика данных"](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="d601e-125">Представление фабрики данных в виде схемы</span><span class="sxs-lookup"><span data-stu-id="d601e-125">Diagram view of your data factory</span></span>
<span data-ttu-id="d601e-126">Hello **схема** представление фабрики данных предоставляет единое toomonitor стекла и управлять hello фабрики данных и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d601e-126">hello **Diagram** view of a data factory provides a single pane of glass toomonitor and manage hello data factory and its assets.</span></span> <span data-ttu-id="d601e-127">toosee hello **схема** фабрики данных, щелкните **схема** на домашней странице приветствия для фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-127">toosee hello **Diagram** view of your data factory, click **Diagram** on hello home page for hello data factory.</span></span>

![Представление схемы](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="d601e-129">Можно увеличить масштаб, уменьшить масштаб toofit масштаба, % too100 масштаба, блокировка hello макет диаграммы hello и автоматическое расположение конвейеров и наборы данных.</span><span class="sxs-lookup"><span data-stu-id="d601e-129">You can zoom in, zoom out, zoom toofit, zoom too100%, lock hello layout of hello diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="d601e-130">Можно также просмотреть информацию журнала обращений и преобразований данных hello (то есть, Показать восходящие и нисходящие элементы выбранных элементов).</span><span class="sxs-lookup"><span data-stu-id="d601e-130">You can also see hello data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="d601e-131">Действия в конвейере</span><span class="sxs-lookup"><span data-stu-id="d601e-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="d601e-132">Щелкните правой кнопкой мыши конвейера hello и нажмите кнопку **откройте конвейера** toosee конвейера все действия в hello, а также входные и выходные наборы данных для действия hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-132">Right-click hello pipeline, and then click **Open pipeline** toosee all activities in hello pipeline, along with input and output datasets for hello activities.</span></span> <span data-ttu-id="d601e-133">Эта возможность полезна, конвейер содержит более одного действия, если необходимо toounderstand hello оперативной журнала обращений и преобразований из одного конвейера.</span><span class="sxs-lookup"><span data-stu-id="d601e-133">This feature is useful when your pipeline includes more than one activity and you want toounderstand hello operational lineage of a single pipeline.</span></span>

    ![Откройте меню конвейера](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="d601e-135">В следующем примере hello вы видите операции копирования в конвейере hello с входным и выходным.</span><span class="sxs-lookup"><span data-stu-id="d601e-135">In hello following example, you see a copy activity in hello pipeline with an input and an output.</span></span> 

    ![Действия в конвейере](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="d601e-137">Можно перейти назад toohello Домашняя страница hello фабрики данных, щелкнув hello **фабрики данных** ссылку на навигатора hello в левом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-137">You can navigate back toohello home page of hello data factory by clicking hello **Data factory** link in hello breadcrumb at hello top-left corner.</span></span>

    ![Перейдите назад toodata фабрики](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="d601e-139">Представление hello состояние каждого действия в конвейере</span><span class="sxs-lookup"><span data-stu-id="d601e-139">View hello state of each activity inside a pipeline</span></span>
<span data-ttu-id="d601e-140">Hello текущее состояние действия можно отследить, просмотрев состояние hello какой-либо hello наборов данных, полученных с действия "hello".</span><span class="sxs-lookup"><span data-stu-id="d601e-140">You can view hello current state of an activity by viewing hello status of any of hello datasets that are produced by hello activity.</span></span>

<span data-ttu-id="d601e-141">Двойным щелчком hello **OutputBlobTable** в hello **схема**, вы увидите все срезы hello, созданные при выполнении различных действий в конвейере.</span><span class="sxs-lookup"><span data-stu-id="d601e-141">By double-clicking hello **OutputBlobTable** in hello **Diagram**, you can see all hello slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="d601e-142">Можно увидеть, что действие копирования hello успешно выполнен для hello последние восемь часов и полученных фрагментов hello в hello **готовности** состояния.</span><span class="sxs-lookup"><span data-stu-id="d601e-142">You can see that hello copy activity ran successfully for hello last eight hours and produced hello slices in hello **Ready** state.</span></span>  

![Состояние конвейера hello](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="d601e-144">Hello срезов набор данных в фабрике данных hello может иметь одно из следующих статусов hello:</span><span class="sxs-lookup"><span data-stu-id="d601e-144">hello dataset slices in hello data factory can have one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="d601e-145">Состояние</span><span class="sxs-lookup"><span data-stu-id="d601e-145">State</span></span></th><th align="left"><span data-ttu-id="d601e-146">Подсостояние</span><span class="sxs-lookup"><span data-stu-id="d601e-146">Substate</span></span></th><th align="left"><span data-ttu-id="d601e-147">Описание</span><span class="sxs-lookup"><span data-stu-id="d601e-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="d601e-148">Waiting</span><span class="sxs-lookup"><span data-stu-id="d601e-148">Waiting</span></span></td><td><span data-ttu-id="d601e-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="d601e-149">ScheduleTime</span></span></td><td><span data-ttu-id="d601e-150">время Hello не входят в toorun срез hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-150">hello time hasn't come for hello slice toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d601e-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="d601e-151">DatasetDependencies</span></span></td><td><span data-ttu-id="d601e-152">Hello восходящие зависимости не готовы.</span><span class="sxs-lookup"><span data-stu-id="d601e-152">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d601e-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="d601e-153">ComputeResources</span></span></td><td><span data-ttu-id="d601e-154">Hello вычислительные ресурсы недоступны.</span><span class="sxs-lookup"><span data-stu-id="d601e-154">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d601e-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="d601e-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="d601e-156">Все экземпляры действий hello заняты обработкой других срезов.</span><span class="sxs-lookup"><span data-stu-id="d601e-156">All hello activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d601e-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="d601e-157">ActivityResume</span></span></td><td><span data-ttu-id="d601e-158">Действие Hello приостановлено и не могут выполняться hello фрагментов до возобновления действия hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-158">hello activity is paused and can't run hello slices until hello activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d601e-159">Retry</span><span class="sxs-lookup"><span data-stu-id="d601e-159">Retry</span></span></td><td><span data-ttu-id="d601e-160">Действие выполняется повторно.</span><span class="sxs-lookup"><span data-stu-id="d601e-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d601e-161">Проверка</span><span class="sxs-lookup"><span data-stu-id="d601e-161">Validation</span></span></td><td><span data-ttu-id="d601e-162">Проверка еще не начата.</span><span class="sxs-lookup"><span data-stu-id="d601e-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d601e-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="d601e-163">ValidationRetry</span></span></td><td><span data-ttu-id="d601e-164">Проверка выполняется повторная toobe ожидания.</span><span class="sxs-lookup"><span data-stu-id="d601e-164">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="d601e-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="d601e-165">InProgress</span></span></td><td><span data-ttu-id="d601e-166">Validating</span><span class="sxs-lookup"><span data-stu-id="d601e-166">Validating</span></span></td><td><span data-ttu-id="d601e-167">Проверка выполняется.</span><span class="sxs-lookup"><span data-stu-id="d601e-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="d601e-168">Hello срез обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="d601e-168">hello slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="d601e-169">Сбой</span><span class="sxs-lookup"><span data-stu-id="d601e-169">Failed</span></span></td><td><span data-ttu-id="d601e-170">TimedOut</span><span class="sxs-lookup"><span data-stu-id="d601e-170">TimedOut</span></span></td><td><span data-ttu-id="d601e-171">Выполнение действия Hello продолжалась дольше, чем допустимых с действия "hello".</span><span class="sxs-lookup"><span data-stu-id="d601e-171">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d601e-172">Canceled</span><span class="sxs-lookup"><span data-stu-id="d601e-172">Canceled</span></span></td><td><span data-ttu-id="d601e-173">срез Hello была отменена пользователем.</span><span class="sxs-lookup"><span data-stu-id="d601e-173">hello slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d601e-174">Проверка</span><span class="sxs-lookup"><span data-stu-id="d601e-174">Validation</span></span></td><td><span data-ttu-id="d601e-175">Сбой проверки.</span><span class="sxs-lookup"><span data-stu-id="d601e-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="d601e-176">срез Hello сбой toobe создан и (или) проверки.</span><span class="sxs-lookup"><span data-stu-id="d601e-176">hello slice failed toobe generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="d601e-177">Ready</span><span class="sxs-lookup"><span data-stu-id="d601e-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="d601e-178">Hello срез будет готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="d601e-178">hello slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d601e-179">Skipped</span><span class="sxs-lookup"><span data-stu-id="d601e-179">Skipped</span></span></td><td><span data-ttu-id="d601e-180">None</span><span class="sxs-lookup"><span data-stu-id="d601e-180">None</span></span></td><td><span data-ttu-id="d601e-181">срез Hello не обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="d601e-181">hello slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d601e-182">None</span><span class="sxs-lookup"><span data-stu-id="d601e-182">None</span></span></td><td>-</td><td><span data-ttu-id="d601e-183">Срез используется tooexist в другом состоянии, но был сброшен.</span><span class="sxs-lookup"><span data-stu-id="d601e-183">A slice used tooexist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="d601e-184">Hello сведения о срез можно просмотреть, щелкнув запись среза на hello **недавно обновлен фрагменты** колонку.</span><span class="sxs-lookup"><span data-stu-id="d601e-184">You can view hello details about a slice by clicking a slice entry on hello **Recently Updated Slices** blade.</span></span>

![Сведения о срезе](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="d601e-186">Если срез hello выполнен несколько раз, можно увидеть несколько строки в hello **действие выполняется** списка.</span><span class="sxs-lookup"><span data-stu-id="d601e-186">If hello slice has been executed multiple times, you see multiple rows in hello **Activity runs** list.</span></span> <span data-ttu-id="d601e-187">Для просмотра сведений о действии, запустить, щелкнув hello выполнить запись в hello **действие выполняется** списка.</span><span class="sxs-lookup"><span data-stu-id="d601e-187">You can view details about an activity run by clicking hello run entry in hello **Activity runs** list.</span></span> <span data-ttu-id="d601e-188">Hello список hello файлов журнала, а также сообщение об ошибке, если таковой имеется.</span><span class="sxs-lookup"><span data-stu-id="d601e-188">hello list shows all hello log files, along with an error message if there is one.</span></span> <span data-ttu-id="d601e-189">Эта возможность очень полезна tooview и отладочный журналы без необходимости tooleave фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="d601e-189">This feature is useful tooview and debug logs without having tooleave your data factory.</span></span>

![СВЕДЕНИЯ О ВЫПОЛНЕННОМ ДЕЙСТВИИ](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="d601e-191">Если срез hello не hello **готовности** состояние, можно увидеть hello восходящие срезы, которые не готовы и блокируют hello текущего среза выполнения в hello **восходящие срезы, которые не готовы** списка.</span><span class="sxs-lookup"><span data-stu-id="d601e-191">If hello slice isn't in hello **Ready** state, you can see hello upstream slices that aren't ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="d601e-192">Эта возможность полезна, когда ваш среза находится в **ожидания** состояние и требуется ожидание восходящие зависимости hello toounderstand, которые hello среза.</span><span class="sxs-lookup"><span data-stu-id="d601e-192">This feature is useful when your slice is in **Waiting** state and you want toounderstand hello upstream dependencies that hello slice is waiting on.</span></span>

![Неготовые восходящие срезы](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="d601e-194">Схема состояний наборов данных</span><span class="sxs-lookup"><span data-stu-id="d601e-194">Dataset state diagram</span></span>
<span data-ttu-id="d601e-195">После развертывания фабрику данных и конвейеры hello имеют допустимые активного периода, набор данных hello срезы переход из одного состояния tooanother.</span><span class="sxs-lookup"><span data-stu-id="d601e-195">After you deploy a data factory and hello pipelines have a valid active period, hello dataset slices transition from one state tooanother.</span></span> <span data-ttu-id="d601e-196">В настоящее время состояние среза hello ниже hello, следующая схема состояний:</span><span class="sxs-lookup"><span data-stu-id="d601e-196">Currently, hello slice status follows hello following state diagram:</span></span>

![Схема состояний](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="d601e-198">Hello поток переход состояния набора данных в фабрике данных необходимо hello в следующем: ожидание -> в ход выполнения и выполнение (проверка) -> готов или ошибка.</span><span class="sxs-lookup"><span data-stu-id="d601e-198">hello dataset state transition flow in data factory is hello following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="d601e-199">срез Hello начинается **ожидания** состояния, ожидая toobe предварительные условия выполнены, прежде чем он выполняется.</span><span class="sxs-lookup"><span data-stu-id="d601e-199">hello slice starts in a **Waiting** state, waiting for preconditions toobe met before it executes.</span></span> <span data-ttu-id="d601e-200">Затем начала выполнения действия hello и срез hello переходит в **выполняющиеся** состояния.</span><span class="sxs-lookup"><span data-stu-id="d601e-200">Then, hello activity starts executing, and hello slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="d601e-201">Выполнение действия Hello может завершаются успехом или сбоем.</span><span class="sxs-lookup"><span data-stu-id="d601e-201">hello activity execution might succeed or fail.</span></span> <span data-ttu-id="d601e-202">Hello среза помечается как **готовности** или **сбой**, основываясь на hello результат выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-202">hello slice is marked as **Ready** or **Failed**, based on hello result of hello execution.</span></span>

<span data-ttu-id="d601e-203">Можно сбросить toogo срез hello обратно из hello **готовности** или **сбой** toohello состояние **ожидания** состояния.</span><span class="sxs-lookup"><span data-stu-id="d601e-203">You can reset hello slice toogo back from hello **Ready** or **Failed** state toohello **Waiting** state.</span></span> <span data-ttu-id="d601e-204">Можно также пометить состояние среза hello слишком**пропустить**, позволяющая активности hello, выполнение и не обработки среза hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-204">You can also mark hello slice state too**Skip**, which prevents hello activity from executing and not processing hello slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="d601e-205">Приостановка и возобновление работы конвейеров</span><span class="sxs-lookup"><span data-stu-id="d601e-205">Pause and resume pipelines</span></span>
<span data-ttu-id="d601e-206">Управлять конвейерами можно с помощью Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="d601e-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="d601e-207">Например, вы можете приостановить и возобновить работу конвейеров, используя командлеты Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d601e-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="d601e-208">Приостановка и возобновление конвейеры Hello представление диаграммы не поддерживает.</span><span class="sxs-lookup"><span data-stu-id="d601e-208">hello diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="d601e-209">Если вы хотите toouse пользовательский интерфейс, используйте hello отслеживания и управления ими приложения.</span><span class="sxs-lookup"><span data-stu-id="d601e-209">If you want toouse an user interface, use hello monitoring and managing application.</span></span> <span data-ttu-id="d601e-210">Дополнительные сведения об использовании приложения hello см. в разделе [мониторинг и управление ими конвейеров фабрики данных с помощью приложения hello мониторинг и управление](data-factory-monitor-manage-app.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="d601e-210">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="d601e-211">Можно приостановить или приостановить конвейеров с помощью hello **Suspend AzureRmDataFactoryPipeline** командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d601e-211">You can pause/suspend pipelines by using hello **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="d601e-212">Этот командлет полезен, если вы не хотите toorun конвейеры до исправления проблемы.</span><span class="sxs-lookup"><span data-stu-id="d601e-212">This cmdlet is useful when you don’t want toorun your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="d601e-213">Например:</span><span class="sxs-lookup"><span data-stu-id="d601e-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="d601e-214">После устранения проблемы hello с конвейером hello hello приостановки конвейера можно возобновить, запустив следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="d601e-214">After hello issue has been fixed with hello pipeline, you can resume hello suspended pipeline by running hello following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="d601e-215">Например:</span><span class="sxs-lookup"><span data-stu-id="d601e-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="d601e-216">Отладка конвейеров</span><span class="sxs-lookup"><span data-stu-id="d601e-216">Debug pipelines</span></span>
<span data-ttu-id="d601e-217">Фабрика данных Azure предоставляет богатые возможности для вас toodebug и устранение неполадок конвейеров с помощью hello портал Azure и Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d601e-217">Azure Data Factory provides rich capabilities for you toodebug and troubleshoot pipelines by using hello Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="d601e-218">[! Обратите внимание}, что это намного проще tootroubleshot, hello ошибок с помощью мониторинга и приложение для управления.</span><span class="sxs-lookup"><span data-stu-id="d601e-218">[!NOTE} It is much easier tootroubleshot errors using hello Monitoring & Management App.</span></span> <span data-ttu-id="d601e-219">Дополнительные сведения об использовании приложения hello см. в разделе [мониторинг и управление ими конвейеров фабрики данных с помощью приложения hello мониторинг и управление](data-factory-monitor-manage-app.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="d601e-219">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="d601e-220">Поиск ошибок в конвейере</span><span class="sxs-lookup"><span data-stu-id="d601e-220">Find errors in a pipeline</span></span>
<span data-ttu-id="d601e-221">Сбой при выполнении действия hello в конвейере hello набора данных, созданного в конвейере hello находится в состоянии ошибки из-за сбоя hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-221">If hello activity run fails in a pipeline, hello dataset that is produced by hello pipeline is in an error state because of hello failure.</span></span> <span data-ttu-id="d601e-222">Отладка и устранение ошибок в фабрике данных Azure с помощью следующих методов hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-222">You can debug and troubleshoot errors in Azure Data Factory by using hello following methods.</span></span>

#### <a name="use-hello-azure-portal-toodebug-an-error"></a><span data-ttu-id="d601e-223">Использовать hello Azure портала toodebug ошибку</span><span class="sxs-lookup"><span data-stu-id="d601e-223">Use hello Azure portal toodebug an error</span></span>
1. <span data-ttu-id="d601e-224">На hello **таблицы** колонка, щелкните срез hello проблемы с hello **состояние** значение слишком**сбой**.</span><span class="sxs-lookup"><span data-stu-id="d601e-224">On hello **Table** blade, click hello problem slice that has hello **Status** set too**Failed**.</span></span>

   ![Колонка "Таблица" с проблемным срезом](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="d601e-226">На hello **срез данных** колонке нажмите кнопку, сбой при выполнении действия hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-226">On hello **Data slice** blade, click hello activity run that failed.</span></span>

   ![Срез данных с ошибкой](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="d601e-228">На hello **сведения о выполнении действия** колонки, файлы можно загрузить hello, связанные с обработкой HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-228">On hello **Activity run details** blade, you can download hello files that are associated with hello HDInsight processing.</span></span> <span data-ttu-id="d601e-229">Нажмите кнопку **загрузки** для состояния и stderr toodownload hello файл журнала ошибок со сведениями об ошибке hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-229">Click **Download** for Status/stderr toodownload hello error log file that contains details about hello error.</span></span>

   ![Колонка "Сведения о циклах выполнения действия" с ошибкой](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a><span data-ttu-id="d601e-231">Используйте PowerShell toodebug ошибку</span><span class="sxs-lookup"><span data-stu-id="d601e-231">Use PowerShell toodebug an error</span></span>
1. <span data-ttu-id="d601e-232">Запустите **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d601e-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="d601e-233">Запустите hello **Get AzureRmDataFactorySlice** команд toosee hello срезов и их состояния.</span><span class="sxs-lookup"><span data-stu-id="d601e-233">Run hello **Get-AzureRmDataFactorySlice** command toosee hello slices and their statuses.</span></span> <span data-ttu-id="d601e-234">Вы увидите срез с состоянием hello **сбой**.</span><span class="sxs-lookup"><span data-stu-id="d601e-234">You should see a slice with hello status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="d601e-235">Например:</span><span class="sxs-lookup"><span data-stu-id="d601e-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="d601e-236">Замените **StartDateTime** на время запуска конвейера.</span><span class="sxs-lookup"><span data-stu-id="d601e-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="d601e-237">Теперь запустите hello **Get AzureRmDataFactoryRun** запустить командлет tooget сведения о действии hello hello среза.</span><span class="sxs-lookup"><span data-stu-id="d601e-237">Now, run hello **Get-AzureRmDataFactoryRun** cmdlet tooget details about hello activity run for hello slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="d601e-238">Например:</span><span class="sxs-lookup"><span data-stu-id="d601e-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="d601e-239">Hello StartDateTime равен hello время начала среза hello ошибки или проблемы, записанными из предыдущего шага hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-239">hello value of StartDateTime is hello start time for hello error/problem slice that you noted from hello previous step.</span></span> <span data-ttu-id="d601e-240">Hello даты времени должна быть заключена в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="d601e-240">hello date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="d601e-241">Вы должны увидеть результаты с подробными сведениями об ошибке hello, аналогичные toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="d601e-241">You should see output with details about hello error that is similar toohello following:</span></span>

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
5. <span data-ttu-id="d601e-242">Можно запустить hello **сохранить AzureRmDataFactoryLog** со значением идентификатора см. в выходных данных hello и загрузите файлы журналов hello с помощью hello hello **- DownloadLogsoption** для командлета hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-242">You can run hello **Save-AzureRmDataFactoryLog** cmdlet with hello Id value that you see from hello output, and download hello log files by using hello **-DownloadLogsoption** for hello cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="d601e-243">Повторная обработка проблемных срезов в конвейере</span><span class="sxs-lookup"><span data-stu-id="d601e-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d601e-244">Это упрощает tootroubleshoot ошибки и повторного запуска невыполненных фрагментов с помощью hello мониторинг & приложение для управления.</span><span class="sxs-lookup"><span data-stu-id="d601e-244">It's easier tootroubleshoot errors and rerun failed slices by using hello Monitoring & Management App.</span></span> <span data-ttu-id="d601e-245">Дополнительные сведения об использовании приложения hello см. в разделе [мониторинг и управление ими конвейеров фабрики данных с помощью приложения hello мониторинг и управление](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="d601e-245">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-hello-azure-portal"></a><span data-ttu-id="d601e-246">Использовать hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d601e-246">Use hello Azure portal</span></span>
<span data-ttu-id="d601e-247">После устранения неполадок и отладки сбоев в конвейере, можно повторно запустить сбоев путем перехода toohello ошибка среза и щелкнув hello **запуска** кнопки на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating toohello error slice and clicking hello **Run** button on hello command bar.</span></span>

![Повторная обработка среза](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="d601e-249">В случае hello срез не прошло проверку из-за сбоя политики (например, если данные не доступны), можно устранить ошибки hello и еще раз проверьте, выбрав hello **проверки** кнопку на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-249">In case hello slice has failed validation because of a policy failure (for example, if data isn't available), you can fix hello failure and validate again by clicking hello **Validate** button on hello command bar.</span></span>

![Исправление ошибок и проверка](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="d601e-251">Использование Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d601e-251">Use Azure PowerShell</span></span>
<span data-ttu-id="d601e-252">Ошибки можно перезапустить с помощью hello **AzureRmDataFactorySliceStatus набор** командлета.</span><span class="sxs-lookup"><span data-stu-id="d601e-252">You can rerun failures by using hello **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="d601e-253">В разделе hello [AzureRmDataFactorySliceStatus набор](https://msdn.microsoft.com/library/mt603522.aspx) раздел о синтаксисе и другие сведения о командлете hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-253">See hello [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about hello cmdlet.</span></span>

<span data-ttu-id="d601e-254">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d601e-254">**Example:**</span></span>

<span data-ttu-id="d601e-255">Hello следующий пример задает hello состояние всех фрагментов для hello таблицу «DAWikiAggregatedData» too'Waiting "в фабрике данных Azure hello «WikiADF».</span><span class="sxs-lookup"><span data-stu-id="d601e-255">hello following example sets hello status of all slices for hello table 'DAWikiAggregatedData' too'Waiting' in hello Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="d601e-256">Hello «Тип обновления» имеет значение too'UpstreamInPipeline, это означает, что состояния каждого среза для hello таблицы и всех таблиц (вышестоящего) hello для зависимых задаются too'Waiting.</span><span class="sxs-lookup"><span data-stu-id="d601e-256">hello 'UpdateType' is set too'UpstreamInPipeline', which means that statuses of each slice for hello table and all hello dependent (upstream) tables are set too'Waiting'.</span></span> <span data-ttu-id="d601e-257">Hello другие возможные значения для этого параметра — это «Пользователь».</span><span class="sxs-lookup"><span data-stu-id="d601e-257">hello other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="d601e-258">Создание оповещений</span><span class="sxs-lookup"><span data-stu-id="d601e-258">Create alerts</span></span>
<span data-ttu-id="d601e-259">Azure регистрирует пользовательские события, когда ресурс Azure (например, фабрика данных) создается, обновляется или удаляется.</span><span class="sxs-lookup"><span data-stu-id="d601e-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="d601e-260">Вы можете создавать оповещения об этих событиях.</span><span class="sxs-lookup"><span data-stu-id="d601e-260">You can create alerts on these events.</span></span> <span data-ttu-id="d601e-261">Можно использовать различные метрики toocapture фабрики данных и создавать предупреждения для метрики.</span><span class="sxs-lookup"><span data-stu-id="d601e-261">You can use Data Factory toocapture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="d601e-262">Мы советуем использовать события для наблюдения в режиме реального времени, а метрики — для статистических целей.</span><span class="sxs-lookup"><span data-stu-id="d601e-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="d601e-263">Оповещения о событиях</span><span class="sxs-lookup"><span data-stu-id="d601e-263">Alerts on events</span></span>
<span data-ttu-id="d601e-264">События Azure позволяют получить представление о том, что происходит в ресурсах Azure.</span><span class="sxs-lookup"><span data-stu-id="d601e-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="d601e-265">При использовании фабрики данных Azure события создаются, когда:</span><span class="sxs-lookup"><span data-stu-id="d601e-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="d601e-266">фабрика данных создается, обновляется или удаляется;</span><span class="sxs-lookup"><span data-stu-id="d601e-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="d601e-267">запускается или завершается обработка данных (цикл выполнения);</span><span class="sxs-lookup"><span data-stu-id="d601e-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="d601e-268">создается и удаляется кластер HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="d601e-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="d601e-269">Можно создавать предупреждения по этим событиям пользователя и их настройки уведомления toohello toosend электронной почты администратора и coadministrators hello подписки.</span><span class="sxs-lookup"><span data-stu-id="d601e-269">You can create alerts on these user events and configure them toosend email notifications toohello administrator and coadministrators of hello subscription.</span></span> <span data-ttu-id="d601e-270">Кроме того можно указать дополнительных адресов электронной почты пользователей, которым требуются уведомления по электронной почте tooreceive при выполнении условий hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-270">In addition, you can specify additional email addresses of users who need tooreceive email notifications when hello conditions are met.</span></span> <span data-ttu-id="d601e-271">Эта возможность полезна, требуется tooget уведомления об ошибках, если не нужно toocontinuously монитор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="d601e-271">This feature is useful when you want tooget notified on failures and don’t want toocontinuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="d601e-272">В настоящее время портал hello не отображать оповещения о событиях.</span><span class="sxs-lookup"><span data-stu-id="d601e-272">Currently, hello portal doesn't show alerts on events.</span></span> <span data-ttu-id="d601e-273">Используйте hello [управление и мониторинг приложения](data-factory-monitor-manage-app.md) toosee все предупреждения.</span><span class="sxs-lookup"><span data-stu-id="d601e-273">Use hello [Monitoring and Management app](data-factory-monitor-manage-app.md) toosee all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="d601e-274">Задание определения оповещения</span><span class="sxs-lookup"><span data-stu-id="d601e-274">Specify an alert definition</span></span>
<span data-ttu-id="d601e-275">toospecify определение предупреждения, создайте файл JSON, описывающий hello операций, которые вы хотите toobe оповещения на.</span><span class="sxs-lookup"><span data-stu-id="d601e-275">toospecify an alert definition, you create a JSON file that describes hello operations that you want toobe alerted on.</span></span> <span data-ttu-id="d601e-276">В следующем примере hello предупреждение hello отправляет уведомление по электронной почте для hello RunFinished операции.</span><span class="sxs-lookup"><span data-stu-id="d601e-276">In hello following example, hello alert sends an email notification for hello RunFinished operation.</span></span> <span data-ttu-id="d601e-277">toobe конкретного уведомления по электронной почте отправляется после завершения выполнения в фабрике данных hello и произошел сбой запуска hello (состояние = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="d601e-277">toobe specific, an email notification is sent when a run in hello data factory has completed and hello run has failed (Status = FailedExecution).</span></span>

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
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
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

<span data-ttu-id="d601e-278">Можно удалить **подсостояния** из определения JSON, если вы не хотите toobe оповещения на конкретный сбой hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-278">You can remove **subStatus** from hello JSON definition if you don’t want toobe alerted on a specific failure.</span></span>

<span data-ttu-id="d601e-279">Этот пример устанавливает hello предупреждения для всех фабрик данных в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="d601e-279">This example sets up hello alert for all data factories in your subscription.</span></span> <span data-ttu-id="d601e-280">Если требуется, чтобы предупреждения toobe hello для фабрики данных, можно указать фабрики данных **resourceUri** в hello **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="d601e-280">If you want hello alert toobe set up for a particular data factory, you can specify data factory **resourceUri** in hello **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="d601e-281">Hello следующей таблице приведен список hello доступные операции и состояния (и Дополнительные сведения).</span><span class="sxs-lookup"><span data-stu-id="d601e-281">hello following table provides hello list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="d601e-282">Имя операции</span><span class="sxs-lookup"><span data-stu-id="d601e-282">Operation name</span></span> | <span data-ttu-id="d601e-283">Состояние</span><span class="sxs-lookup"><span data-stu-id="d601e-283">Status</span></span> | <span data-ttu-id="d601e-284">Подсостояние</span><span class="sxs-lookup"><span data-stu-id="d601e-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d601e-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="d601e-285">RunStarted</span></span> |<span data-ttu-id="d601e-286">Started</span><span class="sxs-lookup"><span data-stu-id="d601e-286">Started</span></span> |<span data-ttu-id="d601e-287">Starting</span><span class="sxs-lookup"><span data-stu-id="d601e-287">Starting</span></span> |
| <span data-ttu-id="d601e-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="d601e-288">RunFinished</span></span> |<span data-ttu-id="d601e-289">Failed / Succeeded</span><span class="sxs-lookup"><span data-stu-id="d601e-289">Failed / Succeeded</span></span> |<span data-ttu-id="d601e-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="d601e-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="d601e-291">Succeeded</span><span class="sxs-lookup"><span data-stu-id="d601e-291">Succeeded</span></span><br/><br/><span data-ttu-id="d601e-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="d601e-292">FailedExecution</span></span><br/><br/><span data-ttu-id="d601e-293">TimedOut</span><span class="sxs-lookup"><span data-stu-id="d601e-293">TimedOut</span></span><br/><br/><span data-ttu-id="d601e-294"><Canceled</span><span class="sxs-lookup"><span data-stu-id="d601e-294"><Canceled</span></span><br/><br/><span data-ttu-id="d601e-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="d601e-295">FailedValidation</span></span><br/><br/><span data-ttu-id="d601e-296">Abandoned</span><span class="sxs-lookup"><span data-stu-id="d601e-296">Abandoned</span></span> |
| <span data-ttu-id="d601e-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="d601e-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="d601e-298">Started</span><span class="sxs-lookup"><span data-stu-id="d601e-298">Started</span></span> | |
| <span data-ttu-id="d601e-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="d601e-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="d601e-300">Успешно</span><span class="sxs-lookup"><span data-stu-id="d601e-300">Succeeded</span></span> | |
| <span data-ttu-id="d601e-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="d601e-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="d601e-302">Успешно</span><span class="sxs-lookup"><span data-stu-id="d601e-302">Succeeded</span></span> | |

<span data-ttu-id="d601e-303">В разделе [создания правила оповещения](https://msdn.microsoft.com/library/azure/dn510366.aspx) подробные сведения об элементах hello JSON, которые используются в примере hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about hello JSON elements that are used in hello example.</span></span>

#### <a name="deploy-hello-alert"></a><span data-ttu-id="d601e-304">Развертывание предупреждение hello</span><span class="sxs-lookup"><span data-stu-id="d601e-304">Deploy hello alert</span></span>
<span data-ttu-id="d601e-305">Предупреждение toodeploy hello, используйте командлет Azure PowerShell hello **New AzureRmResourceGroupDeployment**, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="d601e-305">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="d601e-306">После успешного завершения развертывания группы ресурсов hello отображаются hello следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="d601e-306">After hello resource group deployment has finished successfully, you see hello following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
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
> <span data-ttu-id="d601e-307">Можно использовать hello [создать правило оповещения о](https://msdn.microsoft.com/library/azure/dn510366.aspx) toocreate API-интерфейса REST правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="d601e-307">You can use hello [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate an alert rule.</span></span> <span data-ttu-id="d601e-308">полезные данные JSON Hello — аналогичный пример toohello JSON.</span><span class="sxs-lookup"><span data-stu-id="d601e-308">hello JSON payload is similar toohello JSON example.</span></span>  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a><span data-ttu-id="d601e-309">Получить список hello развертывания группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="d601e-309">Retrieve hello list of Azure resource group deployments</span></span>
<span data-ttu-id="d601e-310">Список hello tooretrieve развернутого развертывания группы ресурсов Azure, с помощью командлета hello **Get AzureRmResourceGroupDeployment**, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="d601e-310">tooretrieve hello list of deployed Azure resource group deployments, use hello cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

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

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="d601e-311">Устранение неполадок пользовательских событий</span><span class="sxs-lookup"><span data-stu-id="d601e-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="d601e-312">Вы можете просмотреть все события hello, созданные после нажатия кнопки hello **метрики и операций** плитки.</span><span class="sxs-lookup"><span data-stu-id="d601e-312">You can see all hello events that are generated after clicking hello **Metrics and operations** tile.</span></span>

    ![Элемент "Метрики и операции"](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="d601e-314">Нажмите кнопку hello **события** плитки toosee hello события.</span><span class="sxs-lookup"><span data-stu-id="d601e-314">Click hello **Events** tile toosee hello events.</span></span>

    ![Плитки "События"](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="d601e-316">На hello **события** колонки, чтобы просмотреть сведения о событиях, отфильтрованных событий и т. д.</span><span class="sxs-lookup"><span data-stu-id="d601e-316">On hello **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Колонка "События"](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="d601e-318">Нажмите кнопку **операции** списка операций hello, приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="d601e-318">Click an **Operation** in hello operations list that causes an error.</span></span>

    ![Выберите операцию](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="d601e-320">Нажмите кнопку **ошибка** событие toosee сведения об ошибке hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-320">Click an **Error** event toosee details about hello error.</span></span>

    ![Ошибка события](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="d601e-322">В разделе [анализ Azure командлеты](https://msdn.microsoft.com/library/mt282452.aspx) для командлетов PowerShell, которые можно использовать tooadd, получения и удаления оповещения.</span><span class="sxs-lookup"><span data-stu-id="d601e-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use tooadd, get, or remove alerts.</span></span> <span data-ttu-id="d601e-323">Вот несколько примеров использования hello **Get AlertRule** командлета:</span><span class="sxs-lookup"><span data-stu-id="d601e-323">Here are a few examples of using hello **Get-AlertRule** cmdlet:</span></span>

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
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
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

<span data-ttu-id="d601e-324">Выполните следующие команды get-help toosee-подробные сведения и примеры для командлета Get-AlertRule hello hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-324">Run hello following get-help commands toosee details and examples for hello Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="d601e-325">Если на события создания оповещений hello hello портала колонки, но не получать уведомления по электронной почте, проверить, установлен ли указанный адрес электронной почты hello tooreceive сообщений электронной почты от внешних отправителей.</span><span class="sxs-lookup"><span data-stu-id="d601e-325">If you see hello alert generation events on hello portal blade but you don't receive email notifications, check whether hello email address that is specified is set tooreceive emails from external senders.</span></span> <span data-ttu-id="d601e-326">предупреждения Hello сообщения электронной почты может были заблокированы параметры электронной почты.</span><span class="sxs-lookup"><span data-stu-id="d601e-326">hello alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="d601e-327">Оповещения по метрикам</span><span class="sxs-lookup"><span data-stu-id="d601e-327">Alerts on metrics</span></span>
<span data-ttu-id="d601e-328">Фабрика данных позволяет собирать различные метрики и создавать по ним оповещения.</span><span class="sxs-lookup"><span data-stu-id="d601e-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="d601e-329">Можно отслеживать и создавать предупреждения для следующих метрик для hello срезов в вашей фабрике данных hello:</span><span class="sxs-lookup"><span data-stu-id="d601e-329">You can monitor and create alerts on hello following metrics for hello slices in your data factory:</span></span>

* <span data-ttu-id="d601e-330">**циклы выполнения со сбоем**;</span><span class="sxs-lookup"><span data-stu-id="d601e-330">**Failed Runs**</span></span>
* <span data-ttu-id="d601e-331">**успешные циклы выполнения**.</span><span class="sxs-lookup"><span data-stu-id="d601e-331">**Successful Runs**</span></span>

<span data-ttu-id="d601e-332">Эти показатели полезны и помочь tooget запуска Обзор в целом, так и неуспешные в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-332">These metrics are useful and help you tooget an overview of overall failed and successful runs in hello data factory.</span></span> <span data-ttu-id="d601e-333">Метрики создаются при каждом цикле выполнения действия со срезом.</span><span class="sxs-lookup"><span data-stu-id="d601e-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="d601e-334">В начале hello hello час, эти показатели объединяются и помещается tooyour учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d601e-334">At hello beginning of hello hour, these metrics are aggregated and pushed tooyour storage account.</span></span> <span data-ttu-id="d601e-335">метрики tooenable Настройка учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d601e-335">tooenable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="d601e-336">Включить метрики</span><span class="sxs-lookup"><span data-stu-id="d601e-336">Enable metrics</span></span>
<span data-ttu-id="d601e-337">tooenable метрик, щелкните следующую команду hello hello **фабрики данных** колонки:</span><span class="sxs-lookup"><span data-stu-id="d601e-337">tooenable metrics, click hello following from hello **Data Factory** blade:</span></span>

<span data-ttu-id="d601e-338">**Мониторинг** > **Метрика** > **Параметры диагностики** > **Диагностика**</span><span class="sxs-lookup"><span data-stu-id="d601e-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Ссылка диагностики](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="d601e-340">На hello **диагностики** колонка, щелкните **на**, выберите учетную запись хранения hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d601e-340">On hello **Diagnostics** blade, click **On**, select hello storage account, and click **Save**.</span></span>

![Выноска "Диагностика"](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="d601e-342">Он может занять час tooone для hello метрики toobe отображается на hello **мониторинг** колонки так как статистических показателей происходит каждый час.</span><span class="sxs-lookup"><span data-stu-id="d601e-342">It might take up tooone hour for hello metrics toobe visible on hello **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="d601e-343">Настройка оповещений по метрикам</span><span class="sxs-lookup"><span data-stu-id="d601e-343">Set up an alert on metrics</span></span>
<span data-ttu-id="d601e-344">Нажмите кнопку hello **фабрики данных метрик** плитки:</span><span class="sxs-lookup"><span data-stu-id="d601e-344">Click hello **Data Factory metrics** tile:</span></span>

![Элемент "Метрики фабрики данных"](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="d601e-346">На hello **метрика** колонка, щелкните **+ добавить оповещение** на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-346">On hello **Metric** blade, click **+ Add alert** on hello toolbar.</span></span>
<span data-ttu-id="d601e-347">![Колонка "Метрики фабрики данных", добавление оповещения](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="d601e-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="d601e-348">На hello **Добавление правила оповещения** , hello, выполнив действия и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d601e-348">On hello **Add an alert rule** page, do hello following steps, and click **OK**.</span></span>

* <span data-ttu-id="d601e-349">Введите имя для оповещения hello (пример: «предупреждение о сбое»).</span><span class="sxs-lookup"><span data-stu-id="d601e-349">Enter a name for hello alert (example: "failed alert").</span></span>
* <span data-ttu-id="d601e-350">Введите описание для предупреждения hello (пример: «отправить сообщение электронной почты, когда происходит сбой»).</span><span class="sxs-lookup"><span data-stu-id="d601e-350">Enter a description for hello alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="d601e-351">Выберите метрику (неудачные и успешные выполнения).</span><span class="sxs-lookup"><span data-stu-id="d601e-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="d601e-352">Укажите условие и пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="d601e-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="d601e-353">Укажите период времени hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-353">Specify hello period of time.</span></span>
* <span data-ttu-id="d601e-354">Укажите, следует ли отправлять сообщение электронной почты, tooowners, участники и читатели.</span><span class="sxs-lookup"><span data-stu-id="d601e-354">Specify whether an email should be sent tooowners, contributors, and readers.</span></span>

![Колонка "Метрики фабрики данных", добавление правила оповещения](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="d601e-356">После успешно добавлено правило генерации оповещений hello, закрывает колонке hello и вы увидите новое предупреждение hello в hello **метрика** колонку.</span><span class="sxs-lookup"><span data-stu-id="d601e-356">After hello alert rule is added successfully, hello blade closes and you see hello new alert on hello **Metric** blade.</span></span>

![Колонка "Метрики фабрики данных", добавление нового оповещения](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="d601e-358">Вы также увидите hello число оповещений за hello **предупреждения правила** плитки.</span><span class="sxs-lookup"><span data-stu-id="d601e-358">You should also see hello number of alerts in hello **Alert rules** tile.</span></span> <span data-ttu-id="d601e-359">Нажмите кнопку hello **предупреждения правила** плитки.</span><span class="sxs-lookup"><span data-stu-id="d601e-359">Click hello **Alert rules** tile.</span></span>

![Колонка "Метрики фабрики данных", правила оповещения](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="d601e-361">На hello **правила оповещения** колонку, вы видите все имеющиеся оповещения.</span><span class="sxs-lookup"><span data-stu-id="d601e-361">On hello **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="d601e-362">tooadd оповещения, щелкните **добавить оповещение** на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-362">tooadd an alert, click **Add alert** on hello toolbar.</span></span>

![Колонка "Правила оповещения"](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="d601e-364">Оповещения</span><span class="sxs-lookup"><span data-stu-id="d601e-364">Alert notifications</span></span>
<span data-ttu-id="d601e-365">После правила оповещения hello соответствует условию hello, вы должны получить сообщение электронной почты о том, что активации предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="d601e-365">After hello alert rule matches hello condition, you should get an email that says hello alert is activated.</span></span> <span data-ttu-id="d601e-366">После устранения проблемы hello и больше не соответствует hello условие оповещения, вы получаете электронное сообщение о том, что предупреждение hello разрешается.</span><span class="sxs-lookup"><span data-stu-id="d601e-366">After hello issue is resolved and hello alert condition doesn’t match anymore, you get an email that says hello alert is resolved.</span></span>

<span data-ttu-id="d601e-367">Такое поведение отличается от ситуации, когда уведомление отправляется по каждому сбою, соответствующему правилу оповещения.</span><span class="sxs-lookup"><span data-stu-id="d601e-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="d601e-368">Развертывание оповещений с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d601e-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="d601e-369">Вы можете развернуть предупреждения для метрики hello таким же образом, как для событий.</span><span class="sxs-lookup"><span data-stu-id="d601e-369">You can deploy alerts for metrics hello same way that you do for events.</span></span>

<span data-ttu-id="d601e-370">**Определение оповещения**</span><span class="sxs-lookup"><span data-stu-id="d601e-370">**Alert definition**</span></span>

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

<span data-ttu-id="d601e-371">Замените *subscriptionId*, *resourceGroupName*, и *с именем dataFactoryName* в образце hello с соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="d601e-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in hello sample with appropriate values.</span></span>

<span data-ttu-id="d601e-372">*metricName* на данный момент поддерживает два значения:</span><span class="sxs-lookup"><span data-stu-id="d601e-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="d601e-373">FailedRuns и</span><span class="sxs-lookup"><span data-stu-id="d601e-373">FailedRuns</span></span>
* <span data-ttu-id="d601e-374">SuccessfulRuns.</span><span class="sxs-lookup"><span data-stu-id="d601e-374">SuccessfulRuns</span></span>

<span data-ttu-id="d601e-375">**Развертывание предупреждение hello**</span><span class="sxs-lookup"><span data-stu-id="d601e-375">**Deploy hello alert**</span></span>

<span data-ttu-id="d601e-376">Предупреждение toodeploy hello, используйте командлет Azure PowerShell hello **New AzureRmResourceGroupDeployment**, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="d601e-376">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="d601e-377">В случае успешного развертывания вы увидите следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="d601e-377">You should see following message after a successful deployment:</span></span>

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

<span data-ttu-id="d601e-378">Можно также использовать hello **AlertRule добавить** toodeploy командлет правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="d601e-378">You can also use hello **Add-AlertRule** cmdlet toodeploy an alert rule.</span></span> <span data-ttu-id="d601e-379">В разделе hello [AlertRule добавить](https://msdn.microsoft.com/library/mt282468.aspx) разделе Дополнительные сведения и примеры.</span><span class="sxs-lookup"><span data-stu-id="d601e-379">See hello [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a><span data-ttu-id="d601e-380">Перемещение данных фабрики tooa другой группе ресурсов или подписки</span><span class="sxs-lookup"><span data-stu-id="d601e-380">Move a data factory tooa different resource group or subscription</span></span>
<span data-ttu-id="d601e-381">Можно переместить данные фабрики tooa другой группе ресурсов или другую подписку с помощью hello **переместить** командной строке кнопки на главной странице hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="d601e-381">You can move a data factory tooa different resource group or a different subscription by using hello **Move** command bar button on hello home page of your data factory.</span></span>

![Перемещение фабрики данных](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="d601e-383">Также можно перемещать все связанные ресурсы (такие как предупреждения, связанные с фабрикой данных hello), вместе с hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="d601e-383">You can also move any related resources (such as alerts that are associated with hello data factory), along with hello data factory.</span></span>

![Диалоговое окно "Перемещение ресурсов"](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
