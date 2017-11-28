---
title: "Управление записями контроля доступа для виртуального массива StorSimple | Документация Майкрософт"
description: "В этой статье объясняется, как с помощью записей контроля доступа (ACR) определять, какие узлы могут подключаться к тому в виртуальном массиве StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2ce65aa4efba735305208f7a6d761bc2814d1b8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-to-manage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="bb124-103">Управление записями контроля доступа для виртуального массива StorSimple с помощью диспетчера устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="bb124-103">Use StorSimple Device Manager to manage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="bb124-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="bb124-104">Overview</span></span>

<span data-ttu-id="bb124-105">Записи контроля доступа (ACR) позволяют указать, какие узлы могут подключаться к тому в виртуальном массиве StorSimple (также известному как локальное виртуальное устройство StorSimple).</span><span class="sxs-lookup"><span data-stu-id="bb124-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple Virtual Array (also known as the StorSimple on-premises virtual device).</span></span> <span data-ttu-id="bb124-106">Записи контроля доступа настроены для конкретного тома и содержат полные имена iSCSI (IQN) для узлов.</span><span class="sxs-lookup"><span data-stu-id="bb124-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="bb124-107">Когда узел пытается подключиться к тому, устройство проверяет запись ACR, сопоставленную с томом для соответствующего имени IQN, и в случае совпадения разрешает подключение.</span><span class="sxs-lookup"><span data-stu-id="bb124-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name, and if there is a match, then the connection is established.</span></span> <span data-ttu-id="bb124-108">Колонка **Записи контроля доступа** в разделе **Конфигурация** службы диспетчера устройств содержит все записи контроля доступа с соответствующими IQN для узлов.</span><span class="sxs-lookup"><span data-stu-id="bb124-108">The **Access control records** blade within the **Configuration** section of your Device Manager service displays all the access control records with the corresponding IQNs of the hosts.</span></span>

