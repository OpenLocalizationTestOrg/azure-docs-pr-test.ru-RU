<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="7fd14-101">toodownload исправления</span><span class="sxs-lookup"><span data-stu-id="7fd14-101">toodownload hotfixes</span></span>

<span data-ttu-id="7fd14-102">Выполните следующие действия toodownload hello обновления из каталога Центра обновления Майкрософт hello hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="7fd14-103">Запустите Internet Explorer и перейдите слишком[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7fd14-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="7fd14-104">Если вы впервые используете hello каталога Центра обновления Майкрософт на этом компьютере, нажмите кнопку **установить** при запрашиваемые tooinstall hello надстройку каталога Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7fd14-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

    ![Установка каталога](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="7fd14-106">В поле поиска hello hello каталога Центра обновления Майкрософт, введите номер базы знаний (KB) hello hello исправления требуется toodownload, например **4037264**, а затем нажмите кнопку **поиска**.</span><span class="sxs-lookup"><span data-stu-id="7fd14-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="7fd14-107">Hello исправление вхождение отображаться, например, **совокупное 5.0 обновления пакета программного обеспечения для StorSimple серии 8000**.</span><span class="sxs-lookup"><span data-stu-id="7fd14-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![Поиск в каталоге](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="7fd14-109">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="7fd14-109">Click **Download**.</span></span> <span data-ttu-id="7fd14-110">Укажите или **Обзор** tooa локального место tooappear загружает hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-110">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="7fd14-111">Выберите файлы hello toodownload toohello указано расположение и папку.</span><span class="sxs-lookup"><span data-stu-id="7fd14-111">Click hello files toodownload toohello specified location and folder.</span></span> <span data-ttu-id="7fd14-112">Папка Hello также может быть скопированный tooa сетевая папка, которая доступна из устройства hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-112">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
5. <span data-ttu-id="7fd14-113">Поиск дополнительных исправления, перечисленные в приведенной выше таблице hello (**4037266**), и соответствующего hello загрузки файлов toohello определенные папки, перечисленные в предшествующей таблице hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-113">Search for any additional hotfixes listed in hello table above (**4037266**), and download hello corresponding files toohello specific folders as listed in hello preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="7fd14-114">исправления Hello должен быть доступен с обоих контроллеров toodetect, все потенциальные ошибки сообщений hello однорангового контроллера.</span><span class="sxs-lookup"><span data-stu-id="7fd14-114">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
>
> <span data-ttu-id="7fd14-115">Hello исправления необходимо скопировать в разные папки и 3.</span><span class="sxs-lookup"><span data-stu-id="7fd14-115">hello hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="7fd14-116">Например, обновление программного обеспечения и Cis/MDS агента hello устройства могут быть скопированы в _FirstOrderUpdate_ hello папки, все другие обновления не нарушают работу может быть скопирован в hello _SecondOrderUpdate_ папки, и обновления в режиме обслуживания копируются в _ThirdOrderUpdate_ папки.</span><span class="sxs-lookup"><span data-stu-id="7fd14-116">For example, hello device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all hello other non-disruptive updates could be copied in hello _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="7fd14-117">tooinstall исправления обычный режим</span><span class="sxs-lookup"><span data-stu-id="7fd14-117">tooinstall and verify regular mode hotfixes</span></span>

<span data-ttu-id="7fd14-118">Выполните следующие шаги tooinstall hello и проверьте исправления в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="7fd14-118">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="7fd14-119">Если вы установили их с помощью hello портал Azure, пропускать слишком[Установка исправлений в режиме обслуживания,](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="7fd14-119">If you already installed them using hello Azure portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="7fd14-120">исправления tooinstall hello, доступа к интерфейсу Windows PowerShell hello в последовательной консоли устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7fd14-120">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="7fd14-121">Выполните hello подробные инструкции в [последовательной консоли используйте PuTTy tooconnect toohello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="7fd14-121">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="7fd14-122">Hello командной строки, нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7fd14-122">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="7fd14-123">Выберите **вариант 1** toolog на устройстве toohello с полным доступом.</span><span class="sxs-lookup"><span data-stu-id="7fd14-123">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="7fd14-124">Мы рекомендуем установить исправление hello на пассивный контроллер hello сначала.</span><span class="sxs-lookup"><span data-stu-id="7fd14-124">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="7fd14-125">исправление tooinstall hello в hello командной строке введите:</span><span class="sxs-lookup"><span data-stu-id="7fd14-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="7fd14-126">Используйте IP, а не DNS в пути к папке в hello выше команды.</span><span class="sxs-lookup"><span data-stu-id="7fd14-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="7fd14-127">параметр Hello учетных данных используется только в том случае, если вы обращаетесь ресурс прошедшего проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="7fd14-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="7fd14-128">Рекомендуется использовать параметр tooaccess hello учетных данных долей.</span><span class="sxs-lookup"><span data-stu-id="7fd14-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="7fd14-129">Даже общих папок, которые открыты слишком пребывание «everyone» обычно не открыть toounauthenticated пользователей.</span><span class="sxs-lookup"><span data-stu-id="7fd14-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
4. <span data-ttu-id="7fd14-130">Укажите hello пароль при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="7fd14-130">Supply hello password when prompted.</span></span> <span data-ttu-id="7fd14-131">Ниже приведен пример выходных данных для установки первого порядка обновления hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-131">A sample output for installing hello first order updates is shown below.</span></span> <span data-ttu-id="7fd14-132">Для первого порядка обновления hello потребуется toopoint toohello определенного файла.</span><span class="sxs-lookup"><span data-stu-id="7fd14-132">For hello first order update, you need toopoint toohello specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="7fd14-133">Следует установить hello _HcsSoftwareUpdate.exe_ первой.</span><span class="sxs-lookup"><span data-stu-id="7fd14-133">You should install hello _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="7fd14-134">Затем установите _CisMdsAgentUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="7fd14-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="7fd14-135">Тип **Y** при запрашиваемые tooconfirm hello установки исправления.</span><span class="sxs-lookup"><span data-stu-id="7fd14-135">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
6. <span data-ttu-id="7fd14-136">Мониторинг hello обновления с помощью hello `Get-HcsUpdateStatus` командлета.</span><span class="sxs-lookup"><span data-stu-id="7fd14-136">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="7fd14-137">Обновление Hello сначала будет выполнена на пассивный контроллер hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-137">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="7fd14-138">Здравствуйте, после обновляется hello пассивного контроллера, произойдет отработка отказа и обновление hello затем будут применяться на другой контроллер.</span><span class="sxs-lookup"><span data-stu-id="7fd14-138">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="7fd14-139">Hello обновления завершается после завершения обновления обоих контроллеров hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-139">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="7fd14-140">Hello следующий образец вывода показывает hello обновление выполняется.</span><span class="sxs-lookup"><span data-stu-id="7fd14-140">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="7fd14-141">Hello `RunInprogress` — `True` при hello идет обновление.</span><span class="sxs-lookup"><span data-stu-id="7fd14-141">hello `RunInprogress` is `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="7fd14-142">Следующий пример выходных данных Hello указывает, что завершения обновления hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-142">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="7fd14-143">Hello `RunInProgress` — `False` hello обновления после завершения операции.</span><span class="sxs-lookup"><span data-stu-id="7fd14-143">hello `RunInProgress` is `False` when hello update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="7fd14-144">В некоторых случаях hello отчеты командлет `False` при обновлении hello она все еще выполняется.</span><span class="sxs-lookup"><span data-stu-id="7fd14-144">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="7fd14-145">tooensure, hello исправление завершена, подождите несколько минут, выполните эту команду повторно и убедитесь, что hello `RunInProgress` — `False`.</span><span class="sxs-lookup"><span data-stu-id="7fd14-145">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="7fd14-146">Если это так, исправление hello завершена.</span><span class="sxs-lookup"><span data-stu-id="7fd14-146">If it is, then hello hotfix has completed.</span></span>

7. <span data-ttu-id="7fd14-147">После завершения обновления программного обеспечения hello проверки версий программного обеспечения системы hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-147">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="7fd14-148">Тип:</span><span class="sxs-lookup"><span data-stu-id="7fd14-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="7fd14-149">Вы должны увидеть следующие версии hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-149">You should see hello following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="7fd14-150">Если номер версии hello остается неизменным после применения обновления hello, это означает, что сбой tooapply исправление hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-150">If hello version number does not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="7fd14-151">В этом случае обратитесь за дополнительной помощью в [службу поддержки Майкрософт](../articles/storsimple/storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="7fd14-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="7fd14-152">Необходимо перезапустить активный контроллер hello через hello `Restart-HcsController` командлет перед применением hello следующего обновления.</span><span class="sxs-lookup"><span data-stu-id="7fd14-152">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello next update.</span></span>
     
8. <span data-ttu-id="7fd14-153">Повторите шаги 3 – 6 hello tooinstall _CisMDSAgentupdate.exe_ агент скачать tooyour _FirstOrderUpdate_ папки.</span><span class="sxs-lookup"><span data-stu-id="7fd14-153">Repeat steps 3-6 tooinstall hello _CisMDSAgentupdate.exe_ agent downloaded tooyour _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="7fd14-154">Повторите шаги 3 – 6 tooinstall hello второго порядка обновления.</span><span class="sxs-lookup"><span data-stu-id="7fd14-154">Repeat steps 3-6 tooinstall hello second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="7fd14-155">Для второго порядка обновлений, можно установить несколько обновлений, просто выполнив hello `Start-HcsHotfix cmdlet` и указать папку toohello, где находятся второго порядка обновления.</span><span class="sxs-lookup"><span data-stu-id="7fd14-155">For second order updates, multiple updates can be installed by just running hello `Start-HcsHotfix cmdlet` and pointing toohello folder where second order updates are located.</span></span> <span data-ttu-id="7fd14-156">Hello командлет выполнит все hello обновления, доступные в папке hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-156">hello cmdlet will execute all hello updates available in hello folder.</span></span> <span data-ttu-id="7fd14-157">Если обновление уже установлено, логика обновления hello обнаружит и не применить это обновление.</span><span class="sxs-lookup"><span data-stu-id="7fd14-157">If an update is already installed, hello update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="7fd14-158">После установки всех исправлений hello использовать hello `Get-HcsSystem` командлета.</span><span class="sxs-lookup"><span data-stu-id="7fd14-158">After all hello hotfixes are installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="7fd14-159">должен быть Hello версии:</span><span class="sxs-lookup"><span data-stu-id="7fd14-159">hello versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="7fd14-160">tooinstall исправления режима обслуживания</span><span class="sxs-lookup"><span data-stu-id="7fd14-160">tooinstall and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="7fd14-161">Используйте обновления встроенного по диска tooinstall KB4037263.</span><span class="sxs-lookup"><span data-stu-id="7fd14-161">Use KB4037263 tooinstall disk firmware updates.</span></span> <span data-ttu-id="7fd14-162">Эти обновления нарушают работу и занять toocomplete около 30 минут.</span><span class="sxs-lookup"><span data-stu-id="7fd14-162">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="7fd14-163">Вы можете tooinstall в период планового обслуживания, подключающегося последовательной консоли устройства toohello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-163">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="7fd14-164">Если встроенного по диска уже обновлена, нет необходимости tooinstall эти обновления.</span><span class="sxs-lookup"><span data-stu-id="7fd14-164">If your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="7fd14-165">Запустите hello `Get-HcsUpdateAvailability` из последовательной консоли toocheck hello устройства, если обновления доступны, является ли hello обновляет являются критическими (режим обслуживания) или не нарушают работу (обычный режим) обновления.</span><span class="sxs-lookup"><span data-stu-id="7fd14-165">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="7fd14-166">обновления встроенного по диска tooinstall hello, следуйте приведенным ниже инструкциям hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-166">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="7fd14-167">Поместите hello устройства в режим обслуживания hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-167">Place hello device in hello maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="7fd14-168">Не используйте удаленное взаимодействие Windows PowerShell, при подключении tooa устройство находится в режиме обслуживания.</span><span class="sxs-lookup"><span data-stu-id="7fd14-168">Do not use Windows PowerShell remoting when connecting tooa device in maintenance mode.</span></span> <span data-ttu-id="7fd14-169">Вместо этого используйте этот командлет на контроллере устройства hello при подключении через последовательную консоль устройства hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-169">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span>

    <span data-ttu-id="7fd14-170">контроллер tooplace hello в режиме обслуживания, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7fd14-170">tooplace hello controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="7fd14-171">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="7fd14-171">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="7fd14-172">Оба контроллера hello перезапустите в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="7fd14-172">Both hello controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="7fd14-173">обновление встроенного по диска hello tooinstall, тип</span><span class="sxs-lookup"><span data-stu-id="7fd14-173">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="7fd14-174">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="7fd14-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="7fd14-175">Монитор hello установка выполняется с помощью `Get-HcsUpdateStatus` команды.</span><span class="sxs-lookup"><span data-stu-id="7fd14-175">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="7fd14-176">Hello обновление будет завершено, после hello `RunInProgress` изменяет слишком`False`.</span><span class="sxs-lookup"><span data-stu-id="7fd14-176">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="7fd14-177">По завершении установки hello перезапуска контроллера hello, на какие hello было установлено исправление режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="7fd14-177">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="7fd14-178">Войдите в систему как вариант 1 с полным доступом и проверка версии встроенного по диска hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-178">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="7fd14-179">Тип:</span><span class="sxs-lookup"><span data-stu-id="7fd14-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="7fd14-180">Hello ожидаемого версии встроенного по диска:</span><span class="sxs-lookup"><span data-stu-id="7fd14-180">hello expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="7fd14-181">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="7fd14-181">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
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
   
    <span data-ttu-id="7fd14-182">Запустите hello `Get-HcsFirmwareVersion` команду на второй контроллер tooverify hello, hello версия программного обеспечения был обновлен.</span><span class="sxs-lookup"><span data-stu-id="7fd14-182">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="7fd14-183">Затем можно выйти из режима обслуживания hello.</span><span class="sxs-lookup"><span data-stu-id="7fd14-183">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="7fd14-184">toodo таким образом, введите следующую команду для каждого устройства контроллера hello:</span><span class="sxs-lookup"><span data-stu-id="7fd14-184">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="7fd14-185">контроллеры Hello перезапустите при выходе из режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="7fd14-185">hello controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="7fd14-186">После встроенного по диска hello успешного применения обновлений и устройство hello вышел из режима обслуживания, возвращаемого toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7fd14-186">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure portal.</span></span> <span data-ttu-id="7fd14-187">Обратите внимание, что этот портал hello может показывать установку обновлений в режиме обслуживания hello на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="7fd14-187">Note that hello portal might not show that you installed hello maintenance mode updates for 24 hours.</span></span>

