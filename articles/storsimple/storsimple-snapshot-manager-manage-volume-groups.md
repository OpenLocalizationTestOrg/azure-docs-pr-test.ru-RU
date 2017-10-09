---
title: "группы томов диспетчера моментальных снимков aaaStorSimple | Документы Microsoft"
description: "Описывается порядок toouse hello toocreate оснастку консоли MMC диспетчера моментальных снимков StorSimple и управление группами томов."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a><span data-ttu-id="eadcf-103">Использование диспетчера моментальных снимков StorSimple toocreate и управление ими группы томов</span><span class="sxs-lookup"><span data-stu-id="eadcf-103">Use StorSimple Snapshot Manager toocreate and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="eadcf-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="eadcf-104">Overview</span></span>
<span data-ttu-id="eadcf-105">Можно использовать hello **группы томов** узел на hello **область** группы toovolume тома tooassign области, просмотр сведений о группе томов, запланировать резервное копирование и изменения групп томов.</span><span class="sxs-lookup"><span data-stu-id="eadcf-105">You can use hello **Volume Groups** node on hello **Scope** pane tooassign volumes toovolume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span>

<span data-ttu-id="eadcf-106">Группы томов представляют собой пулы связанных томов, используемых tooensure резервных копий, согласованных на уровне приложения.</span><span class="sxs-lookup"><span data-stu-id="eadcf-106">Volume groups are pools of related volumes used tooensure that backups are application-consistent.</span></span> <span data-ttu-id="eadcf-107">Дополнительные сведения см. в разделах [Томы и группы томов](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) и [Интеграция со службой теневого копирования томов Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="eadcf-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="eadcf-108">У всех томов в группе томов должен быть один поставщик облачной службы.</span><span class="sxs-lookup"><span data-stu-id="eadcf-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="eadcf-109">При настройке группы томов, не следует смешивать Общие тома кластера (CSV) и других типов в hello одной группе томов.</span><span class="sxs-lookup"><span data-stu-id="eadcf-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in hello same volume group.</span></span> <span data-ttu-id="eadcf-110">StorSimple Snapshot Manager не поддерживает сочетание CSV и других типов в hello же моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="eadcf-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in hello same snapshot.</span></span>

![Узел "Группы томов"](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="eadcf-112">**Рисунок 1. Узел "Группы томов" диспетчера моментальных снимков StorSimple**</span><span class="sxs-lookup"><span data-stu-id="eadcf-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="eadcf-113">В этом учебнике объясняется, как использовать диспетчер моментальных снимков StorSimple для выполнения таких задач:</span><span class="sxs-lookup"><span data-stu-id="eadcf-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="eadcf-114">просмотр сведений о группах томов;</span><span class="sxs-lookup"><span data-stu-id="eadcf-114">View information about your volume groups</span></span>
* <span data-ttu-id="eadcf-115">создание группы томов;</span><span class="sxs-lookup"><span data-stu-id="eadcf-115">Create a volume group</span></span>
* <span data-ttu-id="eadcf-116">архивация группы томов;</span><span class="sxs-lookup"><span data-stu-id="eadcf-116">Back up a volume group</span></span>
* <span data-ttu-id="eadcf-117">внесение изменений в группу томов;</span><span class="sxs-lookup"><span data-stu-id="eadcf-117">Edit a volume group</span></span>
* <span data-ttu-id="eadcf-118">удаление группы томов.</span><span class="sxs-lookup"><span data-stu-id="eadcf-118">Delete a volume group</span></span>

<span data-ttu-id="eadcf-119">Все эти действия также доступны на hello **действия** области.</span><span class="sxs-lookup"><span data-stu-id="eadcf-119">All of these actions are also available on hello **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="eadcf-120">Просмотр групп томов</span><span class="sxs-lookup"><span data-stu-id="eadcf-120">View volume groups</span></span>
<span data-ttu-id="eadcf-121">Если щелкнуть hello **группы томов** узел, hello **результаты** панели отображаются следующие сведения о каждой группе томов hello, в зависимости от выбора столбцов hello сделать.</span><span class="sxs-lookup"><span data-stu-id="eadcf-121">If you click hello **Volume Groups** node, hello **Results** pane shows hello following information about each volume group, depending on hello column selections you make.</span></span> <span data-ttu-id="eadcf-122">(столбцы в hello hello **результатов** области являются настраиваемыми.</span><span class="sxs-lookup"><span data-stu-id="eadcf-122">(hello columns in hello **Results** pane are configurable.</span></span> <span data-ttu-id="eadcf-123">Щелкните правой кнопкой мыши hello **тома** выберите **представление**, а затем выберите **добавить или удалить столбцы**.)</span><span class="sxs-lookup"><span data-stu-id="eadcf-123">Right-click hello **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="eadcf-124">Столбец на панели «Результаты»</span><span class="sxs-lookup"><span data-stu-id="eadcf-124">Results column</span></span> | <span data-ttu-id="eadcf-125">Описание</span><span class="sxs-lookup"><span data-stu-id="eadcf-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eadcf-126">Имя</span><span class="sxs-lookup"><span data-stu-id="eadcf-126">Name</span></span> |<span data-ttu-id="eadcf-127">Hello **имя** столбец содержит имя группы томов hello hello.</span><span class="sxs-lookup"><span data-stu-id="eadcf-127">hello **Name** column contains hello name of hello volume group.</span></span> |
| <span data-ttu-id="eadcf-128">Приложение</span><span class="sxs-lookup"><span data-stu-id="eadcf-128">Application</span></span> |<span data-ttu-id="eadcf-129">Hello **приложений** столбце отображается число hello установленные модули записи VSS и работающих на узле Windows "hello".</span><span class="sxs-lookup"><span data-stu-id="eadcf-129">hello **Applications** column shows hello number of VSS writers currently installed and running on hello Windows host.</span></span> |
| <span data-ttu-id="eadcf-130">Выбрано</span><span class="sxs-lookup"><span data-stu-id="eadcf-130">Selected</span></span> |<span data-ttu-id="eadcf-131">Hello **выбранные** столбец показывает hello число томов, которые содержатся в группе томов hello.</span><span class="sxs-lookup"><span data-stu-id="eadcf-131">hello **Selected** column shows hello number of volumes that are contained in hello volume group.</span></span> <span data-ttu-id="eadcf-132">Ноль (0) указывает, что приложение не связана с томами hello в группу томов hello.</span><span class="sxs-lookup"><span data-stu-id="eadcf-132">A zero (0) indicates that no application is associated with hello volumes in hello volume group.</span></span> |
| <span data-ttu-id="eadcf-133">Импортировано</span><span class="sxs-lookup"><span data-stu-id="eadcf-133">Imported</span></span> |<span data-ttu-id="eadcf-134">Hello **импортировано** столбец показывает hello количество импортированных томов.</span><span class="sxs-lookup"><span data-stu-id="eadcf-134">hello **Imported** column shows hello number of imported volumes.</span></span> <span data-ttu-id="eadcf-135">Если задано слишком**True**, этот столбец показывает, что группы томов была импортирована из hello портал Azure и не был создан диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="eadcf-135">When set too**True**, this column indicates that a volume group was imported from hello Azure portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="eadcf-136">Группы томов диспетчера моментальных снимков StorSimple также отображаются на hello **политики резервного копирования** hello портал Azure на вкладке.</span><span class="sxs-lookup"><span data-stu-id="eadcf-136">StorSimple Snapshot Manager volume groups are also displayed on hello **Backup Policies** tab in hello Azure portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="eadcf-137">создание группы томов;</span><span class="sxs-lookup"><span data-stu-id="eadcf-137">Create a volume group</span></span>
<span data-ttu-id="eadcf-138">Используйте следующие процедуры toocreate группу томов hello.</span><span class="sxs-lookup"><span data-stu-id="eadcf-138">Use hello following procedure toocreate a volume group.</span></span>

#### <a name="toocreate-a-volume-group"></a><span data-ttu-id="eadcf-139">toocreate группы томов</span><span class="sxs-lookup"><span data-stu-id="eadcf-139">toocreate a volume group</span></span>
1. <span data-ttu-id="eadcf-140">Щелкните значок рабочего стола hello toostart диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="eadcf-140">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="eadcf-141">В hello **области** области, щелкните правой кнопкой мыши **группы томов**, а затем нажмите кнопку **создать группу томов**.</span><span class="sxs-lookup"><span data-stu-id="eadcf-141">In hello **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span>
   
    ![Создать группу томов](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="eadcf-143">Hello **Создание группы томов** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="eadcf-143">hello **Create a volume group** dialog box appears.</span></span>
   
    ![Диалоговое окно "Создание группы томов"](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. <span data-ttu-id="eadcf-145">Введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="eadcf-145">Enter hello following information:</span></span>
   
   1. <span data-ttu-id="eadcf-146">В hello **имя** введите уникальное имя для новой группы томов hello.</span><span class="sxs-lookup"><span data-stu-id="eadcf-146">In hello **Name** box, type a unique name for hello new volume group.</span></span>
   2. <span data-ttu-id="eadcf-147">В hello **приложений** поле выберите приложения, связанные с томами hello, добавлении toohello группы томов.</span><span class="sxs-lookup"><span data-stu-id="eadcf-147">In hello **Applications** box, select applications associated with hello volumes that you will be adding toohello volume group.</span></span>
      
       <span data-ttu-id="eadcf-148">Hello **приложений** появляется список включены только те приложения, которые используют тома StorSimple, имеют модули записи VSS для них.</span><span class="sxs-lookup"><span data-stu-id="eadcf-148">hello **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="eadcf-149">Модуль записи VSS включен, только если все hello тома модуля записи hello учитывать томов StorSimple.</span><span class="sxs-lookup"><span data-stu-id="eadcf-149">A VSS writer is enabled only if all hello volumes that hello writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="eadcf-150">Если поле приложения hello пуст, ни одного приложения, использующие Azure StorSimple томов и поддерживаемые модули записи VSS будут установлены.</span><span class="sxs-lookup"><span data-stu-id="eadcf-150">If hello Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="eadcf-151">(В настоящее время Azure StorSimple поддерживает Microsoft Exchange и SQL Server.) Дополнительные сведения о модулях записи VSS см. в разделе [Интеграция со службой теневого копирования томов Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="eadcf-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="eadcf-152">При выборе приложения будут автоматически выбраны все тома, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="eadcf-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="eadcf-153">И наоборот, если выбрать тома, связанные с определенным приложением, приложение hello автоматически выбирается в hello **приложений** поле.</span><span class="sxs-lookup"><span data-stu-id="eadcf-153">Conversely, if you select volumes associated with a specific application, hello application is automatically selected in hello **Applications** box.</span></span> 
   3. <span data-ttu-id="eadcf-154">В hello **тома** выберите группу томов toohello tooadd томов StorSimple.</span><span class="sxs-lookup"><span data-stu-id="eadcf-154">In hello **Volumes** box, select StorSimple volumes tooadd toohello volume group.</span></span> 
      
      * <span data-ttu-id="eadcf-155">Вы можете включить тома с одним или несколькими разделами.</span><span class="sxs-lookup"><span data-stu-id="eadcf-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="eadcf-156">(Тома с несколькими разделами могут представлять собой динамические или основные диски с несколькими разделами.) Том с несколькими разделами рассматривается как единое целое.</span><span class="sxs-lookup"><span data-stu-id="eadcf-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="eadcf-157">Таким образом, при добавлении только один из разделов hello tooa группы томов, все hello других секций будут автоматически добавлены toothat тома группа на hello же время.</span><span class="sxs-lookup"><span data-stu-id="eadcf-157">Consequently, if you add only one of hello partitions tooa volume group, all hello other partitions are automatically added toothat volume group at hello same time.</span></span> <span data-ttu-id="eadcf-158">После добавления группы томов тома tooa несколько секций hello тома с несколькими разделами продолжается toobe обрабатывается как единое целое.</span><span class="sxs-lookup"><span data-stu-id="eadcf-158">After you add a multiple partition volume tooa volume group, hello multiple partition volume continues toobe treated as a single unit.</span></span>
      * <span data-ttu-id="eadcf-159">Можно создать пустые группы томов, не назначая toothem все тома.</span><span class="sxs-lookup"><span data-stu-id="eadcf-159">You can create empty volume groups by not assigning any volumes toothem.</span></span> 
      * <span data-ttu-id="eadcf-160">Не следует смешивать Общие тома кластера (CSV) и других типов в hello одной группе томов.</span><span class="sxs-lookup"><span data-stu-id="eadcf-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in hello same volume group.</span></span> <span data-ttu-id="eadcf-161">Диспетчер моментальных снимков StorSimple поддерживает добавление томов CSV и других ТИПОВ томов в hello же моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="eadcf-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in hello same snapshot.</span></span>
4. <span data-ttu-id="eadcf-162">Нажмите кнопку **ОК** группы томов toosave hello.</span><span class="sxs-lookup"><span data-stu-id="eadcf-162">Click **OK** toosave hello volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="eadcf-163">архивация группы томов;</span><span class="sxs-lookup"><span data-stu-id="eadcf-163">Back up a volume group</span></span>
<span data-ttu-id="eadcf-164">Используйте следующие процедуры tooback копирование группы томов hello.</span><span class="sxs-lookup"><span data-stu-id="eadcf-164">Use hello following procedure tooback up a volume group.</span></span>

#### <a name="tooback-up-a-volume-group"></a><span data-ttu-id="eadcf-165">tooback копирование группы томов</span><span class="sxs-lookup"><span data-stu-id="eadcf-165">tooback up a volume group</span></span>
1. <span data-ttu-id="eadcf-166">Щелкните значок рабочего стола hello toostart диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="eadcf-166">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="eadcf-167">В hello **область** области, разверните hello **группы томов** узел, щелкните правой кнопкой мыши группу томов и нажмите кнопку **резервное**.</span><span class="sxs-lookup"><span data-stu-id="eadcf-167">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span>
   
    ![Немедленная архивация группы томов](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="eadcf-169">В hello **резервное** выберите **локальный моментальный снимок** или **облачного моментального снимка**, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="eadcf-169">In hello **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span>
   
    ![Диалоговое окно "Создание резервной копии"](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. <span data-ttu-id="eadcf-171">выполняется tooconfirm, hello резервного копирования, разверните hello **заданий** , а затем щелкните **под управлением**.</span><span class="sxs-lookup"><span data-stu-id="eadcf-171">tooconfirm that hello backup is running, expand hello **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="eadcf-172">должен быть указан Hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="eadcf-172">hello backup should be listed.</span></span>
5. <span data-ttu-id="eadcf-173">hello tooview завершения моментальных снимков, разверните hello **каталог резервных копий** , разверните группу томов hello и нажмите кнопку **локальный моментальный снимок** или **облачного моментального снимка**.</span><span class="sxs-lookup"><span data-stu-id="eadcf-173">tooview hello completed snapshot, expand hello **Backup Catalog** node, expand hello volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="eadcf-174">Hello резервного копирования указывается, если оно завершилось успешно.</span><span class="sxs-lookup"><span data-stu-id="eadcf-174">hello backup will be listed if it finished successfully.</span></span>

## <a name="edit-a-volume-group"></a><span data-ttu-id="eadcf-175">внесение изменений в группу томов;</span><span class="sxs-lookup"><span data-stu-id="eadcf-175">Edit a volume group</span></span>
<span data-ttu-id="eadcf-176">Используйте следующие процедуры tooedit группу томов hello.</span><span class="sxs-lookup"><span data-stu-id="eadcf-176">Use hello following procedure tooedit a volume group.</span></span>

#### <a name="tooedit-a-volume-group"></a><span data-ttu-id="eadcf-177">tooedit группы томов</span><span class="sxs-lookup"><span data-stu-id="eadcf-177">tooedit a volume group</span></span>
1. <span data-ttu-id="eadcf-178">Щелкните значок рабочего стола hello toostart диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="eadcf-178">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="eadcf-179">В hello **область** области, разверните hello **группы томов** узел, щелкните правой кнопкой мыши группу томов и нажмите кнопку **изменить**.</span><span class="sxs-lookup"><span data-stu-id="eadcf-179">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span>
3. <span data-ttu-id="eadcf-180">Hello ** Создание группы томов ** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="eadcf-180">hello **Create a volume group **dialog box appears.</span></span> <span data-ttu-id="eadcf-181">Вы можете изменить hello **имя**, **приложений**, и **тома** записей.</span><span class="sxs-lookup"><span data-stu-id="eadcf-181">You can change hello **Name**, **Applications**, and **Volumes** entries.</span></span>
4. <span data-ttu-id="eadcf-182">Нажмите кнопку **ОК** toosave изменения.</span><span class="sxs-lookup"><span data-stu-id="eadcf-182">Click **OK** toosave your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="eadcf-183">удаление группы томов.</span><span class="sxs-lookup"><span data-stu-id="eadcf-183">Delete a volume group</span></span>
<span data-ttu-id="eadcf-184">Используйте следующие процедуры toodelete группу томов hello.</span><span class="sxs-lookup"><span data-stu-id="eadcf-184">Use hello following procedure toodelete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="eadcf-185">Это также удаляет все резервные копии hello, связанные с группой томов hello.</span><span class="sxs-lookup"><span data-stu-id="eadcf-185">This also deletes all hello backups associated with hello volume group.</span></span>
> 
> 

#### <a name="toodelete-a-volume-group"></a><span data-ttu-id="eadcf-186">toodelete группы томов</span><span class="sxs-lookup"><span data-stu-id="eadcf-186">toodelete a volume group</span></span>
1. <span data-ttu-id="eadcf-187">Щелкните значок рабочего стола hello toostart диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="eadcf-187">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="eadcf-188">В hello **область** области, разверните hello **группы томов** узел, щелкните правой кнопкой мыши группу томов и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="eadcf-188">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span>
3. <span data-ttu-id="eadcf-189">Hello **удаление группы томов** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="eadcf-189">hello **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="eadcf-190">Тип **Подтверждение** в hello текстовое поле и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="eadcf-190">Type **Confirm** in hello text box, and then click **OK**.</span></span>
   
    <span data-ttu-id="eadcf-191">Группа томов Hello удалены исчезнет из списка hello в hello **результатов** панели и всех резервных копий, которые связаны с группой томов удаляются из каталога резервных копий hello.</span><span class="sxs-lookup"><span data-stu-id="eadcf-191">hello deleted volume group vanishes from hello list in hello **Results** pane and all backups that are associated with that volume group are deleted from hello backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eadcf-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eadcf-192">Next steps</span></span>
* <span data-ttu-id="eadcf-193">Узнайте, каким образом слишком[использования диспетчера моментальных снимков StorSimple tooadminister решения StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="eadcf-193">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="eadcf-194">Узнайте, каким образом слишком[использовать toocreate диспетчера моментальных снимков StorSimple и управления политиками резервного копирования](storsimple-snapshot-manager-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="eadcf-194">Learn how too[use StorSimple Snapshot Manager toocreate and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>

