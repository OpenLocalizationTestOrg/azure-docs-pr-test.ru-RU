---
title: "Управление записями контроля доступа в StorSimple | Документация Майкрософт"
description: "Описывает, как использовать записи контроля доступа (ACR), чтобы определить, какие узлы могут подключаться к тому на устройстве StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a87624b5706c1d9b8c2b9926e5580996a89ce984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="af63f-103">Использование службы диспетчера StorSimple для управления записями контроля доступа</span><span class="sxs-lookup"><span data-stu-id="af63f-103">Use the StorSimple Manager service to manage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="af63f-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="af63f-104">Overview</span></span>
<span data-ttu-id="af63f-105">Записи системы контроля доступа (ACR) позволяют указать, какие узлы могут подключаться к тому на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="af63f-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="af63f-106">Записи системы контроля доступа настроены для конкретного тома и содержат полные имена iSCSI (IQN) для узлов.</span><span class="sxs-lookup"><span data-stu-id="af63f-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="af63f-107">Если узел пытается подключиться к тому, устройство проверяет запись контроля доступа, сопоставленную с томом для имени, и в случае совпадения соединение устанавливается.</span><span class="sxs-lookup"><span data-stu-id="af63f-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="af63f-108">Раздел о записях системы контроля доступа на странице **Настройка** содержит все записи контроля доступом с соответствующими IQN для узлов.</span><span class="sxs-lookup"><span data-stu-id="af63f-108">The access control records section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="af63f-109">В этом учебном материале описываются следующие общие задачи, связанные с записями контроля доступа:</span><span class="sxs-lookup"><span data-stu-id="af63f-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="af63f-110">Добавление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="af63f-110">Add an access control record</span></span> 
* <span data-ttu-id="af63f-111">Изменение записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="af63f-111">Edit an access control record</span></span> 
* <span data-ttu-id="af63f-112">Удаление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="af63f-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="af63f-113">При назначении записи контроля доступа тому, проверьте, чтобы доступ к тому не осуществлялся одновременно более чем одним некластеризованным узлом, так как это может повредить работе тома.</span><span class="sxs-lookup"><span data-stu-id="af63f-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span> 
> * <span data-ttu-id="af63f-114">При удалении записи контроля доступа из тома убедитесь, что соответствующий узел не имеет доступа к тому, поскольку удаление может привести к прерыванию операции чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="af63f-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="af63f-115">Добавление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="af63f-115">Add an access control record</span></span>
<span data-ttu-id="af63f-116">Для добавления записей контроля доступа используется страница **Настройка** службы диспетчера StorSimple.</span><span class="sxs-lookup"><span data-stu-id="af63f-116">You use the StorSimple Manager service **Configure** page to add ACRs.</span></span> <span data-ttu-id="af63f-117">Как правило, одной записи контроля доступа соответствует один том.</span><span class="sxs-lookup"><span data-stu-id="af63f-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="af63f-118">Выполните следующие действия для добавления записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="af63f-118">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-access-control-record"></a><span data-ttu-id="af63f-119">Чтобы добавить запись контроля доступа</span><span class="sxs-lookup"><span data-stu-id="af63f-119">To add an access control record</span></span>
1. <span data-ttu-id="af63f-120">На главной странице служб выберите службу, дважды щелкните по имени службы и выберите элемент **Настройка** .</span><span class="sxs-lookup"><span data-stu-id="af63f-120">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="af63f-121">В табличном списке в строке **Записи контроля доступа** введите **Имя** для вашей записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="af63f-121">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="af63f-122">Введите имя IQN вашего узла Windows в строке **Имя инициатора iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="af63f-122">Provide the IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="af63f-123">Чтобы получить IQN узла Windows Server, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="af63f-123">To get the IQN of your Windows Server host, do the following:</span></span>
   
   * <span data-ttu-id="af63f-124">Запустите инициатор iSCSI (Майкрософт) на узле Windows.</span><span class="sxs-lookup"><span data-stu-id="af63f-124">Start the Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="af63f-125">В окне **Свойства инициатора iSCSI** на вкладке **Конфигурация** выберите и скопируйте строку из поля **Имя инициатора**.</span><span class="sxs-lookup"><span data-stu-id="af63f-125">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
   * <span data-ttu-id="af63f-126">Вставьте эту строку в поле **Имя инициатора iSCSI** в таблице записей контроля доступа на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="af63f-126">Paste this string in the **iSCSI Initiator Name** field on the ACRs table in the Azure classic portal.</span></span>
