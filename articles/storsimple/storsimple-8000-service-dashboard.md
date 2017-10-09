---
title: "Сводка устройства серии StorSimple 8000 aaaUse | Документы Microsoft"
description: "Описывает колонке сводки службы StorSimple hello и объясняет, как toouse его toomonitor hello работоспособность решения StorSimple."
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
ms.openlocfilehash: ec1d971a8656df0be6eb1e3ec2603d97737ff070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-summary-blade-for-storsimple-8000-series-device"></a><span data-ttu-id="1b569-103">Используйте сводки колонке hello службы для устройства серии StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="1b569-103">Use hello service summary blade for StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="1b569-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="1b569-104">Overview</span></span>

<span data-ttu-id="1b569-105">Сводка колонке Hello устройства StorSimple службы предоставляет сводное представление всех hello устройствах, подключенных toohello службе диспетчера устройств StorSimple, с выделением тех устройств, которые требуется внимание системных администраторов.</span><span class="sxs-lookup"><span data-stu-id="1b569-105">hello StorSimple Device Manager service summary blade provides a summary view of all hello devices that are connected toohello StorSimple Device Manager service, highlighting those devices that need a system administrator's attention.</span></span> <span data-ttu-id="1b569-106">Этот учебник представлено сводки колонке hello службы, описывается содержимое панели hello и функции и описаны hello задачи, которые можно выполнять на этой странице.</span><span class="sxs-lookup"><span data-stu-id="1b569-106">This tutorial introduces hello service summary blade, explains hello dashboard content and function, and describes hello tasks that you can perform from this page.</span></span>

![Сводка по службе](./media/storsimple-8000-service-dashboard/service-summary1.png)


## <a name="management-commands"></a><span data-ttu-id="1b569-108">Команды управления</span><span class="sxs-lookup"><span data-stu-id="1b569-108">Management commands</span></span>

<span data-ttu-id="1b569-109">В hello StorSimple службы сводки колонки отображается hello параметры для управления службой диспетчера устройств StorSimple и службы toothis зарегистрированных устройств серии hello StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="1b569-109">In hello StorSimple service summary blade, you see hello options for managing your StorSimple Device Manager service and hello StorSimple 8000 series devices registered toothis service.</span></span> <span data-ttu-id="1b569-110">Команды управления hello разделе hello верхней части колонки hello и левой стороны hello.</span><span class="sxs-lookup"><span data-stu-id="1b569-110">You see hello management commands across hello top of hello blade and on hello left side.</span></span>

![Панель команд](./media/storsimple-8000-service-dashboard/service-summary2.png)

<span data-ttu-id="1b569-112">Используйте эти параметры, tooperform различные операции такие как добавление общих папок или томов или монитор hello различных заданий, выполняемых на устройствах StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="1b569-112">Use these options tooperform various operations such as add shares or volumes, or monitor hello various jobs running on hello StorSimple devices.</span></span>


## <a name="essentials"></a><span data-ttu-id="1b569-113">Основные компоненты</span><span class="sxs-lookup"><span data-stu-id="1b569-113">Essentials</span></span>

<span data-ttu-id="1b569-114">область essentials Hello записывает некоторые важные свойства hello, такие как группы ресурсов hello, местоположение и подписку, в которой был создан в диспетчере устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1b569-114">hello essentials area captures some of hello important properties such as, hello resource group, location, and subscription in which your StorSimple Device Manager was created.</span></span>

![Основные компоненты](./media/storsimple-8000-service-dashboard/service-summary3.png)

## <a name="storsimple-device-manager-service-summary"></a><span data-ttu-id="1b569-116">Сводные данные о службе диспетчера устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="1b569-116">StorSimple Device Manager service summary</span></span>

* <span data-ttu-id="1b569-117">Hello **оповещения** Плитка предоставляет моментальный снимок всех активных оповещений hello на всех устройствах, сгруппированных по уровню серьезности оповещения.</span><span class="sxs-lookup"><span data-stu-id="1b569-117">hello **Alerts** tile provides a snapshot of all hello active alerts across all devices, grouped by alert severity.</span></span>

    ![Элемент "Оповещения"](./media/storsimple-8000-service-dashboard/service-summary4.png)

    <span data-ttu-id="1b569-119">Выбрав hello плитки открывает hello **оповещения** колонке там, где можно щелкнуть отдельные предупреждения tooview Дополнительные сведения об этом оповещении, включая все рекомендуемые действия.</span><span class="sxs-lookup"><span data-stu-id="1b569-119">Clicking hello tile opens hello **Alerts** blade, where you can click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="1b569-120">Также можно очищать hello предупреждение, если hello неполадка устранена.</span><span class="sxs-lookup"><span data-stu-id="1b569-120">You can also clear hello alert if hello issue has been resolved.</span></span>

    ![Выбор элемента "Оповещения"](./media/storsimple-8000-service-dashboard/service-summary8.png)

