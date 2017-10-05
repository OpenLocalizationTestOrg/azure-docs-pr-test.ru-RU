---
title: "Восстановление тома StorSimple из архива | Документация Майкрософт"
description: "Описание способов использования страницы каталога резервного копирования службы диспетчера StorSimple для восстановления тома StorSimple из резервного набора данных."
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
ms.openlocfilehash: 12484338f5b4d489604d70a657ef0992b6267297
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="c546c-103">Восстановление тома StorSimple из резервного набора данных</span><span class="sxs-lookup"><span data-stu-id="c546c-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="c546c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c546c-104">Overview</span></span>
<span data-ttu-id="c546c-105">Страница **Каталог резервного копирования** содержит все наборы резервных данных, созданные во время ручного или автоматического резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c546c-105">The **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="c546c-106">Эта страница позволяет просмотреть все резервные копии для определенной политики резервного копирования или определенного тома, выбрать или удалить резервные копии или использовать резервную копию для восстановления или клонирования тома.</span><span class="sxs-lookup"><span data-stu-id="c546c-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

 ![Страница каталога резервного копирования](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="c546c-108">В этом учебнике объясняется, как использовать страницу **Каталог архивов** для восстановления тома на устройстве из набора архивации.</span><span class="sxs-lookup"><span data-stu-id="c546c-108">This tutorial explains how to use the **Backup Catalog** page to restore a volume on your device from a backup set.</span></span>

## <a name="how-to-use-the-backup-catalog"></a><span data-ttu-id="c546c-109">Как использовать каталог резервных копий</span><span class="sxs-lookup"><span data-stu-id="c546c-109">How to use the backup catalog</span></span>
<span data-ttu-id="c546c-110">Страница **Каталог резервного копирования** позволяет создать запрос, который поможет сузить спектр выбранных резервных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="c546c-110">The **Backup Catalog** page provides a query that helps you to narrow your backup set selection.</span></span> <span data-ttu-id="c546c-111">Вы можете фильтровать полученные резервные наборы данных по следующим параметрам:</span><span class="sxs-lookup"><span data-stu-id="c546c-111">You can filter the backup sets that are retrieved based on the following parameters:</span></span>

* <span data-ttu-id="c546c-112">**Устройство** — устройство, на котором был создан резервный набор данных.</span><span class="sxs-lookup"><span data-stu-id="c546c-112">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="c546c-113">**Политика архивации** или **том** — политика или том архивации, связанные с этим набором архивации.</span><span class="sxs-lookup"><span data-stu-id="c546c-113">**Backup policy** or **volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="c546c-114">**От** и **До** — диапазон дат и времени создания набора архивации.</span><span class="sxs-lookup"><span data-stu-id="c546c-114">**From** and **To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="c546c-115">Затем отфильтрованные резервные наборы данных будут представлены в табличной форме на основе следующих атрибутов:</span><span class="sxs-lookup"><span data-stu-id="c546c-115">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="c546c-116">**Имя** — имя политики резервного копирования или тома, связанное с резервным набором данных.</span><span class="sxs-lookup"><span data-stu-id="c546c-116">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="c546c-117">**Размер** — фактический размер резервного набора данных.</span><span class="sxs-lookup"><span data-stu-id="c546c-117">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="c546c-118">**Создано** — дата и время, когда были созданы резервные копии.</span><span class="sxs-lookup"><span data-stu-id="c546c-118">**Created on** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="c546c-119">**Тип** — наборы резервного копирования могут представлять собой локальные моментальные снимки или облачные моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="c546c-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="c546c-120">Локальный моментальный снимок — это резервная копия всех данных тома, которая хранится локально на устройстве, а облачный моментальный снимок — это резервная копия данных тома, хранящаяся в облаке.</span><span class="sxs-lookup"><span data-stu-id="c546c-120">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="c546c-121">Локальные моментальные снимки обеспечивают более быстрый доступ, а облачные моментальные снимки выбираются для обеспечения устойчивости данных.</span><span class="sxs-lookup"><span data-stu-id="c546c-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="c546c-122">**Инициировано** — резервные копии могут инициироваться автоматически по расписанию или вручную пользователем.</span><span class="sxs-lookup"><span data-stu-id="c546c-122">**Initiated by** – The backups can be initiated automatically according to a schedule or manually by a user.</span></span> <span data-ttu-id="c546c-123">(Для планирования резервного копирования можно использовать политику резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c546c-123">(You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="c546c-124">Кроме того, можно использовать параметр **Создать резервную копию** для резервного копирования в интерактивном режиме.)</span><span class="sxs-lookup"><span data-stu-id="c546c-124">Alternatively, you can use the **Take backup** option to take an interactive backup.)</span></span>

## <a name="how-to-restore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="c546c-125">Восстановление тома StorSimple из резервной копии</span><span class="sxs-lookup"><span data-stu-id="c546c-125">How to restore your StorSimple volume from a backup</span></span>
<span data-ttu-id="c546c-126">С помощью страницы **Каталог резервного копирования** можно восстановить том устройства StorSimple из определенной резервной копии.</span><span class="sxs-lookup"><span data-stu-id="c546c-126">You can use the **Backup Catalog** page to restore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="c546c-127">Восстановление из резервной копии приведет к замене существующих томов томами из резервной копии.</span><span class="sxs-lookup"><span data-stu-id="c546c-127">Restoring from a backup will replace the existing volumes from the backup.</span></span> <span data-ttu-id="c546c-128">Это может привести к потере всех данных, которые были записаны после резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c546c-128">This may cause the loss of any data that was written after the backup was taken.</span></span>
> 
> 

<span data-ttu-id="c546c-129">Прежде чем начать восстановление тома, убедитесь, что он отключен.</span><span class="sxs-lookup"><span data-stu-id="c546c-129">Before you initiate a restore on a volume, ensure that the volume is offline.</span></span> <span data-ttu-id="c546c-130">Сначала следует отключить том на узле, а затем на устройстве.</span><span class="sxs-lookup"><span data-stu-id="c546c-130">You will need to take the volume offline on the host first and then the device.</span></span> <span data-ttu-id="c546c-131">Следуйте указаниям по [отключению тома](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="c546c-131">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="c546c-132">Чтобы восстановить том из набора архивации, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="c546c-132">Perform the following steps to restore a volume from a backup set.</span></span>

### <a name="to-restore-from-a-backup-set"></a><span data-ttu-id="c546c-133">Восстановление из резервного набора данных</span><span class="sxs-lookup"><span data-stu-id="c546c-133">To restore from a backup set</span></span>
1. <span data-ttu-id="c546c-134">На странице службы диспетчера StorSimple щелкните вкладку **Каталог резервных копий** .</span><span class="sxs-lookup"><span data-stu-id="c546c-134">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
   
    ![Каталог резервного копирования](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="c546c-136">Выберите резервный набор данных следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c546c-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="c546c-137">Выберите подходящее устройство.</span><span class="sxs-lookup"><span data-stu-id="c546c-137">Select the appropriate device.</span></span>
   2. <span data-ttu-id="c546c-138">В раскрывающемся списке выберите том или политику резервного копирования для той резервной копии, которую нужно выбрать.</span><span class="sxs-lookup"><span data-stu-id="c546c-138">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="c546c-139">Укажите интервал времени.</span><span class="sxs-lookup"><span data-stu-id="c546c-139">Specify the time range.</span></span>
   4. <span data-ttu-id="c546c-140">Щелкните значок с изображением флажка </span><span class="sxs-lookup"><span data-stu-id="c546c-140">Click the check icon</span></span> ![значок галочки](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="c546c-142">, чтобы выполнить этот запрос.</span><span class="sxs-lookup"><span data-stu-id="c546c-142">to execute this query.</span></span>
      
      <span data-ttu-id="c546c-143">В списке резервных наборов данных должны отобразиться резервные копии, связанные с выбранным томом или политикой резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c546c-143">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="c546c-144">Разверните резервный набор данных для просмотра связанных томов.</span><span class="sxs-lookup"><span data-stu-id="c546c-144">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="c546c-145">Перед восстановлением эти тома необходимо отключить на узле и устройстве.</span><span class="sxs-lookup"><span data-stu-id="c546c-145">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="c546c-146">Следуйте указаниям по [отключению тома](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="c546c-146">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="c546c-147">Прежде чем отключать том на устройстве, сначала отключите его на узле.</span><span class="sxs-lookup"><span data-stu-id="c546c-147">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="c546c-148">Если тома на узле не переведены в автономный режим, это может привести к повреждению данных.</span><span class="sxs-lookup"><span data-stu-id="c546c-148">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="c546c-149">Выберите набор архивации.</span><span class="sxs-lookup"><span data-stu-id="c546c-149">Select a backup set.</span></span> <span data-ttu-id="c546c-150">В нижней части страницы нажмите кнопку **Восстановить** .</span><span class="sxs-lookup"><span data-stu-id="c546c-150">Click **Restore** at the bottom of the page.</span></span>
5. <span data-ttu-id="c546c-151">После этого введите подтверждение для применения этих исправлений.</span><span class="sxs-lookup"><span data-stu-id="c546c-151">You will be prompted for confirmation.</span></span> 
   
    ![Страница подтверждения](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="c546c-153">Проверьте информацию о восстановлении и щелкните значок флажка ![значок галочки](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="c546c-153">Review the restore information and click the check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="c546c-154">Запустится задание восстановления, которое можно просмотреть на странице **Задания** .</span><span class="sxs-lookup"><span data-stu-id="c546c-154">This will initiate a restore job that you can view by accessing the **Jobs** page.</span></span> 
7. <span data-ttu-id="c546c-155">После завершения восстановления можно убедиться, что содержимое томов заменено томами из резервной копии.</span><span class="sxs-lookup"><span data-stu-id="c546c-155">After the restore is complete, you can verify that the contents of your volumes are replaced by volumes from the backup.</span></span>

<span data-ttu-id="c546c-156">![Доступно видео](./media/storsimple-restore-from-backup-set/Video_icon.png) **Доступно видео**</span><span class="sxs-lookup"><span data-stu-id="c546c-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="c546c-157">Чтобы посмотреть видео о том, как использовать функции клонирования и восстановления в StorSimple для восстановления удаленных файлов, щелкните [здесь](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="c546c-157">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c546c-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c546c-158">Next steps</span></span>
* <span data-ttu-id="c546c-159">Узнайте об [управлении томами StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="c546c-159">Learn how to [Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="c546c-160">Узнайте об [использовании службы StorSimple Manager для администрирования устройства StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c546c-160">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

