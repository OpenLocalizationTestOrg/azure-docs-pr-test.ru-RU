---
title: "aaaManage политик резервного копирования StorSimple | Документы Microsoft"
description: "Объясняется, как можно использовать toocreate службы диспетчера StorSimple hello и управлять вручную резервных копий, расписания резервного копирования и хранения резервных копий."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 7b01f29a8d8a096d9890c8406557021317b9baff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a><span data-ttu-id="e73df-103">Используйте hello StorSimple Manager службы toomanage политики резервного копирования (обновление 2)</span><span class="sxs-lookup"><span data-stu-id="e73df-103">Use hello StorSimple Manager service toomanage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="e73df-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="e73df-104">Overview</span></span>
<span data-ttu-id="e73df-105">В этом учебнике описано, как toouse hello в службе StorSimple Manager **политики резервного копирования** toocontrol процессы резервного копирования и хранения резервных копий для тома StorSimple страницы.</span><span class="sxs-lookup"><span data-stu-id="e73df-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="e73df-106">В нем также рассматриваются как toocomplete резервной копии вручную.</span><span class="sxs-lookup"><span data-stu-id="e73df-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="e73df-107">При создании резервной копии тома, вы можете toocreate локальный моментальный снимок или облачный моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="e73df-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="e73df-108">При архивации локально закрепленного тома рекомендуется указать облачный моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="e73df-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="e73df-109">Создание большого числа локальных моментальных снимков локально закрепленных томов в сочетании с набором данных с большим оттоком приведет к ситуации, в которой локальное пространство может быстро заполниться.</span><span class="sxs-lookup"><span data-stu-id="e73df-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="e73df-110">При выборе tootake локальные моментальные снимки, мы рекомендуем занимают последнее состояние hello меньшее число ежедневных tooback моментальные снимки, сохранять их в день, а затем удалите их.</span><span class="sxs-lookup"><span data-stu-id="e73df-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="e73df-111">Можно сделать снимок облачного локально закрепленного тома, копируются только hello изменен данных toohello облака, где она дедупликации и сжатия.</span><span class="sxs-lookup"><span data-stu-id="e73df-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span> 

