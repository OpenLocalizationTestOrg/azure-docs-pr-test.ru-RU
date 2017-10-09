---
title: "дисковый накопитель на устройства серии StorSimple 8000 aaaReplace | Документы Microsoft"
description: "Объясняет, как диск tooreplace диск на StorSimple основного корпуса или корпуса EBOD."
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
ms.date: 073/2017
ms.author: alkohli
ms.openlocfilehash: 09c1bf5e97adf54a609a868e921351bc63e00a83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a><span data-ttu-id="89397-103">Замена диска на устройстве StorSimple серии 8000</span><span class="sxs-lookup"><span data-stu-id="89397-103">Replace a disk drive on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="89397-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="89397-104">Overview</span></span>
<span data-ttu-id="89397-105">В этом учебнике объясняется, как снять и заменить неисправный или вышедший из строя жесткий диск на устройстве Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="89397-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="89397-106">tooreplace дисковый накопитель, необходимо:</span><span class="sxs-lookup"><span data-stu-id="89397-106">tooreplace a disk drive, you need to:</span></span>

* <span data-ttu-id="89397-107">Отключите hello противовзломного замка</span><span class="sxs-lookup"><span data-stu-id="89397-107">Disengage hello antitamper lock</span></span>
* <span data-ttu-id="89397-108">Удалить диск hello</span><span class="sxs-lookup"><span data-stu-id="89397-108">Remove hello disk drive</span></span>
* <span data-ttu-id="89397-109">Установка hello замены диска.</span><span class="sxs-lookup"><span data-stu-id="89397-109">Install hello replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89397-110">До удаления и замены дисковый накопитель, просмотрите сведения о безопасности hello в [замена компонентов оборудования StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="89397-110">Before removing and replacing a disk drive, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
 

## <a name="disengage-hello-antitamper-lock"></a><span data-ttu-id="89397-111">Отключите hello противовзломного замка</span><span class="sxs-lookup"><span data-stu-id="89397-111">Disengage hello antitamper lock</span></span>
<span data-ttu-id="89397-112">Эта процедура объясняет, как hello противовзломный блокировки на устройстве StorSimple можно активировать или деактивировать при замене hello жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="89397-112">This procedure explains how hello antitamper locks on your StorSimple device can be engaged or disengaged when you replace hello disk drives.</span></span> <span data-ttu-id="89397-113">установленным Hello противовзломный блокировок в обработчиках перевозчика диска hello и они доступны через небольшое отверстие в разделе hello кратковременной блокировки дескриптора hello.</span><span class="sxs-lookup"><span data-stu-id="89397-113">hello antitamper locks are fitted in hello drive carrier handles, and they are accessed through a small aperture in hello latch section of hello handle.</span></span> <span data-ttu-id="89397-114">Накопители поставляются с позицией заблокирован toohello набора блокировок hello.</span><span class="sxs-lookup"><span data-stu-id="89397-114">Drives are supplied with hello locks set toohello locked position.</span></span>