![Управление записями контроля доступа](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="bb124-110">В этом учебном материале описываются следующие общие задачи, связанные с записями контроля доступа:</span><span class="sxs-lookup"><span data-stu-id="bb124-110">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="bb124-111">Получение имени IQN</span><span class="sxs-lookup"><span data-stu-id="bb124-111">Get the IQN</span></span>
* <span data-ttu-id="bb124-112">Добавление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="bb124-112">Add an access control record</span></span>
* <span data-ttu-id="bb124-113">Изменение записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="bb124-113">Edit an access control record</span></span>
* <span data-ttu-id="bb124-114">Удаление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="bb124-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="bb124-115">При назначении записи контроля доступа тому, проверьте, чтобы доступ к тому не осуществлялся одновременно более чем одним некластеризованным узлом, так как это может повредить работе тома.</span><span class="sxs-lookup"><span data-stu-id="bb124-115">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="bb124-116">При удалении записи контроля доступа из тома убедитесь, что соответствующий узел не имеет доступа к тому, поскольку удаление может привести к прерыванию операции чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="bb124-116">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


## <a name="get-the-iqn"></a><span data-ttu-id="bb124-117">Получение имени IQN</span><span class="sxs-lookup"><span data-stu-id="bb124-117">Get the IQN</span></span>

<span data-ttu-id="bb124-118">Чтобы получить имя IQN узла Windows, который работает под управлением Windows Server 2012, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bb124-118">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="bb124-119">Добавление записей ACR</span><span class="sxs-lookup"><span data-stu-id="bb124-119">Add an ACR</span></span>

<span data-ttu-id="bb124-120">Добавить записи контроля доступа (ACR) можно в колонке **Записи контроля доступа** в разделе **Конфигурация** службы диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bb124-120">You use **Access control records** blade within the **Configuration** section of your StorSimple Device Manager service to add ACRs.</span></span> <span data-ttu-id="bb124-121">Как правило, одной записи контроля доступа соответствует один том.</span><span class="sxs-lookup"><span data-stu-id="bb124-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="bb124-122">Сведения о связывании записи ACR с томом см. в разделе о [добавлении тома](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="bb124-122">For information about associating an ACR with a volume, go to [add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb124-123">При назначении записи контроля доступа тому, проверьте, чтобы доступ к тому не осуществлялся одновременно более чем одним некластеризованным узлом, так как это может повредить работе тома.</span><span class="sxs-lookup"><span data-stu-id="bb124-123">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>


<span data-ttu-id="bb124-124">Выполните следующие действия для добавления записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="bb124-124">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="bb124-125">Добавление записи ACR</span><span class="sxs-lookup"><span data-stu-id="bb124-125">To add an ACR</span></span>

1. <span data-ttu-id="bb124-126">На главной странице служб выберите службу, дважды щелкните ее имя, а затем в разделе **Конфигурация** щелкните **Записи контроля доступа**.</span><span class="sxs-lookup"><span data-stu-id="bb124-126">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="bb124-127">В колонке **Записи контроля доступа** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bb124-127">In the **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="bb124-128">В колонке **Добавление записи контроля доступа** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bb124-128">In the **Add ACR** blade, do the following:</span></span>
   
    1. <span data-ttu-id="bb124-129">В поле **Имя** введите имя записи управления доступом.</span><span class="sxs-lookup"><span data-stu-id="bb124-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="bb124-130">В строке **Имя инициатора iSCSI**введите имя IQN своего узла Windows.</span><span class="sxs-lookup"><span data-stu-id="bb124-130">Under **iSCSI Initiator Name**, provide the IQN name of your Windows host.</span></span> <span data-ttu-id="bb124-131">Чтобы получить IQN узла Windows Server, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bb124-131">To get the IQN of your Windows Server host, do the following:</span></span>
   
    3. <span data-ttu-id="bb124-132">Запустите инициатор iSCSI (Майкрософт) на узле Windows.</span><span class="sxs-lookup"><span data-stu-id="bb124-132">Start the Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="bb124-133">В окне iSCSI Initiator Properties (Свойства инициатора iSCSI) на вкладке **Конфигурация** выберите и скопируйте строку из поля **Имя инициатора**.</span><span class="sxs-lookup"><span data-stu-id="bb124-133">In the iSCSI Initiator Properties window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
    <span data-ttu-id="bb124-134">Вставьте эту строку в поле **IQN** в колонке **Добавление записи контроля доступа**.</span><span class="sxs-lookup"><span data-stu-id="bb124-134">Paste this string in the **IQN** field in the **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="bb124-135">Чтобы добавить запись контроля доступа, нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bb124-135">Click **Add** to add the ACR.</span></span>  
   
        ![Добавление записей контроля доступа](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="bb124-137">Таблица будет обновлена с учетом данного добавления.</span><span class="sxs-lookup"><span data-stu-id="bb124-137">The tabular listing is updated to reflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="bb124-138">Изменение записей ACR</span><span class="sxs-lookup"><span data-stu-id="bb124-138">Edit an ACR</span></span>

<span data-ttu-id="bb124-139">Изменить записи контроля доступа можно в колонке **Записи контроля доступа** в разделе **Конфигурация** службы диспетчера устройств на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bb124-139">You use the **Access control records** blade within the **Configuration** section of your Device Manager service in the Azure portal to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="bb124-140">Не следует изменять записи контроля доступа, которые используются в настоящий момент.</span><span class="sxs-lookup"><span data-stu-id="bb124-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="bb124-141">Чтобы изменить запись ACR, связанную с томом, который используется в настоящий момент, сначала нужно отключить этот том.</span><span class="sxs-lookup"><span data-stu-id="bb124-141">To edit an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>


<span data-ttu-id="bb124-142">Выполните следующие действия для изменения записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="bb124-142">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-acr"></a><span data-ttu-id="bb124-143">Изменение записи ACR</span><span class="sxs-lookup"><span data-stu-id="bb124-143">To edit an ACR</span></span>

1. <span data-ttu-id="bb124-144">На главной странице служб выберите службу, дважды щелкните ее имя, а затем в разделе **Конфигурация** щелкните **Записи контроля доступа**.</span><span class="sxs-lookup"><span data-stu-id="bb124-144">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="bb124-145">В колонке **Записи контроля доступа** в табличном списке записей контроля доступа дважды щелкните запись ACR, которую нужно изменить.</span><span class="sxs-lookup"><span data-stu-id="bb124-145">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="bb124-146">В колонке **Edit access control records** (Изменение записей контроля доступа) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bb124-146">In the **Edit access control records** blade, do the following:</span></span>
   
    1. <span data-ttu-id="bb124-147">Укажите IQN записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="bb124-147">Supply the IQN for the ACR.</span></span>
   
    2. <span data-ttu-id="bb124-148">Чтобы сохранить измененную запись контроля доступа, щелкните **Сохранить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="bb124-148">Click **Save** at the top of the blade to save the modified ACR.</span></span> <span data-ttu-id="bb124-149">Вы увидите следующее сообщение с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="bb124-149">You see the following confirmation message:</span></span>
   
        ![Изменение записей контроля доступа](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="bb124-151">Удаление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="bb124-151">Delete an access control record</span></span>

<span data-ttu-id="bb124-152">Записи ACR можно удалить на портале Azure на странице **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="bb124-152">You use the **Configuration** page in the Azure portal to delete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="bb124-153">Не следует удалять записи контроля доступа, которые используются в настоящий момент.</span><span class="sxs-lookup"><span data-stu-id="bb124-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="bb124-154">Чтобы удалить запись ACR, связанную с томом, который используется в настоящий момент, сначала нужно отключить этот том.</span><span class="sxs-lookup"><span data-stu-id="bb124-154">To delete an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>
> * <span data-ttu-id="bb124-155">При удалении записи контроля доступа из тома убедитесь, что соответствующий узел не имеет доступа к тому, поскольку удаление может привести к прерыванию операции чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="bb124-155">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="bb124-156">Выполните следующие действия для удаления записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="bb124-156">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="bb124-157">Чтобы удалить запись контроля доступа</span><span class="sxs-lookup"><span data-stu-id="bb124-157">To delete an access control record</span></span>

1. <span data-ttu-id="bb124-158">На главной странице служб выберите службу, дважды щелкните ее имя, а затем в разделе **Конфигурация** щелкните **Записи контроля доступа**.</span><span class="sxs-lookup"><span data-stu-id="bb124-158">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="bb124-159">В колонке **Записи контроля доступа** в табличном списке записей контроля доступа дважды щелкните запись ACR, которую нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="bb124-159">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to delete.</span></span>

3. <span data-ttu-id="bb124-160">В колонке Edit access control records (Изменение записей контроля доступа) щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="bb124-160">In the Edit access control records blade, click **Delete**.</span></span>
   
    ![Удаление записей контроля доступа](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="bb124-162">При появлении запроса на подтверждение нажмите кнопку **Удалить**, чтобы продолжить удаление.</span><span class="sxs-lookup"><span data-stu-id="bb124-162">When prompted for confirmation, click **Delete** to continue with the deletion.</span></span> <span data-ttu-id="bb124-163">Таблица будет обновлена с учетом удаления.</span><span class="sxs-lookup"><span data-stu-id="bb124-163">The tabular listing is updated to reflect the deletion.</span></span>
   
   ![Предупреждение](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="bb124-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb124-165">Next steps</span></span>

* <span data-ttu-id="bb124-166">[Сведения о добавлении томов и настройке записей ACR](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)</span><span class="sxs-lookup"><span data-stu-id="bb124-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

