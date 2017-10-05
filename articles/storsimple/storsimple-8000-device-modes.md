---
title: "Изменение режима устройства StorSimple | Документация Майкрософт"
description: "В статье описываются режимы устройства StorSimple и объясняется, как изменить режим устройства StorSimple с помощью Windows PowerShell."
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
ms.openlocfilehash: dd160ede1189b0de544c8cf5db3b13228d212419
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-device-mode-on-your-storsimple-device"></a><span data-ttu-id="c9fbb-103">Переключение режима устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="c9fbb-103">Change the device mode on your StorSimple device</span></span>

<span data-ttu-id="c9fbb-104">В этой статье представлено краткое описание различных режимов, в которых могут работать устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="c9fbb-105">Устройство StorSimple может работать в трех режимах: нормальном, обслуживания и восстановления.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="c9fbb-106">После прочтения этой статьи вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="c9fbb-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="c9fbb-107">о режимах устройств StorSimple;</span><span class="sxs-lookup"><span data-stu-id="c9fbb-107">What the StorSimple device modes are</span></span>
* <span data-ttu-id="c9fbb-108">о том, как выяснить, в каком режиме находится устройство StorSimple;</span><span class="sxs-lookup"><span data-stu-id="c9fbb-108">How to figure out which mode the StorSimple device is in</span></span>
* <span data-ttu-id="c9fbb-109">о том, как переключиться из нормального режима в режим обслуживания и *наоборот*</span><span class="sxs-lookup"><span data-stu-id="c9fbb-109">How to change from normal to maintenance mode and *vice versa*</span></span>

<span data-ttu-id="c9fbb-110">Эти задачи можно выполнить только через интерфейс Windows PowerShell устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="c9fbb-111">Режимы устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="c9fbb-111">About StorSimple device modes</span></span>

<span data-ttu-id="c9fbb-112">Устройство StorSimple может работать в нормальном режиме, режиме обслуживания и режиме восстановления.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="c9fbb-113">Ниже кратко описан каждый из этих режимов.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="c9fbb-114">Нормальный режим</span><span class="sxs-lookup"><span data-stu-id="c9fbb-114">Normal mode</span></span>

<span data-ttu-id="c9fbb-115">Это нормальный рабочий режим полностью настроенного устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="c9fbb-116">По умолчанию устройство должно находиться в нормальном режиме.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="c9fbb-117">Режим обслуживания</span><span class="sxs-lookup"><span data-stu-id="c9fbb-117">Maintenance mode</span></span>

<span data-ttu-id="c9fbb-118">Иногда может потребоваться перевести устройство StorSimple в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span></span> <span data-ttu-id="c9fbb-119">Этот режим позволяет выполнять обслуживание устройства и устанавливать критические обновления, например обновления встроенного ПО дисков.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span></span>

<span data-ttu-id="c9fbb-120">Перевести систему в режим обслуживания можно только через Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="c9fbb-121">В этом режиме приостанавливаются все запросы ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="c9fbb-122">Также останавливаются некоторые другие службы, например энергонезависимое ОЗУ (NVRAM) или служба кластеров.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="c9fbb-123">При входе в этот режим и выходе из него перезапускаются оба контроллера.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-123">Both the controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="c9fbb-124">При выходе из режима обслуживания все службы возобновляют работу и должны работать без ошибок.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="c9fbb-125">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="c9fbb-126">**Режим обслуживания поддерживается только на устройстве, которое работает корректно. Он не поддерживается на устройстве, на котором не работают один или оба контроллера.**</span><span class="sxs-lookup"><span data-stu-id="c9fbb-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="c9fbb-127">Режим восстановления</span><span class="sxs-lookup"><span data-stu-id="c9fbb-127">Recovery mode</span></span>

<span data-ttu-id="c9fbb-128">Режим восстановления можно описать как "безопасный режим Windows с поддержкой сети".</span><span class="sxs-lookup"><span data-stu-id="c9fbb-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="c9fbb-129">Режим восстановления включает взаимодействие со службой поддержки Майкрософт, сотрудники которой выполняют диагностику системы.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span></span> <span data-ttu-id="c9fbb-130">Основная цель режима восстановления — получение системных журналов.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-130">The primary goal of recovery mode is to retrieve the system logs.</span></span>