#### <a name="toounlock-hello-antitamper-lock"></a><span data-ttu-id="89397-115">противовзломный замок toounlock hello</span><span class="sxs-lookup"><span data-stu-id="89397-115">toounlock hello antitamper lock</span></span>
1. <span data-ttu-id="89397-116">Аккуратно вставьте фиксирующий ключ hello («устойчивую к внешним воздействиям» T10 отвертку, предоставленную Майкрософт) в отверстие hello дескриптор hello и в ее гнездо.</span><span class="sxs-lookup"><span data-stu-id="89397-116">Carefully insert hello lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into hello aperture in hello handle and into its socket.</span></span> 
   
   <span data-ttu-id="89397-117">Если hello противовзломный замок активирован, является видимым в отверстии hello hello красный индикатор.</span><span class="sxs-lookup"><span data-stu-id="89397-117">If hello antitamper lock is activated, hello red indicator is visible in hello aperture.</span></span>
  
    ![Диск с закрытой защитной защелкой](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="89397-119">**Рис. 1.** Защитная защелка закрыта</span><span class="sxs-lookup"><span data-stu-id="89397-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="89397-120">Метка</span><span class="sxs-lookup"><span data-stu-id="89397-120">Label</span></span> | <span data-ttu-id="89397-121">Описание</span><span class="sxs-lookup"><span data-stu-id="89397-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="89397-122">1</span><span class="sxs-lookup"><span data-stu-id="89397-122">1</span></span> |<span data-ttu-id="89397-123">Щель индикатора</span><span class="sxs-lookup"><span data-stu-id="89397-123">Indicator aperture</span></span> |
   | <span data-ttu-id="89397-124">2</span><span class="sxs-lookup"><span data-stu-id="89397-124">2</span></span> |<span data-ttu-id="89397-125">Защитная защелка</span><span class="sxs-lookup"><span data-stu-id="89397-125">Antitamper lock</span></span> |
2. <span data-ttu-id="89397-126">Менять ключ hello против часовой стрелки, пока не отображается в hello отверстии над ключом hello hello красный индикатор.</span><span class="sxs-lookup"><span data-stu-id="89397-126">Rotate hello key in an anticlockwise direction until hello red indicator is not visible in hello aperture above hello key.</span></span>
3. <span data-ttu-id="89397-127">Удалите раздел hello.</span><span class="sxs-lookup"><span data-stu-id="89397-127">Remove hello key.</span></span>
   
    ![Защитная защелка открыта](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="89397-129">**Рис. 2.** Защитная защелка открыта</span><span class="sxs-lookup"><span data-stu-id="89397-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="89397-130">Теперь можно удалить диск Hello.</span><span class="sxs-lookup"><span data-stu-id="89397-130">hello disk drive can now be removed.</span></span>

<span data-ttu-id="89397-131">Следуйте указаниям hello обратного tooengage hello блокировки.</span><span class="sxs-lookup"><span data-stu-id="89397-131">Follow hello steps in reverse tooengage hello lock.</span></span>

## <a name="remove-hello-disk-drive"></a><span data-ttu-id="89397-132">Удалить диск hello</span><span class="sxs-lookup"><span data-stu-id="89397-132">Remove hello disk drive</span></span>
<span data-ttu-id="89397-133">Устройство StorSimple поддерживает конфигурацию хранилища, напоминающую RAID 10.</span><span class="sxs-lookup"><span data-stu-id="89397-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="89397-134">Это означает, что устройство продолжит нормальную работу после выхода из строя одного диска, твердотельного накопителя (SSD) или жесткого диска (HDD).</span><span class="sxs-lookup"><span data-stu-id="89397-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="89397-135">Если система содержит более одного отказавшего диска, не удаляйте больше одного накопителя SSD или HDD из системы hello в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="89397-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from hello system at any point in time.</span></span> <span data-ttu-id="89397-136">Это может привести к потере данных.</span><span class="sxs-lookup"><span data-stu-id="89397-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="89397-137">Убедитесь, что новый SSD устанавливается в слот, в котором ранее находился SSD.</span><span class="sxs-lookup"><span data-stu-id="89397-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="89397-138">Аналогично, новый HDD должен устанавливаться в слот, в котором ранее находился HDD.</span><span class="sxs-lookup"><span data-stu-id="89397-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="89397-139">В hello портал Azure, слоты нумеруются от 0 до 11.</span><span class="sxs-lookup"><span data-stu-id="89397-139">In hello Azure portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="89397-140">Таким образом Если портал hello показывает произошел сбой на диск в слоте 2, на устройстве hello искать hello отказавший диск в третьем слоте hello hello верхнего левого угла.</span><span class="sxs-lookup"><span data-stu-id="89397-140">Therefore, if hello portal shows that a disk in slot 2 has failed, on hello device, look for hello failed disk in hello third slot from hello top left.</span></span>
> 
> 

<span data-ttu-id="89397-141">Диски, можно удалить и заменить при питании hello.</span><span class="sxs-lookup"><span data-stu-id="89397-141">Drives can be removed and replaced while hello system is operating.</span></span>

#### <a name="tooremove-a-drive"></a><span data-ttu-id="89397-142">tooremove диск</span><span class="sxs-lookup"><span data-stu-id="89397-142">tooremove a drive</span></span>
1. <span data-ttu-id="89397-143">tooidentify hello сбой диска в hello портал Azure, на устройстве перейдите tooyour **параметры > работоспособности оборудования**.</span><span class="sxs-lookup"><span data-stu-id="89397-143">tooidentify hello failed disk, in hello Azure portal, go tooyour device **Settings > Hardware health**.</span></span> <span data-ttu-id="89397-144">Так как диск может произойти сбой в основном корпусе hello и/или в корпусе EBOD (Если вы используете модели 8600), просмотрите состояние hello hello дисков в группе **общих компонентов** и в разделе **общие компоненты EBOD** .</span><span class="sxs-lookup"><span data-stu-id="89397-144">Because a disk can fail in hello primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at hello status of hello disks under **Shared components** and under **EBOD shared components**.</span></span> <span data-ttu-id="89397-145">Неисправный диск в любом корпусе будет отмечен красным цветом.</span><span class="sxs-lookup"><span data-stu-id="89397-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="89397-146">Найдите диски hello в начало hello hello основного корпуса или корпуса EBOD hello.</span><span class="sxs-lookup"><span data-stu-id="89397-146">Locate hello drives in hello front of hello primary enclosure or hello EBOD enclosure.</span></span> 
3. <span data-ttu-id="89397-147">Если диск hello разблокирован, перейдите toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="89397-147">If hello disk is unlocked, proceed toohello next step.</span></span> <span data-ttu-id="89397-148">Если hello диск заблокирован, разблокируйте его путем процедуры hello в [отключите противовзломный замок hello](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="89397-148">If hello disk is locked, unlock it by following hello procedure in [Disengage hello antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="89397-149">Нажмите клавишу hello кратковременных блокировок на hello дискового модуля черно -удалите hello Ручка out и из hello в передней части корпуса hello.</span><span class="sxs-lookup"><span data-stu-id="89397-149">Press hello black latch on hello drive carrier module and pull hello drive carrier handle out and away from hello front of hello chassis.</span></span>
   
    ![Открытие рукоятки диска](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="89397-151">**Рис. 3** освобождении hello ручки.</span><span class="sxs-lookup"><span data-stu-id="89397-151">**Figure 3** Releasing hello drive handle</span></span>
5. <span data-ttu-id="89397-152">При расширении hello Ручка полностью слайд hello дисковый модуль из шасси hello.</span><span class="sxs-lookup"><span data-stu-id="89397-152">When hello drive carrier handle is fully extended, slide hello drive carrier out of hello chassis.</span></span> 
   
    ![Извлечение диска](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="89397-154">**Рис. 4** скользящий hello дисковый накопитель из оператора hello</span><span class="sxs-lookup"><span data-stu-id="89397-154">**Figure 4** Sliding hello disk drive out of hello carrier</span></span>

## <a name="install-hello-replacement-disk-drive"></a><span data-ttu-id="89397-155">Установка hello замены диска.</span><span class="sxs-lookup"><span data-stu-id="89397-155">Install hello replacement disk drive</span></span>
<span data-ttu-id="89397-156">Удалено на сбой диска в вашем устройстве StorSimple, выполните этот tooreplace процедуры с помощью нового диска.</span><span class="sxs-lookup"><span data-stu-id="89397-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure tooreplace it with a new drive.</span></span>

#### <a name="tooinsert-a-drive"></a><span data-ttu-id="89397-157">tooinsert диск</span><span class="sxs-lookup"><span data-stu-id="89397-157">tooinsert a drive</span></span>
1. <span data-ttu-id="89397-158">Убедитесь, что hello Ручка дискового модуля полностью выдвинута, как показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="89397-158">Ensure hello drive carrier handle is fully extended, as shown in hello following image.</span></span>
   
    ![Диск с открытой рукояткой](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="89397-160">**Рис. 5.** Диск с открытой рукояткой</span><span class="sxs-lookup"><span data-stu-id="89397-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="89397-161">Слайд hello дисковый модуль все способом hello в корпус hello.</span><span class="sxs-lookup"><span data-stu-id="89397-161">Slide hello drive carrier all hello way into hello chassis.</span></span>
   
    ![Установка диска в дисковый модуль](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="89397-163">**Рис. 6** скользящий hello дисковый модуль в корпус hello</span><span class="sxs-lookup"><span data-stu-id="89397-163">**Figure 6**  Sliding hello drive carrier into hello chassis</span></span>
3. <span data-ttu-id="89397-164">С hello диска оператора inserted, закройте hello Ручка при продолжение toopush hello дисковый модуль в корпус hello, пока hello Ручка привязывается к зафиксирован.</span><span class="sxs-lookup"><span data-stu-id="89397-164">With hello drive carrier inserted, close hello drive carrier handle while continuing toopush hello drive carrier into hello chassis, until hello drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="89397-165">Использовать ключ блокировку hello, предоставленным Майкрософт (устойчивую к внешним воздействиям отвертку жалом звездообразной формы) toosecure hello перевозчика дескриптор в месте, отключив hello Фиксирующий винт на четверть оборота по часовой стрелке.</span><span class="sxs-lookup"><span data-stu-id="89397-165">Use hello lock key that was provided by Microsoft (tamperproof Torx screwdriver) toosecure hello carrier handle into place by turning hello lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="89397-166">Убедитесь, что hello замена выполнена успешно, и hello диск находится в рабочем состоянии.</span><span class="sxs-lookup"><span data-stu-id="89397-166">Verify that hello replacement was successful and hello drive is operational.</span></span> <span data-ttu-id="89397-167">Доступ к hello портал Azure и перейдите слишком**параметры** > **работоспособности оборудования**.</span><span class="sxs-lookup"><span data-stu-id="89397-167">Access hello Azure portal and navigate too**Settings** > **Hardware health**.</span></span> <span data-ttu-id="89397-168">В разделе **общих компонентов** или **общие компоненты EBOD**, состояние диска hello должно быть зеленый, указывающее, что он исправен.</span><span class="sxs-lookup"><span data-stu-id="89397-168">Under **Shared components** or **EBOD shared components**, hello drive status should be green, indicating that it is healthy.</span></span>
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > <span data-ttu-id="89397-169">Он может занять несколько часов для tooturn состояние диска hello зеленый после замены hello.</span><span class="sxs-lookup"><span data-stu-id="89397-169">It may take several hours for hello disk status tooturn green after hello replacement.</span></span>
  
## <a name="next-steps"></a><span data-ttu-id="89397-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89397-170">Next steps</span></span>
<span data-ttu-id="89397-171">Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="89397-171">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