4. <span data-ttu-id="af63f-127">Щелкните **Сохранить** , чтобы сохранить только что созданную запись контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="af63f-127">Click **Save** to save the newly created ACR.</span></span> <span data-ttu-id="af63f-128">Таблица будет обновлена с учетом данного добавления.</span><span class="sxs-lookup"><span data-stu-id="af63f-128">The tabular listing will be updated to reflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="af63f-129">Изменение записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="af63f-129">Edit an access control record</span></span>
<span data-ttu-id="af63f-130">Изменение записей контроля доступа выполняется на странице **Настройка** на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="af63f-130">You use the **Configure** page in the Azure classic portal to edit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="af63f-131">Можно изменить только те записи контроля доступа, которые в настоящее время не используются.</span><span class="sxs-lookup"><span data-stu-id="af63f-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="af63f-132">Чтобы изменить запись контроля доступа, связанную с томом, который используется в настоящий момент, необходимо отключить этот том.</span><span class="sxs-lookup"><span data-stu-id="af63f-132">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="af63f-133">Выполните следующие действия для изменения записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="af63f-133">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="af63f-134">Чтобы изменить запись контроля доступа</span><span class="sxs-lookup"><span data-stu-id="af63f-134">To edit an access control record</span></span>
1. <span data-ttu-id="af63f-135">На главной странице служб выберите службу, дважды щелкните по имени службы и выберите элемент **Настройка** .</span><span class="sxs-lookup"><span data-stu-id="af63f-135">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="af63f-136">В табличном списке записей контроля доступа наведите указатель на запись ACR, которую нужно изменить.</span><span class="sxs-lookup"><span data-stu-id="af63f-136">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="af63f-137">Укажите новое имя и/или IQN для записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="af63f-137">Supply a new name and/or IQN for the ACR.</span></span>
4. <span data-ttu-id="af63f-138">Щелкните **Сохранить** для сохранения изменений в записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="af63f-138">Click **Save** to save the modified ACR.</span></span> <span data-ttu-id="af63f-139">Таблица будет обновлена с учетом изменений.</span><span class="sxs-lookup"><span data-stu-id="af63f-139">The tabular listing will be updated to reflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="af63f-140">Удаление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="af63f-140">Delete an access control record</span></span>
<span data-ttu-id="af63f-141">Удаление записей контроля доступа выполняется на странице **Настройка** на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="af63f-141">You use the **Configure** page in the Azure classic portal to delete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="af63f-142">Можно удалять только те записи контроля доступа, которые в настоящее время не используются.</span><span class="sxs-lookup"><span data-stu-id="af63f-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="af63f-143">Чтобы удалить запись контроля доступа, связанную с томом, который используется в настоящий момент, необходимо отключить этот том.</span><span class="sxs-lookup"><span data-stu-id="af63f-143">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="af63f-144">Выполните следующие действия для удаления записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="af63f-144">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="af63f-145">Чтобы удалить запись контроля доступа</span><span class="sxs-lookup"><span data-stu-id="af63f-145">To delete an access control record</span></span>
1. <span data-ttu-id="af63f-146">На главной странице служб выберите службу, дважды щелкните по имени службы и выберите элемент **Настройка** .</span><span class="sxs-lookup"><span data-stu-id="af63f-146">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="af63f-147">В табличном списке записей контроля доступа (ACR) наведите указатель на запись ACR, которую нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="af63f-147">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span></span>
3. <span data-ttu-id="af63f-148">Значок удаления (**x**) для этой записи контроля доступа будет отображаться в крайнем правом столбце.</span><span class="sxs-lookup"><span data-stu-id="af63f-148">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span></span> <span data-ttu-id="af63f-149">Щелкните значок **x** , чтобы удалить запись контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="af63f-149">Click the **x** icon to delete the ACR.</span></span>
4. <span data-ttu-id="af63f-150">При появлении запроса на подтверждение нажмите кнопку **Да** , чтобы продолжить удаление.</span><span class="sxs-lookup"><span data-stu-id="af63f-150">When prompted for confirmation, click **YES** to continue with the deletion.</span></span> <span data-ttu-id="af63f-151">Таблица будет обновлена с учетом изменений.</span><span class="sxs-lookup"><span data-stu-id="af63f-151">The tabular listing will be updated to reflect the deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af63f-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="af63f-152">Next steps</span></span>
* <span data-ttu-id="af63f-153">Узнайте больше об [управлении томами StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="af63f-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="af63f-154">Узнайте больше об [использовании службы диспетчера StorSimple для администрирования устройства StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="af63f-154">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

