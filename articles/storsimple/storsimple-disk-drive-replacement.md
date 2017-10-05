---
title: "Замена диска на устройстве StorSimple | Документация Майкрософт"
description: "В статье объясняется, как заменить диск в основном корпусе StorSimple или в корпусе EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 0659ab9d304dbfcce72e8c3c79edad68e70b9630
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a><span data-ttu-id="4ed0c-103">Замена диска на устройстве StorSimple</span><span class="sxs-lookup"><span data-stu-id="4ed0c-103">Replace a disk drive on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="4ed0c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="4ed0c-104">Overview</span></span>
<span data-ttu-id="4ed0c-105">В этом учебнике объясняется, как снять и заменить неисправный или вышедший из строя жесткий диск на устройстве Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="4ed0c-106">Для замены жесткого диска необходимо:</span><span class="sxs-lookup"><span data-stu-id="4ed0c-106">To replace a disk drive, you need to:</span></span>

* <span data-ttu-id="4ed0c-107">открыть защитную защелку;</span><span class="sxs-lookup"><span data-stu-id="4ed0c-107">Disengage the antitamper lock</span></span>
* <span data-ttu-id="4ed0c-108">снять жесткий диск;</span><span class="sxs-lookup"><span data-stu-id="4ed0c-108">Remove the disk drive</span></span>
* <span data-ttu-id="4ed0c-109">установить новый жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-109">Install the replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ed0c-110">Перед снятием и заменой диска ознакомьтесь со сведениями о безопасности в разделе [Замена компонентов оборудования StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="4ed0c-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="disengage-the-antitamper-lock"></a><span data-ttu-id="4ed0c-111">открыть защитную защелку;</span><span class="sxs-lookup"><span data-stu-id="4ed0c-111">Disengage the antitamper lock</span></span>
<span data-ttu-id="4ed0c-112">Эта процедура объясняет, как открыть и закрыть защитную защелку при замене дисков на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span></span> <span data-ttu-id="4ed0c-113">Защитная защелка расположена на передней панели дискового модуля, и для доступа к ней используется маленькая щель в области защелки на передней панели.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span></span> <span data-ttu-id="4ed0c-114">Диски поставляются с закрытыми защитными защелками.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-114">Drives are supplied with the locks set to the locked position.</span></span>

#### <a name="to-unlock-the-antitamper-lock"></a><span data-ttu-id="4ed0c-115">Чтобы открыть защитную защелку</span><span class="sxs-lookup"><span data-stu-id="4ed0c-115">To unlock the antitamper lock</span></span>
1. <span data-ttu-id="4ed0c-116">Аккуратно вставьте ключ ("антивандальную" отвертку T10, предоставляемую Майкрософт) в гнездо сквозь щель.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="4ed0c-117">Если защелка закрыта, то в щели будет виден красный индикатор.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span></span>
   > 
   > 
   
    ![Диск с закрытой защитной защелкой](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="4ed0c-119">**Рис. 1.** Защитная защелка закрыта</span><span class="sxs-lookup"><span data-stu-id="4ed0c-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="4ed0c-120">Метка</span><span class="sxs-lookup"><span data-stu-id="4ed0c-120">Label</span></span> | <span data-ttu-id="4ed0c-121">Описание</span><span class="sxs-lookup"><span data-stu-id="4ed0c-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="4ed0c-122">1</span><span class="sxs-lookup"><span data-stu-id="4ed0c-122">1</span></span> |<span data-ttu-id="4ed0c-123">Щель индикатора</span><span class="sxs-lookup"><span data-stu-id="4ed0c-123">Indicator aperture</span></span> |
   | <span data-ttu-id="4ed0c-124">2</span><span class="sxs-lookup"><span data-stu-id="4ed0c-124">2</span></span> |<span data-ttu-id="4ed0c-125">Защитная защелка</span><span class="sxs-lookup"><span data-stu-id="4ed0c-125">Antitamper lock</span></span> |
2. <span data-ttu-id="4ed0c-126">Поворачивайте ключ против часовой стрелки, пока красный индикатор в щели над ключом не перестанет быть видимым.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span></span>
3. <span data-ttu-id="4ed0c-127">Извлеките ключ.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-127">Remove the key.</span></span>
   
    ![Защитная защелка открыта](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="4ed0c-129">**Рис. 2.** Защитная защелка открыта</span><span class="sxs-lookup"><span data-stu-id="4ed0c-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="4ed0c-130">Теперь диск можно снять.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-130">The disk drive can now be removed.</span></span>

<span data-ttu-id="4ed0c-131">Для закрытия защелки выполните эти действия в обратном порядке.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-131">Follow the steps in reverse to engage the lock.</span></span>

## <a name="remove-the-disk-drive"></a><span data-ttu-id="4ed0c-132">снять жесткий диск;</span><span class="sxs-lookup"><span data-stu-id="4ed0c-132">Remove the disk drive</span></span>
<span data-ttu-id="4ed0c-133">Устройство StorSimple поддерживает конфигурацию хранилища, напоминающую RAID 10.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="4ed0c-134">Это означает, что устройство продолжит нормальную работу после выхода из строя одного диска, твердотельного накопителя (SSD) или жесткого диска (HDD).</span><span class="sxs-lookup"><span data-stu-id="4ed0c-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="4ed0c-135">Если в системе несколько неисправных дисков, не снимайте более одного SSD или HDD в один момент времени.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span></span> <span data-ttu-id="4ed0c-136">Это может привести к потере данных.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="4ed0c-137">Убедитесь, что новый SSD устанавливается в слот, в котором ранее находился SSD.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="4ed0c-138">Аналогично, новый HDD должен устанавливаться в слот, в котором ранее находился HDD.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="4ed0c-139">В классическом портале Azure слоты нумеруются от 0 до 11.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-139">In the Azure classic portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="4ed0c-140">Таким образом, если на портале управления отображается, что произошел сбой диска в слоте 2 на устройстве, то неисправным будет третий по счету диск от левого верхнего.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span></span>
> 
> 

<span data-ttu-id="4ed0c-141">Диски можно будет снимать и заменять во время работы системы.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-141">Drives can be removed and replaced while the system is operating.</span></span>

#### <a name="to-remove-a-drive"></a><span data-ttu-id="4ed0c-142">Для снятия диска</span><span class="sxs-lookup"><span data-stu-id="4ed0c-142">To remove a drive</span></span>
1. <span data-ttu-id="4ed0c-143">Для определения неисправного диска на классическом портале Azure выберите **Устройства** > **Обслуживание** > **Состояние оборудования**.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-143">To identify the failed disk, in the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="4ed0c-144">Поскольку неисправный диск может находиться в основном корпусе и/или корпусе EBOD (при использовании модели 8600), просмотрите состояние дисков в разделах **Общие компоненты** и **Общие компоненты EBOD**.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span></span> <span data-ttu-id="4ed0c-145">Неисправный диск в любом корпусе будет отмечен красным цветом.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="4ed0c-146">Найдите диски в передней части основного корпуса или корпуса EBOD.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span></span> 
3. <span data-ttu-id="4ed0c-147">Если защитная защелка диска открыта, перейдите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-147">If the disk is unlocked, proceed to the next step.</span></span> <span data-ttu-id="4ed0c-148">Если защитная защелка закрыта, откройте ее, выполнив процедуру, описанную в разделе [Открывание защитной защелки](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="4ed0c-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="4ed0c-149">Нажмите на черную защелку на дисковом модуле и откройте рукоятку диска на передней панели.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span></span> 
   
    ![Открытие рукоятки диска](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="4ed0c-151">**Рис. 3.** Открытие рукоятки диска</span><span class="sxs-lookup"><span data-stu-id="4ed0c-151">**Figure 3** Releasing the drive handle</span></span>
5. <span data-ttu-id="4ed0c-152">Полностью открыв рукоятку диска, извлеките дисковый модуль из корпуса.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span></span> 
   
    ![Извлечение диска](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="4ed0c-154">**Рис. 4.** Извлечение диска из корпуса</span><span class="sxs-lookup"><span data-stu-id="4ed0c-154">**Figure 4** Sliding the disk drive out of the carrier</span></span>

## <a name="install-the-replacement-disk-drive"></a><span data-ttu-id="4ed0c-155">установить новый жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-155">Install the replacement disk drive</span></span>
<span data-ttu-id="4ed0c-156">После снятия неисправного жесткого диска на устройстве StorSimple выполните эту процедуру для установки нового диска.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span></span>

#### <a name="to-insert-a-drive"></a><span data-ttu-id="4ed0c-157">Для установки диска</span><span class="sxs-lookup"><span data-stu-id="4ed0c-157">To insert a drive</span></span>
1. <span data-ttu-id="4ed0c-158">Убедитесь, что рукоятка дискового модуля полностью открыта, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span></span>
   
    ![Диск с открытой рукояткой](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="4ed0c-160">**Рис. 5.** Диск с открытой рукояткой</span><span class="sxs-lookup"><span data-stu-id="4ed0c-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="4ed0c-161">Полностью установите диск в корпус.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-161">Slide the drive carrier all the way into the chassis.</span></span> 
   
    ![Установка диска в дисковый модуль](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="4ed0c-163">**Рис. 6.** Установка дискового модуля в корпус</span><span class="sxs-lookup"><span data-stu-id="4ed0c-163">**Figure 6**  Sliding the drive carrier into the chassis</span></span>
3. <span data-ttu-id="4ed0c-164">Установив дисковый модуль, закройте рукоятку дискового модуля, продолжая надавливать на диск до тех пор, пока рукоятка не перейдет в закрытое положение.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="4ed0c-165">Для закрепления ручки используйте ключ ("антивандальную" отвертку Torx, предоставляемую Майкрософт), повернув защитный винт на четверть оборота по часовой стрелке.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="4ed0c-166">Убедитесь, что замена выполнена успешно и диск работает, зайдя на классический портал Azure и выбрав **Обслуживание** > **Состояние оборудования**.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-166">Verify that the replacement was successful and the drive is operational by accessing the Azure classic portal and navigating to **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="4ed0c-167">В разделах **Общие компоненты** или **Общие компоненты EBOD** состояние диска должно быть зеленым, что указывает на его работоспособность.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-167">Under **Shared Components** or **EBOD enclosure Shared Components**, the drive status should be green, indicating that it is healthy.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4ed0c-168">После замены диска на изменение состояния диска в портале управления может потребоваться несколько часов.</span><span class="sxs-lookup"><span data-stu-id="4ed0c-168">It may take several hours for the disk status to turn green after the replacement.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="4ed0c-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4ed0c-169">Next steps</span></span>
<span data-ttu-id="4ed0c-170">Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="4ed0c-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

