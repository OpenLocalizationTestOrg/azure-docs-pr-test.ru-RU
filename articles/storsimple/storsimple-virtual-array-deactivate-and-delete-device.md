---
title: "aaaDeactivate и удаление виртуального массива Microsoft Azure StorSimple | Документы Microsoft"
description: "Описывает способ tooremove устройство StorSimple из службы, сначала отключить его, а затем удаляет его."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="a90d0-103">Отключение и удаление виртуального массива StorSimple</span><span class="sxs-lookup"><span data-stu-id="a90d0-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="a90d0-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a90d0-104">Overview</span></span>

<span data-ttu-id="a90d0-105">При отключении StorSimple Virtual Array hello связь между устройством hello и соответствующей службы диспетчера StorSimple устройство hello прерывается.</span><span class="sxs-lookup"><span data-stu-id="a90d0-105">When you deactivate a StorSimple Virtual Array, you break hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="a90d0-106">В этом учебнике объясняется, как выполнить такие задачи:</span><span class="sxs-lookup"><span data-stu-id="a90d0-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="a90d0-107">Отключение устройства</span><span class="sxs-lookup"><span data-stu-id="a90d0-107">Deactivate a device</span></span> 
* <span data-ttu-id="a90d0-108">Удаление отключенного устройства</span><span class="sxs-lookup"><span data-stu-id="a90d0-108">Delete a deactivated device</span></span>