* <span data-ttu-id="1b569-122">Hello **емкость** плитке отображается показано hello объем основного хранилища, подготовлена и оставшихся на всех устройствах относительный toohello общего объема хранилища на всех устройствах.</span><span class="sxs-lookup"><span data-stu-id="1b569-122">hello **Capacity** tile displays shows hello primary storage that is provisioned and remaining across all devices relative toohello total storage available across all devices.</span></span> <span data-ttu-id="1b569-123">**Подготовить** ссылается toohello объем хранилища, подготовлена и выделенный для использования, **остаток** ссылается toohello оставшихся емкости, которая может предоставляться на всех устройствах.</span><span class="sxs-lookup"><span data-stu-id="1b569-123">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, **Remaining** refers toohello remaining capacity that can be provisioned across all devices.</span></span>

    ![Элемент "Емкость"](./media/storsimple-8000-service-dashboard/service-summary6.png)

    <span data-ttu-id="1b569-125">Hello **оставшиеся многоуровневого** емкость — hello доступной емкости, которая может быть подготовлена, включая облачные при hello **оставшиеся локального** — объем hello, оставшихся на дисках hello присоединенного toohello Устройства серии StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="1b569-125">hello **Remaining Tiered** capacity is hello available capacity that can be provisioned including cloud, while hello **Remaining Local** is hello capacity remaining on hello disks attached toohello StorSimple 8000 series devices.</span></span>


* <span data-ttu-id="1b569-126">В hello **использование** диаграммы, для устройств можно увидеть соответствующие метрики hello.</span><span class="sxs-lookup"><span data-stu-id="1b569-126">In hello **Usage** chart, you can see hello relevant metrics for your devices.</span></span> <span data-ttu-id="1b569-127">Вы можете просмотреть hello основного хранилища, используемый для всех устройств и hello облачного хранилища, используемые устройствами через hello за последние 7 дней, по умолчанию hello период времени.</span><span class="sxs-lookup"><span data-stu-id="1b569-127">You can view hello primary storage used across all devices, and hello cloud storage consumed by devices over hello past 7 days, hello default time period.</span></span> 

    ![Плитка "Использование"](./media/storsimple-8000-service-dashboard/service-summary7.png) 

    <span data-ttu-id="1b569-129">toochoose шкалу другое время используйте hello **изменить** параметр в правом верхнем углу hello hello диаграммы.</span><span class="sxs-lookup"><span data-stu-id="1b569-129">toochoose a different time scale, use hello **Edit** option in hello top-right corner of hello chart.</span></span>

     ![Выбор элемента "Использование"](./media/storsimple-8000-service-dashboard/service-summary10.png)

     ![Экспорт данных диаграммы](./media/storsimple-8000-service-dashboard/service-summary11.png)

* <span data-ttu-id="1b569-132">Hello **устройств** Плитка предоставляет сводку hello количеством устройств серии StorSimple 8000 в своем StorSimple устройство Manager группируются по состоянию устройства.</span><span class="sxs-lookup"><span data-stu-id="1b569-132">hello **Devices** tile provides a summary of hello number of StorSimple 8000 series devices in your StorSimple Device Manager grouped by device status.</span></span> 

    ![Элемент "Устройства"](./media/storsimple-8000-service-dashboard/service-summary5.png)

    <span data-ttu-id="1b569-134">Щелкните этот hello tooopen плитки **устройств** колонки, затем щелкните toodrill отдельное устройство в устройство сводки toohello конкретного устройства hello.</span><span class="sxs-lookup"><span data-stu-id="1b569-134">Click this tile tooopen hello **Devices** list blade and then click an individual device toodrill into hello device summary specific toohello device.</span></span> <span data-ttu-id="1b569-135">Кроме того, в колонке сводных данных о конкретном устройстве можно выполнять действия с этим устройством.</span><span class="sxs-lookup"><span data-stu-id="1b569-135">You can also perform device-specific actions from a given device summary blade.</span></span> <span data-ttu-id="1b569-136">Дополнительные сведения о колонке Сводка устройства hello go слишком[сводки колонке устройства](storsimple-8000-device-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="1b569-136">For more information about hello device summary blade, go too[Device summary blade](storsimple-8000-device-dashboard.md).</span></span>

    ![Выбор элемента "Устройства"](./media/storsimple-8000-service-dashboard/service-summary9.png)

## <a name="view-hello-activity-logs"></a><span data-ttu-id="1b569-138">Просмотр журналов действие hello</span><span class="sxs-lookup"><span data-stu-id="1b569-138">View hello activity logs</span></span>

<span data-ttu-id="1b569-139">hello tooview различные операции выполняются в рамках вашей StorSimple диспетчер устройств, нажмите кнопку hello **журналы действий** ссылку на hello слева от оператора к колонке сводки службы StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1b569-139">tooview hello various operations carried out within your StorSimple Device Manager, click hello **Activity logs** link on hello left side of your StorSimple service summary blade.</span></span> <span data-ttu-id="1b569-140">После этого вы перейдете toohello **журналы действий** колонки, где можно просмотреть сводку последних операций hello выполнена.</span><span class="sxs-lookup"><span data-stu-id="1b569-140">This takes you toohello **Activity logs** blade, where you can see a summary of hello recent operations carried out.</span></span>

![Журналы действий](./media/storsimple-8000-service-dashboard/activity-logs1.png)
## <a name="next-steps"></a><span data-ttu-id="1b569-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1b569-142">Next steps</span></span>

* <span data-ttu-id="1b569-143">Дополнительные сведения о том, как слишком[используйте hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="1b569-143">Learn more about how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

