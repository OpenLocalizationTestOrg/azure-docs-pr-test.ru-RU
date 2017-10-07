---
title: "aaaManage каталога резервного копирования StorSimple | Документы Microsoft"
description: "Объясняет, как hello toouse toolist страницы каталога резервных копий службы диспетчера StorSimple устройство, выберите и удалите резервных наборов данных."
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
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="d7abd-103">Использовать toomanage службы диспетчера StorSimple устройство hello каталога резервного копирования</span><span class="sxs-lookup"><span data-stu-id="d7abd-103">Use hello StorSimple Device Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="d7abd-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d7abd-104">Overview</span></span>
<span data-ttu-id="d7abd-105">службе диспетчера StorSimple устройство Hello **каталога резервного копирования** колонке отображает все hello резервные наборы данных, созданные при резервном копировании вручную или по расписанию.</span><span class="sxs-lookup"><span data-stu-id="d7abd-105">hello StorSimple Device Manager service **Backup Catalog** blade displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="d7abd-106">Можно использовать все резервные копии hello toolist этой страницы для политики резервного копирования или тома, выбора или удалить резервные копии, или использовать резервного копирования toorestore или клонирования тома.</span><span class="sxs-lookup"><span data-stu-id="d7abd-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="d7abd-107">В этом учебнике описано, как toolist, select и удаления резервного набора данных.</span><span class="sxs-lookup"><span data-stu-id="d7abd-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="d7abd-108">toolearn как toorestore устройства из резервной копии, go слишком[восстановление из резервной копии устройства](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="d7abd-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="d7abd-109">как tooclone тома, go слишком toolearn[клонирование тома StorSimple](storsimple-8000-clone-volume-u2.md).</span><span class="sxs-lookup"><span data-stu-id="d7abd-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![Каталог резервного копирования](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="d7abd-111">Hello **каталога резервного копирования** колонке предоставляет toonarrow запроса Выбор резервного набора данных.</span><span class="sxs-lookup"><span data-stu-id="d7abd-111">hello **Backup Catalog** blade provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="d7abd-112">Вы можете фильтровать hello резервных наборов данных, полученных, в зависимости от hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="d7abd-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="d7abd-113">**Устройство** — hello устройства, на какие hello резервный набор данных был создан.</span><span class="sxs-lookup"><span data-stu-id="d7abd-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="d7abd-114">**Политики резервного копирования или тома** — hello политики резервного копирования или тома, связанные с этого резервного набора данных.</span><span class="sxs-lookup"><span data-stu-id="d7abd-114">**Backup policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="d7abd-115">**От и до** — hello диапазон дат и времени, когда hello резервный набор данных был создан.</span><span class="sxs-lookup"><span data-stu-id="d7abd-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="d7abd-116">Hello отфильтрованные наборы резервных копий затем помещаются в зависимости от hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="d7abd-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="d7abd-117">**Имя** — hello имя политики резервного копирования hello или тома, связанные с hello резервного набора данных.</span><span class="sxs-lookup"><span data-stu-id="d7abd-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="d7abd-118">**Размер** — hello фактический размер резервного набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="d7abd-119">**Создание** — hello Дата и время создания резервных копий hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="d7abd-120">**Тип** — наборы резервного копирования могут представлять собой локальные моментальные снимки или облачные моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="d7abd-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="d7abd-121">Локальный моментальный снимок является резервная копия всех томов данных, сохраняемых локально на устройстве hello, тогда как toohello резервная копия данных тома, размещенные в облаке hello ссылается облачного моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="d7abd-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="d7abd-122">Локальные моментальные снимки обеспечивают более быстрый доступ, а облачные моментальные снимки выбираются для обеспечения устойчивости данных.</span><span class="sxs-lookup"><span data-stu-id="d7abd-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="d7abd-123">**Инициировано** — hello резервные копии могут инициироваться автоматически по расписанию или вручную пользователем.</span><span class="sxs-lookup"><span data-stu-id="d7abd-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="d7abd-124">Можно использовать резервные копии tooschedule политику резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="d7abd-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="d7abd-125">Кроме того, можно использовать hello **создайте резервную копию** tootake параметр резервного копирования вручную.</span><span class="sxs-lookup"><span data-stu-id="d7abd-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="d7abd-126">Создание списка резервных наборов данных для политики резервного копирования</span><span class="sxs-lookup"><span data-stu-id="d7abd-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="d7abd-127">Выполните следующие шаги toolist hello все резервные копии hello для политики резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="d7abd-127">Complete hello following steps toolist all hello backups for a backup policy.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="d7abd-128">резервные наборы данных toolist</span><span class="sxs-lookup"><span data-stu-id="d7abd-128">toolist backup sets</span></span>
1. <span data-ttu-id="d7abd-129">Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **каталог резервных копий**.</span><span class="sxs-lookup"><span data-stu-id="d7abd-129">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="d7abd-130">Фильтровать выбранные hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d7abd-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="d7abd-131">Укажите диапазон времени hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-131">Specify hello time range.</span></span>
   2. <span data-ttu-id="d7abd-132">Выберите подходящее устройство hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-132">Select hello appropriate device.</span></span>
   3. <span data-ttu-id="d7abd-133">Фильтрация по **политика архивации** tooview hello соответствующим резервным копиям hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-133">Filter by **Backup policy** tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="d7abd-134">Из раскрывающегося списка hello политики резервного копирования, выберите **все** tooview все hello резервные копии на hello выбранного устройства.</span><span class="sxs-lookup"><span data-stu-id="d7abd-134">From hello backup policy dropdown list, choose **All** tooview all hello backups on hello selected device.</span></span>
   4. <span data-ttu-id="d7abd-135">Нажмите кнопку **применить** tooexecute этот запрос.</span><span class="sxs-lookup"><span data-stu-id="d7abd-135">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="d7abd-136">Hello резервные копии, связанные с политикой резервного копирования выбран hello должны появиться в списке наборов резервных копий hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-136">hello backups associated with hello selected backup policy should appear in hello list of backup sets.</span></span>

      ![Перейдите в каталог toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="d7abd-138">Выбор резервного набора данных</span><span class="sxs-lookup"><span data-stu-id="d7abd-138">Select a backup set</span></span>
<span data-ttu-id="d7abd-139">Выполните следующие шаги tooselect резервного набора данных для том или политика архивации hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="d7abd-140">tooselect набора резервных копий</span><span class="sxs-lookup"><span data-stu-id="d7abd-140">tooselect a backup set</span></span>
1. <span data-ttu-id="d7abd-141">Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **каталог резервных копий**.</span><span class="sxs-lookup"><span data-stu-id="d7abd-141">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="d7abd-142">Фильтровать выбранные hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d7abd-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="d7abd-143">Укажите диапазон времени hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-143">Specify hello time range.</span></span> 
   2. <span data-ttu-id="d7abd-144">Выберите подходящее устройство hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-144">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="d7abd-145">Фильтрация по том или политика архивации для резервного копирования hello, что вы хотите tooselect.</span><span class="sxs-lookup"><span data-stu-id="d7abd-145">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="d7abd-146">Нажмите кнопку **применить** tooexecute этот запрос.</span><span class="sxs-lookup"><span data-stu-id="d7abd-146">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="d7abd-147">Hello резервные копии, связанные с hello выбран том или политика архивации должны появиться в списке наборов резервных копий hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-147">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Перейдите в каталог toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="d7abd-149">Выберите и разверните резервный набор данных.</span><span class="sxs-lookup"><span data-stu-id="d7abd-149">Select and expand a backup set.</span></span> <span data-ttu-id="d7abd-150">Теперь можно увидеть hello резервных наборов данных разбивкой на hello томов, которые она содержит.</span><span class="sxs-lookup"><span data-stu-id="d7abd-150">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="d7abd-151">Hello **восстановить** и **удалить** доступны через hello контекстное меню (правой кнопкой мыши) для hello резервного набора данных.</span><span class="sxs-lookup"><span data-stu-id="d7abd-151">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="d7abd-152">Одно из этих действий можно выполнить на hello резервный набор данных, вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="d7abd-152">You can perform either of these actions on hello backup set that you selected.</span></span>

    ![Перейдите в каталог toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="d7abd-154">Удаление резервного набора данных</span><span class="sxs-lookup"><span data-stu-id="d7abd-154">Delete a backup set</span></span>
<span data-ttu-id="d7abd-155">Удаление резервной копии, когда необходимо прекратить tooretain hello данные, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="d7abd-155">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="d7abd-156">Выполните hello следующие шаги toodelete набора резервных копий.</span><span class="sxs-lookup"><span data-stu-id="d7abd-156">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="d7abd-157">toodelete набора резервных копий</span><span class="sxs-lookup"><span data-stu-id="d7abd-157">toodelete a backup set</span></span>
 <span data-ttu-id="d7abd-158">Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **каталог резервных копий**.</span><span class="sxs-lookup"><span data-stu-id="d7abd-158">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="d7abd-159">Фильтровать выбранные hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d7abd-159">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="d7abd-160">Укажите диапазон времени hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-160">Specify hello time range.</span></span> 
   2. <span data-ttu-id="d7abd-161">Выберите подходящее устройство hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-161">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="d7abd-162">Фильтрация по том или политика архивации для резервного копирования hello, что вы хотите tooselect.</span><span class="sxs-lookup"><span data-stu-id="d7abd-162">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="d7abd-163">Нажмите кнопку **применить** tooexecute этот запрос.</span><span class="sxs-lookup"><span data-stu-id="d7abd-163">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="d7abd-164">Hello резервные копии, связанные с hello выбран том или политика архивации должны появиться в списке наборов резервных копий hello.</span><span class="sxs-lookup"><span data-stu-id="d7abd-164">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Перейдите в каталог toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="d7abd-166">Выберите и разверните резервный набор данных.</span><span class="sxs-lookup"><span data-stu-id="d7abd-166">Select and expand a backup set.</span></span> <span data-ttu-id="d7abd-167">Теперь можно увидеть hello резервных наборов данных разбивкой на hello томов, которые она содержит.</span><span class="sxs-lookup"><span data-stu-id="d7abd-167">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="d7abd-168">Hello **восстановить** и **удалить** доступны через hello контекстное меню (правой кнопкой мыши) для hello резервного набора данных.</span><span class="sxs-lookup"><span data-stu-id="d7abd-168">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="d7abd-169">Щелкните правой кнопкой мыши выбранные hello резервного набора данных и hello контекстном меню, выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="d7abd-169">Right-click hello selected backup set and from hello context menu, select **Delete**.</span></span>

    ![Перейдите в каталог toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="d7abd-171">При появлении запроса на подтверждение просмотрите hello отображаются сведения и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="d7abd-171">When prompted for confirmation, review hello displayed information and click **Delete**.</span></span> <span data-ttu-id="d7abd-172">Hello выбранной резервной копии, удаляются навсегда.</span><span class="sxs-lookup"><span data-stu-id="d7abd-172">hello selected backup is deleted permanently.</span></span>

    ![Перейдите в каталог toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="d7abd-174">Вы получите уведомление, когда идет удаление hello и когда завершена успешно.</span><span class="sxs-lookup"><span data-stu-id="d7abd-174">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="d7abd-175">После завершения удаления hello обновите запрос hello на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d7abd-175">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="d7abd-176">Hello удалить резервный набор данных больше не отобразится в списке hello резервных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="d7abd-176">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

    ![Перейдите в каталог toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="d7abd-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d7abd-178">Next steps</span></span>
* <span data-ttu-id="d7abd-179">Узнайте, каким образом слишком[используйте hello toorestore каталога резервного копирования устройства в резервном наборе данных](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="d7abd-179">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="d7abd-180">Узнайте, каким образом слишком[используйте hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d7abd-180">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