<span data-ttu-id="a90d0-109">Hello информация в этой статье относится только tooStorSimple виртуальных массивов.</span><span class="sxs-lookup"><span data-stu-id="a90d0-109">hello information in this article applies tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="a90d0-110">Сведения о серии 8000 go toohow слишком[деактивировать или удалить устройство](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="a90d0-110">For information on 8000 series, go toohow too[deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-toodeactivate"></a><span data-ttu-id="a90d0-111">Когда toodeactivate?</span><span class="sxs-lookup"><span data-stu-id="a90d0-111">When toodeactivate?</span></span>

<span data-ttu-id="a90d0-112">Отключение является НЕОБРАТИМОЙ операцией.</span><span class="sxs-lookup"><span data-stu-id="a90d0-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="a90d0-113">Нельзя зарегистрировать деактивированное устройство с hello службы диспетчера StorSimple устройство еще раз.</span><span class="sxs-lookup"><span data-stu-id="a90d0-113">You cannot register a deactivated device with hello StorSimple Device Manager service again.</span></span> <span data-ttu-id="a90d0-114">Возможно требуется toodeactivate и удалите StorSimple Virtual Array в hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="a90d0-114">You may need toodeactivate and delete a StorSimple Virtual Array in hello following scenarios:</span></span>

* <span data-ttu-id="a90d0-115">**Переход на другой ресурс** : устройство находится в оперативном режиме и планирование toofail отказа устройства.</span><span class="sxs-lookup"><span data-stu-id="a90d0-115">**Planned failover** : Your device is online and you plan toofail over your device.</span></span> <span data-ttu-id="a90d0-116">Если вы планируете tooupgrade tooa больше устройств, может потребоваться toofail отказа устройства.</span><span class="sxs-lookup"><span data-stu-id="a90d0-116">If you are planning tooupgrade tooa larger device, you may need toofail over your device.</span></span> <span data-ttu-id="a90d0-117">После передачи hello право собственности на данные и завершения hello перехода на другой ресурс, hello исходное устройство удаляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="a90d0-117">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="a90d0-118">**Незапланированная отработка отказа** : устройство находится в автономном режиме, и требуется toofail по сравнению с устройства hello.</span><span class="sxs-lookup"><span data-stu-id="a90d0-118">**Unplanned failover** : Your device is offline and you need toofail over hello device.</span></span> <span data-ttu-id="a90d0-119">Данная ситуация может произойти при аварии, когда происходит сбой в центре обработки данных hello и основного устройства не работает.</span><span class="sxs-lookup"><span data-stu-id="a90d0-119">This scenario may occur during a disaster when there is an outage in hello datacenter and your primary device is down.</span></span> <span data-ttu-id="a90d0-120">При планировании toofail устройствами hello устройства tooa получателя.</span><span class="sxs-lookup"><span data-stu-id="a90d0-120">You plan toofail over hello device tooa secondary device.</span></span> <span data-ttu-id="a90d0-121">После передачи hello право собственности на данные и завершения hello перехода на другой ресурс, hello исходное устройство удаляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="a90d0-121">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="a90d0-122">**Списание** : необходимо toodecommission hello устройством.</span><span class="sxs-lookup"><span data-stu-id="a90d0-122">**Decommission** : You want toodecommission hello device.</span></span> <span data-ttu-id="a90d0-123">Для этого необходимо toofirst деактивировать устройство hello, а затем удалите его.</span><span class="sxs-lookup"><span data-stu-id="a90d0-123">This requires you toofirst deactivate hello device and then delete it.</span></span> <span data-ttu-id="a90d0-124">После отключения устройства все данные, хранящиеся локально, станут недоступны.</span><span class="sxs-lookup"><span data-stu-id="a90d0-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="a90d0-125">Вы можете только доступ и восстановление данных hello, хранящихся в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="a90d0-125">You can only access and recover hello data stored in hello cloud.</span></span> <span data-ttu-id="a90d0-126">Если планируется hello tookeep данные на устройстве после отключения, следует сделать снимок облачного всех данных перед отключением устройства.</span><span class="sxs-lookup"><span data-stu-id="a90d0-126">If you plan tookeep hello device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="a90d0-127">Этот моментальный снимок облака позволяет toorecover все hello данных в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="a90d0-127">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="a90d0-128">Отключение устройства</span><span class="sxs-lookup"><span data-stu-id="a90d0-128">Deactivate a device</span></span>

<span data-ttu-id="a90d0-129">toodeactivate устройства, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="a90d0-129">toodeactivate your device, perform hello following steps.</span></span>

#### <a name="toodeactivate-hello-device"></a><span data-ttu-id="a90d0-130">устройство toodeactivate hello</span><span class="sxs-lookup"><span data-stu-id="a90d0-130">toodeactivate hello device</span></span>

1. <span data-ttu-id="a90d0-131">В службе, перейдите слишком**управления > устройства**.</span><span class="sxs-lookup"><span data-stu-id="a90d0-131">In your service, go too**Management > Devices**.</span></span> <span data-ttu-id="a90d0-132">В hello **устройств** колонка, щелкните и обратиться в toodeactivate устройства выберите hello.</span><span class="sxs-lookup"><span data-stu-id="a90d0-132">In hello **Devices** blade, click and select hello device that you wish toodeactivate.</span></span>
   
    ![Выберите устройство toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="a90d0-134">В вашей **панели мониторинга устройства** колонка, щелкните **... Дополнительные** и выберите из списка hello **деактивировать**.</span><span class="sxs-lookup"><span data-stu-id="a90d0-134">In your **Device dashboard** blade, click **… More** and from hello list, select **Deactivate**.</span></span>
   
    ![Нажмите кнопку "Отключить"](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="a90d0-136">В hello **деактивировать** колонки, имя устройства типа hello и нажмите кнопку **деактивировать**.</span><span class="sxs-lookup"><span data-stu-id="a90d0-136">In hello **Deactivate** blade, type hello device name and then click **Deactivate**.</span></span> 
   
    ![Подтвердите отключение](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="a90d0-138">Hello отключить начинается процесс и занимает несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a90d0-138">hello deactivate process starts and takes a few minutes toocomplete.</span></span>
   
    ![Отключение выполняется](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="a90d0-140">После деактивации обновляет hello список устройств.</span><span class="sxs-lookup"><span data-stu-id="a90d0-140">After deactivation, hello list of devices refreshes.</span></span>
   
    ![Отключение завершено](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="a90d0-142">Теперь устройство можно удалить.</span><span class="sxs-lookup"><span data-stu-id="a90d0-142">You can now delete this device.</span></span>

## <a name="delete-hello-device"></a><span data-ttu-id="a90d0-143">Удаление устройства hello</span><span class="sxs-lookup"><span data-stu-id="a90d0-143">Delete hello device</span></span>

<span data-ttu-id="a90d0-144">Устройство имеет первый деактивированный toodelete toobe его.</span><span class="sxs-lookup"><span data-stu-id="a90d0-144">A device has toobe first deactivated toodelete it.</span></span> <span data-ttu-id="a90d0-145">При удалении устройства удаляется из списка hello службы toohello подключенных устройств.</span><span class="sxs-lookup"><span data-stu-id="a90d0-145">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="a90d0-146">Hello службы могут больше не сможете управлять hello удалить устройство.</span><span class="sxs-lookup"><span data-stu-id="a90d0-146">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="a90d0-147">Однако Hello данные, связанные с устройством hello остается в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="a90d0-147">hello data associated with hello device however remains in hello cloud.</span></span> <span data-ttu-id="a90d0-148">За эти данные будет взиматься плата.</span><span class="sxs-lookup"><span data-stu-id="a90d0-148">This data then accrues charges.</span></span>

<span data-ttu-id="a90d0-149">toodelete hello устройства, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="a90d0-149">toodelete hello device, perform hello following steps.</span></span>

#### <a name="toodelete-hello-device"></a><span data-ttu-id="a90d0-150">устройство toodelete hello</span><span class="sxs-lookup"><span data-stu-id="a90d0-150">toodelete hello device</span></span>

1. <span data-ttu-id="a90d0-151">В вашей StorSimple диспетчер устройств, перейдите в слишком**управления > устройства**.</span><span class="sxs-lookup"><span data-stu-id="a90d0-151">In your StorSimple Device Manager, go too**Management > Devices**.</span></span> <span data-ttu-id="a90d0-152">В hello **устройств** колонке выберите деактивированное устройство, что вы хотите toodelete.</span><span class="sxs-lookup"><span data-stu-id="a90d0-152">In hello **Devices** blade, select a deactivated device that you wish toodelete.</span></span>
2. <span data-ttu-id="a90d0-153">В hello **панели мониторинга устройства** колонка, щелкните **... Дополнительные** и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="a90d0-153">In hello **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Выберите устройство toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="a90d0-155">В hello **удаление** колонки, имя типа hello удалять hello tooconfirm устройства и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="a90d0-155">In hello **Delete** blade, type hello name of your device tooconfirm hello deletion and then click **Delete**.</span></span> <span data-ttu-id="a90d0-156">Идет удаление устройства hello не удаляет hello облачные данные, связанные с устройством hello.</span><span class="sxs-lookup"><span data-stu-id="a90d0-156">Deleting hello device does not delete hello cloud data associated with hello device.</span></span> 
   
   ![Подтверждение удаления](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="a90d0-158">Удаление Hello запускается, занимающий toocomplete несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a90d0-158">hello deletion starts and takes a few minutes toocomplete.</span></span>
   
   ![Удаление выполняется](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="a90d0-160">После удаления устройства hello, можно просмотреть hello обновить список устройств.</span><span class="sxs-lookup"><span data-stu-id="a90d0-160">After hello device is deleted, you can view hello updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a90d0-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a90d0-161">Next steps</span></span>

* <span data-ttu-id="a90d0-162">Сведения о том, как toofail, перейти слишком[отработки отказа и аварийного восстановления виртуального массива StorSimple](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="a90d0-162">For information on how toofail over, go too[Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="a90d0-163">Дополнительные сведения о toolearn как hello toouse службы диспетчера StorSimple устройство go слишком[используйте hello tooadminister службы диспетчера StorSimple устройство виртуального массива StorSimple](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a90d0-163">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

