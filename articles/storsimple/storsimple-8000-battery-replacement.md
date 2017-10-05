---
title: "Замена аккумулятора на устройстве Microsoft Azure StorSimple серии 8000 | Документация Майкрософт"
description: "Описывает процедуры снятия, замены и обслуживания модуля резервного аккумулятора на устройстве StorSimple."
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
ms.openlocfilehash: 174a3163082594ea6a49b7f5a78857848f8f0566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="02b35-103">Замена резервного аккумулятора на устройстве StorSimple</span><span class="sxs-lookup"><span data-stu-id="02b35-103">Replace the backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="02b35-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="02b35-104">Overview</span></span>
<span data-ttu-id="02b35-105">Блок питания и охлаждения (БПО) устройства Microsoft Azure StorSimple имеет резервный аккумулятор.</span><span class="sxs-lookup"><span data-stu-id="02b35-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="02b35-106">Он позволит сохранить данные устройства StorSimple при исчезновении питания основного корпуса.</span><span class="sxs-lookup"><span data-stu-id="02b35-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="02b35-107">Резервный аккумулятор здесь называется *модулем резервного аккумулятора*.</span><span class="sxs-lookup"><span data-stu-id="02b35-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="02b35-108">Модуль резервного аккумулятора используется только для основного корпуса устройства StorSimple (для корпуса EBOD модуль резервного аккумулятора не используется).</span><span class="sxs-lookup"><span data-stu-id="02b35-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="02b35-109">В этом учебнике объясняется, как выполнить такие задачи:</span><span class="sxs-lookup"><span data-stu-id="02b35-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="02b35-110">Снятие модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="02b35-110">Remove the backup battery module</span></span>
* <span data-ttu-id="02b35-111">Установка нового модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="02b35-111">Install a new backup battery module</span></span>
* <span data-ttu-id="02b35-112">Обслуживание модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="02b35-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02b35-113">Перед извлечением и заменой модуля резервного аккумулятора ознакомьтесь с мерами предосторожности в разделе [Общие сведения о замене компонентов оборудования StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="02b35-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="02b35-114">Снятие модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="02b35-114">Remove the backup battery module</span></span>
<span data-ttu-id="02b35-115">Модуль резервного аккумулятора устройства StorSimple является модулем, заменяемым в полевых условиях.</span><span class="sxs-lookup"><span data-stu-id="02b35-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="02b35-116">Перед установкой в БПО модуль резервного аккумулятора должен храниться в оригинальной упаковке.</span><span class="sxs-lookup"><span data-stu-id="02b35-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="02b35-117">Чтобы извлечь резервный аккумулятор, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="02b35-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="02b35-118">Для снятия модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="02b35-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="02b35-119">На портале Azure перейдите на колонку службы диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="02b35-119">In the Azure portal, go to your StorSimple Device Manager service blade.</span></span> <span data-ttu-id="02b35-120">Откройте раздел **Устройства** и выберите свое устройство из списка.</span><span class="sxs-lookup"><span data-stu-id="02b35-120">Go to **Devices** and then select your device from the list of devices.</span></span> <span data-ttu-id="02b35-121">Откройте элементы **Отслеживание** > **Работоспособность оборудования**.</span><span class="sxs-lookup"><span data-stu-id="02b35-121">Navigate to **Monitor** > **Hardware health**.</span></span> <span data-ttu-id="02b35-122">В разделе **Общие компоненты**взгляните на состояние батареи.</span><span class="sxs-lookup"><span data-stu-id="02b35-122">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="02b35-123">Определите БПО, в котором произошел сбой батареи.</span><span class="sxs-lookup"><span data-stu-id="02b35-123">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="02b35-124">На рис. 1 показана задняя поверхность устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="02b35-124">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![Задняя панель модулей основного корпуса устройства](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="02b35-126">**Рис. 1.** Задняя поверхность основного устройства с БПО и модулями контроллера</span><span class="sxs-lookup"><span data-stu-id="02b35-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="02b35-127">Метка</span><span class="sxs-lookup"><span data-stu-id="02b35-127">Label</span></span> | <span data-ttu-id="02b35-128">Описание</span><span class="sxs-lookup"><span data-stu-id="02b35-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="02b35-129">1</span><span class="sxs-lookup"><span data-stu-id="02b35-129">1</span></span> |<span data-ttu-id="02b35-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="02b35-130">PCM 0</span></span> |
   | <span data-ttu-id="02b35-131">2</span><span class="sxs-lookup"><span data-stu-id="02b35-131">2</span></span> |<span data-ttu-id="02b35-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="02b35-132">PCM 1</span></span> |
   | <span data-ttu-id="02b35-133">3</span><span class="sxs-lookup"><span data-stu-id="02b35-133">3</span></span> |<span data-ttu-id="02b35-134">Контроллер 0</span><span class="sxs-lookup"><span data-stu-id="02b35-134">Controller 0</span></span> |
   | <span data-ttu-id="02b35-135">4.</span><span class="sxs-lookup"><span data-stu-id="02b35-135">4</span></span> |<span data-ttu-id="02b35-136">Контроллер 1</span><span class="sxs-lookup"><span data-stu-id="02b35-136">Controller 1</span></span> |
   
    <span data-ttu-id="02b35-137">Как показывает число 3 на рис. 2, должен гореть индикатор для БПО 0, который соответствует **Неисправности батареи**.</span><span class="sxs-lookup"><span data-stu-id="02b35-137">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![Светодиодные индикаторы мониторинга на задней панели БПО устройства](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="02b35-139">**Рис. 2.** Задняя поверхность БПО с индикаторами</span><span class="sxs-lookup"><span data-stu-id="02b35-139">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="02b35-140">Метка</span><span class="sxs-lookup"><span data-stu-id="02b35-140">Label</span></span> | <span data-ttu-id="02b35-141">Описание</span><span class="sxs-lookup"><span data-stu-id="02b35-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="02b35-142">1</span><span class="sxs-lookup"><span data-stu-id="02b35-142">1</span></span> |<span data-ttu-id="02b35-143">Сбой питания от электросети</span><span class="sxs-lookup"><span data-stu-id="02b35-143">AC power failure</span></span> |
   | <span data-ttu-id="02b35-144">2</span><span class="sxs-lookup"><span data-stu-id="02b35-144">2</span></span> |<span data-ttu-id="02b35-145">Сбой вентилятора</span><span class="sxs-lookup"><span data-stu-id="02b35-145">Fan failure</span></span> |
   | <span data-ttu-id="02b35-146">3</span><span class="sxs-lookup"><span data-stu-id="02b35-146">3</span></span> |<span data-ttu-id="02b35-147">Сбой аккумулятора</span><span class="sxs-lookup"><span data-stu-id="02b35-147">Battery fault</span></span> |
   | <span data-ttu-id="02b35-148">4.</span><span class="sxs-lookup"><span data-stu-id="02b35-148">4</span></span> |<span data-ttu-id="02b35-149">БПО исправен</span><span class="sxs-lookup"><span data-stu-id="02b35-149">PCM OK</span></span> |
   | <span data-ttu-id="02b35-150">5</span><span class="sxs-lookup"><span data-stu-id="02b35-150">5</span></span> |<span data-ttu-id="02b35-151">Сбой постоянного напряжения</span><span class="sxs-lookup"><span data-stu-id="02b35-151">DC power failure</span></span> |
   | <span data-ttu-id="02b35-152">6</span><span class="sxs-lookup"><span data-stu-id="02b35-152">6</span></span> |<span data-ttu-id="02b35-153">Батарея работоспособна</span><span class="sxs-lookup"><span data-stu-id="02b35-153">Battery healthy</span></span> |
3. <span data-ttu-id="02b35-154">Для снятия БПО с неисправной батареей выполните действия, описанные в разделе [Снятие БПО](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="02b35-154">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="02b35-155">Сняв БПО, поднимите и поверните рукоятку модуля аккумулятора вверх, как показано на следующем рисунке, и потяните за нее для снятия модуля аккумулятора.</span><span class="sxs-lookup"><span data-stu-id="02b35-155">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![Снятие батареи БПО](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="02b35-157">**Рис. 3.** Извлечение аккумуляторной батареи из БПО</span><span class="sxs-lookup"><span data-stu-id="02b35-157">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="02b35-158">Поместите модуль в упаковку модуля, заменяемого в полевых условиях.</span><span class="sxs-lookup"><span data-stu-id="02b35-158">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="02b35-159">Верните неисправный блок Microsoft для соответствующего обслуживания.</span><span class="sxs-lookup"><span data-stu-id="02b35-159">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="02b35-160">Установка нового модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="02b35-160">Install a new backup battery module</span></span>
<span data-ttu-id="02b35-161">Чтобы установить новый модуль аккумулятора в БПО в основном корпусе устройства StorSimple, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="02b35-161">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="02b35-162">Для установки модуля аккумулятора</span><span class="sxs-lookup"><span data-stu-id="02b35-162">To install the battery module</span></span>
1. <span data-ttu-id="02b35-163">Установите модуль резервного аккумулятора в БПО в правильном положении.</span><span class="sxs-lookup"><span data-stu-id="02b35-163">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="02b35-164">Нажимайте на модуль аккумулятора до упора, чтобы он вошел в разъем.</span><span class="sxs-lookup"><span data-stu-id="02b35-164">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="02b35-165">Замените БПО в основном корпусе в соответствии с инструкциями в разделе [Замена блока питания и охлаждения для устройства StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="02b35-165">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="02b35-166">После замены перейдите на страницу устройства на портале Azure и откройте разделы **Отслеживание** > **Работоспособность оборудования**.</span><span class="sxs-lookup"><span data-stu-id="02b35-166">After the replacement is complete, go to your device and then go to **Monitor** > **Hardware health** in the Azure portal.</span></span> <span data-ttu-id="02b35-167">Проверьте состояние аккумулятора, чтобы убедиться в том, что установка прошла успешно.</span><span class="sxs-lookup"><span data-stu-id="02b35-167">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="02b35-168">Зеленый индикатор указывает на то, что аккумулятор исправен.</span><span class="sxs-lookup"><span data-stu-id="02b35-168">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="02b35-169">Обслуживание модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="02b35-169">Maintain the backup battery module</span></span>
<span data-ttu-id="02b35-170">Модуль резервного аккумулятора в устройстве StorSimple предоставляет аварийное питание для контроллера при исчезновении сетевого напряжения.</span><span class="sxs-lookup"><span data-stu-id="02b35-170">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="02b35-171">Это позволяет устройству StorSimple сохранить важные данные до завершения работы контролируемым образом.</span><span class="sxs-lookup"><span data-stu-id="02b35-171">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="02b35-172">С двумя полностью заряженными аккумуляторами в БПО система может выдержать два последовательных отключения питания.</span><span class="sxs-lookup"><span data-stu-id="02b35-172">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="02b35-173">На портале Azure в разделе **Работоспособность оборудования** в колонке **Отслеживание** отображается информация о неисправности аккумулятора и об окончании срока службы аккумуляторной батареи.</span><span class="sxs-lookup"><span data-stu-id="02b35-173">In the Azure portal, the **Hardware health** under the **Monitor** blade indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="02b35-174">Состояние аккумуляторов отображается в разделах **Батарея в PCM 0** и **Батарея в PCM 1** в разделе **Общие компоненты**.</span><span class="sxs-lookup"><span data-stu-id="02b35-174">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="02b35-175">В этой колонке отображается состояние **ОГРАНИЧЕНО** при приближении окончания срока службы и **НЕИСПРАВНО** при окончании срока службы.</span><span class="sxs-lookup"><span data-stu-id="02b35-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="02b35-176">Состояние аккумулятора может измениться на **НЕИСПРАВЕН** при необходимости его зарядки.</span><span class="sxs-lookup"><span data-stu-id="02b35-176">The battery can report **FAILED** when it simply needs to be charged.</span></span>


<span data-ttu-id="02b35-177">При появлении состояния **ОГРАНИЧЕН** рекомендуется следующий порядок действий:</span><span class="sxs-lookup"><span data-stu-id="02b35-177">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="02b35-178">Система могла недавно подвергнуться отключению питания или аккумуляторы могут подвергаться периодическому обслуживанию.</span><span class="sxs-lookup"><span data-stu-id="02b35-178">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="02b35-179">Перед выполнением дальнейших действий наблюдайте за состоянием системы в течение 12 часов.</span><span class="sxs-lookup"><span data-stu-id="02b35-179">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="02b35-180">Если по истечении 12 часов подключения к сети питания с работающими контроллерами и БПО аккумулятор по-прежнему находится в состоянии **ОГРАНИЧЕН** , этот аккумулятор необходимо заменить.</span><span class="sxs-lookup"><span data-stu-id="02b35-180">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="02b35-181">Для получения нового модуля резервного аккумулятора [обратитесь в службу поддержки Microsoft](storsimple-8000-contact-microsoft-support.md) .</span><span class="sxs-lookup"><span data-stu-id="02b35-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="02b35-182">Если за 12 часов состояние аккумулятора изменилось на исправное, аккумулятор работает нормально, и ему требуется только обслуживание.</span><span class="sxs-lookup"><span data-stu-id="02b35-182">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="02b35-183">Если соответствующего отключения сетевого напряжения не было, БПО включен и подключен к сети, аккумулятор необходимо заменить.</span><span class="sxs-lookup"><span data-stu-id="02b35-183">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="02b35-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) .</span><span class="sxs-lookup"><span data-stu-id="02b35-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02b35-185">Утилизируйте неисправную батарею в соответствии с федеральным и региональным законодательством.</span><span class="sxs-lookup"><span data-stu-id="02b35-185">Dispose of the failed battery according to national and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02b35-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02b35-186">Next steps</span></span>
<span data-ttu-id="02b35-187">Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="02b35-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

