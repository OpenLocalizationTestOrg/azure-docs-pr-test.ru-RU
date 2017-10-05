---
title: "Колонка сводки устройства виртуального массива StorSimple | Документация Майкрософт"
description: "Сведения о колонке сводных данных об устройстве в диспетчере устройств StorSimple и способах ее использования для мониторинга работоспособности виртуального массива StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 35413d597c3b6b1c7600241a78572b63f982d175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-blade-for-storsimple-device-manager-connected-to-storsimple-virtual-array"></a><span data-ttu-id="ad21a-103">Использование колонки сводных данных об устройстве в диспетчере устройств StorSimple, подключенному к виртуальному массиву StorSimple</span><span class="sxs-lookup"><span data-stu-id="ad21a-103">Use the device summary blade for StorSimple Device Manager connected to StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="ad21a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="ad21a-104">Overview</span></span>

<span data-ttu-id="ad21a-105">Колонка сводных данных об устройстве в диспетчере устройств StorSimple содержит сводное представление о виртуальном массиве StorSimple, зарегистрированном в определенном диспетчере устройств StorSimple. В ней также выделены те проблемы устройства, которые требуют внимания системного администратора.</span><span class="sxs-lookup"><span data-stu-id="ad21a-105">The StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="ad21a-106">В этом руководстве приведены общие сведения об этой колонке, объясняются ее функции и содержимое, а также описываются задачи, которые можно в ней выполнять.</span><span class="sxs-lookup"><span data-stu-id="ad21a-106">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="ad21a-107">В колонке сводных данных об устройстве отображается следующая информация.</span><span class="sxs-lookup"><span data-stu-id="ad21a-107">The device summary blade displays the following information:</span></span>

![Панель мониторинга устройства](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="ad21a-109">управления</span><span class="sxs-lookup"><span data-stu-id="ad21a-109">Management</span></span>

<span data-ttu-id="ad21a-110">В колонке устройства StorSimple доступны параметры для управления этим устройством.</span><span class="sxs-lookup"><span data-stu-id="ad21a-110">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="ad21a-111">Команды управления расположены в верхней части колонки, а также с левой стороны.</span><span class="sxs-lookup"><span data-stu-id="ad21a-111">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="ad21a-112">Эти параметры позволяют добавлять общие файловые ресурсы или тома, обновлять виртуальный массив или выполнять отработку отказа для него.</span><span class="sxs-lookup"><span data-stu-id="ad21a-112">Use these options to add shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="ad21a-113">В области "Основные компоненты" расположены некоторые важные свойства, например "Состояние", "Модель", "Версия программного обеспечения устройства", а также ссылка на **веб-интерфейс** массива.</span><span class="sxs-lookup"><span data-stu-id="ad21a-113">The essentials area captures some of the important properties such as, the status, model, software version as well as a link to the **Web UI** of the array.</span></span> <span data-ttu-id="ad21a-114">При наличии подключения к локальной сети вы можете напрямую запустить [локальный веб-интерфейс](storsimple-ova-web-ui-admin.md) для управления виртуальным массивом.</span><span class="sxs-lookup"><span data-stu-id="ad21a-114">If you are on an internal network, you can directly launch the [local web UI](storsimple-ova-web-ui-admin.md) to administer your virtual array.</span></span>

![Основные компоненты устройства](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="ad21a-116">Сводка по устройству StorSimple</span><span class="sxs-lookup"><span data-stu-id="ad21a-116">StorSimple device summary</span></span>

* <span data-ttu-id="ad21a-117">Элемент **Оповещения** содержит все активные оповещения для виртуального массива, сгруппированные по уровню серьезности.</span><span class="sxs-lookup"><span data-stu-id="ad21a-117">The **Alerts** tile provides a snapshot of all the active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="ad21a-118">Щелкните этот элемент, чтобы открыть колонку **Оповещения**, а затем выберите отдельное оповещение, чтобы просмотреть дополнительные сведения о нем, включая рекомендуемые действия.</span><span class="sxs-lookup"><span data-stu-id="ad21a-118">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="ad21a-119">Также можно удалить предупреждение, если проблема решена.</span><span class="sxs-lookup"><span data-stu-id="ad21a-119">You can also clear the alert if the issue has been resolved.</span></span>

* <span data-ttu-id="ad21a-120">Элемент **Емкость** содержит сведения о подготовленной и оставшейся емкости основного хранилища на виртуальном устройстве относительно общего объема хранилища для устройства.</span><span class="sxs-lookup"><span data-stu-id="ad21a-120">The **Capacity** tile displays the primary storage that is provisioned and remaining across the virtual device relative to the total storage available for the same.</span></span> <span data-ttu-id="ad21a-121">В разделе **Подготовлено** приведены сведения о подготовленной и выделенной для использования емкости хранилища, а в разделе **Осталось** — сведения об оставшейся емкости, которую можно подготовить для этого устройства.</span><span class="sxs-lookup"><span data-stu-id="ad21a-121">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="ad21a-122">Элемент **Remaining Tiered** (Оставшаяся многоуровневая емкость) содержит сведения о доступной емкости, которую можно подготовить, в том числе в облаке, а элемент **Remaining Local** (Оставшаяся локальная емкость) — сведения о емкости, которая осталась на дисках, присоединенных к виртуальному массиву.</span><span class="sxs-lookup"><span data-stu-id="ad21a-122">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this virtual array.</span></span>

* <span data-ttu-id="ad21a-123">На диаграмме **Использование** доступны сведения об использовании основного хранилища на виртуальном массиве, а также об использовании облачного хранилища за последние 7 дней (период по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="ad21a-123">In the **Usage** chart, you can view the primary storage used across your virtual array, as well as the cloud storage consumed  over the past 7 days, the default time period.</span></span> <span data-ttu-id="ad21a-124">С помощью команды **Изменить**, расположенной в правом верхнем углу диаграммы, можно выбрать другую временную шкалу.</span><span class="sxs-lookup"><span data-stu-id="ad21a-124">Use the **Edit** option in the top-right corner of the chart to choose a different time scale.</span></span>

* <span data-ttu-id="ad21a-125">Элемент **Общие файловые ресурсы** или **Тома** содержит сводные данные о количестве общих файловых ресурсов или томов на устройстве, сгруппированные по состоянию.</span><span class="sxs-lookup"><span data-stu-id="ad21a-125">The **Shares** or **Volumes** tile provides a summary of the number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="ad21a-126">Щелкните определенный элемент, чтобы открыть колонку со списком **общих файловых ресурсов** или **томов**, а затем выберите отдельный общий файловый ресурс или том, чтобы просмотреть или изменить его свойства.</span><span class="sxs-lookup"><span data-stu-id="ad21a-126">Click the tile to open the **Shares**  or **Volumes** list blade, and then click on an individual share or volume to view or modify its properties.</span></span> <span data-ttu-id="ad21a-127">Дополнительные сведения см. в статье об [управлении общими файловыми ресурсами](storsimple-virtual-array-manage-shares.md) или [томами](storsimple-virtual-array-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="ad21a-127">For more information, see how to [manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad21a-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad21a-128">Next steps</span></span>
<span data-ttu-id="ad21a-129">Ниже перечислено, что вы можете узнать.</span><span class="sxs-lookup"><span data-stu-id="ad21a-129">Learn how to:</span></span>
- [<span data-ttu-id="ad21a-130">Управление общими файловыми ресурсами в виртуальном массиве StorSimple</span><span class="sxs-lookup"><span data-stu-id="ad21a-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="ad21a-131">Управление томами в виртуальном массиве StorSimple</span><span class="sxs-lookup"><span data-stu-id="ad21a-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

