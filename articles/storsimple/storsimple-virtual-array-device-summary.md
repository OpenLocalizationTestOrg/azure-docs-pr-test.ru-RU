---
title: "Сводка колонке aaaStorSimple Virtual Array устройства | Документы Microsoft"
description: "Описание сводки колонке hello устройства для устройства StorSimple и как toouse его работоспособность hello toomonitor виртуального массива StorSimple."
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
ms.openlocfilehash: 3649eaac8a924a772f310a809ddf9706e912157a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-blade-for-storsimple-device-manager-connected-toostorsimple-virtual-array"></a><span data-ttu-id="b9fee-103">Используйте hello устройства сводки колонку для устройства StorSimple подключен tooStorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="b9fee-103">Use hello device summary blade for StorSimple Device Manager connected tooStorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="b9fee-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b9fee-104">Overview</span></span>

<span data-ttu-id="b9fee-105">Hello устройства StorSimple устройство колонке предоставляет Сводная информация о StorSimple Virtual Array, зарегистрированного с помощью заданного StorSimple диспетчера устройств, выделение неполадки с этих устройств, требующих вмешательства системного администратора.</span><span class="sxs-lookup"><span data-stu-id="b9fee-105">hello StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="b9fee-106">Этого учебника представлено сводки колонке hello устройства, описание содержимого hello и функции и описаны hello задачи, которые можно выполнять из эту колонку.</span><span class="sxs-lookup"><span data-stu-id="b9fee-106">This tutorial introduces hello device summary blade, explains hello content and function, and describes hello tasks that you can perform from this blade.</span></span>

<span data-ttu-id="b9fee-107">Сводка колонке Hello устройства отображает hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="b9fee-107">hello device summary blade displays hello following information:</span></span>

