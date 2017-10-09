---
title: "aaaView и управление заданиями StorSimple | Документы Microsoft"
description: "Описывает hello StorSimple страница службы диспетчера заданий и как toouse его tootrack последних, текущего и запланированные задания резервного копирования."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="1f3e0-103">Использовать tooview службы диспетчера StorSimple hello и управление заданиями StorSimple (обновление 2)</span><span class="sxs-lookup"><span data-stu-id="1f3e0-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="1f3e0-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="1f3e0-104">Overview</span></span>
<span data-ttu-id="1f3e0-105">Hello **заданий** страница представляет собой один центральный портал для просмотра и управление заданиями, которые были запущены на устройствах, подключенных tooyour служб StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="1f3e0-106">Вы можете просмотреть запланированные, запущенные, завершенные, отмененные и неудачные задания для нескольких устройств.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="1f3e0-107">Результаты представляются в табличном формате.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-107">Results are presented in a tabular format.</span></span> 

![Страница "Задания"](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="1f3e0-109">Можно быстро найти hello заданий, которые вам нужны путем фильтрации по полям, такие как:</span><span class="sxs-lookup"><span data-stu-id="1f3e0-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="1f3e0-110">**Состояние** — задание может быть запущено, запланировано, завершено ошибкой, завершено, в состоянии «отменяется» или отменено.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="1f3e0-111">**От и до** — задания могут быть отфильтрованный на основе hello диапазон дат и времени.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-111">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="1f3e0-112">**Тип** — тип задания hello может быть резервного копирования, ручной архивации, восстановления, клонирования, отработки отказа устройства, создание локально закрепленного тома, изменения тома, обновление и поддерживают пакета или подготовки виртуального устройства.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-112">**Type** – hello job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="1f3e0-113">**Устройства** — задания инициируются на сообщение определенной службе tooyour подключенное устройство.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-113">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  <span data-ttu-id="1f3e0-114">Hello отфильтрованные задания Далее помещаются на основе hello hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="1f3e0-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
  * <span data-ttu-id="1f3e0-115">**Тип** — архивация, ручная архивация, восстановление, клонирование, отработки отказа устройства, создание локально закрепленного тома, изменение тома, обновление, пакет поддержки или подготовка виртуального устройства.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="1f3e0-116">**Состояние** — запущено, запланировано, завершено ошибкой, завершено, в состоянии «отменяется» или отменено.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="1f3e0-117">**Сущность** — hello задания могут быть связаны с томом, политикой резервного копирования или устройство.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="1f3e0-118">Например, задание клонирования связано с томом, тогда как запланированное задание архивации связано с политикой архивации.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="1f3e0-119">Задание устройства создается в результате аварийного восстановления (DR) или операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="1f3e0-120">**Устройство** — hello именем hello устройства, на какие hello задание было запущено.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-120">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="1f3e0-121">**Запущен на** — hello время начала задания hello.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-121">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="1f3e0-122">**Ход выполнения** — hello процент завершения выполняемого задания.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="1f3e0-123">Для завершенного задания это значение равно 100 %.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="1f3e0-124">Hello список заданий обновляется каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="1f3e0-125">Вы можете выполнять следующие действия, связанные с работой на этой странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="1f3e0-126">Просмотреть сведения о задании</span><span class="sxs-lookup"><span data-stu-id="1f3e0-126">View job details</span></span>
* <span data-ttu-id="1f3e0-127">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="1f3e0-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="1f3e0-128">Просмотреть сведения о задании</span><span class="sxs-lookup"><span data-stu-id="1f3e0-128">View job details</span></span>
<span data-ttu-id="1f3e0-129">Выполните следующие шаги tooview hello сведения о любом задании hello.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="1f3e0-130">сведения о задании tooview</span><span class="sxs-lookup"><span data-stu-id="1f3e0-130">tooview job details</span></span>
1. <span data-ttu-id="1f3e0-131">На hello **заданий** отображаются hello заданий необходимо выполнить в результате выполнения запроса с подходящими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="1f3e0-132">Можно искать завершенные, выполняющиеся или отмененные задания.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="1f3e0-133">Выберите задание.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-133">Select a job.</span></span>
3. <span data-ttu-id="1f3e0-134">Внизу hello страницы приветствия щелкните **сведения**.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="1f3e0-135">В hello **сведений о задании резервного копирования** диалоговое окно, можно просмотреть состояние hello, сведения, Статистика по времени и статистику данных.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Страница сведений о задании](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="1f3e0-137">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="1f3e0-137">Cancel a job</span></span>
<span data-ttu-id="1f3e0-138">Выполните следующие шаги toocancel работающее задание hello.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-138">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="1f3e0-139">Некоторые задания, например изменение тома toochange hello томе, тип или расширить том, нельзя отменить.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-139">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="toocancel-a-job"></a><span data-ttu-id="1f3e0-140">toocancel задания</span><span class="sxs-lookup"><span data-stu-id="1f3e0-140">toocancel a job</span></span>
1. <span data-ttu-id="1f3e0-141">На hello **заданий** отображаются выполняемые задания hello требуется toocancel путем выполнения запроса с подходящими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-141">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="1f3e0-142">Выберите задание hello.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-142">Select hello job.</span></span>
3. <span data-ttu-id="1f3e0-143">Внизу hello страницы приветствия щелкните **отменить**.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-143">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="1f3e0-144">При появлении запроса на подтверждение нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="1f3e0-145">Теперь это задание отменено.</span><span class="sxs-lookup"><span data-stu-id="1f3e0-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f3e0-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f3e0-146">Next steps</span></span>
* <span data-ttu-id="1f3e0-147">Узнайте, каким образом слишком[Управление политиками резервного копирования к StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="1f3e0-147">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="1f3e0-148">Узнайте, каким образом слишком[используйте hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="1f3e0-148">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

