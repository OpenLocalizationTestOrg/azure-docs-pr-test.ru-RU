---
title: "батарея aaaReplace устройства серии Microsoft Azure StorSimple 8000 | Документы Microsoft"
description: "Описывается порядок tooremove, замените и поддерживать hello резервного аккумуляторного модуля на устройстве StorSimple."
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
ms.openlocfilehash: 5ac767807e6c3fd817d8d522629db2aceaac9bdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="590ac-103">Замените hello резервного аккумуляторного модуля на устройстве StorSimple</span><span class="sxs-lookup"><span data-stu-id="590ac-103">Replace hello backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="590ac-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="590ac-104">Overview</span></span>
<span data-ttu-id="590ac-105">основной корпус Hello питания и охлаждения модуля (PCM) на устройстве Microsoft Azure StorSimple с дополнительным комплектом аккумуляторов.</span><span class="sxs-lookup"><span data-stu-id="590ac-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="590ac-106">Этот комплект предоставляет электроэнергию, чтобы hello устройства StorSimple можно сохранить данные при отключении питания переменного ТОКА: toohello основного корпуса.</span><span class="sxs-lookup"><span data-stu-id="590ac-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="590ac-107">Этот комплект аккумуляторов — hello ссылка tooas *резервного аккумуляторного модуля*.</span><span class="sxs-lookup"><span data-stu-id="590ac-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="590ac-108">Hello резервный Аккумуляторный модуль предусмотрен только для основного корпуса устройства StorSimple hello (hello корпусе не содержат резервного аккумуляторного модуля).</span><span class="sxs-lookup"><span data-stu-id="590ac-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="590ac-109">В этом учебнике объясняется, как выполнить такие задачи:</span><span class="sxs-lookup"><span data-stu-id="590ac-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="590ac-110">Удалите hello резервного аккумуляторного модуля</span><span class="sxs-lookup"><span data-stu-id="590ac-110">Remove hello backup battery module</span></span>
* <span data-ttu-id="590ac-111">Установка нового модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="590ac-111">Install a new backup battery module</span></span>
* <span data-ttu-id="590ac-112">Ведение hello резервного аккумуляторного модуля</span><span class="sxs-lookup"><span data-stu-id="590ac-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="590ac-113">До удаления и замены резервного аккумуляторного модуля, просмотрите сведения о безопасности hello в hello [замена компонентов оборудования введение tooStorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="590ac-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="590ac-114">Удалите hello резервного аккумуляторного модуля</span><span class="sxs-lookup"><span data-stu-id="590ac-114">Remove hello backup battery module</span></span>
<span data-ttu-id="590ac-115">Hello резервного аккумуляторного модуля для устройства StorSimple является сменного блока.</span><span class="sxs-lookup"><span data-stu-id="590ac-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="590ac-116">Перед установкой в hello PCM hello аккумуляторного модуля должны храниться в своей оригинальной упаковке.</span><span class="sxs-lookup"><span data-stu-id="590ac-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="590ac-117">Выполните следующие шаги tooremove hello резервного аккумулятора hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="590ac-118">tooremove hello резервного аккумуляторного модуля</span><span class="sxs-lookup"><span data-stu-id="590ac-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="590ac-119">В hello портал Azure перейдите колонке службы tooyour устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="590ac-119">In hello Azure portal, go tooyour StorSimple Device Manager service blade.</span></span> <span data-ttu-id="590ac-120">Go слишком**устройств** и выберите устройство из списка устройств hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-120">Go too**Devices** and then select your device from hello list of devices.</span></span> <span data-ttu-id="590ac-121">Перейдите в слишком**монитор** > **работоспособности оборудования**.</span><span class="sxs-lookup"><span data-stu-id="590ac-121">Navigate too**Monitor** > **Hardware health**.</span></span> <span data-ttu-id="590ac-122">В разделе **общие компоненты**, просмотрите состояние аккумулятора, hello hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-122">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="590ac-123">Идентифицируйте PCM hello, в которой hello перестал работать аккумулятор.</span><span class="sxs-lookup"><span data-stu-id="590ac-123">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="590ac-124">Рисунок 1 демонстрирует hello задняя сторона устройства StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-124">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Задняя панель модулей основного корпуса устройства](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="590ac-126">**Рис. 1.** Задняя поверхность основного устройства с БПО и модулями контроллера</span><span class="sxs-lookup"><span data-stu-id="590ac-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="590ac-127">Метка</span><span class="sxs-lookup"><span data-stu-id="590ac-127">Label</span></span> | <span data-ttu-id="590ac-128">Описание</span><span class="sxs-lookup"><span data-stu-id="590ac-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="590ac-129">1</span><span class="sxs-lookup"><span data-stu-id="590ac-129">1</span></span> |<span data-ttu-id="590ac-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="590ac-130">PCM 0</span></span> |
   | <span data-ttu-id="590ac-131">2</span><span class="sxs-lookup"><span data-stu-id="590ac-131">2</span></span> |<span data-ttu-id="590ac-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="590ac-132">PCM 1</span></span> |
   | <span data-ttu-id="590ac-133">3</span><span class="sxs-lookup"><span data-stu-id="590ac-133">3</span></span> |<span data-ttu-id="590ac-134">Контроллер 0</span><span class="sxs-lookup"><span data-stu-id="590ac-134">Controller 0</span></span> |
   | <span data-ttu-id="590ac-135">4.</span><span class="sxs-lookup"><span data-stu-id="590ac-135">4</span></span> |<span data-ttu-id="590ac-136">Контроллер 1</span><span class="sxs-lookup"><span data-stu-id="590ac-136">Controller 1</span></span> |
   
    <span data-ttu-id="590ac-137">Как показано номер 3 на рис. 2 hello hello мониторинга индикатор СВЕТОДИОД PCM 0, который соответствует слишком**батареи** должен гореть.</span><span class="sxs-lookup"><span data-stu-id="590ac-137">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Светодиодные индикаторы мониторинга на задней панели БПО устройства](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="590ac-139">**На рисунке 2** задняя сторона модуля PCM отображение hello Светодиодные индикаторы мониторинга</span><span class="sxs-lookup"><span data-stu-id="590ac-139">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="590ac-140">Метка</span><span class="sxs-lookup"><span data-stu-id="590ac-140">Label</span></span> | <span data-ttu-id="590ac-141">Описание</span><span class="sxs-lookup"><span data-stu-id="590ac-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="590ac-142">1</span><span class="sxs-lookup"><span data-stu-id="590ac-142">1</span></span> |<span data-ttu-id="590ac-143">Сбой питания от электросети</span><span class="sxs-lookup"><span data-stu-id="590ac-143">AC power failure</span></span> |
   | <span data-ttu-id="590ac-144">2</span><span class="sxs-lookup"><span data-stu-id="590ac-144">2</span></span> |<span data-ttu-id="590ac-145">Сбой вентилятора</span><span class="sxs-lookup"><span data-stu-id="590ac-145">Fan failure</span></span> |
   | <span data-ttu-id="590ac-146">3</span><span class="sxs-lookup"><span data-stu-id="590ac-146">3</span></span> |<span data-ttu-id="590ac-147">Сбой аккумулятора</span><span class="sxs-lookup"><span data-stu-id="590ac-147">Battery fault</span></span> |
   | <span data-ttu-id="590ac-148">4.</span><span class="sxs-lookup"><span data-stu-id="590ac-148">4</span></span> |<span data-ttu-id="590ac-149">БПО исправен</span><span class="sxs-lookup"><span data-stu-id="590ac-149">PCM OK</span></span> |
   | <span data-ttu-id="590ac-150">5</span><span class="sxs-lookup"><span data-stu-id="590ac-150">5</span></span> |<span data-ttu-id="590ac-151">Сбой постоянного напряжения</span><span class="sxs-lookup"><span data-stu-id="590ac-151">DC power failure</span></span> |
   | <span data-ttu-id="590ac-152">6</span><span class="sxs-lookup"><span data-stu-id="590ac-152">6</span></span> |<span data-ttu-id="590ac-153">Батарея работоспособна</span><span class="sxs-lookup"><span data-stu-id="590ac-153">Battery healthy</span></span> |
3. <span data-ttu-id="590ac-154">hello tooremove PCM с неисправным аккумулятором, следуйте указаниям hello [удаления PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="590ac-154">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="590ac-155">Удален PCM приветствия, точности прогнозов и поворот hello батареи модуль обработки вверх, как указано в следующий рисунок hello и выдвинуть tooremove hello батареи.</span><span class="sxs-lookup"><span data-stu-id="590ac-155">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![Снятие батареи БПО](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="590ac-157">**Рис. 3** удаление hello батареи из hello PCM</span><span class="sxs-lookup"><span data-stu-id="590ac-157">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="590ac-158">Поместите hello модуль в упаковку сменного блока hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-158">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="590ac-159">Возвращает tooMicrosoft hello неисправный блок для соответствующего обслуживания и обработки.</span><span class="sxs-lookup"><span data-stu-id="590ac-159">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="590ac-160">Установка нового модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="590ac-160">Install a new backup battery module</span></span>
<span data-ttu-id="590ac-161">Выполните следующие шаги tooinstall hello замены аккумуляторного модуля в hello PCM в hello основного корпуса устройства StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-161">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="590ac-162">tooinstall hello аккумуляторного модуля</span><span class="sxs-lookup"><span data-stu-id="590ac-162">tooinstall hello battery module</span></span>
1. <span data-ttu-id="590ac-163">Поместите hello резервного аккумуляторного модуля в правильное расположение hello в hello PCM.</span><span class="sxs-lookup"><span data-stu-id="590ac-163">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="590ac-164">Нажмите клавишу вниз hello аккумуляторного модуля обработки всех hello способом tooseat hello соединителя.</span><span class="sxs-lookup"><span data-stu-id="590ac-164">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="590ac-165">Замените hello PCM в основном корпусе hello, следуя правилам hello в [замена модуля питания и охлаждения на устройстве StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="590ac-165">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="590ac-166">После завершения замены hello переходит tooyour устройства, а затем слишком**монитор** > **работоспособности оборудования** в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="590ac-166">After hello replacement is complete, go tooyour device and then go too**Monitor** > **Hardware health** in hello Azure portal.</span></span> <span data-ttu-id="590ac-167">Проверьте состояние hello toomake батареи hello убедиться в успешности установки hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-167">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="590ac-168">Зеленый индикатор указывает, что hello аккумулятор исправен.</span><span class="sxs-lookup"><span data-stu-id="590ac-168">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="590ac-169">Ведение hello резервного аккумуляторного модуля</span><span class="sxs-lookup"><span data-stu-id="590ac-169">Maintain hello backup battery module</span></span>
<span data-ttu-id="590ac-170">В вашем устройстве StorSimple hello резервного аккумуляторного модуля предоставляет power toohello контроллера при отключении сетевого питания.</span><span class="sxs-lookup"><span data-stu-id="590ac-170">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="590ac-171">Она позволяет hello StorSimple устройство toosave критически важных данных предыдущих tooshutting вниз контролируемым образом.</span><span class="sxs-lookup"><span data-stu-id="590ac-171">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="590ac-172">С hello PCM две полностью заряженной батареи hello системы может обрабатывать два последовательных отключения питания.</span><span class="sxs-lookup"><span data-stu-id="590ac-172">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="590ac-173">В hello портал Azure, hello **работоспособности оборудования** под hello **монитор** колонке указывает неисправности аккумуляторов hello или hello окончания срок приближается.</span><span class="sxs-lookup"><span data-stu-id="590ac-173">In hello Azure portal, hello **Hardware health** under hello **Monitor** blade indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="590ac-174">Указывает состояние батареи Hello **батарея в PCM 0** или **аккумулятор в PCM 1** под **общие компоненты**.</span><span class="sxs-lookup"><span data-stu-id="590ac-174">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="590ac-175">В этой колонке отображается состояние **ОГРАНИЧЕНО** при приближении окончания срока службы и **НЕИСПРАВНО** при окончании срока службы.</span><span class="sxs-lookup"><span data-stu-id="590ac-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="590ac-176">можно сообщить Hello батареи **сбой** при достаточно toobe взимается плата.</span><span class="sxs-lookup"><span data-stu-id="590ac-176">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>


<span data-ttu-id="590ac-177">Если hello **ДЕГРАДАЦИЯ** отображается состояние, мы рекомендуем hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="590ac-177">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="590ac-178">Hello системы может испытывать последних отключения питания или hello батарей может выполняться периодическое обслуживание.</span><span class="sxs-lookup"><span data-stu-id="590ac-178">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="590ac-179">Наблюдать за системы hello 12 часов, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="590ac-179">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="590ac-180">Если по-прежнему находится в состоянии hello **ДЕГРАДАЦИЯ** после 12 часов power tooAC постоянного соединения с hello контроллеров и PCM под управлением, затем hello батарей должна toobe замены.</span><span class="sxs-lookup"><span data-stu-id="590ac-180">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="590ac-181">Для получения нового модуля резервного аккумулятора [обратитесь в службу поддержки Microsoft](storsimple-8000-contact-microsoft-support.md) .</span><span class="sxs-lookup"><span data-stu-id="590ac-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="590ac-182">Если переходит в состояние hello ОК через 12 часов, hello аккумулятор Исправен и его потребуется лишь расходов на обслуживание.</span><span class="sxs-lookup"><span data-stu-id="590ac-182">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="590ac-183">Если не было связанного потери питания и hello PCM включен и подключен tooAC power, батареи hello должен toobe замены.</span><span class="sxs-lookup"><span data-stu-id="590ac-183">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="590ac-184">[Обратитесь в службу поддержки корпорации Майкрософт](storsimple-8000-contact-microsoft-support.md) tooorder сменного резервного аккумуляторного модуля.</span><span class="sxs-lookup"><span data-stu-id="590ac-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="590ac-185">Уничтожьте hello сбой аккумулятора, в соответствии с toonational и язык правила.</span><span class="sxs-lookup"><span data-stu-id="590ac-185">Dispose of hello failed battery according toonational and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="590ac-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="590ac-186">Next steps</span></span>
<span data-ttu-id="590ac-187">Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="590ac-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

