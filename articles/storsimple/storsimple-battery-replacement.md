---
title: "Замена аккумулятора на устройстве Microsoft Azure StorSimple | Документация Майкрософт"
description: "Описывает процедуры снятия, замены и обслуживания модуля резервного аккумулятора на устройстве StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8b89b3f6851ec9ee0570f551b5407419fdba2d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="177e1-103">Замена резервного аккумулятора на устройстве StorSimple</span><span class="sxs-lookup"><span data-stu-id="177e1-103">Replace the backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="177e1-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="177e1-104">Overview</span></span>
<span data-ttu-id="177e1-105">Блок питания и охлаждения (БПО) устройства Microsoft Azure StorSimple имеет резервный аккумулятор.</span><span class="sxs-lookup"><span data-stu-id="177e1-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="177e1-106">Он позволит сохранить данные устройства StorSimple при исчезновении питания основного корпуса.</span><span class="sxs-lookup"><span data-stu-id="177e1-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="177e1-107">Резервный аккумулятор здесь называется *модулем резервного аккумулятора*.</span><span class="sxs-lookup"><span data-stu-id="177e1-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="177e1-108">Модуль резервного аккумулятора используется только для основного корпуса устройства StorSimple (для корпуса EBOD модуль резервного аккумулятора не используется).</span><span class="sxs-lookup"><span data-stu-id="177e1-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="177e1-109">В этом учебнике объясняется, как выполнить такие задачи:</span><span class="sxs-lookup"><span data-stu-id="177e1-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="177e1-110">Снятие модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="177e1-110">Remove the backup battery module</span></span> 
* <span data-ttu-id="177e1-111">Установка нового модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="177e1-111">Install a new backup battery module</span></span>
* <span data-ttu-id="177e1-112">Обслуживание модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="177e1-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="177e1-113">Перед извлечением и заменой модуля резервного аккумулятора ознакомьтесь с мерами предосторожности в разделе [Общие сведения о замене компонентов оборудования StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="177e1-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="177e1-114">Снятие модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="177e1-114">Remove the backup battery module</span></span>
<span data-ttu-id="177e1-115">Модуль резервного аккумулятора устройства StorSimple является модулем, заменяемым в полевых условиях.</span><span class="sxs-lookup"><span data-stu-id="177e1-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="177e1-116">Перед установкой в БПО модуль резервного аккумулятора должен храниться в оригинальной упаковке.</span><span class="sxs-lookup"><span data-stu-id="177e1-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="177e1-117">Чтобы извлечь резервный аккумулятор, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="177e1-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="177e1-118">Для снятия модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="177e1-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="177e1-119">На классическом портале Azure выберите **Устройства** > **Обслуживание** > **Состояние оборудования**.</span><span class="sxs-lookup"><span data-stu-id="177e1-119">In the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="177e1-120">В разделе **Общие компоненты**взгляните на состояние батареи.</span><span class="sxs-lookup"><span data-stu-id="177e1-120">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="177e1-121">Определите БПО, в котором произошел сбой батареи.</span><span class="sxs-lookup"><span data-stu-id="177e1-121">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="177e1-122">На рис. 1 показана задняя поверхность устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="177e1-122">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![Задняя панель модулей основного корпуса устройства](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="177e1-124">**Рис. 1.** Задняя поверхность основного устройства с БПО и модулями контроллера</span><span class="sxs-lookup"><span data-stu-id="177e1-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="177e1-125">Метка</span><span class="sxs-lookup"><span data-stu-id="177e1-125">Label</span></span> | <span data-ttu-id="177e1-126">Описание</span><span class="sxs-lookup"><span data-stu-id="177e1-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="177e1-127">1</span><span class="sxs-lookup"><span data-stu-id="177e1-127">1</span></span> |<span data-ttu-id="177e1-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="177e1-128">PCM 0</span></span> |
   | <span data-ttu-id="177e1-129">2</span><span class="sxs-lookup"><span data-stu-id="177e1-129">2</span></span> |<span data-ttu-id="177e1-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="177e1-130">PCM 1</span></span> |
   | <span data-ttu-id="177e1-131">3</span><span class="sxs-lookup"><span data-stu-id="177e1-131">3</span></span> |<span data-ttu-id="177e1-132">Контроллер 0</span><span class="sxs-lookup"><span data-stu-id="177e1-132">Controller 0</span></span> |
   | <span data-ttu-id="177e1-133">4.</span><span class="sxs-lookup"><span data-stu-id="177e1-133">4</span></span> |<span data-ttu-id="177e1-134">Контроллер 1</span><span class="sxs-lookup"><span data-stu-id="177e1-134">Controller 1</span></span> |
   
    <span data-ttu-id="177e1-135">Как показывает число 3 на рис. 2, должен гореть индикатор для БПО 0, который соответствует **Неисправности батареи**.</span><span class="sxs-lookup"><span data-stu-id="177e1-135">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![Светодиодные индикаторы мониторинга на задней панели БПО устройства](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="177e1-137">**Рис. 2.** Задняя поверхность БПО с индикаторами</span><span class="sxs-lookup"><span data-stu-id="177e1-137">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="177e1-138">Метка</span><span class="sxs-lookup"><span data-stu-id="177e1-138">Label</span></span> | <span data-ttu-id="177e1-139">Описание</span><span class="sxs-lookup"><span data-stu-id="177e1-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="177e1-140">1</span><span class="sxs-lookup"><span data-stu-id="177e1-140">1</span></span> |<span data-ttu-id="177e1-141">Сбой питания от электросети</span><span class="sxs-lookup"><span data-stu-id="177e1-141">AC power failure</span></span> |
   | <span data-ttu-id="177e1-142">2</span><span class="sxs-lookup"><span data-stu-id="177e1-142">2</span></span> |<span data-ttu-id="177e1-143">Сбой вентилятора</span><span class="sxs-lookup"><span data-stu-id="177e1-143">Fan failure</span></span> |
   | <span data-ttu-id="177e1-144">3</span><span class="sxs-lookup"><span data-stu-id="177e1-144">3</span></span> |<span data-ttu-id="177e1-145">Сбой аккумулятора</span><span class="sxs-lookup"><span data-stu-id="177e1-145">Battery fault</span></span> |
   | <span data-ttu-id="177e1-146">4.</span><span class="sxs-lookup"><span data-stu-id="177e1-146">4</span></span> |<span data-ttu-id="177e1-147">БПО исправен</span><span class="sxs-lookup"><span data-stu-id="177e1-147">PCM OK</span></span> |
   | <span data-ttu-id="177e1-148">5</span><span class="sxs-lookup"><span data-stu-id="177e1-148">5</span></span> |<span data-ttu-id="177e1-149">Сбой постоянного напряжения</span><span class="sxs-lookup"><span data-stu-id="177e1-149">DC power failure</span></span> |
   | <span data-ttu-id="177e1-150">6</span><span class="sxs-lookup"><span data-stu-id="177e1-150">6</span></span> |<span data-ttu-id="177e1-151">Батарея работоспособна</span><span class="sxs-lookup"><span data-stu-id="177e1-151">Battery healthy</span></span> |
3. <span data-ttu-id="177e1-152">Для снятия БПО с неисправной батареей выполните действия, описанные в разделе [Снятие БПО](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="177e1-152">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="177e1-153">Сняв БПО, поднимите и поверните рукоятку модуля аккумулятора вверх, как показано на следующем рисунке, и потяните за нее для снятия модуля аккумулятора.</span><span class="sxs-lookup"><span data-stu-id="177e1-153">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![Снятие батареи БПО](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="177e1-155">**Рис. 3.** Извлечение аккумуляторной батареи из БПО</span><span class="sxs-lookup"><span data-stu-id="177e1-155">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="177e1-156">Поместите модуль в упаковку модуля, заменяемого в полевых условиях.</span><span class="sxs-lookup"><span data-stu-id="177e1-156">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="177e1-157">Верните неисправный блок Microsoft для соответствующего обслуживания.</span><span class="sxs-lookup"><span data-stu-id="177e1-157">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="177e1-158">Установка нового модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="177e1-158">Install a new backup battery module</span></span>
<span data-ttu-id="177e1-159">Чтобы установить новый модуль аккумулятора в БПО в основном корпусе устройства StorSimple, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="177e1-159">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="177e1-160">Для установки модуля аккумулятора</span><span class="sxs-lookup"><span data-stu-id="177e1-160">To install the battery module</span></span>
1. <span data-ttu-id="177e1-161">Установите модуль резервного аккумулятора в БПО в правильном положении.</span><span class="sxs-lookup"><span data-stu-id="177e1-161">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="177e1-162">Нажимайте на модуль аккумулятора до упора, чтобы он вошел в разъем.</span><span class="sxs-lookup"><span data-stu-id="177e1-162">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="177e1-163">Замените БПО в основном корпусе в соответствии с инструкциями в разделе [Замена блока питания и охлаждения для устройства StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="177e1-163">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="177e1-164">По завершении замены на классическом портале Azure выберите **Устройства** > **Обслуживание** > **Состояние оборудования**.</span><span class="sxs-lookup"><span data-stu-id="177e1-164">After the replacement is complete, go to **Devices** > **Maintenance** > **Hardware Status** in the Azure classic portal.</span></span> <span data-ttu-id="177e1-165">Проверьте состояние аккумулятора, чтобы убедиться в том, что установка прошла успешно.</span><span class="sxs-lookup"><span data-stu-id="177e1-165">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="177e1-166">Зеленый индикатор указывает на то, что аккумулятор исправен.</span><span class="sxs-lookup"><span data-stu-id="177e1-166">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="177e1-167">Обслуживание модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="177e1-167">Maintain the backup battery module</span></span>
<span data-ttu-id="177e1-168">Модуль резервного аккумулятора в устройстве StorSimple предоставляет аварийное питание для контроллера при исчезновении сетевого напряжения.</span><span class="sxs-lookup"><span data-stu-id="177e1-168">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="177e1-169">Это позволяет устройству StorSimple сохранить важные данные до завершения работы контролируемым образом.</span><span class="sxs-lookup"><span data-stu-id="177e1-169">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="177e1-170">С двумя полностью заряженными аккумуляторами в БПО система может выдержать два последовательных отключения питания.</span><span class="sxs-lookup"><span data-stu-id="177e1-170">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="177e1-171">На классическом портале Azure в разделе **Состояние оборудования** на странице **Обслуживание** отображается информация о неисправности аккумулятора и об окончании срока службы аккумуляторной батареи.</span><span class="sxs-lookup"><span data-stu-id="177e1-171">In the Azure classic portal, the **Hardware Status** on the **Maintenance** page indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="177e1-172">Состояние аккумуляторов отображается в разделах **Батарея в PCM 0** и **Батарея в PCM 1** в разделе **Общие компоненты**.</span><span class="sxs-lookup"><span data-stu-id="177e1-172">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="177e1-173">На этой странице отображается состояние **Ограничено** при приближении окончания срока службы и **Неисправен** при окончании срока службы.</span><span class="sxs-lookup"><span data-stu-id="177e1-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="177e1-174">Состояние аккумулятора может измениться на **НЕИСПРАВЕН** при необходимости его зарядки.</span><span class="sxs-lookup"><span data-stu-id="177e1-174">The battery can report **FAILED** when it simply needs to be charged.</span></span>
> 
> 

<span data-ttu-id="177e1-175">При появлении состояния **ОГРАНИЧЕН** рекомендуется следующий порядок действий:</span><span class="sxs-lookup"><span data-stu-id="177e1-175">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="177e1-176">Система могла недавно подвергнуться отключению питания или аккумуляторы могут подвергаться периодическому обслуживанию.</span><span class="sxs-lookup"><span data-stu-id="177e1-176">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="177e1-177">Перед выполнением дальнейших действий наблюдайте за состоянием системы в течение 12 часов.</span><span class="sxs-lookup"><span data-stu-id="177e1-177">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="177e1-178">Если по истечении 12 часов подключения к сети питания с работающими контроллерами и БПО аккумулятор по-прежнему находится в состоянии **ОГРАНИЧЕН** , этот аккумулятор необходимо заменить.</span><span class="sxs-lookup"><span data-stu-id="177e1-178">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="177e1-179">Для получения нового модуля резервного аккумулятора [обратитесь в службу поддержки Microsoft](storsimple-contact-microsoft-support.md) .</span><span class="sxs-lookup"><span data-stu-id="177e1-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="177e1-180">Если за 12 часов состояние аккумулятора изменилось на исправное, аккумулятор работает нормально, и ему требуется только обслуживание.</span><span class="sxs-lookup"><span data-stu-id="177e1-180">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="177e1-181">Если соответствующего отключения сетевого напряжения не было, БПО включен и подключен к сети, аккумулятор необходимо заменить.</span><span class="sxs-lookup"><span data-stu-id="177e1-181">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="177e1-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) .</span><span class="sxs-lookup"><span data-stu-id="177e1-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="177e1-183">Утилизируйте неисправную батарею в соответствии с федеральным и региональным законодательством.</span><span class="sxs-lookup"><span data-stu-id="177e1-183">Dispose of the failed battery according to national and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="177e1-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="177e1-184">Next steps</span></span>
<span data-ttu-id="177e1-185">Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="177e1-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

