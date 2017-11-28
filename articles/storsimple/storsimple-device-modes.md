---
title: "Изменение режима устройства StorSimple | Документация Майкрософт"
description: "В статье описываются режимы устройства StorSimple и объясняется, как изменить режим устройства StorSimple с помощью Windows PowerShell."
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
ms.openlocfilehash: 33c65bf2eecff3914f3227c76f7d638a4507e1f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-device-mode-on-your-storsimple-device"></a><span data-ttu-id="a42e9-103">Переключение режима устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="a42e9-103">Change the device mode on your StorSimple device</span></span>
<span data-ttu-id="a42e9-104">В этой статье представлено краткое описание различных режимов, в которых могут работать устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a42e9-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="a42e9-105">Устройство StorSimple может работать в трех режимах: нормальном, обслуживания и восстановления.</span><span class="sxs-lookup"><span data-stu-id="a42e9-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span> 

<span data-ttu-id="a42e9-106">После прочтения этой статьи вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="a42e9-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="a42e9-107">о режимах устройств StorSimple;</span><span class="sxs-lookup"><span data-stu-id="a42e9-107">What the StorSimple device modes are</span></span>
* <span data-ttu-id="a42e9-108">о том, как выяснить, в каком режиме находится устройство StorSimple;</span><span class="sxs-lookup"><span data-stu-id="a42e9-108">How to figure out which mode the StorSimple device is in</span></span>
* <span data-ttu-id="a42e9-109">о том, как переключиться из нормального режима в режим обслуживания и *наоборот*</span><span class="sxs-lookup"><span data-stu-id="a42e9-109">How to change from normal to maintenance mode and *vice versa*</span></span>

<span data-ttu-id="a42e9-110">Эти задачи можно выполнить только через интерфейс Windows PowerShell устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a42e9-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="a42e9-111">Режимы устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="a42e9-111">About StorSimple device modes</span></span>
<span data-ttu-id="a42e9-112">Устройство StorSimple может работать в нормальном режиме, режиме обслуживания и режиме восстановления.</span><span class="sxs-lookup"><span data-stu-id="a42e9-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="a42e9-113">Ниже кратко описан каждый из этих режимов.</span><span class="sxs-lookup"><span data-stu-id="a42e9-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="a42e9-114">Нормальный режим</span><span class="sxs-lookup"><span data-stu-id="a42e9-114">Normal mode</span></span>
<span data-ttu-id="a42e9-115">Это нормальный рабочий режим полностью настроенного устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a42e9-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="a42e9-116">По умолчанию устройство должно находиться в нормальном режиме.</span><span class="sxs-lookup"><span data-stu-id="a42e9-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="a42e9-117">Режим обслуживания</span><span class="sxs-lookup"><span data-stu-id="a42e9-117">Maintenance mode</span></span>
<span data-ttu-id="a42e9-118">Иногда может потребоваться перевести устройство StorSimple в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="a42e9-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span></span> <span data-ttu-id="a42e9-119">Этот режим позволяет выполнять обслуживание устройства и устанавливать критические обновления, например обновления встроенного ПО дисков.</span><span class="sxs-lookup"><span data-stu-id="a42e9-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span></span>

<span data-ttu-id="a42e9-120">Перевести систему в режим обслуживания можно только через Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a42e9-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="a42e9-121">В этом режиме приостанавливаются все запросы ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="a42e9-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="a42e9-122">Также останавливаются некоторые другие службы, например энергонезависимое ОЗУ (NVRAM) или служба кластеров.</span><span class="sxs-lookup"><span data-stu-id="a42e9-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="a42e9-123">При входе в этот режим и выходе из него перезапускаются оба контроллера.</span><span class="sxs-lookup"><span data-stu-id="a42e9-123">Both the controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="a42e9-124">При выходе из режима обслуживания все службы возобновляют работу и должны работать без ошибок.</span><span class="sxs-lookup"><span data-stu-id="a42e9-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="a42e9-125">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a42e9-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="a42e9-126">**Режим обслуживания поддерживается только на устройстве, которое работает корректно. Он не поддерживается на устройстве, на котором не работают один или оба контроллера.**
> </span><span class="sxs-lookup"><span data-stu-id="a42e9-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**
</span></span></br>
> 
> 

### <a name="recovery-mode"></a><span data-ttu-id="a42e9-127">Режим восстановления</span><span class="sxs-lookup"><span data-stu-id="a42e9-127">Recovery mode</span></span>
<span data-ttu-id="a42e9-128">Режим восстановления можно описать как "безопасный режим Windows с поддержкой сети".</span><span class="sxs-lookup"><span data-stu-id="a42e9-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="a42e9-129">Режим восстановления включает взаимодействие со службой поддержки Майкрософт, сотрудники которой выполняют диагностику системы.</span><span class="sxs-lookup"><span data-stu-id="a42e9-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span></span> <span data-ttu-id="a42e9-130">Основная цель режима восстановления — получение системных журналов.</span><span class="sxs-lookup"><span data-stu-id="a42e9-130">The primary goal of recovery mode is to retrieve the system logs.</span></span>

