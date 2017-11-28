---
title: "Отработка отказа и аварийное восстановление для устройств StorSimple серии 8000 | Документация Майкрософт"
description: "Узнайте, как выполнять отработку отказа устройства StorSimple на то же устройство."
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: acc8929dc3476e9590e8e4d9526b38b7c0719570
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-your-storsimple-physical-device-to-same-device"></a><span data-ttu-id="41773-103">Отработка отказа физического устройства StorSimple на то же устройство</span><span class="sxs-lookup"><span data-stu-id="41773-103">Fail over your StorSimple physical device to same device</span></span>

## <a name="overview"></a><span data-ttu-id="41773-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="41773-104">Overview</span></span>

<span data-ttu-id="41773-105">В этом руководстве описаны шаги, необходимые для отработки отказа физического устройства StorSimple серии 8000 на то же устройство в случае аварии.</span><span class="sxs-lookup"><span data-stu-id="41773-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to itself if there is a disaster.</span></span> <span data-ttu-id="41773-106">StorSimple использует функцию отработки отказа устройства для переноса данных с исходного физического устройства в центре обработки данных на другое физическое устройство.</span><span class="sxs-lookup"><span data-stu-id="41773-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to another physical device.</span></span> <span data-ttu-id="41773-107">Рекомендации в этом руководстве относятся к физическим устройствам StorSimple серии 8000 под управлением версий программного обеспечения с обновлением 3 и более поздних.</span><span class="sxs-lookup"><span data-stu-id="41773-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="41773-108">Чтобы узнать больше об отработке отказа устройств и его использовании для восстановления после аварии, см. статью [Failover and disaster recovery for your StorSimple 8000 series device](storsimple-8000-device-failover-disaster-recovery.md) (Отработка отказа и аварийное восстановление для устройств StorSimple серии 8000).</span><span class="sxs-lookup"><span data-stu-id="41773-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="41773-109">Сведения об отработке отказа с одного физического устройства на другое физическое устройство см. в статье [Fail over to a StorSimple 8000 series physical device](storsimple-8000-device-failover-physical-device.md) (Отработка отказа на то же физическое устройство StorSimple серии 8000).</span><span class="sxs-lookup"><span data-stu-id="41773-109">To fail over a physical device to another physical device, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="41773-110">Сведения об отработке отказа физического устройства StorSimple на облачное устройство StorSimple см. в статье [Fail over to your StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md) (Отработка отказа на облачное устройство StorSimple).</span><span class="sxs-lookup"><span data-stu-id="41773-110">To fail over a StorSimple physical device to a StorSimple Cloud Appliance, go to [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="41773-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="41773-111">Prerequisites</span></span>

- <span data-ttu-id="41773-112">Обязательно ознакомьтесь с рекомендациями по отработке отказа устройств.</span><span class="sxs-lookup"><span data-stu-id="41773-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="41773-113">Дополнительные сведения см. в статье с [общими рекомендациями по отработке отказа устройств](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="41773-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-to-fail-over-to-the-same-device"></a><span data-ttu-id="41773-114">Шаги по отработке отказа на то же устройство</span><span class="sxs-lookup"><span data-stu-id="41773-114">Steps to fail over to the same device</span></span>

<span data-ttu-id="41773-115">Если необходимо выполнить отработку отказа на то же устройство, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="41773-115">Perform the following steps if you need to fail over to the same device.</span></span>

1. <span data-ttu-id="41773-116">Создайте облачные моментальные снимки всех томов на устройстве.</span><span class="sxs-lookup"><span data-stu-id="41773-116">Take cloud snapshots of all the volumes in your device.</span></span> <span data-ttu-id="41773-117">Дополнительные сведения см. в статье [Use the StorSimple Device Manager service in Azure portal to manage backup policies](storsimple-8000-manage-backup-policies-u2.md) (Использование службы диспетчера устройств StorSimple на портале Azure для управления политиками резервного копирования).</span><span class="sxs-lookup"><span data-stu-id="41773-117">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="41773-118">Восстановите параметры устройства по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="41773-118">Reset your device to factory defaults.</span></span> <span data-ttu-id="41773-119">Выполните подробные инструкции по [восстановлению параметров по умолчанию для устройства StorSimple](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="41773-119">Follow the detailed instructions in [how to reset a StorSimple device to factory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="41773-120">Перейдите к службе диспетчера устройств StorSimple, а затем выберите **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="41773-120">Go to the StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="41773-121">В колонке **Устройства** для старого устройства должно отображаться состояние **Отключено**.</span><span class="sxs-lookup"><span data-stu-id="41773-121">In the **Devices** blade, the old device should show as **Offline**.</span></span>

    ![Исходное устройство не в сети](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="41773-123">Настройте устройство и снова зарегистрируйте его в службе диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41773-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="41773-124">У только что зарегистрированного устройства отображается состояние **Готово к настройке**.</span><span class="sxs-lookup"><span data-stu-id="41773-124">The newly registered device should show as **Ready to set up**.</span></span> <span data-ttu-id="41773-125">Имя нового устройства такое же, что и у старого, но дополнено цифрой, чтобы обозначить, что устройство восстановлено до уровня заводских настроек и зарегистрировано снова.</span><span class="sxs-lookup"><span data-stu-id="41773-125">The device name for the new device is the same as the old device but appended with a numeral to indicate that the device was reset to factory default and registered again.</span></span>

    ![Только что зарегистрированное устройство готово к настройке](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="41773-127">Нужно выполнить настройку нового устройства.</span><span class="sxs-lookup"><span data-stu-id="41773-127">For the new device, complete the device setup.</span></span> <span data-ttu-id="41773-128">Дополнительные сведения см. в разделе [Выполнение минимальной настройки устройства](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="41773-128">For more information, go to [Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="41773-129">В колонке **Устройства** состояние устройства изменится на **Включено**.</span><span class="sxs-lookup"><span data-stu-id="41773-129">On the **Devices** blade, the status of the device changes to **Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="41773-130">**Сначала выполните минимальную настройку, иначе аварийное восстановление может завершиться сбоем.**</span><span class="sxs-lookup"><span data-stu-id="41773-130">**Complete the minimum configuration first, or your DR may fail.**</span></span>

    ![Только что зарегистрированное устройство включено](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="41773-132">Выберите старое устройство (состояние "Отключено") и на панели команд щелкните **Отработка отказа**.</span><span class="sxs-lookup"><span data-stu-id="41773-132">Select the old device (status offline) and from the command bar, click **Fail over**.</span></span> <span data-ttu-id="41773-133">В колонке **Отработка отказа** выберите старое устройство в качестве источника, а новое устройство укажите в качестве целевого устройства.</span><span class="sxs-lookup"><span data-stu-id="41773-133">In the **Fail over** blade, select old device as the source and specify the target device as the newly registered device.</span></span>

    ![Сводка отработки отказа](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="41773-135">Подробные инструкции см. в разделе [Отработка отказа на другое физическое устройство](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="41773-135">For detailed instructions, refer to [Fail over to another physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="41773-136">Будет создано задание восстановления устройства, которое можно отслеживать в колонке **Задания**.</span><span class="sxs-lookup"><span data-stu-id="41773-136">A device restore job is created that you can monitor from the **Jobs** blade.</span></span>

8. <span data-ttu-id="41773-137">После успешного выполнения задания перейдите на новое устройство и откройте колонку **Контейнеры томов**.</span><span class="sxs-lookup"><span data-stu-id="41773-137">After the job has successfully completed, access the new device and navigate to the **Volume containers** blade.</span></span> <span data-ttu-id="41773-138">Убедитесь, что все контейнеры томов из старого устройства перенесены на новое устройство.</span><span class="sxs-lookup"><span data-stu-id="41773-138">Verify that all the volume containers from the old device have migrated to the new device.</span></span>

   ![Контейнеры томов перенесены](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="41773-140">После завершения отработки отказа старое устройство можно отключить и удалить с портала.</span><span class="sxs-lookup"><span data-stu-id="41773-140">After the failover is complete, you can deactivate and delete the old device from the portal.</span></span> <span data-ttu-id="41773-141">Выберите старое устройство (отключенное), щелкните его правой кнопкой мыши и выберите **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="41773-141">Select the old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="41773-142">После отключения устройства его состояние обновится.</span><span class="sxs-lookup"><span data-stu-id="41773-142">After the device is deactivated, the status of the device is updated.</span></span>

     ![Исходное устройство отключено](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="41773-144">Выберите отключенное устройство, щелкните его правой кнопкой мыши и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="41773-144">Select the deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="41773-145">Это удалит устройство из списка устройств.</span><span class="sxs-lookup"><span data-stu-id="41773-145">This deletes the device from the list of devices.</span></span>

    ![Исходное устройство удалено](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="41773-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="41773-147">Next steps</span></span>

* <span data-ttu-id="41773-148">После отработки отказа, возможно, нужно будет [отключить или удалить устройство StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="41773-148">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="41773-149">Сведения об использовании службы диспетчера устройств StorSimple см. в статье [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md) (Администрирование устройства StorSimple с помощью службы диспетчера устройств StorSimple).</span><span class="sxs-lookup"><span data-stu-id="41773-149">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

