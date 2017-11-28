---
title: "aaaUpdate устройства StorSimple | Документы Microsoft"
description: "Объясняет, как обновить toouse hello StorSimple tooinstall функция регулярных и обновления в режиме обслуживания и исправления."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="b1cba-103">Обновление устройства StorSimple серии 8000</span><span class="sxs-lookup"><span data-stu-id="b1cba-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="b1cba-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b1cba-104">Overview</span></span>
<span data-ttu-id="b1cba-105">Hello StorSimple обновления предоставляет следующие возможности tooeasily актуальность устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b1cba-105">hello StorSimple updates features allow you tooeasily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="b1cba-106">В зависимости от типа hello обновления можно применить обновления toohello устройства hello классический портал Azure или с помощью интерфейса Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="b1cba-106">Depending on hello update type, you can apply updates toohello device via hello Azure classic portal or via hello Windows PowerShell interface.</span></span> <span data-ttu-id="b1cba-107">Этот учебник описывает типы обновления hello и как tooinstall каждого из них.</span><span class="sxs-lookup"><span data-stu-id="b1cba-107">This tutorial describes hello update types and how tooinstall each of them.</span></span>

<span data-ttu-id="b1cba-108">Можно применить два вида обновлений устройств:</span><span class="sxs-lookup"><span data-stu-id="b1cba-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="b1cba-109">Обычные обновления.</span><span class="sxs-lookup"><span data-stu-id="b1cba-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="b1cba-110">Обновления режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b1cba-110">Maintenance mode updates</span></span>

<span data-ttu-id="b1cba-111">Можно устанавливать регулярные обновления через hello классический портал Azure или Windows PowerShell; Тем не менее необходимо использовать Windows PowerShell tooinstall обновления в режиме обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b1cba-111">You can install regular updates via hello Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell tooinstall Maintenance mode updates.</span></span> 

