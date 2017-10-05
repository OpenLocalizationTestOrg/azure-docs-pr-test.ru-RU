---
title: "Использование сводки по устройствам StorSimple серии 8000 | Документация Майкрософт"
description: "В статье описывается колонка сводки по службе StorSimple и способы ее использования для наблюдения за работоспособностью решения StorSimple."
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
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: d987a4ae170f21532a886552cbe1eb5a0d25fc3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-service-summary-blade-for-storsimple-8000-series-device"></a><span data-ttu-id="71bd0-103">Использование колонки сводки по службе для устройства StorSimple серии 8000</span><span class="sxs-lookup"><span data-stu-id="71bd0-103">Use the service summary blade for StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="71bd0-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="71bd0-104">Overview</span></span>

<span data-ttu-id="71bd0-105">Колонка сводки по службе диспетчера устройств StorSimple содержит сводное представление всех устройств, подключенных к службе диспетчера устройств StorSimple. Устройства, требующие вмешательства системного администратора, в нем выделены.</span><span class="sxs-lookup"><span data-stu-id="71bd0-105">The StorSimple Device Manager service summary blade provides a summary view of all the devices that are connected to the StorSimple Device Manager service, highlighting those devices that need a system administrator's attention.</span></span> <span data-ttu-id="71bd0-106">В этом руководстве приведены общие сведения об этой колонке, объясняются ее функции и содержимое, а также описываются задачи, которые можно выполнять на этой странице.</span><span class="sxs-lookup"><span data-stu-id="71bd0-106">This tutorial introduces the service summary blade, explains the dashboard content and function, and describes the tasks that you can perform from this page.</span></span>

![Сводка по службе](./media/storsimple-8000-service-dashboard/service-summary1.png)


## <a name="management-commands"></a><span data-ttu-id="71bd0-108">Команды управления</span><span class="sxs-lookup"><span data-stu-id="71bd0-108">Management commands</span></span>

<span data-ttu-id="71bd0-109">В колонке сводки по службе StorSimple отображаются параметры управления службой диспетчера устройств StorSimple, а также устройства StorSimple серии 8000, зарегистрированные в этой службе.</span><span class="sxs-lookup"><span data-stu-id="71bd0-109">In the StorSimple service summary blade, you see the options for managing your StorSimple Device Manager service and the StorSimple 8000 series devices registered to this service.</span></span> <span data-ttu-id="71bd0-110">Команды управления расположены в верхней части колонки, а также с левой стороны.</span><span class="sxs-lookup"><span data-stu-id="71bd0-110">You see the management commands across the top of the blade and on the left side.</span></span>

![Панель команд](./media/storsimple-8000-service-dashboard/service-summary2.png)

<span data-ttu-id="71bd0-112">Эти параметры используются для выполнения различных операций, таких как добавление общих ресурсов или томов, мониторинг различных заданий, запущенных в на устройствах StorSimple.</span><span class="sxs-lookup"><span data-stu-id="71bd0-112">Use these options to perform various operations such as add shares or volumes, or monitor the various jobs running on the StorSimple devices.</span></span>


## <a name="essentials"></a><span data-ttu-id="71bd0-113">Основные компоненты</span><span class="sxs-lookup"><span data-stu-id="71bd0-113">Essentials</span></span>

<span data-ttu-id="71bd0-114">В области "Основные компоненты" расположены некоторые важные свойства, например группа ресурсов, расположение и подписка, где был создан диспетчер устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="71bd0-114">The essentials area captures some of the important properties such as, the resource group, location, and subscription in which your StorSimple Device Manager was created.</span></span>

![Основные компоненты](./media/storsimple-8000-service-dashboard/service-summary3.png)

## <a name="storsimple-device-manager-service-summary"></a><span data-ttu-id="71bd0-116">Сводные данные о службе диспетчера устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="71bd0-116">StorSimple Device Manager service summary</span></span>

* <span data-ttu-id="71bd0-117">На элементе **Оповещения** отображаются все активные оповещения для всех устройств, сгруппированные по уровню серьезности.</span><span class="sxs-lookup"><span data-stu-id="71bd0-117">The **Alerts** tile provides a snapshot of all the active alerts across all devices, grouped by alert severity.</span></span>

    ![Элемент "Оповещения"](./media/storsimple-8000-service-dashboard/service-summary4.png)

    <span data-ttu-id="71bd0-119">Если щелкнуть плитку, откроется колонка **Оповещения**, в которой можно выбрать отдельное оповещение, чтобы просмотреть дополнительные сведения о нем, включая рекомендуемые действия.</span><span class="sxs-lookup"><span data-stu-id="71bd0-119">Clicking the tile opens the **Alerts** blade, where you can click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="71bd0-120">Также можно удалить предупреждение, если проблема решена.</span><span class="sxs-lookup"><span data-stu-id="71bd0-120">You can also clear the alert if the issue has been resolved.</span></span>

    ![Выбор элемента "Оповещения"](./media/storsimple-8000-service-dashboard/service-summary8.png)

