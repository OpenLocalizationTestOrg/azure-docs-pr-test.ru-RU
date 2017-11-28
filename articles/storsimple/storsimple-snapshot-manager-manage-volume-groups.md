---
title: "Группы томов StorSimple Snapshot Manager | Документация Майкрософт"
description: "Узнайте, как использовать оснастку консоли MMC \"Диспетчер моментальных снимков StorSimple\" для создания групп томов и управления ими."
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
ms.openlocfilehash: 6067a88cd42d29c3d2f4b74580095424de77561e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-volume-groups"></a><span data-ttu-id="a6918-103">Создание групп томов и управление ими с помощью диспетчера моментальных снимков StorSimple</span><span class="sxs-lookup"><span data-stu-id="a6918-103">Use StorSimple Snapshot Manager to create and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="a6918-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a6918-104">Overview</span></span>
<span data-ttu-id="a6918-105">Узел **Группы томов** на панели **Область** позволяет назначить тома группам томов, просмотреть сведения о группе томов, запланировать операции архивации и внести изменения в группы томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-105">You can use the **Volume Groups** node on the **Scope** pane to assign volumes to volume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span>

<span data-ttu-id="a6918-106">Группы томов — это пулы связанных томов, которые используются для обеспечения согласованности резервных копий с приложениями.</span><span class="sxs-lookup"><span data-stu-id="a6918-106">Volume groups are pools of related volumes used to ensure that backups are application-consistent.</span></span> <span data-ttu-id="a6918-107">Дополнительные сведения см. в разделах [Томы и группы томов](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) и [Интеграция со службой теневого копирования томов Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="a6918-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="a6918-108">У всех томов в группе томов должен быть один поставщик облачной службы.</span><span class="sxs-lookup"><span data-stu-id="a6918-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="a6918-109">Настраивая группы томов, не размещайте в одной группе томов общие тома кластера (CSV) и тома других типов.</span><span class="sxs-lookup"><span data-stu-id="a6918-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="a6918-110">Диспетчер моментальных снимков StorSimple не поддерживает совместное использование общих томов кластера и томов других типов в одном моментальном снимке.</span><span class="sxs-lookup"><span data-stu-id="a6918-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in the same snapshot.</span></span>

![Узел "Группы томов"](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="a6918-112">**Рисунок 1. Узел "Группы томов" диспетчера моментальных снимков StorSimple**</span><span class="sxs-lookup"><span data-stu-id="a6918-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="a6918-113">В этом учебнике объясняется, как использовать диспетчер моментальных снимков StorSimple для выполнения таких задач:</span><span class="sxs-lookup"><span data-stu-id="a6918-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="a6918-114">просмотр сведений о группах томов;</span><span class="sxs-lookup"><span data-stu-id="a6918-114">View information about your volume groups</span></span>
* <span data-ttu-id="a6918-115">создание группы томов;</span><span class="sxs-lookup"><span data-stu-id="a6918-115">Create a volume group</span></span>
* <span data-ttu-id="a6918-116">архивация группы томов;</span><span class="sxs-lookup"><span data-stu-id="a6918-116">Back up a volume group</span></span>
* <span data-ttu-id="a6918-117">внесение изменений в группу томов;</span><span class="sxs-lookup"><span data-stu-id="a6918-117">Edit a volume group</span></span>
* <span data-ttu-id="a6918-118">удаление группы томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-118">Delete a volume group</span></span>

<span data-ttu-id="a6918-119">Все эти действия также можно выполнить на панели **Действия** .</span><span class="sxs-lookup"><span data-stu-id="a6918-119">All of these actions are also available on the **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="a6918-120">Просмотр групп томов</span><span class="sxs-lookup"><span data-stu-id="a6918-120">View volume groups</span></span>
<span data-ttu-id="a6918-121">Если щелкнуть узел **Группы томов**, то в области **Результаты** отобразятся указанные ниже сведения о каждой группе томов в зависимости от того, какие столбцы вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="a6918-121">If you click the **Volume Groups** node, the **Results** pane shows the following information about each volume group, depending on the column selections you make.</span></span> <span data-ttu-id="a6918-122">(Столбцы на панели **Результаты** можно настраивать.</span><span class="sxs-lookup"><span data-stu-id="a6918-122">(The columns in the **Results** pane are configurable.</span></span> <span data-ttu-id="a6918-123">Щелкните правой кнопкой мыши узел **Тома**, а затем последовательно выберите пункты **Вид** и **Добавить или удалить столбцы**.)</span><span class="sxs-lookup"><span data-stu-id="a6918-123">Right-click the **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="a6918-124">Столбец на панели «Результаты»</span><span class="sxs-lookup"><span data-stu-id="a6918-124">Results column</span></span> | <span data-ttu-id="a6918-125">Описание</span><span class="sxs-lookup"><span data-stu-id="a6918-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a6918-126">Имя</span><span class="sxs-lookup"><span data-stu-id="a6918-126">Name</span></span> |<span data-ttu-id="a6918-127">Столбец **Имя** содержит имя группы томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-127">The **Name** column contains the name of the volume group.</span></span> |
| <span data-ttu-id="a6918-128">Приложение</span><span class="sxs-lookup"><span data-stu-id="a6918-128">Application</span></span> |<span data-ttu-id="a6918-129">В столбце **Приложения** указано количество модулей записи VSS, которые в настоящее время установлены и запущены на узле Windows.</span><span class="sxs-lookup"><span data-stu-id="a6918-129">The **Applications** column shows the number of VSS writers currently installed and running on the Windows host.</span></span> |
| <span data-ttu-id="a6918-130">Выбрано</span><span class="sxs-lookup"><span data-stu-id="a6918-130">Selected</span></span> |<span data-ttu-id="a6918-131">В столбце **Выбрано** указывается количество томов в группе томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-131">The **Selected** column shows the number of volumes that are contained in the volume group.</span></span> <span data-ttu-id="a6918-132">Ноль (0) значит, что с томами в группе томов не связано ни одно приложение.</span><span class="sxs-lookup"><span data-stu-id="a6918-132">A zero (0) indicates that no application is associated with the volumes in the volume group.</span></span> |
| <span data-ttu-id="a6918-133">Импортировано</span><span class="sxs-lookup"><span data-stu-id="a6918-133">Imported</span></span> |<span data-ttu-id="a6918-134">В столбце **Импортировано** отображается количество импортированных томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-134">The **Imported** column shows the number of imported volumes.</span></span> <span data-ttu-id="a6918-135">Если задано значение **True**, этот столбец указывает, что группа томов импортирована с портала Azure, а не создана в диспетчере моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a6918-135">When set to **True**, this column indicates that a volume group was imported from the Azure portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="a6918-136">Группы томов диспетчера моментальных снимков StorSimple также отображаются на вкладке **Политики архивации** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a6918-136">StorSimple Snapshot Manager volume groups are also displayed on the **Backup Policies** tab in the Azure portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="a6918-137">создание группы томов;</span><span class="sxs-lookup"><span data-stu-id="a6918-137">Create a volume group</span></span>
<span data-ttu-id="a6918-138">Выполните указанные ниже действия, чтобы создать группу томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-138">Use the following procedure to create a volume group.</span></span>

#### <a name="to-create-a-volume-group"></a><span data-ttu-id="a6918-139">Создание группы томов</span><span class="sxs-lookup"><span data-stu-id="a6918-139">To create a volume group</span></span>
1. <span data-ttu-id="a6918-140">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a6918-140">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a6918-141">На панели **Область** щелкните правой кнопкой мыши **Группы томов** и выберите пункт **Создать группу томов**.</span><span class="sxs-lookup"><span data-stu-id="a6918-141">In the **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span>
   
    ![Создать группу томов](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="a6918-143">Откроется диалоговое окно **Создание группы томов** .</span><span class="sxs-lookup"><span data-stu-id="a6918-143">The **Create a volume group** dialog box appears.</span></span>
   
    ![Диалоговое окно "Создание группы томов"](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. <span data-ttu-id="a6918-145">Введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="a6918-145">Enter the following information:</span></span>
   
   1. <span data-ttu-id="a6918-146">В поле **Имя** введите уникальное имя новой группы томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-146">In the **Name** box, type a unique name for the new volume group.</span></span>
   2. <span data-ttu-id="a6918-147">В поле **Приложения** выберите приложения, связанные с томами, которые будут добавлены в группу томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-147">In the **Applications** box, select applications associated with the volumes that you will be adding to the volume group.</span></span>
      
       <span data-ttu-id="a6918-148">В поле **Приложения** указаны только те приложения, которые используют тома StorSimple и для которых активированы модули записи VSS.</span><span class="sxs-lookup"><span data-stu-id="a6918-148">The **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="a6918-149">Модуль записи VSS включается, только если все тома, известные ему, представляют собой тома StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a6918-149">A VSS writer is enabled only if all the volumes that the writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="a6918-150">Если оставить поле "Приложения" пустым, не будет установлено ни одно приложение, использующее тома Azure StorSimple и содержащее поддерживаемые модули записи VSS.</span><span class="sxs-lookup"><span data-stu-id="a6918-150">If the Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="a6918-151">(В настоящее время Azure StorSimple поддерживает Microsoft Exchange и SQL Server.) Дополнительные сведения о модулях записи VSS см. в разделе [Интеграция со службой теневого копирования томов Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="a6918-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="a6918-152">При выборе приложения будут автоматически выбраны все тома, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="a6918-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="a6918-153">И наоборот, если выбрать тома, связанные с определенным приложением, приложение будет автоматически выбрано в поле **Приложения** .</span><span class="sxs-lookup"><span data-stu-id="a6918-153">Conversely, if you select volumes associated with a specific application, the application is automatically selected in the **Applications** box.</span></span> 
   3. <span data-ttu-id="a6918-154">В поле **Тома** выберите тома StorSimple, которые нужно добавить в группу томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-154">In the **Volumes** box, select StorSimple volumes to add to the volume group.</span></span> 
      
      * <span data-ttu-id="a6918-155">Вы можете включить тома с одним или несколькими разделами.</span><span class="sxs-lookup"><span data-stu-id="a6918-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="a6918-156">(Тома с несколькими разделами могут представлять собой динамические или основные диски с несколькими разделами.) Том с несколькими разделами рассматривается как единое целое.</span><span class="sxs-lookup"><span data-stu-id="a6918-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="a6918-157">Таким образом, если добавить в группу томов только один из разделов, одновременно в нее будут автоматически добавлены все другие разделы.</span><span class="sxs-lookup"><span data-stu-id="a6918-157">Consequently, if you add only one of the partitions to a volume group, all the other partitions are automatically added to that volume group at the same time.</span></span> <span data-ttu-id="a6918-158">Том с несколькими разделами по-прежнему будет считаться единым целым даже после добавления в группу томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-158">After you add a multiple partition volume to a volume group, the multiple partition volume continues to be treated as a single unit.</span></span>
      * <span data-ttu-id="a6918-159">Вы можете создать пустые группы томов, не назначая им каких-либо томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-159">You can create empty volume groups by not assigning any volumes to them.</span></span> 
      * <span data-ttu-id="a6918-160">Не размещайте в одной группе томов общие тома кластера (CSV) и тома других типов.</span><span class="sxs-lookup"><span data-stu-id="a6918-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="a6918-161">Диспетчер моментальных снимков StorSimple не поддерживает совместное использование общих томов кластера (CSV) и томов других типов в одном моментальном снимке.</span><span class="sxs-lookup"><span data-stu-id="a6918-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in the same snapshot.</span></span>
4. <span data-ttu-id="a6918-162">Нажмите кнопку **ОК** , чтобы сохранить группу томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-162">Click **OK** to save the volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="a6918-163">архивация группы томов;</span><span class="sxs-lookup"><span data-stu-id="a6918-163">Back up a volume group</span></span>
<span data-ttu-id="a6918-164">Выполните указанные ниже действия, чтобы архивировать группу томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-164">Use the following procedure to back up a volume group.</span></span>

#### <a name="to-back-up-a-volume-group"></a><span data-ttu-id="a6918-165">Архивация группы томов</span><span class="sxs-lookup"><span data-stu-id="a6918-165">To back up a volume group</span></span>
1. <span data-ttu-id="a6918-166">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a6918-166">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a6918-167">На панели **Область** разверните узел **Группы томов**, щелкните правой кнопкой мыши имя группы томов и выберите пункт **Создать резервную копию**.</span><span class="sxs-lookup"><span data-stu-id="a6918-167">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span>
   
    ![Немедленная архивация группы томов](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="a6918-169">В диалоговом окне **Создать резервную копию** выберите пункт **Локальный моментальный снимок** или **Облачный моментальный снимок**, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a6918-169">In the **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span>
   
    ![Диалоговое окно "Создание резервной копии"](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. <span data-ttu-id="a6918-171">Чтобы убедиться, что архивация запущена, разверните узел **Задания** и щелкните **Выполняются**.</span><span class="sxs-lookup"><span data-stu-id="a6918-171">To confirm that the backup is running, expand the **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="a6918-172">Операция архивации должна быть указана в списке.</span><span class="sxs-lookup"><span data-stu-id="a6918-172">The backup should be listed.</span></span>
5. <span data-ttu-id="a6918-173">Чтобы просмотреть созданный моментальный снимок, последовательно разверните узел **Каталог архивов** и имя группы томов, а затем щелкните **Локальный моментальный снимок** или **Облачный моментальный снимок**.</span><span class="sxs-lookup"><span data-stu-id="a6918-173">To view the completed snapshot, expand the **Backup Catalog** node, expand the volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="a6918-174">Если операция архивации успешно завершена, она будет указана в списке.</span><span class="sxs-lookup"><span data-stu-id="a6918-174">The backup will be listed if it finished successfully.</span></span>

## <a name="edit-a-volume-group"></a><span data-ttu-id="a6918-175">внесение изменений в группу томов;</span><span class="sxs-lookup"><span data-stu-id="a6918-175">Edit a volume group</span></span>
<span data-ttu-id="a6918-176">Выполните указанные ниже действия, чтобы внести изменения в группу томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-176">Use the following procedure to edit a volume group.</span></span>

#### <a name="to-edit-a-volume-group"></a><span data-ttu-id="a6918-177">Внесение изменений в группу томов</span><span class="sxs-lookup"><span data-stu-id="a6918-177">To edit a volume group</span></span>
1. <span data-ttu-id="a6918-178">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a6918-178">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a6918-179">На панели **Область** разверните узел **Группы томов**, щелкните правой кнопкой мыши имя группы томов и выберите пункт **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="a6918-179">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span>
3. <span data-ttu-id="a6918-180">Откроется диалоговое окно **Создание группы томов**.</span><span class="sxs-lookup"><span data-stu-id="a6918-180">The **Create a volume group **dialog box appears.</span></span> <span data-ttu-id="a6918-181">Вы можете изменить значения в полях **Имя**, **Приложения** и **Тома**.</span><span class="sxs-lookup"><span data-stu-id="a6918-181">You can change the **Name**, **Applications**, and **Volumes** entries.</span></span>
4. <span data-ttu-id="a6918-182">Нажмите кнопку **ОК** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="a6918-182">Click **OK** to save your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="a6918-183">удаление группы томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-183">Delete a volume group</span></span>
<span data-ttu-id="a6918-184">Выполните указанные ниже действия, чтобы удалить группу томов.</span><span class="sxs-lookup"><span data-stu-id="a6918-184">Use the following procedure to delete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="a6918-185">Вместе с ней также будут удалены все связанные резервные копии.</span><span class="sxs-lookup"><span data-stu-id="a6918-185">This also deletes all the backups associated with the volume group.</span></span>
> 
> 

#### <a name="to-delete-a-volume-group"></a><span data-ttu-id="a6918-186">Удаление группы томов</span><span class="sxs-lookup"><span data-stu-id="a6918-186">To delete a volume group</span></span>
1. <span data-ttu-id="a6918-187">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a6918-187">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a6918-188">На панели **Область** разверните узел **Группы томов**, щелкните правой кнопкой мыши имя группы томов и выберите пункт **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="a6918-188">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span>
3. <span data-ttu-id="a6918-189">Откроется диалоговое окно **Удаление группы томов** .</span><span class="sxs-lookup"><span data-stu-id="a6918-189">The **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="a6918-190">В текстовом поле введите **Confirm** (Подтверждаю) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a6918-190">Type **Confirm** in the text box, and then click **OK**.</span></span>
   
    <span data-ttu-id="a6918-191">Удаленная группа томов исчезнет из списка на панели **Результаты** , а все резервные копии, связанные с этой группой, будут удалены из каталога архивов.</span><span class="sxs-lookup"><span data-stu-id="a6918-191">The deleted volume group vanishes from the list in the **Results** pane and all backups that are associated with that volume group are deleted from the backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6918-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a6918-192">Next steps</span></span>
* <span data-ttu-id="a6918-193">Узнайте, как [использовать диспетчер моментальных снимков StorSimple для администрирования решения StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="a6918-193">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="a6918-194">Узнайте, как [создавать политики архивации и управлять ими с помощью диспетчера моментальных снимков StorSimple](storsimple-snapshot-manager-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="a6918-194">Learn how to [use StorSimple Snapshot Manager to create and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>

