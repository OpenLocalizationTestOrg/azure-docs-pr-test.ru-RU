---
title: "aaaConnect удаленное устройство StorSimple tooyour | Документы Microsoft"
description: "Объясняет, как tooconfigure устройства для удаленного управления и как tooconnect tooWindows PowerShell для StorSimple через HTTP или HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="e7ca7-103">Удаленное подключение устройства серии StorSimple 8000 tooyour</span><span class="sxs-lookup"><span data-stu-id="e7ca7-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="e7ca7-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="e7ca7-104">Overview</span></span>
<span data-ttu-id="e7ca7-105">Можно использовать устройство StorSimple tooyour tooconnect удаленного взаимодействия Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-105">You can use Windows PowerShell remoting tooconnect tooyour StorSimple device.</span></span> <span data-ttu-id="e7ca7-106">При таком способе подключения меню не отображается.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="e7ca7-107">(Вы увидеть меню только в том случае, если вы используете hello последовательной консоли на устройстве tooconnect hello.) С помощью удаленного взаимодействия Windows PowerShell подключитесь tooa определенной среде выполнения.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="e7ca7-108">Можно также указать язык отображения приветствия.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-108">You can also specify hello display language.</span></span> 

<span data-ttu-id="e7ca7-109">Дополнительные сведения об использовании toomanage удаленного взаимодействия Windows PowerShell устройства go слишком[с помощью Windows PowerShell для StorSimple tooadminister устройства StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e7ca7-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="e7ca7-110">В этом учебнике описано как tooconfigure устройства для удаленного управления и затем как tooconnect tooWindows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="e7ca7-111">Можно использовать HTTP или HTTPS tooconnect через удаленное взаимодействие Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-111">You can use HTTP or HTTPS tooconnect via Windows PowerShell remoting.</span></span> <span data-ttu-id="e7ca7-112">Тем не менее, при определении как tooconnect tooWindows PowerShell для StorSimple, рассмотрим следующие hello:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following:</span></span> 

* <span data-ttu-id="e7ca7-113">Непосредственное подключение toohello последовательной консоли устройства защищено, но подключения последовательной консоли toohello через сетевые коммутаторы не.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="e7ca7-114">Тщательно hello угрозу безопасности при соединении через сетевые коммутаторы toohello последовательной консоли устройства.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span> 
* <span data-ttu-id="e7ca7-115">Подключение через сеанс HTTP является более безопасным, чем подключение через последовательную консоль hello hello сети.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="e7ca7-116">Несмотря на то, что это не самый безопасный метод hello, он допустим для надежных сетей.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="e7ca7-117">Hello наиболее безопасный и рекомендуемый параметр hello является подключение посредством сеанса HTTPS с самозаверяющим сертификатом.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="e7ca7-118">Можно удаленно подключиться toohello интерфейс Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="e7ca7-119">Однако устройства StorSimple tooyour удаленного доступа через интерфейс Windows PowerShell hello не включается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="e7ca7-120">Сначала необходимо tooenable удаленного управления на устройстве hello, а затем на hello клиента, который будет использоваться tooaccess устройства.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-120">You need tooenable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="e7ca7-121">Hello действия, описанные в этой статье были выполнены в системе узла под управлением Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="e7ca7-122">Подключение по протоколу HTTP</span><span class="sxs-lookup"><span data-stu-id="e7ca7-122">Connect through HTTP</span></span>
<span data-ttu-id="e7ca7-123">Подключение tooWindows PowerShell для StorSimple через сеанс HTTP является более безопасным, чем подключение через последовательную консоль устройства StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="e7ca7-124">Несмотря на то, что это не самый безопасный метод hello, он допустим для надежных сетей.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="e7ca7-125">Можно использовать hello классический портал Azure или hello последовательной консоли tooconfigure удаленного управления.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-125">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="e7ca7-126">Выберите один из следующих процедур hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="e7ca7-127">Использовать hello Azure классического портала tooenable удаленное управление по протоколу HTTP</span><span class="sxs-lookup"><span data-stu-id="e7ca7-127">Use hello Azure classic portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="e7ca7-128">Используйте hello последовательной консоли tooenable удаленное управление по протоколу HTTP</span><span class="sxs-lookup"><span data-stu-id="e7ca7-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="e7ca7-129">После включения удаленного управления, используйте hello, выполнив процедуру tooprepare hello клиента для удаленного подключения.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="e7ca7-130">Подготовка hello клиента для удаленного подключения</span><span class="sxs-lookup"><span data-stu-id="e7ca7-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="e7ca7-131">Использовать hello Azure классического портала tooenable удаленное управление по протоколу HTTP</span><span class="sxs-lookup"><span data-stu-id="e7ca7-131">Use hello Azure classic portal tooenable remote management over HTTP</span></span>
<span data-ttu-id="e7ca7-132">Выполните следующие шаги в hello Azure классического портала tooenable удаленное управление по протоколу HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-132">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a><span data-ttu-id="e7ca7-133">удаленное управление tooenable через hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="e7ca7-133">tooenable remote management through hello Azure classic portal</span></span>
1. <span data-ttu-id="e7ca7-134">Откройте **Устройства** > **Настроить** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="e7ca7-135">Прокрутите вниз toohello **удаленного управления** раздела.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-135">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="e7ca7-136">Задать **Включение удаленного управления** слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-136">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="e7ca7-137">Теперь вы можете tooconnect с помощью протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-137">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="e7ca7-138">(по умолчанию hello — tooconnect по протоколу HTTPS). Убедитесь, что выбран HTTP.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-138">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e7ca7-139">Подключение по HTTP допустимо только в доверенных сетях.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="e7ca7-140">Нажмите кнопку **Сохранить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-140">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="e7ca7-141">Используйте hello последовательной консоли tooenable удаленное управление по протоколу HTTP</span><span class="sxs-lookup"><span data-stu-id="e7ca7-141">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="e7ca7-142">Выполните следующие шаги на удаленное управление последовательной консоли устройства tooenable hello hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-142">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="e7ca7-143">удаленное управление tooenable через последовательную консоль устройства hello</span><span class="sxs-lookup"><span data-stu-id="e7ca7-143">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="e7ca7-144">В меню последовательной консоли hello выберите вариант 1.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-144">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="e7ca7-145">Дополнительные сведения об использовании последовательной консоли hello на устройстве hello go слишком[подключения tooWindows PowerShell для StorSimple через последовательную консоль устройства](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="e7ca7-145">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="e7ca7-146">Привет введите в строке:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="e7ca7-146">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="e7ca7-147">Вы получите уведомление об уязвимостях безопасности с помощью HTTP tooconnect toohello устройства hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-147">You will be notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="e7ca7-148">При появлении запроса подтверждения введите **Y**.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="e7ca7-149">Убедитесь, что HTTP включен, набрав: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="e7ca7-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="e7ca7-150">Убедитесь, что hello **RemoteManagementMode** отображается **HttpsAndHttpEnabled**.hello следующие иллюстрации показаны эти параметры в PuTTY.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-150">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Последовательный HTTPS и HTTP включены](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="e7ca7-152">Подготовка hello клиента для удаленного подключения</span><span class="sxs-lookup"><span data-stu-id="e7ca7-152">Prepare hello client for remote connection</span></span>
<span data-ttu-id="e7ca7-153">Выполните следующие шаги на приветствия клиента tooenable удаленного управления hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-153">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="e7ca7-154">tooprepare hello клиента для удаленного подключения</span><span class="sxs-lookup"><span data-stu-id="e7ca7-154">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="e7ca7-155">Запустите сеанс Windows PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="e7ca7-156">Тип hello следующая команда tooadd hello IP-адрес устройства toohello hello StorSimple клиента списку доверенных узлов:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-156">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="e7ca7-157">Замените <*device_ip*> hello IP-адрес устройства, например:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-157">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="e7ca7-158">Тип hello следующая команда toosave hello устройство и учетные данные в переменной:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-158">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="e7ca7-159">В диалоговом окне приветствия, которая отображается:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-159">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="e7ca7-160">Введите имя пользователя hello в следующем формате: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-160">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="e7ca7-161">Введите пароль администратора устройства hello, который был задан при настройке устройства hello с приветствия мастера установки.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-161">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="e7ca7-162">пароль по умолчанию Hello — *Password1*.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-162">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="e7ca7-163">Запустите сеанс Windows PowerShell на устройстве hello, введя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-163">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="e7ca7-164">toocreate сеанс Windows PowerShell для использования с виртуального устройства StorSimple hello append hello `–Port` параметра и укажите общий порт hello, настроенные для виртуального устройства StorSimple в системе удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-164">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="e7ca7-165">На этом этапе необходимо активного устройства toohello удаленного сеанса Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-165">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
    ![Удаленное взаимодействие PowerShell через HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="e7ca7-167">Подключение по протоколу HTTPS</span><span class="sxs-lookup"><span data-stu-id="e7ca7-167">Connect through HTTPS</span></span>
<span data-ttu-id="e7ca7-168">Подключение tooWindows PowerShell для StorSimple через сеанс HTTPS — наиболее безопасный hello и рекомендуется использовать метод Microsoft Azure StorSimple устройство удаленно подключения tooyour.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-168">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="e7ca7-169">Hello следующих процедур объясняется, как tooset копирование hello последовательную консоль и клиентские компьютеры, чтобы можно было использовать HTTPS tooconnect tooWindows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-169">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="e7ca7-170">Можно использовать hello классический портал Azure или hello последовательной консоли tooconfigure удаленного управления.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-170">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="e7ca7-171">Выберите один из следующих процедур hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-171">Select from hello following procedures:</span></span>

* [<span data-ttu-id="e7ca7-172">Использовать hello Azure классического портала tooenable удаленное управление по протоколу HTTPS</span><span class="sxs-lookup"><span data-stu-id="e7ca7-172">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="e7ca7-173">Использовать hello последовательной консоли tooenable удаленное управление по протоколу HTTPS</span><span class="sxs-lookup"><span data-stu-id="e7ca7-173">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="e7ca7-174">После включения удаленного управления, используйте следующие процедуры tooprepare hello узлов для удаленного управления hello и подключить устройство toohello от удаленного хоста hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-174">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="e7ca7-175">Подготовка узла hello для удаленного управления</span><span class="sxs-lookup"><span data-stu-id="e7ca7-175">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="e7ca7-176">Подключите устройство toohello от удаленного хоста hello</span><span class="sxs-lookup"><span data-stu-id="e7ca7-176">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="e7ca7-177">Использовать hello Azure классического портала tooenable удаленное управление по протоколу HTTPS</span><span class="sxs-lookup"><span data-stu-id="e7ca7-177">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>
<span data-ttu-id="e7ca7-178">Выполните следующие шаги в hello Azure классического портала tooenable удаленное управление по протоколу HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-178">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a><span data-ttu-id="e7ca7-179">удаленное управление по протоколу HTTPS из классического портала Azure hello tooenable</span><span class="sxs-lookup"><span data-stu-id="e7ca7-179">tooenable remote management over HTTPS from hello Azure classic portal</span></span>
1. <span data-ttu-id="e7ca7-180">Откройте **Устройства** > **Настроить** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="e7ca7-181">Прокрутите вниз toohello **удаленного управления** раздела.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-181">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="e7ca7-182">Задать **Включение удаленного управления** слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-182">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="e7ca7-183">Теперь вы можете tooconnect с помощью протокола HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-183">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="e7ca7-184">(по умолчанию hello — tooconnect по протоколу HTTPS). Убедитесь, что выбран HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-184">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="e7ca7-185">Щелкните **Загрузить сертификат удаленного управления**.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="e7ca7-186">Укажите toosave расположение этого файла.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-186">Specify a location toosave this file.</span></span> <span data-ttu-id="e7ca7-187">Вам потребуется tooinstall этот сертификат на компьютере клиента или узла hello, который будет использоваться tooconnect toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-187">You will need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="e7ca7-188">Нажмите кнопку **Сохранить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-188">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="e7ca7-189">Использовать hello последовательной консоли tooenable удаленное управление по протоколу HTTPS</span><span class="sxs-lookup"><span data-stu-id="e7ca7-189">Use hello serial console tooenable remote management over HTTPS</span></span>
<span data-ttu-id="e7ca7-190">Выполните следующие шаги на удаленное управление последовательной консоли устройства tooenable hello hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-190">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="e7ca7-191">удаленное управление tooenable через последовательную консоль устройства hello</span><span class="sxs-lookup"><span data-stu-id="e7ca7-191">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="e7ca7-192">В меню последовательной консоли hello выберите вариант 1.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-192">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="e7ca7-193">Дополнительные сведения об использовании последовательной консоли hello на устройстве hello go слишком[подключения tooWindows PowerShell для StorSimple через последовательную консоль устройства](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="e7ca7-193">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="e7ca7-194">Привет введите в строке:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-194">At hello prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="e7ca7-195">Эта команда должна включить протокол HTTPS на вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="e7ca7-196">Убедитесь, что HTTPS включен, набрав:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="e7ca7-197">Убедитесь в том, что hello **RemoteManagementMode** отображается **HttpsEnabled**.hello следующие иллюстрации показаны эти параметры в PuTTY.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-197">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Последовательный HTTPS включен](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="e7ca7-199">Из вывода hello `Get-HcsSystem`, скопируйте серийный номер устройства hello hello и сохранить его для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-199">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e7ca7-200">серийный номер Hello указывает toohello CN-имени в сертификате hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-200">hello serial number maps toohello CN name in hello certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="e7ca7-201">Получите сертификат удаленного управления, набрав:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="e7ca7-202">Появится сертификат аналогичные toohello следующее.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-202">A certificate similar toohello following will appear.</span></span>
   
    ![Получение сертификата удаленного управления](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="e7ca7-204">Скопируйте hello сведения в сертификате hello **---BEGIN CERTIFICATE---** слишком**---конечный СЕРТИФИКАТ---** в текстовый редактор, например Блокнот и сохраните его как файл CER.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-204">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="e7ca7-205">(Необходимо будет скопировать этот файл tooyour удаленного узла при подготовке узла hello.)</span><span class="sxs-lookup"><span data-stu-id="e7ca7-205">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e7ca7-206">toogenerate новый сертификат, используйте hello `Set-HcsRemoteManagementCert` командлета.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-206">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="e7ca7-207">Подготовка узла hello для удаленного управления</span><span class="sxs-lookup"><span data-stu-id="e7ca7-207">Prepare hello host for remote management</span></span>
<span data-ttu-id="e7ca7-208">tooprepare hello главного компьютера для удаленного подключения, которое использует сеанс HTTPS выполните hello следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-208">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="e7ca7-209">[Импортировать файл .cer hello в корневое хранилище hello hello клиента или удаленного узла](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="e7ca7-209">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="e7ca7-210">[Добавьте файл hosts toohello серийные номера устройств hello на удаленном узле](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="e7ca7-210">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="e7ca7-211">Каждая из этих процедур описана ниже.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-211">Each of these procedures is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="e7ca7-212">tooimport hello сертификата удаленного узла hello</span><span class="sxs-lookup"><span data-stu-id="e7ca7-212">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="e7ca7-213">Щелкните правой кнопкой мыши hello CER-файл и выберите **установить сертификат**.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-213">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="e7ca7-214">Будет запущен мастер импорта сертификатов hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-214">This will start hello Certificate Import Wizard.</span></span>
   
    ![Мастер импорта сертификатов 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="e7ca7-216">В качестве **Расположения хранилища** выберите **Локальный компьютер**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="e7ca7-217">Выберите **поместить все сертификаты в следующие хранилища hello**, а затем нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-217">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="e7ca7-218">Перейдите в удаленный узел toohello корневое хранилище и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-218">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Мастер импорта сертификатов 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="e7ca7-220">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="e7ca7-220">Click **Finish**.</span></span> <span data-ttu-id="e7ca7-221">Появится сообщение, информирующее о том, что hello Импорт успешно выполнен.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-221">A message that tells you that hello import was successful appears.</span></span>
   
    ![Мастер импорта сертификатов 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="e7ca7-223">удаленный узел серийные номера устройств toohello tooadd</span><span class="sxs-lookup"><span data-stu-id="e7ca7-223">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="e7ca7-224">Откройте Блокнот от имени администратора, а затем откройте файл hosts hello, расположенный в \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-224">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="e7ca7-225">Добавьте следующие три файла hosts записи tooyour hello: **DATA 0 IP-адрес**, **фиксированный IP-адрес контроллера 0**, и **фиксированный IP-адрес контроллера 1 адрес**.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-225">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="e7ca7-226">Введите серийный номер устройства hello сохраненный ранее.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-226">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="e7ca7-227">Сопоставьте этот IP-адрес toohello, как показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-227">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="e7ca7-228">Для контроллера 0 и 1, добавьте **Controller0** и **Controller1** в конце hello hello серийный номер (CN-имя).</span><span class="sxs-lookup"><span data-stu-id="e7ca7-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![Добавление файла toohosts CN-имени](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="e7ca7-230">Сохранить файл hosts hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-230">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="e7ca7-231">Подключите устройство toohello от удаленного хоста hello</span><span class="sxs-lookup"><span data-stu-id="e7ca7-231">Connect toohello device from hello remote host</span></span>
<span data-ttu-id="e7ca7-232">Использование Windows PowerShell и SSL tooenter сеанс SSAdmin на устройстве с удаленного узла или клиента.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-232">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="e7ca7-233">Hello сеанс SSAdmin сопоставляется toooption 1 в hello [последовательной консоли](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) меню вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-233">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="e7ca7-234">Выполните процедуру, приведенную на компьютере hello, с которого будет осуществляться удаленное подключение Windows PowerShell toomake hello hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-234">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="e7ca7-235">tooenter сеанс SSAdmin на устройстве hello с помощью Windows PowerShell и SSL</span><span class="sxs-lookup"><span data-stu-id="e7ca7-235">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="e7ca7-236">Запустите сеанс Windows PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="e7ca7-237">Добавьте hello устройства IP адрес toohello доверенные узлы клиента введя:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-237">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="e7ca7-238">Где <*device_ip*> hello IP-адрес устройства, например:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-238">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="e7ca7-239">Создайте новые учетные данные, введя:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="e7ca7-240">Где <*IP-адрес целевого устройства*> — hello IP-адрес DATA 0 для устройства, например, **10.126.173.90** как показано в предшествующих образ файла hosts hello hello.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-240">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="e7ca7-241">Также укажите пароль администратора hello для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-241">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="e7ca7-242">Создайте сеанс, набрав:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="e7ca7-243">Для параметра - ComputerName hello в командлете hello, предоставляют hello <*серийный номер целевого устройства*>.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-243">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="e7ca7-244">Этот серийный номер был сопоставлен toohello IP-адрес DATA 0 в файле hosts hello на удаленном узле; например **SHX0991003G44MT** как показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-244">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="e7ca7-245">Тип:</span><span class="sxs-lookup"><span data-stu-id="e7ca7-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="e7ca7-246">Toowait потребуется несколько минут и затем будет tooyour подключенного устройства через HTTPS по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-246">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="e7ca7-247">Появится сообщение о том, что вы являетесь tooyour подключенных устройств.</span><span class="sxs-lookup"><span data-stu-id="e7ca7-247">You will see a message that indicates you are connected tooyour device.</span></span>
   
    ![Удаленное взаимодействие PowerShell через HTTPS и SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="e7ca7-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e7ca7-249">Next steps</span></span>
* <span data-ttu-id="e7ca7-250">Дополнительные сведения о [с помощью tooadminister Windows PowerShell устройства StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e7ca7-250">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="e7ca7-251">Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e7ca7-251">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

