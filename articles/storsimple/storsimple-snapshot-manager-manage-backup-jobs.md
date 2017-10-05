---
title: "Задания архивации StorSimple Snapshot Manager | Документация Майкрософт"
description: "Узнайте, как использовать оснастку консоли MMC \"Диспетчер моментальных снимков StorSimple\" для просмотра запланированных, выполняющихся и завершенных заданий архивации, а также управления ими."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 03e306b62250f2bb033cc14e856a59760b5406c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-backup-jobs"></a><span data-ttu-id="a7d85-103">Просмотр заданий архивации и управление ими с помощью диспетчера моментальных снимков StorSimple</span><span class="sxs-lookup"><span data-stu-id="a7d85-103">Use StorSimple Snapshot Manager to view and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="a7d85-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a7d85-104">Overview</span></span>
<span data-ttu-id="a7d85-105">В узле **Задания** на панели **Область** отображаются отсортированные по категориям (**Запланированные**, **За последние 24 часа** и **Выполняются**) задачи архивации, которые вы инициировали в интерактивном режиме или с помощью настроенной политики.</span><span class="sxs-lookup"><span data-stu-id="a7d85-105">The **Jobs** node in the **Scope** pane shows the **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="a7d85-106">В этом учебнике объясняется, как с помощью узла **Задания** отобразить сведения о запланированных, последних и выполняющихся заданиях архивации.</span><span class="sxs-lookup"><span data-stu-id="a7d85-106">This tutorial explains how you can use the **Jobs** node to display information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="a7d85-107">(Список заданий и соответствующие сведения о них отображаются на панели **Результаты**). Кроме того, вы можете щелкнуть правой кнопкой мыши задание в списке и просмотреть контекстное меню, в котором перечисляются доступные действия.</span><span class="sxs-lookup"><span data-stu-id="a7d85-107">(The list of jobs and corresponding information appears in the **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="a7d85-108">Просмотр запланированных заданий</span><span class="sxs-lookup"><span data-stu-id="a7d85-108">View scheduled jobs</span></span>
<span data-ttu-id="a7d85-109">Чтобы просмотреть запланированные задания резервного копирования, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="a7d85-109">Use the following procedure to view scheduled backup jobs.</span></span>

#### <a name="to-view-scheduled-jobs"></a><span data-ttu-id="a7d85-110">Просмотр запланированных заданий</span><span class="sxs-lookup"><span data-stu-id="a7d85-110">To view scheduled jobs</span></span>
1. <span data-ttu-id="a7d85-111">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a7d85-111">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="a7d85-112">На панели **Область** разверните узел **Задания** и щелкните **Запланированные**.</span><span class="sxs-lookup"><span data-stu-id="a7d85-112">In the **Scope** pane, expand the **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="a7d85-113">На панели **Результаты** отобразятся следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="a7d85-113">The following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="a7d85-114">**Имя** : имя запланированного моментального снимка</span><span class="sxs-lookup"><span data-stu-id="a7d85-114">**Name** – the name of the scheduled snapshot</span></span>
   * <span data-ttu-id="a7d85-115">**Следующее выполнение** : дата и время следующего запланированного моментального снимка</span><span class="sxs-lookup"><span data-stu-id="a7d85-115">**Next Run** – the date and time of the next scheduled snapshot</span></span>
   * <span data-ttu-id="a7d85-116">**Последнее выполнение** : дата и время последнего запланированного моментального снимка</span><span class="sxs-lookup"><span data-stu-id="a7d85-116">**Last Run** – the date and time of the most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="a7d85-117">Если моментальный снимок создается только один раз, то значения параметров **Следующее выполнение** и **Последнее выполнение** будут совпадать.</span><span class="sxs-lookup"><span data-stu-id="a7d85-117">For one-time only snapshots, the **Next Run** and **Last Run** will be the same.</span></span>
     
     ![Запланированные задания архивации](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="a7d85-119">Чтобы выполнить дополнительные действия для конкретного задания, щелкните правой кнопкой мыши имя задания на панели **Результаты** и выберите необходимые параметры меню.</span><span class="sxs-lookup"><span data-stu-id="a7d85-119">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="a7d85-120">Просмотр последних заданий</span><span class="sxs-lookup"><span data-stu-id="a7d85-120">View recent jobs</span></span>
<span data-ttu-id="a7d85-121">Выполните указанные ниже действия, чтобы просмотреть задания резервного копирования и восстановления, завершенные за последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="a7d85-121">Use the following procedure to view backup and restore jobs that were completed in the last 24 hours.</span></span>

#### <a name="to-view-recent-jobs"></a><span data-ttu-id="a7d85-122">Просмотр последних заданий</span><span class="sxs-lookup"><span data-stu-id="a7d85-122">To view recent jobs</span></span>
1. <span data-ttu-id="a7d85-123">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a7d85-123">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a7d85-124">На панели **Область** разверните узел **Задания** и щелкните **За последние 24 часа**.</span><span class="sxs-lookup"><span data-stu-id="a7d85-124">In the **Scope** pane, expand the **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="a7d85-125">На панели **Результаты** отобразятся задания архивации за последние 24 часа (не более 64 заданий).</span><span class="sxs-lookup"><span data-stu-id="a7d85-125">The **Results** pane shows backup jobs for the last 24 hours (to a maximum of 64 jobs).</span></span> <span data-ttu-id="a7d85-126">В зависимости от параметров, указанных в меню **Вид**, на панели **Результаты** отобразятся указанные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="a7d85-126">The following information appears in the **Results** pane, depending on the **View** options you specify:</span></span>
   
   * <span data-ttu-id="a7d85-127">**Имя** : имя запланированного моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="a7d85-127">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="a7d85-128">**Запущено** : дата и время начала создания моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="a7d85-128">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="a7d85-129">**Остановлено** : дата и время, когда создание моментального снимка было завершено или прервано.</span><span class="sxs-lookup"><span data-stu-id="a7d85-129">**Stopped** – the date and time when the snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="a7d85-130">**Прошло**: промежуток времени между значениями параметров **Запущено** и **Остановлено**.</span><span class="sxs-lookup"><span data-stu-id="a7d85-130">**Elapsed** – the amount of time between the **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="a7d85-131">**Состояние** : состояние недавно выполненного задания.</span><span class="sxs-lookup"><span data-stu-id="a7d85-131">**Status** – the state of the recently completed job.</span></span> <span data-ttu-id="a7d85-132">**Успешно** : резервная копия создана.</span><span class="sxs-lookup"><span data-stu-id="a7d85-132">**Success** indicates that the backup was created successfully.</span></span> <span data-ttu-id="a7d85-133">**Сбой** : задание не выполнено.</span><span class="sxs-lookup"><span data-stu-id="a7d85-133">**Failed** indicates that the job did not run successfully.</span></span>
   * <span data-ttu-id="a7d85-134">**Сведения** : причина сбоя.</span><span class="sxs-lookup"><span data-stu-id="a7d85-134">**Information** – the reason for the failure.</span></span>
   * <span data-ttu-id="a7d85-135">**Обработано байт (МБ)** : объем обработанных данных группы томов (в мегабайтах).</span><span class="sxs-lookup"><span data-stu-id="a7d85-135">**Bytes processed (MB)** – the amount of data from the volume group that was processed (in MBs).</span></span> 
     
     ![Задания, которые выполнялись за последние 24 часа](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="a7d85-137">Чтобы выполнить дополнительные действия для конкретного задания, щелкните правой кнопкой мыши имя задания на панели **Результаты** и выберите необходимые параметры меню.</span><span class="sxs-lookup"><span data-stu-id="a7d85-137">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>
   
    ![Удаление задания](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="a7d85-139">Просмотр выполняющихся заданий</span><span class="sxs-lookup"><span data-stu-id="a7d85-139">View currently running jobs</span></span>
<span data-ttu-id="a7d85-140">Выполните указанные ниже действия, чтобы просмотреть выполняющиеся задания.</span><span class="sxs-lookup"><span data-stu-id="a7d85-140">Use the following procedure to view jobs that are currently running.</span></span>

#### <a name="to-view-currently-running-jobs"></a><span data-ttu-id="a7d85-141">Просмотр текущих заданий</span><span class="sxs-lookup"><span data-stu-id="a7d85-141">To view currently running jobs</span></span>
1. <span data-ttu-id="a7d85-142">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a7d85-142">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a7d85-143">На панели **Область** разверните узел **Задания** и щелкните **Выполняются**.</span><span class="sxs-lookup"><span data-stu-id="a7d85-143">In the **Scope** pane, expand the **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="a7d85-144">В зависимости от параметров, указанных в меню **Вид**, на панели **Результаты** отобразятся указанные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="a7d85-144">Depending on the **View** options you specify, the following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="a7d85-145">**Имя** : имя запланированного моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="a7d85-145">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="a7d85-146">**Запущено** : дата и время начала создания моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="a7d85-146">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="a7d85-147">**Контрольная точка** : текущее действие по архивации.</span><span class="sxs-lookup"><span data-stu-id="a7d85-147">**Checkpoint** – the current action of the backup.</span></span>
   * <span data-ttu-id="a7d85-148">**Состояние** : процент выполнения.</span><span class="sxs-lookup"><span data-stu-id="a7d85-148">**Status** – the percentage of completion.</span></span>
   * <span data-ttu-id="a7d85-149">**Прошло** : время после начала архивации.</span><span class="sxs-lookup"><span data-stu-id="a7d85-149">**Elapsed** – the amount of time that has passed since the backup began.</span></span> 
   * <span data-ttu-id="a7d85-150">**Средняя пропускная способность (МБ)** — отношение общего числа байтов обработанных данных и общего времени, необходимого для обработки (в МБ).</span><span class="sxs-lookup"><span data-stu-id="a7d85-150">**Average throughput (MB)** – ratio of total bytes of data processed to that of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="a7d85-151">**Обработано байтов (МБ)** — общее число байтов обработанных данных (в МБ).</span><span class="sxs-lookup"><span data-stu-id="a7d85-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="a7d85-152">**Записано байтов (МБ)** — общее число байтов записанных данных (в МБ).</span><span class="sxs-lookup"><span data-stu-id="a7d85-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="a7d85-153">Сюда входят как данные, так и метаданные, поэтому это значение обычно больше, чем значение "Обработано байтов".</span><span class="sxs-lookup"><span data-stu-id="a7d85-153">It includes the data as well as the metadata and hence is typically greater than the Bytes Processed.</span></span>
     
     ![Выполняющиеся задания](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="a7d85-155">Чтобы выполнить дополнительные действия для конкретного задания, щелкните правой кнопкой мыши имя задания на панели **Результаты** и выберите необходимые параметры меню.</span><span class="sxs-lookup"><span data-stu-id="a7d85-155">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7d85-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7d85-156">Next steps</span></span>
* <span data-ttu-id="a7d85-157">Узнайте об [использовании диспетчера моментальных снимков StorSimple для администрирования решения StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="a7d85-157">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="a7d85-158">Узнайте об [использовании диспетчера моментальных снимков StorSimple для управления каталогом резервных копий](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="a7d85-158">Learn how to [use StorSimple Snapshot Manager to manage the backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

