---
title: "Управление каталогом архивов StorSimple | Документация Майкрософт"
description: "В этой статье описывается, как с помощью страницы каталога резервного копирования для службы диспетчера устройств StorSimple получить список резервных наборов данных, а также выбрать и удалить ненужные."
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
ms.openlocfilehash: ac2577c6cd350d6d437d55e61ec73d954cb24893
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-your-backup-catalog"></a><span data-ttu-id="2f006-103">Использование службы диспетчера устройств StorSimple для управления каталогом резервного копирования</span><span class="sxs-lookup"><span data-stu-id="2f006-103">Use the StorSimple Device Manager service to manage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="2f006-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2f006-104">Overview</span></span>
<span data-ttu-id="2f006-105">На странице **Каталог резервного копирования** для службы диспетчера устройств StorSimple отображаются все резервные наборы данных, созданные при плановом или ручном резервном копировании.</span><span class="sxs-lookup"><span data-stu-id="2f006-105">The StorSimple Device Manager service **Backup Catalog** blade displays all the backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="2f006-106">Эта страница позволяет просмотреть все резервные копии для определенной политики резервного копирования или определенного тома, выбрать или удалить резервные копии или использовать резервную копию для восстановления или клонирования тома.</span><span class="sxs-lookup"><span data-stu-id="2f006-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

