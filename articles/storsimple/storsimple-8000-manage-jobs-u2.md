---
title: "aaaView и управление заданиями для StorSimple серии 8000 | Документы Microsoft"
description: "Описывает колонке задания службы диспетчера StorSimple устройство hello и как toouse его tootrack последних, текущего и запланированные задания резервного копирования."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="a0e32-103">Использовать tooview службы диспетчера StorSimple устройство hello заданий и управление ими (обновление 3 и более поздние версии)</span><span class="sxs-lookup"><span data-stu-id="a0e32-103">Use hello StorSimple Device Manager service tooview and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="a0e32-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a0e32-104">Overview</span></span>
<span data-ttu-id="a0e32-105">Hello **заданий** колонке представляет собой один центральный портал для просмотра и управление заданиями, которые были запущены на устройствах, подключенных служб tooyour устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a0e32-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="a0e32-106">Вы можете просмотреть запланированные, запущенные, завершенные, отмененные и неудачные задания для нескольких устройств.</span><span class="sxs-lookup"><span data-stu-id="a0e32-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="a0e32-107">Результаты представляются в табличном формате.</span><span class="sxs-lookup"><span data-stu-id="a0e32-107">Results are presented in a tabular format.</span></span>

![Колонка "Задания"](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="a0e32-109">Можно быстро найти hello заданий, которые вам нужны путем фильтрации по полям, такие как:</span><span class="sxs-lookup"><span data-stu-id="a0e32-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="a0e32-110">**Состояние** — возможные варианты для заданий: выполняется, успешно завершено, отменено, завершено сбоем, выполняется отмена, успешно завершено с ошибками.</span><span class="sxs-lookup"><span data-stu-id="a0e32-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="a0e32-111">**Временной диапазон** — задания могут быть отфильтрованный на основе hello диапазон дат и времени.</span><span class="sxs-lookup"><span data-stu-id="a0e32-111">**Time range** – Jobs can be filtered based on hello date and time range.</span></span> <span data-ttu-id="a0e32-112">диапазоны Hello были разрешены за 1 час, за последние 24 часа, последние 7 дней, за последние 30 дней, в прошлом году, или настраиваемые дата.</span><span class="sxs-lookup"><span data-stu-id="a0e32-112">hello ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="a0e32-113">**Тип** — может быть типа hello задания архивации по расписанию, вручную резервного копирования, восстановления резервной копии, клонирование тома, отработки отказа контейнеры томов, локально закрепленного тома, изменения тома, установки обновлений, собирать журналы поддержки и создание облачных устройств.</span><span class="sxs-lookup"><span data-stu-id="a0e32-113">**Type** – hello job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="a0e32-114">**Устройства** — задания инициируются на сообщение определенной службе tooyour подключенное устройство.</span><span class="sxs-lookup"><span data-stu-id="a0e32-114">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  
<span data-ttu-id="a0e32-115">Hello отфильтрованные задания Далее помещаются на основе hello hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="a0e32-115">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
* <span data-ttu-id="a0e32-116">**Имя** — запланированное резервное копирование, резервное копирование вручную, восстановление резервной копии, клонирование тома, отработка отказа контейнеров томов, создание локально закрепленного тома, изменение тома, установка обновлений, сбор журналов поддержки или создание облачного устройства.</span><span class="sxs-lookup"><span data-stu-id="a0e32-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="a0e32-117">**Состояние** — запущено, запланировано, завершено ошибкой, завершено, в состоянии «отменяется» или отменено.</span><span class="sxs-lookup"><span data-stu-id="a0e32-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="a0e32-118">**Сущность** — hello задания могут быть связаны с томом, политикой резервного копирования или устройство.</span><span class="sxs-lookup"><span data-stu-id="a0e32-118">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="a0e32-119">Например, задание клонирования связано с томом, тогда как запланированное задание архивации связано с политикой архивации.</span><span class="sxs-lookup"><span data-stu-id="a0e32-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="a0e32-120">Задание устройства создается в результате аварийного восстановления (DR) или операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="a0e32-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="a0e32-121">**Устройство** — hello именем hello устройства, на какие hello задание было запущено.</span><span class="sxs-lookup"><span data-stu-id="a0e32-121">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="a0e32-122">**Запущен на** — hello время начала задания hello.</span><span class="sxs-lookup"><span data-stu-id="a0e32-122">**Started on** – hello time when hello job was started.</span></span>
* <span data-ttu-id="a0e32-123">**Длительность** — задание hello необходимые toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="a0e32-123">**Duration** – hello time required toocomplete hello job.</span></span>

<span data-ttu-id="a0e32-124">Hello список заданий обновляется каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="a0e32-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="a0e32-125">Вы можете выполнять следующие действия, связанные с работой на этой странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="a0e32-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="a0e32-126">Просмотреть сведения о задании</span><span class="sxs-lookup"><span data-stu-id="a0e32-126">View job details</span></span>
* <span data-ttu-id="a0e32-127">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="a0e32-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="a0e32-128">Просмотреть сведения о задании</span><span class="sxs-lookup"><span data-stu-id="a0e32-128">View job details</span></span>
<span data-ttu-id="a0e32-129">Выполните следующие шаги tooview hello сведения о любом задании hello.</span><span class="sxs-lookup"><span data-stu-id="a0e32-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="a0e32-130">сведения о задании tooview</span><span class="sxs-lookup"><span data-stu-id="a0e32-130">tooview job details</span></span>
1. <span data-ttu-id="a0e32-131">Перейдите в службе диспетчера StorSimple устройство tooyour и нажмите кнопку **задания**.</span><span class="sxs-lookup"><span data-stu-id="a0e32-131">Go tooyour StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="a0e32-132">В hello **заданий** колонки, отображения hello заданий необходимо выполнить в результате выполнения запроса с подходящими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="a0e32-132">In hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="a0e32-133">Можно искать завершенные, выполняющиеся или отмененные задания.</span><span class="sxs-lookup"><span data-stu-id="a0e32-133">You can search for completed, running, or canceled jobs.</span></span>

    ![Колонка "Задание"](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="a0e32-135">Выберите нужное задание.</span><span class="sxs-lookup"><span data-stu-id="a0e32-135">Select and click a job.</span></span>

    ![Колонка "Задание"](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="a0e32-137">В колонке сведения hello задания можно просмотреть состояние hello, сведения, Статистика по времени и статистику данных.</span><span class="sxs-lookup"><span data-stu-id="a0e32-137">In hello job details blade, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Сведения о задании](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="a0e32-139">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="a0e32-139">Cancel a job</span></span>
<span data-ttu-id="a0e32-140">Выполните следующие шаги toocancel работающее задание hello.</span><span class="sxs-lookup"><span data-stu-id="a0e32-140">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="a0e32-141">Некоторые задания, например изменение тома toochange hello томе, тип или расширить том, нельзя отменить.</span><span class="sxs-lookup"><span data-stu-id="a0e32-141">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="toocancel-a-job"></a><span data-ttu-id="a0e32-142">toocancel задания</span><span class="sxs-lookup"><span data-stu-id="a0e32-142">toocancel a job</span></span>
1. <span data-ttu-id="a0e32-143">На hello **заданий** отображаются выполняемые задания hello требуется toocancel путем выполнения запроса с подходящими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="a0e32-143">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span> <span data-ttu-id="a0e32-144">Выберите задание hello.</span><span class="sxs-lookup"><span data-stu-id="a0e32-144">Select hello job.</span></span>

2. <span data-ttu-id="a0e32-145">Щелкните правой кнопкой мыши hello выбранное задание tooinvoke hello контекстного меню и нажмите кнопку **отменить**.</span><span class="sxs-lookup"><span data-stu-id="a0e32-145">Right-click on hello selected job tooinvoke hello context menu and click **Cancel**.</span></span>

    ![Сведения о задании](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="a0e32-147">При появлении запроса на подтверждение нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="a0e32-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="a0e32-148">Теперь это задание отменено.</span><span class="sxs-lookup"><span data-stu-id="a0e32-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0e32-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a0e32-149">Next steps</span></span>
* <span data-ttu-id="a0e32-150">Узнайте, каким образом слишком[Управление политиками резервного копирования к StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="a0e32-150">Learn how too[manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="a0e32-151">Узнайте, каким образом слишком[используйте hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a0e32-151">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

