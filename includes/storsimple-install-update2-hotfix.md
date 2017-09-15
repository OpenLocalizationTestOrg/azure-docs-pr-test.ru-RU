<!--author=alkohli last changed: 03/17/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="bdc13-101">Загрузка исправления</span><span class="sxs-lookup"><span data-stu-id="bdc13-101">To download hotfixes</span></span>
<span data-ttu-id="bdc13-102">Для загрузки обновления программного обеспечения из каталога обновления Майкрософт выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bdc13-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="bdc13-103">Запустите Internet Explorer и откройте страницу [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="bdc13-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="bdc13-104">Если вы впервые используете каталог Центра обновления Майкрософт на этом компьютере, нажмите кнопку **Установить** , когда будет предложено установить надстройку каталога Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="bdc13-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="bdc13-105">![Установка каталога](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="bdc13-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="bdc13-106">В поле поиска каталога Центра обновления Майкрософт введите номер необходимого исправления в базе знаний, например **3121901**, а затем нажмите кнопку **Найти**.</span><span class="sxs-lookup"><span data-stu-id="bdc13-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3121901**, and then click **Search**.</span></span>
   
    <span data-ttu-id="bdc13-107">Появится список исправлений, например **Совокупное обновление программного обеспечения версии 2.0 для StorSimple серии 8000**.</span><span class="sxs-lookup"><span data-stu-id="bdc13-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.0 for StorSimple 8000 Series**.</span></span>
   
    ![Поиск в каталоге](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="bdc13-109">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bdc13-109">Click **Add**.</span></span> <span data-ttu-id="bdc13-110">Обновление будет добавлено в корзину.</span><span class="sxs-lookup"><span data-stu-id="bdc13-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="bdc13-111">Найдите дополнительные исправления, перечисленные в приведенной выше таблице (**3121900**, **3080728**, **3090322** и **3121899**), и добавьте каждое из них в корзину.</span><span class="sxs-lookup"><span data-stu-id="bdc13-111">Search for any additional hotfixes listed in the table above (**3121900**, **3080728**, **3090322**, and **3121899**), and add each the basket.</span></span>
6. <span data-ttu-id="bdc13-112">Щелкните **Просмотреть корзину**.</span><span class="sxs-lookup"><span data-stu-id="bdc13-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="bdc13-113">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="bdc13-113">Click **Download**.</span></span> <span data-ttu-id="bdc13-114">Укажите или **выберите** локальное расположение, в которое хотите скачать файлы.</span><span class="sxs-lookup"><span data-stu-id="bdc13-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="bdc13-115">Обновления скачиваются в указанное расположение и помещаются во вложенную папку с тем же именем, что и имя обновления.</span><span class="sxs-lookup"><span data-stu-id="bdc13-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="bdc13-116">Этот каталог также можно скопировать в сетевую папку, которая доступна с вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="bdc13-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="bdc13-117">Исправления должны быть доступны с обоих контроллеров, чтобы можно было получить любые возможные сообщения об ошибке от однорангового контроллера.</span><span class="sxs-lookup"><span data-stu-id="bdc13-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="bdc13-118">Установка и проверка исправлений обычного режима</span><span class="sxs-lookup"><span data-stu-id="bdc13-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="bdc13-119">Выполните следующие действия для установки и проверки обычных исправлений.</span><span class="sxs-lookup"><span data-stu-id="bdc13-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="bdc13-120">Если вы уже установили их с помощью портала Azure, перейдите к [установке и проверке исправлений режима обслуживания](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="bdc13-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="bdc13-121">Чтобы установить исправления, откройте интерфейс Windows PowerShell на последовательной консоли своего устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bdc13-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="bdc13-122">Подробные инструкции см. в разделе [Подключение к последовательной консоли устройства с помощью PuTTY](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="bdc13-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="bdc13-123">В командной строке нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="bdc13-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="bdc13-124">Выберите **Вариант 1** , чтобы войти на устройство с правами на полный доступ.</span><span class="sxs-lookup"><span data-stu-id="bdc13-124">Select **Option 1** to log on to the device with full access.</span></span>
3. <span data-ttu-id="bdc13-125">Чтобы установить исправление, в командной строке введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bdc13-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="bdc13-126">В указанной выше команде вместо DNS в адресе общей папки укажите IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="bdc13-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="bdc13-127">Параметр "credential" используется только для доступа к общему ресурсу с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="bdc13-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="bdc13-128">Для доступа к общим ресурсам рекомендуем использовать параметр учетных данных.</span><span class="sxs-lookup"><span data-stu-id="bdc13-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="bdc13-129">Даже те общие ресурсы, которые доступны для всех, обычно закрыты для пользователей, не прошедших проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="bdc13-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="bdc13-130">Пример выходных данных этой команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="bdc13-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```
4. <span data-ttu-id="bdc13-131">Введите **Y** , когда будет предложено подтвердить установку исправлений.</span><span class="sxs-lookup"><span data-stu-id="bdc13-131">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="bdc13-132">Проверьте обновление с помощью командлета `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="bdc13-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="bdc13-133">Ниже приведен пример выходных данных для обновления, которое выполняется.</span><span class="sxs-lookup"><span data-stu-id="bdc13-133">The following sample output shows the update in progress.</span></span> <span data-ttu-id="bdc13-134">Пока обновление выполняется, `RunInprogress` будет иметь значение `True`.</span><span class="sxs-lookup"><span data-stu-id="bdc13-134">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 12/21/2015 10:36:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="bdc13-135">Ниже приведен пример выходных данных для обновления, установка которого завершена.</span><span class="sxs-lookup"><span data-stu-id="bdc13-135">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="bdc13-136">После установки обновления `RunInProgress` будет иметь значение `False`.</span><span class="sxs-lookup"><span data-stu-id="bdc13-136">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 12/21/2015 10:59:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="bdc13-137">В некоторых случаях командлет выдает значение `False`, пока обновление еще устанавливается.</span><span class="sxs-lookup"><span data-stu-id="bdc13-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="bdc13-138">Чтобы проверить установку обновления, подождите несколько минут, выполните эту команду еще раз и убедитесь в том, что `RunInProgress` имеет значение `False`.</span><span class="sxs-lookup"><span data-stu-id="bdc13-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="bdc13-139">Если это так, значит, исправление установлено.</span><span class="sxs-lookup"><span data-stu-id="bdc13-139">If it is, then the hotfix has completed.</span></span>

6. <span data-ttu-id="bdc13-140">После завершения обновления программного обеспечения повторите шаги 3–5 для установки агента SaaS и агента MDS и наблюдения за ними.</span><span class="sxs-lookup"><span data-stu-id="bdc13-140">After the software update is complete, repeat steps 3-5 to install and monitor the SaaS agent and MDS agent .</span></span> <span data-ttu-id="bdc13-141">Убедитесь, что `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` установлен до `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span><span class="sxs-lookup"><span data-stu-id="bdc13-141">Ensure that `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is installed before `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span></span>
7. <span data-ttu-id="bdc13-142">Проверьте версии программного обеспечения системы.</span><span class="sxs-lookup"><span data-stu-id="bdc13-142">Verify the system software versions.</span></span> <span data-ttu-id="bdc13-143">Тип:</span><span class="sxs-lookup"><span data-stu-id="bdc13-143">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="bdc13-144">Номера версий должны быть следующими:</span><span class="sxs-lookup"><span data-stu-id="bdc13-144">You should see the following versions:</span></span>
   
   * <span data-ttu-id="bdc13-145">HcsSoftwareVersion: 6.3.9600.17673</span><span class="sxs-lookup"><span data-stu-id="bdc13-145">HcsSoftwareVersion: 6.3.9600.17673</span></span>
   * <span data-ttu-id="bdc13-146">CisAgentVersion: 1.0.9150.0</span><span class="sxs-lookup"><span data-stu-id="bdc13-146">CisAgentVersion: 1.0.9150.0</span></span>
   * <span data-ttu-id="bdc13-147">MdsAgentVersion: 30.0.4698.13</span><span class="sxs-lookup"><span data-stu-id="bdc13-147">MdsAgentVersion: 30.0.4698.13</span></span>
     
     <span data-ttu-id="bdc13-148">Если после установки обновления номера версий не изменились, значит, исправление установить не удалось.</span><span class="sxs-lookup"><span data-stu-id="bdc13-148">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="bdc13-149">В этом случае обратитесь за дополнительной помощью в [службу поддержки Майкрософт](../articles/storsimple/storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="bdc13-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
8. <span data-ttu-id="bdc13-150">Повторите шаги 3–5 для установки оставшихся обычных исправлений.</span><span class="sxs-lookup"><span data-stu-id="bdc13-150">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="bdc13-151">Драйвер LSI — KB3121900</span><span class="sxs-lookup"><span data-stu-id="bdc13-151">The LSI driver - KB3121900</span></span>
   * <span data-ttu-id="bdc13-152">Обновление Storport — KB3080728</span><span class="sxs-lookup"><span data-stu-id="bdc13-152">The Storport update - KB3080728</span></span>
   * <span data-ttu-id="bdc13-153">Обновление Spaceport — KB3090322</span><span class="sxs-lookup"><span data-stu-id="bdc13-153">The Spaceport update - KB3090322</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="bdc13-154">Установка и проверка исправлений режима обслуживания</span><span class="sxs-lookup"><span data-stu-id="bdc13-154">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="bdc13-155">Используйте KB3121899, чтобы установить обновления встроенного ПО дисков.</span><span class="sxs-lookup"><span data-stu-id="bdc13-155">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="bdc13-156">Эти обновления прерывают работу, и на их завершение может потребоваться около 30 минут.</span><span class="sxs-lookup"><span data-stu-id="bdc13-156">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="bdc13-157">Данные обновления можно установить в период планового техобслуживания, подключившись к последовательной консоли устройства.</span><span class="sxs-lookup"><span data-stu-id="bdc13-157">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="bdc13-158">Обратите внимание, что если встроенное ПО диска уже обновлено, устанавливать эти обновления не требуется.</span><span class="sxs-lookup"><span data-stu-id="bdc13-158">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="bdc13-159">Выполните командлет `Get-HcsUpdateAvailability` в последовательной консоли устройства, чтобы проверить, доступны ли обновления и являются ли они критическими (режим обслуживания) или некритическими (обычный режим).</span><span class="sxs-lookup"><span data-stu-id="bdc13-159">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="bdc13-160">Чтобы установить обновления встроенного ПО диска, следуйте приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="bdc13-160">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="bdc13-161">Переведите устройство в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="bdc13-161">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="bdc13-162">Обратите внимание, что не следует использовать удаленное взаимодействие Windows PowerShell при переключении устройства в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="bdc13-162">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="bdc13-163">Вместо этого запустите следующий командлет при подключении через последовательную консоль устройства.</span><span class="sxs-lookup"><span data-stu-id="bdc13-163">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="bdc13-164">Тип:</span><span class="sxs-lookup"><span data-stu-id="bdc13-164">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="bdc13-165">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="bdc13-165">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17664
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="bdc13-166">После этого оба контроллера перезапускаются и переходят в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="bdc13-166">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="bdc13-167">Чтобы установить обновление встроенного ПО диска, введите:</span><span class="sxs-lookup"><span data-stu-id="bdc13-167">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="bdc13-168">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="bdc13-168">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="bdc13-169">Отслеживайте ход выполнения установки с помощью команды `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="bdc13-169">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="bdc13-170">Обновление завершится, когда `RunInProgress` поменяется на `False`.</span><span class="sxs-lookup"><span data-stu-id="bdc13-170">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="bdc13-171">После завершения установки контроллер, на котором установлено исправление режима обслуживания, будет перезагружен.</span><span class="sxs-lookup"><span data-stu-id="bdc13-171">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="bdc13-172">В качестве варианта 1 войдите в систему с полным доступом и проверьте версию встроенного ПО диска.</span><span class="sxs-lookup"><span data-stu-id="bdc13-172">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="bdc13-173">Тип:</span><span class="sxs-lookup"><span data-stu-id="bdc13-173">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="bdc13-174">Ожидаемые версии встроенного ПО диска:</span><span class="sxs-lookup"><span data-stu-id="bdc13-174">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="bdc13-175">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="bdc13-175">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17664
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    <span data-ttu-id="bdc13-176">Выполните команду `Get-HcsFirmwareVersion` на втором контроллере, чтобы проверить обновление версии программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="bdc13-176">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="bdc13-177">Затем можно выйти из режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="bdc13-177">You can then exit the maintenance mode.</span></span> <span data-ttu-id="bdc13-178">Для этого введите следующую команду для каждого контроллера устройства:</span><span class="sxs-lookup"><span data-stu-id="bdc13-178">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="bdc13-179">При выходе из режима обслуживания контроллеры перезапускаются.</span><span class="sxs-lookup"><span data-stu-id="bdc13-179">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="bdc13-180">Когда обновления встроенного ПО диска будут успешно установлены, а устройство будет выведено из режима обслуживания, вернитесь в классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc13-180">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="bdc13-181">Обратите внимание, что для отображения установленных обновлений режима обслуживания на портале может потребоваться до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="bdc13-181">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

