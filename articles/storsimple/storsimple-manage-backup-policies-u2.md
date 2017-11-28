---
title: "Управление политиками архивации StorSimple | Документация Майкрософт"
description: "Объясняет, как использовать службу диспетчера StorSimple для создания резервных копий, созданных вручную, расписания снятия резервных копий и срока хранения резервных копий, а также для управления ими."
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
ms.openlocfilehash: 5448247428ab96887470c6b53f7a9b3dcd9238f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-backup-policies-update-2"></a><span data-ttu-id="b2bd7-103">Использование службы диспетчера StorSimple для управления политиками архивации (обновление 2)</span><span class="sxs-lookup"><span data-stu-id="b2bd7-103">Use the StorSimple Manager service to manage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="b2bd7-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b2bd7-104">Overview</span></span>
<span data-ttu-id="b2bd7-105">В данном учебнике рассказывается, как на странице **Политики архивации** службы диспетчера StorSimple управлять процессами архивации и хранения резервных копий для томов StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="b2bd7-106">Кроме того, в нем описан способ выполнения архивации вручную.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="b2bd7-107">При архивации тома можно создать его локальный или облачный моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="b2bd7-108">При архивации локально закрепленного тома рекомендуется указать облачный моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="b2bd7-109">Создание большого числа локальных моментальных снимков локально закрепленных томов в сочетании с набором данных с большим оттоком приведет к ситуации, в которой локальное пространство может быстро заполниться.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="b2bd7-110">Если вы решите создавать локальные моментальные снимки, мы рекомендуем создавать меньше ежедневных моментальных снимков, чтобы архивировать самое последнее состояние, сохранять их в течение дня, а затем удалять.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="b2bd7-111">При создании облачного моментального снимка локально закрепленного тома в облако копируются только измененные данные, где они дедуплицируются и сжимаются.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span></span> 

## <a name="the-backup-policies-page"></a><span data-ttu-id="b2bd7-112">Страница «Политики архивации»</span><span class="sxs-lookup"><span data-stu-id="b2bd7-112">The Backup Policies page</span></span>
<span data-ttu-id="b2bd7-113">На странице **Политики архивации** можно управлять политиками архивации и планировать создание локальных и облачных моментальных копий.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-113">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="b2bd7-114">(Политики архивации используются для настройки расписаний архивации и хранения резервных копий для коллекции томов). Политики архивации позволяют делать снимок нескольких томов одновременно.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-114">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="b2bd7-115">Это означает, что резервные копии, созданные политикой архивации, будут отказоустойчивыми.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-115">This means that the backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="b2bd7-116">На странице **Политики архивации** отображаются политики архивации, их типы, сопоставленные тома, количество хранимых резервных копий и переключатели для включения этих политик.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-116">The **Backup Policies** page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span></span>

<span data-ttu-id="b2bd7-117">Кроме того, на странице **Политики архивации** можно отфильтровать имеющиеся политики архивации по одному или нескольким указанным ниже полям.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-117">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="b2bd7-118">**Имя политики** — имя, сопоставленное с политикой.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-118">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="b2bd7-119">Ниже перечислены возможные типы политик.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-119">The different types of policies include:</span></span>
  
  * <span data-ttu-id="b2bd7-120">Запланированные политики, которые явно созданы пользователем.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-120">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="b2bd7-121">Автоматические политики, которые создаются, если при создании тома был включен параметр архивации тома по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-121">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span></span> <span data-ttu-id="b2bd7-122">Названия этих политик выглядят следующим образом: *ИмяТома*_Default, где *ИмяТома* — это имя тома StorSimple, заданное пользователем на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-122">These policies are named as *VolumeName*_Default where *VolumeName* refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span></span> <span data-ttu-id="b2bd7-123">При использовании автоматических политик облачные моментальные снимки создаются ежедневно, начиная c 22:30 по настроенному в устройстве времени.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-123">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="b2bd7-124">Импортированные политики, изначально созданные в диспетчере моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-124">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="b2bd7-125">У них имеется тег, описывающий узел диспетчера моментальных снимков StorSimple, из которого импортированы политики.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-125">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>