![Панель мониторинга устройства](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="b9fee-109">управления</span><span class="sxs-lookup"><span data-stu-id="b9fee-109">Management</span></span>

<span data-ttu-id="b9fee-110">В колонке устройства StorSimple hello вы видите hello параметры для управления устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b9fee-110">In hello StorSimple device blade, you see hello options for managing your StorSimple device.</span></span> <span data-ttu-id="b9fee-111">Команды управления hello разделе hello верхней части колонки hello и левой стороны hello.</span><span class="sxs-lookup"><span data-stu-id="b9fee-111">You see hello management commands across hello top of hello blade and on hello left side.</span></span> <span data-ttu-id="b9fee-112">Используйте эти параметры tooadd папок или томов, или обновить или переключения виртуального массива.</span><span class="sxs-lookup"><span data-stu-id="b9fee-112">Use these options tooadd shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="b9fee-113">Hello области essentials записывает некоторые hello важных свойств, таких как, состояние hello, модели, версии программного обеспечения а также toohello ссылку **веб-интерфейса** hello массива.</span><span class="sxs-lookup"><span data-stu-id="b9fee-113">hello essentials area captures some of hello important properties such as, hello status, model, software version as well as a link toohello **Web UI** of hello array.</span></span> <span data-ttu-id="b9fee-114">Если находятся во внутренней сети, можно запустить напрямую hello [локальный веб-Интерфейс](storsimple-ova-web-ui-admin.md) tooadminister виртуального массива.</span><span class="sxs-lookup"><span data-stu-id="b9fee-114">If you are on an internal network, you can directly launch hello [local web UI](storsimple-ova-web-ui-admin.md) tooadminister your virtual array.</span></span>

![Основные компоненты устройства](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="b9fee-116">Сводка по устройству StorSimple</span><span class="sxs-lookup"><span data-stu-id="b9fee-116">StorSimple device summary</span></span>

* <span data-ttu-id="b9fee-117">Hello **оповещения** Плитка предоставляет моментальный снимок всех активных оповещений hello виртуального массива, сгруппированных по уровню серьезности оповещения.</span><span class="sxs-lookup"><span data-stu-id="b9fee-117">hello **Alerts** tile provides a snapshot of all hello active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="b9fee-118">Щелкните hello tooopen плитки приветствия **оповещения** колонку и нажмите кнопку отдельного предупреждения tooview Дополнительные сведения об этом оповещении, включая все рекомендуемые действия.</span><span class="sxs-lookup"><span data-stu-id="b9fee-118">Click hello tile tooopen hello **Alerts** blade and then click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="b9fee-119">Также можно очищать hello предупреждение, если hello неполадка устранена.</span><span class="sxs-lookup"><span data-stu-id="b9fee-119">You can also clear hello alert if hello issue has been resolved.</span></span>

* <span data-ttu-id="b9fee-120">Hello **емкость** плитки отображает hello основного хранилища, предоставляемому и оставшийся через hello виртуального устройства относительный toohello общего объема хранилища для hello таким же.</span><span class="sxs-lookup"><span data-stu-id="b9fee-120">hello **Capacity** tile displays hello primary storage that is provisioned and remaining across hello virtual device relative toohello total storage available for hello same.</span></span> <span data-ttu-id="b9fee-121">**Подготовить** ссылается toohello объем хранилища, подготовлена и выделенный для использования, **остаток** ссылается toohello оставшихся емкости, которая может предоставляться через это устройство.</span><span class="sxs-lookup"><span data-stu-id="b9fee-121">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, **Remaining** refers toohello remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="b9fee-122">Hello **оставшиеся многоуровневого** емкость — hello доступной емкости, которая может быть подготовлена, включая облачные при hello **оставшиеся локального** — объем hello, оставшихся на дисках hello присоединенного toothis виртуальный массив.</span><span class="sxs-lookup"><span data-stu-id="b9fee-122">hello **Remaining Tiered** capacity is hello available capacity that can be provisioned including cloud, while hello **Remaining Local** is hello capacity remaining on hello disks attached toothis virtual array.</span></span>

* <span data-ttu-id="b9fee-123">В hello **использование** диаграммы, можно просмотреть hello основного хранилища в масштабах виртуального массива, а также hello облачного хранилища, используемых в течение hello за последние 7 дней, по умолчанию hello период времени.</span><span class="sxs-lookup"><span data-stu-id="b9fee-123">In hello **Usage** chart, you can view hello primary storage used across your virtual array, as well as hello cloud storage consumed  over hello past 7 days, hello default time period.</span></span> <span data-ttu-id="b9fee-124">Используйте hello **изменить** параметр в правом верхнем углу hello toochoose диаграммы hello шкалу другое время.</span><span class="sxs-lookup"><span data-stu-id="b9fee-124">Use hello **Edit** option in hello top-right corner of hello chart toochoose a different time scale.</span></span>

* <span data-ttu-id="b9fee-125">Hello **долей** или **тома** плитки Сводная информация о hello количество папок или томов в устройстве, сгруппированных по состоянию.</span><span class="sxs-lookup"><span data-stu-id="b9fee-125">hello **Shares** or **Volumes** tile provides a summary of hello number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="b9fee-126">Щелкните hello tooopen плитки приветствия **общих папок** или **тома** список колонке и щелкните отдельные папки или тома tooview или измените его свойства.</span><span class="sxs-lookup"><span data-stu-id="b9fee-126">Click hello tile tooopen hello **Shares**  or **Volumes** list blade, and then click on an individual share or volume tooview or modify its properties.</span></span> <span data-ttu-id="b9fee-127">Дополнительные сведения см. в разделе как слишком[Управление общими папками](storsimple-virtual-array-manage-shares.md) или [управление томами](storsimple-virtual-array-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="b9fee-127">For more information, see how too[manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9fee-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9fee-128">Next steps</span></span>
<span data-ttu-id="b9fee-129">Ниже перечислено, что вы можете узнать.</span><span class="sxs-lookup"><span data-stu-id="b9fee-129">Learn how to:</span></span>
- [<span data-ttu-id="b9fee-130">Управление общими файловыми ресурсами в виртуальном массиве StorSimple</span><span class="sxs-lookup"><span data-stu-id="b9fee-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="b9fee-131">Управление томами в виртуальном массиве StorSimple</span><span class="sxs-lookup"><span data-stu-id="b9fee-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

