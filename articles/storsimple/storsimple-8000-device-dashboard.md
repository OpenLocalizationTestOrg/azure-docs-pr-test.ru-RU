---
title: "Использование сводки по устройствам StorSimple серии 8000 | Документация Майкрософт"
description: "Описание сводки по устройству службы диспетчера устройств StorSimple и ее использования для просмотра метрик хранилища и подключенных инициаторов, а также поиска серийного номера и IQN."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 784d3ce9d8f926b00ac1c6fbf48a05c0b04f900a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="c1cfa-103">Использование сводки по устройству в службе диспетчера устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="c1cfa-103">Use the device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="c1cfa-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c1cfa-104">Overview</span></span>
<span data-ttu-id="c1cfa-105">Колонка сводных данных устройства StorSimple предоставляет общие сведения для конкретного устройства StorSimple в отличие от колонки сводных данных службы, которая предоставляет сведения обо всех устройствах, включенных в решение Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-105">The StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast to the service summary blade, which gives you information about all the devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="c1cfa-106">Колонка сводных данных об устройстве содержит сводное представление об устройстве StorSimple серии 8000, зарегистрированном в определенном диспетчере устройств StorSimple. В ней также выделены те проблемы устройства, которые требуют внимания системного администратора.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-106">The device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="c1cfa-107">В этом руководстве приведены общие сведения об этой колонке, объясняются ее функции и содержимое, а также описываются задачи, которые можно в ней выполнять.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-107">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="c1cfa-108">В колонке сводных данных об устройстве отображается следующая информация.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-108">The device summary blade displays the following information:</span></span>