* <span data-ttu-id="b2bd7-126">**Тома** — тома, сопоставленные с политикой.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-126">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="b2bd7-127">При создании резервных копий все тома, сопоставленные с политикой архивации, будут объединены в одну группу.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-127">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="b2bd7-128">**Последняя успешная архивация** — дата и время последней успешной архивации, выполненной с помощью политики.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-128">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="b2bd7-129">**Следующая архивация** — дата и время следующей запланированной архивации, которая будет запущена политикой.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-129">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="b2bd7-130">**Расписания** — количество расписаний, сопоставленных с политикой архивации.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-130">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="b2bd7-131">Ниже перечислены часто используемые операции, которые можно выполнить на этой странице.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-131">The frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="b2bd7-132">Добавление политики архивации</span><span class="sxs-lookup"><span data-stu-id="b2bd7-132">Add a backup policy</span></span> 
* <span data-ttu-id="b2bd7-133">Добавление или изменение расписания</span><span class="sxs-lookup"><span data-stu-id="b2bd7-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="b2bd7-134">Удаление политики архивации</span><span class="sxs-lookup"><span data-stu-id="b2bd7-134">Delete a backup policy</span></span> 
* <span data-ttu-id="b2bd7-135">Создание резервной копии вручную</span><span class="sxs-lookup"><span data-stu-id="b2bd7-135">Take a manual backup</span></span> 
* <span data-ttu-id="b2bd7-136">Создание пользовательской политики архивации с несколькими томами и расписаниями</span><span class="sxs-lookup"><span data-stu-id="b2bd7-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="b2bd7-137">Добавление политики архивации</span><span class="sxs-lookup"><span data-stu-id="b2bd7-137">Add a backup policy</span></span>
<span data-ttu-id="b2bd7-138">Добавление политики архивации для автоматического планирования архивации.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-138">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="b2bd7-139">Чтобы добавить политику архивации для устройства StorSimple, выполните указанные ниже действия на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-139">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="b2bd7-140">После добавления политики можно задать расписание (см. раздел [Добавление или изменение расписания](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="b2bd7-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="b2bd7-141">![Доступный видеоролик](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Доступный видеоролик**</span><span class="sxs-lookup"><span data-stu-id="b2bd7-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="b2bd7-142">Чтобы просмотреть видео о создании локальной или облачной политики архивации, щелкните [здесь](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="b2bd7-142">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="b2bd7-143">Добавление или изменение расписания</span><span class="sxs-lookup"><span data-stu-id="b2bd7-143">Add or modify a schedule</span></span>
<span data-ttu-id="b2bd7-144">Вы можете добавить или изменить расписание, присоединенное к существующей политике архивации на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-144">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="b2bd7-145">Чтобы создать или изменить расписание, выполните указанные ниже действия на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-145">Perform the following steps in the Azure classic portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="b2bd7-146">Удаление политики архивации</span><span class="sxs-lookup"><span data-stu-id="b2bd7-146">Delete a backup policy</span></span>
<span data-ttu-id="b2bd7-147">Чтобы удалить политику архивации на устройстве StorSimple, выполните указанные ниже действия на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-147">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="b2bd7-148">Создание резервной копии вручную</span><span class="sxs-lookup"><span data-stu-id="b2bd7-148">Take a manual backup</span></span>
<span data-ttu-id="b2bd7-149">Чтобы создать резервную копию по запросу (вручную) для одного тома, выполните указанные ниже действия на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-149">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="b2bd7-150">Создание пользовательской политики архивации с несколькими томами и расписаниями</span><span class="sxs-lookup"><span data-stu-id="b2bd7-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="b2bd7-151">Чтобы создать пользовательскую политику архивации с несколькими томами и расписаниями, выполните указанные ниже действия на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b2bd7-151">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="b2bd7-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b2bd7-152">Next steps</span></span>
<span data-ttu-id="b2bd7-153">Узнайте больше об [использовании службы диспетчера StorSimple для администрирования устройства StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="b2bd7-153">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

