---
title: "aaaStorSimple перехода на другой ресурс tooa восстановления после сбоев облачных устройств StorSimple | Документы Microsoft"
description: "Дополнительные сведения об toofail по вашей tooa физического устройства серии StorSimple 8000 облачных устройств."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a><span data-ttu-id="f8109-103">При сбое tooyour облачных устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="f8109-103">Fail over tooyour StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="f8109-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f8109-104">Overview</span></span>

<span data-ttu-id="f8109-105">В данном учебнике требуется toofail hello действия над tooa физического устройства серии StorSimple 8000 устройство StorSimple облака при аварии.</span><span class="sxs-lookup"><span data-stu-id="f8109-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooa StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="f8109-106">StorSimple использует данные hello устройства отработки отказа компонентов toomigrate из источника физического устройства в hello tooa центра обработки данных облака устройства, работающие в Azure.</span><span class="sxs-lookup"><span data-stu-id="f8109-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooa cloud appliance running in Azure.</span></span> <span data-ttu-id="f8109-107">руководство Hello в этом учебнике применяется физических устройств серии tooStorSimple 8000 и облачных устройств под управлением версий программного обеспечения обновления 3 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="f8109-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="f8109-108">toolearn Дополнительные сведения о отработки отказа устройства и как она используется toorecover после аварии, go слишком[отработки отказа и аварийного восстановления для устройства серии StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="f8109-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="f8109-109">toofail на физическое устройство tooanother физическом устройстве StorSimple, перейдите в слишком[при сбое физических устройств StorSimple tooa](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="f8109-109">toofail over a StorSimple physical device tooanother physical device, go too[Fail over tooa StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="f8109-110">toofail над tooitself устройства go слишком[при сбое toohello же физических устройств StorSimple](storsimple-8000-device-failover-same-device.md).</span><span class="sxs-lookup"><span data-stu-id="f8109-110">toofail over a device tooitself, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8109-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f8109-111">Prerequisites</span></span>

- <span data-ttu-id="f8109-112">Убедитесь, можно ознакомиться с разделом hello рекомендации для обработки отказа устройства.</span><span class="sxs-lookup"><span data-stu-id="f8109-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="f8109-113">Дополнительные сведения см. слишком[Общие рекомендации для обработки отказа устройства](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="f8109-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="f8109-114">Перед началом этой процедуры нужно создать и настроить облачное устройство StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f8109-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="f8109-115">Если выполняется обновление 3 версии программного обеспечения или более поздней версии, рекомендуется использовать устройство 8020 облака для hello аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="f8109-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for hello DR.</span></span> <span data-ttu-id="f8109-116">модели 8020 Hello 64 ТБ и использует хранилище Premium.</span><span class="sxs-lookup"><span data-stu-id="f8109-116">hello 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="f8109-117">Дополнительные сведения см. слишком[развертывание и управление ими в StorSimple Appliance облака](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="f8109-117">For more information, go too[Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-toofail-over-tooa-cloud-appliance"></a><span data-ttu-id="f8109-118">Toofail действия над tooa облачному устройству</span><span class="sxs-lookup"><span data-stu-id="f8109-118">Steps toofail over tooa cloud appliance</span></span>

<span data-ttu-id="f8109-119">Выполните hello после целевого действия toorestore hello устройства tooa облачному устройству StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f8109-119">Perform hello following steps toorestore hello device tooa target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="f8109-120">Убедитесь, что нужные toofail через контейнера томов hello связаны облачные моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="f8109-120">Verify that hello volume container you want toofail over has associated cloud snapshots.</span></span> <span data-ttu-id="f8109-121">Дополнительные сведения см. слишком[резервные копии toocreate службы с помощью диспетчера устройств StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="f8109-121">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="f8109-122">Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **устройств**.</span><span class="sxs-lookup"><span data-stu-id="f8109-122">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="f8109-123">В hello **устройств** колонки, последовательно выберите toohello список устройств, подключенных с помощью службы.</span><span class="sxs-lookup"><span data-stu-id="f8109-123">In hello **Devices** blade, go toohello list of devices connected with your service.</span></span>
    <span data-ttu-id="f8109-124">![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="f8109-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="f8109-125">Выберите и щелкните исходное устройство.</span><span class="sxs-lookup"><span data-stu-id="f8109-125">Select and click your source device.</span></span> <span data-ttu-id="f8109-126">Hello исходное устройство имеет hello контейнеры томов, которые требуется toofail к.</span><span class="sxs-lookup"><span data-stu-id="f8109-126">hello source device has hello volume containers that you want toofail over.</span></span> <span data-ttu-id="f8109-127">Go слишком**параметры > контейнеры томов**.</span><span class="sxs-lookup"><span data-stu-id="f8109-127">Go too**Settings > Volume Containers**.</span></span>

    ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="f8109-129">Выберите контейнер томов, желательно toofail над tooanother устройством.</span><span class="sxs-lookup"><span data-stu-id="f8109-129">Select a volume container that you would like toofail over tooanother device.</span></span> <span data-ttu-id="f8109-130">Выберите hello тома контейнера toodisplay hello список томов в контейнере.</span><span class="sxs-lookup"><span data-stu-id="f8109-130">Click hello volume container toodisplay hello list of volumes within this container.</span></span> <span data-ttu-id="f8109-131">Выберите тома, щелкните правой кнопкой мыши и нажмите кнопку **перевести в автономный режим** tootake том hello в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="f8109-131">Select a volume, right-click, and click **Take Offline** tootake hello volume offline.</span></span>

    ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="f8109-133">Повторите эту процедуру для всех томов hello в контейнер тома hello.</span><span class="sxs-lookup"><span data-stu-id="f8109-133">Repeat this process for all hello volumes in hello volume container.</span></span>

     ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="f8109-135">Hello повторите предыдущий шаг для всех hello контейнеры томов хотелось бы toofail над tooanother устройством.</span><span class="sxs-lookup"><span data-stu-id="f8109-135">Repeat hello previous step for all hello volume containers you would like toofail over tooanother device.</span></span>

7. <span data-ttu-id="f8109-136">Вернитесь к предыдущему окну toohello **устройств** колонку.</span><span class="sxs-lookup"><span data-stu-id="f8109-136">Go back toohello **Devices** blade.</span></span> <span data-ttu-id="f8109-137">На панели команд hello, нажмите кнопку **при сбое**.</span><span class="sxs-lookup"><span data-stu-id="f8109-137">From hello command bar, click **Fail over**.</span></span>

    ![Команда "Отработка отказа"](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="f8109-139">В hello **при сбое** колонки, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f8109-139">In hello **Fail over** blade, perform hello following steps:</span></span>
   
    1. <span data-ttu-id="f8109-140">Щелкните **Источник**.</span><span class="sxs-lookup"><span data-stu-id="f8109-140">Click **Source**.</span></span> <span data-ttu-id="f8109-141">Выберите контейнеры toofail hello тома по.</span><span class="sxs-lookup"><span data-stu-id="f8109-141">Select hello volume containers toofail over.</span></span> <span data-ttu-id="f8109-142">**Здравствуйте, только контейнеры томов со связанных облачных моментальных снимков и отображаются томами в автономном режиме.**</span><span class="sxs-lookup"><span data-stu-id="f8109-142">**Only hello volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="f8109-143">![Выбрать источник](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="f8109-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="f8109-144">Щелкните **Цель**.</span><span class="sxs-lookup"><span data-stu-id="f8109-144">Click **Target**.</span></span> <span data-ttu-id="f8109-145">Выберите целевой облачному устройству hello в раскрывающемся списке доступных устройств.</span><span class="sxs-lookup"><span data-stu-id="f8109-145">Select a target cloud appliance from hello dropdown list of available devices.</span></span> <span data-ttu-id="f8109-146">**В списке hello отображаются только hello устройства имеют достаточно мощности tooaccommodate исходные контейнеры тома.**</span><span class="sxs-lookup"><span data-stu-id="f8109-146">**Only hello devices that have sufficient capacity tooaccommodate source volume containers are displayed in hello list.**</span></span>

        ![Выбор цели](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="f8109-148">Просмотрите параметры hello отработки отказа в группе **Сводка** и выберите hello флажок, указывающее, что hello томов в контейнере выбранного тома находятся в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="f8109-148">Review hello failover settings under **Summary** and select hello checkbox indicating that hello volumes in selected volume containers are offline.</span></span> 

        ![Просмотр параметров отработки отказа](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="f8109-150">Задание отработки отказа создано.</span><span class="sxs-lookup"><span data-stu-id="f8109-150">A failover job is created.</span></span> <span data-ttu-id="f8109-151">отработка отказа hello toomonitor задания, щелкните уведомление задания hello.</span><span class="sxs-lookup"><span data-stu-id="f8109-151">toomonitor hello failover job, click hello job notification.</span></span>

    ![Мониторинг задания отработки отказа](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="f8109-153">После завершения отработки отказа hello, вернитесь к предыдущему окну toohello **устройств** колонку.</span><span class="sxs-lookup"><span data-stu-id="f8109-153">After hello failover is completed, go back toohello **Devices** blade.</span></span>

    1. <span data-ttu-id="f8109-154">Выберите устройство hello, используемой в качестве целевой hello hello перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="f8109-154">Select hello device that was used as hello target for hello failover.</span></span>

       ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="f8109-156">Щелкните **Контейнеры томов**.</span><span class="sxs-lookup"><span data-stu-id="f8109-156">Click **Volume Containers**.</span></span> <span data-ttu-id="f8109-157">Должны появиться все контейнеры томов hello и hello томами из старого устройства hello.</span><span class="sxs-lookup"><span data-stu-id="f8109-157">All hello volume containers, along with hello volumes from hello old device, should be listed.</span></span>

       <span data-ttu-id="f8109-158">Если контейнер томов hello отработку отказа локально закрепленные тома, эти тома являются отработку отказа, как и многоуровневые тома.</span><span class="sxs-lookup"><span data-stu-id="f8109-158">If hello volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="f8109-159">Локально закрепленные тома не поддерживаются облачным устройством StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f8109-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Просмотр целевых контейнеров томов](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="f8109-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f8109-161">Next steps</span></span>

* <span data-ttu-id="f8109-162">После выполнения отработки отказа, может потребоваться слишком[отключение или удаление устройства StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="f8109-162">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="f8109-163">Сведения о toouse Здравствуйте устройства StorSimple, как службы, перейдите в слишком[используйте hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f8109-163">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

