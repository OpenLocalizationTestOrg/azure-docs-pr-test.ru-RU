---
title: "записи управления доступом aaaManage в StorSimple | Документы Microsoft"
description: "Описывает принципы управления доступом toouse записей toodetermine (ACR), какие узлы могут подключаться tooa тома на устройстве StorSimple hello."
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
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="4c6f7-103">Использовать записи управления доступом toomanage службы диспетчера StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="4c6f7-103">Use hello StorSimple Manager service toomanage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="4c6f7-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="4c6f7-104">Overview</span></span>
<span data-ttu-id="4c6f7-105">Записи управления доступом (ACR) позволяют toospecify, какие узлы могут подключаться tooa тома на устройстве StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="4c6f7-106">Записи контроля доступа задаются tooa томов и содержать hello iSCSI (IQN) полные имена узлов hello.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="4c6f7-107">Когда узел пытается tooconnect tooa тома, устройство hello проверяет hello контроля доступа, связанной с этим томом hello IQN-имя и если имеется соответствие, то hello подключения.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="4c6f7-108">записи управления доступом Hello раздела, посвященного hello **Настройка** странице отображаются все записи управления доступом hello с hello соответствующее IQN узлов hello.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-108">hello access control records section on hello **Configure** page displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="4c6f7-109">В этом учебнике описано следующие общие задачи, связанные с ACR hello:</span><span class="sxs-lookup"><span data-stu-id="4c6f7-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="4c6f7-110">Добавление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="4c6f7-110">Add an access control record</span></span> 
* <span data-ttu-id="4c6f7-111">Изменение записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="4c6f7-111">Edit an access control record</span></span> 
* <span data-ttu-id="4c6f7-112">Удаление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="4c6f7-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="4c6f7-113">При назначении томе tooa контроля доступа, будьте внимательны, что тома hello не имеет доступа к одновременно более чем одного некластеризованного узла, так как это может повредить том hello.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span> 
> * <span data-ttu-id="4c6f7-114">При удалении записи управления Доступом из тома, убедитесь, что соответствующий узел, hello не имеет доступа к hello тома, так как hello удаление может привести к прерыванию чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="4c6f7-115">Добавление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="4c6f7-115">Add an access control record</span></span>
<span data-ttu-id="4c6f7-116">Используйте службу диспетчера StorSimple hello **Настройка** страница tooadd записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-116">You use hello StorSimple Manager service **Configure** page tooadd ACRs.</span></span> <span data-ttu-id="4c6f7-117">Как правило, одной записи контроля доступа соответствует один том.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="4c6f7-118">Выполните hello, выполнив шаги tooadd записи управления Доступом.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-118">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-access-control-record"></a><span data-ttu-id="4c6f7-119">tooadd записи управления доступом</span><span class="sxs-lookup"><span data-stu-id="4c6f7-119">tooadd an access control record</span></span>
1. <span data-ttu-id="4c6f7-120">На целевой странице службы hello, выберите службу, дважды щелкните имя службы hello и нажмите кнопку hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-120">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="4c6f7-121">В hello табличный список в разделе **записи управления доступом**указывайте **имя** для этой записи управления Доступом.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-121">In hello tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="4c6f7-122">Укажите имя hello IQN узла Windows под **имя инициатора iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-122">Provide hello IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="4c6f7-123">hello tooget IQN узла Windows Server, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="4c6f7-123">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
   * <span data-ttu-id="4c6f7-124">Запустите инициатор Microsoft iSCSI hello на узле Windows.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-124">Start hello Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="4c6f7-125">В hello **свойства инициатора iSCSI** в hello окна **конфигурации** выберите и скопируйте строку hello из hello **имя инициатора** поля.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-125">In hello **iSCSI Initiator Properties** window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
   * <span data-ttu-id="4c6f7-126">Вставьте эту строку в hello **имя инициатора iSCSI** на таблицу ACR hello в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-126">Paste this string in hello **iSCSI Initiator Name** field on hello ACRs table in hello Azure classic portal.</span></span>
