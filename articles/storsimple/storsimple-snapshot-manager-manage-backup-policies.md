---
title: "политики резервного копирования диспетчера моментальных снимков aaaStorSimple | Документы Microsoft"
description: "Описывается порядок toouse hello toocreate оснастку консоли MMC диспетчера моментальных снимков StorSimple и управления политиками резервного копирования hello, управляющие запланированных операций резервного копирования."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a><span data-ttu-id="a5827-103">Использование диспетчера моментальных снимков StorSimple toocreate и управления политиками резервного копирования</span><span class="sxs-lookup"><span data-stu-id="a5827-103">Use StorSimple Snapshot Manager toocreate and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="a5827-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a5827-104">Overview</span></span>
<span data-ttu-id="a5827-105">Политики резервного копирования создает расписание для резервного копирования данных тома локально или в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="a5827-105">A backup policy creates a schedule for backing up volume data locally or in hello cloud.</span></span> <span data-ttu-id="a5827-106">Создавая политику архивации, вы также можете указать политику хранения.</span><span class="sxs-lookup"><span data-stu-id="a5827-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="a5827-107">(Можно сохранить не более 64 моментальных снимков.) Дополнительные сведения о политиках архивации см. в разделе [Типы резервных копий](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) и статье [Серия StorSimple 8000: решение гибридного облачного хранилища](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5827-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="a5827-108">В этом учебнике объясняется, как выполнить такие задачи:</span><span class="sxs-lookup"><span data-stu-id="a5827-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="a5827-109">создание политики архивации;</span><span class="sxs-lookup"><span data-stu-id="a5827-109">Create a backup policy</span></span>
* <span data-ttu-id="a5827-110">внесение изменений в политику архивации;</span><span class="sxs-lookup"><span data-stu-id="a5827-110">Edit a backup policy</span></span>
* <span data-ttu-id="a5827-111">Удаление политики архивации</span><span class="sxs-lookup"><span data-stu-id="a5827-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="a5827-112">создание политики архивации;</span><span class="sxs-lookup"><span data-stu-id="a5827-112">Create a backup policy</span></span>
<span data-ttu-id="a5827-113">Используйте следующие процедуры toocreate новую политику резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="a5827-113">Use hello following procedure toocreate a new backup policy.</span></span>