* <span data-ttu-id="71bd0-122">На элементе **Емкость** показан объем подготовленного основного хранилища и свободный объем на всех устройствах относительно их общего доступного объема.</span><span class="sxs-lookup"><span data-stu-id="71bd0-122">The **Capacity** tile displays shows the primary storage that is provisioned and remaining across all devices relative to the total storage available across all devices.</span></span> <span data-ttu-id="71bd0-123">В разделе **Подготовлено** приведены сведения о подготовленной и выделенной для использования емкости хранилища, а в разделе **Осталось** — сведения об оставшейся емкости, которую можно подготовить для всех устройств.</span><span class="sxs-lookup"><span data-stu-id="71bd0-123">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across all devices.</span></span>

    ![Элемент "Емкость"](./media/storsimple-8000-service-dashboard/service-summary6.png)

    <span data-ttu-id="71bd0-125">Элемент **Remaining Tiered** (Оставшаяся многоуровневая емкость) содержит сведения о доступной емкости, которую можно подготовить, в том числе в облаке, а элемент **Remaining Local** (Оставшаяся локальная емкость) — сведения о емкости, которая осталась на дисках, подключенных к устройствам StorSimple серии 8000.</span><span class="sxs-lookup"><span data-stu-id="71bd0-125">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to the StorSimple 8000 series devices.</span></span>


* <span data-ttu-id="71bd0-126">На диаграмме **Использование** можно увидеть соответствующие метрики для устройств.</span><span class="sxs-lookup"><span data-stu-id="71bd0-126">In the **Usage** chart, you can see the relevant metrics for your devices.</span></span> <span data-ttu-id="71bd0-127">Здесь можно просмотреть сведения об использовании основного хранилища на всех устройствах, а также об использовании облачного хранилища за последние 7 дней (период по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="71bd0-127">You can view the primary storage used across all devices, and the cloud storage consumed by devices over the past 7 days, the default time period.</span></span> 

    ![Плитка "Использование"](./media/storsimple-8000-service-dashboard/service-summary7.png) 

    <span data-ttu-id="71bd0-129">С помощью параметра **Изменить**, расположенного в правом верхнем углу диаграммы, можно выбрать другую временную шкалу.</span><span class="sxs-lookup"><span data-stu-id="71bd0-129">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![Выбор элемента "Использование"](./media/storsimple-8000-service-dashboard/service-summary10.png)

     ![Экспорт данных диаграммы](./media/storsimple-8000-service-dashboard/service-summary11.png)

* <span data-ttu-id="71bd0-132">Элемент **Устройства** содержит сводные данные о числе устройств StorSimple серии 8000 в диспетчере устройств StorSimple, сгруппированные по состоянию устройства.</span><span class="sxs-lookup"><span data-stu-id="71bd0-132">The **Devices** tile provides a summary of the number of StorSimple 8000 series devices in your StorSimple Device Manager grouped by device status.</span></span> 

    ![Элемент "Устройства"](./media/storsimple-8000-service-dashboard/service-summary5.png)

    <span data-ttu-id="71bd0-134">Щелкните эту плитку, чтобы открыть колонку **Устройства**, а затем выберите отдельное устройство для получения сводных данных о конкретном устройстве.</span><span class="sxs-lookup"><span data-stu-id="71bd0-134">Click this tile to open the **Devices** list blade and then click an individual device to drill into the device summary specific to the device.</span></span> <span data-ttu-id="71bd0-135">Кроме того, в колонке сводных данных о конкретном устройстве можно выполнять действия с этим устройством.</span><span class="sxs-lookup"><span data-stu-id="71bd0-135">You can also perform device-specific actions from a given device summary blade.</span></span> <span data-ttu-id="71bd0-136">Дополнительные сведения о колонке сводных данных устройства см. в статье [Использование колонки сводных данных об устройстве в диспетчере устройств StorSimple, подключенному к виртуальному массиву StorSimple](storsimple-8000-device-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="71bd0-136">For more information about the device summary blade, go to [Device summary blade](storsimple-8000-device-dashboard.md).</span></span>

    ![Выбор элемента "Устройства"](./media/storsimple-8000-service-dashboard/service-summary9.png)

## <a name="view-the-activity-logs"></a><span data-ttu-id="71bd0-138">Просмотр журналов действий</span><span class="sxs-lookup"><span data-stu-id="71bd0-138">View the activity logs</span></span>

<span data-ttu-id="71bd0-139">Чтобы просмотреть различные операции, выполняемые в диспетчере устройств StorSimple, щелкните ссылку **Журналы действий** в левой части колонки сводных данных о службе StorSimple.</span><span class="sxs-lookup"><span data-stu-id="71bd0-139">To view the various operations carried out within your StorSimple Device Manager, click the **Activity logs** link on the left side of your StorSimple service summary blade.</span></span> <span data-ttu-id="71bd0-140">Отобразится колонка **Журналы действий**, в которой можно просмотреть сводку по последним выполненным операциям.</span><span class="sxs-lookup"><span data-stu-id="71bd0-140">This takes you to the **Activity logs** blade, where you can see a summary of the recent operations carried out.</span></span>

![Журналы действий](./media/storsimple-8000-service-dashboard/activity-logs1.png)
## <a name="next-steps"></a><span data-ttu-id="71bd0-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="71bd0-142">Next steps</span></span>

* <span data-ttu-id="71bd0-143">Узнайте больше об [использовании службы диспетчера устройств StorSimple для администрирования устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="71bd0-143">Learn more about how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