4. <span data-ttu-id="4c6f7-127">Нажмите кнопку **Сохранить** toosave hello вновь созданные записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-127">Click **Save** toosave hello newly created ACR.</span></span> <span data-ttu-id="4c6f7-128">Hello табличный список будет иметь обновленные tooreflect это дополнение.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-128">hello tabular listing will be updated tooreflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="4c6f7-129">Изменение записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="4c6f7-129">Edit an access control record</span></span>
<span data-ttu-id="4c6f7-130">Использовать hello **Настройка** страницу приветствия записи контроля доступа Azure tooedit классического портала.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-130">You use hello **Configure** page in hello Azure classic portal tooedit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="4c6f7-131">Можно изменить только те записи контроля доступа, которые в настоящее время не используются.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="4c6f7-132">tooedit записи управления Доступом, ассоциированный с томом, который используется в настоящий момент, сначала нужно hello том вне сети.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-132">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="4c6f7-133">Выполните hello, выполнив шаги tooedit записи управления Доступом.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-133">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="4c6f7-134">tooedit записи управления доступом</span><span class="sxs-lookup"><span data-stu-id="4c6f7-134">tooedit an access control record</span></span>
1. <span data-ttu-id="4c6f7-135">На целевой странице службы hello, выберите службу, дважды щелкните имя службы hello и нажмите кнопку hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-135">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="4c6f7-136">В hello табличном списке записей управления доступом hello, наведите указатель мыши hello обратиться в toomodify контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-136">In hello tabular listing of hello access control records, hover over hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="4c6f7-137">Укажите новое имя и IQN для hello контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-137">Supply a new name and/or IQN for hello ACR.</span></span>
4. <span data-ttu-id="4c6f7-138">Нажмите кнопку **Сохранить** toosave hello изменения записи управления Доступом.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-138">Click **Save** toosave hello modified ACR.</span></span> <span data-ttu-id="4c6f7-139">Hello табличный список будет иметь обновленные tooreflect это изменение.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-139">hello tabular listing will be updated tooreflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="4c6f7-140">Удаление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="4c6f7-140">Delete an access control record</span></span>
<span data-ttu-id="4c6f7-141">Использовать hello **Настройка** страницу приветствия записи контроля доступа Azure toodelete классического портала.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-141">You use hello **Configure** page in hello Azure classic portal toodelete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="4c6f7-142">Можно удалять только те записи контроля доступа, которые в настоящее время не используются.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="4c6f7-143">toodelete записи управления Доступом, ассоциированный с томом, который используется в настоящий момент, сначала нужно hello том вне сети.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-143">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="4c6f7-144">Выполните hello, выполнив шаги toodelete записи управления доступом.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-144">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="4c6f7-145">toodelete записи управления доступом</span><span class="sxs-lookup"><span data-stu-id="4c6f7-145">toodelete an access control record</span></span>
1. <span data-ttu-id="4c6f7-146">На целевой странице службы hello, выберите службу, дважды щелкните имя службы hello и нажмите кнопку hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-146">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="4c6f7-147">В hello табличный список hello записи управления доступом (ACR), наведите указатель мыши hello обратиться в toodelete контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-147">In hello tabular listing of hello access control records (ACRs), hover over hello ACR that you wish toodelete.</span></span>
3. <span data-ttu-id="4c6f7-148">Значок удаления (**x**) будет отображаться в крайнем правом углу hello для контроля доступа, который выбран hello.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-148">A delete icon (**x**) will appear in hello extreme right column for hello ACR that you select.</span></span> <span data-ttu-id="4c6f7-149">Нажмите кнопку hello **x** hello toodelete значок контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-149">Click hello **x** icon toodelete hello ACR.</span></span>
4. <span data-ttu-id="4c6f7-150">При появлении запроса на подтверждение нажмите кнопку **Да** toocontinue с удалением hello.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-150">When prompted for confirmation, click **YES** toocontinue with hello deletion.</span></span> <span data-ttu-id="4c6f7-151">Hello табличный список будет обновленные tooreflect hello удаления.</span><span class="sxs-lookup"><span data-stu-id="4c6f7-151">hello tabular listing will be updated tooreflect hello deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c6f7-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4c6f7-152">Next steps</span></span>
* <span data-ttu-id="4c6f7-153">Узнайте больше об [управлении томами StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="4c6f7-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="4c6f7-154">Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4c6f7-154">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

