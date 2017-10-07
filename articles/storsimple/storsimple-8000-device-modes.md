---
title: "режим устройства StorSimple aaaChange | Документы Microsoft"
description: "Описание режимов устройства StorSimple hello и как toouse Windows PowerShell для StorSimple toochange hello режим устройства."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="4c572-103">Изменение режима hello устройства на устройстве StorSimple</span><span class="sxs-lookup"><span data-stu-id="4c572-103">Change hello device mode on your StorSimple device</span></span>

<span data-ttu-id="4c572-104">В этой статье предоставляет краткое описание hello различные режимы, в которых могут работать устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4c572-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="4c572-105">Устройство StorSimple может работать в трех режимах: нормальном, обслуживания и восстановления.</span><span class="sxs-lookup"><span data-stu-id="4c572-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="4c572-106">После прочтения этой статьи вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="4c572-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="4c572-107">Каковы hello режимов устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="4c572-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="4c572-108">Как toofigure ожидания режима hello устройство StorSimple находится в</span><span class="sxs-lookup"><span data-stu-id="4c572-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="4c572-109">Как toochange из toomaintenance в обычном режиме и *наоборот;*</span><span class="sxs-lookup"><span data-stu-id="4c572-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="4c572-110">Hello выше задач управления может выполняться только через интерфейс Windows PowerShell hello устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4c572-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="4c572-111">Режимы устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="4c572-111">About StorSimple device modes</span></span>

<span data-ttu-id="4c572-112">Устройство StorSimple может работать в нормальном режиме, режиме обслуживания и режиме восстановления.</span><span class="sxs-lookup"><span data-stu-id="4c572-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="4c572-113">Ниже кратко описан каждый из этих режимов.</span><span class="sxs-lookup"><span data-stu-id="4c572-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="4c572-114">Нормальный режим</span><span class="sxs-lookup"><span data-stu-id="4c572-114">Normal mode</span></span>

<span data-ttu-id="4c572-115">Это определяется как hello обычный режим работы полностью настроенного устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4c572-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="4c572-116">По умолчанию устройство должно находиться в нормальном режиме.</span><span class="sxs-lookup"><span data-stu-id="4c572-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="4c572-117">Режим обслуживания</span><span class="sxs-lookup"><span data-stu-id="4c572-117">Maintenance mode</span></span>

<span data-ttu-id="4c572-118">Иногда hello устройство StorSimple может потребоваться toobe переведен в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="4c572-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="4c572-119">Этот режим позволяет tooperform обслуживания на устройстве hello и устанавливать обновления, например, связанных с ними toodisk встроенного по.</span><span class="sxs-lookup"><span data-stu-id="4c572-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="4c572-120">Можно поместить hello системы в режим обслуживания только через hello Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4c572-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="4c572-121">В этом режиме приостанавливаются все запросы ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="4c572-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="4c572-122">Службы, такие как энергонезависимой ОЗУ (NVRAM) или служба кластеров hello также останавливаются.</span><span class="sxs-lookup"><span data-stu-id="4c572-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="4c572-123">Оба контроллера hello перезапускаются, при входе или выходе из этого режима.</span><span class="sxs-lookup"><span data-stu-id="4c572-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="4c572-124">При выходе из режима обслуживания hello, все службы hello будет возобновлена и должен быть работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="4c572-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="4c572-125">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4c572-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="4c572-126">**Режим обслуживания поддерживается только на устройстве, которое работает корректно. Не поддерживается на устройстве, в котором одного или обоих контроллеров hello не работают.**</span><span class="sxs-lookup"><span data-stu-id="4c572-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="4c572-127">Режим восстановления</span><span class="sxs-lookup"><span data-stu-id="4c572-127">Recovery mode</span></span>

