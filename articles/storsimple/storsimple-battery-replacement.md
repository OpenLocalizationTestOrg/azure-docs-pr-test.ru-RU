---
title: "батарея aaaReplace устройство Microsoft Azure StorSimple | Документы Microsoft"
description: "Описывается порядок tooremove, замените и поддерживать hello резервного аккумуляторного модуля на устройстве StorSimple."
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
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="973dc-103">Замените hello резервного аккумуляторного модуля на устройстве StorSimple</span><span class="sxs-lookup"><span data-stu-id="973dc-103">Replace hello backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="973dc-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="973dc-104">Overview</span></span>
<span data-ttu-id="973dc-105">основной корпус Hello питания и охлаждения модуля (PCM) на устройстве Microsoft Azure StorSimple с дополнительным комплектом аккумуляторов.</span><span class="sxs-lookup"><span data-stu-id="973dc-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="973dc-106">Этот комплект предоставляет электроэнергию, чтобы hello устройства StorSimple можно сохранить данные при отключении питания переменного ТОКА: toohello основного корпуса.</span><span class="sxs-lookup"><span data-stu-id="973dc-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="973dc-107">Этот комплект аккумуляторов — hello ссылка tooas *резервного аккумуляторного модуля*.</span><span class="sxs-lookup"><span data-stu-id="973dc-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="973dc-108">Hello резервный Аккумуляторный модуль предусмотрен только для основного корпуса устройства StorSimple hello (hello корпусе не содержат резервного аккумуляторного модуля).</span><span class="sxs-lookup"><span data-stu-id="973dc-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="973dc-109">В этом учебнике объясняется, как выполнить такие задачи:</span><span class="sxs-lookup"><span data-stu-id="973dc-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="973dc-110">Удалите hello резервного аккумуляторного модуля</span><span class="sxs-lookup"><span data-stu-id="973dc-110">Remove hello backup battery module</span></span> 
* <span data-ttu-id="973dc-111">Установка нового модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="973dc-111">Install a new backup battery module</span></span>
* <span data-ttu-id="973dc-112">Ведение hello резервного аккумуляторного модуля</span><span class="sxs-lookup"><span data-stu-id="973dc-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="973dc-113">До удаления и замены резервного аккумуляторного модуля, просмотрите сведения о безопасности hello в hello [замена компонентов оборудования введение tooStorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="973dc-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="973dc-114">Удалите hello резервного аккумуляторного модуля</span><span class="sxs-lookup"><span data-stu-id="973dc-114">Remove hello backup battery module</span></span>
<span data-ttu-id="973dc-115">Hello резервного аккумуляторного модуля для устройства StorSimple является сменного блока.</span><span class="sxs-lookup"><span data-stu-id="973dc-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="973dc-116">Перед установкой в hello PCM hello аккумуляторного модуля должны храниться в своей оригинальной упаковке.</span><span class="sxs-lookup"><span data-stu-id="973dc-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="973dc-117">Выполните следующие шаги tooremove hello резервного аккумулятора hello.</span><span class="sxs-lookup"><span data-stu-id="973dc-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="973dc-118">tooremove hello резервного аккумуляторного модуля</span><span class="sxs-lookup"><span data-stu-id="973dc-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="973dc-119">В hello классический портал Azure, перейдите в слишком**устройств** > **обслуживания** > **состояние оборудования**.</span><span class="sxs-lookup"><span data-stu-id="973dc-119">In hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="973dc-120">В разделе **общие компоненты**, просмотрите состояние аккумулятора, hello hello.</span><span class="sxs-lookup"><span data-stu-id="973dc-120">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="973dc-121">Идентифицируйте PCM hello, в которой hello перестал работать аккумулятор.</span><span class="sxs-lookup"><span data-stu-id="973dc-121">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="973dc-122">Рисунок 1 демонстрирует hello задняя сторона устройства StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="973dc-122">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Задняя панель модулей основного корпуса устройства](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="973dc-124">**Рис. 1.** Задняя поверхность основного устройства с БПО и модулями контроллера</span><span class="sxs-lookup"><span data-stu-id="973dc-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="973dc-125">Метка</span><span class="sxs-lookup"><span data-stu-id="973dc-125">Label</span></span> | <span data-ttu-id="973dc-126">Описание</span><span class="sxs-lookup"><span data-stu-id="973dc-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="973dc-127">1</span><span class="sxs-lookup"><span data-stu-id="973dc-127">1</span></span> |<span data-ttu-id="973dc-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="973dc-128">PCM 0</span></span> |
   | <span data-ttu-id="973dc-129">2</span><span class="sxs-lookup"><span data-stu-id="973dc-129">2</span></span> |<span data-ttu-id="973dc-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="973dc-130">PCM 1</span></span> |
   | <span data-ttu-id="973dc-131">3</span><span class="sxs-lookup"><span data-stu-id="973dc-131">3</span></span> |<span data-ttu-id="973dc-132">Контроллер 0</span><span class="sxs-lookup"><span data-stu-id="973dc-132">Controller 0</span></span> |
   | <span data-ttu-id="973dc-133">4.</span><span class="sxs-lookup"><span data-stu-id="973dc-133">4</span></span> |<span data-ttu-id="973dc-134">Контроллер 1</span><span class="sxs-lookup"><span data-stu-id="973dc-134">Controller 1</span></span> |
   
    <span data-ttu-id="973dc-135">Как показано номер 3 на рис. 2 hello hello мониторинга индикатор СВЕТОДИОД PCM 0, который соответствует слишком**батареи** должен гореть.</span><span class="sxs-lookup"><span data-stu-id="973dc-135">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Светодиодные индикаторы мониторинга на задней панели БПО устройства](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="973dc-137">**На рисунке 2** задняя сторона модуля PCM отображение hello Светодиодные индикаторы мониторинга</span><span class="sxs-lookup"><span data-stu-id="973dc-137">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="973dc-138">Метка</span><span class="sxs-lookup"><span data-stu-id="973dc-138">Label</span></span> | <span data-ttu-id="973dc-139">Описание</span><span class="sxs-lookup"><span data-stu-id="973dc-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="973dc-140">1</span><span class="sxs-lookup"><span data-stu-id="973dc-140">1</span></span> |<span data-ttu-id="973dc-141">Сбой питания от электросети</span><span class="sxs-lookup"><span data-stu-id="973dc-141">AC power failure</span></span> |
   | <span data-ttu-id="973dc-142">2</span><span class="sxs-lookup"><span data-stu-id="973dc-142">2</span></span> |<span data-ttu-id="973dc-143">Сбой вентилятора</span><span class="sxs-lookup"><span data-stu-id="973dc-143">Fan failure</span></span> |
   | <span data-ttu-id="973dc-144">3</span><span class="sxs-lookup"><span data-stu-id="973dc-144">3</span></span> |<span data-ttu-id="973dc-145">Сбой аккумулятора</span><span class="sxs-lookup"><span data-stu-id="973dc-145">Battery fault</span></span> |
   | <span data-ttu-id="973dc-146">4.</span><span class="sxs-lookup"><span data-stu-id="973dc-146">4</span></span> |<span data-ttu-id="973dc-147">БПО исправен</span><span class="sxs-lookup"><span data-stu-id="973dc-147">PCM OK</span></span> |
   | <span data-ttu-id="973dc-148">5</span><span class="sxs-lookup"><span data-stu-id="973dc-148">5</span></span> |<span data-ttu-id="973dc-149">Сбой постоянного напряжения</span><span class="sxs-lookup"><span data-stu-id="973dc-149">DC power failure</span></span> |
   | <span data-ttu-id="973dc-150">6</span><span class="sxs-lookup"><span data-stu-id="973dc-150">6</span></span> |<span data-ttu-id="973dc-151">Батарея работоспособна</span><span class="sxs-lookup"><span data-stu-id="973dc-151">Battery healthy</span></span> |
3. <span data-ttu-id="973dc-152">hello tooremove PCM с неисправным аккумулятором, следуйте указаниям hello [удаления PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="973dc-152">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="973dc-153">Удален PCM приветствия, точности прогнозов и поворот hello батареи модуль обработки вверх, как указано в следующий рисунок hello и выдвинуть tooremove hello батареи.</span><span class="sxs-lookup"><span data-stu-id="973dc-153">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![Снятие батареи БПО](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="973dc-155">**Рис. 3** удаление hello батареи из hello PCM</span><span class="sxs-lookup"><span data-stu-id="973dc-155">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="973dc-156">Поместите hello модуль в упаковку сменного блока hello.</span><span class="sxs-lookup"><span data-stu-id="973dc-156">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="973dc-157">Возвращает tooMicrosoft hello неисправный блок для соответствующего обслуживания и обработки.</span><span class="sxs-lookup"><span data-stu-id="973dc-157">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="973dc-158">Установка нового модуля резервного аккумулятора</span><span class="sxs-lookup"><span data-stu-id="973dc-158">Install a new backup battery module</span></span>
<span data-ttu-id="973dc-159">Выполните следующие шаги tooinstall hello замены аккумуляторного модуля в hello PCM в hello основного корпуса устройства StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="973dc-159">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="973dc-160">tooinstall hello аккумуляторного модуля</span><span class="sxs-lookup"><span data-stu-id="973dc-160">tooinstall hello battery module</span></span>
1. <span data-ttu-id="973dc-161">Поместите hello резервного аккумуляторного модуля в правильное расположение hello в hello PCM.</span><span class="sxs-lookup"><span data-stu-id="973dc-161">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="973dc-162">Нажмите клавишу вниз hello аккумуляторного модуля обработки всех hello способом tooseat hello соединителя.</span><span class="sxs-lookup"><span data-stu-id="973dc-162">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="973dc-163">Замените hello PCM в основном корпусе hello, следуя правилам hello в [замена модуля питания и охлаждения на устройстве StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="973dc-163">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="973dc-164">После завершения замены hello go слишком**устройств** > **обслуживания** > **состояние оборудования** в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="973dc-164">After hello replacement is complete, go too**Devices** > **Maintenance** > **Hardware Status** in hello Azure classic portal.</span></span> <span data-ttu-id="973dc-165">Проверьте состояние hello toomake батареи hello убедиться в успешности установки hello.</span><span class="sxs-lookup"><span data-stu-id="973dc-165">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="973dc-166">Зеленый индикатор указывает, что hello аккумулятор исправен.</span><span class="sxs-lookup"><span data-stu-id="973dc-166">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="973dc-167">Ведение hello резервного аккумуляторного модуля</span><span class="sxs-lookup"><span data-stu-id="973dc-167">Maintain hello backup battery module</span></span>
<span data-ttu-id="973dc-168">В вашем устройстве StorSimple hello резервного аккумуляторного модуля предоставляет power toohello контроллера при отключении сетевого питания.</span><span class="sxs-lookup"><span data-stu-id="973dc-168">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="973dc-169">Она позволяет hello StorSimple устройство toosave критически важных данных предыдущих tooshutting вниз контролируемым образом.</span><span class="sxs-lookup"><span data-stu-id="973dc-169">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="973dc-170">С hello PCM две полностью заряженной батареи hello системы может обрабатывать два последовательных отключения питания.</span><span class="sxs-lookup"><span data-stu-id="973dc-170">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="973dc-171">В hello классический портал Azure, hello **состояние оборудования** на hello **обслуживания** страницы указывает неисправности аккумуляторов hello или hello окончания срок приближается.</span><span class="sxs-lookup"><span data-stu-id="973dc-171">In hello Azure classic portal, hello **Hardware Status** on hello **Maintenance** page indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="973dc-172">Указывает состояние батареи Hello **батарея в PCM 0** или **аккумулятор в PCM 1** под **общие компоненты**.</span><span class="sxs-lookup"><span data-stu-id="973dc-172">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="973dc-173">На этой странице отображается состояние **Ограничено** при приближении окончания срока службы и **Неисправен** при окончании срока службы.</span><span class="sxs-lookup"><span data-stu-id="973dc-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="973dc-174">можно сообщить Hello батареи **сбой** при достаточно toobe взимается плата.</span><span class="sxs-lookup"><span data-stu-id="973dc-174">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>
> 
> 

<span data-ttu-id="973dc-175">Если hello **ДЕГРАДАЦИЯ** отображается состояние, мы рекомендуем hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="973dc-175">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="973dc-176">Hello системы может испытывать последних отключения питания или hello батарей может выполняться периодическое обслуживание.</span><span class="sxs-lookup"><span data-stu-id="973dc-176">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="973dc-177">Наблюдать за системы hello 12 часов, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="973dc-177">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="973dc-178">Если по-прежнему находится в состоянии hello **ДЕГРАДАЦИЯ** после 12 часов power tooAC постоянного соединения с hello контроллеров и PCM под управлением, затем hello батарей должна toobe замены.</span><span class="sxs-lookup"><span data-stu-id="973dc-178">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="973dc-179">Для получения нового модуля резервного аккумулятора [обратитесь в службу поддержки Microsoft](storsimple-contact-microsoft-support.md) .</span><span class="sxs-lookup"><span data-stu-id="973dc-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="973dc-180">Если переходит в состояние hello ОК через 12 часов, hello аккумулятор Исправен и его потребуется лишь расходов на обслуживание.</span><span class="sxs-lookup"><span data-stu-id="973dc-180">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="973dc-181">Если не было связанного потери питания и hello PCM включен и подключен tooAC power, батареи hello должен toobe замены.</span><span class="sxs-lookup"><span data-stu-id="973dc-181">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="973dc-182">[Обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md) tooorder сменного резервного аккумуляторного модуля.</span><span class="sxs-lookup"><span data-stu-id="973dc-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="973dc-183">Уничтожьте hello сбой аккумулятора, в соответствии с toonational и язык правила.</span><span class="sxs-lookup"><span data-stu-id="973dc-183">Dispose of hello failed battery according toonational and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="973dc-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="973dc-184">Next steps</span></span>
<span data-ttu-id="973dc-185">Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="973dc-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

