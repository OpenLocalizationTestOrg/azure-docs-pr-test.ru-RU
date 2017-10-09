---
title: "политики резервного копирования, серии StorSimple 8000 aaaManage | Документы Microsoft"
description: "Объясняется, как можно использовать toocreate службы диспетчера StorSimple устройство hello и управлять вручную резервных копий, расписания резервного копирования и хранения резервных копий на устройства серии StorSimple 8000."
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a><span data-ttu-id="70832-103">Использовать службу диспетчера StorSimple устройство hello политики резервного копирования Azure toomanage портала</span><span class="sxs-lookup"><span data-stu-id="70832-103">Use hello StorSimple Device Manager service in Azure portal toomanage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="70832-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="70832-104">Overview</span></span>

<span data-ttu-id="70832-105">В этом учебнике описано, как toouse hello службы диспетчера StorSimple устройство **политика архивации** процессы резервного копирования toocontrol колонки и хранения резервных копий для тома StorSimple.</span><span class="sxs-lookup"><span data-stu-id="70832-105">This tutorial explains how toouse hello StorSimple Device Manager service **Backup policy** blade toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="70832-106">В нем также рассматриваются как toocomplete резервной копии вручную.</span><span class="sxs-lookup"><span data-stu-id="70832-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="70832-107">При создании резервной копии тома, вы можете toocreate локальный моментальный снимок или облачный моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="70832-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="70832-108">При архивации локально закрепленного тома рекомендуется указать облачный моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="70832-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="70832-109">Создание большого числа локальных моментальных снимков локально закрепленных томов в сочетании с набором данных с большим оттоком приведет к ситуации, в которой локальное пространство может быстро заполниться.</span><span class="sxs-lookup"><span data-stu-id="70832-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="70832-110">При выборе tootake локальные моментальные снимки, мы рекомендуем занимают последнее состояние hello меньшее число ежедневных tooback моментальные снимки, сохранять их в день, а затем удалите их.</span><span class="sxs-lookup"><span data-stu-id="70832-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="70832-111">Можно сделать снимок облачного локально закрепленного тома, копируются только hello изменен данных toohello облака, где она дедупликации и сжатия.</span><span class="sxs-lookup"><span data-stu-id="70832-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span>

## <a name="hello-backup-policy-blade"></a><span data-ttu-id="70832-112">Hello колонку политики резервного копирования</span><span class="sxs-lookup"><span data-stu-id="70832-112">hello Backup policy blade</span></span>

<span data-ttu-id="70832-113">Hello **политика архивации** колонку для устройства StorSimple позволяет toomanage политики резервного копирования и расписание локальных и облачных моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="70832-113">hello **Backup policy** blade for your StorSimple device allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="70832-114">Политики резервного копирования не используется tooconfigure расписания резервного копирования и хранения резервной копии для набора томов.</span><span class="sxs-lookup"><span data-stu-id="70832-114">Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="70832-115">Политики резервного копирования, обеспечивают tootake моментальный снимок нескольких томах одновременно.</span><span class="sxs-lookup"><span data-stu-id="70832-115">Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="70832-116">Это означает, что hello резервных копий, созданных политику резервного копирования копии на момент аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="70832-116">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="70832-117">Табличный список политик резервного копирования Hello также позволяет вам toofilter hello существующие политики резервного копирования одним или несколькими hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="70832-117">hello backup policies tabular listing also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="70832-118">**Имя политики** — hello имя, связанное с политикой hello.</span><span class="sxs-lookup"><span data-stu-id="70832-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="70832-119">Hello различные типы политик:</span><span class="sxs-lookup"><span data-stu-id="70832-119">hello different types of policies include:</span></span>

  * <span data-ttu-id="70832-120">Запланированные политики, которые явно создаются пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="70832-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="70832-121">Импорт политики, которые были созданы в hello диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="70832-121">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="70832-122">Они имеют метки, описывающие узел диспетчера моментальных снимков StorSimple hello, hello политики были импортированы.</span><span class="sxs-lookup"><span data-stu-id="70832-122">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="70832-123">Политики резервного копирования автоматически или по умолчанию больше не включены одновременно hello создания тома.</span><span class="sxs-lookup"><span data-stu-id="70832-123">Automatic or default backup policies are no longer enabled at hello time of volume creation.</span></span>

