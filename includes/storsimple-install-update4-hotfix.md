<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="f0f95-101">Загрузка исправления</span><span class="sxs-lookup"><span data-stu-id="f0f95-101">To download hotfixes</span></span>

<span data-ttu-id="f0f95-102">Для загрузки обновления программного обеспечения из каталога обновления Майкрософт выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f0f95-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="f0f95-103">Запустите Internet Explorer и откройте страницу [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f0f95-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="f0f95-104">Если вы впервые используете каталог Центра обновления Майкрософт на этом компьютере, нажмите кнопку **Установить** , когда будет предложено установить надстройку каталога Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f0f95-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

    ![Установка каталога](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="f0f95-106">В поле поиска каталога Центра обновления Майкрософт введите номер необходимого исправления в базе знаний, например **4011839**, а затем нажмите кнопку **Найти**.</span><span class="sxs-lookup"><span data-stu-id="f0f95-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4011839**, and then click **Search**.</span></span>
   
    <span data-ttu-id="f0f95-107">Появится список исправлений, например **Совокупное обновление программного обеспечения версии 4.0 для StorSimple серии 8000**.</span><span class="sxs-lookup"><span data-stu-id="f0f95-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 4.0 for StorSimple 8000 Series**.</span></span>
   
    ![Поиск в каталоге](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)

4. <span data-ttu-id="f0f95-109">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="f0f95-109">Click **Download**.</span></span> <span data-ttu-id="f0f95-110">Укажите или **выберите** локальное расположение, в которое хотите скачать файлы.</span><span class="sxs-lookup"><span data-stu-id="f0f95-110">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="f0f95-111">Выберите файлы для загрузки в указанное расположение и папку.</span><span class="sxs-lookup"><span data-stu-id="f0f95-111">Click the files to download to the specified location and folder.</span></span> <span data-ttu-id="f0f95-112">Этот каталог также можно скопировать в сетевую папку, которая доступна с вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="f0f95-112">The folder can also be copied to a network share that is reachable from the device.</span></span>
5. <span data-ttu-id="f0f95-113">Найдите дополнительные исправления, перечисленные в приведенной выше таблице (**4011841**), и скачайте соответствующие файлы в папки, указанные в этой таблице.</span><span class="sxs-lookup"><span data-stu-id="f0f95-113">Search for any additional hotfixes listed in the table above (**4011841**), and download the corresponding files to the specific folders as listed in the preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="f0f95-114">Исправления должны быть доступны с обоих контроллеров, чтобы можно было получить любые возможные сообщения об ошибке от однорангового контроллера.</span><span class="sxs-lookup"><span data-stu-id="f0f95-114">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
>
> <span data-ttu-id="f0f95-115">Исправления необходимо скопировать в 3 отдельные папки.</span><span class="sxs-lookup"><span data-stu-id="f0f95-115">The hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="f0f95-116">Например, обновление агента программного обеспечения устройства Cis/MDS необходимо скопировать в папку _FirstOrderUpdate_. Все остальные обновления, не нарушающие работу устройства, можно скопировать в папку _SecondOrderUpdate_, а обновления в режиме обслуживания — в папку _ThirdOrderUpdate_.</span><span class="sxs-lookup"><span data-stu-id="f0f95-116">For example, the device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="f0f95-117">Установка и проверка исправлений обычного режима</span><span class="sxs-lookup"><span data-stu-id="f0f95-117">To install and verify regular mode hotfixes</span></span>

<span data-ttu-id="f0f95-118">Выполните следующие действия для установки и проверки обычных исправлений.</span><span class="sxs-lookup"><span data-stu-id="f0f95-118">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="f0f95-119">Если вы уже установили их с помощью классического портала Azure, перейдите к [установке и проверке исправлений режима обслуживания](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="f0f95-119">If you already installed them using the Azure classic portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="f0f95-120">Чтобы установить исправления, откройте интерфейс Windows PowerShell на последовательной консоли своего устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f0f95-120">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="f0f95-121">Подробные инструкции см. в разделе [Подключение к последовательной консоли устройства с помощью PuTTY](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="f0f95-121">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="f0f95-122">В командной строке нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="f0f95-122">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="f0f95-123">Выберите **Вариант 1** , чтобы войти на устройство с правами на полный доступ.</span><span class="sxs-lookup"><span data-stu-id="f0f95-123">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="f0f95-124">Рекомендуем сначала установить исправление на пассивный контроллер.</span><span class="sxs-lookup"><span data-stu-id="f0f95-124">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="f0f95-125">Чтобы установить исправление, в командной строке введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f0f95-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="f0f95-126">В указанной выше команде вместо DNS в адресе общей папки укажите IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f0f95-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="f0f95-127">Параметр "credential" используется только для доступа к общему ресурсу с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="f0f95-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="f0f95-128">Для доступа к общим ресурсам рекомендуем использовать параметр учетных данных.</span><span class="sxs-lookup"><span data-stu-id="f0f95-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="f0f95-129">Даже те общие ресурсы, которые доступны для всех, обычно закрыты для пользователей, не прошедших проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="f0f95-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="f0f95-130">В ответ на запрос введите пароль.</span><span class="sxs-lookup"><span data-stu-id="f0f95-130">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="f0f95-131">Ниже приведен пример выходных данных для установки обновлений первого типа.</span><span class="sxs-lookup"><span data-stu-id="f0f95-131">A sample output for installing the first order updates is shown below.</span></span> <span data-ttu-id="f0f95-132">Для обновления первого типа необходимо указать определенный файл.</span><span class="sxs-lookup"><span data-stu-id="f0f95-132">For the first order update, you need to point to the specific file.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="f0f95-133">Введите **Y** , когда будет предложено подтвердить установку исправлений.</span><span class="sxs-lookup"><span data-stu-id="f0f95-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="f0f95-134">Проверьте обновление с помощью командлета `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="f0f95-134">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="f0f95-135">Сначала обновится пассивный контроллер.</span><span class="sxs-lookup"><span data-stu-id="f0f95-135">The update will first complete on the passive controller.</span></span> <span data-ttu-id="f0f95-136">После этого будет выполнена отработка отказа. Затем обновление будет применено на другом контроллере.</span><span class="sxs-lookup"><span data-stu-id="f0f95-136">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="f0f95-137">Установка обновления завершится, когда оба контроллера будут обновлены.</span><span class="sxs-lookup"><span data-stu-id="f0f95-137">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="f0f95-138">Ниже приведен пример выходных данных для обновления, которое выполняется.</span><span class="sxs-lookup"><span data-stu-id="f0f95-138">The following sample output shows the update in progress.</span></span> <span data-ttu-id="f0f95-139">Пока обновление выполняется, `RunInprogress` будет иметь значение `True`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-139">The `RunInprogress` will be `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="f0f95-140">Ниже приведен пример выходных данных для обновления, установка которого завершена.</span><span class="sxs-lookup"><span data-stu-id="f0f95-140">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="f0f95-141">После установки обновления `RunInProgress` будет иметь значение `False`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-141">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="f0f95-142">В некоторых случаях командлет выдает значение `False`, пока обновление еще устанавливается.</span><span class="sxs-lookup"><span data-stu-id="f0f95-142">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="f0f95-143">Чтобы проверить установку обновления, подождите несколько минут, выполните эту команду еще раз и убедитесь в том, что `RunInProgress` имеет значение `False`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-143">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="f0f95-144">Если это так, значит, исправление установлено.</span><span class="sxs-lookup"><span data-stu-id="f0f95-144">If it is, then the hotfix has completed.</span></span>

6. <span data-ttu-id="f0f95-145">Когда установка обновления будет завершена, проверьте версии программного обеспечения системы.</span><span class="sxs-lookup"><span data-stu-id="f0f95-145">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="f0f95-146">Тип:</span><span class="sxs-lookup"><span data-stu-id="f0f95-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="f0f95-147">Номера версий должны быть следующими:</span><span class="sxs-lookup"><span data-stu-id="f0f95-147">You should see the following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    <span data-ttu-id="f0f95-148">Если после установки обновления номер версии не изменился, значит исправление установить не удалось.</span><span class="sxs-lookup"><span data-stu-id="f0f95-148">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="f0f95-149">В этом случае обратитесь за дополнительной помощью в [службу поддержки Майкрософт](../articles/storsimple/storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="f0f95-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="f0f95-150">Прежде чем применять следующее обновление, необходимо перезапустить активный контроллер с помощью командлета `Restart-HcsController`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-150">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the next update.</span></span>
     
7. <span data-ttu-id="f0f95-151">Повторите шаги 3–5, чтобы установить агент Cis/MDS, скачанный в папку _FirstOrderUpdate_.</span><span class="sxs-lookup"><span data-stu-id="f0f95-151">Repeat steps 3-5 to install the Cis/MDS agent downloaded to your _FirstOrderUpdate_ folder.</span></span> 
8. <span data-ttu-id="f0f95-152">Повторите шаги 3–5, чтобы установить обновления второго типа.</span><span class="sxs-lookup"><span data-stu-id="f0f95-152">Repeat steps 3-5 to install the second order updates.</span></span> <span data-ttu-id="f0f95-153">**Для обновлений второго типа можно установить несколько обновлений, просто запустив командлет `Start-HcsHotfix cmdlet` и указав папку, где они находятся. Командлет выполнит все обновления, доступные в папке.**</span><span class="sxs-lookup"><span data-stu-id="f0f95-153">**For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located. The cmdlet will execute all the updates available in the folder.**</span></span> <span data-ttu-id="f0f95-154">Если обновление уже установлено, логика обновления обнаружит это и не установит его.</span><span class="sxs-lookup"><span data-stu-id="f0f95-154">If an update is already installed, the update logic will detect that and not apply that update.</span></span> 

<span data-ttu-id="f0f95-155">После установки всех исправлений используйте командлет `Get-HcsSystem`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-155">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="f0f95-156">Необходимые версии:</span><span class="sxs-lookup"><span data-stu-id="f0f95-156">The versions should be:</span></span>

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="f0f95-157">Установка и проверка исправлений режима обслуживания</span><span class="sxs-lookup"><span data-stu-id="f0f95-157">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="f0f95-158">Используйте статью KB4011837, чтобы установить обновления встроенного ПО дисков.</span><span class="sxs-lookup"><span data-stu-id="f0f95-158">Use KB4011837 to install disk firmware updates.</span></span> <span data-ttu-id="f0f95-159">Эти обновления прерывают работу, и на их завершение может потребоваться около 30 минут.</span><span class="sxs-lookup"><span data-stu-id="f0f95-159">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="f0f95-160">Данные обновления можно установить в период планового техобслуживания, подключившись к последовательной консоли устройства.</span><span class="sxs-lookup"><span data-stu-id="f0f95-160">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="f0f95-161">Обратите внимание, что если встроенное ПО диска уже обновлено, устанавливать эти обновления не требуется.</span><span class="sxs-lookup"><span data-stu-id="f0f95-161">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="f0f95-162">Выполните командлет `Get-HcsUpdateAvailability` в последовательной консоли устройства, чтобы проверить, доступны ли обновления и являются ли они критическими (режим обслуживания) или некритическими (обычный режим).</span><span class="sxs-lookup"><span data-stu-id="f0f95-162">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="f0f95-163">Чтобы установить обновления встроенного ПО диска, следуйте приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="f0f95-163">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="f0f95-164">Переведите устройство в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="f0f95-164">Place the device in the maintenance mode.</span></span> <span data-ttu-id="f0f95-165">**Обратите внимание, что не следует использовать удаленное взаимодействие Windows PowerShell при переключении устройства в режим обслуживания. Вместо этого запустите следующий командлет при подключении через последовательную консоль устройства.**</span><span class="sxs-lookup"><span data-stu-id="f0f95-165">**Note that you should not use Windows PowerShell remoting when connecting to a device in maintenance mode. Instead run this cmdlet on the device controller when connected through the device serial console.**</span></span> <span data-ttu-id="f0f95-166">Тип:</span><span class="sxs-lookup"><span data-stu-id="f0f95-166">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="f0f95-167">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="f0f95-167">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="f0f95-168">После этого оба контроллера перезапускаются и переходят в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="f0f95-168">Both the controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="f0f95-169">Чтобы установить обновление встроенного ПО диска, введите:</span><span class="sxs-lookup"><span data-stu-id="f0f95-169">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="f0f95-170">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="f0f95-170">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="f0f95-171">Отслеживайте ход выполнения установки с помощью команды `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="f0f95-171">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="f0f95-172">Обновление завершится, когда `RunInProgress` поменяется на `False`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-172">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="f0f95-173">После завершения установки контроллер, на котором установлено исправление режима обслуживания, будет перезагружен.</span><span class="sxs-lookup"><span data-stu-id="f0f95-173">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="f0f95-174">В качестве варианта 1 войдите в систему с полным доступом и проверьте версию встроенного ПО диска.</span><span class="sxs-lookup"><span data-stu-id="f0f95-174">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="f0f95-175">Тип:</span><span class="sxs-lookup"><span data-stu-id="f0f95-175">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="f0f95-176">Ожидаемые версии встроенного ПО диска:</span><span class="sxs-lookup"><span data-stu-id="f0f95-176">The expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   <span data-ttu-id="f0f95-177">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="f0f95-177">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17820
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    <span data-ttu-id="f0f95-178">Выполните команду `Get-HcsFirmwareVersion` на втором контроллере, чтобы проверить обновление версии программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="f0f95-178">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="f0f95-179">Затем можно выйти из режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="f0f95-179">You can then exit the maintenance mode.</span></span> <span data-ttu-id="f0f95-180">Для этого введите следующую команду для каждого контроллера устройства:</span><span class="sxs-lookup"><span data-stu-id="f0f95-180">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="f0f95-181">При выходе из режима обслуживания контроллеры перезапускаются.</span><span class="sxs-lookup"><span data-stu-id="f0f95-181">The controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="f0f95-182">Когда обновления встроенного ПО диска будут успешно установлены, а устройство будет выведено из режима обслуживания, вернитесь в классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f0f95-182">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="f0f95-183">Обратите внимание, что для отображения установленных обновлений режима обслуживания на портале может потребоваться до 24 часов.</span><span class="sxs-lookup"><span data-stu-id="f0f95-183">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span></span>