<span data-ttu-id="c9fbb-131">Если система переходит в режим восстановления, вы должны обратиться в службу технической поддержки Майкрософт за дальнейшими действиями.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="c9fbb-132">Для получения дополнительных сведений [обратитесь в службу поддержки Майкрософт](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="c9fbb-132">For more information, go to [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c9fbb-133">**Переключить устройство в режим восстановления нельзя. Если устройство находится в неисправном состоянии, то в режиме восстановления будет предпринята попытка переключить его в то состояние, в котором его смогут изучить специалисты технической поддержки Майкрософт.**</span><span class="sxs-lookup"><span data-stu-id="c9fbb-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="c9fbb-134">Определение режима устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="c9fbb-134">Determine StorSimple device mode</span></span>

#### <a name="to-determine-the-current-device-mode"></a><span data-ttu-id="c9fbb-135">Порядок определения текущего режима устройства</span><span class="sxs-lookup"><span data-stu-id="c9fbb-135">To determine the current device mode</span></span>

1. <span data-ttu-id="c9fbb-136">Войдите в последовательную консоль устройства, выполнив действия, описанные в разделе [Использование PuTTY для подключения к последовательной консоли устройства](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="c9fbb-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="c9fbb-137">Просмотрите заглавное сообщение в меню последовательной консоли устройства.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-137">Look at the banner message in the serial console menu of the device.</span></span> <span data-ttu-id="c9fbb-138">Это сообщение явно указывает, в каком режиме находится устройство: обслуживания или восстановления.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span></span> <span data-ttu-id="c9fbb-139">Если сообщение не содержит никакой специальной информации, относящейся к режиму работы системы, то устройство находится в нормальном режиме.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span></span>

## <a name="change-the-storsimple-device-mode"></a><span data-ttu-id="c9fbb-140">Изменение режима устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="c9fbb-140">Change the StorSimple device mode</span></span>

<span data-ttu-id="c9fbb-141">Устройство можно переключить в режим обслуживания (из нормального режима) для проведения обслуживания или установки обновлений режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="c9fbb-142">Для ввода в режим обслуживания или выхода из него выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-142">Perform the following procedures to enter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9fbb-143">Перед переключением в режим обслуживания убедитесь, что оба контроллера устройства работоспособны. Для этого откройте меню **Параметры устройства > Работоспособность оборудования** своего устройства на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Device settings > Hardware health** for your device in the Azure portal.</span></span> <span data-ttu-id="c9fbb-144">Если один или оба контроллера неработоспособны, обратитесь в службу поддержки Майкрософт для получения дальнейших указаний.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="c9fbb-145">Для получения дополнительных сведений [обратитесь в службу поддержки Майкрософт](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="c9fbb-145">For more information, go to [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="c9fbb-146">Переход в режим обслуживания</span><span class="sxs-lookup"><span data-stu-id="c9fbb-146">To enter maintenance mode</span></span>

1. <span data-ttu-id="c9fbb-147">Войдите в последовательную консоль устройства, выполнив действия, описанные в разделе [Использование PuTTY для подключения к последовательной консоли устройства](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="c9fbb-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="c9fbb-148">В меню последовательной консоли выберите вариант 1 **Войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-148">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="c9fbb-149">При выводе запроса введите **пароль администратора устройства**.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-149">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="c9fbb-150">Пароль по умолчанию: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-150">The default password is: `Password1`.</span></span>
3. <span data-ttu-id="c9fbb-151">В командной строке выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c9fbb-151">At the command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="c9fbb-152">Отобразится предупреждающее сообщение о том, что режим обслуживания будет мешать работе всех запросов ввода-вывода и приведет к разрыву подключения к порталу Azure, в результате чего появится запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="c9fbb-153">Нажмите клавишу **Y** , чтобы перейти в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-153">Type **Y** to enter maintenance mode.</span></span>
5. <span data-ttu-id="c9fbb-154">Оба контроллера будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-154">Both controllers will restart.</span></span> <span data-ttu-id="c9fbb-155">После завершения перезапуска баннер последовательной консоли отобразит сообщение о том, что устройство находится в режиме обслуживания.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-155">When the restart is complete, the serial console banner will indicate that the device is in maintenance mode.</span></span> <span data-ttu-id="c9fbb-156">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-156">A sample output is shown below.</span></span>

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="to-exit-maintenance-mode"></a><span data-ttu-id="c9fbb-157">Выход из режима обслуживания</span><span class="sxs-lookup"><span data-stu-id="c9fbb-157">To exit maintenance mode</span></span>

1. <span data-ttu-id="c9fbb-158">Войдите в последовательную консоль устройства.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-158">Log on to the device serial console.</span></span> <span data-ttu-id="c9fbb-159">Проверьте, находится ли устройство в режиме обслуживания, с помощью заглавного сообщения.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-159">Verify from the banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="c9fbb-160">В командной строке выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c9fbb-160">At the command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="c9fbb-161">Отобразится сообщение с предупреждением и сообщение с запросом на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="c9fbb-162">Нажмите клавишу **Y** , чтобы выйти из режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-162">Type **Y** to exit maintenance mode.</span></span>
4. <span data-ttu-id="c9fbb-163">Оба контроллера будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-163">Both controllers will restart.</span></span> <span data-ttu-id="c9fbb-164">После завершения перезапуска баннер последовательной консоли отобразит сообщение о том, что устройство находится в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-164">When the restart is complete, the serial console banner indicates that the device is in normal mode.</span></span> <span data-ttu-id="c9fbb-165">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-165">A sample output is shown below.</span></span>

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure to install on each controller could result in data corruption. Exiting maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to exit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a><span data-ttu-id="c9fbb-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9fbb-166">Next steps</span></span>

<span data-ttu-id="c9fbb-167">Узнайте, как [применить обновления нормального режима и режима обслуживания](storsimple-update-device.md) к своему устройству StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c9fbb-167">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

