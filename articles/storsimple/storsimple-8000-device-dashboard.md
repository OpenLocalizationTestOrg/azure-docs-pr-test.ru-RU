---
title: "Сводка устройства серии StorSimple 8000 aaaUse | Документы Microsoft"
description: "Описывает hello устройства StorSimple службы об устройствах и как toouse его tooview метрик хранилища и подключенные инициаторы и найти hello серийный номер и IQN."
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
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="0c89b-103">Используйте hello об устройствах в службе диспетчера StorSimple устройство</span><span class="sxs-lookup"><span data-stu-id="0c89b-103">Use hello device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="0c89b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="0c89b-104">Overview</span></span>
<span data-ttu-id="0c89b-105">Колонка Сводка устройства StorSimple Hello предоставляет общие сведения о соответствии указанного устройства StorSimple, в отличие от toohello службы сводки колонки, где отображаются сведения обо всех устройствах hello, входящих в состав решения Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0c89b-105">hello StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast toohello service summary blade, which gives you information about all hello devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="0c89b-106">Сводка колонке устройства Hello представлена сводная информация устройства серии StorSimple 8000, зарегистрированного с помощью заданного StorSimple диспетчера устройств, выделение неполадки с этих устройств, требующих вмешательства системного администратора.</span><span class="sxs-lookup"><span data-stu-id="0c89b-106">hello device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="0c89b-107">Этого учебника представлено сводки колонке hello устройства, описание содержимого hello и функции и описаны hello задачи, которые можно выполнять из эту колонку.</span><span class="sxs-lookup"><span data-stu-id="0c89b-107">This tutorial introduces hello device summary blade, explains hello content and function, and describes hello tasks that you can perform from this blade.</span></span>

<span data-ttu-id="0c89b-108">Сводка колонке Hello устройства отображает hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="0c89b-108">hello device summary blade displays hello following information:</span></span>