<span data-ttu-id="b1cba-112">Каждый тип обновления будет описан отдельно ниже.</span><span class="sxs-lookup"><span data-stu-id="b1cba-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="b1cba-113">Обычные обновления</span><span class="sxs-lookup"><span data-stu-id="b1cba-113">Regular updates</span></span>
<span data-ttu-id="b1cba-114">Регулярные обновления, не нарушающие работу обновления, которые можно установить при hello устройство находится в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="b1cba-114">Regular updates are non-disruptive updates that can be installed when hello device is in Normal mode.</span></span> <span data-ttu-id="b1cba-115">Эти обновления применяются через контроллера устройства tooeach веб-сайт центра обновления Майкрософт hello.</span><span class="sxs-lookup"><span data-stu-id="b1cba-115">These updates are applied through hello Microsoft Update website tooeach device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b1cba-116">Отработка отказа контроллера может возникнуть во время процесса обновления hello.</span><span class="sxs-lookup"><span data-stu-id="b1cba-116">A controller failover may occur during hello update process.</span></span> <span data-ttu-id="b1cba-117">Однако это не повлияет на доступность системы или операции.</span><span class="sxs-lookup"><span data-stu-id="b1cba-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="b1cba-118">Дополнительные сведения о способах tooinstall регулярные обновления через hello классического портала Azure см. в разделе [Установка регулярных обновлений через hello классический портал Azure](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="b1cba-118">For details on how tooinstall regular updates via hello Azure classic portal, see [Install regular updates via hello Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="b1cba-119">Обычные обновления можно также установить через Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b1cba-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b1cba-120">Дополнительные сведения см. в статье [Установка обычных обновлений через Windows PowerShell для StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="b1cba-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="b1cba-121">Обновления режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b1cba-121">Maintenance mode updates</span></span>
<span data-ttu-id="b1cba-122">Обновления режима обслуживания прерывают работу. К ним относятся, например, обновления встроенного ПО дисков.</span><span class="sxs-lookup"><span data-stu-id="b1cba-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="b1cba-123">Эти обновления требуют toobe устройства hello перевести в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b1cba-123">These updates require hello device toobe put into Maintenance mode.</span></span> <span data-ttu-id="b1cba-124">Дополнительные сведения см. в разделе [Шаг 2. Вход в режим обслуживания](#step2).</span><span class="sxs-lookup"><span data-stu-id="b1cba-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="b1cba-125">Нельзя использовать hello Azure классического портала tooinstall обновления в режиме обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b1cba-125">You cannot use hello Azure classic portal tooinstall Maintenance mode updates.</span></span> <span data-ttu-id="b1cba-126">Вместо этого необходимо использовать Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b1cba-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="b1cba-127">Дополнительные сведения о способах обновления tooinstall режима обслуживания см. в разделе [обновления в режиме обслуживания, установите через Windows PowerShell для StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="b1cba-127">For details on how tooinstall Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1cba-128">Режим обслуживания, обновления, необходимо применять отдельно tooeach контроллера.</span><span class="sxs-lookup"><span data-stu-id="b1cba-128">Maintenance mode updates must be applied separately tooeach controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a><span data-ttu-id="b1cba-129">Установка регулярных обновлений через hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="b1cba-129">Install regular updates via hello Azure classic portal</span></span>
<span data-ttu-id="b1cba-130">Можно использовать устройство StorSimple tooyour обновления Azure классического портала tooapply hello.</span><span class="sxs-lookup"><span data-stu-id="b1cba-130">You can use hello Azure classic portal tooapply updates tooyour StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="b1cba-131">Установка обычных обновлений через Windows PowerShell для StorSimple</span><span class="sxs-lookup"><span data-stu-id="b1cba-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="b1cba-132">Кроме того можно использовать Windows PowerShell для StorSimple tooapply (обычный режим) регулярных обновлений.</span><span class="sxs-lookup"><span data-stu-id="b1cba-132">Alternatively, you can use Windows PowerShell for StorSimple tooapply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1cba-133">Несмотря на то, что можно устанавливать регулярные обновления, с помощью Windows PowerShell для StorSimple, настоятельно рекомендуется установить регулярные обновления через hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b1cba-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through hello Azure classic portal.</span></span> <span data-ttu-id="b1cba-134">Предварительная проверка, начиная с обновлением 1, будет выполнено предыдущих tooinstalling обновлений с портала hello.</span><span class="sxs-lookup"><span data-stu-id="b1cba-134">Beginning with Update 1, pre-checks will be performed prior tooinstalling updates from hello portal.</span></span> <span data-ttu-id="b1cba-135">Эти предварительные проверки устраняют сбои и обеспечивают более стабильную работу.</span><span class="sxs-lookup"><span data-stu-id="b1cba-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="b1cba-136">Установка обновлений режима обслуживания через Windows PowerShell для StorSimple</span><span class="sxs-lookup"><span data-stu-id="b1cba-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="b1cba-137">Вы используете Windows PowerShell для StorSimple режим обслуживания tooapply обновлений устройства StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="b1cba-137">You use Windows PowerShell for StorSimple tooapply Maintenance mode updates tooyour StorSimple device.</span></span> <span data-ttu-id="b1cba-138">В этом режиме приостанавливаются все запросы ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="b1cba-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="b1cba-139">Службы, такие как энергонезависимой ОЗУ (NVRAM) или служба кластеров hello также останавливаются.</span><span class="sxs-lookup"><span data-stu-id="b1cba-139">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="b1cba-140">Оба контроллера перезагружаются при входе и выходе из этого режима.</span><span class="sxs-lookup"><span data-stu-id="b1cba-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="b1cba-141">При выходе из этого режима все службы hello будет возобновлена и должен быть работоспособное.</span><span class="sxs-lookup"><span data-stu-id="b1cba-141">When you exit this mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="b1cba-142">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b1cba-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="b1cba-143">Если вам требуется tooapply обновления в режиме обслуживания, вы получите оповещение через hello классический портал Azure о наличии обновлений, которые должны быть установлены.</span><span class="sxs-lookup"><span data-stu-id="b1cba-143">If you need tooapply Maintenance mode updates, you will receive an alert through hello Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="b1cba-144">Оповещения содержат инструкции по использованию Windows PowerShell для StorSimple tooinstall hello обновлений.</span><span class="sxs-lookup"><span data-stu-id="b1cba-144">This alert will include instructions for using Windows PowerShell for StorSimple tooinstall hello updates.</span></span> <span data-ttu-id="b1cba-145">После установки устройства используйте hello же процедура toochange hello устройства tooRegular режим.</span><span class="sxs-lookup"><span data-stu-id="b1cba-145">After you update your device, use hello same procedure toochange hello device tooRegular mode.</span></span> <span data-ttu-id="b1cba-146">Пошаговые инструкции см. в разделе [Шаг 4. Выход из режима обслуживания](#step4).</span><span class="sxs-lookup"><span data-stu-id="b1cba-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b1cba-147">Перед переходом в режим обслуживания, убедитесь, что оба контроллера устройства находятся в работоспособном состоянии, проверив hello **состояние оборудования** на hello **обслуживания** страницу приветствия классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b1cba-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="b1cba-148">Если hello контроллер не работает, обратитесь в службу поддержки Майкрософт за дальнейшими действиями hello.</span><span class="sxs-lookup"><span data-stu-id="b1cba-148">If hello controller is not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="b1cba-149">Дополнительные сведения см. в tooContact технической поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b1cba-149">For more information, go tooContact Microsoft Support.</span></span> 
> * <span data-ttu-id="b1cba-150">При работе в режиме обслуживания необходимо tooapply сначала hello обновления на одном контроллере, и затем на hello другой контроллер.</span><span class="sxs-lookup"><span data-stu-id="b1cba-150">When you are in Maintenance mode, you need tooapply hello update first on one controller and then on hello other controller.</span></span>
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a><span data-ttu-id="b1cba-151">Шаг 1: Подключение toohello последовательной консоли<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="b1cba-151">Step 1: Connect toohello serial console <a name="step1"></span></span>
<span data-ttu-id="b1cba-152">Во-первых работать с приложением, такие как PuTTY tooaccess hello последовательной консоли.</span><span class="sxs-lookup"><span data-stu-id="b1cba-152">First, use an application such as PuTTY tooaccess hello serial console.</span></span> <span data-ttu-id="b1cba-153">Hello следующая процедура описывает, как toouse PuTTY tooconnect toohello последовательной консоли.</span><span class="sxs-lookup"><span data-stu-id="b1cba-153">hello following procedure explains how toouse PuTTY tooconnect toohello serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="b1cba-154">Шаг 2. Вход в режим обслуживания <a name="step2"></span><span class="sxs-lookup"><span data-stu-id="b1cba-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="b1cba-155">После подключения консоли toohello проверить наличие обновлений tooinstall и введите tooinstall режим обслуживания их.</span><span class="sxs-lookup"><span data-stu-id="b1cba-155">After you connect toohello console, determine whether there are updates tooinstall, and enter Maintenance mode tooinstall them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="b1cba-156">Шаг 3. Установка обновлений <a name="step3"></span><span class="sxs-lookup"><span data-stu-id="b1cba-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="b1cba-157">Затем установите обновления.</span><span class="sxs-lookup"><span data-stu-id="b1cba-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="b1cba-158">Шаг 4. Выход из режима обслуживания <a name="step4"></span><span class="sxs-lookup"><span data-stu-id="b1cba-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="b1cba-159">В конце выйдите из режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b1cba-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="b1cba-160">Установка исправлений через Windows PowerShell или StorSimple</span><span class="sxs-lookup"><span data-stu-id="b1cba-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="b1cba-161">В отличие от обновлений для Microsoft Azure StorSimple, исправления устанавливаются из общей папки.</span><span class="sxs-lookup"><span data-stu-id="b1cba-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="b1cba-162">Как и в случае обновлений, существует два вида исправлений:</span><span class="sxs-lookup"><span data-stu-id="b1cba-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="b1cba-163">Обычные исправления.</span><span class="sxs-lookup"><span data-stu-id="b1cba-163">Regular hotfixes</span></span> 
* <span data-ttu-id="b1cba-164">Исправления режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b1cba-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="b1cba-165">Hello следующих процедурах объясняется, как toouse Windows PowerShell для StorSimple tooinstall регулярных и исправлений в режиме обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b1cba-165">hello following procedures explain how toouse Windows PowerShell for StorSimple tooinstall regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a><span data-ttu-id="b1cba-166">Что произойдет, tooupdates при выполнении фабрику для сброса устройства hello?</span><span class="sxs-lookup"><span data-stu-id="b1cba-166">What happens tooupdates if you perform a factory reset of hello device?</span></span>
<span data-ttu-id="b1cba-167">Если устройство является toofactory Сброс параметров, все обновления hello будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="b1cba-167">If a device is reset toofactory settings, then all hello updates are lost.</span></span> <span data-ttu-id="b1cba-168">После регистрации и настройки hello Восстановление заводских настроек устройства необходимо будет устанавливать обновления toomanually через hello классический портал Azure и (или) Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b1cba-168">After hello factory-reset device is registered and configured, you will need toomanually install updates through hello Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b1cba-169">Дополнительные сведения о Восстановление заводских настроек см. в разделе [сбросить параметры по умолчанию hello устройства toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="b1cba-169">For more information about factory reset, see [Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1cba-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b1cba-170">Next steps</span></span>
* <span data-ttu-id="b1cba-171">Дополнительные сведения о [устройства StorSimple с помощью Windows PowerShell для StorSimple tooadminister](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="b1cba-171">Learn more about [using Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="b1cba-172">Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="b1cba-172">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

