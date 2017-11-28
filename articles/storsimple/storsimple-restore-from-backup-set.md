---
title: "тома StorSimple из резервной копии aaaRestore | Документы Microsoft"
description: "Объясняет, как toouse hello toorestore странице каталога резервных копий службы диспетчера StorSimple тома StorSimple из резервной копии."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="31d4a-103">Восстановление тома StorSimple из резервного набора данных</span><span class="sxs-lookup"><span data-stu-id="31d4a-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="31d4a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="31d4a-104">Overview</span></span>
<span data-ttu-id="31d4a-105">Hello **каталога резервного копирования** странице отображаются все hello резервные наборы данных, созданные при резервном копировании автоматически или вручную.</span><span class="sxs-lookup"><span data-stu-id="31d4a-105">hello **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="31d4a-106">Можно использовать все резервные копии hello toolist этой страницы для политики резервного копирования или тома, выбора или удалить резервные копии, или использовать резервного копирования toorestore или клонирования тома.</span><span class="sxs-lookup"><span data-stu-id="31d4a-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

 ![Страница каталога резервного копирования](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="31d4a-108">В этом учебнике описано как toouse hello **каталога резервного копирования** toorestore страницы тома на устройстве из резервной копии.</span><span class="sxs-lookup"><span data-stu-id="31d4a-108">This tutorial explains how toouse hello **Backup Catalog** page toorestore a volume on your device from a backup set.</span></span>

## <a name="how-toouse-hello-backup-catalog"></a><span data-ttu-id="31d4a-109">Как toouse hello каталога резервного копирования</span><span class="sxs-lookup"><span data-stu-id="31d4a-109">How toouse hello backup catalog</span></span>
<span data-ttu-id="31d4a-110">Hello **каталога резервного копирования** страница содержит запрос, который помогает toonarrow Выбор резервного набора данных.</span><span class="sxs-lookup"><span data-stu-id="31d4a-110">hello **Backup Catalog** page provides a query that helps you toonarrow your backup set selection.</span></span> <span data-ttu-id="31d4a-111">Вы можете фильтровать hello резервных наборов данных, получаемых основании hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="31d4a-111">You can filter hello backup sets that are retrieved based on hello following parameters:</span></span>

* <span data-ttu-id="31d4a-112">**Устройство** — hello устройства, на какие hello резервный набор данных был создан.</span><span class="sxs-lookup"><span data-stu-id="31d4a-112">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="31d4a-113">**Политика архивации** или **тома** — hello политики резервного копирования или тома, связанные с этого резервного набора данных.</span><span class="sxs-lookup"><span data-stu-id="31d4a-113">**Backup policy** or **volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="31d4a-114">**Из** и **для** — hello диапазон дат и времени, когда hello резервный набор данных был создан.</span><span class="sxs-lookup"><span data-stu-id="31d4a-114">**From** and **To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="31d4a-115">Hello отфильтрованные наборы резервных копий затем помещаются в зависимости от hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="31d4a-115">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="31d4a-116">**Имя** — hello имя политики резервного копирования hello или тома, связанные с hello резервного набора данных.</span><span class="sxs-lookup"><span data-stu-id="31d4a-116">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="31d4a-117">**Размер** — hello фактический размер резервного набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="31d4a-117">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="31d4a-118">**Создан на** — hello Дата и время создания резервных копий hello.</span><span class="sxs-lookup"><span data-stu-id="31d4a-118">**Created on** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="31d4a-119">**Тип** — наборы резервного копирования могут представлять собой локальные моментальные снимки или облачные моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="31d4a-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="31d4a-120">Локальный моментальный снимок является резервная копия всех томов данных, сохраняемых локально на устройстве hello, тогда как toohello резервная копия данных тома, размещенные в облаке hello ссылается облачного моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="31d4a-120">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="31d4a-121">Локальные моментальные снимки обеспечивают более быстрый доступ, а облачные моментальные снимки выбираются для обеспечения устойчивости данных.</span><span class="sxs-lookup"><span data-stu-id="31d4a-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="31d4a-122">**Инициировано** — hello резервные копии могут инициироваться автоматически в соответствии с расписанием tooa или вручную пользователем.</span><span class="sxs-lookup"><span data-stu-id="31d4a-122">**Initiated by** – hello backups can be initiated automatically according tooa schedule or manually by a user.</span></span> <span data-ttu-id="31d4a-123">(Можно использовать резервные копии tooschedule политику резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="31d4a-123">(You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="31d4a-124">Кроме того, можно использовать hello **создайте резервную копию** tootake параметр интерактивного резервного копирования.)</span><span class="sxs-lookup"><span data-stu-id="31d4a-124">Alternatively, you can use hello **Take backup** option tootake an interactive backup.)</span></span>

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="31d4a-125">Как toorestore тома StorSimple из резервной копии</span><span class="sxs-lookup"><span data-stu-id="31d4a-125">How toorestore your StorSimple volume from a backup</span></span>
<span data-ttu-id="31d4a-126">Можно использовать hello **каталога резервного копирования** страница toorestore тома StorSimple из заданной резервной копии.</span><span class="sxs-lookup"><span data-stu-id="31d4a-126">You can use hello **Backup Catalog** page toorestore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="31d4a-127">Восстановление из резервной копии заменит существующие тома hello из резервной копии hello.</span><span class="sxs-lookup"><span data-stu-id="31d4a-127">Restoring from a backup will replace hello existing volumes from hello backup.</span></span> <span data-ttu-id="31d4a-128">Это может привести к потере hello любых данных, которые были записаны после hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="31d4a-128">This may cause hello loss of any data that was written after hello backup was taken.</span></span>
> 
> 

<span data-ttu-id="31d4a-129">Прежде чем начать восстановление на томе, убедитесь, что hello том находится в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="31d4a-129">Before you initiate a restore on a volume, ensure that hello volume is offline.</span></span> <span data-ttu-id="31d4a-130">Может потребоваться tootake hello том в автономный режим на узле hello сначала и затем hello устройства.</span><span class="sxs-lookup"><span data-stu-id="31d4a-130">You will need tootake hello volume offline on hello host first and then hello device.</span></span> <span data-ttu-id="31d4a-131">Следуйте указаниям hello [перевести том в автономный режим](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="31d4a-131">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="31d4a-132">Выполните следующие шаги toorestore тома из резервной копии hello.</span><span class="sxs-lookup"><span data-stu-id="31d4a-132">Perform hello following steps toorestore a volume from a backup set.</span></span>

### <a name="toorestore-from-a-backup-set"></a><span data-ttu-id="31d4a-133">toorestore из резервной копии</span><span class="sxs-lookup"><span data-stu-id="31d4a-133">toorestore from a backup set</span></span>
1. <span data-ttu-id="31d4a-134">На странице службы диспетчера StorSimple hello щелкните hello **каталог резервных копий** вкладки.</span><span class="sxs-lookup"><span data-stu-id="31d4a-134">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
   
    ![Каталог резервного копирования](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="31d4a-136">Выберите резервный набор данных следующим образом:</span><span class="sxs-lookup"><span data-stu-id="31d4a-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="31d4a-137">Выберите подходящее устройство hello.</span><span class="sxs-lookup"><span data-stu-id="31d4a-137">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="31d4a-138">В раскрывающемся списке hello выберите hello том или политика архивации для резервного копирования hello, tooselect.</span><span class="sxs-lookup"><span data-stu-id="31d4a-138">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="31d4a-139">Укажите диапазон времени hello.</span><span class="sxs-lookup"><span data-stu-id="31d4a-139">Specify hello time range.</span></span>
   4. <span data-ttu-id="31d4a-140">Щелкните значок галочки hello</span><span class="sxs-lookup"><span data-stu-id="31d4a-140">Click hello check icon</span></span> ![значок галочки](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="31d4a-142">tooexecute этот запрос.</span><span class="sxs-lookup"><span data-stu-id="31d4a-142">tooexecute this query.</span></span>
      
      <span data-ttu-id="31d4a-143">Hello резервные копии, связанные с hello выбран том или политика архивации должны появиться в списке наборов резервных копий hello.</span><span class="sxs-lookup"><span data-stu-id="31d4a-143">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="31d4a-144">Раскройте hello резервного набора данных tooview hello связанные тома.</span><span class="sxs-lookup"><span data-stu-id="31d4a-144">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="31d4a-145">Эти тома необходимо отключить от сети на узле hello и устройства, прежде чем их можно восстановить.</span><span class="sxs-lookup"><span data-stu-id="31d4a-145">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="31d4a-146">Следуйте указаниям hello [перевести том в автономный режим](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="31d4a-146">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="31d4a-147">Убедитесь, что вы предпримете hello тома в автономный режим на узле hello во-первых, прежде чем переводить hello тома в автономный режим на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="31d4a-147">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="31d4a-148">Если не будет выполнено hello тома в автономный режим на узле hello, он может привести toodata повреждения.</span><span class="sxs-lookup"><span data-stu-id="31d4a-148">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="31d4a-149">Выберите набор архивации.</span><span class="sxs-lookup"><span data-stu-id="31d4a-149">Select a backup set.</span></span> <span data-ttu-id="31d4a-150">Нажмите кнопку **восстановить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="31d4a-150">Click **Restore** at hello bottom of hello page.</span></span>
5. <span data-ttu-id="31d4a-151">После этого введите подтверждение для применения этих исправлений.</span><span class="sxs-lookup"><span data-stu-id="31d4a-151">You will be prompted for confirmation.</span></span> 
   
    ![Страница подтверждения](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="31d4a-153">Просмотрите информацию восстановления hello и щелкните значок галочки hello ![значок галочки](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="31d4a-153">Review hello restore information and click hello check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="31d4a-154">Это инициирует задание восстановления, который можно просмотреть с hello **заданий** страницы.</span><span class="sxs-lookup"><span data-stu-id="31d4a-154">This will initiate a restore job that you can view by accessing hello **Jobs** page.</span></span> 
7. <span data-ttu-id="31d4a-155">После завершения восстановления hello, вы можете проверить, что hello содержимое томов заменено томами из резервной копии hello.</span><span class="sxs-lookup"><span data-stu-id="31d4a-155">After hello restore is complete, you can verify that hello contents of your volumes are replaced by volumes from hello backup.</span></span>

<span data-ttu-id="31d4a-156">![Доступно видео](./media/storsimple-restore-from-backup-set/Video_icon.png) **Доступно видео**</span><span class="sxs-lookup"><span data-stu-id="31d4a-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="31d4a-157">toowatch видео, в котором показано, как использовать клон hello и восстановить возможности StorSimple toorecover удалены файлы, нажмите кнопку [здесь](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="31d4a-157">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31d4a-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31d4a-158">Next steps</span></span>
* <span data-ttu-id="31d4a-159">Узнайте, каким образом слишком[томов StorSimple управление](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="31d4a-159">Learn how too[Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="31d4a-160">Узнайте, каким образом слишком[используйте hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="31d4a-160">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

