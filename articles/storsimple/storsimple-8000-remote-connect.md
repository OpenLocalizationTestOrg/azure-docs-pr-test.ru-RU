---
title: "Удаленное подключение к устройству StorSimple | Документация Майкрософт"
description: "Объясняется, как настроить устройство для удаленного управления, а затем подключиться к Windows PowerShell для StorSimple по протоколу HTTP или HTTPS."
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
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff76884f020a0fb8a1b48bd371c419bd65e85fd3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="e77b8-103">Удаленное подключение к устройству StorSimple серии 8000</span><span class="sxs-lookup"><span data-stu-id="e77b8-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="e77b8-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="e77b8-104">Overview</span></span>

<span data-ttu-id="e77b8-105">Вы можете подключаться к своему устройству удаленно с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e77b8-105">You can remotely connect to your device via Windows PowerShell.</span></span> <span data-ttu-id="e77b8-106">При таком способе подключения меню не отображается.</span><span class="sxs-lookup"><span data-stu-id="e77b8-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="e77b8-107">(Меню появляется только при подключении к устройству с помощью последовательной консоли.) При использовании удаленного взаимодействия Windows PowerShell вы подключаетесь к конкретному пространству выполнения.</span><span class="sxs-lookup"><span data-stu-id="e77b8-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="e77b8-108">Также можно указать язык интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e77b8-108">You can also specify the display language.</span></span>

