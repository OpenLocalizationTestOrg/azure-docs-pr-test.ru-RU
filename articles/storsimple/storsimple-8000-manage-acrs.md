---
title: "записи управления доступом aaaManage в StorSimple | Документы Microsoft"
description: "Описывает принципы управления доступом toouse записей toodetermine (ACR), какие узлы могут подключаться tooa тома на устройстве StorSimple hello."
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
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="55519-103">Использовать записи управления доступом toomanage службы диспетчера StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="55519-103">Use hello StorSimple Manager service toomanage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="55519-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="55519-104">Overview</span></span>
<span data-ttu-id="55519-105">Записи управления доступом (ACR) позволяют toospecify, какие узлы могут подключаться tooa тома на устройстве StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="55519-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="55519-106">Записи контроля доступа задаются tooa томов и содержать hello iSCSI (IQN) полные имена узлов hello.</span><span class="sxs-lookup"><span data-stu-id="55519-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="55519-107">Когда узел пытается tooconnect tooa тома, устройство hello проверяет hello контроля доступа, связанной с этим томом hello IQN-имя и если имеется соответствие, то hello подключения.</span><span class="sxs-lookup"><span data-stu-id="55519-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="55519-108">Здравствуйте, записи управления доступом в hello **конфигурации** части колонки службы вашего устройства StorSimple отобразить все записи управления доступом hello с hello соответствующее IQN узлов hello.</span><span class="sxs-lookup"><span data-stu-id="55519-108">hello access control records in hello **Configuration** section of your StorSimple Device Manager service blade display all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="55519-109">В этом учебнике описано следующие общие задачи, связанные с ACR hello:</span><span class="sxs-lookup"><span data-stu-id="55519-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="55519-110">Добавление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="55519-110">Add an access control record</span></span>
* <span data-ttu-id="55519-111">Изменение записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="55519-111">Edit an access control record</span></span>
* <span data-ttu-id="55519-112">Удаление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="55519-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="55519-113">При назначении томе tooa контроля доступа, будьте внимательны, что тома hello не имеет доступа к одновременно более чем одного некластеризованного узла, так как это может повредить том hello.</span><span class="sxs-lookup"><span data-stu-id="55519-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="55519-114">При удалении записи управления Доступом из тома, убедитесь, что соответствующий узел, hello не имеет доступа к hello тома, так как hello удаление может привести к прерыванию чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="55519-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>

## <a name="get-hello-iqn"></a><span data-ttu-id="55519-115">Получение IQN hello</span><span class="sxs-lookup"><span data-stu-id="55519-115">Get hello IQN</span></span>

<span data-ttu-id="55519-116">Выполните следующие шаги tooget hello IQN узла Windows под управлением Windows Server 2012 hello.</span><span class="sxs-lookup"><span data-stu-id="55519-116">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="55519-117">Добавление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="55519-117">Add an access control record</span></span>
<span data-ttu-id="55519-118">Использовать hello **конфигурации** раздел в колонке службы tooadd записи контроля доступа для hello устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="55519-118">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooadd ACRs.</span></span> <span data-ttu-id="55519-119">Как правило, одной записи контроля доступа соответствует один том.</span><span class="sxs-lookup"><span data-stu-id="55519-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="55519-120">Выполните hello, выполнив шаги tooadd записи управления Доступом.</span><span class="sxs-lookup"><span data-stu-id="55519-120">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="55519-121">tooadd запись контроля доступа</span><span class="sxs-lookup"><span data-stu-id="55519-121">tooadd an ACR</span></span>

