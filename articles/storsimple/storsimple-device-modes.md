---
title: "режим устройства StorSimple hello aaaChange | Документы Microsoft"
description: "Описание режимов устройства StorSimple hello и как toouse Windows PowerShell для StorSimple toochange hello режим устройства."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 299fd380a83bcd06780c97937f4064f0791b440d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="55b90-103">Изменение режима hello устройства на устройстве StorSimple</span><span class="sxs-lookup"><span data-stu-id="55b90-103">Change hello device mode on your StorSimple device</span></span>
<span data-ttu-id="55b90-104">В этой статье предоставляет краткое описание hello различные режимы, в которых могут работать устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="55b90-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="55b90-105">Устройство StorSimple может работать в трех режимах: нормальном, обслуживания и восстановления.</span><span class="sxs-lookup"><span data-stu-id="55b90-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span> 

<span data-ttu-id="55b90-106">После прочтения этой статьи вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="55b90-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="55b90-107">Каковы hello режимов устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="55b90-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="55b90-108">Как toofigure ожидания режима hello устройство StorSimple находится в</span><span class="sxs-lookup"><span data-stu-id="55b90-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="55b90-109">Как toochange из toomaintenance в обычном режиме и *наоборот;*</span><span class="sxs-lookup"><span data-stu-id="55b90-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="55b90-110">Hello выше задач управления может выполняться только через интерфейс Windows PowerShell hello устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="55b90-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="55b90-111">Режимы устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="55b90-111">About StorSimple device modes</span></span>
<span data-ttu-id="55b90-112">Устройство StorSimple может работать в нормальном режиме, режиме обслуживания и режиме восстановления.</span><span class="sxs-lookup"><span data-stu-id="55b90-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="55b90-113">Ниже кратко описан каждый из этих режимов.</span><span class="sxs-lookup"><span data-stu-id="55b90-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="55b90-114">Нормальный режим</span><span class="sxs-lookup"><span data-stu-id="55b90-114">Normal mode</span></span>
<span data-ttu-id="55b90-115">Это определяется как hello обычный режим работы полностью настроенного устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="55b90-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="55b90-116">По умолчанию устройство должно находиться в нормальном режиме.</span><span class="sxs-lookup"><span data-stu-id="55b90-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="55b90-117">Режим обслуживания</span><span class="sxs-lookup"><span data-stu-id="55b90-117">Maintenance mode</span></span>
<span data-ttu-id="55b90-118">Иногда hello устройство StorSimple может потребоваться toobe переведен в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="55b90-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="55b90-119">Этот режим позволяет tooperform обслуживания на устройстве hello и устанавливать обновления, например, связанных с ними toodisk встроенного по.</span><span class="sxs-lookup"><span data-stu-id="55b90-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="55b90-120">Можно поместить hello системы в режим обслуживания только через hello Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="55b90-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="55b90-121">В этом режиме приостанавливаются все запросы ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="55b90-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="55b90-122">Службы, такие как энергонезависимой ОЗУ (NVRAM) или служба кластеров hello также останавливаются.</span><span class="sxs-lookup"><span data-stu-id="55b90-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="55b90-123">Оба контроллера hello перезапускаются, при входе или выходе из этого режима.</span><span class="sxs-lookup"><span data-stu-id="55b90-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="55b90-124">При выходе из режима обслуживания hello, все службы hello будет возобновлена и должен быть работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="55b90-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="55b90-125">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="55b90-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="55b90-126">**Режим обслуживания поддерживается только на устройстве, которое работает корректно. Не поддерживается на устройстве, в котором одного или обоих контроллеров hello не работают.**
> </span><span class="sxs-lookup"><span data-stu-id="55b90-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**
</span></span></br>
> 
> 

