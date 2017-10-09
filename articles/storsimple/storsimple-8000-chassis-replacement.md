---
title: "корпус aaaReplace на устройства серии StorSimple 8000 | Документы Microsoft"
description: "Описывает, как tooremove и замены hello корпуса для StorSimple основного корпуса или корпуса EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 94bbd3d354a9b8866ece036238927e67ec5ce2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a><span data-ttu-id="6c1d3-103">Замена шасси hello на устройстве StorSimple</span><span class="sxs-lookup"><span data-stu-id="6c1d3-103">Replace hello chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="6c1d3-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="6c1d3-104">Overview</span></span>
<span data-ttu-id="6c1d3-105">В этом учебнике описано как tooremove и заменить шасси в устройства серии StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-105">This tutorial explains how tooremove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="6c1d3-106">модель StorSimple 8100 Hello является устройство с одним корпусом (одним шасси), тогда как hello 8600 состоит из двух корпусов (два шасси).</span><span class="sxs-lookup"><span data-stu-id="6c1d3-106">hello StorSimple 8100 model is a single enclosure device (one chassis), whereas hello 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="6c1d3-107">В моделях 8600 являются потенциально два шасси, которые может завершиться ошибкой в устройстве hello: hello шасси для основного корпуса hello или hello шасси для корпуса EBOD hello.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-107">For an 8600 model, there are potentially two chassis that could fail in hello device: hello chassis for hello primary enclosure or hello chassis for hello EBOD enclosure.</span></span>

<span data-ttu-id="6c1d3-108">В любом случае hello запасное шасси, поставляемое компанией Майкрософт является пустым.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-108">In either case, hello replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="6c1d3-109">В комплект поставки не входят блоки питания и охлаждения (БПО), модули контроллера, твердотельные дисковые накопители (SSD), жесткие диски (HDD) и модули EBOD.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c1d3-110">До удаления и замены шасси hello, просмотрите сведения о безопасности hello в [замена компонентов оборудования StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="6c1d3-110">Before removing and replacing hello chassis, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-chassis"></a><span data-ttu-id="6c1d3-111">Удаление шасси hello</span><span class="sxs-lookup"><span data-stu-id="6c1d3-111">Remove hello chassis</span></span>
<span data-ttu-id="6c1d3-112">Выполните следующие шаги tooremove hello корпуса на устройстве StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-112">Perform hello following steps tooremove hello chassis on your StorSimple device.</span></span>

#### <a name="tooremove-a-chassis"></a><span data-ttu-id="6c1d3-113">tooremove шасси</span><span class="sxs-lookup"><span data-stu-id="6c1d3-113">tooremove a chassis</span></span>
1. <span data-ttu-id="6c1d3-114">Убедитесь в том, что это устройство StorSimple hello выключено и отключено от всех источников питания hello.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-114">Make sure that hello StorSimple device is shut down and disconnected from all hello power sources.</span></span>
2. <span data-ttu-id="6c1d3-115">Удалите все сети hello и кабели SAS, если это применимо.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-115">Remove all hello network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="6c1d3-116">Удалите устройство hello из стойки hello.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-116">Remove hello unit from hello rack.</span></span>
4. <span data-ttu-id="6c1d3-117">Извлеките каждого из устройств hello и отметьте слоты hello, от которых они будут удалены.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-117">Remove each of hello drives and note hello slots from which they are removed.</span></span> <span data-ttu-id="6c1d3-118">Дополнительные сведения см. в разделе [удалить диск hello](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="6c1d3-118">For more information, see [Remove hello disk drive](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="6c1d3-119">Удалите hello модулей контроллера EBOD на hello корпуса EBOD (если это hello шасси, сбой).</span><span class="sxs-lookup"><span data-stu-id="6c1d3-119">On hello EBOD enclosure (if this is hello chassis that failed), remove hello EBOD controller modules.</span></span> <span data-ttu-id="6c1d3-120">Дополнительные сведения см. в разделе [Снятие контроллера EBOD](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="6c1d3-120">For more information, see [Remove an EBOD controller](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span>
   
    <span data-ttu-id="6c1d3-121">На hello основной корпус (если это hello шасси, сбой), удалите hello контроллеры и отметьте слоты hello, от которых они будут удалены.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-121">On hello primary enclosure (if this is hello chassis that failed), remove hello controllers and note hello slots from which they are removed.</span></span> <span data-ttu-id="6c1d3-122">Дополнительные сведения см. в разделе [Снятие контроллера](storsimple-8000-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="6c1d3-122">For more information, see [Remove a controller](storsimple-8000-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-hello-chassis"></a><span data-ttu-id="6c1d3-123">Установка шасси hello</span><span class="sxs-lookup"><span data-stu-id="6c1d3-123">Install hello chassis</span></span>
<span data-ttu-id="6c1d3-124">Выполните следующие шаги tooinstall hello корпуса на устройстве StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-124">Perform hello following steps tooinstall hello chassis on your StorSimple device.</span></span>

#### <a name="tooinstall-a-chassis"></a><span data-ttu-id="6c1d3-125">tooinstall шасси</span><span class="sxs-lookup"><span data-stu-id="6c1d3-125">tooinstall a chassis</span></span>
1. <span data-ttu-id="6c1d3-126">Подключите hello корпуса в стойку hello.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-126">Mount hello chassis in hello rack.</span></span> <span data-ttu-id="6c1d3-127">Дополнительные сведения см. в разделах [Установка устройства StorSimple 8100 в стойку](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) или [Установка устройства StorSimple 8600 в стойку](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="6c1d3-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="6c1d3-128">После hello шасси в стойке hello, установите модули контроллера hello в приветствия же устанавливает, что они были установлены в.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-128">After hello chassis is mounted in hello rack, install hello controller modules in hello same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="6c1d3-129">Установка hello дисков в hello же размещает и слотов, они были установлены в.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-129">Install hello drives in hello same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6c1d3-130">Рекомендуется сначала установить hello SSDs в слотах hello и затем установить HDD hello.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-130">We recommend that you install hello SSDs in hello slots first, and then install hello HDDs.</span></span>
  
4. <span data-ttu-id="6c1d3-131">С hello устройства в стойку hello и установленных компонентов hello подключение вашего устройства toohello соответствующим источниками питания, включите устройство hello.</span><span class="sxs-lookup"><span data-stu-id="6c1d3-131">With hello device mounted in hello rack and hello components installed, connect your device toohello appropriate power sources, and turn on hello device.</span></span> <span data-ttu-id="6c1d3-132">Дополнительные сведения см. в разделах [Подключение кабельного хозяйства к устройству StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) или [Подключение кабельного хозяйства к устройству StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="6c1d3-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c1d3-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c1d3-133">Next steps</span></span>
<span data-ttu-id="6c1d3-134">Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="6c1d3-134">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

