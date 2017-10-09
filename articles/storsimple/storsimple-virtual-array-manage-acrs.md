---
title: "aaaManage записи управления доступом для StorSimple Virtual Array | Документы Microsoft"
description: "Описывает принципы управления доступом toomanage записей toodetermine (ACR), какие узлы могут подключаться tooa томе hello StorSimple Virtual Array."
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
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="02b18-103">Записи управления доступом с помощью диспетчера устройств StorSimple toomanage для StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="02b18-103">Use StorSimple Device Manager toomanage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="02b18-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="02b18-104">Overview</span></span>

<span data-ttu-id="02b18-105">Записи управления доступом (ACR) позволяют toospecify, какие узлы могут подключаться tooa томе hello StorSimple Virtual Array (также известный как hello локального виртуального устройства StorSimple).</span><span class="sxs-lookup"><span data-stu-id="02b18-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device).</span></span> <span data-ttu-id="02b18-106">Записи контроля доступа задаются tooa томов и содержать hello iSCSI (IQN) полные имена узлов hello.</span><span class="sxs-lookup"><span data-stu-id="02b18-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="02b18-107">Когда узел пытается tooconnect tooa тома, устройство hello проверяет hello ACR, связанную с этим томом hello IQN-имя, и в случае совпадения, устанавливается соединение hello.</span><span class="sxs-lookup"><span data-stu-id="02b18-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name, and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="02b18-108">Hello **записи управления доступом** колонки в hello **конфигурации** разделе службы диспетчера устройств отображаются все записи управления доступом hello с hello соответствующее IQN узлов hello.</span><span class="sxs-lookup"><span data-stu-id="02b18-108">hello **Access control records** blade within hello **Configuration** section of your Device Manager service displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

