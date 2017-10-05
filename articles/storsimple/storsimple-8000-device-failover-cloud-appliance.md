---
title: "Отработка отказа и аварийное восстановление на облачное устройство StorSimple | Документация Майкрософт"
description: "Узнайте, как выполнять отработку отказа физического устройства StorSimple серии 8000 на облачное устройство."
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
ms.openlocfilehash: ec8bebf2854e84a37e84b45564e80fc20b63d8d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-to-your-storsimple-cloud-appliance"></a><span data-ttu-id="a7739-103">Отработка отказа на облачное устройство StorSimple</span><span class="sxs-lookup"><span data-stu-id="a7739-103">Fail over to your StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="a7739-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a7739-104">Overview</span></span>

<span data-ttu-id="a7739-105">В этом руководстве описаны шаги, необходимые для отработки отказа физического устройства StorSimple серии 8000 на облачное устройство StorSimple в случае аварии.</span><span class="sxs-lookup"><span data-stu-id="a7739-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to a StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="a7739-106">StorSimple использует функцию отработки отказа устройства для переноса данных с исходного физического устройства в центре данных на облачное устройство, выполняющееся в Azure.</span><span class="sxs-lookup"><span data-stu-id="a7739-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to a cloud appliance running in Azure.</span></span> <span data-ttu-id="a7739-107">Рекомендации в этом руководстве относятся к облачным устройствам и физическим устройствам StorSimple серии 8000 под управлением версий программного обеспечения с обновлением 3 и более поздним.</span><span class="sxs-lookup"><span data-stu-id="a7739-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="a7739-108">Чтобы узнать больше об отработке отказа устройств и его использовании для восстановления после аварии, см. статью [Failover and disaster recovery for your StorSimple 8000 series device](storsimple-8000-device-failover-disaster-recovery.md) (Отработка отказа и аварийное восстановление для устройств StorSimple серии 8000).</span><span class="sxs-lookup"><span data-stu-id="a7739-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="a7739-109">Сведения об отработке отказа с одного физического устройства StorSimple на другое физическое устройство см. в статье [Fail over to a StorSimple physical device](storsimple-8000-device-failover-physical-device.md) (Отработка отказа на физическое устройство StorSimple).</span><span class="sxs-lookup"><span data-stu-id="a7739-109">To fail over a StorSimple physical device to another physical device, go to [Fail over to a StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="a7739-110">Сведения об отработке отказа на то же устройство см. в статье [Fail over to a StorSimple 8000 series physical device](storsimple-8000-device-failover-same-device.md) (Отработка отказа на то же физическое устройство StorSimple).</span><span class="sxs-lookup"><span data-stu-id="a7739-110">To fail over a device to itself, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7739-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a7739-111">Prerequisites</span></span>

- <span data-ttu-id="a7739-112">Обязательно ознакомьтесь с рекомендациями по отработке отказа устройств.</span><span class="sxs-lookup"><span data-stu-id="a7739-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="a7739-113">Дополнительные сведения см. в статье с [общими рекомендациями по отработке отказа устройств](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="a7739-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="a7739-114">Перед началом этой процедуры нужно создать и настроить облачное устройство StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a7739-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="a7739-115">Если на устройстве установлено программное обеспечение с обновлением 3 или более поздним, рассмотрите возможность использования облачного устройства 8020 для аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="a7739-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for the DR.</span></span> <span data-ttu-id="a7739-116">Модель 8020 обладает 64 ТБ памяти и использует хранилище класса Premium.</span><span class="sxs-lookup"><span data-stu-id="a7739-116">The 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="a7739-117">Дополнительные сведения см. в статье [Развертывание и администрирование облачного устройства StorSimple в Azure (обновление 3 и более поздние версии)](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="a7739-117">For more information, go to [Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-to-fail-over-to-a-cloud-appliance"></a><span data-ttu-id="a7739-118">Шаги по отработке отказа на облачное устройство</span><span class="sxs-lookup"><span data-stu-id="a7739-118">Steps to fail over to a cloud appliance</span></span>

<span data-ttu-id="a7739-119">Вот как можно восстановить устройство на целевом облачном устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a7739-119">Perform the following steps to restore the device to a target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="a7739-120">Убедитесь, что контейнер томов, для которого необходимо выполнить отработку отказа, имеет связанные с собой облачные моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="a7739-120">Verify that the volume container you want to fail over has associated cloud snapshots.</span></span> <span data-ttu-id="a7739-121">Дополнительные сведения см. в статье [Use the StorSimple Device Manager service in Azure portal to manage backup policies](storsimple-8000-manage-backup-policies-u2.md) (Использование службы диспетчера устройств StorSimple на портале Azure для управления политиками резервного копирования).</span><span class="sxs-lookup"><span data-stu-id="a7739-121">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="a7739-122">В службе диспетчера устройств StorSimple выберите **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="a7739-122">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="a7739-123">В колонке **Устройства** перейдите к списку устройств, подключенных к вашей службе.</span><span class="sxs-lookup"><span data-stu-id="a7739-123">In the **Devices** blade, go to the list of devices connected with your service.</span></span>
    <span data-ttu-id="a7739-124">![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="a7739-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="a7739-125">Выберите и щелкните исходное устройство.</span><span class="sxs-lookup"><span data-stu-id="a7739-125">Select and click your source device.</span></span> <span data-ttu-id="a7739-126">Исходное устройство содержит контейнеры томов, для которых необходимо выполнить отработку отказа.</span><span class="sxs-lookup"><span data-stu-id="a7739-126">The source device has the volume containers that you want to fail over.</span></span> <span data-ttu-id="a7739-127">Последовательно выберите пункты **Параметры > Контейнеры томов**.</span><span class="sxs-lookup"><span data-stu-id="a7739-127">Go to **Settings > Volume Containers**.</span></span>

    ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="a7739-129">Выберите контейнер томов, для которого следует выполнить отработку отказа на другое устройство.</span><span class="sxs-lookup"><span data-stu-id="a7739-129">Select a volume container that you would like to fail over to another device.</span></span> <span data-ttu-id="a7739-130">Щелкните контейнер томов, чтобы открыть список томов в контейнере.</span><span class="sxs-lookup"><span data-stu-id="a7739-130">Click the volume container to display the list of volumes within this container.</span></span> <span data-ttu-id="a7739-131">Выберите том, щелкните его правой кнопкой мыши и выберите **Отключить**, чтобы отключить том.</span><span class="sxs-lookup"><span data-stu-id="a7739-131">Select a volume, right-click, and click **Take Offline** to take the volume offline.</span></span>

    ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="a7739-133">Повторите эту процедуру для всех томов в контейнере томов.</span><span class="sxs-lookup"><span data-stu-id="a7739-133">Repeat this process for all the volumes in the volume container.</span></span>

     ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="a7739-135">Повторите предыдущий шаг для всех контейнеров томов, для которых необходимо выполнить отработку отказа на другое устройство.</span><span class="sxs-lookup"><span data-stu-id="a7739-135">Repeat the previous step for all the volume containers you would like to fail over to another device.</span></span>

7. <span data-ttu-id="a7739-136">Вернитесь в колонку **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="a7739-136">Go back to the **Devices** blade.</span></span> <span data-ttu-id="a7739-137">На панели команд щелкните **Отработка отказа**.</span><span class="sxs-lookup"><span data-stu-id="a7739-137">From the command bar, click **Fail over**.</span></span>

    ![Команда "Отработка отказа"](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="a7739-139">В колонке **Отработка отказа** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a7739-139">In the **Fail over** blade, perform the following steps:</span></span>
   
    1. <span data-ttu-id="a7739-140">Щелкните **Источник**.</span><span class="sxs-lookup"><span data-stu-id="a7739-140">Click **Source**.</span></span> <span data-ttu-id="a7739-141">Выберите контейнеры томов для отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="a7739-141">Select the volume containers to fail over.</span></span> <span data-ttu-id="a7739-142">**Отображаться будут только контейнеры тома со связанными облачными моментальными снимками и тома в автономном режиме.**</span><span class="sxs-lookup"><span data-stu-id="a7739-142">**Only the volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="a7739-143">![Выбрать источник](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="a7739-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="a7739-144">Щелкните **Цель**.</span><span class="sxs-lookup"><span data-stu-id="a7739-144">Click **Target**.</span></span> <span data-ttu-id="a7739-145">Выберите целевое облачное устройство из раскрывающегося списка доступных устройств.</span><span class="sxs-lookup"><span data-stu-id="a7739-145">Select a target cloud appliance from the dropdown list of available devices.</span></span> <span data-ttu-id="a7739-146">**В списке отображаются только те устройства, емкость которых достаточна для размещения исходных контейнеров томов.**</span><span class="sxs-lookup"><span data-stu-id="a7739-146">**Only the devices that have sufficient capacity to accommodate source volume containers are displayed in the list.**</span></span>

        ![Выбор цели](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="a7739-148">Просмотрите параметры отработки отказа в разделе **Сводка** и установите флажок, указывающий, что тома в выбранных контейнерах томов находятся в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="a7739-148">Review the failover settings under **Summary** and select the checkbox indicating that the volumes in selected volume containers are offline.</span></span> 

        ![Просмотр параметров отработки отказа](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="a7739-150">Задание отработки отказа создано.</span><span class="sxs-lookup"><span data-stu-id="a7739-150">A failover job is created.</span></span> <span data-ttu-id="a7739-151">Чтобы отслеживать ход выполнения задания, щелкните уведомление задания.</span><span class="sxs-lookup"><span data-stu-id="a7739-151">To monitor the failover job, click the job notification.</span></span>

    ![Мониторинг задания отработки отказа](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="a7739-153">После завершения отработки отказа вернитесь в колонку **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="a7739-153">After the failover is completed, go back to the **Devices** blade.</span></span>

    1. <span data-ttu-id="a7739-154">Выберите устройство, которое было использовано в качестве целевого при отработке отказа.</span><span class="sxs-lookup"><span data-stu-id="a7739-154">Select the device that was used as the target for the failover.</span></span>

       ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="a7739-156">Щелкните **Контейнеры томов**.</span><span class="sxs-lookup"><span data-stu-id="a7739-156">Click **Volume Containers**.</span></span> <span data-ttu-id="a7739-157">В списке должны отобразиться все контейнеры томов, а также тома со старого устройства.</span><span class="sxs-lookup"><span data-stu-id="a7739-157">All the volume containers, along with the volumes from the old device, should be listed.</span></span>

       <span data-ttu-id="a7739-158">Если контейнер томов, для которого выполнена отработка отказа, содержит локально закрепленные тома, отработка отказа для них будет выполнена как для многоуровневых томов.</span><span class="sxs-lookup"><span data-stu-id="a7739-158">If the volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="a7739-159">Локально закрепленные тома не поддерживаются облачным устройством StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a7739-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Просмотр целевых контейнеров томов](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="a7739-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7739-161">Next steps</span></span>

* <span data-ttu-id="a7739-162">После отработки отказа, возможно, нужно будет [отключить или удалить устройство StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="a7739-162">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="a7739-163">Сведения об использовании службы диспетчера устройств StorSimple см. в статье [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md) (Администрирование устройства StorSimple с помощью службы диспетчера устройств StorSimple).</span><span class="sxs-lookup"><span data-stu-id="a7739-163">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