<span data-ttu-id="e77b8-109">Дополнительные сведения об использовании удаленного взаимодействия Windows PowerShell для управления устройством см. в статье [Использование Windows PowerShell для StorSimple для администрирования устройства StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e77b8-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="e77b8-110">В этом учебнике объясняется, как настроить устройство для удаленного управления, а затем подключиться к Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e77b8-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="e77b8-111">Для удаленного подключения с использованием Windows PowerShell можно использовать HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e77b8-111">You can use HTTP or HTTPS to remotely connect via Windows PowerShell.</span></span> <span data-ttu-id="e77b8-112">Однако при выборе способа подключения к Windows PowerShell для StorSimple следует учесть приведенные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="e77b8-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following information:</span></span>

* <span data-ttu-id="e77b8-113">Прямое подключение к последовательной консоли устройства является безопасным, а подключение к последовательной консоли через сетевые коммутаторы — нет.</span><span class="sxs-lookup"><span data-stu-id="e77b8-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="e77b8-114">При подключении к последовательной консоли устройства через сетевые коммутаторы учитывайте угрозы для безопасности.</span><span class="sxs-lookup"><span data-stu-id="e77b8-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span>
* <span data-ttu-id="e77b8-115">Подключение через сеанс HTTP может быть более безопасным, чем подключение через последовательную консоль по сети.</span><span class="sxs-lookup"><span data-stu-id="e77b8-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="e77b8-116">Хотя это не самый безопасный метод, его можно использовать в доверенных сетях.</span><span class="sxs-lookup"><span data-stu-id="e77b8-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="e77b8-117">Наиболее безопасным и рекомендуемым способом подключения является подключение через сеанс HTTPS с самозаверяющим сертификатом.</span><span class="sxs-lookup"><span data-stu-id="e77b8-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="e77b8-118">К интерфейсу Windows PowerShell можно подключиться удаленно.</span><span class="sxs-lookup"><span data-stu-id="e77b8-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="e77b8-119">Однако удаленный доступ к устройству StorSimple в интерфейсе Windows PowerShell по умолчанию отключен.</span><span class="sxs-lookup"><span data-stu-id="e77b8-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="e77b8-120">Следует включить удаленное управление сначала на устройстве, а затем — в клиенте, который будет использоваться для доступа к устройству.</span><span class="sxs-lookup"><span data-stu-id="e77b8-120">You must enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="e77b8-121">Действия, описанные в этой статье, были выполнены в системе узла под управлением Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="e77b8-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="e77b8-122">Подключение по протоколу HTTP</span><span class="sxs-lookup"><span data-stu-id="e77b8-122">Connect through HTTP</span></span>

<span data-ttu-id="e77b8-123">Подключение к Windows PowerShell для StorSimple через сеанс HTTP обеспечивает более высокий уровень безопасности по сравнению с подключением через последовательную консоль устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e77b8-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="e77b8-124">Хотя это не самый безопасный метод, его можно использовать в доверенных сетях.</span><span class="sxs-lookup"><span data-stu-id="e77b8-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="e77b8-125">Для настройки удаленного управления можно использовать портал Azure или последовательную консоль.</span><span class="sxs-lookup"><span data-stu-id="e77b8-125">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="e77b8-126">Выберите одну из следующих процедур:</span><span class="sxs-lookup"><span data-stu-id="e77b8-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="e77b8-127">Включение удаленного управления по протоколу HTTP с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="e77b8-127">Use the Azure portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="e77b8-128">Включение удаленного управления по протоколу HTTP с помощью последовательной консоли</span><span class="sxs-lookup"><span data-stu-id="e77b8-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="e77b8-129">После включения удаленного управления используйте следующую процедуру для подготовки клиента для удаленного подключения.</span><span class="sxs-lookup"><span data-stu-id="e77b8-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="e77b8-130">Подготовка клиента для удаленного подключения</span><span class="sxs-lookup"><span data-stu-id="e77b8-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="e77b8-131">Включение удаленного управления по протоколу HTTP с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="e77b8-131">Use the Azure portal to enable remote management over HTTP</span></span>

<span data-ttu-id="e77b8-132">Чтобы включить удаленное управление по протоколу HTTP, выполните следующие действия на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e77b8-132">Perform the following steps in the Azure portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-portal"></a><span data-ttu-id="e77b8-133">Включение удаленного управления с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="e77b8-133">To enable remote management through the Azure portal</span></span>

1. <span data-ttu-id="e77b8-134">Откройте службу диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e77b8-134">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="e77b8-135">Выберите **Устройства**, а затем щелкните устройство, на котором нужно настроить удаленное управление.</span><span class="sxs-lookup"><span data-stu-id="e77b8-135">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="e77b8-136">Последовательно выберите пункты **Параметры устройства > Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-136">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="e77b8-137">В колонке **Параметры безопасности** щелкните **Удаленное управление**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-137">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="e77b8-138">В колонке **Удаленное управление** для параметра **Включить удаленное управление** установите значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-138">In the **Remote management** blade, set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="e77b8-139">Теперь вы можете выбрать подключение по HTTP.</span><span class="sxs-lookup"><span data-stu-id="e77b8-139">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="e77b8-140">(По умолчанию выбрано подключение по HTTPS.) Убедитесь, что выбран HTTP.</span><span class="sxs-lookup"><span data-stu-id="e77b8-140">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e77b8-141">Подключение по HTTP допустимо только в доверенных сетях.</span><span class="sxs-lookup"><span data-stu-id="e77b8-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="e77b8-142">Щелкните **Сохранить**, а затем щелкните **Да**, когда появится запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="e77b8-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="e77b8-143">Включение удаленного управления по протоколу HTTP с помощью последовательной консоли</span><span class="sxs-lookup"><span data-stu-id="e77b8-143">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="e77b8-144">Для включения удаленного управления выполните следующие действия в последовательной консоли устройства.</span><span class="sxs-lookup"><span data-stu-id="e77b8-144">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="e77b8-145">Включение удаленного управления с помощью последовательной консоли</span><span class="sxs-lookup"><span data-stu-id="e77b8-145">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="e77b8-146">В меню последовательной консоли выберите вариант 1.</span><span class="sxs-lookup"><span data-stu-id="e77b8-146">On the serial console menu, select option 1.</span></span> <span data-ttu-id="e77b8-147">Дополнительные сведения об использовании последовательной консоли устройства см. в статье [Подключение к Windows PowerShell для StorSimple через последовательную консоль устройства](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="e77b8-147">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="e77b8-148">В командной строке введите следующую команду: `Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="e77b8-148">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="e77b8-149">Вы получите уведомление об уязвимостях системы безопасности при подключении к устройству с помощью HTTP.</span><span class="sxs-lookup"><span data-stu-id="e77b8-149">You are notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="e77b8-150">При появлении запроса подтверждения введите **Y**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="e77b8-151">Убедитесь, что HTTP включен, набрав: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="e77b8-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="e77b8-152">Убедитесь, что значение поля **RemoteManagementMode** равно **HttpsAndHttpEnabled**. На следующем рисунке показаны эти параметры в PuTTY.</span><span class="sxs-lookup"><span data-stu-id="e77b8-152">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Последовательный HTTPS и HTTP включены](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="e77b8-154">Подготовка клиента для удаленного подключения</span><span class="sxs-lookup"><span data-stu-id="e77b8-154">Prepare the client for remote connection</span></span>
<span data-ttu-id="e77b8-155">Для включения удаленного управления выполните следующие действия в клиенте.</span><span class="sxs-lookup"><span data-stu-id="e77b8-155">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="e77b8-156">Подготовка клиента для удаленного подключения</span><span class="sxs-lookup"><span data-stu-id="e77b8-156">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="e77b8-157">Запустите сеанс Windows PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="e77b8-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="e77b8-158">Введите следующую команду, чтобы добавить IP-адрес устройства StorSimple в список доверенных узлов клиента:</span><span class="sxs-lookup"><span data-stu-id="e77b8-158">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="e77b8-159">Замените <*device_ip*> IP-адресом своего устройства, например:</span><span class="sxs-lookup"><span data-stu-id="e77b8-159">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="e77b8-160">Введите следующую команду, чтобы сохранить учетные данные устройства в переменной:</span><span class="sxs-lookup"><span data-stu-id="e77b8-160">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="e77b8-161">В открывшемся диалоговом окне:</span><span class="sxs-lookup"><span data-stu-id="e77b8-161">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="e77b8-162">Введите имя пользователя в следующем формате: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="e77b8-162">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="e77b8-163">Введите пароль администратора устройства, который был установлен при настройке устройства с помощью мастера установки.</span><span class="sxs-lookup"><span data-stu-id="e77b8-163">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="e77b8-164">Пароль по умолчанию — *Password1*.</span><span class="sxs-lookup"><span data-stu-id="e77b8-164">The default password is *Password1*.</span></span>
5. <span data-ttu-id="e77b8-165">Запустите сеанс Windows PowerShell на устройстве, введя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e77b8-165">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="e77b8-166">Чтобы создать сеанс Windows PowerShell для виртуального устройства StorSimple, добавьте параметр `–Port` и укажите общий порт, настроенный для удаленного взаимодействия с виртуальным устройством StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e77b8-166">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="e77b8-167">На этом этапе у вас должен быть активный удаленный сеанс Windows PowerShell с устройством.</span><span class="sxs-lookup"><span data-stu-id="e77b8-167">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
![Удаленное взаимодействие PowerShell через HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="e77b8-169">Подключение по протоколу HTTPS</span><span class="sxs-lookup"><span data-stu-id="e77b8-169">Connect through HTTPS</span></span>

<span data-ttu-id="e77b8-170">Подключение к Windows PowerShell для StorSimple через сеанс HTTPS — наиболее безопасный и рекомендуемый метод удаленного подключения к устройству Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e77b8-170">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="e77b8-171">В следующих процедурах описана настройка последовательной консоли и клиентских компьютеров для использования HTTPS для подключения к Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e77b8-171">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="e77b8-172">Для настройки удаленного управления можно использовать портал Azure или последовательную консоль.</span><span class="sxs-lookup"><span data-stu-id="e77b8-172">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="e77b8-173">Выберите одну из следующих процедур:</span><span class="sxs-lookup"><span data-stu-id="e77b8-173">Select from the following procedures:</span></span>

* [<span data-ttu-id="e77b8-174">Включение удаленного управления по протоколу HTTPS с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="e77b8-174">Use the Azure portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="e77b8-175">Включение удаленного управления по протоколу HTTPS с помощью последовательной консоли</span><span class="sxs-lookup"><span data-stu-id="e77b8-175">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="e77b8-176">После включения удаленного управления используйте следующие процедуры для подготовки узла для удаленного управления и подключения к устройству с удаленного узла.</span><span class="sxs-lookup"><span data-stu-id="e77b8-176">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="e77b8-177">Подготовка узла для удаленного управления</span><span class="sxs-lookup"><span data-stu-id="e77b8-177">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="e77b8-178">Подключение к устройству с удаленного узла</span><span class="sxs-lookup"><span data-stu-id="e77b8-178">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="e77b8-179">Включение удаленного управления по протоколу HTTPS с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="e77b8-179">Use the Azure portal to enable remote management over HTTPS</span></span>

<span data-ttu-id="e77b8-180">Чтобы включить удаленное управление по протоколу HTTPS, выполните следующие действия на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e77b8-180">Perform the following steps in the Azure portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-portal"></a><span data-ttu-id="e77b8-181">Включение удаленного управления по протоколу HTTPS на портале Azure</span><span class="sxs-lookup"><span data-stu-id="e77b8-181">To enable remote management over HTTPS from the Azure portal</span></span>

1. <span data-ttu-id="e77b8-182">Откройте службу диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e77b8-182">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="e77b8-183">Выберите **Устройства**, а затем щелкните устройство, на котором нужно настроить удаленное управление.</span><span class="sxs-lookup"><span data-stu-id="e77b8-183">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="e77b8-184">Последовательно выберите пункты **Параметры устройства > Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-184">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="e77b8-185">В колонке **Параметры безопасности** щелкните **Удаленное управление**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-185">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="e77b8-186">Задайте для пункта **Включить удаленное управление** значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-186">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="e77b8-187">Теперь вы можете выбрать подключение по HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e77b8-187">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="e77b8-188">(По умолчанию выбрано подключение по HTTPS.) Убедитесь, что выбран HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e77b8-188">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="e77b8-189">Щелкните многоточие (…), а затем выберите **Загрузить сертификат удаленного управления**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="e77b8-190">Укажите расположение для сохранения этого файла.</span><span class="sxs-lookup"><span data-stu-id="e77b8-190">Specify a location to save this file.</span></span> <span data-ttu-id="e77b8-191">Этот сертификат следует установить на компьютере клиента или узла, который будет использоваться для подключения к устройству.</span><span class="sxs-lookup"><span data-stu-id="e77b8-191">You need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="e77b8-192">Нажмите кнопку **Сохранить**, а затем щелкните **Да**, когда появится запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="e77b8-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="e77b8-193">Включение удаленного управления по протоколу HTTPS с помощью последовательной консоли</span><span class="sxs-lookup"><span data-stu-id="e77b8-193">Use the serial console to enable remote management over HTTPS</span></span>

<span data-ttu-id="e77b8-194">Для включения удаленного управления выполните следующие действия в последовательной консоли устройства.</span><span class="sxs-lookup"><span data-stu-id="e77b8-194">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="e77b8-195">Включение удаленного управления с помощью последовательной консоли</span><span class="sxs-lookup"><span data-stu-id="e77b8-195">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="e77b8-196">В меню последовательной консоли выберите вариант 1.</span><span class="sxs-lookup"><span data-stu-id="e77b8-196">On the serial console menu, select option 1.</span></span> <span data-ttu-id="e77b8-197">Дополнительные сведения об использовании последовательной консоли устройства см. в статье [Подключение к Windows PowerShell для StorSimple через последовательную консоль устройства](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="e77b8-197">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="e77b8-198">В командной строке введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e77b8-198">At the prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="e77b8-199">Эта команда должна включить протокол HTTPS на вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="e77b8-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="e77b8-200">Убедитесь, что HTTPS включен, набрав:</span><span class="sxs-lookup"><span data-stu-id="e77b8-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="e77b8-201">Убедитесь, что в поле **RemoteManagementMode** задано значение **HttpsEnabled**. На следующем рисунке показаны эти параметры в PuTTY.</span><span class="sxs-lookup"><span data-stu-id="e77b8-201">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Последовательный HTTPS включен](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="e77b8-203">Из вывода команды `Get-HcsSystem`скопируйте серийный номер устройства и сохраните его для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="e77b8-203">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e77b8-204">Серийный номер сопоставляется CN-имени в сертификате.</span><span class="sxs-lookup"><span data-stu-id="e77b8-204">The serial number maps to the CN name in the certificate.</span></span>
   
5. <span data-ttu-id="e77b8-205">Получите сертификат удаленного управления, набрав:</span><span class="sxs-lookup"><span data-stu-id="e77b8-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="e77b8-206">Появится сертификат, похожий на показанный ниже:</span><span class="sxs-lookup"><span data-stu-id="e77b8-206">A certificate similar to the following will appear.</span></span>
   
    ![Получение сертификата удаленного управления](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="e77b8-208">Скопируйте информацию из сертификата от **-----BEGIN CERTIFICATE-----** до **-----END CERTIFICATE-----** в текстовый редактор, например в "Блокнот", и сохраните файл в формате CER.</span><span class="sxs-lookup"><span data-stu-id="e77b8-208">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="e77b8-209">(При подготовке удаленного узла этот файл будет необходимо скопировать на этот узел.)</span><span class="sxs-lookup"><span data-stu-id="e77b8-209">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e77b8-210">Чтобы создать новый сертификат, используйте командлет `Set-HcsRemoteManagementCert`.</span><span class="sxs-lookup"><span data-stu-id="e77b8-210">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="e77b8-211">Подготовка узла для удаленного управления</span><span class="sxs-lookup"><span data-stu-id="e77b8-211">Prepare the host for remote management</span></span>

<span data-ttu-id="e77b8-212">Чтобы подготовить компьютер узла для удаленного подключения, которое использует сеанс HTTPS, выполните следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="e77b8-212">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="e77b8-213">[Импортируйте CER-файл в корневое хранилище клиента или удаленного узла](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="e77b8-213">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="e77b8-214">[Добавьте серийные номера устройств в файл hosts на удаленном узле](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="e77b8-214">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="e77b8-215">Каждая из этих процедур описана ниже.</span><span class="sxs-lookup"><span data-stu-id="e77b8-215">Each of the preceding procedures, is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="e77b8-216">Импорт сертификата на удаленном узле</span><span class="sxs-lookup"><span data-stu-id="e77b8-216">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="e77b8-217">Щелкните правой кнопкой мыши на CER-файле и выберите **Установить сертификат**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-217">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="e77b8-218">Откроется мастер импорта сертификатов.</span><span class="sxs-lookup"><span data-stu-id="e77b8-218">This starts the Certificate Import Wizard.</span></span>
   
    ![Мастер импорта сертификатов 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="e77b8-220">В качестве **Расположения хранилища** выберите **Локальный компьютер**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="e77b8-221">Выберите **Поместить все сертификаты в следующее хранилище**, затем нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-221">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="e77b8-222">Перейдите в корневое хранилище удаленного узла и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-222">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![Мастер импорта сертификатов 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="e77b8-224">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="e77b8-224">Click **Finish**.</span></span> <span data-ttu-id="e77b8-225">Появится сообщение о том, что импорт успешно выполнен.</span><span class="sxs-lookup"><span data-stu-id="e77b8-225">A message that tells you that the import was successful appears.</span></span>
   
    ![Мастер импорта сертификатов 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="e77b8-227">Добавление серийных номеров устройства в удаленный узел</span><span class="sxs-lookup"><span data-stu-id="e77b8-227">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="e77b8-228">Откройте "Блокнот" от имени администратора и откройте файл hosts, расположенный в папке \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="e77b8-228">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="e77b8-229">Добавьте следующие три записи в файл hosts: **IP-адрес данных 0**, **Фиксированный IP-адрес контроллера 0** и **Фиксированный IP-адрес контроллера 1**.</span><span class="sxs-lookup"><span data-stu-id="e77b8-229">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="e77b8-230">Введите серийный номер устройства, сохраненный ранее.</span><span class="sxs-lookup"><span data-stu-id="e77b8-230">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="e77b8-231">Сопоставьте его с IP-адресом, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="e77b8-231">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="e77b8-232">Для контроллера 0 и контроллера 1 добавьте **Controller0** и **Controller1** в конце серийного номера (CN-имени).</span><span class="sxs-lookup"><span data-stu-id="e77b8-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![Добавление имени CN в файл hosts](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="e77b8-234">Сохраните файл hosts.</span><span class="sxs-lookup"><span data-stu-id="e77b8-234">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="e77b8-235">Подключение к устройству с удаленного узла</span><span class="sxs-lookup"><span data-stu-id="e77b8-235">Connect to the device from the remote host</span></span>

<span data-ttu-id="e77b8-236">С помощью Windows PowerShell и SSL создайте сеанс SSAdmin на устройстве с удаленного узла или клиента.</span><span class="sxs-lookup"><span data-stu-id="e77b8-236">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="e77b8-237">Сеанс SSAdmin соответствует пункту 1 в меню [последовательной консоли](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) устройства.</span><span class="sxs-lookup"><span data-stu-id="e77b8-237">The SSAdmin session maps to option 1 in the [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="e77b8-238">Выполните следующую процедуру на компьютере, с которого будет выполняться удаленное подключение Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e77b8-238">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="e77b8-239">Создание сеанса SSAdmin на устройстве с помощью Windows PowerShell и SSL</span><span class="sxs-lookup"><span data-stu-id="e77b8-239">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="e77b8-240">Запустите сеанс Windows PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="e77b8-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="e77b8-241">Добавьте IP-адрес устройства в доверенные узлы клиента, набрав:</span><span class="sxs-lookup"><span data-stu-id="e77b8-241">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="e77b8-242">Замените <*device_ip*> IP-адресом своего устройства, например:</span><span class="sxs-lookup"><span data-stu-id="e77b8-242">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="e77b8-243">Чтобы создать новые учетные данные, введите:</span><span class="sxs-lookup"><span data-stu-id="e77b8-243">To create a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="e77b8-244">Где <*IP of target device*> — это IP-адрес DATA 0 вашего устройства, например, **10.126.173.90**, как показано на предыдущем рисунке файла hosts.</span><span class="sxs-lookup"><span data-stu-id="e77b8-244">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="e77b8-245">Также укажите пароль администратора для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="e77b8-245">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="e77b8-246">Создайте сеанс, набрав:</span><span class="sxs-lookup"><span data-stu-id="e77b8-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="e77b8-247">В качестве параметра -ComputerName в командлете введите <*серийный номер целевого устройства*>.</span><span class="sxs-lookup"><span data-stu-id="e77b8-247">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="e77b8-248">Этот серийный номер был сопоставлен с IP-адресом DATA 0 в файле hosts на удаленном узле. Пример — **SHX0991003G44MT**, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="e77b8-248">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="e77b8-249">Тип:</span><span class="sxs-lookup"><span data-stu-id="e77b8-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="e77b8-250">Необходимо подождать несколько минут, после чего вы будете подключены к устройству через HTTPS по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="e77b8-250">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="e77b8-251">Вы увидите сообщение о том, что вы подключены к устройству.</span><span class="sxs-lookup"><span data-stu-id="e77b8-251">You see a message that indicates you are connected to your device.</span></span>
   
    ![Удаленное взаимодействие PowerShell через HTTPS и SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="e77b8-253">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e77b8-253">Next steps</span></span>

* <span data-ttu-id="e77b8-254">Узнайте больше об [использовании Windows PowerShell для администрирования устройства StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e77b8-254">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="e77b8-255">Узнайте больше об [использовании службы диспетчера устройств StorSimple для администрирования устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e77b8-255">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