<span data-ttu-id="2f006-107">В этом учебнике описывается, как выбирать и удалять резервный набор данных.</span><span class="sxs-lookup"><span data-stu-id="2f006-107">This tutorial explains how to list, select, and delete a backup set.</span></span> <span data-ttu-id="2f006-108">Сведения о восстановлении устройства из архива см. в разделе [Восстановление тома StorSimple из резервного набора данных](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="2f006-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="2f006-109">Сведения о клонировании тома см. в разделе [Клонирование тома с помощью службы диспетчера StorSimple](storsimple-8000-clone-volume-u2.md).</span><span class="sxs-lookup"><span data-stu-id="2f006-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![Каталог резервного копирования](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="2f006-111">Колонка **Каталог резервного копирования** позволяет создать запрос, чтобы сузить выбор резервных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="2f006-111">The **Backup Catalog** blade provides a query to narrow your backup set selection.</span></span> <span data-ttu-id="2f006-112">Вы можете фильтровать полученные резервные наборы данных по следующим параметрам:</span><span class="sxs-lookup"><span data-stu-id="2f006-112">You can filter the backup sets that are retrieved, based on the following parameters:</span></span>

* <span data-ttu-id="2f006-113">**Устройство** — устройство, на котором был создан резервный набор данных.</span><span class="sxs-lookup"><span data-stu-id="2f006-113">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="2f006-114">**Том или политика резервного копирования** — выбор политики или тома, связанных с этим резервным набором данных.</span><span class="sxs-lookup"><span data-stu-id="2f006-114">**Backup policy or Volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="2f006-115">**От и до** — диапазон дат и времени создания резервного набора данных.</span><span class="sxs-lookup"><span data-stu-id="2f006-115">**From and To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="2f006-116">Затем отфильтрованные резервные наборы данных будут представлены в табличной форме на основе следующих атрибутов:</span><span class="sxs-lookup"><span data-stu-id="2f006-116">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="2f006-117">**Имя** — имя политики резервного копирования или тома, связанное с резервным набором данных.</span><span class="sxs-lookup"><span data-stu-id="2f006-117">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="2f006-118">**Размер** — фактический размер резервного набора данных.</span><span class="sxs-lookup"><span data-stu-id="2f006-118">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="2f006-119">**Создано** — дата и время создания резервных копий.</span><span class="sxs-lookup"><span data-stu-id="2f006-119">**Created On** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="2f006-120">**Тип** — наборы резервного копирования могут представлять собой локальные моментальные снимки или облачные моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="2f006-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="2f006-121">Локальный моментальный снимок — это резервная копия всех данных тома, которая хранится локально на устройстве, а облачный моментальный снимок — это резервная копия данных тома, хранящаяся в облаке.</span><span class="sxs-lookup"><span data-stu-id="2f006-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="2f006-122">Локальные моментальные снимки обеспечивают более быстрый доступ, а облачные моментальные снимки выбираются для обеспечения устойчивости данных.</span><span class="sxs-lookup"><span data-stu-id="2f006-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="2f006-123">**Инициировано** — резервные копии могут инициироваться автоматически по расписанию или вручную пользователем.</span><span class="sxs-lookup"><span data-stu-id="2f006-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="2f006-124">Для планирования резервного копирования можно использовать политику резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="2f006-124">You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="2f006-125">Кроме того, можно использовать параметр **Создать резервную копию** для резервного копирования вручную.</span><span class="sxs-lookup"><span data-stu-id="2f006-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="2f006-126">Создание списка резервных наборов данных для политики резервного копирования</span><span class="sxs-lookup"><span data-stu-id="2f006-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="2f006-127">Выполните следующие действия, чтобы создать список всех резервных копий для политики резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="2f006-127">Complete the following steps to list all the backups for a backup policy.</span></span>

#### <a name="to-list-backup-sets"></a><span data-ttu-id="2f006-128">Для создания списка резервных наборов данных</span><span class="sxs-lookup"><span data-stu-id="2f006-128">To list backup sets</span></span>
1. <span data-ttu-id="2f006-129">В службе диспетчера устройств StorSimple выберите **Каталог резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="2f006-129">Go to your StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="2f006-130">Отфильтруйте выбранные элементы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2f006-130">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="2f006-131">Укажите интервал времени.</span><span class="sxs-lookup"><span data-stu-id="2f006-131">Specify the time range.</span></span>
   2. <span data-ttu-id="2f006-132">Выберите подходящее устройство.</span><span class="sxs-lookup"><span data-stu-id="2f006-132">Select the appropriate device.</span></span>
   3. <span data-ttu-id="2f006-133">Установите фильтр по **политике резервного копирования**, чтобы просмотреть соответствующие резервные копии.</span><span class="sxs-lookup"><span data-stu-id="2f006-133">Filter by **Backup policy** to view the corresponding the backups.</span></span>
   3. <span data-ttu-id="2f006-134">В раскрывающемся списке политики резервного копирования выберите значение **Все**, чтобы получить полный список резервных копий на выбранном устройстве.</span><span class="sxs-lookup"><span data-stu-id="2f006-134">From the backup policy dropdown list, choose **All** to view all the backups on the selected device.</span></span>
   4. <span data-ttu-id="2f006-135">Щелкните **Применить**, чтобы выполнить этот запрос.</span><span class="sxs-lookup"><span data-stu-id="2f006-135">Click **Apply** to execute this query.</span></span>
      
      <span data-ttu-id="2f006-136">В списке резервных наборов данных должны отобразиться резервные копии, связанные с выбранной политикой резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="2f006-136">The backups associated with the selected backup policy should appear in the list of backup sets.</span></span>

      ![Переход в каталог резервного копирования](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="2f006-138">Выбор резервного набора данных</span><span class="sxs-lookup"><span data-stu-id="2f006-138">Select a backup set</span></span>
<span data-ttu-id="2f006-139">Чтобы выбрать резервный набор данных для тома или политики резервного копирования, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2f006-139">Complete the following steps to select a backup set for a volume or backup policy.</span></span>

#### <a name="to-select-a-backup-set"></a><span data-ttu-id="2f006-140">Для выбора резервного набора данных</span><span class="sxs-lookup"><span data-stu-id="2f006-140">To select a backup set</span></span>
1. <span data-ttu-id="2f006-141">В службе диспетчера устройств StorSimple выберите **Каталог резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="2f006-141">Go to your StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="2f006-142">Отфильтруйте выбранные элементы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2f006-142">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="2f006-143">Укажите интервал времени.</span><span class="sxs-lookup"><span data-stu-id="2f006-143">Specify the time range.</span></span> 
   2. <span data-ttu-id="2f006-144">Выберите подходящее устройство.</span><span class="sxs-lookup"><span data-stu-id="2f006-144">Select the appropriate device.</span></span> 
   3. <span data-ttu-id="2f006-145">В раскрывающемся списке выберите том или политику резервного копирования для нужной резервной копии.</span><span class="sxs-lookup"><span data-stu-id="2f006-145">Filter by volume or backup policy for the backup that you wish to select.</span></span>
   4. <span data-ttu-id="2f006-146">Щелкните **Применить**, чтобы выполнить этот запрос.</span><span class="sxs-lookup"><span data-stu-id="2f006-146">Click **Apply** to execute this query.</span></span>
      
      <span data-ttu-id="2f006-147">В списке резервных наборов данных должны отобразиться резервные копии, связанные с выбранным томом или политикой резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="2f006-147">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>

      ![Переход в каталог резервного копирования](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="2f006-149">Выберите и разверните резервный набор данных.</span><span class="sxs-lookup"><span data-stu-id="2f006-149">Select and expand a backup set.</span></span> <span data-ttu-id="2f006-150">Теперь вы увидите резервные наборы данных с разбивкой по томам, которые они содержат.</span><span class="sxs-lookup"><span data-stu-id="2f006-150">You can now see the backup sets broken down by the volumes that it contains.</span></span> <span data-ttu-id="2f006-151">Действия **Восстановить** и **Удалить** для резервного набора данных доступны в контекстном меню (правая кнопка мыши).</span><span class="sxs-lookup"><span data-stu-id="2f006-151">The **Restore** and **Delete** options are available via the context menu (right-click) for the backup set.</span></span> <span data-ttu-id="2f006-152">С выбранным резервным набором данных можно выполнить одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="2f006-152">You can perform either of these actions on the backup set that you selected.</span></span>

    ![Переход в каталог резервного копирования](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="2f006-154">Удаление резервного набора данных</span><span class="sxs-lookup"><span data-stu-id="2f006-154">Delete a backup set</span></span>
<span data-ttu-id="2f006-155">Удаление резервной копии, если больше не требуется хранить связанные с ней данные.</span><span class="sxs-lookup"><span data-stu-id="2f006-155">Delete a backup when you no longer wish to retain the data associated with it.</span></span> <span data-ttu-id="2f006-156">Чтобы удалить резервный набор данных, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="2f006-156">Perform the following steps to delete a backup set.</span></span>

#### <a name="to-delete-a-backup-set"></a><span data-ttu-id="2f006-157">Чтобы удалить резервный набор данных</span><span class="sxs-lookup"><span data-stu-id="2f006-157">To delete a backup set</span></span>
 <span data-ttu-id="2f006-158">В службе диспетчера устройств StorSimple выберите **Каталог резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="2f006-158">Go to your StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="2f006-159">Отфильтруйте выбранные элементы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2f006-159">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="2f006-160">Укажите интервал времени.</span><span class="sxs-lookup"><span data-stu-id="2f006-160">Specify the time range.</span></span> 
   2. <span data-ttu-id="2f006-161">Выберите подходящее устройство.</span><span class="sxs-lookup"><span data-stu-id="2f006-161">Select the appropriate device.</span></span> 
   3. <span data-ttu-id="2f006-162">В раскрывающемся списке выберите том или политику резервного копирования для нужной резервной копии.</span><span class="sxs-lookup"><span data-stu-id="2f006-162">Filter by volume or backup policy for the backup that you wish to select.</span></span>
   4. <span data-ttu-id="2f006-163">Щелкните **Применить**, чтобы выполнить этот запрос.</span><span class="sxs-lookup"><span data-stu-id="2f006-163">Click **Apply** to execute this query.</span></span>
      
      <span data-ttu-id="2f006-164">В списке резервных наборов данных должны отобразиться резервные копии, связанные с выбранным томом или политикой резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="2f006-164">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>

      ![Переход в каталог резервного копирования](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="2f006-166">Выберите и разверните резервный набор данных.</span><span class="sxs-lookup"><span data-stu-id="2f006-166">Select and expand a backup set.</span></span> <span data-ttu-id="2f006-167">Теперь вы увидите резервные наборы данных с разбивкой по томам, которые они содержат.</span><span class="sxs-lookup"><span data-stu-id="2f006-167">You can now see the backup sets broken down by the volumes that it contains.</span></span> <span data-ttu-id="2f006-168">Действия **Восстановить** и **Удалить** для резервного набора данных доступны в контекстном меню (правая кнопка мыши).</span><span class="sxs-lookup"><span data-stu-id="2f006-168">The **Restore** and **Delete** options are available via the context menu (right-click) for the backup set.</span></span> <span data-ttu-id="2f006-169">Щелкните выбранный резервный набор данных правой кнопкой мыши, а затем в контекстном меню выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="2f006-169">Right-click the selected backup set and from the context menu, select **Delete**.</span></span>

    ![Переход в каталог резервного копирования](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="2f006-171">Когда появится запрос на подтверждение, проверьте отображаемые сведения и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="2f006-171">When prompted for confirmation, review the displayed information and click **Delete**.</span></span> <span data-ttu-id="2f006-172">Выбранная резервная копия будет удалена без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="2f006-172">The selected backup is deleted permanently.</span></span>

    ![Переход в каталог резервного копирования](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="2f006-174">Во время выполнения удаления и его успешного завершения вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="2f006-174">You will be notified when the deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="2f006-175">После завершения удаления обновите запрос на этой странице.</span><span class="sxs-lookup"><span data-stu-id="2f006-175">After the deletion is done, refresh the query on this page.</span></span> <span data-ttu-id="2f006-176">Удаленный резервный набор данных больше не будет отображаться в списке резервных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="2f006-176">The deleted backup set will no longer appear in the list of backup sets.</span></span>

    ![Переход в каталог резервного копирования](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="2f006-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2f006-178">Next steps</span></span>
* <span data-ttu-id="2f006-179">Узнайте об использовании каталога резервного копирования [для восстановления устройства с помощью набора архивации](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="2f006-179">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="2f006-180">Узнайте, как [использовать службу диспетчера устройств StorSimple для администрирования устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="2f006-180">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