1. <span data-ttu-id="55519-122">Go tooyour службы диспетчера StorSimple устройство, дважды щелкните hello имя службы и затем в hello **конфигурации** щелкните **записи управления доступом**.</span><span class="sxs-lookup"><span data-stu-id="55519-122">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="55519-123">В hello **записи управления доступом** колонка, щелкните **+ добавить запись контроля доступа**.</span><span class="sxs-lookup"><span data-stu-id="55519-123">In hello **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Щелкните "Добавить запись контроля доступа"](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="55519-125">В hello **Добавление ACR** колонке hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="55519-125">In hello **Add ACR** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="55519-126">Введите имя для записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="55519-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="55519-127">Укажите имя hello IQN узла Windows Server в поле **имя инициатора (IQN) iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="55519-127">Provide hello IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="55519-128">Нажмите кнопку **добавить** toocreate hello контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="55519-128">Click **Add** toocreate hello ACR.</span></span>

        ![Щелкните "Добавить запись контроля доступа"](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="55519-130">Hello недавно добавленный ACR будут отображаться в табличном списке записей контроля доступа hello.</span><span class="sxs-lookup"><span data-stu-id="55519-130">hello newly added ACR will display in hello tabular listing of ACRs.</span></span>

    ![Щелкните "Добавить запись контроля доступа"](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="55519-132">Изменение записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="55519-132">Edit an access control record</span></span>
<span data-ttu-id="55519-133">Использовать hello **конфигурации** раздел в колонке службы tooedit записи контроля доступа для hello устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="55519-133">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="55519-134">Мы рекомендуем изменять только те записи, которые сейчас не используются.</span><span class="sxs-lookup"><span data-stu-id="55519-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="55519-135">tooedit записи управления Доступом, ассоциированный с томом, который используется в настоящий момент, сначала нужно hello том вне сети.</span><span class="sxs-lookup"><span data-stu-id="55519-135">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="55519-136">Выполните hello, выполнив шаги tooedit записи управления Доступом.</span><span class="sxs-lookup"><span data-stu-id="55519-136">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="55519-137">tooedit записи управления доступом</span><span class="sxs-lookup"><span data-stu-id="55519-137">tooedit an access control record</span></span>
1.  <span data-ttu-id="55519-138">Go tooyour службы диспетчера StorSimple устройство, дважды щелкните hello имя службы и затем в hello **конфигурации** щелкните **записи управления доступом**.</span><span class="sxs-lookup"><span data-stu-id="55519-138">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Go tooaccess управления записей](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="55519-140">В hello табличном списке записей управления доступом hello, щелкните и выберите записи контроля доступа, что вы хотите toomodify hello.</span><span class="sxs-lookup"><span data-stu-id="55519-140">In hello tabular listing of hello access control records, click and select hello ACR that you wish toomodify.</span></span>

    ![Изменение записей контроля доступа](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="55519-142">В hello **редактирование записи контроля доступа** колонки, укажите другой узел соответствующий tooanother IQN.</span><span class="sxs-lookup"><span data-stu-id="55519-142">In hello **Edit access control record** blade, provide a different IQN corresponding tooanother host.</span></span>

    ![Изменение записей контроля доступа](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="55519-144">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="55519-144">Click **Save**.</span></span> <span data-ttu-id="55519-145">При появлении запроса на подтверждение нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="55519-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Изменение записей контроля доступа](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="55519-147">Уведомляются при обновлении hello контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="55519-147">You are notified when hello ACR is updated.</span></span> <span data-ttu-id="55519-148">Табличный список Hello также обновляет tooreflect hello изменений.</span><span class="sxs-lookup"><span data-stu-id="55519-148">hello tabular listing also updates tooreflect hello change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="55519-149">Удаление записи контроля доступа</span><span class="sxs-lookup"><span data-stu-id="55519-149">Delete an access control record</span></span>
<span data-ttu-id="55519-150">Использовать hello **конфигурации** раздел в колонке службы toodelete записи контроля доступа для hello устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="55519-150">You use hello **Configuration** section in hello StorSimple Device Manager service blade toodelete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="55519-151">Можно удалять только те записи контроля доступа, которые в настоящее время не используются.</span><span class="sxs-lookup"><span data-stu-id="55519-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="55519-152">toodelete записи управления Доступом, ассоциированный с томом, который используется в настоящий момент, сначала нужно hello том вне сети.</span><span class="sxs-lookup"><span data-stu-id="55519-152">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="55519-153">Выполните hello, выполнив шаги toodelete записи управления доступом.</span><span class="sxs-lookup"><span data-stu-id="55519-153">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="55519-154">toodelete записи управления доступом</span><span class="sxs-lookup"><span data-stu-id="55519-154">toodelete an access control record</span></span>
1.  <span data-ttu-id="55519-155">Go tooyour службы диспетчера StorSimple устройство, дважды щелкните hello имя службы и затем в hello **конфигурации** щелкните **записи управления доступом**.</span><span class="sxs-lookup"><span data-stu-id="55519-155">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Go tooaccess управления записей](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="55519-157">В hello табличном списке записей управления доступом hello, щелкните и выберите записи контроля доступа, что вы хотите toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="55519-157">In hello tabular listing of hello access control records, click and select hello ACR that you wish toodelete.</span></span>

    ![Go tooaccess управления записей](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="55519-159">Щелкните правой кнопкой мыши tooinvoke hello контекстное меню и выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="55519-159">Right-click tooinvoke hello context menu and select **Delete**.</span></span>

    ![Go tooaccess управления записей](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="55519-161">При появлении запроса на подтверждение, просмотрите сведения hello и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="55519-161">When prompted for confirmation, review hello information and then click **Delete**.</span></span>

    ![Go tooaccess управления записей](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="55519-163">Вы будете оповещены, после завершения удаления hello.</span><span class="sxs-lookup"><span data-stu-id="55519-163">You are notified when hello deletion completes.</span></span> <span data-ttu-id="55519-164">Табличный список Hello является обновленные tooreflect hello удаления.</span><span class="sxs-lookup"><span data-stu-id="55519-164">hello tabular listing is updated tooreflect hello deletion.</span></span>

    ![Go tooaccess управления записей](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="55519-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55519-166">Next steps</span></span>
* <span data-ttu-id="55519-167">Узнайте больше об [управлении томами StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="55519-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="55519-168">Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="55519-168">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

