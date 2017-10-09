---
title: "задания резервного копирования диспетчера моментальных снимков aaaStorSimple | Документы Microsoft"
description: "Описывается порядок toouse hello tooview оснастку консоли MMC диспетчера моментальных снимков StorSimple и управлять запланированных, выполняющихся и завершенных заданий резервного копирования."
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
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a><span data-ttu-id="2fc75-103">Использование диспетчера моментальных снимков StorSimple tooview и управление ими заданий резервного копирования</span><span class="sxs-lookup"><span data-stu-id="2fc75-103">Use StorSimple Snapshot Manager tooview and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="2fc75-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2fc75-104">Overview</span></span>
<span data-ttu-id="2fc75-105">Hello **заданий** узел в hello **область** панель отображает hello **запланированное**, **последние 24 часа**, и **под управлением**задачи резервного копирования, инициированные интерактивно или в соответствии с настроенной политикой.</span><span class="sxs-lookup"><span data-stu-id="2fc75-105">hello **Jobs** node in hello **Scope** pane shows hello **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="2fc75-106">В этом учебнике описано, как можно использовать hello **заданий** узел toodisplay сведения о запланированных, недавно и выполняющихся заданий резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="2fc75-106">This tutorial explains how you can use hello **Jobs** node toodisplay information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="2fc75-107">(в hello появится список заданий и соответствующие сведения о hello **результатов** области.) Кроме того, вы можете щелкнуть правой кнопкой мыши задание в списке и просмотреть контекстное меню, в котором перечисляются доступные действия.</span><span class="sxs-lookup"><span data-stu-id="2fc75-107">(hello list of jobs and corresponding information appears in hello **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="2fc75-108">Просмотр запланированных заданий</span><span class="sxs-lookup"><span data-stu-id="2fc75-108">View scheduled jobs</span></span>
<span data-ttu-id="2fc75-109">Следующая процедура tooview hello используйте запланированные задания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="2fc75-109">Use hello following procedure tooview scheduled backup jobs.</span></span>

#### <a name="tooview-scheduled-jobs"></a><span data-ttu-id="2fc75-110">tooview запланированных заданий</span><span class="sxs-lookup"><span data-stu-id="2fc75-110">tooview scheduled jobs</span></span>
1. <span data-ttu-id="2fc75-111">Щелкните значок рабочего стола hello toostart диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2fc75-111">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="2fc75-112">В hello **область** области, разверните hello **заданий** и щелкните **запланированное**.</span><span class="sxs-lookup"><span data-stu-id="2fc75-112">In hello **Scope** pane, expand hello **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="2fc75-113">Hello следующая информация появится на hello **результатов** панели:</span><span class="sxs-lookup"><span data-stu-id="2fc75-113">hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="2fc75-114">**Имя** — hello имя запланированного моментального снимка hello</span><span class="sxs-lookup"><span data-stu-id="2fc75-114">**Name** – hello name of hello scheduled snapshot</span></span>
   * <span data-ttu-id="2fc75-115">**Далее выполните** — hello Дата и время следующего запланированного моментального снимка hello</span><span class="sxs-lookup"><span data-stu-id="2fc75-115">**Next Run** – hello date and time of hello next scheduled snapshot</span></span>
   * <span data-ttu-id="2fc75-116">**Последний запуск** — hello Дата и время последнего запланированного моментального снимка hello</span><span class="sxs-lookup"><span data-stu-id="2fc75-116">**Last Run** – hello date and time of hello most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="2fc75-117">Единовременных моментальных снимков, hello **следующего запуска** и **последний запуск** будет таким же hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-117">For one-time only snapshots, hello **Next Run** and **Last Run** will be hello same.</span></span>
     
     ![Запланированные задания архивации](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="2fc75-119">tooperform дополнительные действия для конкретного задания, щелкните правой кнопкой мыши имя задания hello в hello **результатов** и выберите из меню параметров hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-119">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="2fc75-120">Просмотр последних заданий</span><span class="sxs-lookup"><span data-stu-id="2fc75-120">View recent jobs</span></span>
<span data-ttu-id="2fc75-121">Используйте следующие процедуры архивации tooview hello и восстановления соответствующие задания, которые были выполнены в hello последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="2fc75-121">Use hello following procedure tooview backup and restore jobs that were completed in hello last 24 hours.</span></span>

#### <a name="tooview-recent-jobs"></a><span data-ttu-id="2fc75-122">tooview последних заданий</span><span class="sxs-lookup"><span data-stu-id="2fc75-122">tooview recent jobs</span></span>
1. <span data-ttu-id="2fc75-123">Щелкните значок рабочего стола hello toostart диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2fc75-123">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="2fc75-124">В hello **область** области, разверните hello **заданий** и щелкните **последние 24 часа**.</span><span class="sxs-lookup"><span data-stu-id="2fc75-124">In hello **Scope** pane, expand hello **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="2fc75-125">Hello **результатов** панели показаны задания резервного копирования для hello последние 24 часа (максимум 64 задания tooa).</span><span class="sxs-lookup"><span data-stu-id="2fc75-125">hello **Results** pane shows backup jobs for hello last 24 hours (tooa maximum of 64 jobs).</span></span> <span data-ttu-id="2fc75-126">Hello следующая информация появится на hello **результатов** области, в зависимости от hello **представление** указанных параметров:</span><span class="sxs-lookup"><span data-stu-id="2fc75-126">hello following information appears in hello **Results** pane, depending on hello **View** options you specify:</span></span>
   
   * <span data-ttu-id="2fc75-127">**Имя** — hello имя запланированного моментального снимка hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-127">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="2fc75-128">**Запущен** — hello Дата и время начала создания снимка hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-128">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="2fc75-129">**Остановить** — hello дату и время при hello моментального снимка завершено или прервано.</span><span class="sxs-lookup"><span data-stu-id="2fc75-129">**Stopped** – hello date and time when hello snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="2fc75-130">**Затраченное** — hello промежуток времени между hello **Started** и **остановлена** раз.</span><span class="sxs-lookup"><span data-stu-id="2fc75-130">**Elapsed** – hello amount of time between hello **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="2fc75-131">**Состояние** — hello состояния hello Недавно завершенные задания.</span><span class="sxs-lookup"><span data-stu-id="2fc75-131">**Status** – hello state of hello recently completed job.</span></span> <span data-ttu-id="2fc75-132">**Успех** успешном создании резервной копии hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-132">**Success** indicates that hello backup was created successfully.</span></span> <span data-ttu-id="2fc75-133">**Не удалось выполнить** означает задания hello не был выполнен успешно.</span><span class="sxs-lookup"><span data-stu-id="2fc75-133">**Failed** indicates that hello job did not run successfully.</span></span>
   * <span data-ttu-id="2fc75-134">**Сведения о** — hello причину сбоя hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-134">**Information** – hello reason for hello failure.</span></span>
   * <span data-ttu-id="2fc75-135">**Обработано байт (МБ)** — hello объема данных из группы томов hello, который был обработан (в МБ).</span><span class="sxs-lookup"><span data-stu-id="2fc75-135">**Bytes processed (MB)** – hello amount of data from hello volume group that was processed (in MBs).</span></span> 
     
     ![Задания, которые выполнялись в hello последние 24 часа](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="2fc75-137">tooperform дополнительные действия для конкретного задания, щелкните правой кнопкой мыши имя задания hello в hello **результатов** и выберите из меню параметров hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-137">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>
   
    ![Удаление задания](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="2fc75-139">Просмотр выполняющихся заданий</span><span class="sxs-lookup"><span data-stu-id="2fc75-139">View currently running jobs</span></span>
<span data-ttu-id="2fc75-140">Используйте следующие процедуры tooview заданий, выполняющихся в данный момент hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-140">Use hello following procedure tooview jobs that are currently running.</span></span>

#### <a name="tooview-currently-running-jobs"></a><span data-ttu-id="2fc75-141">tooview, выполняющихся заданий</span><span class="sxs-lookup"><span data-stu-id="2fc75-141">tooview currently running jobs</span></span>
1. <span data-ttu-id="2fc75-142">Щелкните значок рабочего стола hello toostart диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2fc75-142">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="2fc75-143">В hello **область** области, разверните hello **заданий** и щелкните **под управлением**.</span><span class="sxs-lookup"><span data-stu-id="2fc75-143">In hello **Scope** pane, expand hello **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="2fc75-144">В зависимости от hello **представление** параметры определяют, hello следующие сведения, отображаемые в hello **результатов** панели:</span><span class="sxs-lookup"><span data-stu-id="2fc75-144">Depending on hello **View** options you specify, hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="2fc75-145">**Имя** — hello имя запланированного моментального снимка hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-145">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="2fc75-146">**Запущен** — hello Дата и время начала создания снимка hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-146">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="2fc75-147">**Контрольная точка** — hello текущее действие резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-147">**Checkpoint** – hello current action of hello backup.</span></span>
   * <span data-ttu-id="2fc75-148">**Состояние** — hello процент завершения.</span><span class="sxs-lookup"><span data-stu-id="2fc75-148">**Status** – hello percentage of completion.</span></span>
   * <span data-ttu-id="2fc75-149">**Затраченное** — hello объем время, истекшее с момента начала резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-149">**Elapsed** – hello amount of time that has passed since hello backup began.</span></span> 
   * <span data-ttu-id="2fc75-150">**Средняя пропускная способность (МБ)** — доля общее число байтов данных, обрабатываемая toothat из общее время, необходимое для обработки (МБ).</span><span class="sxs-lookup"><span data-stu-id="2fc75-150">**Average throughput (MB)** – ratio of total bytes of data processed toothat of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="2fc75-151">**Обработано байтов (МБ)** — общее число байтов обработанных данных (в МБ).</span><span class="sxs-lookup"><span data-stu-id="2fc75-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="2fc75-152">**Записано байтов (МБ)** — общее число байтов записанных данных (в МБ).</span><span class="sxs-lookup"><span data-stu-id="2fc75-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="2fc75-153">Он включает hello данных, а также метаданные hello и поэтому обычно больше, чем hello обработано байт.</span><span class="sxs-lookup"><span data-stu-id="2fc75-153">It includes hello data as well as hello metadata and hence is typically greater than hello Bytes Processed.</span></span>
     
     ![Выполняющиеся задания](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="2fc75-155">tooperform дополнительные действия для конкретного задания, щелкните правой кнопкой мыши имя задания hello в hello **результатов** и выберите из меню параметров hello.</span><span class="sxs-lookup"><span data-stu-id="2fc75-155">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fc75-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2fc75-156">Next steps</span></span>
* <span data-ttu-id="2fc75-157">Узнайте, каким образом слишком[использования диспетчера моментальных снимков StorSimple tooadminister решения StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="2fc75-157">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="2fc75-158">Узнайте, каким образом слишком[использовать каталог резервного копирования hello диспетчера моментальных снимков StorSimple toomanage](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="2fc75-158">Learn how too[use StorSimple Snapshot Manager toomanage hello backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