### <a name="recovery-mode"></a><span data-ttu-id="55b90-127">Режим восстановления</span><span class="sxs-lookup"><span data-stu-id="55b90-127">Recovery mode</span></span>
<span data-ttu-id="55b90-128">Режим восстановления можно описать как "безопасный режим Windows с поддержкой сети".</span><span class="sxs-lookup"><span data-stu-id="55b90-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="55b90-129">Режим восстановления использует службу поддержки Microsoft hello и позволяет tooperform диагностики в системе hello.</span><span class="sxs-lookup"><span data-stu-id="55b90-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="55b90-130">Основная цель режима восстановления Hello — tooretrieve hello системные журналы.</span><span class="sxs-lookup"><span data-stu-id="55b90-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="55b90-131">Если система переходит в режим восстановления, вы должны обратиться в службу технической поддержки Майкрософт за дальнейшими действиями.</span><span class="sxs-lookup"><span data-stu-id="55b90-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="55b90-132">Дополнительные сведения см. слишком[обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="55b90-132">For more information, go too[Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="55b90-133">**Не удается разместить hello устройства в режиме восстановления. Если hello устройство находится в неисправном состоянии, режим восстановления пытается tooget hello устройство в состояние, в котором службу поддержки Microsoft смогут проанализировать его.**</span><span class="sxs-lookup"><span data-stu-id="55b90-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>
> 
> 

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="55b90-134">Определение режима устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="55b90-134">Determine StorSimple device mode</span></span>
#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="55b90-135">текущий режим устройства toodetermine hello</span><span class="sxs-lookup"><span data-stu-id="55b90-135">toodetermine hello current device mode</span></span>
1. <span data-ttu-id="55b90-136">Войдите на последовательную консоль устройства toohello, следуя указаниям hello [последовательной консоли устройства toohello использование PuTTY tooconnect](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="55b90-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="55b90-137">Просмотрите сообщение hello баннер в hello меню последовательной консоли устройства hello.</span><span class="sxs-lookup"><span data-stu-id="55b90-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="55b90-138">Это сообщение явным образом указывает ли hello устройство находится в режиме обслуживания или восстановления.</span><span class="sxs-lookup"><span data-stu-id="55b90-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="55b90-139">Если сообщение hello не содержит никакой конкретной информации о режиме системы toohello, hello устройство находится в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="55b90-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="55b90-140">Изменение режима устройства StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="55b90-140">Change hello StorSimple device mode</span></span>
<span data-ttu-id="55b90-141">Можно поместить устройство StorSimple hello в процедур обслуживания tooperform режим (обычный режим) или установки обновлений режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="55b90-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="55b90-142">Выполните следующие процедуры tooenter или завершения режима обслуживания hello.</span><span class="sxs-lookup"><span data-stu-id="55b90-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55b90-143">Перед переходом в режим обслуживания, убедитесь, что оба контроллера устройства находятся в работоспособном состоянии, обратившись к hello **состояние оборудования** на hello **обслуживания** страницу приветствия классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="55b90-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="55b90-144">Если один или оба контроллера hello не находятся в работоспособном состоянии, обратитесь в службу поддержки Майкрософт hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="55b90-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="55b90-145">Дополнительные сведения см. слишком[обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="55b90-145">For more information, go too[Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
> 
> 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="55b90-146">режим обслуживания tooenter</span><span class="sxs-lookup"><span data-stu-id="55b90-146">tooenter maintenance mode</span></span>
1. <span data-ttu-id="55b90-147">Войдите на последовательную консоль устройства toohello, следуя указаниям hello [последовательной консоли устройства toohello использование PuTTY tooconnect](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="55b90-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="55b90-148">В меню последовательной консоли hello, выберите параметр 1, **войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="55b90-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="55b90-149">При появлении запроса укажите hello **пароль администратора устройства**.</span><span class="sxs-lookup"><span data-stu-id="55b90-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="55b90-150">пароль по умолчанию Hello: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="55b90-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="55b90-151">Введите в командной строке hello</span><span class="sxs-lookup"><span data-stu-id="55b90-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="55b90-152">Появится предупреждающее сообщение о том, что режим обслуживания прервет все запросы ввода-вывода и разорвет подключение hello toohello классический портал Azure, а также будет приглашение для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="55b90-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="55b90-153">Тип **Y** tooenter режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="55b90-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="55b90-154">Оба контроллера будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="55b90-154">Both controllers will restart.</span></span> <span data-ttu-id="55b90-155">После завершения перезагрузки hello другое сообщение появится, указывающий, что это устройство hello находится в режиме обслуживания.</span><span class="sxs-lookup"><span data-stu-id="55b90-155">When hello restart is complete, another message will appear indicating that hello device is in maintenance mode.</span></span>

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="55b90-156">режим обслуживания tooexit</span><span class="sxs-lookup"><span data-stu-id="55b90-156">tooexit maintenance mode</span></span>
1. <span data-ttu-id="55b90-157">Войдите на последовательную консоль устройства toohello.</span><span class="sxs-lookup"><span data-stu-id="55b90-157">Log on toohello device serial console.</span></span> <span data-ttu-id="55b90-158">Проверьте из сообщения hello баннера, ваше устройство находится в режиме обслуживания.</span><span class="sxs-lookup"><span data-stu-id="55b90-158">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="55b90-159">Hello командной строки введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="55b90-159">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="55b90-160">Отобразится сообщение с предупреждением и сообщение с запросом на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="55b90-160">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="55b90-161">Тип **Y** tooexit режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="55b90-161">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="55b90-162">Оба контроллера будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="55b90-162">Both controllers will restart.</span></span> <span data-ttu-id="55b90-163">После завершения перезагрузки hello другое сообщение появится, указывающий, что это устройство hello находится в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="55b90-163">When hello restart is complete, another message will appear indicating that hello device is in normal mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55b90-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55b90-164">Next steps</span></span>
<span data-ttu-id="55b90-165">Узнайте, каким образом слишком[применить обновления в режиме обычный и обслуживания](storsimple-update-device.md) на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="55b90-165">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