<span data-ttu-id="a42e9-131">Если система переходит в режим восстановления, вы должны обратиться в службу технической поддержки Майкрософт за дальнейшими действиями.</span><span class="sxs-lookup"><span data-stu-id="a42e9-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="a42e9-132">Для получения дополнительных сведений [обратитесь в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="a42e9-132">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a42e9-133">**Переключить устройство в режим восстановления нельзя. Если устройство находится в неисправном состоянии, то в режиме восстановления будет предпринята попытка переключить его в то состояние, в котором его смогут изучить специалисты технической поддержки Майкрософт.**</span><span class="sxs-lookup"><span data-stu-id="a42e9-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span></span>
> 
> 

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="a42e9-134">Определение режима устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="a42e9-134">Determine StorSimple device mode</span></span>
#### <a name="to-determine-the-current-device-mode"></a><span data-ttu-id="a42e9-135">Порядок определения текущего режима устройства</span><span class="sxs-lookup"><span data-stu-id="a42e9-135">To determine the current device mode</span></span>
1. <span data-ttu-id="a42e9-136">Войдите в последовательную консоль устройства, выполнив действия, описанные в разделе [Использование PuTTY для подключения к последовательной консоли устройства](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="a42e9-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="a42e9-137">Просмотрите заглавное сообщение в меню последовательной консоли устройства.</span><span class="sxs-lookup"><span data-stu-id="a42e9-137">Look at the banner message in the serial console menu of the device.</span></span> <span data-ttu-id="a42e9-138">Это сообщение явно указывает, в каком режиме находится устройство: обслуживания или восстановления.</span><span class="sxs-lookup"><span data-stu-id="a42e9-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span></span> <span data-ttu-id="a42e9-139">Если сообщение не содержит никакой специальной информации, относящейся к режиму работы системы, то устройство находится в нормальном режиме.</span><span class="sxs-lookup"><span data-stu-id="a42e9-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span></span>

## <a name="change-the-storsimple-device-mode"></a><span data-ttu-id="a42e9-140">Изменение режима устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="a42e9-140">Change the StorSimple device mode</span></span>
<span data-ttu-id="a42e9-141">Устройство можно переключить в режим обслуживания (из нормального режима) для проведения обслуживания или установки обновлений режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="a42e9-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="a42e9-142">Для ввода в режим обслуживания или выхода из него выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a42e9-142">Perform the following procedures to enter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a42e9-143">Перед переключением в режим обслуживания убедитесь, что оба контроллера устройства работоспособны, проверив **состояние оборудования** на странице **Обслуживание** классического портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a42e9-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="a42e9-144">Если один или оба контроллера неработоспособны, обратитесь в службу поддержки Майкрософт для получения дальнейших указаний.</span><span class="sxs-lookup"><span data-stu-id="a42e9-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="a42e9-145">Для получения дополнительных сведений [обратитесь в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="a42e9-145">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
> 
> 

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="a42e9-146">Переход в режим обслуживания</span><span class="sxs-lookup"><span data-stu-id="a42e9-146">To enter maintenance mode</span></span>
1. <span data-ttu-id="a42e9-147">Войдите в последовательную консоль устройства, выполнив действия, описанные в разделе [Использование PuTTY для подключения к последовательной консоли устройства](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="a42e9-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="a42e9-148">В меню последовательной консоли выберите вариант 1 **Войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="a42e9-148">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="a42e9-149">При выводе запроса введите **пароль администратора устройства**.</span><span class="sxs-lookup"><span data-stu-id="a42e9-149">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="a42e9-150">Пароль по умолчанию: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="a42e9-150">The default password is: `Password1`.</span></span>
3. <span data-ttu-id="a42e9-151">В командной строке выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a42e9-151">At the command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="a42e9-152">Отобразится предупреждение о том, что режим обслуживания будет мешать работе всех запросов ввода-вывода и приведет к разрыву подключения к классическом порталу Azure, в результате чего появится запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="a42e9-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="a42e9-153">Нажмите клавишу **Y** , чтобы перейти в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="a42e9-153">Type **Y** to enter maintenance mode.</span></span>
5. <span data-ttu-id="a42e9-154">Оба контроллера будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="a42e9-154">Both controllers will restart.</span></span> <span data-ttu-id="a42e9-155">После завершения перезапуска отобразится сообщение о том, что устройство находится в режиме обслуживания.</span><span class="sxs-lookup"><span data-stu-id="a42e9-155">When the restart is complete, another message will appear indicating that the device is in maintenance mode.</span></span>

#### <a name="to-exit-maintenance-mode"></a><span data-ttu-id="a42e9-156">Выход из режима обслуживания</span><span class="sxs-lookup"><span data-stu-id="a42e9-156">To exit maintenance mode</span></span>
1. <span data-ttu-id="a42e9-157">Войдите в последовательную консоль устройства.</span><span class="sxs-lookup"><span data-stu-id="a42e9-157">Log on to the device serial console.</span></span> <span data-ttu-id="a42e9-158">Проверьте, находится ли устройство в режиме обслуживания, с помощью заглавного сообщения.</span><span class="sxs-lookup"><span data-stu-id="a42e9-158">Verify from the banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="a42e9-159">В командной строке выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a42e9-159">At the command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="a42e9-160">Отобразится сообщение с предупреждением и сообщение с запросом на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="a42e9-160">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="a42e9-161">Нажмите клавишу **Y** , чтобы выйти из режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="a42e9-161">Type **Y** to exit maintenance mode.</span></span>
4. <span data-ttu-id="a42e9-162">Оба контроллера будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="a42e9-162">Both controllers will restart.</span></span> <span data-ttu-id="a42e9-163">После завершения перезапуска появится сообщение о том, что устройство находится в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="a42e9-163">When the restart is complete, another message will appear indicating that the device is in normal mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a42e9-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a42e9-164">Next steps</span></span>
<span data-ttu-id="a42e9-165">Узнайте, как [применить обновления нормального режима и режима обслуживания](storsimple-update-device.md) к своему устройству StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a42e9-165">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

