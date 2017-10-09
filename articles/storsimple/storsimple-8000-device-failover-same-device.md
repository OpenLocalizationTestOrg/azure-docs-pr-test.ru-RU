---
title: "При сбое aaaStorSimple, аварийное восстановление для устройств серии 8000 | Документы Microsoft"
description: "Узнайте, как toofail по вашей toohello устройства StorSimple одного устройства."
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
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a><span data-ttu-id="64bf5-103">При сбое устройства toosame физического устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="64bf5-103">Fail over your StorSimple physical device toosame device</span></span>

## <a name="overview"></a><span data-ttu-id="64bf5-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="64bf5-104">Overview</span></span>

<span data-ttu-id="64bf5-105">В данном учебнике требуется toofail hello действия над tooitself физического устройства серии StorSimple 8000 при аварии.</span><span class="sxs-lookup"><span data-stu-id="64bf5-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooitself if there is a disaster.</span></span> <span data-ttu-id="64bf5-106">StorSimple использует данные hello устройства отработки отказа компонентов toomigrate из источника физического устройства в hello datacenter tooanother физического устройства.</span><span class="sxs-lookup"><span data-stu-id="64bf5-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooanother physical device.</span></span> <span data-ttu-id="64bf5-107">руководство Hello в этом учебнике применяется tooStorSimple 8000 ряда физических устройств под управлением версий программного обеспечения обновления 3 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="64bf5-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="64bf5-108">toolearn Дополнительные сведения о отработки отказа устройства и как она используется toorecover после аварии, go слишком[отработки отказа и аварийного восстановления для устройства серии StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="64bf5-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="64bf5-109">toofail на физическое устройство tooanother физическое устройство, перейдите в слишком[при сбое toohello же физических устройств StorSimple](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="64bf5-109">toofail over a physical device tooanother physical device, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="64bf5-110">toofail над tooa физическое устройство StorSimple облачному устройству StorSimple, перейдите в слишком[tooa StorSimple Appliance облака при сбое](storsimple-8000-device-failover-cloud-appliance.md).</span><span class="sxs-lookup"><span data-stu-id="64bf5-110">toofail over a StorSimple physical device tooa StorSimple Cloud Appliance, go too[Fail over tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="64bf5-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="64bf5-111">Prerequisites</span></span>

- <span data-ttu-id="64bf5-112">Убедитесь, можно ознакомиться с разделом hello рекомендации для обработки отказа устройства.</span><span class="sxs-lookup"><span data-stu-id="64bf5-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="64bf5-113">Дополнительные сведения см. слишком[Общие рекомендации для обработки отказа устройства](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="64bf5-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-toofail-over-toohello-same-device"></a><span data-ttu-id="64bf5-114">Toofail действия над toohello одного устройства</span><span class="sxs-lookup"><span data-stu-id="64bf5-114">Steps toofail over toohello same device</span></span>

<span data-ttu-id="64bf5-115">Выполните следующие действия, если требуется toofail по сравнению с toohello hello одного устройства.</span><span class="sxs-lookup"><span data-stu-id="64bf5-115">Perform hello following steps if you need toofail over toohello same device.</span></span>

1. <span data-ttu-id="64bf5-116">Выполните моментальные облачные снимки всех томов hello в вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="64bf5-116">Take cloud snapshots of all hello volumes in your device.</span></span> <span data-ttu-id="64bf5-117">Дополнительные сведения см. слишком[резервные копии toocreate службы с помощью диспетчера устройств StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="64bf5-117">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="64bf5-118">Сбросьте настройки устройства toofactory по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="64bf5-118">Reset your device toofactory defaults.</span></span> <span data-ttu-id="64bf5-119">Выполните hello подробные инструкции в [как параметры по умолчанию tooreset toofactory устройство StorSimple](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="64bf5-119">Follow hello detailed instructions in [how tooreset a StorSimple device toofactory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="64bf5-120">Службе диспетчера StorSimple устройство toohello перейдите и выберите **устройств**.</span><span class="sxs-lookup"><span data-stu-id="64bf5-120">Go toohello StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="64bf5-121">В hello **устройств** колонке hello старое устройство должно отображаться как **Offline**.</span><span class="sxs-lookup"><span data-stu-id="64bf5-121">In hello **Devices** blade, hello old device should show as **Offline**.</span></span>

    ![Исходное устройство не в сети](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="64bf5-123">Настройте устройство и снова зарегистрируйте его в службе диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="64bf5-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="64bf5-124">Hello вновь зарегистрированного устройства должно отображаться как **готов tooset копирование**.</span><span class="sxs-lookup"><span data-stu-id="64bf5-124">hello newly registered device should show as **Ready tooset up**.</span></span> <span data-ttu-id="64bf5-125">Имя устройства Hello для нового устройства hello — hello так же, как старое устройство hello но с добавлением чисел tooindicate hello устройства по умолчанию toofactory сброса и зарегистрировать его заново.</span><span class="sxs-lookup"><span data-stu-id="64bf5-125">hello device name for hello new device is hello same as hello old device but appended with a numeral tooindicate that hello device was reset toofactory default and registered again.</span></span>

    ![Только что зарегистрированные устройства готовы tooset вверх](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="64bf5-127">Для hello новое устройство выполните настройку hello.</span><span class="sxs-lookup"><span data-stu-id="64bf5-127">For hello new device, complete hello device setup.</span></span> <span data-ttu-id="64bf5-128">Дополнительные сведения см. слишком[шаг 4: выполнение минимальной настройки устройства](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="64bf5-128">For more information, go too[Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="64bf5-129">На hello **устройств** колонке hello состояние устройства hello изменяет слишком**Online**.</span><span class="sxs-lookup"><span data-stu-id="64bf5-129">On hello **Devices** blade, hello status of hello device changes too**Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="64bf5-130">**Сначала завершите hello минимальной конфигурации или решение аварийного восстановления может завершиться ошибкой.**</span><span class="sxs-lookup"><span data-stu-id="64bf5-130">**Complete hello minimum configuration first, or your DR may fail.**</span></span>

    ![Только что зарегистрированное устройство включено](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="64bf5-132">Выберите старое устройство hello (состояние вне сети) и на панели команд hello, нажмите кнопку **при сбое**.</span><span class="sxs-lookup"><span data-stu-id="64bf5-132">Select hello old device (status offline) and from hello command bar, click **Fail over**.</span></span> <span data-ttu-id="64bf5-133">В hello **при сбое** колонке выберите старое устройство в качестве источника hello и укажите целевое устройство hello hello вновь зарегистрированного устройства.</span><span class="sxs-lookup"><span data-stu-id="64bf5-133">In hello **Fail over** blade, select old device as hello source and specify hello target device as hello newly registered device.</span></span>

    ![Сводка отработки отказа](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="64bf5-135">Подробные инструкции см. в разделе слишком[отработки отказа физического устройства tooanother](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="64bf5-135">For detailed instructions, refer too[Fail over tooanother physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="64bf5-136">Создается задание восстановления устройства, можно отслеживать из hello **заданий** колонку.</span><span class="sxs-lookup"><span data-stu-id="64bf5-136">A device restore job is created that you can monitor from hello **Jobs** blade.</span></span>

8. <span data-ttu-id="64bf5-137">После успешного завершения задания hello, для доступа к hello новое устройство, так и для перехода toohello **контейнеры томов** колонку.</span><span class="sxs-lookup"><span data-stu-id="64bf5-137">After hello job has successfully completed, access hello new device and navigate toohello **Volume containers** blade.</span></span> <span data-ttu-id="64bf5-138">Убедитесь, что все контейнеры томов hello из старого устройства hello перенесены toohello новое устройство.</span><span class="sxs-lookup"><span data-stu-id="64bf5-138">Verify that all hello volume containers from hello old device have migrated toohello new device.</span></span>

   ![Контейнеры томов перенесены](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="64bf5-140">После завершения отработки отказа hello, можно отключить и удалить hello старое устройство с портала hello.</span><span class="sxs-lookup"><span data-stu-id="64bf5-140">After hello failover is complete, you can deactivate and delete hello old device from hello portal.</span></span> <span data-ttu-id="64bf5-141">Выберите hello старое устройство (вне сети), щелкните правой кнопкой мыши, а затем выберите **деактивировать**.</span><span class="sxs-lookup"><span data-stu-id="64bf5-141">Select hello old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="64bf5-142">После деактивации устройство hello обновляется состояние hello hello устройства.</span><span class="sxs-lookup"><span data-stu-id="64bf5-142">After hello device is deactivated, hello status of hello device is updated.</span></span>

     ![Исходное устройство отключено](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="64bf5-144">Выберите hello деактивации устройства, щелкните правой кнопкой мыши, а затем выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="64bf5-144">Select hello deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="64bf5-145">При этом будет удалено hello устройство из списка устройств hello.</span><span class="sxs-lookup"><span data-stu-id="64bf5-145">This deletes hello device from hello list of devices.</span></span>

    ![Исходное устройство удалено](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="64bf5-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64bf5-147">Next steps</span></span>

* <span data-ttu-id="64bf5-148">После выполнения отработки отказа, может потребоваться слишком[отключение или удаление устройства StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="64bf5-148">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="64bf5-149">Сведения о toouse Здравствуйте устройства StorSimple, как службы, перейдите в слишком[используйте hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="64bf5-149">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