![Колонка сводных данных устройства](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="0c89b-110">Панель команд управления</span><span class="sxs-lookup"><span data-stu-id="0c89b-110">Management command bar</span></span>

<span data-ttu-id="0c89b-111">В колонке устройства StorSimple hello вы видите hello параметры для управления устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0c89b-111">In hello StorSimple device blade, you see hello options for managing your StorSimple device.</span></span> <span data-ttu-id="0c89b-112">Команды управления hello разделе hello верхней части колонки hello и левой стороны hello.</span><span class="sxs-lookup"><span data-stu-id="0c89b-112">You see hello management commands across hello top of hello blade and on hello left side.</span></span> <span data-ttu-id="0c89b-113">Используйте эти параметры tooadd папок или томов, или обновить или отработки отказа устройства.</span><span class="sxs-lookup"><span data-stu-id="0c89b-113">Use these options tooadd shares or volumes, or update or fail over your device.</span></span>

![Панель команд управления](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="0c89b-115">Основные компоненты</span><span class="sxs-lookup"><span data-stu-id="0c89b-115">Essentials</span></span>

<span data-ttu-id="0c89b-116">область essentials Hello записывает некоторые hello важных свойств, таких как, состояние hello, модели, целевой IQN и версия программного обеспечения hello.</span><span class="sxs-lookup"><span data-stu-id="0c89b-116">hello essentials area captures some of hello important properties such as, hello status, model, target IQN, and hello software version.</span></span> 

![Основные компоненты устройства](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="0c89b-118">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="0c89b-118">Monitoring</span></span>

* <span data-ttu-id="0c89b-119">Hello **оповещения** Плитка предоставляет моментальный снимок всех активных оповещений hello для вашего устройства, сгруппированные по уровню серьезности оповещения.</span><span class="sxs-lookup"><span data-stu-id="0c89b-119">hello **Alerts** tile provides a snapshot of all hello active alerts for your device, grouped by alert severity.</span></span>

    ![Элемент "Оповещения"](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="0c89b-121">Щелкните hello tooopen плитки приветствия **оповещения** колонку и нажмите кнопку отдельного предупреждения tooview Дополнительные сведения об этом оповещении, включая все рекомендуемые действия.</span><span class="sxs-lookup"><span data-stu-id="0c89b-121">Click hello tile tooopen hello **Alerts** blade and then click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="0c89b-122">Также можно очищать hello предупреждение, если hello неполадка устранена.</span><span class="sxs-lookup"><span data-stu-id="0c89b-122">You can also clear hello alert if hello issue has been resolved.</span></span>

    ![Щелкните элемент "Оповещения"](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="0c89b-124">Hello **состоянии и работоспособности** плитки позволяет анализировать работоспособность компонента hello оборудования для устройств, включая состояние устройства hello.</span><span class="sxs-lookup"><span data-stu-id="0c89b-124">hello **Status and health** tile provides insights into hello hardware component health for a device including hello device status.</span></span> <span data-ttu-id="0c89b-125">Состояние устройства Hello может быть вне сети, сети, отключено или готовы tooset вверх.</span><span class="sxs-lookup"><span data-stu-id="0c89b-125">hello device status may be offline, online, deactivated, or ready tooset up.</span></span>

    ![Элемент "Состояние и работоспособность"](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="0c89b-127">Hello **тома** плитки Сводная информация о hello число томов в устройстве, сгруппированных по состоянию.</span><span class="sxs-lookup"><span data-stu-id="0c89b-127">hello **Volumes** tile provides a summary of hello number of volumes in your device grouped by status.</span></span>

    ![Элемент "Тома"](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="0c89b-129">Щелкните hello tooopen плитки приветствия **тома** колонки, список, а затем щелкните на отдельный том tooview или измените его свойства.</span><span class="sxs-lookup"><span data-stu-id="0c89b-129">Click hello tile tooopen hello **Volumes** list blade, and then click on an individual volume tooview or modify its properties.</span></span>
    
    ![Щелкните элемент "Тома"](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="0c89b-131">Дополнительные сведения см. в разделе как слишком[управление томами](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="0c89b-131">For more information, see how too[manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="0c89b-132">В hello **использование** диаграммы, можно просмотреть hello основного хранилища, используемые устройства и hello облачного хранилища, используемых в течение hello за последние 7 дней, по умолчанию hello период времени.</span><span class="sxs-lookup"><span data-stu-id="0c89b-132">In hello **Usage** chart, you can view hello primary storage used across your device, and hello cloud storage consumed over hello past 7 days, hello default time period.</span></span>

     ![Плитка "Использование"](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="0c89b-134">toochoose шкалу другое время используйте hello **изменить** параметр в правом верхнем углу hello hello диаграммы.</span><span class="sxs-lookup"><span data-stu-id="0c89b-134">toochoose a different time scale, use hello **Edit** option in hello top-right corner of hello chart.</span></span>

     ![Изменение диаграммы использования](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="0c89b-136">На этой диаграмме можно просмотреть показатели для всего основного хранилища hello (hello объем данных, записанных устройством tooyour узлов) и hello общее Облачное хранилище, используемое устройством за период времени.</span><span class="sxs-lookup"><span data-stu-id="0c89b-136">In this chart, you can view metrics for hello total primary storage (hello amount of data written by hosts tooyour device) and hello total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="0c89b-137">В этом контексте *основного хранилища* ссылается toohello общий объем данных, записанных узлом hello и могут подразделяться по типу тома: *основной многоуровневого хранилища* включает в себя локально хранимые данные и данные облако многоуровневого toohello.</span><span class="sxs-lookup"><span data-stu-id="0c89b-137">In this context, *primary storage* refers toohello total amount of data written by hello host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered toohello cloud.</span></span> <span data-ttu-id="0c89b-138">*Основное локально закрепленное хранилище* включает в себя только данные, хранимые локально.</span><span class="sxs-lookup"><span data-stu-id="0c89b-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="0c89b-139">*Облачное хранилище*, на hello другой стороны, это мера hello общий объем данных, хранящихся в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="0c89b-139">*Cloud storage*, on hello other hand, is a measurement of hello total amount of data stored in hello cloud.</span></span> <span data-ttu-id="0c89b-140">В хранилище содержатся многоуровневые данные и резервные копии.</span><span class="sxs-lookup"><span data-stu-id="0c89b-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="0c89b-141">Hello данные, хранящиеся в облаке hello дедупликации и сжимается, а hello объем хранилища до дедупликации и сжатых данных hello указывает основного хранилища.</span><span class="sxs-lookup"><span data-stu-id="0c89b-141">hello data stored in hello cloud is deduplicated and compressed, whereas primary storage indicates hello amount of storage used before hello data is deduplicated and compressed.</span></span> <span data-ttu-id="0c89b-142">(Вы можете сравнить эти два числа tooget представление о степень сжатия hello). Для основного и облачным хранилищем hello суммы основаны на настроенной частоте отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="0c89b-142">(You can compare these two numbers tooget an idea of hello compression rate.) For both primary and cloud storage, hello amounts shown are based on hello tracking frequency you configure.</span></span> <span data-ttu-id="0c89b-143">Например если частота одну неделю, затем hello диаграмме показано данных за каждый день в hello предыдущей недели.</span><span class="sxs-lookup"><span data-stu-id="0c89b-143">For example, if you choose a one week frequency, then hello chart shows data for each day in hello previous week.</span></span>

     <span data-ttu-id="0c89b-144">toosee hello объем облачного хранилища, используемых в течение времени, выберите hello **ИСПОЛЬЗОВАННЫЙ объем ОБЛАЧНОГО ХРАНИЛИЩА** параметр.</span><span class="sxs-lookup"><span data-stu-id="0c89b-144">toosee hello amount of cloud storage consumed over time, select hello **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="0c89b-145">общий объем хранилища hello toosee, который был записан узлом hello, выберите hello **МНОГОУРОВНЕВОГО ИСПОЛЬЗОВАННЫЙ объем основного ХРАНИЛИЩА** и **ЛОКАЛЬНО ЗАКРЕПЛЕННЫЕ ИСПОЛЬЗОВАННЫЙ объем основного ХРАНИЛИЩА** параметры.</span><span class="sxs-lookup"><span data-stu-id="0c89b-145">toosee hello total storage that has been written by hello host, select hello **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="0c89b-146">Дополнительные сведения см. в разделе [используйте hello toomonitor службы диспетчера StorSimple устройство устройства StorSimple](storsimple-monitor-device.md).</span><span class="sxs-lookup"><span data-stu-id="0c89b-146">For more information, see [Use hello StorSimple Device Manager service toomonitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="0c89b-147">Hello **емкость** плитки отображает hello основного хранилища, предоставляемому и оставшийся через hello устройства относительный toohello общего объема хранилища для hello таким же.</span><span class="sxs-lookup"><span data-stu-id="0c89b-147">hello **Capacity** tile displays hello primary storage that is provisioned and remaining across hello device relative toohello total storage available for hello same.</span></span> <span data-ttu-id="0c89b-148">**Подготовить** ссылается toohello объем хранилища, подготовлена и выделенный для использования, **остаток** ссылается toohello оставшихся емкости, которая может предоставляться через это устройство.</span><span class="sxs-lookup"><span data-stu-id="0c89b-148">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, **Remaining** refers toohello remaining capacity that can be provisioned across this device.</span></span> 

    ![Плитка "Использование"](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="0c89b-150">Щелкните этот tooview плитки, как hello емкость предоставляется через многоуровневого и локально закрепленного тома.</span><span class="sxs-lookup"><span data-stu-id="0c89b-150">Click this tile tooview how hello capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="0c89b-151">Hello **оставшиеся многоуровневого** емкость — hello доступной емкости, которая может быть подготовлена, включая облачные при hello **оставшиеся локального** — объем hello, оставшихся на дисках hello toothis устройство подключено.</span><span class="sxs-lookup"><span data-stu-id="0c89b-151">hello **Remaining Tiered** capacity is hello available capacity that can be provisioned including cloud, while hello **Remaining Local** is hello capacity remaining on hello disks attached toothis device.</span></span>

    ![Щелкните диаграмму использования](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="0c89b-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0c89b-153">Next steps</span></span>
* <span data-ttu-id="0c89b-154">Дополнительные сведения о hello [сводки колонке службы StorSimple](storsimple-8000-service-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="0c89b-154">Learn more about hello [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="0c89b-155">Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0c89b-155">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