#### <a name="toocreate-a-backup-policy"></a><span data-ttu-id="a5827-114">toocreate политику резервного копирования</span><span class="sxs-lookup"><span data-stu-id="a5827-114">toocreate a backup policy</span></span>
1. <span data-ttu-id="a5827-115">Щелкните значок рабочего стола hello toostart диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a5827-115">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a5827-116">В hello **область** панели, щелкните правой кнопкой мыши **политики резервного копирования**и нажмите кнопку **создать политику резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="a5827-116">In hello **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![создание политики архивации;](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="a5827-118">Hello **создать политику** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a5827-118">hello **Create a Policy** dialog box appears.</span></span>

    ![Создание политики — вкладка "Общие"](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="a5827-120">На hello **Общие** вкладка, полный hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="a5827-120">On hello **General** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="a5827-121">В hello **имя** текстовом поле введите имя для политики hello.</span><span class="sxs-lookup"><span data-stu-id="a5827-121">In hello **Name** text box, type a name for hello policy.</span></span>
   2. <span data-ttu-id="a5827-122">В hello **группы томов** текстовое поле, имя типа hello hello группы томов, связанные с политикой hello.</span><span class="sxs-lookup"><span data-stu-id="a5827-122">In hello **Volume group** text box, type hello name of hello volume group associated with hello policy.</span></span>
   3. <span data-ttu-id="a5827-123">Выберите **Локальный моментальный снимок** или **Облачный моментальный снимок**.</span><span class="sxs-lookup"><span data-stu-id="a5827-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="a5827-124">Выберите число hello tooretain моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="a5827-124">Select hello number of snapshots tooretain.</span></span> <span data-ttu-id="a5827-125">При выборе **все**, будут сохранены 64 моментальных снимков (hello максимальное).</span><span class="sxs-lookup"><span data-stu-id="a5827-125">If you select **All**, 64 snapshots will be retained (hello maximum).</span></span>
4. <span data-ttu-id="a5827-126">Нажмите кнопку hello **расписание** вкладки.</span><span class="sxs-lookup"><span data-stu-id="a5827-126">Click hello **Schedule** tab.</span></span>

    ![Создание политики — вкладка "Расписание"](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="a5827-128">На hello **расписание** вкладка, полный hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="a5827-128">On hello **Schedule** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="a5827-129">Нажмите кнопку hello **включить** tooschedule флажок hello следующего резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="a5827-129">Click hello **Enable** check box tooschedule hello next backup.</span></span>
   2. <span data-ttu-id="a5827-130">В разделе **Параметры** выберите вариант **Один раз**, **Ежедневно**, **Еженедельно** или **Ежемесячно**.</span><span class="sxs-lookup"><span data-stu-id="a5827-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="a5827-131">В hello **запустить** текстовое поле, щелкните значок календаря hello и выберите дату начала.</span><span class="sxs-lookup"><span data-stu-id="a5827-131">In hello **Start** text box, click hello calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="a5827-132">В разделе **Дополнительные параметры**можно задать дополнительные расписания и дату окончания.</span><span class="sxs-lookup"><span data-stu-id="a5827-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="a5827-133">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a5827-133">Click **OK**.</span></span>

<span data-ttu-id="a5827-134">Появляется после создания политики резервного копирования, hello следующую информацию в hello **результатов** панели:</span><span class="sxs-lookup"><span data-stu-id="a5827-134">After you create a backup policy, hello following information appears in hello **Results** pane:</span></span>

* <span data-ttu-id="a5827-135">**Имя** — hello имя политики резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="a5827-135">**Name** – hello name of backup policy.</span></span>
* <span data-ttu-id="a5827-136">**Тип** : тип моментального снимка (локальный или облачный).</span><span class="sxs-lookup"><span data-stu-id="a5827-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="a5827-137">**Группа томов** — hello группы томов, связанные с политикой hello.</span><span class="sxs-lookup"><span data-stu-id="a5827-137">**Volume Group** – hello volume group associated with hello policy.</span></span>
* <span data-ttu-id="a5827-138">**Хранения** — hello количество сохраняемых моментальных снимков; hello максимальное — 64.</span><span class="sxs-lookup"><span data-stu-id="a5827-138">**Retention** – hello number of snapshots retained; hello maximum is 64.</span></span>
* <span data-ttu-id="a5827-139">**Создать** — hello Дата создания этой политики.</span><span class="sxs-lookup"><span data-stu-id="a5827-139">**Created** – hello date that this policy was created.</span></span>
* <span data-ttu-id="a5827-140">**Включить** — используется ли в настоящий момент политики hello: **True** указывает, что фактически; **False** указывает, что он не действует.</span><span class="sxs-lookup"><span data-stu-id="a5827-140">**Enabled** – whether hello policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="a5827-141">внесение изменений в политику архивации;</span><span class="sxs-lookup"><span data-stu-id="a5827-141">Edit a backup policy</span></span>
<span data-ttu-id="a5827-142">Используйте следующие процедуры tooedit существует политика резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="a5827-142">Use hello following procedure tooedit an existing backup policy.</span></span>

#### <a name="tooedit-a-backup-policy"></a><span data-ttu-id="a5827-143">tooedit политику резервного копирования</span><span class="sxs-lookup"><span data-stu-id="a5827-143">tooedit a backup policy</span></span>
1. <span data-ttu-id="a5827-144">Щелкните значок рабочего стола hello toostart диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a5827-144">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a5827-145">В hello **область** панели щелкните hello **политики резервного копирования** узла.</span><span class="sxs-lookup"><span data-stu-id="a5827-145">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="a5827-146">Отображаются все политики резервного копирования hello в hello **результатов** области.</span><span class="sxs-lookup"><span data-stu-id="a5827-146">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="a5827-147">Щелкните правой кнопкой мыши политику hello требуется tooedit и нажмите кнопку **изменить**.</span><span class="sxs-lookup"><span data-stu-id="a5827-147">Right-click hello policy that you want tooedit, and then click **Edit**.</span></span>

    ![внесение изменений в политику архивации;](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="a5827-149">Здравствуйте, когда **создать политику** появится окно, внесите изменения и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a5827-149">When hello **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="a5827-150">Удаление политики архивации</span><span class="sxs-lookup"><span data-stu-id="a5827-150">Delete a backup policy</span></span>
<span data-ttu-id="a5827-151">Используйте следующие процедуры toodelete политику резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="a5827-151">Use hello following procedure toodelete a backup policy.</span></span>

#### <a name="toodelete-a-backup-policy"></a><span data-ttu-id="a5827-152">toodelete политику резервного копирования</span><span class="sxs-lookup"><span data-stu-id="a5827-152">toodelete a backup policy</span></span>
1. <span data-ttu-id="a5827-153">Щелкните значок рабочего стола hello toostart диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a5827-153">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a5827-154">В hello **область** панели щелкните hello **политики резервного копирования** узла.</span><span class="sxs-lookup"><span data-stu-id="a5827-154">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="a5827-155">Отображаются все политики резервного копирования hello в hello **результатов** области.</span><span class="sxs-lookup"><span data-stu-id="a5827-155">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="a5827-156">Щелкните правой кнопкой мыши политику резервного копирования hello требуется toodelete и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="a5827-156">Right-click hello backup policy that you want toodelete, and then click **Delete**.</span></span>
4. <span data-ttu-id="a5827-157">Когда появится сообщение с подтверждением hello, щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="a5827-157">When hello confirmation message appears, click **Yes**.</span></span>

    ![Подтверждение удаления политики архивации](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="a5827-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a5827-159">Next steps</span></span>
* <span data-ttu-id="a5827-160">Узнайте, каким образом слишком[использования диспетчера моментальных снимков StorSimple tooadminister решения StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="a5827-160">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="a5827-161">Узнайте, каким образом слишком[использование tooview диспетчера моментальных снимков StorSimple и управление ими заданий резервного копирования](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="a5827-161">Learn how too[use StorSimple Snapshot Manager tooview and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