![Колонка сводных данных устройства](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="c1cfa-110">Панель команд управления</span><span class="sxs-lookup"><span data-stu-id="c1cfa-110">Management command bar</span></span>

<span data-ttu-id="c1cfa-111">В колонке устройства StorSimple доступны параметры для управления этим устройством.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-111">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="c1cfa-112">Команды управления расположены в верхней части колонки, а также с левой стороны.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-112">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="c1cfa-113">Эти параметры позволяют добавлять общие файловые ресурсы или тома, обновлять устройство или выполнять отработку отказа для него.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-113">Use these options to add shares or volumes, or update or fail over your device.</span></span>

![Панель команд управления](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="c1cfa-115">Основные компоненты</span><span class="sxs-lookup"><span data-stu-id="c1cfa-115">Essentials</span></span>

<span data-ttu-id="c1cfa-116">В области "Основные компоненты" расположены некоторые важные свойства, такие как состояние, модель, целевой IQN и версия программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-116">The essentials area captures some of the important properties such as, the status, model, target IQN, and the software version.</span></span> 

![Основные компоненты устройства](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="c1cfa-118">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="c1cfa-118">Monitoring</span></span>

* <span data-ttu-id="c1cfa-119">Элемент **Оповещения** содержит все активные оповещения для устройства, сгруппированные по уровню серьезности.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-119">The **Alerts** tile provides a snapshot of all the active alerts for your device, grouped by alert severity.</span></span>

    ![Элемент "Оповещения"](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="c1cfa-121">Щелкните этот элемент, чтобы открыть колонку **Оповещения**, а затем выберите отдельное оповещение, чтобы просмотреть дополнительные сведения о нем, включая рекомендуемые действия.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-121">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="c1cfa-122">Также можно удалить предупреждение, если проблема решена.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-122">You can also clear the alert if the issue has been resolved.</span></span>

    ![Щелкните элемент "Оповещения"](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="c1cfa-124">Элемент **Состояние и работоспособность** содержит сведения о работоспособности компонентов оборудования устройства, включая его состояние.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-124">The **Status and health** tile provides insights into the hardware component health for a device including the device status.</span></span> <span data-ttu-id="c1cfa-125">Состояние устройства может быть "Автономно", "В сети", "Отключено" или "Готово к настройке".</span><span class="sxs-lookup"><span data-stu-id="c1cfa-125">The device status may be offline, online, deactivated, or ready to set up.</span></span>

    ![Элемент "Состояние и работоспособность"](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="c1cfa-127">Элемент **Тома** содержит сводные данные о количеств томов на устройстве, сгруппированных по состоянию.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-127">The **Volumes** tile provides a summary of the number of volumes in your device grouped by status.</span></span>

    ![Элемент "Тома"](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="c1cfa-129">Щелкните элемент, чтобы открыть колонку со списком **томов**, а затем выберите отдельный том, чтобы просмотреть или изменить его свойства.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-129">Click the tile to open the **Volumes** list blade, and then click on an individual volume to view or modify its properties.</span></span>
    
    ![Щелкните элемент "Тома"](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="c1cfa-131">Дополнительные сведения см. в статье [об управлении томами](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="c1cfa-131">For more information, see how to [manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="c1cfa-132">На диаграмме **Использование** доступны сведения об использовании основного хранилища на устройстве, а также об использовании облачного хранилища за последние 7 дней (период по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="c1cfa-132">In the **Usage** chart, you can view the primary storage used across your device, and the cloud storage consumed over the past 7 days, the default time period.</span></span>

     ![Плитка "Использование"](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="c1cfa-134">С помощью параметра **Изменить**, расположенного в правом верхнем углу диаграммы, можно выбрать другую временную шкалу.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-134">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![Изменение диаграммы использования](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="c1cfa-136">На этой диаграмме можно просмотреть метрики для всего основного хранилища (объем данных, записанных узлами на устройство) и общий объем облачного хранилища, использованный устройством в течение определенного периода времени.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-136">In this chart, you can view metrics for the total primary storage (the amount of data written by hosts to your device) and the total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="c1cfa-137">В этом контексте *основное хранилище* представляет общий объем данных, записанных узлом, и может отличаться по типу тома. *Основное многоуровневое хранилище* включает в себя данные, хранимые локально, и данные, расположенные в облаке.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-137">In this context, *primary storage* refers to the total amount of data written by the host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered to the cloud.</span></span> <span data-ttu-id="c1cfa-138">*Основное локально закрепленное хранилище* включает в себя только данные, хранимые локально.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="c1cfa-139">*Облачное хранилище*, с другой стороны, — это мера общего объема данных, хранящихся в облаке.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-139">*Cloud storage*, on the other hand, is a measurement of the total amount of data stored in the cloud.</span></span> <span data-ttu-id="c1cfa-140">В хранилище содержатся многоуровневые данные и резервные копии.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="c1cfa-141">Данные, которые хранятся в облаке, дедуплицированы и сжаты. При этом в основном хранилище указывается объем хранилища, используемый до их дедупликации и сжатия.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-141">The data stored in the cloud is deduplicated and compressed, whereas primary storage indicates the amount of storage used before the data is deduplicated and compressed.</span></span> <span data-ttu-id="c1cfa-142">(Можно сравнить эти две величины, чтобы получить представление о степени сжатия.) Для первичного и облачного хранилища показанные объемы будут зависеть от настроенной частоты отслеживания.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-142">(You can compare these two numbers to get an idea of the compression rate.) For both primary and cloud storage, the amounts shown are based on the tracking frequency you configure.</span></span> <span data-ttu-id="c1cfa-143">Например, если выбрать одну неделю в качестве частоты, на диаграмме будут показаны данные за каждый день предыдущей недели.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-143">For example, if you choose a one week frequency, then the chart shows data for each day in the previous week.</span></span>

     <span data-ttu-id="c1cfa-144">Чтобы увидеть объем облачного хранилища, использованного в течение времени, выберите параметр **ИСПОЛЬЗОВАННОЕ ОБЛАЧНОЕ ХРАНИЛИЩЕ** .</span><span class="sxs-lookup"><span data-stu-id="c1cfa-144">To see the amount of cloud storage consumed over time, select the **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="c1cfa-145">Чтобы просмотреть общий объем хранилища, записанный узлом, выберите параметр **PRIMARY TIERED STORAGE USED** (Используемое основное многоуровневое хранилище) и **PRIMARY LOCALLY PINNED STORAGE USED** (Используемое основное локально закрепленное хранилище).</span><span class="sxs-lookup"><span data-stu-id="c1cfa-145">To see the total storage that has been written by the host, select the **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="c1cfa-146">Дополнительные сведения см. в статье [Использование службы диспетчера устройств StorSimple для мониторинга устройства StorSimple](storsimple-monitor-device.md).</span><span class="sxs-lookup"><span data-stu-id="c1cfa-146">For more information, see [Use the StorSimple Device Manager service to monitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="c1cfa-147">Элемент **Емкость** содержит сведения о подготовленной и оставшейся емкости основного хранилища на устройстве относительно общего объема хранилища для устройства.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-147">The **Capacity** tile displays the primary storage that is provisioned and remaining across the device relative to the total storage available for the same.</span></span> <span data-ttu-id="c1cfa-148">В разделе **Подготовлено** приведены сведения о подготовленной и выделенной для использования емкости хранилища, а в разделе **Осталось** — сведения об оставшейся емкости, которую можно подготовить для этого устройства.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-148">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> 

    ![Плитка "Использование"](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="c1cfa-150">Щелкните этот элемент, чтобы просмотреть, как емкость предоставляется через многоуровневые и локально закрепленные тома.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-150">Click this tile to view how the capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="c1cfa-151">Элемент **Оставшаяся многоуровневая емкость** содержит сведения о доступной емкости, которую можно подготовить, в том числе в облаке, а элемент **Оставшаяся локальная емкость** — сведения о емкости, которая осталась на дисках, присоединенных к устройству.</span><span class="sxs-lookup"><span data-stu-id="c1cfa-151">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this device.</span></span>

    ![Щелкните диаграмму использования](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="c1cfa-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1cfa-153">Next steps</span></span>
* <span data-ttu-id="c1cfa-154">Узнайте больше об [использовании колонки сводки службы StorSimple](storsimple-8000-service-dashboard.md)</span><span class="sxs-lookup"><span data-stu-id="c1cfa-154">Learn more about the [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="c1cfa-155">Узнайте больше об [использовании службы диспетчера устройств StorSimple для администрирования устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c1cfa-155">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

