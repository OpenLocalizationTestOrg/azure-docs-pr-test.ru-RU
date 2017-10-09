<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="d85e4-101">tooconfigure и зарегистрировать устройство hello</span><span class="sxs-lookup"><span data-stu-id="d85e4-101">tooconfigure and register hello device</span></span>

1. <span data-ttu-id="d85e4-102">Доступ к интерфейсу Windows PowerShell hello в последовательной консоли устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d85e4-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="d85e4-103">В разделе [последовательной консоли устройства toohello использование PuTTY tooconnect](#use-putty-to-connect-to-the-device-serial-console) инструкции.</span><span class="sxs-lookup"><span data-stu-id="d85e4-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="d85e4-104">**Полностью toofollow убедиться, что процедура hello или не будет возможности tooaccess hello консоли.**</span><span class="sxs-lookup"><span data-stu-id="d85e4-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>

2. <span data-ttu-id="d85e4-105">В сеансе hello, открывающемся, клавишу **ввод** один раз tooget командную строку.</span><span class="sxs-lookup"><span data-stu-id="d85e4-105">In hello session that opens up, press **Enter** one time tooget a command prompt.</span></span>

3. <span data-ttu-id="d85e4-106">Появится запрос toochoose hello язык, что tooset для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="d85e4-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="d85e4-107">Указать язык hello и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="d85e4-107">Specify hello language, and then press **Enter**.</span></span>

4. <span data-ttu-id="d85e4-108">В меню последовательной консоли hello, представленными в, выберите параметр 1 слишком**войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="d85e4-108">In hello serial console menu that is presented, choose option 1 too**log in with full access**.</span></span>
     <span data-ttu-id="d85e4-109">Выполните шаги с 5-12 tooconfigure hello минимальные необходимые параметры сети для устройства.</span><span class="sxs-lookup"><span data-stu-id="d85e4-109">Complete steps 5-12 tooconfigure hello minimum required network settings for your device.</span></span> <span data-ttu-id="d85e4-110">**Эти шаги по настройке должны toobe блокировкой hello активного контроллера устройства hello.**</span><span class="sxs-lookup"><span data-stu-id="d85e4-110">**These configuration steps need toobe performed on hello active controller of hello device.**</span></span> <span data-ttu-id="d85e4-111">меню последовательной консоли Hello указывает состояние контроллера hello в текст заголовка hello.</span><span class="sxs-lookup"><span data-stu-id="d85e4-111">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="d85e4-112">Если вы не подключены toohello активный контроллер, отключите и подключите toohello активного контроллера.</span><span class="sxs-lookup"><span data-stu-id="d85e4-112">If you are not connected toohello active controller, disconnect and then connect toohello active controller.</span></span>

5. <span data-ttu-id="d85e4-113">Hello командной строки введите пароль.</span><span class="sxs-lookup"><span data-stu-id="d85e4-113">At hello command prompt, type your password.</span></span> <span data-ttu-id="d85e4-114">пароль устройства по умолчанию Hello **Password1**.</span><span class="sxs-lookup"><span data-stu-id="d85e4-114">hello default device password is **Password1**.</span></span>

6. <span data-ttu-id="d85e4-115">Тип hello следующую команду: `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="d85e4-115">Type hello following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="d85e4-116">Мастер установки появится toohelp, настроить параметры сети hello hello устройства.</span><span class="sxs-lookup"><span data-stu-id="d85e4-116">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="d85e4-117">Ввести hello hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="d85e4-117">Supply hello hello following information:</span></span>
   
   * <span data-ttu-id="d85e4-118">IP-адрес для hello сетевого интерфейса DATA 0</span><span class="sxs-lookup"><span data-stu-id="d85e4-118">IP address for hello DATA 0 network interface</span></span>
   * <span data-ttu-id="d85e4-119">Маска подсети</span><span class="sxs-lookup"><span data-stu-id="d85e4-119">Subnet mask</span></span>
   * <span data-ttu-id="d85e4-120">Шлюз</span><span class="sxs-lookup"><span data-stu-id="d85e4-120">Gateway</span></span>
   * <span data-ttu-id="d85e4-121">IP-адрес основного DNS-сервера</span><span class="sxs-lookup"><span data-stu-id="d85e4-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="d85e4-122">Ниже приведен пример выходных данных.</span><span class="sxs-lookup"><span data-stu-id="d85e4-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="d85e4-123">В hello предшествующий пример выходных данных вы увидите, что системы hello проверке параметров сети после каждого шага в процессе hello.</span><span class="sxs-lookup"><span data-stu-id="d85e4-123">In hello preceding sample output, you can see that hello system is validating network settings after each step in hello process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="d85e4-124">Toowait может иметь несколько минут для маски подсети hello и применены параметры toobe с DNS hello.</span><span class="sxs-lookup"><span data-stu-id="d85e4-124">You may have toowait for a few minutes for hello subnet mask and hello DNS settings toobe applied.</span></span> <span data-ttu-id="d85e4-125">Если появляется сообщение об ошибке «Проверка hello сетевого подключения tooData 0», проверьте hello физическое подключение hello сетевого интерфейса DATA 0 вашего используемого контроллера.</span><span class="sxs-lookup"><span data-stu-id="d85e4-125">If you get a "Check hello network connectivity tooData 0" error message, check hello physical network connection on hello DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="d85e4-126">(Необязательно.) Настройте прокси-сервер доступа в Интернет.</span><span class="sxs-lookup"><span data-stu-id="d85e4-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="d85e4-127">Хотя использовать веб-прокси не обязательно, **следует знать, что, если в вашей сети имеется веб-прокси, настройку для работы с ним можно выполнить только в этом разделе**.</span><span class="sxs-lookup"><span data-stu-id="d85e4-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="d85e4-128">Дополнительные сведения см. слишком[Настройка веб-прокси для устройства](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="d85e4-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="d85e4-129">Настройте основной NTP-сервер для своего устройства.</span><span class="sxs-lookup"><span data-stu-id="d85e4-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="d85e4-130">NTP-серверы необходимы, так как ваше устройство должно синхронизироваться по времени, чтобы оно могло проверять подлинность с вашими поставщиками облачных служб.</span><span class="sxs-lookup"><span data-stu-id="d85e4-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="d85e4-131">Убедитесь, что ваша сеть позволяет toopass трафик NTP из вашего центра обработки данных toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="d85e4-131">Ensure that your network allows NTP traffic toopass from your datacenter toohello Internet.</span></span> <span data-ttu-id="d85e4-132">Если это невозможно, укажите внутренний NTP-сервер.</span><span class="sxs-lookup"><span data-stu-id="d85e4-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="d85e4-133">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="d85e4-133">A sample output is shown below.</span></span>

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="d85e4-134">В целях безопасности пароль администратора устройства hello срок действия истекает через hello первого сеанса, и нужно будет toochange теперь ИТ.</span><span class="sxs-lookup"><span data-stu-id="d85e4-134">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="d85e4-135">При выводе запроса задайте пароль администратора устройства.</span><span class="sxs-lookup"><span data-stu-id="d85e4-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="d85e4-136">Требуемая длина пароля администратора устройства от 8 до 15 символов.</span><span class="sxs-lookup"><span data-stu-id="d85e4-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="d85e4-137">Hello пароль должен содержать символы трех из следующих hello: нижнем регистре, верхнем регистре, цифры и специальные символы.</span><span class="sxs-lookup"><span data-stu-id="d85e4-137">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="d85e4-138">Последний шаг мастера установки hello Hello регистрирует устройство hello службы диспетчера StorSimple устройство.</span><span class="sxs-lookup"><span data-stu-id="d85e4-138">hello final step in hello setup wizard registers your device with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="d85e4-139">Для этого потребуется ключ регистрации службы hello, полученный на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="d85e4-139">For this, you will need hello service registration key that you obtained in step 2.</span></span> <span data-ttu-id="d85e4-140">После ввода ключа регистрации hello, может понадобиться toowait 2-3 минуты до регистрации устройства hello.</span><span class="sxs-lookup"><span data-stu-id="d85e4-140">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="d85e4-141">В любое время мастер установки hello tooexit можно нажать клавиши Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="d85e4-141">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="d85e4-142">Если введено все параметры сети hello (IP-адрес Data 0, маску подсети и шлюз) записей будут сохранены.</span><span class="sxs-lookup"><span data-stu-id="d85e4-142">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="d85e4-143">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="d85e4-143">A sample output is shown below.</span></span>

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="d85e4-144">После регистрации устройства hello отображается ключ шифрования данных службы.</span><span class="sxs-lookup"><span data-stu-id="d85e4-144">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="d85e4-145">Скопируйте этот ключ и сохраните его в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="d85e4-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="d85e4-146">**Этот ключ потребуется с hello службы регистрации ключа tooregister дополнительных устройств с hello службы диспетчера StorSimple устройство.**</span><span class="sxs-lookup"><span data-stu-id="d85e4-146">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Device Manager service.**</span></span> <span data-ttu-id="d85e4-147">См. слишком[безопасность StorSimple](../articles/storsimple/storsimple-security.md) Дополнительные сведения об этом ключе.</span><span class="sxs-lookup"><span data-stu-id="d85e4-147">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Регистрация StorSimple: устройство 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="d85e4-149">текст hello toocopy из окна последовательной консоли hello, просто выделите текст hello.</span><span class="sxs-lookup"><span data-stu-id="d85e4-149">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="d85e4-150">Затем можно будет toopaste его в буфер обмена hello или любой текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="d85e4-150">You should then be able toopaste it in hello clipboard or any text editor.</span></span> <span data-ttu-id="d85e4-151">НЕ используйте сочетание клавиш Ctrl + C toocopy hello ключа шифрования.</span><span class="sxs-lookup"><span data-stu-id="d85e4-151">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="d85e4-152">С помощью клавиши Ctrl + C вызовет вы tooexit приветствия мастера установки.</span><span class="sxs-lookup"><span data-stu-id="d85e4-152">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="d85e4-153">В результате пароль администратора устройства hello не будут изменены и hello устройство вернется toohello пароль по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d85e4-153">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    
13. <span data-ttu-id="d85e4-154">Выход hello последовательной консоли.</span><span class="sxs-lookup"><span data-stu-id="d85e4-154">Exit hello serial console.</span></span>
14. <span data-ttu-id="d85e4-155">Получите toohello портал Azure и выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="d85e4-155">Return toohello Azure portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="d85e4-156">Перейдите в службе диспетчера StorSimple устройство tooyour.</span><span class="sxs-lookup"><span data-stu-id="d85e4-156">Go tooyour StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="d85e4-157">Щелкните **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="d85e4-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="d85e4-158">Hello табличный список устройств убедитесь, что в это устройство hello успешно подключен toohello службы путем поиска информации о состоянии hello.</span><span class="sxs-lookup"><span data-stu-id="d85e4-158">In hello tabular listing of devices, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="d85e4-159">Состояние устройства Hello должно быть **готов tooset копирование**.</span><span class="sxs-lookup"><span data-stu-id="d85e4-159">hello device status should be **Ready tooset up**.</span></span>
       
        ![Страница устройств StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="d85e4-161">Может потребоваться toowait для несколько минут для toochange состояние устройства hello слишком**готов tooset копирование**.</span><span class="sxs-lookup"><span data-stu-id="d85e4-161">You may need toowait for a couple of minutes for hello device status toochange too**Ready tooset up**.</span></span>
       
        <span data-ttu-id="d85e4-162">Если hello устройство не отображается в этом списке, то вы должны убедиться, что брандмауэр сети была настроена, как описано в toomake [требования к сети для устройства StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="d85e4-162">If hello device does not show up in this list, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="d85e4-163">Убедитесь, что порт 9354 открыт для исходящей связи используется hello служебной шины для устройства StorSimple устройство службы связи.</span><span class="sxs-lookup"><span data-stu-id="d85e4-163">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Device Manager service-to-device communication.</span></span>

