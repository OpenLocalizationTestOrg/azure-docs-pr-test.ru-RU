---
title: "Замена корпуса устройства StorSimple серии 8000 | Документация Майкрософт"
description: "Эта статья описывает снятие и установку основного корпуса или корпуса EBOD устройства StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5295c5dd039b1d4746ebaaf90372932e4c3e7c26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-chassis-on-your-storsimple-device"></a><span data-ttu-id="63e26-103">Замена корпуса устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="63e26-103">Replace the chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="63e26-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="63e26-104">Overview</span></span>
<span data-ttu-id="63e26-105">В этом учебнике объясняется, как снять и заменить корпус устройства StorSimple серии 8000.</span><span class="sxs-lookup"><span data-stu-id="63e26-105">This tutorial explains how to remove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="63e26-106">Модель StorSimple 8100 — устройство в отдельном корпусе (один корпус), тогда как модель 8600 состоит из двух корпусов (два корпуса).</span><span class="sxs-lookup"><span data-stu-id="63e26-106">The StorSimple 8100 model is a single enclosure device (one chassis), whereas the 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="63e26-107">В модели 8600 неисправность может возникнуть в двух корпусах: в основном корпусе и в корпусе EBOD.</span><span class="sxs-lookup"><span data-stu-id="63e26-107">For an 8600 model, there are potentially two chassis that could fail in the device: the chassis for the primary enclosure or the chassis for the EBOD enclosure.</span></span>

<span data-ttu-id="63e26-108">В каждом из этих случаев Майкрософт предоставляет на замену пустой корпус.</span><span class="sxs-lookup"><span data-stu-id="63e26-108">In either case, the replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="63e26-109">В комплект поставки не входят блоки питания и охлаждения (БПО), модули контроллера, твердотельные дисковые накопители (SSD), жесткие диски (HDD) и модули EBOD.</span><span class="sxs-lookup"><span data-stu-id="63e26-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63e26-110">Перед снятием и заменой корпуса ознакомьтесь со сведениями о безопасности в разделе [Замена компонентов оборудования StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="63e26-110">Before removing and replacing the chassis, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-the-chassis"></a><span data-ttu-id="63e26-111">Снятие корпуса</span><span class="sxs-lookup"><span data-stu-id="63e26-111">Remove the chassis</span></span>
<span data-ttu-id="63e26-112">Выполните следующие действия для снятия корпуса устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="63e26-112">Perform the following steps to remove the chassis on your StorSimple device.</span></span>

#### <a name="to-remove-a-chassis"></a><span data-ttu-id="63e26-113">Снятие корпуса</span><span class="sxs-lookup"><span data-stu-id="63e26-113">To remove a chassis</span></span>
1. <span data-ttu-id="63e26-114">Убедитесь, что устройство StorSimple выключено и отключено от всех источников питания.</span><span class="sxs-lookup"><span data-stu-id="63e26-114">Make sure that the StorSimple device is shut down and disconnected from all the power sources.</span></span>
2. <span data-ttu-id="63e26-115">Отключите все сетевые кабели и кабели SAS, если они используются.</span><span class="sxs-lookup"><span data-stu-id="63e26-115">Remove all the network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="63e26-116">Извлеките устройство из стойки.</span><span class="sxs-lookup"><span data-stu-id="63e26-116">Remove the unit from the rack.</span></span>
4. <span data-ttu-id="63e26-117">Извлеките каждый из дисков и запишите номера слотов, из которых они извлекаются.</span><span class="sxs-lookup"><span data-stu-id="63e26-117">Remove each of the drives and note the slots from which they are removed.</span></span> <span data-ttu-id="63e26-118">Дополнительные сведения см. в разделе [Снять жесткий диск](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="63e26-118">For more information, see [Remove the disk drive](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="63e26-119">Для корпуса EBOD (при неисправности корпуса) снимите модули контроллеров EBOD.</span><span class="sxs-lookup"><span data-stu-id="63e26-119">On the EBOD enclosure (if this is the chassis that failed), remove the EBOD controller modules.</span></span> <span data-ttu-id="63e26-120">Дополнительные сведения см. в разделе [Снятие контроллера EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="63e26-120">For more information, see [Remove an EBOD controller](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span> 
   
    <span data-ttu-id="63e26-121">Для основного корпуса (при неисправности корпуса) снимите модули контроллеров и запишите номера слотов, в которых они находились.</span><span class="sxs-lookup"><span data-stu-id="63e26-121">On the primary enclosure (if this is the chassis that failed), remove the controllers and note the slots from which they are removed.</span></span> <span data-ttu-id="63e26-122">Дополнительные сведения см. в разделе [Снятие контроллера](storsimple-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="63e26-122">For more information, see [Remove a controller](storsimple-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-the-chassis"></a><span data-ttu-id="63e26-123">Установка корпуса</span><span class="sxs-lookup"><span data-stu-id="63e26-123">Install the chassis</span></span>
<span data-ttu-id="63e26-124">Чтобы установить корпус устройства StorSimple, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="63e26-124">Perform the following steps to install the chassis on your StorSimple device.</span></span>

#### <a name="to-install-a-chassis"></a><span data-ttu-id="63e26-125">Установка корпуса</span><span class="sxs-lookup"><span data-stu-id="63e26-125">To install a chassis</span></span>
1. <span data-ttu-id="63e26-126">Установите корпус в стойку.</span><span class="sxs-lookup"><span data-stu-id="63e26-126">Mount the chassis in the rack.</span></span> <span data-ttu-id="63e26-127">Дополнительные сведения см. в разделах [Установка устройства StorSimple 8100 в стойку](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) или [Установка устройства StorSimple 8600 в стойку](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="63e26-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="63e26-128">После установки корпуса в стойку установите модули контроллера так же, как они были установлены ранее.</span><span class="sxs-lookup"><span data-stu-id="63e26-128">After the chassis is mounted in the rack, install the controller modules in the same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="63e26-129">Установите диски в те же слоты, в которые они были установлены ранее.</span><span class="sxs-lookup"><span data-stu-id="63e26-129">Install the drives in the same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="63e26-130">Рекомендуется сначала устанавливать твердотельные жесткие диски, а затем жесткие диски.</span><span class="sxs-lookup"><span data-stu-id="63e26-130">We recommend that you install the SSDs in the slots first, and then install the HDDs.</span></span>
   > 
   > 
4. <span data-ttu-id="63e26-131">После установки корпуса в стойку и установки компонентов подключите устройство к соответствующим источникам питания и включите устройство.</span><span class="sxs-lookup"><span data-stu-id="63e26-131">With the device mounted in the rack and the components installed, connect your device to the appropriate power sources, and turn on the device.</span></span> <span data-ttu-id="63e26-132">Дополнительные сведения см. в разделах [Подключение кабельного хозяйства к устройству StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) или [Подключение кабельного хозяйства к устройству StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="63e26-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="63e26-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63e26-133">Next steps</span></span>
<span data-ttu-id="63e26-134">Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="63e26-134">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

