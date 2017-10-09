---
title: "aaaReplace PCM устройства серии StorSimple 8000 | Документы Microsoft"
description: "Объясняет, как tooremove и замены hello модуля питания и охлаждения (PCM) на устройстве StorSimple"
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 474fd09787c5361a81efda4de74356027ac60f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="23569-103">Замена блока питания и охлаждения на устройстве StorSimple</span><span class="sxs-lookup"><span data-stu-id="23569-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="23569-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="23569-104">Overview</span></span>
<span data-ttu-id="23569-105">Hello Power модуля и охлаждения (PCM) в Microsoft Azure StorSimple устройство состоит из источников питания и вентиляторы, управление которыми осуществляется через hello основного корпуса и корпуса EBOD.</span><span class="sxs-lookup"><span data-stu-id="23569-105">hello Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through hello primary and EBOD enclosures.</span></span> <span data-ttu-id="23569-106">Для каждого корпуса сертифицирована только одна модель БПО.</span><span class="sxs-lookup"><span data-stu-id="23569-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="23569-107">Hello основной корпус сертифицирован для 764 Вт и hello корпусе сертифицирован для 580 Вт.</span><span class="sxs-lookup"><span data-stu-id="23569-107">hello primary enclosure is certified for a 764 W PCM and hello EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="23569-108">Несмотря на то, что hello PCM hello основного корпуса и корпуса EBOD hello не совпадают, процедура их замены hello совпадает.</span><span class="sxs-lookup"><span data-stu-id="23569-108">Although hello PCMs for hello primary enclosure and hello EBOD enclosure are different, hello replacement procedure is identical.</span></span>

