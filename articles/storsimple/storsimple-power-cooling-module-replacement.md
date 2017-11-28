---
title: "Замена БПО на устройстве StorSimple | Документация Майкрософт"
description: "Объясняется процесс снятия и замены блока питания и охлаждения модуля (БПО) на устройстве StorSimple"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 2a956de58b279a013913631a077d7b03c6327f72
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="669d2-103">Замена блока питания и охлаждения на устройстве StorSimple</span><span class="sxs-lookup"><span data-stu-id="669d2-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="669d2-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="669d2-104">Overview</span></span>
<span data-ttu-id="669d2-105">Блок питания и охлаждения (БПО) на устройстве Microsoft Azure StorSimple состоит из источников питания и вентиляторов, которые управляются с помощью основного корпуса и корпуса EBOD.</span><span class="sxs-lookup"><span data-stu-id="669d2-105">The Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through the primary and EBOD enclosures.</span></span> <span data-ttu-id="669d2-106">Для каждого корпуса сертифицирована только одна модель БПО.</span><span class="sxs-lookup"><span data-stu-id="669d2-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="669d2-107">Основной корпус сертифицирован для БПО мощностью 764 Вт, а корпус EBOD — для БПО мощностью 580 Вт.</span><span class="sxs-lookup"><span data-stu-id="669d2-107">The primary enclosure is certified for a 764 W PCM and the EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="669d2-108">Несмотря на то что БПО для основного корпуса и корпуса EBOD различаются, процедура замены идентична.</span><span class="sxs-lookup"><span data-stu-id="669d2-108">Although the PCMs for the primary enclosure and the EBOD enclosure are different, the replacement procedure is identical.</span></span>

