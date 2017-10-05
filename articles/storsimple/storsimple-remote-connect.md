---
title: "Удаленное подключение к устройству StorSimple | Документация Майкрософт"
description: "Объясняется, как настроить устройство для удаленного управления, а затем подключиться к Windows PowerShell для StorSimple по протоколу HTTP или HTTPS."
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
ms.openlocfilehash: b916173e127394d3ea06eded36285bdbbf884b12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="d3ea0-103">Удаленное подключение к устройству StorSimple серии 8000</span><span class="sxs-lookup"><span data-stu-id="d3ea0-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="d3ea0-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d3ea0-104">Overview</span></span>
<span data-ttu-id="d3ea0-105">Для подключения к устройству StorSimple можно использовать удаленное взаимодействие Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-105">You can use Windows PowerShell remoting to connect to your StorSimple device.</span></span> <span data-ttu-id="d3ea0-106">При таком способе подключения меню не отображается.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="d3ea0-107">(Меню появляется только при подключении к устройству с помощью последовательной консоли.) При использовании удаленного взаимодействия Windows PowerShell вы подключаетесь к конкретному пространству выполнения.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="d3ea0-108">Также можно указать язык интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-108">You can also specify the display language.</span></span> 

<span data-ttu-id="d3ea0-109">Дополнительные сведения об использовании удаленного взаимодействия Windows PowerShell для управления устройством см. в статье [Использование Windows PowerShell для StorSimple для администрирования устройства StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d3ea0-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="d3ea0-110">В этом учебнике объясняется, как настроить устройство для удаленного управления, а затем подключиться к Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="d3ea0-111">Для подключения с использованием удаленного взаимодействия Windows PowerShell можно использовать HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-111">You can use HTTP or HTTPS to connect via Windows PowerShell remoting.</span></span> <span data-ttu-id="d3ea0-112">Однако при выборе способа подключения к Windows PowerShell для StorSimple следует учесть перечисленные ниже аспекты.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following:</span></span> 

* <span data-ttu-id="d3ea0-113">Прямое подключение к последовательной консоли устройства является безопасным, а подключение к последовательной консоли через сетевые коммутаторы — нет.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="d3ea0-114">При подключении к последовательной консоли устройства через сетевые коммутаторы учитывайте угрозы для безопасности.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span> 
* <span data-ttu-id="d3ea0-115">Подключение через сеанс HTTP может быть более безопасным, чем подключение через последовательную консоль по сети.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="d3ea0-116">Хотя это не самый безопасный метод, его можно использовать в доверенных сетях.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="d3ea0-117">Наиболее безопасным и рекомендуемым способом подключения является подключение через сеанс HTTPS с самозаверяющим сертификатом.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="d3ea0-118">К интерфейсу Windows PowerShell можно подключиться удаленно.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="d3ea0-119">Однако удаленный доступ к устройству StorSimple в интерфейсе Windows PowerShell по умолчанию отключен.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="d3ea0-120">Необходимо сначала включить удаленное управление на устройстве, а затем включить его в клиенте, который будет использоваться для доступа к устройству.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-120">You need to enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="d3ea0-121">Действия, описанные в этой статье, были выполнены в системе узла под управлением Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="d3ea0-122">Подключение по протоколу HTTP</span><span class="sxs-lookup"><span data-stu-id="d3ea0-122">Connect through HTTP</span></span>
<span data-ttu-id="d3ea0-123">Подключение к Windows PowerShell для StorSimple через сеанс HTTP обеспечивает более высокий уровень безопасности по сравнению с подключением через последовательную консоль устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="d3ea0-124">Хотя это не самый безопасный метод, его можно использовать в доверенных сетях.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="d3ea0-125">Для настройки удаленного управления можно использовать классический портал Azure или последовательную консоль.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-125">You can use either the Azure classic portal or the serial console to configure remote management.</span></span> <span data-ttu-id="d3ea0-126">Выберите одну из следующих процедур:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="d3ea0-127">Включение удаленного управления по протоколу HTTP с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="d3ea0-127">Use the Azure classic portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="d3ea0-128">Включение удаленного управления по протоколу HTTP с помощью последовательной консоли</span><span class="sxs-lookup"><span data-stu-id="d3ea0-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="d3ea0-129">После включения удаленного управления используйте следующую процедуру для подготовки клиента для удаленного подключения.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="d3ea0-130">Подготовка клиента для удаленного подключения</span><span class="sxs-lookup"><span data-stu-id="d3ea0-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="d3ea0-131">Включение удаленного управления по протоколу HTTP с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="d3ea0-131">Use the Azure classic portal to enable remote management over HTTP</span></span>
<span data-ttu-id="d3ea0-132">Для включения удаленного управления по протоколу HTTP выполните следующие действия на классическом портале Azure.с</span><span class="sxs-lookup"><span data-stu-id="d3ea0-132">Perform the following steps in the Azure classic portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-classic-portal"></a><span data-ttu-id="d3ea0-133">Включение удаленного управления с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="d3ea0-133">To enable remote management through the Azure classic portal</span></span>
1. <span data-ttu-id="d3ea0-134">Откройте **Устройства** > **Настроить** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="d3ea0-135">Прокрутите экран вниз, к разделу **Удаленное управление** .</span><span class="sxs-lookup"><span data-stu-id="d3ea0-135">Scroll down to the **Remote Management** section.</span></span>
3. <span data-ttu-id="d3ea0-136">Задайте для пункта **Включить удаленное управление** значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-136">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="d3ea0-137">Теперь вы можете выбрать подключение по HTTP.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-137">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="d3ea0-138">(По умолчанию выбрано подключение по HTTPS.) Убедитесь, что выбран HTTP.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-138">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d3ea0-139">Подключение по HTTP допустимо только в доверенных сетях.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="d3ea0-140">В нижней части страницы нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d3ea0-140">Click **Save** at the bottom of the page.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="d3ea0-141">Включение удаленного управления по протоколу HTTP с помощью последовательной консоли</span><span class="sxs-lookup"><span data-stu-id="d3ea0-141">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="d3ea0-142">Для включения удаленного управления выполните следующие действия в последовательной консоли устройства.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-142">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="d3ea0-143">Включение удаленного управления с помощью последовательной консоли</span><span class="sxs-lookup"><span data-stu-id="d3ea0-143">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="d3ea0-144">В меню последовательной консоли выберите вариант 1.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-144">On the serial console menu, select option 1.</span></span> <span data-ttu-id="d3ea0-145">Дополнительные сведения об использовании последовательной консоли устройства см. в статье [Подключение к Windows PowerShell для StorSimple через последовательную консоль устройства](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d3ea0-145">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="d3ea0-146">В командной строке введите следующую команду: `Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="d3ea0-146">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="d3ea0-147">Вы получите уведомление об уязвимостях системы безопасности при подключении к устройству с помощью HTTP.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-147">You will be notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="d3ea0-148">При появлении запроса подтверждения введите **Y**.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="d3ea0-149">Убедитесь, что HTTP включен, набрав: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="d3ea0-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="d3ea0-150">Убедитесь, что значение поля **RemoteManagementMode** равно **HttpsAndHttpEnabled**. На следующем рисунке показаны эти параметры в PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-150">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Последовательный HTTPS и HTTP включены](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="d3ea0-152">Подготовка клиента для удаленного подключения</span><span class="sxs-lookup"><span data-stu-id="d3ea0-152">Prepare the client for remote connection</span></span>
<span data-ttu-id="d3ea0-153">Для включения удаленного управления выполните следующие действия в клиенте.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-153">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="d3ea0-154">Подготовка клиента для удаленного подключения</span><span class="sxs-lookup"><span data-stu-id="d3ea0-154">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="d3ea0-155">Запустите сеанс Windows PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="d3ea0-156">Введите следующую команду, чтобы добавить IP-адрес устройства StorSimple в список доверенных узлов клиента:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-156">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="d3ea0-157">Замените <*device_ip*> IP-адресом своего устройства, например:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-157">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="d3ea0-158">Введите следующую команду, чтобы сохранить учетные данные устройства в переменной:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-158">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="d3ea0-159">В открывшемся диалоговом окне:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-159">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="d3ea0-160">Введите имя пользователя в следующем формате: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-160">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="d3ea0-161">Введите пароль администратора устройства, который был установлен при настройке устройства с помощью мастера установки.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-161">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="d3ea0-162">Пароль по умолчанию — *Password1*.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-162">The default password is *Password1*.</span></span>
5. <span data-ttu-id="d3ea0-163">Запустите сеанс Windows PowerShell на устройстве, введя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-163">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="d3ea0-164">Чтобы создать сеанс Windows PowerShell для виртуального устройства StorSimple, добавьте параметр `–Port` и укажите общий порт, настроенный для удаленного взаимодействия с виртуальным устройством StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-164">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="d3ea0-165">На этом этапе у вас должен быть активный удаленный сеанс Windows PowerShell с устройством.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-165">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
    ![Удаленное взаимодействие PowerShell через HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="d3ea0-167">Подключение по протоколу HTTPS</span><span class="sxs-lookup"><span data-stu-id="d3ea0-167">Connect through HTTPS</span></span>
<span data-ttu-id="d3ea0-168">Подключение к Windows PowerShell для StorSimple через сеанс HTTPS — наиболее безопасный и рекомендуемый метод удаленного подключения к устройству Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-168">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="d3ea0-169">В следующих процедурах описана настройка последовательной консоли и клиентских компьютеров для использования HTTPS для подключения к Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-169">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="d3ea0-170">Для настройки удаленного управления можно использовать классический портал Azure или последовательную консоль.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-170">You can use either the Azure classic portal or the serial console to configure remote management.</span></span> <span data-ttu-id="d3ea0-171">Выберите одну из следующих процедур:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-171">Select from the following procedures:</span></span>

* [<span data-ttu-id="d3ea0-172">Включение удаленного управления по протоколу HTTPS с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="d3ea0-172">Use the Azure classic portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="d3ea0-173">Включение удаленного управления по протоколу HTTPS с помощью последовательной консоли</span><span class="sxs-lookup"><span data-stu-id="d3ea0-173">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="d3ea0-174">После включения удаленного управления используйте следующие процедуры для подготовки узла для удаленного управления и подключения к устройству с удаленного узла.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-174">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="d3ea0-175">Подготовка узла для удаленного управления</span><span class="sxs-lookup"><span data-stu-id="d3ea0-175">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="d3ea0-176">Подключение к устройству с удаленного узла</span><span class="sxs-lookup"><span data-stu-id="d3ea0-176">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="d3ea0-177">Включение удаленного управления по протоколу HTTPS с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="d3ea0-177">Use the Azure classic portal to enable remote management over HTTPS</span></span>
<span data-ttu-id="d3ea0-178">Для включения удаленного управления по протоколу HTTPS выполните следующие действия на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-178">Perform the following steps in the Azure classic portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-classic-portal"></a><span data-ttu-id="d3ea0-179">Включение удаленного управления по протоколу HTTPS на классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="d3ea0-179">To enable remote management over HTTPS from the Azure classic portal</span></span>
1. <span data-ttu-id="d3ea0-180">Откройте **Устройства** > **Настроить** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="d3ea0-181">Прокрутите экран вниз, к разделу **Удаленное управление** .</span><span class="sxs-lookup"><span data-stu-id="d3ea0-181">Scroll down to the **Remote Management** section.</span></span>
3. <span data-ttu-id="d3ea0-182">Задайте для пункта **Включить удаленное управление** значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-182">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="d3ea0-183">Теперь вы можете выбрать подключение по HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-183">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="d3ea0-184">(По умолчанию выбрано подключение по HTTPS.) Убедитесь, что выбран HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-184">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="d3ea0-185">Щелкните **Загрузить сертификат удаленного управления**.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="d3ea0-186">Укажите расположение для сохранения этого файла.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-186">Specify a location to save this file.</span></span> <span data-ttu-id="d3ea0-187">Этот сертификат необходимо установить на компьютере клиента или узла, который будет использоваться для подключения к устройству.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-187">You will need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="d3ea0-188">В нижней части страницы нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d3ea0-188">Click **Save** at the bottom of the page.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="d3ea0-189">Включение удаленного управления по протоколу HTTPS с помощью последовательной консоли</span><span class="sxs-lookup"><span data-stu-id="d3ea0-189">Use the serial console to enable remote management over HTTPS</span></span>
<span data-ttu-id="d3ea0-190">Для включения удаленного управления выполните следующие действия в последовательной консоли устройства.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-190">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="d3ea0-191">Включение удаленного управления с помощью последовательной консоли</span><span class="sxs-lookup"><span data-stu-id="d3ea0-191">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="d3ea0-192">В меню последовательной консоли выберите вариант 1.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-192">On the serial console menu, select option 1.</span></span> <span data-ttu-id="d3ea0-193">Дополнительные сведения об использовании последовательной консоли устройства см. в статье [Подключение к Windows PowerShell для StorSimple через последовательную консоль устройства](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d3ea0-193">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="d3ea0-194">В командной строке введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-194">At the prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="d3ea0-195">Эта команда должна включить протокол HTTPS на вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="d3ea0-196">Убедитесь, что HTTPS включен, набрав:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="d3ea0-197">Убедитесь, что в поле **RemoteManagementMode** задано значение **HttpsEnabled**. На следующем рисунке показаны эти параметры в PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-197">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Последовательный HTTPS включен](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="d3ea0-199">Из вывода команды `Get-HcsSystem`скопируйте серийный номер устройства и сохраните его для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-199">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d3ea0-200">Серийный номер сопоставляется CN-имени в сертификате.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-200">The serial number maps to the CN name in the certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="d3ea0-201">Получите сертификат удаленного управления, набрав:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="d3ea0-202">Появится сертификат, похожий на показанный ниже:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-202">A certificate similar to the following will appear.</span></span>
   
    ![Получение сертификата удаленного управления](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="d3ea0-204">Скопируйте информацию из сертификата от **-----BEGIN CERTIFICATE-----** до **-----END CERTIFICATE-----** в текстовый редактор, например в "Блокнот", и сохраните файл в формате CER.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-204">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="d3ea0-205">(При подготовке удаленного узла этот файл будет необходимо скопировать на этот узел.)</span><span class="sxs-lookup"><span data-stu-id="d3ea0-205">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d3ea0-206">Чтобы создать новый сертификат, используйте командлет `Set-HcsRemoteManagementCert`.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-206">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="d3ea0-207">Подготовка узла для удаленного управления</span><span class="sxs-lookup"><span data-stu-id="d3ea0-207">Prepare the host for remote management</span></span>
<span data-ttu-id="d3ea0-208">Чтобы подготовить компьютер узла для удаленного подключения, которое использует сеанс HTTPS, выполните следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-208">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="d3ea0-209">[Импортируйте CER-файл в корневое хранилище клиента или удаленного узла](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="d3ea0-209">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="d3ea0-210">[Добавьте серийные номера устройств в файл hosts на удаленном узле](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="d3ea0-210">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="d3ea0-211">Каждая из этих процедур описана ниже.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-211">Each of these procedures is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="d3ea0-212">Импорт сертификата на удаленном узле</span><span class="sxs-lookup"><span data-stu-id="d3ea0-212">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="d3ea0-213">Щелкните правой кнопкой мыши на CER-файле и выберите **Установить сертификат**.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-213">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="d3ea0-214">Откроется мастер импорта сертификатов.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-214">This will start the Certificate Import Wizard.</span></span>
   
    ![Мастер импорта сертификатов 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="d3ea0-216">В качестве **Расположения хранилища** выберите **Локальный компьютер**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="d3ea0-217">Выберите **Поместить все сертификаты в следующее хранилище**, затем нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-217">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="d3ea0-218">Перейдите в корневое хранилище удаленного узла и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-218">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![Мастер импорта сертификатов 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="d3ea0-220">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="d3ea0-220">Click **Finish**.</span></span> <span data-ttu-id="d3ea0-221">Появится сообщение о том, что импорт успешно выполнен.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-221">A message that tells you that the import was successful appears.</span></span>
   
    ![Мастер импорта сертификатов 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="d3ea0-223">Добавление серийных номеров устройства в удаленный узел</span><span class="sxs-lookup"><span data-stu-id="d3ea0-223">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="d3ea0-224">Откройте "Блокнот" от имени администратора и откройте файл hosts, расположенный в папке \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-224">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="d3ea0-225">Добавьте следующие три записи в файл hosts: **IP-адрес данных 0**, **Фиксированный IP-адрес контроллера 0** и **Фиксированный IP-адрес контроллера 1**.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-225">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="d3ea0-226">Введите серийный номер устройства, сохраненный ранее.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-226">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="d3ea0-227">Сопоставьте его с IP-адресом, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-227">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="d3ea0-228">Для контроллера 0 и контроллера 1 добавьте **Controller0** и **Controller1** в конце серийного номера (CN-имени).</span><span class="sxs-lookup"><span data-stu-id="d3ea0-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![Добавление имени CN в файл hosts](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="d3ea0-230">Сохраните файл hosts.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-230">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="d3ea0-231">Подключение к устройству с удаленного узла</span><span class="sxs-lookup"><span data-stu-id="d3ea0-231">Connect to the device from the remote host</span></span>
<span data-ttu-id="d3ea0-232">С помощью Windows PowerShell и SSL создайте сеанс SSAdmin на устройстве с удаленного узла или клиента.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-232">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="d3ea0-233">Сеанс SSAdmin соответствует пункту 1 в меню [последовательной консоли](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) устройства.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-233">The SSAdmin session maps to option 1 in the [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="d3ea0-234">Выполните следующую процедуру на компьютере, с которого будет выполняться удаленное подключение Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-234">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="d3ea0-235">Создание сеанса SSAdmin на устройстве с помощью Windows PowerShell и SSL</span><span class="sxs-lookup"><span data-stu-id="d3ea0-235">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="d3ea0-236">Запустите сеанс Windows PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="d3ea0-237">Добавьте IP-адрес устройства в доверенные узлы клиента, набрав:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-237">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="d3ea0-238">Замените <*device_ip*> IP-адресом своего устройства, например:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-238">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="d3ea0-239">Создайте новые учетные данные, введя:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="d3ea0-240">Где <*IP of target device*> — это IP-адрес DATA 0 вашего устройства, например, **10.126.173.90**, как показано на предыдущем рисунке файла hosts.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-240">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="d3ea0-241">Также укажите пароль администратора для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-241">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="d3ea0-242">Создайте сеанс, набрав:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="d3ea0-243">В качестве параметра -ComputerName в командлете введите <*серийный номер целевого устройства*>.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-243">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="d3ea0-244">Этот серийный номер был сопоставлен с IP-адресом DATA 0 в файле hosts на удаленном узле. Пример — **SHX0991003G44MT**, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-244">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="d3ea0-245">Тип:</span><span class="sxs-lookup"><span data-stu-id="d3ea0-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="d3ea0-246">Необходимо подождать несколько минут, после чего вы будете подключены к устройству через HTTPS по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-246">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="d3ea0-247">Появится сообщение о том, что вы подключены к устройству.</span><span class="sxs-lookup"><span data-stu-id="d3ea0-247">You will see a message that indicates you are connected to your device.</span></span>
   
    ![Удаленное взаимодействие PowerShell через HTTPS и SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="d3ea0-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d3ea0-249">Next steps</span></span>
* <span data-ttu-id="d3ea0-250">Узнайте больше об [использовании Windows PowerShell для администрирования устройства StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d3ea0-250">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="d3ea0-251">Узнайте больше об [использовании службы диспетчера StorSimple для администрирования устройства StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d3ea0-251">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

