---
title: "Отключение и удаление устройства StorSimple серии 8000 | Документация Майкрософт"
description: "Описание процедуры вывода устройства StorSimple из эксплуатации путем его отключения и последующего удаления."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 3c00867a29cf8343a57e74e2aabe3971ae6837af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a><span data-ttu-id="f9018-103">Отключение и удаление устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="f9018-103">Deactivate and delete a StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="f9018-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f9018-104">Overview</span></span>

<span data-ttu-id="f9018-105">В этой статье описывается, как отключать и удалять устройства StorSimple, подключенные к службе диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f9018-105">This article describes how to deactivate and delete a StorSimple device that is connected to a StorSimple Device Manager service.</span></span> <span data-ttu-id="f9018-106">Рекомендации в этой статье применяются только к устройствам серии StorSimple серии 8000, включая облачные устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f9018-106">The guidance in this article applies only to StorSimple 8000 series devices including the StorSimple Cloud Appliances.</span></span> <span data-ttu-id="f9018-107">При использовании виртуального массива StorSimple перейдите к статье [Отключение и удаление виртуального массива StorSimple](storsimple-virtual-array-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="f9018-107">If you are using a StorSimple Virtual Array, then go to [Deactivate and delete a StorSimple Virtual Array](storsimple-virtual-array-deactivate-and-delete-device.md).</span></span>

<span data-ttu-id="f9018-108">Отключение обрывает соединение между устройством и соответствующей службой диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f9018-108">Deactivation severs the connection between the device and the corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="f9018-109">Вам может потребоваться вывести устройство StorSimple из эксплуатации (например при замене или обновлении устройства, либо если StorSimple больше не используется).</span><span class="sxs-lookup"><span data-stu-id="f9018-109">You may wish to take a StorSimple device out of service (for example, if you are replacing or upgrading your device or if you are no longer using StorSimple).</span></span> <span data-ttu-id="f9018-110">В этом случае необходимо отключить устройство перед его удалением.</span><span class="sxs-lookup"><span data-stu-id="f9018-110">If so, you need to deactivate the device before you can delete it.</span></span>

<span data-ttu-id="f9018-111">После отключения устройства все данные, хранящиеся в его внутренней памяти, станут недоступны.</span><span class="sxs-lookup"><span data-stu-id="f9018-111">When you deactivate a device, any data that was stored locally on the device is no longer accessible.</span></span> <span data-ttu-id="f9018-112">Восстановлению подлежат лишь связанные с устройством данные, хранящиеся в облаке.</span><span class="sxs-lookup"><span data-stu-id="f9018-112">Only the data associated with the device that was stored in the cloud can be recovered.</span></span>

> [!WARNING]
> <span data-ttu-id="f9018-113">Отключение является НЕОБРАТИМОЙ операцией.</span><span class="sxs-lookup"><span data-stu-id="f9018-113">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="f9018-114">Отключенное устройство нельзя зарегистрировать в службе диспетчера устройств StorSimple, пока оно не будет сброшено к заводским настройкам.</span><span class="sxs-lookup"><span data-stu-id="f9018-114">A deactivated device cannot be registered with the StorSimple Device Manager service unless it is reset to factory defaults.</span></span>
>
> <span data-ttu-id="f9018-115">Процедура возврата к заводским настройкам удаляет все данные, хранящиеся во внутренней памяти устройства.</span><span class="sxs-lookup"><span data-stu-id="f9018-115">The factory reset process deletes all the data that was stored locally on your device.</span></span> <span data-ttu-id="f9018-116">Таким образом необходимо создать облачный моментальный снимок всех данных перед отключением устройства.</span><span class="sxs-lookup"><span data-stu-id="f9018-116">Therefore, you must take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="f9018-117">Он позволит восстановить все данные в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="f9018-117">This cloud snapshot allows you to recover all the data at a later stage.</span></span>

<span data-ttu-id="f9018-118">После изучения этого учебника вы сможете сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="f9018-118">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="f9018-119">Отключить устройство и удалить данные.</span><span class="sxs-lookup"><span data-stu-id="f9018-119">Deactivate a device and delete the data.</span></span>
* <span data-ttu-id="f9018-120">Отключить устройство и сохранить данные.</span><span class="sxs-lookup"><span data-stu-id="f9018-120">Deactivate a device and retain the data.</span></span>

> [!NOTE]
> <span data-ttu-id="f9018-121">Перед отключением физического или облачного устройства StorSimple удалите зависящие от него клиенты и узлы или прекратите их работу.</span><span class="sxs-lookup"><span data-stu-id="f9018-121">Before you deactivate a StorSimple physical device or cloud appliance, stop or delete clients and hosts that depend on that device.</span></span>


## <a name="deactivate-and-delete-data"></a><span data-ttu-id="f9018-122">Отключение и удаление данных</span><span class="sxs-lookup"><span data-stu-id="f9018-122">Deactivate and delete data</span></span>

<span data-ttu-id="f9018-123">Если вам требуется полностью удалить устройство без сохранения данных на нем, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="f9018-123">If you are interested in deleting the device completely and do not want to retain the data on the device, then complete the following steps.</span></span>

#### <a name="to-deactivate-the-device-and-delete-the-data"></a><span data-ttu-id="f9018-124">Отключение устройства и удаление данных</span><span class="sxs-lookup"><span data-stu-id="f9018-124">To deactivate the device and delete the data</span></span>

1. <span data-ttu-id="f9018-125">Перед отключением устройства вам потребуется удалить все контейнеры томов (и сами тома), связанные с устройством.</span><span class="sxs-lookup"><span data-stu-id="f9018-125">Before you deactivate a device, you must delete all the volume containers (and the volumes) associated with the device.</span></span> <span data-ttu-id="f9018-126">Контейнеры томов можно удалить только после удаления связанных резервных копий.</span><span class="sxs-lookup"><span data-stu-id="f9018-126">You can delete volume containers only after you have deleted the associated backups.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9018-127">Перед отключением физического или облачного устройства StorSimple убедитесь, что все данные из удаленного контейнера томов фактически удалены с устройства.</span><span class="sxs-lookup"><span data-stu-id="f9018-127">Before you deactivate a StorSimple physical device or cloud appliance, ensure that the data from the deleted volume container is actually deleted from the device.</span></span> <span data-ttu-id="f9018-128">Вы можете отслеживать диаграммы потребления облачных ресурсов и, обнаружив снижение уровня потребления в результате удаления резервных копий, можете отключить устройство.</span><span class="sxs-lookup"><span data-stu-id="f9018-128">You can monitor the cloud consumption charts and when you see the cloud usage drop because of the backups you have deleted, then you can proceed to deactivate the device.</span></span> <span data-ttu-id="f9018-129">Если отключить устройство до этого снижения, данные останутся в учетной записи хранения и за них будет начисляться плата.</span><span class="sxs-lookup"><span data-stu-id="f9018-129">If you deactivate the device before this drop occurs, the data is stranded in the storage account and accrues charges.</span></span>

2. <span data-ttu-id="f9018-130">Отключите устройство, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f9018-130">Deactivate the device as follows:</span></span>
   
   1. <span data-ttu-id="f9018-131">В службе диспетчера устройств StorSimple выберите **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="f9018-131">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="f9018-132">В колонке **Устройства** выберите устройство, которое необходимо отключить, щелкните правой кнопкой мыши и выберите **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="f9018-132">In the **Devices** blade, select the device that you wish to deactivate, right-click, and then click **Deactivate**.</span></span>

        ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. <span data-ttu-id="f9018-134">В колонке **Отключение** введите имя устройства для подтверждения и щелкните **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="f9018-134">In the **Deactivate** blade, type the device name to confirm and then click **Deactivate**.</span></span> <span data-ttu-id="f9018-135">Начнется процесс отключения, который займет несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f9018-135">The deactivate process starts and takes a few minutes to complete.</span></span>

        ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. <span data-ttu-id="f9018-137">После отключения вы можете полностью удалить устройство.</span><span class="sxs-lookup"><span data-stu-id="f9018-137">After deactivation, you can delete the device completely.</span></span> <span data-ttu-id="f9018-138">При этом устройство удаляется из списка устройств, подключенных к службе.</span><span class="sxs-lookup"><span data-stu-id="f9018-138">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="f9018-139">После удаления устройства служба больше не сможет управлять им.</span><span class="sxs-lookup"><span data-stu-id="f9018-139">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="f9018-140">Вот как можно удалить устройство:</span><span class="sxs-lookup"><span data-stu-id="f9018-140">Use the following steps to delete the device:</span></span>
   
   1. <span data-ttu-id="f9018-141">В службе диспетчера устройств StorSimple выберите **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="f9018-141">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="f9018-142">В колонке **Устройства** выберите отключенное устройство, которое необходимо удалить, щелкните правой кнопкой мыши и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="f9018-142">In the **Devices** blade, select the deactivated device that you wish to delete, right-click, and then click **Delete**.</span></span>

        ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. <span data-ttu-id="f9018-144">В колонке **Удаление** введите имя устройства для подтверждения и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="f9018-144">In the **Delete** blade, type the device name to confirm and then click **Delete**.</span></span> <span data-ttu-id="f9018-145">Удаление занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f9018-145">The deletion takes a few minutes to complete.</span></span>

        ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. <span data-ttu-id="f9018-147">После успешного удаления вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="f9018-147">After the deletion is successfully complete, you are notified.</span></span> <span data-ttu-id="f9018-148">Список также будет обновлен с учетом удаления.</span><span class="sxs-lookup"><span data-stu-id="f9018-148">The device list also updates to reflect the deletion.</span></span>

## <a name="deactivate-and-retain-data"></a><span data-ttu-id="f9018-149">Отключение и сохранение данных</span><span class="sxs-lookup"><span data-stu-id="f9018-149">Deactivate and retain data</span></span>

<span data-ttu-id="f9018-150">Если вам требуется удалить устройство и сохранить данные на нем, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="f9018-150">If you are interested in deleting the device but want to retain the data, then complete the following steps:</span></span>

#### <a name="to-deactivate-a-device-and-retain-the-data"></a><span data-ttu-id="f9018-151">Отключение устройства и сохранение данных</span><span class="sxs-lookup"><span data-stu-id="f9018-151">To deactivate a device and retain the data</span></span>
1. <span data-ttu-id="f9018-152">Отключите устройство.</span><span class="sxs-lookup"><span data-stu-id="f9018-152">Deactivate the device.</span></span> <span data-ttu-id="f9018-153">Все контейнеры томов и моментальные снимки на устройстве сохраняются.</span><span class="sxs-lookup"><span data-stu-id="f9018-153">All the volume containers and the snapshots of the device remain.</span></span>
   
   1. <span data-ttu-id="f9018-154">В службе диспетчера устройств StorSimple выберите **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="f9018-154">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="f9018-155">В колонке **Устройства** выберите устройство, которое необходимо отключить, щелкните правой кнопкой мыши и выберите **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="f9018-155">In the **Devices** blade, select the device that you wish to deactivate, right-click, and then click **Deactivate**.</span></span>

         ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. <span data-ttu-id="f9018-157">В колонке **Отключение** введите имя устройства для подтверждения и щелкните **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="f9018-157">In the **Deactivate** blade, type the device name to confirm and then click **Deactivate**.</span></span> <span data-ttu-id="f9018-158">Начнется процесс отключения, который займет несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f9018-158">The deactivate process starts and takes a few minutes to complete.</span></span>

         ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. <span data-ttu-id="f9018-160">Теперь вы можете выполнить отработку отказа для контейнеров томов и связанных моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="f9018-160">You can now fail over the volume containers and the associated snapshots.</span></span> <span data-ttu-id="f9018-161">Сведения о том, как это сделать, см. в статье [Отработка отказа и аварийное восстановление для устройства StorSimple](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="f9018-161">For procedures, go to [Failover and disaster recovery for your StorSimple device](storsimple-8000-device-failover-disaster-recovery.md).</span></span>
3. <span data-ttu-id="f9018-162">После отключения и отработки отказа вы можете полностью удалить устройство.</span><span class="sxs-lookup"><span data-stu-id="f9018-162">After deactivation and failover, you can delete the device completely.</span></span> <span data-ttu-id="f9018-163">При этом устройство удаляется из списка устройств, подключенных к службе.</span><span class="sxs-lookup"><span data-stu-id="f9018-163">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="f9018-164">После удаления устройства служба больше не сможет управлять им.</span><span class="sxs-lookup"><span data-stu-id="f9018-164">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="f9018-165">Чтобы удалить устройство, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f9018-165">To delete the device, complete the following steps:</span></span>
   
   1. <span data-ttu-id="f9018-166">В службе диспетчера устройств StorSimple выберите **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="f9018-166">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="f9018-167">В колонке **Устройства** выберите отключенное устройство, которое необходимо удалить, щелкните правой кнопкой мыши и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="f9018-167">In the **Devices** blade, select the deactivated device that you wish to delete, right-click, and then click **Delete**.</span></span>

       ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. <span data-ttu-id="f9018-169">В колонке **Удаление** введите имя устройства для подтверждения и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="f9018-169">In the **Delete** blade, type the device name to confirm and then click **Delete**.</span></span> <span data-ttu-id="f9018-170">Удаление занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f9018-170">The deletion takes a few minutes to complete.</span></span>

       ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. <span data-ttu-id="f9018-172">После успешного удаления вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="f9018-172">After the deletion is successfully complete, you are notified.</span></span> <span data-ttu-id="f9018-173">Список также будет обновлен с учетом удаления.</span><span class="sxs-lookup"><span data-stu-id="f9018-173">The device list also updates to reflect the deletion.</span></span>

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a><span data-ttu-id="f9018-174">Отключение и удаление облачного устройства</span><span class="sxs-lookup"><span data-stu-id="f9018-174">Deactivate and delete a cloud appliance</span></span>

<span data-ttu-id="f9018-175">Отключение облачного устройства StorSimple с портала освобождает и удаляет виртуальную машину, а также ресурсы, созданные при ее подготовке.</span><span class="sxs-lookup"><span data-stu-id="f9018-175">For a StorSimple Cloud Appliance, deactivation from the portal deallocates and deletes the virtual machine, and the resources created when it was provisioned.</span></span> <span data-ttu-id="f9018-176">После деактивации облачного устройства его невозможно вернуть в предыдущее состояние.</span><span class="sxs-lookup"><span data-stu-id="f9018-176">After the cloud appliance is deactivated, it cannot be restored to its previous state.</span></span>

![Отключение облачного устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

<span data-ttu-id="f9018-178">Отключение приводит к следующим результатам:</span><span class="sxs-lookup"><span data-stu-id="f9018-178">Deactivation results in the following actions:</span></span>

* <span data-ttu-id="f9018-179">Облачное устройство StorSimple удаляется из службы.</span><span class="sxs-lookup"><span data-stu-id="f9018-179">The StorSimple Cloud Appliance is removed from the service.</span></span>
* <span data-ttu-id="f9018-180">Виртуальная машина для облачного устройства StorSimple удаляется.</span><span class="sxs-lookup"><span data-stu-id="f9018-180">The virtual machine for the StorSimple Cloud Appliance is deleted.</span></span>
* <span data-ttu-id="f9018-181">Диск ОС и диски данных, созданные для облачного устройства StorSimple, будут удалены.</span><span class="sxs-lookup"><span data-stu-id="f9018-181">The OS disk and data disks created for the StorSimple Cloud Appliance are removed.</span></span>
* <span data-ttu-id="f9018-182">Размещенная служба и виртуальная сеть, созданные во время подготовки к работе, будут сохранены.</span><span class="sxs-lookup"><span data-stu-id="f9018-182">The hosted service and Virtual Network that were created during provisioning are retained.</span></span> <span data-ttu-id="f9018-183">Если вы их не используете их, удалите их вручную.</span><span class="sxs-lookup"><span data-stu-id="f9018-183">If you are not using these entities, you should delete them manually.</span></span>
* <span data-ttu-id="f9018-184">Облачные моментальные снимки, созданные облачным устройством StorSimple, будут сохранены.</span><span class="sxs-lookup"><span data-stu-id="f9018-184">Cloud snapshots created by the StorSimple Cloud Appliance are retained.</span></span>

<span data-ttu-id="f9018-185">После отключения облачного устройства его можно удалить из списка устройств.</span><span class="sxs-lookup"><span data-stu-id="f9018-185">After the cloud appliance is deactivated, you can delete it from the list of devices.</span></span> <span data-ttu-id="f9018-186">Выберите отключенное устройство, щелкните правой кнопкой мыши и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="f9018-186">Select the deactivated device, right-click, and then click **Delete**.</span></span> <span data-ttu-id="f9018-187">StorSimple уведомит вас об удалении устройства, и список устройств обновится.</span><span class="sxs-lookup"><span data-stu-id="f9018-187">StorSimple notifies you once the device is deleted and the list of devices updates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9018-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f9018-188">Next steps</span></span>

* <span data-ttu-id="f9018-189">Сведения о том, как восстановить на отключенном устройстве заводские параметры, см. в разделе [Восстановление на устройстве заводских настроек](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="f9018-189">To restore the deactivated device to factory defaults, go to [Reset the device to factory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
* <span data-ttu-id="f9018-190">Чтобы получить техническую поддержку, [обратитесь в службу поддержки Майкрософт](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="f9018-190">For technical assistance, [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="f9018-191">Дополнительные сведения об управлении устройством с помощью службы диспетчера устройств StorSimple см. в статье [Использование службы диспетчера устройств StorSimple для администрирования устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f9018-191">To learn more about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

