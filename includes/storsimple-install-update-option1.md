<!--author=SharS last changed: 03/17/2016-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="b9acf-101">Загрузка исправления</span><span class="sxs-lookup"><span data-stu-id="b9acf-101">To download hotfixes</span></span>
<span data-ttu-id="b9acf-102">Для загрузки обновления программного обеспечения выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b9acf-102">Perform the following steps to download the software update.</span></span>

1. <span data-ttu-id="b9acf-103">Запустите Internet Explorer и откройте страницу [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b9acf-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="b9acf-104">Если вы впервые используете каталог Центра обновления Майкрософт на этом компьютере, нажмите кнопку **Установить** , когда будет предложено установить надстройку каталога Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b9acf-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="b9acf-105">![Установка каталога](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="b9acf-105">![Install catalog](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="b9acf-106">В поле поиска каталога Центра обновления Майкрософт введите номер необходимого исправления в базе знаний, например **3063418**, а затем нажмите кнопку **Найти**.</span><span class="sxs-lookup"><span data-stu-id="b9acf-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3063418**, and then click **Search**.</span></span>
4. <span data-ttu-id="b9acf-107">Вы увидите пакет **StorSimple Update 1.2 Appliance Update** .</span><span class="sxs-lookup"><span data-stu-id="b9acf-107">You will see the **StorSimple Update 1.2 Appliance Update** bundle.</span></span> <span data-ttu-id="b9acf-108">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b9acf-108">Click **Add**.</span></span> <span data-ttu-id="b9acf-109">Пакет обновлений будет добавлен в вашу корзину.</span><span class="sxs-lookup"><span data-stu-id="b9acf-109">The update will be added to the basket.</span></span>
5. <span data-ttu-id="b9acf-110">Найдите дополнительные исправления, перечисленные в приведенной выше таблице (**3043005** и **3063416**), и добавьте каждое из них в корзину.</span><span class="sxs-lookup"><span data-stu-id="b9acf-110">Search for any additional hotfixes listed in the table above (**3043005** and **3063416**), and add each the basket.</span></span>
6. <span data-ttu-id="b9acf-111">Щелкните **Просмотреть корзину**.</span><span class="sxs-lookup"><span data-stu-id="b9acf-111">Click **View Basket**.</span></span>
   
    ![Просмотреть корзину](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. <span data-ttu-id="b9acf-113">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="b9acf-113">Click **Download**.</span></span> <span data-ttu-id="b9acf-114">Укажите или **выберите** локальное расположение, в которое хотите скачать файлы.</span><span class="sxs-lookup"><span data-stu-id="b9acf-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="b9acf-115">Обновления скачиваются в указанное расположение и помещаются во вложенную папку с тем же именем, что и имя обновления.</span><span class="sxs-lookup"><span data-stu-id="b9acf-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="b9acf-116">Этот каталог также можно скопировать в сетевую папку, которая доступна с вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="b9acf-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="b9acf-117">Исправления должны быть доступны с обоих контроллеров, чтобы можно было получить любые возможные сообщения об ошибке от однорангового контроллера.</span><span class="sxs-lookup"><span data-stu-id="b9acf-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="b9acf-118">Установка и проверка исправлений обычного режима</span><span class="sxs-lookup"><span data-stu-id="b9acf-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="b9acf-119">Выполните следующие действия для установки и проверки обычных исправлений.</span><span class="sxs-lookup"><span data-stu-id="b9acf-119">Perform the following steps to install and verify the regular-mode hotfixes.</span></span> <span data-ttu-id="b9acf-120">Если вы уже установили их с помощью портала Azure, перейдите к [установке и проверке исправлений режима обслуживания](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="b9acf-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="b9acf-121">Чтобы установить обновление для ПО, откройте интерфейс Windows PowerShell на последовательной консоли своего устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b9acf-121">To install the software update, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="b9acf-122">Подробные инструкции см. в разделе [Подключение к последовательной консоли устройства с помощью PuTTY](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b9acf-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="b9acf-123">В командной строке нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="b9acf-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="b9acf-124">Выберите **Вариант 1** , чтобы войти на устройство с правами на полный доступ.</span><span class="sxs-lookup"><span data-stu-id="b9acf-124">Select **Option 1** to log on to the device with full access.</span></span>
3. <span data-ttu-id="b9acf-125">Чтобы установить пакет обновления, в командной строке введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b9acf-125">To install the update package, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="b9acf-126">В указанной выше команде вместо DNS в адресе общей папки укажите IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="b9acf-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="b9acf-127">Параметр "credential" используется только для доступа к общему ресурсу с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="b9acf-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="b9acf-128">Для доступа к общим ресурсам рекомендуем использовать параметр учетных данных.</span><span class="sxs-lookup"><span data-stu-id="b9acf-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="b9acf-129">Даже те общие ресурсы, которые доступны для всех, обычно закрыты для пользователей, не прошедших проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b9acf-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="b9acf-130">Пример выходных данных этой команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="b9acf-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="b9acf-131">Введите **Y** , когда будет предложено подтвердить установку исправлений.</span><span class="sxs-lookup"><span data-stu-id="b9acf-131">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="b9acf-132">Проверьте обновление с помощью командлета `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="b9acf-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="b9acf-133">Ниже приведен пример выходных данных для обновления, которое выполняется.</span><span class="sxs-lookup"><span data-stu-id="b9acf-133">The following sample output shows the update in progress.</span></span> <span data-ttu-id="b9acf-134">Пока обновление выполняется, `RunInprogress` будет иметь значение `True`.</span><span class="sxs-lookup"><span data-stu-id="b9acf-134">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="b9acf-135">Ниже приведен пример выходных данных для обновления, установка которого завершена.</span><span class="sxs-lookup"><span data-stu-id="b9acf-135">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="b9acf-136">После установки обновления `RunInProgress` будет иметь значение `False`.</span><span class="sxs-lookup"><span data-stu-id="b9acf-136">The `RunInProgress` will be `False` when the update has completed.</span></span>

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="b9acf-137">В некоторых случаях командлет выдает значение `False`, пока обновление еще устанавливается.</span><span class="sxs-lookup"><span data-stu-id="b9acf-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="b9acf-138">Чтобы проверить установку обновления, подождите несколько минут, выполните эту команду еще раз и убедитесь в том, что `RunInProgress` имеет значение `False`.</span><span class="sxs-lookup"><span data-stu-id="b9acf-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="b9acf-139">Если это так, значит, исправление установлено.</span><span class="sxs-lookup"><span data-stu-id="b9acf-139">If it is, then the hotfix has completed.</span></span>
   > 
   > 
6. <span data-ttu-id="b9acf-140">Когда установка обновления будет завершена, проверьте версии программного обеспечения системы.</span><span class="sxs-lookup"><span data-stu-id="b9acf-140">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="b9acf-141">Введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b9acf-141">Type the following command:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="b9acf-142">Номера версий должны быть следующими:</span><span class="sxs-lookup"><span data-stu-id="b9acf-142">You should see the following versions:</span></span>
   
   * <span data-ttu-id="b9acf-143">HcsSoftwareVersion: 6.3.9600.17584</span><span class="sxs-lookup"><span data-stu-id="b9acf-143">HcsSoftwareVersion: 6.3.9600.17584</span></span>
   * <span data-ttu-id="b9acf-144">CisAgentVersion: 1.0.9049.0</span><span class="sxs-lookup"><span data-stu-id="b9acf-144">CisAgentVersion: 1.0.9049.0</span></span>
   * <span data-ttu-id="b9acf-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="b9acf-145">MdsAgentVersion: 26.0.4696.1433</span></span>
     
     <span data-ttu-id="b9acf-146">Если после установки обновления номера версий не изменились, значит, исправление установить не удалось.</span><span class="sxs-lookup"><span data-stu-id="b9acf-146">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="b9acf-147">В этом случае обратитесь за дополнительной помощью в [службу поддержки Майкрософт](../articles/storsimple/storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b9acf-147">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
7. <span data-ttu-id="b9acf-148">Повторите шаги 3–5, чтобы установить оставшееся обычное исправление (KB3043005).</span><span class="sxs-lookup"><span data-stu-id="b9acf-148">Repeat steps 3-5 to install the remaining regular-mode hotfix (KB3043005).</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="b9acf-149">Установка и проверка исправлений режима обслуживания</span><span class="sxs-lookup"><span data-stu-id="b9acf-149">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="b9acf-150">Используйте KB3063416, чтобы установить обновления встроенного ПО дисков.</span><span class="sxs-lookup"><span data-stu-id="b9acf-150">Use KB3063416 to install disk firmware updates.</span></span> <span data-ttu-id="b9acf-151">Эти обновления прерывают работу, и на их завершение может потребоваться около 30–45 минут.</span><span class="sxs-lookup"><span data-stu-id="b9acf-151">These are disruptive updates and take around 30-45 minutes to complete.</span></span> <span data-ttu-id="b9acf-152">Данные обновления можно установить в период планового техобслуживания, подключившись к последовательной консоли устройства.</span><span class="sxs-lookup"><span data-stu-id="b9acf-152">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="b9acf-153">Чтобы установить обновления встроенного ПО диска, следуйте приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="b9acf-153">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="b9acf-154">Переведите устройство в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b9acf-154">Place the device in Maintenance mode.</span></span> <span data-ttu-id="b9acf-155">Обратите внимание, что не следует использовать удаленное взаимодействие Windows PowerShell при переключении устройства в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b9acf-155">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="b9acf-156">При подключении через последовательную консоль устройства необходимо будет выполнить этот командлет на контроллере устройства.</span><span class="sxs-lookup"><span data-stu-id="b9acf-156">You will need to run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="b9acf-157">Тип:</span><span class="sxs-lookup"><span data-stu-id="b9acf-157">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="b9acf-158">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="b9acf-158">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="b9acf-159">После этого оба контроллера перезапускаются и переходят в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b9acf-159">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="b9acf-160">Чтобы установить обновление встроенного ПО диска, введите:</span><span class="sxs-lookup"><span data-stu-id="b9acf-160">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="b9acf-161">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="b9acf-161">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="b9acf-162">Отслеживайте ход выполнения установки с помощью команды `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="b9acf-162">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="b9acf-163">Обновление завершится, когда `RunInProgress` поменяется на `False`.</span><span class="sxs-lookup"><span data-stu-id="b9acf-163">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="b9acf-164">После завершения установки будет перезагружен контроллер, на котором установлено исправление режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b9acf-164">After the installation is complete, the controller on which the maintenance mode hotfix was installed will be rebooted.</span></span> <span data-ttu-id="b9acf-165">В качестве варианта 1 войдите в систему с полным доступом и проверьте версию встроенного ПО диска.</span><span class="sxs-lookup"><span data-stu-id="b9acf-165">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="b9acf-166">Тип:</span><span class="sxs-lookup"><span data-stu-id="b9acf-166">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="b9acf-167">Ожидаемые версии встроенного ПО диска:</span><span class="sxs-lookup"><span data-stu-id="b9acf-167">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   <span data-ttu-id="b9acf-168">Выполните команду `Get-HcsFirmwareVersion` на втором контроллере, чтобы проверить обновление версии программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="b9acf-168">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="b9acf-169">Затем можно выйти из режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b9acf-169">You can then exit the maintenance mode.</span></span> <span data-ttu-id="b9acf-170">Введите следующую команду для каждого контроллера устройства:</span><span class="sxs-lookup"><span data-stu-id="b9acf-170">Type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="b9acf-171">При выходе из режима обслуживания контроллеры перезапускаются.</span><span class="sxs-lookup"><span data-stu-id="b9acf-171">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="b9acf-172">Когда обновления встроенного ПО диска будут успешно установлены, а устройство будет выведено из режима обслуживания, вернитесь в классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b9acf-172">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="b9acf-173">Обратите внимание, что для отображения установленных обновлений режима обслуживания на портале может потребоваться до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="b9acf-173">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

