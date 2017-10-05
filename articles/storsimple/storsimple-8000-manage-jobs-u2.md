---
title: "Просмотр и администрирование заданий для устройства StorSimple серии 8000 | Документация Майкрософт"
description: "Сведения о колонке заданий службы диспетчера устройств StorSimple и возможностях ее использования для отслеживания недавно выполненных, текущих и запланированных заданий."
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
ms.openlocfilehash: bf8038b7171053b75eeb9aed88bff4246e65a8a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="36bb4-103">Использование службы диспетчера устройств StorSimple для просмотра и администрирования заданий StorSimple (обновление 3 или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="36bb4-103">Use the StorSimple Device Manager service to view and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="36bb4-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="36bb4-104">Overview</span></span>
<span data-ttu-id="36bb4-105">Колонка **Задания** выполняет роль централизованного портала для просмотра и администрирования заданий, запущенных на устройствах, которые подключены к службе диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="36bb4-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="36bb4-106">Вы можете просмотреть запланированные, запущенные, завершенные, отмененные и неудачные задания для нескольких устройств.</span><span class="sxs-lookup"><span data-stu-id="36bb4-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="36bb4-107">Результаты представляются в табличном формате.</span><span class="sxs-lookup"><span data-stu-id="36bb4-107">Results are presented in a tabular format.</span></span>

![Колонка "Задания"](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="36bb4-109">Вы можете быстро найти задания, которые вам нужны, фильтруя данные по следующим полям:</span><span class="sxs-lookup"><span data-stu-id="36bb4-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="36bb4-110">**Состояние** — возможные варианты для заданий: выполняется, успешно завершено, отменено, завершено сбоем, выполняется отмена, успешно завершено с ошибками.</span><span class="sxs-lookup"><span data-stu-id="36bb4-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="36bb4-111">**Диапазон времени** — задания можно фильтровать по диапазону даты и времени.</span><span class="sxs-lookup"><span data-stu-id="36bb4-111">**Time range** – Jobs can be filtered based on the date and time range.</span></span> <span data-ttu-id="36bb4-112">Допустимые варианты: за последний час, за последние 24 часа, за последние 7 дней, за последние 30 дней, за последний год, пользовательские даты.</span><span class="sxs-lookup"><span data-stu-id="36bb4-112">The ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="36bb4-113">**Тип** — допустимые типы заданий: запланированное резервное копирование, резервное копирование вручную, восстановление резервной копии, клонирование тома, отработка отказа контейнеров томов, создание локально закрепленного тома, изменение тома, установка обновлений, сбор журналов поддержки или создание облачного устройства.</span><span class="sxs-lookup"><span data-stu-id="36bb4-113">**Type** – The job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="36bb4-114">**Устройства** — задания инициируются на определенном устройстве, подключенном к службе.</span><span class="sxs-lookup"><span data-stu-id="36bb4-114">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  
<span data-ttu-id="36bb4-115">Затем отфильтрованные задания будут представлены в табличной форме на основе следующих атрибутов:</span><span class="sxs-lookup"><span data-stu-id="36bb4-115">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
* <span data-ttu-id="36bb4-116">**Имя** — запланированное резервное копирование, резервное копирование вручную, восстановление резервной копии, клонирование тома, отработка отказа контейнеров томов, создание локально закрепленного тома, изменение тома, установка обновлений, сбор журналов поддержки или создание облачного устройства.</span><span class="sxs-lookup"><span data-stu-id="36bb4-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="36bb4-117">**Состояние** — запущено, запланировано, завершено ошибкой, завершено, в состоянии «отменяется» или отменено.</span><span class="sxs-lookup"><span data-stu-id="36bb4-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="36bb4-118">**Сущность** — задания могут быть связаны с томом, политикой архивации или устройством.</span><span class="sxs-lookup"><span data-stu-id="36bb4-118">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="36bb4-119">Например, задание клонирования связано с томом, тогда как запланированное задание архивации связано с политикой архивации.</span><span class="sxs-lookup"><span data-stu-id="36bb4-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="36bb4-120">Задание устройства создается в результате аварийного восстановления (DR) или операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="36bb4-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="36bb4-121">**Устройство** — имя устройства, на котором запущено задание.</span><span class="sxs-lookup"><span data-stu-id="36bb4-121">**Device** – The name of the device on which the job was started.</span></span>
* <span data-ttu-id="36bb4-122">**Время запуска** — время начала задания.</span><span class="sxs-lookup"><span data-stu-id="36bb4-122">**Started on** – The time when the job was started.</span></span>
* <span data-ttu-id="36bb4-123">**Длительность** — время, необходимое для выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="36bb4-123">**Duration** – The time required to complete the job.</span></span>

<span data-ttu-id="36bb4-124">Список заданий обновляется каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="36bb4-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="36bb4-125">На этой странице можно выполнить следующие действия, связанные с заданием.</span><span class="sxs-lookup"><span data-stu-id="36bb4-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="36bb4-126">Просмотр сведений о задании</span><span class="sxs-lookup"><span data-stu-id="36bb4-126">View job details</span></span>
* <span data-ttu-id="36bb4-127">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="36bb4-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="36bb4-128">Просмотр сведений о задании</span><span class="sxs-lookup"><span data-stu-id="36bb4-128">View job details</span></span>
<span data-ttu-id="36bb4-129">Выполните следующие действия для просмотра сведений о любом задании.</span><span class="sxs-lookup"><span data-stu-id="36bb4-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="36bb4-130">Просмотр сведений о задании</span><span class="sxs-lookup"><span data-stu-id="36bb4-130">To view job details</span></span>
1. <span data-ttu-id="36bb4-131">В службе диспетчера устройств StorSimple выберите **Задания**.</span><span class="sxs-lookup"><span data-stu-id="36bb4-131">Go to your StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="36bb4-132">В колонке **Задания** найдите интересующие вас задания, выполнив запрос с соответствующими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="36bb4-132">In the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="36bb4-133">Можно искать завершенные, выполняющиеся или отмененные задания.</span><span class="sxs-lookup"><span data-stu-id="36bb4-133">You can search for completed, running, or canceled jobs.</span></span>

    ![Колонка "Задание"](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="36bb4-135">Выберите нужное задание.</span><span class="sxs-lookup"><span data-stu-id="36bb4-135">Select and click a job.</span></span>

    ![Колонка "Задание"](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="36bb4-137">В колонке сведений о задании вы можете просмотреть состояние, подробные данные, а также статистику по времени и данным.</span><span class="sxs-lookup"><span data-stu-id="36bb4-137">In the job details blade, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![Сведения о задании](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="36bb4-139">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="36bb4-139">Cancel a job</span></span>
<span data-ttu-id="36bb4-140">Выполните следующие действия для отмены запущенного задания.</span><span class="sxs-lookup"><span data-stu-id="36bb4-140">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="36bb4-141">Некоторые задания, например изменение тома для смены типа тома или расширения тома, нельзя отменить.</span><span class="sxs-lookup"><span data-stu-id="36bb4-141">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="to-cancel-a-job"></a><span data-ttu-id="36bb4-142">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="36bb4-142">To cancel a job</span></span>
1. <span data-ttu-id="36bb4-143">На странице **Задания** можно отобразить задания, которые нужно отменить, выполнив запрос с соответствующими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="36bb4-143">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span> <span data-ttu-id="36bb4-144">Выберите задание.</span><span class="sxs-lookup"><span data-stu-id="36bb4-144">Select the job.</span></span>

2. <span data-ttu-id="36bb4-145">Щелкните выбранное задание правой кнопкой мыши, чтобы открыть контекстное меню, и выберите действие **Отмена**.</span><span class="sxs-lookup"><span data-stu-id="36bb4-145">Right-click on the selected job to invoke the context menu and click **Cancel**.</span></span>

    ![Сведения о задании](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="36bb4-147">При появлении запроса на подтверждение нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="36bb4-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="36bb4-148">Теперь это задание отменено.</span><span class="sxs-lookup"><span data-stu-id="36bb4-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36bb4-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36bb4-149">Next steps</span></span>
* <span data-ttu-id="36bb4-150">Узнайте об [управлении политиками архивации StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="36bb4-150">Learn how to [manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="36bb4-151">Узнайте, как [использовать службу диспетчера устройств StorSimple для администрирования устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="36bb4-151">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

