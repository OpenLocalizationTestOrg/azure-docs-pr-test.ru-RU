---
title: "aaaView и управление заданиями StorSimple | Документы Microsoft"
description: "Описывает hello StorSimple страница службы диспетчера заданий и как toouse его tootrack последних, текущего и запланированные задания резервного копирования."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b7341270e37a9f2530a8da1fb7c54f6b699c699c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs"></a><span data-ttu-id="c6fae-103">Использовать tooview службы диспетчера StorSimple hello и управление заданиями StorSimple</span><span class="sxs-lookup"><span data-stu-id="c6fae-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="c6fae-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c6fae-104">Overview</span></span>
<span data-ttu-id="c6fae-105">Hello **заданий** страница представляет собой один центральный портал для просмотра и управление заданиями, которые были запущены на устройствах, подключенных tooyour служб StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="c6fae-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="c6fae-106">Вы можете просмотреть запланированные, запущенные, завершенные и неудачные задания для нескольких устройств.</span><span class="sxs-lookup"><span data-stu-id="c6fae-106">You can view scheduled, running, completed, and failed jobs for multiple devices.</span></span> <span data-ttu-id="c6fae-107">Результаты представляются в табличном формате.</span><span class="sxs-lookup"><span data-stu-id="c6fae-107">Results are presented in a tabular format.</span></span> 

![Страница "Задания"](./media/storsimple-manage-jobs/HCS_JobsPage.png)

<span data-ttu-id="c6fae-109">Можно быстро найти hello заданий, которые вам нужны путем фильтрации по полям, такие как:</span><span class="sxs-lookup"><span data-stu-id="c6fae-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="c6fae-110">**Состояние** — у заданий могут быть следующие состояния: запущено, запланировано, ошибка, завершено, отменяется или отменено.</span><span class="sxs-lookup"><span data-stu-id="c6fae-110">**Status** – Jobs can be running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="c6fae-111">**Тип** — задания могут быть созданы по расписанию или по запросу (**Сделать архив**), в результате клонирования, восстановления устройства или операции обновления.</span><span class="sxs-lookup"><span data-stu-id="c6fae-111">**Type** – Jobs can be created as a result of a scheduled or an on-demand backup (**Take Backup**), cloning, a device restore, or an update operation.</span></span>
* <span data-ttu-id="c6fae-112">**Устройства** — задания инициируются на сообщение определенной службе tooyour подключенное устройство.</span><span class="sxs-lookup"><span data-stu-id="c6fae-112">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
* <span data-ttu-id="c6fae-113">**От и до** — задания могут быть отфильтрованный на основе hello диапазон дат и времени.</span><span class="sxs-lookup"><span data-stu-id="c6fae-113">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>

<span data-ttu-id="c6fae-114">Hello отфильтрованные задания Далее помещаются на основе hello hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="c6fae-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>