<span data-ttu-id="4c572-128">Режим восстановления можно описать как "безопасный режим Windows с поддержкой сети".</span><span class="sxs-lookup"><span data-stu-id="4c572-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="4c572-129">Режим восстановления использует службу поддержки Microsoft hello и позволяет tooperform диагностики в системе hello.</span><span class="sxs-lookup"><span data-stu-id="4c572-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="4c572-130">Основная цель режима восстановления Hello — tooretrieve hello системные журналы.</span><span class="sxs-lookup"><span data-stu-id="4c572-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="4c572-131">Если система переходит в режим восстановления, вы должны обратиться в службу технической поддержки Майкрософт за дальнейшими действиями.</span><span class="sxs-lookup"><span data-stu-id="4c572-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="4c572-132">Дополнительные сведения см. слишком[обратитесь в службу поддержки корпорации Майкрософт](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="4c572-132">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4c572-133">**Не удается разместить hello устройства в режиме восстановления. Если hello устройство находится в неисправном состоянии, режим восстановления пытается tooget hello устройство в состояние, в котором службу поддержки Microsoft смогут проанализировать его.**</span><span class="sxs-lookup"><span data-stu-id="4c572-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="4c572-134">Определение режима устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="4c572-134">Determine StorSimple device mode</span></span>

#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="4c572-135">текущий режим устройства toodetermine hello</span><span class="sxs-lookup"><span data-stu-id="4c572-135">toodetermine hello current device mode</span></span>

1. <span data-ttu-id="4c572-136">Войдите на последовательную консоль устройства toohello, следуя указаниям hello [последовательной консоли устройства toohello использование PuTTY tooconnect](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="4c572-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="4c572-137">Просмотрите сообщение hello баннер в hello меню последовательной консоли устройства hello.</span><span class="sxs-lookup"><span data-stu-id="4c572-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="4c572-138">Это сообщение явным образом указывает ли hello устройство находится в режиме обслуживания или восстановления.</span><span class="sxs-lookup"><span data-stu-id="4c572-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="4c572-139">Если сообщение hello не содержит никакой конкретной информации о режиме системы toohello, hello устройство находится в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="4c572-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="4c572-140">Изменение режима устройства StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="4c572-140">Change hello StorSimple device mode</span></span>

<span data-ttu-id="4c572-141">Можно поместить устройство StorSimple hello в процедур обслуживания tooperform режим (обычный режим) или установки обновлений режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="4c572-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="4c572-142">Выполните следующие процедуры tooenter или завершения режима обслуживания hello.</span><span class="sxs-lookup"><span data-stu-id="4c572-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c572-143">Перед переходом в режим обслуживания, убедитесь, что оба контроллера устройства находятся в работоспособном состоянии, обратившись к hello **параметры устройства > работоспособности оборудования** для вашего устройства в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4c572-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Device settings > Hardware health** for your device in hello Azure portal.</span></span> <span data-ttu-id="4c572-144">Если один или оба контроллера hello не находятся в работоспособном состоянии, обратитесь в службу поддержки Майкрософт hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="4c572-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="4c572-145">Дополнительные сведения см. слишком[обратитесь в службу поддержки корпорации Майкрософт](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="4c572-145">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="4c572-146">режим обслуживания tooenter</span><span class="sxs-lookup"><span data-stu-id="4c572-146">tooenter maintenance mode</span></span>

1. <span data-ttu-id="4c572-147">Войдите на последовательную консоль устройства toohello, следуя указаниям hello [последовательной консоли устройства toohello использование PuTTY tooconnect](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="4c572-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="4c572-148">В меню последовательной консоли hello, выберите параметр 1, **войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="4c572-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="4c572-149">При появлении запроса укажите hello **пароль администратора устройства**.</span><span class="sxs-lookup"><span data-stu-id="4c572-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="4c572-150">пароль по умолчанию Hello: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="4c572-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="4c572-151">Введите в командной строке hello</span><span class="sxs-lookup"><span data-stu-id="4c572-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="4c572-152">Вы увидите предупреждение о том, что режим обслуживания прервет все запросы ввода-вывода и разорвет toohello подключения hello портал Azure и будет приглашение для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="4c572-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="4c572-153">Тип **Y** tooenter режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="4c572-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="4c572-154">Оба контроллера будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="4c572-154">Both controllers will restart.</span></span> <span data-ttu-id="4c572-155">После завершения перезагрузки hello баннер hello последовательной консоли будет указать, что это hello устройство находится в режиме обслуживания.</span><span class="sxs-lookup"><span data-stu-id="4c572-155">When hello restart is complete, hello serial console banner will indicate that hello device is in maintenance mode.</span></span> <span data-ttu-id="4c572-156">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="4c572-156">A sample output is shown below.</span></span>

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="4c572-157">режим обслуживания tooexit</span><span class="sxs-lookup"><span data-stu-id="4c572-157">tooexit maintenance mode</span></span>

1. <span data-ttu-id="4c572-158">Войдите на последовательную консоль устройства toohello.</span><span class="sxs-lookup"><span data-stu-id="4c572-158">Log on toohello device serial console.</span></span> <span data-ttu-id="4c572-159">Проверьте из сообщения hello баннера, ваше устройство находится в режиме обслуживания.</span><span class="sxs-lookup"><span data-stu-id="4c572-159">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="4c572-160">Hello командной строки введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4c572-160">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="4c572-161">Отобразится сообщение с предупреждением и сообщение с запросом на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="4c572-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="4c572-162">Тип **Y** tooexit режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="4c572-162">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="4c572-163">Оба контроллера будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="4c572-163">Both controllers will restart.</span></span> <span data-ttu-id="4c572-164">После завершения перезагрузки hello баннер последовательной консоли hello указывает, что это hello устройство находится в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="4c572-164">When hello restart is complete, hello serial console banner indicates that hello device is in normal mode.</span></span> <span data-ttu-id="4c572-165">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="4c572-165">A sample output is shown below.</span></span>

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a><span data-ttu-id="4c572-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4c572-166">Next steps</span></span>

<span data-ttu-id="4c572-167">Узнайте, каким образом слишком[применить обновления в режиме обычный и обслуживания](storsimple-update-device.md) на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4c572-167">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

