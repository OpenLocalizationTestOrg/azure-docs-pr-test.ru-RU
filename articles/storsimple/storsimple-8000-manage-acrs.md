---
title: "Управление записями контроля доступа в StorSimple | Документация Майкрософт"
description: "Описывает, как использовать записи контроля доступа (ACR), чтобы определить, какие узлы могут подключаться к тому на устройстве StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: 9173e34f889ce1c082b20bb382cb6ca9a03dd797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="e3591-103">Использование службы диспетчера StorSimple для управления записями контроля доступа</span><span class="sxs-lookup"><span data-stu-id="e3591-103">Use the StorSimple Manager service to manage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="e3591-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="e3591-104">Overview</span></span>
<span data-ttu-id="e3591-105">Записи системы контроля доступа (ACR) позволяют указать, какие узлы могут подключаться к тому на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e3591-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="e3591-106">Записи системы контроля доступа настроены для конкретного тома и содержат полные имена iSCSI (IQN) для узлов.</span><span class="sxs-lookup"><span data-stu-id="e3591-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="e3591-107">Если узел пытается подключиться к тому, устройство проверяет запись контроля доступа, сопоставленную с томом для имени, и в случае совпадения соединение устанавливается.</span><span class="sxs-lookup"><span data-stu-id="e3591-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="e3591-108">Раздел **Конфигурация** в колонке службы диспетчера устройств StorSimple отображает все записи контроля доступа и имена IQN соответствующих узлов.</span><span class="sxs-lookup"><span data-stu-id="e3591-108">The access control records in the **Configuration** section of your StorSimple Device Manager service blade display all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="e3591-109">В этом учебном материале описываются следующие общие задачи, связанные с записями контроля доступа:</span><span class="sxs-lookup"><span data-stu-id="e3591-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="e3591-110">Добавление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="e3591-110">Add an access control record</span></span>
* <span data-ttu-id="e3591-111">Изменение записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="e3591-111">Edit an access control record</span></span>
* <span data-ttu-id="e3591-112">Удаление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="e3591-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="e3591-113">При назначении записи контроля доступа тому, проверьте, чтобы доступ к тому не осуществлялся одновременно более чем одним некластеризованным узлом, так как это может повредить работе тома.</span><span class="sxs-lookup"><span data-stu-id="e3591-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="e3591-114">При удалении записи контроля доступа из тома убедитесь, что соответствующий узел не имеет доступа к тому, поскольку удаление может привести к прерыванию операции чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="e3591-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>

## <a name="get-the-iqn"></a><span data-ttu-id="e3591-115">Получение имени IQN</span><span class="sxs-lookup"><span data-stu-id="e3591-115">Get the IQN</span></span>

<span data-ttu-id="e3591-116">Чтобы получить имя IQN узла Windows, который работает под управлением Windows Server 2012, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e3591-116">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="e3591-117">Добавление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="e3591-117">Add an access control record</span></span>
<span data-ttu-id="e3591-118">Раздел **Конфигурация** в колонке службы диспетчера устройств StorSimple позволяет добавлять записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="e3591-118">You use the **Configuration** section in the StorSimple Device Manager service blade to add ACRs.</span></span> <span data-ttu-id="e3591-119">Как правило, одной записи контроля доступа соответствует один том.</span><span class="sxs-lookup"><span data-stu-id="e3591-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="e3591-120">Выполните следующие действия для добавления записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="e3591-120">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="e3591-121">Добавление записи ACR</span><span class="sxs-lookup"><span data-stu-id="e3591-121">To add an ACR</span></span>