* <span data-ttu-id="c6fae-115">**Тип** — архивация, клонирование, восстановление, отработка отказа или обновление.</span><span class="sxs-lookup"><span data-stu-id="c6fae-115">**Type** – Backup, clone, restore, failover, or update.</span></span>
* <span data-ttu-id="c6fae-116">**Состояние** — запущено, запланировано, ошибка, завершено, отменяется или отменено.</span><span class="sxs-lookup"><span data-stu-id="c6fae-116">**Status** – Running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="c6fae-117">**Сущность** — hello задания могут быть связаны с томом, политикой резервного копирования или устройство.</span><span class="sxs-lookup"><span data-stu-id="c6fae-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="c6fae-118">Задание клонирования связано с томом, тогда как запланированное задание резервного копирования связано с политикой резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c6fae-118">A clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="c6fae-119">Задание устройства создается в результате аварийного восстановления (DR) или операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="c6fae-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="c6fae-120">**Устройство** — hello именем hello устройства, на какие hello задание было запущено.</span><span class="sxs-lookup"><span data-stu-id="c6fae-120">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="c6fae-121">**Начато** — hello время начала задания hello.</span><span class="sxs-lookup"><span data-stu-id="c6fae-121">**Started On** – hello time when hello job was started.</span></span>
* <span data-ttu-id="c6fae-122">**Ход выполнения** — hello процент завершения выполняемого задания.</span><span class="sxs-lookup"><span data-stu-id="c6fae-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="c6fae-123">Для завершенного задания это значение равно 100 %.</span><span class="sxs-lookup"><span data-stu-id="c6fae-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="c6fae-124">Hello список заданий обновляется каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="c6fae-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="c6fae-125">Вы можете выполнять следующие действия, связанные с работой на этой странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="c6fae-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="c6fae-126">Просмотреть сведения о задании</span><span class="sxs-lookup"><span data-stu-id="c6fae-126">View job details</span></span>
* <span data-ttu-id="c6fae-127">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="c6fae-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="c6fae-128">Просмотреть сведения о задании</span><span class="sxs-lookup"><span data-stu-id="c6fae-128">View job details</span></span>
<span data-ttu-id="c6fae-129">Выполните следующие шаги tooview hello сведения о любом задании hello.</span><span class="sxs-lookup"><span data-stu-id="c6fae-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="c6fae-130">сведения о задании tooview</span><span class="sxs-lookup"><span data-stu-id="c6fae-130">tooview job details</span></span>
1. <span data-ttu-id="c6fae-131">На hello **заданий** отображаются hello заданий необходимо выполнить в результате выполнения запроса с подходящими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="c6fae-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="c6fae-132">Можно искать завершенные, выполняющиеся или отмененные задания.</span><span class="sxs-lookup"><span data-stu-id="c6fae-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="c6fae-133">Выберите задание.</span><span class="sxs-lookup"><span data-stu-id="c6fae-133">Select a job.</span></span>
3. <span data-ttu-id="c6fae-134">Внизу hello страницы приветствия щелкните **сведения**.</span><span class="sxs-lookup"><span data-stu-id="c6fae-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="c6fae-135">В hello **сведений о задании резервного копирования** диалоговое окно, можно просмотреть состояние hello, сведения, Статистика по времени и статистику данных.</span><span class="sxs-lookup"><span data-stu-id="c6fae-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>

## <a name="cancel-a-job"></a><span data-ttu-id="c6fae-136">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="c6fae-136">Cancel a job</span></span>
<span data-ttu-id="c6fae-137">Выполните следующие шаги toocancel работающее задание hello.</span><span class="sxs-lookup"><span data-stu-id="c6fae-137">Perform hello following steps toocancel a running job.</span></span>

### <a name="toocancel-a-job"></a><span data-ttu-id="c6fae-138">toocancel задания</span><span class="sxs-lookup"><span data-stu-id="c6fae-138">toocancel a job</span></span>
1. <span data-ttu-id="c6fae-139">На hello **заданий** отображаются выполняемые задания hello требуется toocancel путем выполнения запроса с подходящими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="c6fae-139">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="c6fae-140">Выберите задание hello.</span><span class="sxs-lookup"><span data-stu-id="c6fae-140">Select hello job.</span></span>
3. <span data-ttu-id="c6fae-141">Внизу hello страницы приветствия щелкните **отменить**.</span><span class="sxs-lookup"><span data-stu-id="c6fae-141">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="c6fae-142">При появлении запроса на подтверждение нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="c6fae-142">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="c6fae-143">Теперь это задание отменено.</span><span class="sxs-lookup"><span data-stu-id="c6fae-143">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6fae-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6fae-144">Next steps</span></span>
* <span data-ttu-id="c6fae-145">Узнайте, каким образом слишком[Управление политиками резервного копирования к StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c6fae-145">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="c6fae-146">Узнайте, каким образом слишком[используйте hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c6fae-146">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