<span data-ttu-id="23569-109">В этом учебнике объясняется, как выполнить такие задачи:</span><span class="sxs-lookup"><span data-stu-id="23569-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="23569-110">Снятие БПО</span><span class="sxs-lookup"><span data-stu-id="23569-110">Remove a PCM</span></span>
* <span data-ttu-id="23569-111">Установка нового БПО</span><span class="sxs-lookup"><span data-stu-id="23569-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23569-112">До удаления и замены PCM, просмотрите сведения о безопасности hello в [замена компонентов оборудования StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="23569-112">Before removing and replacing a PCM, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="23569-113">Перед заменой БПО</span><span class="sxs-lookup"><span data-stu-id="23569-113">Before you replace a PCM</span></span>
<span data-ttu-id="23569-114">Следует учитывать следующие важные проблемы перед заменой PCM hello.</span><span class="sxs-lookup"><span data-stu-id="23569-114">Be aware of hello following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="23569-115">Если из источника питания hello приветствия PCM Перестал работать, не вынимайте неисправный модуль hello, но удаления шнура питания hello.</span><span class="sxs-lookup"><span data-stu-id="23569-115">If hello power supply of hello PCM fails, leave hello faulty module installed, but remove hello power cord.</span></span> <span data-ttu-id="23569-116">вентилятор Hello будет продолжить выполнение tooreceive питание из корпуса hello; tooprovide охлаждение.</span><span class="sxs-lookup"><span data-stu-id="23569-116">hello fan will continue tooreceive power from hello enclosure and continue tooprovide proper cooling.</span></span> <span data-ttu-id="23569-117">При сбое вентилятора hello hello PCM необходимо немедленно заменить toobe.</span><span class="sxs-lookup"><span data-stu-id="23569-117">If hello fan fails, hello PCM needs toobe replaced immediately.</span></span>
* <span data-ttu-id="23569-118">Перед удалением hello PCM, отключиться hello power hello PCM, отключив hello главный выключатель (при наличии) или шнур hello питания.</span><span class="sxs-lookup"><span data-stu-id="23569-118">Before removing hello PCM, disconnect hello power from hello PCM by turning off hello main switch (where present) or by physically removing hello power cord.</span></span> <span data-ttu-id="23569-119">Это обеспечивает tooyour сигнализация приближается, выключение питания.</span><span class="sxs-lookup"><span data-stu-id="23569-119">This provides a warning tooyour system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="23569-120">Убедитесь, что другой PCM продолжает работать для этого приветствия продолжение работы системы до замены неисправного модуля PCM "hello".</span><span class="sxs-lookup"><span data-stu-id="23569-120">Make sure that hello other PCM is functional for continued system operation before replacing hello faulty PCM.</span></span> <span data-ttu-id="23569-121">Неисправный БПО необходимо заменить на полностью рабочий БПО как можно быстрее.</span><span class="sxs-lookup"><span data-stu-id="23569-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="23569-122">Замены модуля PCM выполняется только toocomplete на несколько минут, но она должна быть завершена в 10 минут после удаления перегрева tooprevent hello сбой PCM.</span><span class="sxs-lookup"><span data-stu-id="23569-122">PCM module replacement takes only few minutes toocomplete, but it must be completed within 10 minutes of removing hello failed PCM tooprevent overheating.</span></span>
* <span data-ttu-id="23569-123">Обратите внимание, что hello замены 764 W PCM модули поставляются из фабрики hello не содержат hello резервного аккумуляторного модуля.</span><span class="sxs-lookup"><span data-stu-id="23569-123">Note that hello replacement 764 W PCM modules shipped from hello factory do not contain hello backup battery module.</span></span> <span data-ttu-id="23569-124">Может потребоваться tooremove hello батареи из вашего неисправного модуля PCM и вставьте его в замена hello замены модуля предыдущих tooperforming hello.</span><span class="sxs-lookup"><span data-stu-id="23569-124">You will need tooremove hello battery from your faulty PCM and then insert it into hello replacement module prior tooperforming hello replacement.</span></span> <span data-ttu-id="23569-125">Дополнительные сведения см. в разделе как слишком[удалить и вставить резервного аккумуляторного модуля](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="23569-125">For more information, see how too[remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="23569-126">Снятие БПО</span><span class="sxs-lookup"><span data-stu-id="23569-126">Remove a PCM</span></span>
<span data-ttu-id="23569-127">При работе с устройства Microsoft Azure StorSimple готов tooremove питания и охлаждения модуля (PCM), выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="23569-127">Follow these instructions when you are ready tooremove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="23569-128">Перед извлечением модуля PCM убедитесь, что вы есть запасной модуль нужного (типа 764 Вт для основного корпуса hello) или 580 Вт для корпуса EBOD hello.</span><span class="sxs-lookup"><span data-stu-id="23569-128">Before you remove your PCM, verify that you have a correct replacement (764 W for hello primary enclosure or 580 W for hello EBOD enclosure).</span></span>

#### <a name="tooremove-a-pcm"></a><span data-ttu-id="23569-129">tooremove PCM</span><span class="sxs-lookup"><span data-stu-id="23569-129">tooremove a PCM</span></span>
1. <span data-ttu-id="23569-130">В hello классический портал Azure, щелкните **параметры > монитор > работоспособности оборудования**.</span><span class="sxs-lookup"><span data-stu-id="23569-130">In hello Azure classic portal, click **Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="23569-131">Проверьте состояние компонентов PCM hello в разделе hello **общих компонентов** tooidentify неисправный PCM:</span><span class="sxs-lookup"><span data-stu-id="23569-131">Check hello status of hello PCM components under **Shared components** tooidentify which PCM has failed:</span></span>
   
   * <span data-ttu-id="23569-132">Если произошел сбой питания в PCM 0, hello состояние **источника питания в PCM 0** будет выделен красным цветом.</span><span class="sxs-lookup"><span data-stu-id="23569-132">If a power supply in PCM 0 has failed, hello status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="23569-133">Если источник питания в PCM 1 завершается неудачно, hello состояние **источник питания в PCM 1** будет выделен красным цветом.</span><span class="sxs-lookup"><span data-stu-id="23569-133">If a power supply in PCM 1 has failed, hello status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="23569-134">Если произошел сбой вентилятора hello в PCM 1, hello состояние любого **охлаждение 0 для PCM 0** или **охлаждение 1 для PCM 0** будет выделен красным цветом.</span><span class="sxs-lookup"><span data-stu-id="23569-134">If hello fan in PCM 1 has failed, hello status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="23569-135">Найдите отказавший PCM на hello резервное основного корпуса hello hello.</span><span class="sxs-lookup"><span data-stu-id="23569-135">Locate hello failed PCM on hello back of hello primary enclosure.</span></span> <span data-ttu-id="23569-136">При использовании модели 8600 идентифицировать hello основного корпуса в hello идентификационный номер системы единицы, показан на дисплее передней панели hello.</span><span class="sxs-lookup"><span data-stu-id="23569-136">If you are running an 8600 model, identify hello primary enclosure by looking at hello System Unit Identification Number shown on hello front panel LED display.</span></span> <span data-ttu-id="23569-137">Здравствуйте, по умолчанию является идентификатор единицы измерения, отображаемого на основном корпусе hello **00**, тогда как hello по умолчанию отображается идентификатор модуля hello корпусе — **01**.</span><span class="sxs-lookup"><span data-stu-id="23569-137">hello default Unit ID displayed on hello primary enclosure is **00**, whereas hello default Unit ID displayed on hello EBOD enclosure is **01**.</span></span> <span data-ttu-id="23569-138">Hello следующие схемы и таблице поясняется hello передней панели отображения hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="23569-138">hello following diagram and table explain hello front panel of hello LED display.</span></span>
   
    ![Идентификатор системы на передней панели OPS](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="23569-140">**Рис. 1** передняя панель устройства hello</span><span class="sxs-lookup"><span data-stu-id="23569-140">**Figure 1** Front panel of hello device</span></span>  
   
   | <span data-ttu-id="23569-141">Метка</span><span class="sxs-lookup"><span data-stu-id="23569-141">Label</span></span> | <span data-ttu-id="23569-142">Описание</span><span class="sxs-lookup"><span data-stu-id="23569-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="23569-143">1</span><span class="sxs-lookup"><span data-stu-id="23569-143">1</span></span> |<span data-ttu-id="23569-144">Кнопка выключения</span><span class="sxs-lookup"><span data-stu-id="23569-144">Mute button</span></span> |
   | <span data-ttu-id="23569-145">2</span><span class="sxs-lookup"><span data-stu-id="23569-145">2</span></span> |<span data-ttu-id="23569-146">Питание системы</span><span class="sxs-lookup"><span data-stu-id="23569-146">System power</span></span> |
   | <span data-ttu-id="23569-147">3</span><span class="sxs-lookup"><span data-stu-id="23569-147">3</span></span> |<span data-ttu-id="23569-148">Сбой модуля</span><span class="sxs-lookup"><span data-stu-id="23569-148">Module fault</span></span> |
   | <span data-ttu-id="23569-149">4.</span><span class="sxs-lookup"><span data-stu-id="23569-149">4</span></span> |<span data-ttu-id="23569-150">Логический сбой</span><span class="sxs-lookup"><span data-stu-id="23569-150">Logical fault</span></span> |
   | <span data-ttu-id="23569-151">5</span><span class="sxs-lookup"><span data-stu-id="23569-151">5</span></span> |<span data-ttu-id="23569-152">Дисплей идентификатора модуля</span><span class="sxs-lookup"><span data-stu-id="23569-152">Unit ID display</span></span> |
3. <span data-ttu-id="23569-153">также можно использовать Светодиодные индикаторы в hello задняя сторона основного корпуса hello мониторинга Hello tooidentify hello неисправного модуля PCM.</span><span class="sxs-lookup"><span data-stu-id="23569-153">hello monitoring indicator LEDs in hello back of hello primary enclosure can also be used tooidentify hello faulty PCM.</span></span> <span data-ttu-id="23569-154">См. ниже hello диаграмма и таблица toounderstand как индикаторы toolocate toouse hello hello неисправного модуля PCM.</span><span class="sxs-lookup"><span data-stu-id="23569-154">See hello following diagram and table toounderstand how toouse hello LEDs toolocate hello faulty PCM.</span></span> <span data-ttu-id="23569-155">Если hello РУКОВОДСТВОМ соответствующий toohello **сбою вентилятора** — означает, hello вентилятор перестал работать.</span><span class="sxs-lookup"><span data-stu-id="23569-155">For example, if hello LED corresponding toohello **Fan Fail** is lit, hello fan has failed.</span></span> <span data-ttu-id="23569-156">Аналогично, если hello РУКОВОДСТВОМ соответствующий слишком**сбой Электропитания** — горит, сбой питания hello.</span><span class="sxs-lookup"><span data-stu-id="23569-156">Likewise, if hello LED corresponding too**AC Fail** is lit, hello power supply has failed.</span></span> 
   
    ![Светодиодные индикаторы мониторинга на задней панели БПО устройства](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="23569-158">**Рис. 2.** Задняя панель БПО со светодиодными индикаторами</span><span class="sxs-lookup"><span data-stu-id="23569-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="23569-159">Метка</span><span class="sxs-lookup"><span data-stu-id="23569-159">Label</span></span> | <span data-ttu-id="23569-160">Описание</span><span class="sxs-lookup"><span data-stu-id="23569-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="23569-161">1</span><span class="sxs-lookup"><span data-stu-id="23569-161">1</span></span> |<span data-ttu-id="23569-162">Сбой питания от электросети</span><span class="sxs-lookup"><span data-stu-id="23569-162">AC power failure</span></span> |
   | <span data-ttu-id="23569-163">2</span><span class="sxs-lookup"><span data-stu-id="23569-163">2</span></span> |<span data-ttu-id="23569-164">Сбой вентилятора</span><span class="sxs-lookup"><span data-stu-id="23569-164">Fan failure</span></span> |
   | <span data-ttu-id="23569-165">3</span><span class="sxs-lookup"><span data-stu-id="23569-165">3</span></span> |<span data-ttu-id="23569-166">Сбой аккумулятора</span><span class="sxs-lookup"><span data-stu-id="23569-166">Battery fault</span></span> |
   | <span data-ttu-id="23569-167">4.</span><span class="sxs-lookup"><span data-stu-id="23569-167">4</span></span> |<span data-ttu-id="23569-168">БПО исправен</span><span class="sxs-lookup"><span data-stu-id="23569-168">PCM OK</span></span> |
   | <span data-ttu-id="23569-169">5</span><span class="sxs-lookup"><span data-stu-id="23569-169">5</span></span> |<span data-ttu-id="23569-170">Сбой постоянного напряжения</span><span class="sxs-lookup"><span data-stu-id="23569-170">DC power failure</span></span> |
   | <span data-ttu-id="23569-171">6</span><span class="sxs-lookup"><span data-stu-id="23569-171">6</span></span> |<span data-ttu-id="23569-172">Батарея работоспособна</span><span class="sxs-lookup"><span data-stu-id="23569-172">Battery healthy</span></span> |
4. <span data-ttu-id="23569-173">См. в toohello следующая схема hello задняя сторона модуля PCM hello сбой toolocate устройства hello StorSimple.</span><span class="sxs-lookup"><span data-stu-id="23569-173">Refer toohello following diagram of hello back of hello StorSimple device toolocate hello failed PCM module.</span></span> <span data-ttu-id="23569-174">PCM 0 находится слева hello и PCM 1 имеет hello вправо.</span><span class="sxs-lookup"><span data-stu-id="23569-174">PCM 0 is on hello left and PCM 1 is on hello right.</span></span> <span data-ttu-id="23569-175">Hello приведен в следующей таблице описывается hello модулей.</span><span class="sxs-lookup"><span data-stu-id="23569-175">hello table that follows explains hello modules.</span></span>
   
     ![Задняя панель модулей основного корпуса устройства](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="23569-177">**Рис. 3.** Задняя панель устройства с подключенными модулями</span><span class="sxs-lookup"><span data-stu-id="23569-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="23569-178">Метка</span><span class="sxs-lookup"><span data-stu-id="23569-178">Label</span></span> | <span data-ttu-id="23569-179">Описание</span><span class="sxs-lookup"><span data-stu-id="23569-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="23569-180">1</span><span class="sxs-lookup"><span data-stu-id="23569-180">1</span></span> |<span data-ttu-id="23569-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="23569-181">PCM 0</span></span> |
   | <span data-ttu-id="23569-182">2</span><span class="sxs-lookup"><span data-stu-id="23569-182">2</span></span> |<span data-ttu-id="23569-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="23569-183">PCM 1</span></span> |
   | <span data-ttu-id="23569-184">3</span><span class="sxs-lookup"><span data-stu-id="23569-184">3</span></span> |<span data-ttu-id="23569-185">Контроллер 0</span><span class="sxs-lookup"><span data-stu-id="23569-185">Controller 0</span></span> |
   | <span data-ttu-id="23569-186">4.</span><span class="sxs-lookup"><span data-stu-id="23569-186">4</span></span> |<span data-ttu-id="23569-187">Контроллер 1</span><span class="sxs-lookup"><span data-stu-id="23569-187">Controller 1</span></span> |
5. <span data-ttu-id="23569-188">Включить выходить из системы hello неисправного модуля PCM и отключите шнур питания hello питания.</span><span class="sxs-lookup"><span data-stu-id="23569-188">Turn off hello faulty PCM and disconnect hello power supply cord.</span></span> <span data-ttu-id="23569-189">Теперь можно удалить hello PCM.</span><span class="sxs-lookup"><span data-stu-id="23569-189">You can now remove hello PCM.</span></span>
6. <span data-ttu-id="23569-190">Возьмитесь за кратковременной блокировки hello и hello части hello PCM обрабатывать thumb и указательным пальцами и сожмите их вместе tooopen hello дескриптор.</span><span class="sxs-lookup"><span data-stu-id="23569-190">Grasp hello latch and hello side of hello PCM handle between your thumb and forefinger, and squeeze them together tooopen hello handle.</span></span>
   
    ![Открытие рукоятки БПО](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="23569-192">**Рис. 4** обработки открывающий hello PCM</span><span class="sxs-lookup"><span data-stu-id="23569-192">**Figure 4** Opening hello PCM handle</span></span>
7. <span data-ttu-id="23569-193">Захват hello обработки и удалите hello PCM.</span><span class="sxs-lookup"><span data-stu-id="23569-193">Grip hello handle and remove hello PCM.</span></span>
   
    ![Снятие устройства БПО](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="23569-195">**Рис. 5** hello удаление PCM</span><span class="sxs-lookup"><span data-stu-id="23569-195">**Figure 5** Removing hello PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="23569-196">Установка нового БПО</span><span class="sxs-lookup"><span data-stu-id="23569-196">Install a replacement PCM</span></span>
<span data-ttu-id="23569-197">Выполните эти инструкции tooinstall PCM устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="23569-197">Follow these instructions tooinstall a PCM in your StorSimple device.</span></span> <span data-ttu-id="23569-198">Убедитесь, вставленные hello резервного аккумуляторного модуля предыдущих tooinstalling hello замены PCM (применяется только W PCM too764).</span><span class="sxs-lookup"><span data-stu-id="23569-198">Ensure that you have inserted hello backup battery module prior tooinstalling hello replacement PCM (applies too764 W PCMs only).</span></span> <span data-ttu-id="23569-199">Дополнительные сведения см. в разделе как слишком[удалить и вставить резервного аккумуляторного модуля](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="23569-199">For more information, see how too[remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

#### <a name="tooinstall-a-pcm"></a><span data-ttu-id="23569-200">tooinstall PCM</span><span class="sxs-lookup"><span data-stu-id="23569-200">tooinstall a PCM</span></span>
1. <span data-ttu-id="23569-201">Убедитесь, что у вас есть hello правильный сменный PCM для этого корпуса.</span><span class="sxs-lookup"><span data-stu-id="23569-201">Verify that you have hello correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="23569-202">Hello для основного корпуса требуется PCM мощностью 764 Вт и hello корпуса EBOD требуется PCM мощностью 580 Вт.</span><span class="sxs-lookup"><span data-stu-id="23569-202">hello primary enclosure needs a 764 W PCM and hello EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="23569-203">Не допускается toouse hello 580 Вт в основном корпусе hello или hello 764 Вт в корпусе hello.</span><span class="sxs-lookup"><span data-stu-id="23569-203">You should not attempt toouse hello 580 W PCM in hello Primary enclosure, or hello 764 W PCM in hello EBOD enclosure.</span></span> <span data-ttu-id="23569-204">Следующие изображения Hello показывает, где tooidentify эти сведения о hello метки, прикрепленной toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="23569-204">hello following image shows where tooidentify this information on hello label that is affixed toohello PCM.</span></span>
   
    ![Наклейка БПО](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="23569-206">**Рис. 6.** Наклейка БПО</span><span class="sxs-lookup"><span data-stu-id="23569-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="23569-207">Проверьте наличие повреждений toohello корпусе, уделяя особое внимание toohello соединители.</span><span class="sxs-lookup"><span data-stu-id="23569-207">Check for damage toohello enclosure, paying particular attention toohello connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="23569-208">**Если любой выводы соединителей погнуты, не устанавливайте модуль hello.**</span><span class="sxs-lookup"><span data-stu-id="23569-208">**Do not install hello module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="23569-209">Откройте позиции слайд hello модуль в корпус hello hello PCM обрабатывать hello.</span><span class="sxs-lookup"><span data-stu-id="23569-209">With hello PCM handle in hello open position, slide hello module into hello enclosure.</span></span>
   
    ![Установка устройства БПО](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="23569-211">**Рис. 7** hello Установка PCM</span><span class="sxs-lookup"><span data-stu-id="23569-211">**Figure 7** Installing hello PCM</span></span>
4. <span data-ttu-id="23569-212">Закрытие дескриптора PCM hello вручную.</span><span class="sxs-lookup"><span data-stu-id="23569-212">Manually close hello PCM handle.</span></span> <span data-ttu-id="23569-213">При фиксации защелки дескриптор hello должны услышать щелчок.</span><span class="sxs-lookup"><span data-stu-id="23569-213">You should hear a click as hello handle latch engages.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="23569-214">зафиксированы, hello штырьки tooensure, может Аккуратно потяните за маркер hello без освобождение кратковременной блокировки hello.</span><span class="sxs-lookup"><span data-stu-id="23569-214">tooensure that hello connector pins have engaged, you can gently tug on hello handle without releasing hello latch.</span></span> <span data-ttu-id="23569-215">Если hello PCM выдвигается, это означает, что такую блокировку hello был закрыт до были зафиксированы соединители hello.</span><span class="sxs-lookup"><span data-stu-id="23569-215">If hello PCM slides out, it implies that hello latch was closed before hello connectors engaged.</span></span>
   
5. <span data-ttu-id="23569-216">Подключите источник питания toohello кабели питания hello и toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="23569-216">Connect hello power cables toohello power source and toohello PCM.</span></span>
6. <span data-ttu-id="23569-217">Защита от изгиба hello нагрузку.</span><span class="sxs-lookup"><span data-stu-id="23569-217">Secure hello strain relief bales.</span></span>
7. <span data-ttu-id="23569-218">Включите hello PCM.</span><span class="sxs-lookup"><span data-stu-id="23569-218">Turn on hello PCM.</span></span>
8. <span data-ttu-id="23569-219">Убедитесь, что hello замена выполнена успешно: hello Azure портала службы диспетчера StorSimple устройство, перейдите tooyour устройства и затем слишком**параметры > монитор > работоспособности оборудования**.</span><span class="sxs-lookup"><span data-stu-id="23569-219">Verify that hello replacement was successful: in hello Azure portal of your StorSimple Device Manager service, navigate tooyour device and then too**Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="23569-220">В разделе hello **общих компонентов**, состояние hello hello PCM должны гореть зеленым.</span><span class="sxs-lookup"><span data-stu-id="23569-220">Under hello **Shared components**, hello status of hello PCM should be green.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="23569-221">Он может занять несколько минут, чтобы инициализировать toocompletely PCM замену hello.</span><span class="sxs-lookup"><span data-stu-id="23569-221">It may take a few minutes for hello replacement PCM toocompletely initialize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23569-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="23569-222">Next steps</span></span>
<span data-ttu-id="23569-223">Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="23569-223">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

