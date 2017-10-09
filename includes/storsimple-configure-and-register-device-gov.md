<!--author=SharS last changed: 02/22/16-->

### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="64f62-101">tooconfigure и зарегистрировать устройство hello</span><span class="sxs-lookup"><span data-stu-id="64f62-101">tooconfigure and register hello device</span></span>
1. <span data-ttu-id="64f62-102">Доступ к интерфейсу Windows PowerShell hello в последовательной консоли устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="64f62-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="64f62-103">В разделе [последовательной консоли устройства toohello использование PuTTY tooconnect](#use-putty-to-connect-to-the-device-serial-console) инструкции.</span><span class="sxs-lookup"><span data-stu-id="64f62-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="64f62-104">**Полностью toofollow убедиться, что процедура hello или не будет возможности tooaccess hello консоли.**</span><span class="sxs-lookup"><span data-stu-id="64f62-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>
2. <span data-ttu-id="64f62-105">В сеансе hello, открывающемся нажмите клавишу ВВОД один раз tooget командную строку.</span><span class="sxs-lookup"><span data-stu-id="64f62-105">In hello session that opens up, press Enter one time tooget a command prompt.</span></span> 
3. <span data-ttu-id="64f62-106">Появится запрос toochoose hello язык, что tooset для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="64f62-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="64f62-107">Укажите язык hello и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="64f62-107">Specify hello language, and then press Enter.</span></span> 
   
    ![Настройка и регистрация StorSimple: устройство 1](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="64f62-109">В меню последовательной консоли hello, представленные выберите вариант 1 toolog на с полным доступом.</span><span class="sxs-lookup"><span data-stu-id="64f62-109">In hello serial console menu that is presented, choose option 1 toolog on with full access.</span></span> 
   
    ![Регистрация StorSimple: устройство 2](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="64f62-111">Выполните следующие шаги tooconfigure hello минимальные необходимые параметры сети для устройства hello.</span><span class="sxs-lookup"><span data-stu-id="64f62-111">Perform hello following steps tooconfigure hello minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="64f62-112">Эти шаги по настройке должны toobe блокировкой hello активного контроллера устройства hello.</span><span class="sxs-lookup"><span data-stu-id="64f62-112">These configuration steps need toobe performed on hello active controller of hello device.</span></span> <span data-ttu-id="64f62-113">меню последовательной консоли Hello указывает состояние контроллера hello в текст заголовка hello.</span><span class="sxs-lookup"><span data-stu-id="64f62-113">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="64f62-114">Если не являются подключиться toohello активный контроллер, отключитесь и подключитесь toohello активного контроллера.</span><span class="sxs-lookup"><span data-stu-id="64f62-114">If you are not connect toohello active controller, disconnect and then connect toohello active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="64f62-115">Hello командной строки введите пароль.</span><span class="sxs-lookup"><span data-stu-id="64f62-115">At hello command prompt, type your password.</span></span> <span data-ttu-id="64f62-116">пароль устройства по умолчанию Hello **Password1**.</span><span class="sxs-lookup"><span data-stu-id="64f62-116">hello default device password is **Password1**.</span></span>
   2. <span data-ttu-id="64f62-117">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="64f62-117">Type hello following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="64f62-118">Мастер установки появится toohelp, настроить параметры сети hello hello устройства.</span><span class="sxs-lookup"><span data-stu-id="64f62-118">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="64f62-119">Ввести hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="64f62-119">Supply hello following information:</span></span> 
      
      * <span data-ttu-id="64f62-120">IP-адрес для сетевого интерфейса DATA 0</span><span class="sxs-lookup"><span data-stu-id="64f62-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="64f62-121">Маска подсети</span><span class="sxs-lookup"><span data-stu-id="64f62-121">Subnet mask</span></span>
      * <span data-ttu-id="64f62-122">Шлюз</span><span class="sxs-lookup"><span data-stu-id="64f62-122">Gateway</span></span>
      * <span data-ttu-id="64f62-123">IP-адрес основного DNS-сервера</span><span class="sxs-lookup"><span data-stu-id="64f62-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="64f62-124">IP-адрес основного NTP-сервера</span><span class="sxs-lookup"><span data-stu-id="64f62-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="64f62-125">Toowait может иметь несколько минут для маски подсети hello и применения toobe параметры DNS.</span><span class="sxs-lookup"><span data-stu-id="64f62-125">You may have toowait for a few minutes for hello subnet mask and DNS settings toobe applied.</span></span> 
      > 
      > 
   4. <span data-ttu-id="64f62-126">(Необязательно.) Настройте прокси-сервер доступа в Интернет.</span><span class="sxs-lookup"><span data-stu-id="64f62-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="64f62-127">Хотя использовать прокси-сервер доступа в Интернет не обязательно, следует знать, что, если в вашей сети он имеется, настройку для работы с ним можно выполнить только в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="64f62-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="64f62-128">Дополнительные сведения см. слишком[Настройка веб-прокси для устройства](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="64f62-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span> 
      > 
      > 
6. <span data-ttu-id="64f62-129">Нажмите клавиши Ctrl + C мастер установки tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="64f62-129">Press Ctrl + C tooexit hello setup wizard.</span></span>
7. <span data-ttu-id="64f62-130">Установите обновления hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="64f62-130">Install hello updates as follows:</span></span>
   
   1. <span data-ttu-id="64f62-131">Используйте следующий командлет tooset IP-адресов на обоих контроллерах hello hello.</span><span class="sxs-lookup"><span data-stu-id="64f62-131">Use hello following cmdlet tooset IPs on both hello controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="64f62-132">Hello командной строки, выполнив `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="64f62-132">At hello command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="64f62-133">Вы должны получить уведомление о доступности обновлений.</span><span class="sxs-lookup"><span data-stu-id="64f62-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="64f62-134">Запустите `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="64f62-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="64f62-135">Эту команду можно выполнить на любом узле.</span><span class="sxs-lookup"><span data-stu-id="64f62-135">You can run this command on any node.</span></span> <span data-ttu-id="64f62-136">Обновления будут применяться на первом контроллере hello, выполнит переход контроллера hello и затем hello обновления будут применяться на hello другой контроллер.</span><span class="sxs-lookup"><span data-stu-id="64f62-136">Updates will be applied on hello first controller, hello controller will fail over, and then hello updates will be applied on hello other controller.</span></span>
      
      <span data-ttu-id="64f62-137">Можно следить за ходом hello hello обновления, запустив `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="64f62-137">You can monitor hello progress of hello update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="64f62-138">Hello следующий образец вывода показывает hello обновление выполняется.</span><span class="sxs-lookup"><span data-stu-id="64f62-138">hello following sample output shows hello update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      <span data-ttu-id="64f62-139">Следующий пример выходных данных Hello указывает, что завершения обновления hello.</span><span class="sxs-lookup"><span data-stu-id="64f62-139">hello following sample output indicates that hello update is finished.</span></span>
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      <span data-ttu-id="64f62-140">Это может потребоваться до too11 часы Здравствуйте, tooapply все hello обновлений, включая обновления Windows.</span><span class="sxs-lookup"><span data-stu-id="64f62-140">It may take up too11 hours tooapply all hello updates, including hello Windows Updates.</span></span>

8. <span data-ttu-id="64f62-141">После того как все hello обновления можно успешно установлена, запустите hello следующий командлет tooconfirm, Здравствуйте, правильно ли были применены обновления программного обеспечения:</span><span class="sxs-lookup"><span data-stu-id="64f62-141">After all hello updates are successfully installed, run hello following cmdlet tooconfirm that hello software updates were applied correctly:</span></span>
   
     `Get-HcsSystem`
   
    <span data-ttu-id="64f62-142">Вы должны увидеть следующие версии hello.</span><span class="sxs-lookup"><span data-stu-id="64f62-142">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="64f62-143">HcsSoftwareVersion: 6.3.9600.17491</span><span class="sxs-lookup"><span data-stu-id="64f62-143">HcsSoftwareVersion: 6.3.9600.17491</span></span>
   * <span data-ttu-id="64f62-144">CisAgentVersion: 1.0.9037.0</span><span class="sxs-lookup"><span data-stu-id="64f62-144">CisAgentVersion: 1.0.9037.0</span></span>
   * <span data-ttu-id="64f62-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="64f62-145">MdsAgentVersion: 26.0.4696.1433</span></span>
9. <span data-ttu-id="64f62-146">Верно ли был применен выполнения hello, выполнив командлет tooconfirm, hello обновление встроенного по:</span><span class="sxs-lookup"><span data-stu-id="64f62-146">Run hello following cmdlet tooconfirm that hello firmware update was applied correctly:</span></span>
   
    <span data-ttu-id="64f62-147">`Start-HcsFirmwareCheck`.</span><span class="sxs-lookup"><span data-stu-id="64f62-147">`Start-HcsFirmwareCheck`.</span></span>
   
     <span data-ttu-id="64f62-148">состояние Hello встроенное по должно быть **: UpToDate**.</span><span class="sxs-lookup"><span data-stu-id="64f62-148">hello firmware status should be **UpToDate**.</span></span>
10. <span data-ttu-id="64f62-149">Запустите hello, следуя портал Microsoft Azure для государственных toohello устройств hello командлет toopoint (так как он указывает toohello открытый классического портала Azure по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="64f62-149">Run hello following cmdlet toopoint hello device toohello Microsoft Azure Government portal (because it points toohello public Azure classic portal by default).</span></span> <span data-ttu-id="64f62-150">Оба контроллера будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="64f62-150">This will restart both controllers.</span></span> <span data-ttu-id="64f62-151">Рекомендуется использовать два сеанса PuTTY, toosimultaneously подключения tooboth контроллеров, чтобы вы могли видеть при перезапуске каждого контроллера.</span><span class="sxs-lookup"><span data-stu-id="64f62-151">We recommend that you use two PuTTY sessions toosimultaneously connect tooboth controllers so that you can see when each controller is restarted.</span></span>
    
     `Set-CloudPlatform -AzureGovt_US`
    
    <span data-ttu-id="64f62-152">Появится сообщение подтверждения.</span><span class="sxs-lookup"><span data-stu-id="64f62-152">You will see a confirmation message.</span></span> <span data-ttu-id="64f62-153">Примите значение по умолчанию hello (**Y**).</span><span class="sxs-lookup"><span data-stu-id="64f62-153">Accept hello default (**Y**).</span></span>
11. <span data-ttu-id="64f62-154">Выполните командлет tooresume установке hello.</span><span class="sxs-lookup"><span data-stu-id="64f62-154">Run hello following cmdlet tooresume setup:</span></span>
    
     `Invoke-HcsSetupWizard`
    
     ![Продолжение работы мастера установки](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    <span data-ttu-id="64f62-156">При возобновлении работы программы установки, мастер hello будет hello с обновлением 1 версии (соответствует tooversion 17469).</span><span class="sxs-lookup"><span data-stu-id="64f62-156">When you resume setup, hello wizard will be hello Update 1 version (which corresponds tooversion 17469).</span></span> 
12. <span data-ttu-id="64f62-157">Примите параметры сети hello.</span><span class="sxs-lookup"><span data-stu-id="64f62-157">Accept hello network settings.</span></span> <span data-ttu-id="64f62-158">Вы увидите сообщение проверки после принятия каждого параметра.</span><span class="sxs-lookup"><span data-stu-id="64f62-158">You will see a validation message after you accept each setting.</span></span>
13. <span data-ttu-id="64f62-159">В целях безопасности пароль администратора устройства hello срок действия истекает через hello первого сеанса, и нужно будет toochange теперь ИТ.</span><span class="sxs-lookup"><span data-stu-id="64f62-159">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="64f62-160">При выводе запроса задайте пароль администратора устройства.</span><span class="sxs-lookup"><span data-stu-id="64f62-160">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="64f62-161">Требуемая длина пароля администратора устройства от 8 до 15 символов.</span><span class="sxs-lookup"><span data-stu-id="64f62-161">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="64f62-162">Hello пароль должен содержать символы трех из следующих hello: нижнем регистре, верхнем регистре, цифры и специальные символы.</span><span class="sxs-lookup"><span data-stu-id="64f62-162">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![Регистрация StorSimple: устройство 5](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. <span data-ttu-id="64f62-164">Последний шаг мастера установки hello Hello регистрирует устройство hello в службе StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="64f62-164">hello final step in hello setup wizard registers your device with hello StorSimple Manager service.</span></span> <span data-ttu-id="64f62-165">Для этого вам будет необходимо hello регистрационный ключ службы, полученный в [шаг 2: ключ регистрации службы hello Get](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="64f62-165">For this, you will need hello service registration key that you obtained in [Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="64f62-166">После ввода ключа регистрации hello, может понадобиться toowait 2-3 минуты до регистрации устройства hello.</span><span class="sxs-lookup"><span data-stu-id="64f62-166">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="64f62-167">В любое время мастер установки hello tooexit можно нажать клавиши Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="64f62-167">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="64f62-168">Если введено все параметры сети hello (IP-адрес Data 0, маску подсети и шлюз) записей будут сохранены.</span><span class="sxs-lookup"><span data-stu-id="64f62-168">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Ход выполнения регистрации StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. <span data-ttu-id="64f62-170">После регистрации устройства hello отображается ключ шифрования данных службы.</span><span class="sxs-lookup"><span data-stu-id="64f62-170">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="64f62-171">Скопируйте этот ключ и сохраните его в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="64f62-171">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="64f62-172">**Этот ключ потребуется с hello службы регистрации ключа tooregister дополнительных устройств с hello в службе StorSimple Manager.**</span><span class="sxs-lookup"><span data-stu-id="64f62-172">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Manager service.**</span></span> <span data-ttu-id="64f62-173">См. слишком[безопасность StorSimple](../articles/storsimple/storsimple-security.md) Дополнительные сведения об этом ключе.</span><span class="sxs-lookup"><span data-stu-id="64f62-173">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Регистрация StorSimple: устройство 7](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="64f62-175">текст hello toocopy из окна последовательной консоли hello, просто выделите текст hello.</span><span class="sxs-lookup"><span data-stu-id="64f62-175">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="64f62-176">Затем можно будет toopaste его в буфер обмена hello или любой текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="64f62-176">You should then be able toopaste it in hello clipboard or any text editor.</span></span> 
    > 
    > <span data-ttu-id="64f62-177">НЕ используйте сочетание клавиш Ctrl + C toocopy hello ключа шифрования.</span><span class="sxs-lookup"><span data-stu-id="64f62-177">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="64f62-178">С помощью клавиши Ctrl + C вызовет вы tooexit приветствия мастера установки.</span><span class="sxs-lookup"><span data-stu-id="64f62-178">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="64f62-179">В результате пароль администратора устройства hello не будут изменены и hello устройство вернется toohello пароль по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="64f62-179">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    > 
    > 
16. <span data-ttu-id="64f62-180">Выход hello последовательной консоли.</span><span class="sxs-lookup"><span data-stu-id="64f62-180">Exit hello serial console.</span></span>
17. <span data-ttu-id="64f62-181">Вернитесь toohello государственных портал Azure и завершите hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="64f62-181">Return toohello Azure Government Portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="64f62-182">Дважды щелкните вашей hello tooaccess службы диспетчера StorSimple **быстрый запуск** страницы.</span><span class="sxs-lookup"><span data-stu-id="64f62-182">Double-click your StorSimple Manager service tooaccess hello **Quick Start** page.</span></span>
    2. <span data-ttu-id="64f62-183">Щелкните **Просмотр подключенных устройств**.</span><span class="sxs-lookup"><span data-stu-id="64f62-183">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="64f62-184">На hello **устройств** проверьте hello устройства успешно подключен toohello службы путем поиска информации о состоянии hello.</span><span class="sxs-lookup"><span data-stu-id="64f62-184">On hello **Devices** page, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="64f62-185">Состояние устройства Hello должно быть **Online**.</span><span class="sxs-lookup"><span data-stu-id="64f62-185">hello device status should be **Online**.</span></span>
       
        ![Страница устройств StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        <span data-ttu-id="64f62-187">Если состояние устройства hello **Offline**, подождите несколько минут для hello toocome устройства через Интернет.</span><span class="sxs-lookup"><span data-stu-id="64f62-187">If hello device status is **Offline**, wait for a couple of minutes for hello device toocome online.</span></span> 
       
        <span data-ttu-id="64f62-188">Если устройство hello еще в автономном режиме, через несколько минут, то необходимо убедиться, что брандмауэр сети была настроена, как описано в toomake [требования к сети для устройства StorSimple](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="64f62-188">If hello device is still offline after a few minutes, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span> 
       
        <span data-ttu-id="64f62-189">Убедитесь, что порт 9354 открыт для исходящей связи используется hello служебной шины для диспетчера StorSimple устройство службы связи.</span><span class="sxs-lookup"><span data-stu-id="64f62-189">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Manager service-to-device communication.</span></span>