![Управление записями контроля доступа](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="02b18-110">В этом учебнике описано следующие общие задачи, связанные с ACR hello:</span><span class="sxs-lookup"><span data-stu-id="02b18-110">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="02b18-111">Получение IQN hello</span><span class="sxs-lookup"><span data-stu-id="02b18-111">Get hello IQN</span></span>
* <span data-ttu-id="02b18-112">Добавление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="02b18-112">Add an access control record</span></span>
* <span data-ttu-id="02b18-113">Изменение записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="02b18-113">Edit an access control record</span></span>
* <span data-ttu-id="02b18-114">Удаление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="02b18-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="02b18-115">При назначении томе tooa контроля доступа, будьте внимательны, что тома hello не имеет доступа к одновременно более чем одного некластеризованного узла, так как это может повредить том hello.</span><span class="sxs-lookup"><span data-stu-id="02b18-115">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="02b18-116">При удалении записи управления Доступом из тома, убедитесь, что соответствующий узел, hello не имеет доступа к hello тома, так как hello удаление может привести к прерыванию чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="02b18-116">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


## <a name="get-hello-iqn"></a><span data-ttu-id="02b18-117">Получение IQN hello</span><span class="sxs-lookup"><span data-stu-id="02b18-117">Get hello IQN</span></span>

<span data-ttu-id="02b18-118">Выполните следующие шаги tooget hello IQN узла Windows под управлением Windows Server 2012 hello.</span><span class="sxs-lookup"><span data-stu-id="02b18-118">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="02b18-119">Добавление записей ACR</span><span class="sxs-lookup"><span data-stu-id="02b18-119">Add an ACR</span></span>

<span data-ttu-id="02b18-120">Вы используете **записи управления доступом** колонки в hello **конфигурации** части вашего tooadd службы диспетчера StorSimple устройство записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="02b18-120">You use **Access control records** blade within hello **Configuration** section of your StorSimple Device Manager service tooadd ACRs.</span></span> <span data-ttu-id="02b18-121">Как правило, одной записи контроля доступа соответствует один том.</span><span class="sxs-lookup"><span data-stu-id="02b18-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="02b18-122">Сведения о связывании записи управления Доступом с томом go слишком[добавить том](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="02b18-122">For information about associating an ACR with a volume, go too[add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02b18-123">При назначении томе tooa контроля доступа, будьте внимательны, что тома hello не имеет доступа к одновременно более чем одного некластеризованного узла, так как это может повредить том hello.</span><span class="sxs-lookup"><span data-stu-id="02b18-123">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>


<span data-ttu-id="02b18-124">Выполните hello, выполнив шаги tooadd записи управления Доступом.</span><span class="sxs-lookup"><span data-stu-id="02b18-124">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="02b18-125">tooadd запись контроля доступа</span><span class="sxs-lookup"><span data-stu-id="02b18-125">tooadd an ACR</span></span>

1. <span data-ttu-id="02b18-126">На целевой странице службы hello, выберите службу, дважды щелкните hello имя службы и затем в hello **конфигурации** щелкните **записи управления доступом**.</span><span class="sxs-lookup"><span data-stu-id="02b18-126">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="02b18-127">В hello **записи управления доступом** колонка, щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="02b18-127">In hello **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="02b18-128">В hello **Добавление ACR** колонке hello следующие:</span><span class="sxs-lookup"><span data-stu-id="02b18-128">In hello **Add ACR** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="02b18-129">В поле **Имя** введите имя записи управления доступом.</span><span class="sxs-lookup"><span data-stu-id="02b18-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="02b18-130">В разделе **имя инициатора iSCSI**, укажите имя hello IQN узла Windows.</span><span class="sxs-lookup"><span data-stu-id="02b18-130">Under **iSCSI Initiator Name**, provide hello IQN name of your Windows host.</span></span> <span data-ttu-id="02b18-131">hello tooget IQN узла Windows Server, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="02b18-131">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
    3. <span data-ttu-id="02b18-132">Запустите инициатор Microsoft iSCSI hello на узле Windows.</span><span class="sxs-lookup"><span data-stu-id="02b18-132">Start hello Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="02b18-133">В окне свойств инициатора iSCSI hello на hello **конфигурации** выберите и скопируйте строку hello из hello **имя инициатора** поля.</span><span class="sxs-lookup"><span data-stu-id="02b18-133">In hello iSCSI Initiator Properties window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
    <span data-ttu-id="02b18-134">Вставьте эту строку в hello **IQN** в hello **Добавление ACR** колонку.</span><span class="sxs-lookup"><span data-stu-id="02b18-134">Paste this string in hello **IQN** field in hello **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="02b18-135">Нажмите кнопку **добавить** tooadd hello контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="02b18-135">Click **Add** tooadd hello ACR.</span></span>  
   
        ![Добавление записей контроля доступа](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="02b18-137">Здравствуйте, табличный список — это дополнение обновленные tooreflect.</span><span class="sxs-lookup"><span data-stu-id="02b18-137">hello tabular listing is updated tooreflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="02b18-138">Изменение записей ACR</span><span class="sxs-lookup"><span data-stu-id="02b18-138">Edit an ACR</span></span>

<span data-ttu-id="02b18-139">Использовать hello **записи управления доступом** колонки в hello **конфигурации** раздела в записи контроля доступа Azure портала tooedit hello службы диспетчера устройств.</span><span class="sxs-lookup"><span data-stu-id="02b18-139">You use hello **Access control records** blade within hello **Configuration** section of your Device Manager service in hello Azure portal tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="02b18-140">Не следует изменять записи контроля доступа, которые используются в настоящий момент.</span><span class="sxs-lookup"><span data-stu-id="02b18-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="02b18-141">tooedit записи управления Доступом, ассоциированный с томом, который используется в настоящий момент, вы должны сначала отключите hello тома.</span><span class="sxs-lookup"><span data-stu-id="02b18-141">tooedit an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>


<span data-ttu-id="02b18-142">Выполните hello, выполнив шаги tooedit записи управления Доступом.</span><span class="sxs-lookup"><span data-stu-id="02b18-142">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-acr"></a><span data-ttu-id="02b18-143">tooedit запись контроля доступа</span><span class="sxs-lookup"><span data-stu-id="02b18-143">tooedit an ACR</span></span>

1. <span data-ttu-id="02b18-144">На целевой странице службы hello, выберите службу, дважды щелкните hello имя службы и затем в hello **конфигурации** разделе **записи управления доступом**.</span><span class="sxs-lookup"><span data-stu-id="02b18-144">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="02b18-145">В hello **записи управления доступом** колонку из hello табличном списке записей управления доступом hello, дважды щелкните hello обратиться в toomodify контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="02b18-145">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="02b18-146">В hello **редактирование записи управления доступом** колонке hello следующие:</span><span class="sxs-lookup"><span data-stu-id="02b18-146">In hello **Edit access control records** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="02b18-147">Укажите hello IQN для hello контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="02b18-147">Supply hello IQN for hello ACR.</span></span>
   
    2. <span data-ttu-id="02b18-148">Нажмите кнопку **Сохранить** hello верхней части колонки toosave hello hello изменения записи управления Доступом.</span><span class="sxs-lookup"><span data-stu-id="02b18-148">Click **Save** at hello top of hello blade toosave hello modified ACR.</span></span> <span data-ttu-id="02b18-149">Появляется после сообщения о подтверждении hello:</span><span class="sxs-lookup"><span data-stu-id="02b18-149">You see hello following confirmation message:</span></span>
   
        ![Изменение записей контроля доступа](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="02b18-151">Удаление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="02b18-151">Delete an access control record</span></span>

<span data-ttu-id="02b18-152">Использовать hello **конфигурации** страницы в записи контроля доступа Azure портала toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="02b18-152">You use hello **Configuration** page in hello Azure portal toodelete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="02b18-153">Не следует удалять записи контроля доступа, которые используются в настоящий момент.</span><span class="sxs-lookup"><span data-stu-id="02b18-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="02b18-154">toodelete записи управления Доступом, ассоциированный с томом, который используется в настоящий момент, вы должны сначала отключите hello тома.</span><span class="sxs-lookup"><span data-stu-id="02b18-154">toodelete an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>
> * <span data-ttu-id="02b18-155">При удалении записи управления Доступом из тома, убедитесь, что соответствующий узел, hello не имеет доступа к hello тома, так как hello удаление может привести к прерыванию чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="02b18-155">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="02b18-156">Выполните hello, выполнив шаги toodelete записи управления доступом.</span><span class="sxs-lookup"><span data-stu-id="02b18-156">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="02b18-157">toodelete записи управления доступом</span><span class="sxs-lookup"><span data-stu-id="02b18-157">toodelete an access control record</span></span>

1. <span data-ttu-id="02b18-158">На целевой странице службы hello, выберите службу, дважды щелкните hello имя службы и затем в hello **конфигурации** разделе **записи управления доступом**.</span><span class="sxs-lookup"><span data-stu-id="02b18-158">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="02b18-159">В hello **записи управления доступом** колонку из hello табличном списке записей управления доступом hello, дважды щелкните hello обратиться в toodelete контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="02b18-159">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toodelete.</span></span>

3. <span data-ttu-id="02b18-160">В колонке записей управления доступом редактирования hello, нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="02b18-160">In hello Edit access control records blade, click **Delete**.</span></span>
   
    ![Удаление записей контроля доступа](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="02b18-162">При появлении запроса на подтверждение нажмите кнопку **удаление** toocontinue с удалением hello.</span><span class="sxs-lookup"><span data-stu-id="02b18-162">When prompted for confirmation, click **Delete** toocontinue with hello deletion.</span></span> <span data-ttu-id="02b18-163">Табличный список Hello является обновленные tooreflect hello удаления.</span><span class="sxs-lookup"><span data-stu-id="02b18-163">hello tabular listing is updated tooreflect hello deletion.</span></span>
   
   ![Предупреждение](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="02b18-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02b18-165">Next steps</span></span>

* <span data-ttu-id="02b18-166">[Сведения о добавлении томов и настройке записей ACR](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)</span><span class="sxs-lookup"><span data-stu-id="02b18-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