## <a name="hello-backup-policies-page"></a><span data-ttu-id="e73df-112">Страница приветствия политики резервного копирования</span><span class="sxs-lookup"><span data-stu-id="e73df-112">hello Backup Policies page</span></span>
<span data-ttu-id="e73df-113">Hello **политики резервного копирования** страница позволяет toomanage политики резервного копирования и расписание локальных и облачных моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="e73df-113">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="e73df-114">(Политики резервного копирования не используется tooconfigure расписания резервного копирования и хранения резервной копии для набора томов). Политики резервного копирования, обеспечивают tootake моментальный снимок нескольких томах одновременно.</span><span class="sxs-lookup"><span data-stu-id="e73df-114">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="e73df-115">Это означает, что hello резервных копий, созданных политику резервного копирования копии на момент аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="e73df-115">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="e73df-116">Hello **политики резервного копирования** странице перечислены hello политики резервного копирования, их типы, hello связанные тома, количество сохраняемых резервных копий hello и hello параметр tooenable эти политики.</span><span class="sxs-lookup"><span data-stu-id="e73df-116">hello **Backup Policies** page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="e73df-117">Hello **политики резервного копирования** также можно toofilter hello существующие политики резервного копирования по одному или нескольким hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="e73df-117">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="e73df-118">**Имя политики** — hello имя, связанное с политикой hello.</span><span class="sxs-lookup"><span data-stu-id="e73df-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="e73df-119">Hello различные типы политик:</span><span class="sxs-lookup"><span data-stu-id="e73df-119">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="e73df-120">Запланированные политики, которые явно создаются пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="e73df-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="e73df-121">Автоматические политики, которые создаются при включении hello резервное копирование по умолчанию для этого параметра том на время создания тома hello.</span><span class="sxs-lookup"><span data-stu-id="e73df-121">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="e73df-122">Эти политики именуются как *VolumeName*_Default где *VolumeName* относится имя toohello hello тома StorSimple, настроенного пользователем hello в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e73df-122">These policies are named as *VolumeName*_Default where *VolumeName* refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="e73df-123">Hello автоматические политики выполняют ежедневные облачные моментальные снимки, начиная с временем устройства 22:30.</span><span class="sxs-lookup"><span data-stu-id="e73df-123">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="e73df-124">Импорт политики, которые были созданы в hello диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e73df-124">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="e73df-125">Они имеют метки, описывающие узел диспетчера моментальных снимков StorSimple hello, hello политики были импортированы.</span><span class="sxs-lookup"><span data-stu-id="e73df-125">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="e73df-126">**Тома** — hello тома, связанные с политикой hello.</span><span class="sxs-lookup"><span data-stu-id="e73df-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="e73df-127">Все тома hello, связанные с политикой резервного копирования, группируются вместе при создании резервных копий.</span><span class="sxs-lookup"><span data-stu-id="e73df-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="e73df-128">**Последней успешной архивации** — hello даты и времени hello последней успешной резервной копии, сделанной с этой политикой.</span><span class="sxs-lookup"><span data-stu-id="e73df-128">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="e73df-129">**Следующая резервная копия** — hello Дата и время hello следующего запланированного резервного копирования, будет инициировано этой политикой.</span><span class="sxs-lookup"><span data-stu-id="e73df-129">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="e73df-130">**Расписания** — число расписаний, связанных с политикой резервного копирования hello hello.</span><span class="sxs-lookup"><span data-stu-id="e73df-130">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="e73df-131">Hello часто используемых операций, которые можно выполнять на этой странице перечислены.</span><span class="sxs-lookup"><span data-stu-id="e73df-131">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="e73df-132">Добавление политики архивации</span><span class="sxs-lookup"><span data-stu-id="e73df-132">Add a backup policy</span></span> 
* <span data-ttu-id="e73df-133">Добавление или изменение расписания</span><span class="sxs-lookup"><span data-stu-id="e73df-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="e73df-134">Удаление политики архивации</span><span class="sxs-lookup"><span data-stu-id="e73df-134">Delete a backup policy</span></span> 
* <span data-ttu-id="e73df-135">Создание резервной копии вручную</span><span class="sxs-lookup"><span data-stu-id="e73df-135">Take a manual backup</span></span> 
* <span data-ttu-id="e73df-136">Создание пользовательской политики архивации с несколькими томами и расписаниями</span><span class="sxs-lookup"><span data-stu-id="e73df-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="e73df-137">Добавление политики архивации</span><span class="sxs-lookup"><span data-stu-id="e73df-137">Add a backup policy</span></span>
<span data-ttu-id="e73df-138">Добавьте расписание tooautomatically политику резервного копирования резервных копий.</span><span class="sxs-lookup"><span data-stu-id="e73df-138">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="e73df-139">Выполните следующие шаги в hello Azure классического портала tooadd политику резервного копирования для устройства StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="e73df-139">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="e73df-140">После добавления hello политики, можно задать расписание (см. [добавить или изменить расписание](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="e73df-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="e73df-141">![Доступно видео](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Доступно видео**</span><span class="sxs-lookup"><span data-stu-id="e73df-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="e73df-142">Нажмите кнопку toowatch видео, в котором показано, как политика, архивации toocreate локальной или облачной [здесь](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="e73df-142">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="e73df-143">Добавление или изменение расписания</span><span class="sxs-lookup"><span data-stu-id="e73df-143">Add or modify a schedule</span></span>
<span data-ttu-id="e73df-144">Можно добавить или изменить расписание, существует политика резервного копирования вложенного tooan на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e73df-144">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="e73df-145">Выполните следующие шаги в hello Azure классического портала tooadd hello или изменение расписания.</span><span class="sxs-lookup"><span data-stu-id="e73df-145">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="e73df-146">Удаление политики архивации</span><span class="sxs-lookup"><span data-stu-id="e73df-146">Delete a backup policy</span></span>
<span data-ttu-id="e73df-147">Выполните следующие действия, описанные в hello Azure классического портала toodelete политику резервного копирования на устройстве StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="e73df-147">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="e73df-148">Создание резервной копии вручную</span><span class="sxs-lookup"><span data-stu-id="e73df-148">Take a manual backup</span></span>
<span data-ttu-id="e73df-149">Выполните следующие шаги в hello Azure классического портала toocreate по требованию (вручную) резервного копирования для одного тома hello.</span><span class="sxs-lookup"><span data-stu-id="e73df-149">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="e73df-150">Создание пользовательской политики архивации с несколькими томами и расписаниями</span><span class="sxs-lookup"><span data-stu-id="e73df-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="e73df-151">Выполните следующие шаги в hello Azure классического портала toocreate настраиваемую политику резервного копирования с несколькими томами и расписаниями hello.</span><span class="sxs-lookup"><span data-stu-id="e73df-151">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="e73df-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e73df-152">Next steps</span></span>
<span data-ttu-id="e73df-153">Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e73df-153">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