1. <span data-ttu-id="e3591-122">Найдите службу диспетчера устройств StorSimple, дважды щелкните имя этой службы, а затем в разделе **Конфигурация** щелкните **Записи контроля доступа**.</span><span class="sxs-lookup"><span data-stu-id="e3591-122">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="e3591-123">В колонке **Записи контроля доступа** щелкните **+ Добавить запись контроля доступа**.</span><span class="sxs-lookup"><span data-stu-id="e3591-123">In the **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Щелкните "Добавить запись контроля доступа"](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="e3591-125">В колонке **Добавление записи контроля доступа** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e3591-125">In the **Add ACR** blade, do the following steps:</span></span>

    1. <span data-ttu-id="e3591-126">Введите имя для записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="e3591-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="e3591-127">Введите имя IQN нужного узла Windows Server в строке **Имя инициатора iSCSI (IQN)**.</span><span class="sxs-lookup"><span data-stu-id="e3591-127">Provide the IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="e3591-128">Нажмите кнопку **Добавить**, чтобы создать запись контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="e3591-128">Click **Add** to create the ACR.</span></span>

        ![Щелкните "Добавить запись контроля доступа"](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="e3591-130">Добавленная запись контроля доступа сразу появится в табличном списке записей контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="e3591-130">The newly added ACR will display in the tabular listing of ACRs.</span></span>

    ![Щелкните "Добавить запись контроля доступа"](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="e3591-132">Изменение записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="e3591-132">Edit an access control record</span></span>
<span data-ttu-id="e3591-133">Раздел **Конфигурация** в колонке службы диспетчера устройств StorSimple позволяет изменять записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="e3591-133">You use the **Configuration** section in the StorSimple Device Manager service blade to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="e3591-134">Мы рекомендуем изменять только те записи, которые сейчас не используются.</span><span class="sxs-lookup"><span data-stu-id="e3591-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="e3591-135">Чтобы изменить запись контроля доступа, связанную с томом, который используется в настоящий момент, необходимо отключить этот том.</span><span class="sxs-lookup"><span data-stu-id="e3591-135">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="e3591-136">Выполните следующие действия для изменения записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="e3591-136">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="e3591-137">Чтобы изменить запись контроля доступа</span><span class="sxs-lookup"><span data-stu-id="e3591-137">To edit an access control record</span></span>
1.  <span data-ttu-id="e3591-138">Найдите службу диспетчера устройств StorSimple, дважды щелкните имя этой службы, а затем в разделе **Конфигурация** щелкните **Записи контроля доступа**.</span><span class="sxs-lookup"><span data-stu-id="e3591-138">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Переход к записям контроля доступа](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="e3591-140">В табличном списке записей контроля доступа щелкните ту запись, которую нужно изменить.</span><span class="sxs-lookup"><span data-stu-id="e3591-140">In the tabular listing of the access control records, click and select the ACR that you wish to modify.</span></span>

    ![Изменение записей контроля доступа](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="e3591-142">В колонке **Правка записи контроля доступа** введите новое имя IQN, обозначающее другой узел.</span><span class="sxs-lookup"><span data-stu-id="e3591-142">In the **Edit access control record** blade, provide a different IQN corresponding to another host.</span></span>

    ![Изменение записей контроля доступа](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="e3591-144">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e3591-144">Click **Save**.</span></span> <span data-ttu-id="e3591-145">При появлении запроса на подтверждение нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="e3591-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Изменение записей контроля доступа](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="e3591-147">Вы получите уведомление об изменении записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="e3591-147">You are notified when the ACR is updated.</span></span> <span data-ttu-id="e3591-148">Таблица со списком также обновится с учетом этих изменений.</span><span class="sxs-lookup"><span data-stu-id="e3591-148">The tabular listing also updates to reflect the change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="e3591-149">Удаление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="e3591-149">Delete an access control record</span></span>
<span data-ttu-id="e3591-150">Раздел **Конфигурация** в колонке службы диспетчера устройств StorSimple позволяет удалять записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="e3591-150">You use the **Configuration** section in the StorSimple Device Manager service blade to delete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="e3591-151">Можно удалять только те записи контроля доступа, которые в настоящее время не используются.</span><span class="sxs-lookup"><span data-stu-id="e3591-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="e3591-152">Чтобы удалить запись контроля доступа, связанную с томом, который используется в настоящий момент, необходимо отключить этот том.</span><span class="sxs-lookup"><span data-stu-id="e3591-152">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="e3591-153">Выполните следующие действия для удаления записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="e3591-153">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="e3591-154">Чтобы удалить запись контроля доступа</span><span class="sxs-lookup"><span data-stu-id="e3591-154">To delete an access control record</span></span>
1.  <span data-ttu-id="e3591-155">Найдите службу диспетчера устройств StorSimple, дважды щелкните имя этой службы, а затем в разделе **Конфигурация** щелкните **Записи контроля доступа**.</span><span class="sxs-lookup"><span data-stu-id="e3591-155">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Переход к записям контроля доступа](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="e3591-157">В табличном списке записей контроля доступа щелкните ту запись, которую нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="e3591-157">In the tabular listing of the access control records, click and select the ACR that you wish to delete.</span></span>

    ![Переход к записям контроля доступа](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="e3591-159">Щелкните правой кнопкой мыши и в открывшемся контекстном меню выберите пункт **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="e3591-159">Right-click to invoke the context menu and select **Delete**.</span></span>

    ![Переход к записям контроля доступа](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="e3591-161">Когда появится запрос на подтверждение, проверьте указанные сведения и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="e3591-161">When prompted for confirmation, review the information and then click **Delete**.</span></span>

    ![Переход к записям контроля доступа](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="e3591-163">Вы получите уведомление, когда удаление завершится.</span><span class="sxs-lookup"><span data-stu-id="e3591-163">You are notified when the deletion completes.</span></span> <span data-ttu-id="e3591-164">Таблица будет обновлена с учетом удаления.</span><span class="sxs-lookup"><span data-stu-id="e3591-164">The tabular listing is updated to reflect the deletion.</span></span>

    ![Переход к записям контроля доступа](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="e3591-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e3591-166">Next steps</span></span>
* <span data-ttu-id="e3591-167">Узнайте больше об [управлении томами StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="e3591-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="e3591-168">Узнайте больше об [использовании службы диспетчера StorSimple для администрирования устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e3591-168">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