* <span data-ttu-id="70832-124">**Последней успешной архивации** — hello даты и времени hello последней успешной резервной копии, сделанной с этой политикой.</span><span class="sxs-lookup"><span data-stu-id="70832-124">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="70832-125">**Следующая резервная копия** — hello Дата и время hello следующего запланированного резервного копирования, будет инициировано этой политикой.</span><span class="sxs-lookup"><span data-stu-id="70832-125">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="70832-126">**Тома** — hello тома, связанные с политикой hello.</span><span class="sxs-lookup"><span data-stu-id="70832-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="70832-127">Все тома hello, связанные с политикой резервного копирования, группируются вместе при создании резервных копий.</span><span class="sxs-lookup"><span data-stu-id="70832-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="70832-128">**Расписания** — число расписаний, связанных с политикой резервного копирования hello hello.</span><span class="sxs-lookup"><span data-stu-id="70832-128">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="70832-129">часто используемые Hello операции, которые можно выполнять для политики резервного копирования являются:</span><span class="sxs-lookup"><span data-stu-id="70832-129">hello frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="70832-130">Добавление политики архивации</span><span class="sxs-lookup"><span data-stu-id="70832-130">Add a backup policy</span></span>
* <span data-ttu-id="70832-131">Добавление или изменение расписания</span><span class="sxs-lookup"><span data-stu-id="70832-131">Add or modify a schedule</span></span>
* <span data-ttu-id="70832-132">добавление или удаление тома;</span><span class="sxs-lookup"><span data-stu-id="70832-132">Add or remove a volume</span></span>
* <span data-ttu-id="70832-133">Удаление политики архивации</span><span class="sxs-lookup"><span data-stu-id="70832-133">Delete a backup policy</span></span>
* <span data-ttu-id="70832-134">Создание резервной копии вручную</span><span class="sxs-lookup"><span data-stu-id="70832-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="70832-135">Добавление политики архивации</span><span class="sxs-lookup"><span data-stu-id="70832-135">Add a backup policy</span></span>

<span data-ttu-id="70832-136">Добавьте расписание tooautomatically политику резервного копирования резервных копий.</span><span class="sxs-lookup"><span data-stu-id="70832-136">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="70832-137">При первоначальном создании тома для него не существует политики резервного копирования по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="70832-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="70832-138">Требуется tooadd и назначить тома данных tooprotect политику резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="70832-138">You need tooadd and assign a backup policy tooprotect volume data.</span></span>

<span data-ttu-id="70832-139">Выполните следующие шаги в hello Azure портала tooadd политику резервного копирования для устройства StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="70832-139">Perform hello following steps in hello Azure portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="70832-140">После добавления hello политики, можно задать расписание (см. [добавить или изменить расписание](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="70832-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="70832-141">Добавление или изменение расписания</span><span class="sxs-lookup"><span data-stu-id="70832-141">Add or modify a schedule</span></span>

<span data-ttu-id="70832-142">Можно добавить или изменить расписание, существует политика резервного копирования вложенного tooan на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="70832-142">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="70832-143">Выполните следующие шаги в hello Azure портала tooadd hello или изменение расписания.</span><span class="sxs-lookup"><span data-stu-id="70832-143">Perform hello following steps in hello Azure portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="70832-144">добавление или удаление тома;</span><span class="sxs-lookup"><span data-stu-id="70832-144">Add or remove a volume</span></span>

<span data-ttu-id="70832-145">Можно добавить или удалить том, назначенных tooa политику резервного копирования на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="70832-145">You can add or remove a volume assigned tooa backup policy on your StorSimple device.</span></span> <span data-ttu-id="70832-146">Выполните следующие шаги в hello Azure портала tooadd hello или удалить том.</span><span class="sxs-lookup"><span data-stu-id="70832-146">Perform hello following steps in hello Azure portal tooadd or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="70832-147">Удаление политики архивации</span><span class="sxs-lookup"><span data-stu-id="70832-147">Delete a backup policy</span></span>

<span data-ttu-id="70832-148">Выполните следующие действия, описанные в hello Azure портала toodelete политику резервного копирования на устройстве StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="70832-148">Perform hello following steps in hello Azure portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="70832-149">Создание резервной копии вручную</span><span class="sxs-lookup"><span data-stu-id="70832-149">Take a manual backup</span></span>

<span data-ttu-id="70832-150">Выполните следующие шаги в hello Azure портала toocreate по требованию (вручную) резервного копирования для одного тома hello.</span><span class="sxs-lookup"><span data-stu-id="70832-150">Perform hello following steps in hello Azure portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="70832-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="70832-151">Next steps</span></span>

<span data-ttu-id="70832-152">Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="70832-152">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

