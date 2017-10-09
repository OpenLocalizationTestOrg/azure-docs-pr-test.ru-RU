<!--author=alkohli last changed: 02/10/17-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="b07ad-101">toodownload исправления</span><span class="sxs-lookup"><span data-stu-id="b07ad-101">toodownload hotfixes</span></span>

<span data-ttu-id="b07ad-102">Выполните следующие действия toodownload hello обновления из каталога Центра обновления Майкрософт hello hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="b07ad-103">Запустите Internet Explorer и перейдите слишком[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b07ad-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="b07ad-104">Если вы впервые используете hello каталога Центра обновления Майкрософт на этом компьютере, нажмите кнопку **установить** при запрашиваемые tooinstall hello надстройку каталога Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b07ad-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

    ![Установка каталога](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="b07ad-106">В поле поиска hello hello каталога Центра обновления Майкрософт, введите номер базы знаний (KB) hello hello исправления требуется toodownload, например **4011839**, а затем нажмите кнопку **поиска**.</span><span class="sxs-lookup"><span data-stu-id="b07ad-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **4011839**, and then click **Search**.</span></span>
   
    <span data-ttu-id="b07ad-107">Hello исправление вхождение отображаться, например, **совокупное 4.0 обновления пакета программного обеспечения для StorSimple серии 8000**.</span><span class="sxs-lookup"><span data-stu-id="b07ad-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 4.0 for StorSimple 8000 Series**.</span></span>
   
    ![Поиск в каталоге](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)

4. <span data-ttu-id="b07ad-109">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="b07ad-109">Click **Download**.</span></span> <span data-ttu-id="b07ad-110">Укажите или **Обзор** tooa локального место tooappear загружает hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-110">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="b07ad-111">Выберите файлы hello toodownload toohello указано расположение и папку.</span><span class="sxs-lookup"><span data-stu-id="b07ad-111">Click hello files toodownload toohello specified location and folder.</span></span> <span data-ttu-id="b07ad-112">Папка Hello также может быть скопированный tooa сетевая папка, которая доступна из устройства hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-112">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
5. <span data-ttu-id="b07ad-113">Поиск дополнительных исправления, перечисленные в приведенной выше таблице hello (**4011841**), и соответствующего hello загрузки файлов toohello определенные папки, перечисленные в предшествующей таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-113">Search for any additional hotfixes listed in hello table above (**4011841**), and download hello corresponding files toohello specific folders as listed in hello preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="b07ad-114">исправления Hello должен быть доступен с обоих контроллеров toodetect, все потенциальные ошибки сообщений hello однорангового контроллера.</span><span class="sxs-lookup"><span data-stu-id="b07ad-114">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
>
> <span data-ttu-id="b07ad-115">Hello исправления необходимо скопировать в разные папки и 3.</span><span class="sxs-lookup"><span data-stu-id="b07ad-115">hello hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="b07ad-116">Например, обновление программного обеспечения и Cis/MDS агента hello устройства могут быть скопированы в _FirstOrderUpdate_ hello папки, все другие обновления не нарушают работу может быть скопирован в hello _SecondOrderUpdate_ папки, и обновления в режиме обслуживания копируются в _ThirdOrderUpdate_ папки.</span><span class="sxs-lookup"><span data-stu-id="b07ad-116">For example, hello device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all hello other non-disruptive updates could be copied in hello _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="b07ad-117">tooinstall исправления обычный режим</span><span class="sxs-lookup"><span data-stu-id="b07ad-117">tooinstall and verify regular mode hotfixes</span></span>

<span data-ttu-id="b07ad-118">Выполните следующие шаги tooinstall hello и проверьте исправления в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="b07ad-118">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="b07ad-119">Если вы установили их с помощью hello классический портал Azure, пропускать слишком[Установка исправлений в режиме обслуживания,](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="b07ad-119">If you already installed them using hello Azure classic portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="b07ad-120">исправления tooinstall hello, доступа к интерфейсу Windows PowerShell hello в последовательной консоли устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b07ad-120">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="b07ad-121">Выполните hello подробные инструкции в [последовательной консоли используйте PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b07ad-121">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="b07ad-122">Hello командной строки, нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="b07ad-122">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="b07ad-123">Выберите **вариант 1** toolog на устройстве toohello с полным доступом.</span><span class="sxs-lookup"><span data-stu-id="b07ad-123">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="b07ad-124">Мы рекомендуем установить исправление hello на пассивный контроллер hello сначала.</span><span class="sxs-lookup"><span data-stu-id="b07ad-124">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="b07ad-125">исправление tooinstall hello в hello командной строке введите:</span><span class="sxs-lookup"><span data-stu-id="b07ad-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="b07ad-126">Используйте IP, а не DNS в пути к папке в hello выше команды.</span><span class="sxs-lookup"><span data-stu-id="b07ad-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="b07ad-127">параметр Hello учетных данных используется только в том случае, если вы обращаетесь ресурс прошедшего проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b07ad-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="b07ad-128">Рекомендуется использовать параметр tooaccess hello учетных данных долей.</span><span class="sxs-lookup"><span data-stu-id="b07ad-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="b07ad-129">Даже общих папок, которые открыты слишком пребывание «everyone» обычно не открыть toounauthenticated пользователей.</span><span class="sxs-lookup"><span data-stu-id="b07ad-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="b07ad-130">Укажите hello пароль при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="b07ad-130">Supply hello password when prompted.</span></span>
   
    <span data-ttu-id="b07ad-131">Ниже приведен пример выходных данных для установки первого порядка обновления hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-131">A sample output for installing hello first order updates is shown below.</span></span> <span data-ttu-id="b07ad-132">Для первого порядка обновления hello потребуется toopoint toohello определенного файла.</span><span class="sxs-lookup"><span data-stu-id="b07ad-132">For hello first order update, you need toopoint toohello specific file.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="b07ad-133">Тип **Y** при запрашиваемые tooconfirm hello установки исправления.</span><span class="sxs-lookup"><span data-stu-id="b07ad-133">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="b07ad-134">Мониторинг hello обновления с помощью hello `Get-HcsUpdateStatus` командлета.</span><span class="sxs-lookup"><span data-stu-id="b07ad-134">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="b07ad-135">Обновление Hello сначала будет выполнена на пассивный контроллер hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-135">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="b07ad-136">Здравствуйте, после обновляется hello пассивного контроллера, произойдет отработка отказа и обновление hello затем будут применяться на другой контроллер.</span><span class="sxs-lookup"><span data-stu-id="b07ad-136">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="b07ad-137">Hello обновления завершается после завершения обновления обоих контроллеров hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-137">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="b07ad-138">Hello следующий образец вывода показывает hello обновление выполняется.</span><span class="sxs-lookup"><span data-stu-id="b07ad-138">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="b07ad-139">Hello `RunInprogress` будет `True` при hello идет обновление.</span><span class="sxs-lookup"><span data-stu-id="b07ad-139">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="b07ad-140">Следующий пример выходных данных Hello указывает, что завершения обновления hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-140">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="b07ad-141">Hello `RunInProgress` будет `False` после завершения обновления hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-141">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="b07ad-142">В некоторых случаях hello отчеты командлет `False` при обновлении hello она все еще выполняется.</span><span class="sxs-lookup"><span data-stu-id="b07ad-142">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="b07ad-143">tooensure, hello исправление завершена, подождите несколько минут, выполните эту команду повторно и убедитесь, что hello `RunInProgress` — `False`.</span><span class="sxs-lookup"><span data-stu-id="b07ad-143">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="b07ad-144">Если это так, исправление hello завершена.</span><span class="sxs-lookup"><span data-stu-id="b07ad-144">If it is, then hello hotfix has completed.</span></span>

6. <span data-ttu-id="b07ad-145">После завершения обновления программного обеспечения hello проверки версий программного обеспечения системы hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-145">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="b07ad-146">Тип:</span><span class="sxs-lookup"><span data-stu-id="b07ad-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="b07ad-147">Вы должны увидеть следующие версии hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-147">You should see hello following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    <span data-ttu-id="b07ad-148">Если номер версии hello остается неизменным после применения обновления hello, это означает, что сбой tooapply исправление hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-148">If hello version number does not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="b07ad-149">В этом случае обратитесь за дополнительной помощью в [службу поддержки Майкрософт](../articles/storsimple/storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b07ad-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="b07ad-150">Необходимо перезапустить активный контроллер hello через hello `Restart-HcsController` командлет перед применением hello следующего обновления.</span><span class="sxs-lookup"><span data-stu-id="b07ad-150">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello next update.</span></span>
     
7. <span data-ttu-id="b07ad-151">Повторите шаги 3 – 5 tooinstall hello tooyour загрузить агент Cis/MDS _FirstOrderUpdate_ папки.</span><span class="sxs-lookup"><span data-stu-id="b07ad-151">Repeat steps 3-5 tooinstall hello Cis/MDS agent downloaded tooyour _FirstOrderUpdate_ folder.</span></span> 
8. <span data-ttu-id="b07ad-152">Повторите шаги 3 – 5 tooinstall hello второго порядка обновления.</span><span class="sxs-lookup"><span data-stu-id="b07ad-152">Repeat steps 3-5 tooinstall hello second order updates.</span></span> <span data-ttu-id="b07ad-153">**Для второго порядка обновлений, можно установить несколько обновлений, просто выполнив hello `Start-HcsHotfix cmdlet` и указывающего toohello папку, где находятся второго порядка обновления. hello командлет выполнит все hello обновления, доступные в папке hello.**</span><span class="sxs-lookup"><span data-stu-id="b07ad-153">**For second order updates, multiple updates can be installed by just running hello `Start-HcsHotfix cmdlet` and pointing toohello folder where second order updates are located. hello cmdlet will execute all hello updates available in hello folder.**</span></span> <span data-ttu-id="b07ad-154">Если обновление уже установлено, логика обновления hello обнаружит и не применить это обновление.</span><span class="sxs-lookup"><span data-stu-id="b07ad-154">If an update is already installed, hello update logic will detect that and not apply that update.</span></span> 

<span data-ttu-id="b07ad-155">После установки всех исправлений hello использовать hello `Get-HcsSystem` командлета.</span><span class="sxs-lookup"><span data-stu-id="b07ad-155">After all hello hotfixes are installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="b07ad-156">должен быть Hello версии:</span><span class="sxs-lookup"><span data-stu-id="b07ad-156">hello versions should be:</span></span>

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="b07ad-157">tooinstall исправления режима обслуживания</span><span class="sxs-lookup"><span data-stu-id="b07ad-157">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="b07ad-158">Используйте обновления встроенного по диска tooinstall KB4011837.</span><span class="sxs-lookup"><span data-stu-id="b07ad-158">Use KB4011837 tooinstall disk firmware updates.</span></span> <span data-ttu-id="b07ad-159">Эти обновления нарушают работу и занять toocomplete около 30 минут.</span><span class="sxs-lookup"><span data-stu-id="b07ad-159">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="b07ad-160">Вы можете tooinstall в период планового обслуживания, подключающегося последовательной консоли устройства toohello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-160">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="b07ad-161">Обратите внимание, что если встроенного по диска уже обновлена, вам не нужно tooinstall эти обновления.</span><span class="sxs-lookup"><span data-stu-id="b07ad-161">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="b07ad-162">Запустите hello `Get-HcsUpdateAvailability` из последовательной консоли toocheck hello устройства, если обновления доступны, является ли hello обновляет являются критическими (режим обслуживания) или не нарушают работу (обычный режим) обновления.</span><span class="sxs-lookup"><span data-stu-id="b07ad-162">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="b07ad-163">обновления встроенного по диска tooinstall hello, следуйте приведенным ниже инструкциям hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-163">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="b07ad-164">Поместите hello устройства в режим обслуживания hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-164">Place hello device in hello maintenance mode.</span></span> <span data-ttu-id="b07ad-165">**Обратите внимание, что не следует использовать удаленное взаимодействие Windows PowerShell при подключении tooa устройство находится в режиме обслуживания. Вместо этого используйте этот командлет на контроллере устройства hello при подключении через последовательную консоль устройства hello.**</span><span class="sxs-lookup"><span data-stu-id="b07ad-165">**Note that you should not use Windows PowerShell remoting when connecting tooa device in maintenance mode. Instead run this cmdlet on hello device controller when connected through hello device serial console.**</span></span> <span data-ttu-id="b07ad-166">Тип:</span><span class="sxs-lookup"><span data-stu-id="b07ad-166">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="b07ad-167">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="b07ad-167">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="b07ad-168">Оба контроллера hello перезапустите в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b07ad-168">Both hello controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="b07ad-169">обновление встроенного по диска hello tooinstall, тип</span><span class="sxs-lookup"><span data-stu-id="b07ad-169">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="b07ad-170">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="b07ad-170">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="b07ad-171">Монитор hello установка выполняется с помощью `Get-HcsUpdateStatus` команды.</span><span class="sxs-lookup"><span data-stu-id="b07ad-171">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="b07ad-172">Hello обновление будет завершено, после hello `RunInProgress` изменяет слишком`False`.</span><span class="sxs-lookup"><span data-stu-id="b07ad-172">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="b07ad-173">По завершении установки hello перезапуска контроллера hello, на какие hello было установлено исправление режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b07ad-173">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="b07ad-174">Войдите в систему как вариант 1 с полным доступом и проверка версии встроенного по диска hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-174">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="b07ad-175">Тип:</span><span class="sxs-lookup"><span data-stu-id="b07ad-175">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="b07ad-176">Hello ожидаемого версии встроенного по диска:</span><span class="sxs-lookup"><span data-stu-id="b07ad-176">hello expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   <span data-ttu-id="b07ad-177">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="b07ad-177">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17820
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
   
    <span data-ttu-id="b07ad-178">Запустите hello `Get-HcsFirmwareVersion` команду на второй контроллер tooverify hello, hello версия программного обеспечения был обновлен.</span><span class="sxs-lookup"><span data-stu-id="b07ad-178">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="b07ad-179">Затем можно выйти из режима обслуживания hello.</span><span class="sxs-lookup"><span data-stu-id="b07ad-179">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="b07ad-180">toodo таким образом, введите следующую команду для каждого устройства контроллера hello:</span><span class="sxs-lookup"><span data-stu-id="b07ad-180">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="b07ad-181">контроллеры Hello перезапустите при выходе из режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b07ad-181">hello controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="b07ad-182">После встроенного по диска hello успешного применения обновлений и устройство hello вышел из режима обслуживания, возвращаемого toohello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b07ad-182">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="b07ad-183">Обратите внимание, что этот портал hello может показывать установку обновлений в режиме обслуживания hello на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="b07ad-183">Note that hello portal might not show that you installed hello maintenance mode updates for 24 hours.</span></span>