<span data-ttu-id="669d2-109">В этом учебнике объясняется, как выполнить такие задачи:</span><span class="sxs-lookup"><span data-stu-id="669d2-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="669d2-110">Снятие БПО</span><span class="sxs-lookup"><span data-stu-id="669d2-110">Remove a PCM</span></span>
* <span data-ttu-id="669d2-111">Установка нового БПО</span><span class="sxs-lookup"><span data-stu-id="669d2-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="669d2-112">Перед снятием и заменой БПО ознакомьтесь со сведениями о безопасности в разделе [Замена компонентов оборудования StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="669d2-112">Before removing and replacing a PCM, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="669d2-113">Перед заменой БПО</span><span class="sxs-lookup"><span data-stu-id="669d2-113">Before you replace a PCM</span></span>
<span data-ttu-id="669d2-114">Перед заменой учтите следующие важные моменты.</span><span class="sxs-lookup"><span data-stu-id="669d2-114">Be aware of the following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="669d2-115">В случае сбоя питания БПО оставьте неисправный блок на месте, но отключите шнур питания.</span><span class="sxs-lookup"><span data-stu-id="669d2-115">If the power supply of the PCM fails, leave the faulty module installed, but remove the power cord.</span></span> <span data-ttu-id="669d2-116">Вентилятор продолжит получать питание от корпуса и обеспечивать необходимое охлаждение.</span><span class="sxs-lookup"><span data-stu-id="669d2-116">The fan will continue to receive power from the enclosure and continue to provide proper cooling.</span></span> <span data-ttu-id="669d2-117">В случае сбоя вентилятора БПО необходимо немедленно заменить.</span><span class="sxs-lookup"><span data-stu-id="669d2-117">If the fan fails, the PCM needs to be replaced immediately.</span></span>
* <span data-ttu-id="669d2-118">Перед снятием БПО отключите питание БПО, выключив тумблер питания (при наличии) или физически отключив шнур питания.</span><span class="sxs-lookup"><span data-stu-id="669d2-118">Before removing the PCM, disconnect the power from the PCM by turning off the main switch (where present) or by physically removing the power cord.</span></span> <span data-ttu-id="669d2-119">При этом в системе появится предупреждение о предстоящем отключении питания.</span><span class="sxs-lookup"><span data-stu-id="669d2-119">This provides a warning to your system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="669d2-120">Перед заменой неисправного БПО убедитесь, что другие БПО работают.</span><span class="sxs-lookup"><span data-stu-id="669d2-120">Make sure that the other PCM is functional for continued system operation before replacing the faulty PCM.</span></span> <span data-ttu-id="669d2-121">Неисправный БПО необходимо заменить на полностью рабочий БПО как можно быстрее.</span><span class="sxs-lookup"><span data-stu-id="669d2-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="669d2-122">Замена БПО занимает всего несколько минут, но она должна быть завершена в течение 10 минут после снятия неисправного БПО для предотвращения перегрева.</span><span class="sxs-lookup"><span data-stu-id="669d2-122">PCM module replacement takes only few minutes to complete, but it must be completed within 10 minutes of removing the failed PCM to prevent overheating.</span></span>
* <span data-ttu-id="669d2-123">Обратите внимание на то, что сменные модули 764 W PCM, поставленные с завода, не включают модуль резервного аккумулятора.</span><span class="sxs-lookup"><span data-stu-id="669d2-123">Note that the replacement 764 W PCM modules shipped from the factory do not contain the backup battery module.</span></span> <span data-ttu-id="669d2-124">Извлеките аккумулятор из неисправного PCM и вставьте его в сменный модуль, прежде чем произвести замену.</span><span class="sxs-lookup"><span data-stu-id="669d2-124">You will need to remove the battery from your faulty PCM and then insert it into the replacement module prior to performing the replacement.</span></span> <span data-ttu-id="669d2-125">Дополнительные сведения см. в инструкциях по [извлечению и вставке нового модуля резервного аккумулятора](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="669d2-125">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="669d2-126">Снятие БПО</span><span class="sxs-lookup"><span data-stu-id="669d2-126">Remove a PCM</span></span>
<span data-ttu-id="669d2-127">Когда вы будете готовы к снятию блока питания и охлаждения (БПО) с устройства Microsoft Azure StorSimple, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="669d2-127">Follow these instructions when you are ready to remove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="669d2-128">Перед снятием БПО убедитесь, что правильно выбрали замену (764 Вт для основного корпуса и 580 Вт для корпуса EBOD).</span><span class="sxs-lookup"><span data-stu-id="669d2-128">Before you remove your PCM, verify that you have a correct replacement (764 W for the primary enclosure or 580 W for the EBOD enclosure).</span></span>
> 
> 

#### <a name="to-remove-a-pcm"></a><span data-ttu-id="669d2-129">Снятие БПО</span><span class="sxs-lookup"><span data-stu-id="669d2-129">To remove a PCM</span></span>
1. <span data-ttu-id="669d2-130">На классическом портале Azure щелкните **Устройства** > **Обслуживание** > **Состояние оборудования**.</span><span class="sxs-lookup"><span data-stu-id="669d2-130">In the Azure classic portal, click **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="669d2-131">Проверьте состояние компонентов БПО в разделе **Общие компоненты** , чтобы определить неисправный БПО.</span><span class="sxs-lookup"><span data-stu-id="669d2-131">Check the status of the PCM components under **Shared Components** to identify which PCM has failed:</span></span>
   
   * <span data-ttu-id="669d2-132">В случае сбоя питания БПО 0 индикатор **Питание БПО 0** будет красного цвета.</span><span class="sxs-lookup"><span data-stu-id="669d2-132">If a power supply in PCM 0 has failed, the status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="669d2-133">В случае сбоя питания БПО 1 индикатор **Питание БПО 1** будет красного цвета.</span><span class="sxs-lookup"><span data-stu-id="669d2-133">If a power supply in PCM 1 has failed, the status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="669d2-134">При неисправности вентилятора в БПО 1 элементы **Cooling 0 for PCM 0** (Охлаждение 0 для БПО 0) или **Cooling 1 for PCM 0** (Охлаждение 1 для БПО 0) будут красными.</span><span class="sxs-lookup"><span data-stu-id="669d2-134">If the fan in PCM 1 has failed, the status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="669d2-135">Найдите неисправный БПО на обратной стороне основного корпуса.</span><span class="sxs-lookup"><span data-stu-id="669d2-135">Locate the failed PCM on the back of the primary enclosure.</span></span> <span data-ttu-id="669d2-136">При использовании модели 8600 определите основной корпус с помощью идентификационного номера компонента системы, отображаемого на передней панели светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="669d2-136">If you are running an 8600 model, identify the primary enclosure by looking at the System Unit Identification Number shown on the front panel LED display.</span></span> <span data-ttu-id="669d2-137">Идентификационный номер модуля по умолчанию на основном корпусе — это **00**, а идентификационный номер модуля по умолчанию на корпусе EBOD — **01**.</span><span class="sxs-lookup"><span data-stu-id="669d2-137">The default Unit ID displayed on the primary enclosure is **00**, whereas the default Unit ID displayed on the EBOD enclosure is **01**.</span></span> <span data-ttu-id="669d2-138">Передняя панель светодиодного индикатора приведена на следующей схеме и описана в таблице.</span><span class="sxs-lookup"><span data-stu-id="669d2-138">The following diagram and table explain the front panel of the LED display.</span></span>
   
    ![Идентификатор системы на передней панели OPS](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="669d2-140">**Рис. 1.** Передняя панель устройства</span><span class="sxs-lookup"><span data-stu-id="669d2-140">**Figure 1** Front panel of the device</span></span>  
   
   | <span data-ttu-id="669d2-141">Метка</span><span class="sxs-lookup"><span data-stu-id="669d2-141">Label</span></span> | <span data-ttu-id="669d2-142">Описание</span><span class="sxs-lookup"><span data-stu-id="669d2-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="669d2-143">1</span><span class="sxs-lookup"><span data-stu-id="669d2-143">1</span></span> |<span data-ttu-id="669d2-144">Кнопка выключения</span><span class="sxs-lookup"><span data-stu-id="669d2-144">Mute button</span></span> |
   | <span data-ttu-id="669d2-145">2</span><span class="sxs-lookup"><span data-stu-id="669d2-145">2</span></span> |<span data-ttu-id="669d2-146">Питание системы</span><span class="sxs-lookup"><span data-stu-id="669d2-146">System power</span></span> |
   | <span data-ttu-id="669d2-147">3</span><span class="sxs-lookup"><span data-stu-id="669d2-147">3</span></span> |<span data-ttu-id="669d2-148">Сбой модуля</span><span class="sxs-lookup"><span data-stu-id="669d2-148">Module fault</span></span> |
   | <span data-ttu-id="669d2-149">4.</span><span class="sxs-lookup"><span data-stu-id="669d2-149">4</span></span> |<span data-ttu-id="669d2-150">Логический сбой</span><span class="sxs-lookup"><span data-stu-id="669d2-150">Logical fault</span></span> |
   | <span data-ttu-id="669d2-151">5</span><span class="sxs-lookup"><span data-stu-id="669d2-151">5</span></span> |<span data-ttu-id="669d2-152">Дисплей идентификатора модуля</span><span class="sxs-lookup"><span data-stu-id="669d2-152">Unit ID display</span></span> |
3. <span data-ttu-id="669d2-153">Неисправный БПО также можно определить с помощью светодиодных индикаторов мониторинга на задней поверхности основного корпуса.</span><span class="sxs-lookup"><span data-stu-id="669d2-153">The monitoring indicator LEDs in the back of the primary enclosure can also be used to identify the faulty PCM.</span></span> <span data-ttu-id="669d2-154">Определение неисправного БПО с помощью светодиодов показано на следующей схеме и в таблице.</span><span class="sxs-lookup"><span data-stu-id="669d2-154">See the following diagram and table to understand how to use the LEDs to locate the faulty PCM.</span></span> <span data-ttu-id="669d2-155">Например, если горит светодиод **Неисправность вентилятора** , это означает неисправность вентилятора.</span><span class="sxs-lookup"><span data-stu-id="669d2-155">For example, if the LED corresponding to the **Fan Fail** is lit, the fan has failed.</span></span> <span data-ttu-id="669d2-156">Аналогично, если горит светодиодный индикатор **Сбой питания** , произошел сбой питания.</span><span class="sxs-lookup"><span data-stu-id="669d2-156">Likewise, if the LED corresponding to **AC Fail** is lit, the power supply has failed.</span></span> 
   
    ![Светодиодные индикаторы мониторинга на задней панели БПО устройства](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="669d2-158">**Рис. 2.** Задняя панель БПО со светодиодными индикаторами</span><span class="sxs-lookup"><span data-stu-id="669d2-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="669d2-159">Метка</span><span class="sxs-lookup"><span data-stu-id="669d2-159">Label</span></span> | <span data-ttu-id="669d2-160">Описание</span><span class="sxs-lookup"><span data-stu-id="669d2-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="669d2-161">1</span><span class="sxs-lookup"><span data-stu-id="669d2-161">1</span></span> |<span data-ttu-id="669d2-162">Сбой питания от электросети</span><span class="sxs-lookup"><span data-stu-id="669d2-162">AC power failure</span></span> |
   | <span data-ttu-id="669d2-163">2</span><span class="sxs-lookup"><span data-stu-id="669d2-163">2</span></span> |<span data-ttu-id="669d2-164">Сбой вентилятора</span><span class="sxs-lookup"><span data-stu-id="669d2-164">Fan failure</span></span> |
   | <span data-ttu-id="669d2-165">3</span><span class="sxs-lookup"><span data-stu-id="669d2-165">3</span></span> |<span data-ttu-id="669d2-166">Сбой аккумулятора</span><span class="sxs-lookup"><span data-stu-id="669d2-166">Battery fault</span></span> |
   | <span data-ttu-id="669d2-167">4.</span><span class="sxs-lookup"><span data-stu-id="669d2-167">4</span></span> |<span data-ttu-id="669d2-168">БПО исправен</span><span class="sxs-lookup"><span data-stu-id="669d2-168">PCM OK</span></span> |
   | <span data-ttu-id="669d2-169">5</span><span class="sxs-lookup"><span data-stu-id="669d2-169">5</span></span> |<span data-ttu-id="669d2-170">Сбой постоянного напряжения</span><span class="sxs-lookup"><span data-stu-id="669d2-170">DC power failure</span></span> |
   | <span data-ttu-id="669d2-171">6</span><span class="sxs-lookup"><span data-stu-id="669d2-171">6</span></span> |<span data-ttu-id="669d2-172">Батарея работоспособна</span><span class="sxs-lookup"><span data-stu-id="669d2-172">Battery healthy</span></span> |
4. <span data-ttu-id="669d2-173">Для поиска неисправного БПО обратитесь к следующей схеме задней панели устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="669d2-173">Refer to the following diagram of the back of the StorSimple device to locate the failed PCM module.</span></span> <span data-ttu-id="669d2-174">БПО 0 находится слева, а БПО 1 — справа.</span><span class="sxs-lookup"><span data-stu-id="669d2-174">PCM 0 is on the left and PCM 1 is on the right.</span></span> <span data-ttu-id="669d2-175">Подробная информация о БПО приведена в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="669d2-175">The table that follows explains the modules.</span></span>
   
     ![Задняя панель модулей основного корпуса устройства](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="669d2-177">**Рис. 3.** Задняя панель устройства с подключенными модулями</span><span class="sxs-lookup"><span data-stu-id="669d2-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="669d2-178">Метка</span><span class="sxs-lookup"><span data-stu-id="669d2-178">Label</span></span> | <span data-ttu-id="669d2-179">Описание</span><span class="sxs-lookup"><span data-stu-id="669d2-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="669d2-180">1</span><span class="sxs-lookup"><span data-stu-id="669d2-180">1</span></span> |<span data-ttu-id="669d2-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="669d2-181">PCM 0</span></span> |
   | <span data-ttu-id="669d2-182">2</span><span class="sxs-lookup"><span data-stu-id="669d2-182">2</span></span> |<span data-ttu-id="669d2-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="669d2-183">PCM 1</span></span> |
   | <span data-ttu-id="669d2-184">3</span><span class="sxs-lookup"><span data-stu-id="669d2-184">3</span></span> |<span data-ttu-id="669d2-185">Контроллер 0</span><span class="sxs-lookup"><span data-stu-id="669d2-185">Controller 0</span></span> |
   | <span data-ttu-id="669d2-186">4.</span><span class="sxs-lookup"><span data-stu-id="669d2-186">4</span></span> |<span data-ttu-id="669d2-187">Контроллер 1</span><span class="sxs-lookup"><span data-stu-id="669d2-187">Controller 1</span></span> |
5. <span data-ttu-id="669d2-188">Отключите неисправный БПО и отсоедините кабель питания.</span><span class="sxs-lookup"><span data-stu-id="669d2-188">Turn off the faulty PCM and disconnect the power supply cord.</span></span> <span data-ttu-id="669d2-189">Теперь можно снять БПО.</span><span class="sxs-lookup"><span data-stu-id="669d2-189">You can now remove the PCM.</span></span>
6. <span data-ttu-id="669d2-190">Возьмитесь за защелку и боковую поверхность рукоятки БПО большим и указательным пальцем и сожмите их, чтобы открыть рукоятку.</span><span class="sxs-lookup"><span data-stu-id="669d2-190">Grasp the latch and the side of the PCM handle between your thumb and forefinger, and squeeze them together to open the handle.</span></span>
   
    ![Открытие рукоятки БПО](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="669d2-192">**Рис. 4.** Открытие рукоятки БПО</span><span class="sxs-lookup"><span data-stu-id="669d2-192">**Figure 4** Opening the PCM handle</span></span>
7. <span data-ttu-id="669d2-193">Возьмитесь за рукоятку и снимите БПО.</span><span class="sxs-lookup"><span data-stu-id="669d2-193">Grip the handle and remove the PCM.</span></span>
   
    ![Снятие устройства БПО](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="669d2-195">**Рис. 5.** Извлечение БПО</span><span class="sxs-lookup"><span data-stu-id="669d2-195">**Figure 5** Removing the PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="669d2-196">Установка нового БПО</span><span class="sxs-lookup"><span data-stu-id="669d2-196">Install a replacement PCM</span></span>
<span data-ttu-id="669d2-197">Для установки нового БПО на устройство StorSimple выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="669d2-197">Follow these instructions to install a PCM in your StorSimple device.</span></span> <span data-ttu-id="669d2-198">Перед установкой сменного PCM установите модуль резервного аккумулятора (только для 764 W PCM).</span><span class="sxs-lookup"><span data-stu-id="669d2-198">Ensure that you have inserted the backup battery module prior to installing the replacement PCM (applies to 764 W PCMs only).</span></span> <span data-ttu-id="669d2-199">Дополнительные сведения см. в инструкциях по [извлечению и вставке нового модуля резервного аккумулятора](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="669d2-199">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

#### <a name="to-install-a-pcm"></a><span data-ttu-id="669d2-200">Установка БПО</span><span class="sxs-lookup"><span data-stu-id="669d2-200">To install a PCM</span></span>
1. <span data-ttu-id="669d2-201">Убедитесь, что замена для заданного типа корпуса выбрана правильно.</span><span class="sxs-lookup"><span data-stu-id="669d2-201">Verify that you have the correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="669d2-202">Для основного корпуса необходим БПО мощностью 764 Вт, для корпуса EBOD — мощностью 580 Вт.</span><span class="sxs-lookup"><span data-stu-id="669d2-202">The primary enclosure needs a 764 W PCM and the EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="669d2-203">Не стоит пытаться использовать БПО мощностью 580 Вт для основного корпуса или БПО мощностью 764 Вт для корпуса EBOD.</span><span class="sxs-lookup"><span data-stu-id="669d2-203">You should not attempt to use the 580 W PCM in the Primary enclosure, or the 764 W PCM in the EBOD enclosure.</span></span> <span data-ttu-id="669d2-204">На следующем рисунке показано, где найти эти сведения на наклейке изготовителя БПО.</span><span class="sxs-lookup"><span data-stu-id="669d2-204">The following image shows where to identify this information on the label that is affixed to the PCM.</span></span>
   
    ![Наклейка БПО](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="669d2-206">**Рис. 6.** Наклейка БПО</span><span class="sxs-lookup"><span data-stu-id="669d2-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="669d2-207">Проверьте отсутствие повреждений корпуса, уделяя особое внимание разъемам.</span><span class="sxs-lookup"><span data-stu-id="669d2-207">Check for damage to the enclosure, paying particular attention to the connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="669d2-208">**Не устанавливайте блок, если контакты на разъеме изогнуты.**</span><span class="sxs-lookup"><span data-stu-id="669d2-208">**Do not install the module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="669d2-209">С рукояткой БПО в открытом положении установите БПО в корпус.</span><span class="sxs-lookup"><span data-stu-id="669d2-209">With the PCM handle in the open position, slide the module into the enclosure.</span></span>
   
    ![Установка устройства БПО](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="669d2-211">**Рис. 7.** Установка БПО</span><span class="sxs-lookup"><span data-stu-id="669d2-211">**Figure 7** Installing the PCM</span></span>
4. <span data-ttu-id="669d2-212">Закройте рукоятку БПО.</span><span class="sxs-lookup"><span data-stu-id="669d2-212">Manually close the PCM handle.</span></span> <span data-ttu-id="669d2-213">При срабатывании защелки рукоятки должен раздаться щелчок.</span><span class="sxs-lookup"><span data-stu-id="669d2-213">You should hear a click as the handle latch engages.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="669d2-214">Чтобы убедиться, что штырьки разъема встали на место, можно аккуратно потянуть рукоятку, не открывая защелку.</span><span class="sxs-lookup"><span data-stu-id="669d2-214">To ensure that the connector pins have engaged, you can gently tug on the handle without releasing the latch.</span></span> <span data-ttu-id="669d2-215">Если БПО сдвигается, это означает, что защелка закрылась до соединения разъема.</span><span class="sxs-lookup"><span data-stu-id="669d2-215">If the PCM slides out, it implies that the latch was closed before the connectors engaged.</span></span>
   > 
   > 
5. <span data-ttu-id="669d2-216">Подключите кабели питания к источнику питания и БПО.</span><span class="sxs-lookup"><span data-stu-id="669d2-216">Connect the power cables to the power source and to the PCM.</span></span>
6. <span data-ttu-id="669d2-217">Закрепите механические зажимы.</span><span class="sxs-lookup"><span data-stu-id="669d2-217">Secure the strain relief bales.</span></span> 
7. <span data-ttu-id="669d2-218">Включите БПО.</span><span class="sxs-lookup"><span data-stu-id="669d2-218">Turn on the PCM.</span></span>
8. <span data-ttu-id="669d2-219">Убедитесь, что замена выполнена успешно: на классическом портале Azure службы диспетчера StorSimple выберите **Устройства** > **Обслуживание** > **Состояние оборудования**.</span><span class="sxs-lookup"><span data-stu-id="669d2-219">Verify that the replacement was successful: in the Azure classic portal of your StorSimple Manager service, navigate to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="669d2-220">В разделе **Общие компоненты**индикатор состояния БПО должен быть зеленого цвета.</span><span class="sxs-lookup"><span data-stu-id="669d2-220">Under **Shared Components**, the status of the PCM should be green.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="669d2-221">Для полной инициализации установленного БПО может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="669d2-221">It may take a few minutes for the replacement PCM to completely initialize.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="669d2-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="669d2-222">Next steps</span></span>
<span data-ttu-id="669d2-223">Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="669d2-223">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

