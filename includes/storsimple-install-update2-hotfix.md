<!--author=alkohli last changed: 03/17/16-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="6b39f-101">toodownload исправления</span><span class="sxs-lookup"><span data-stu-id="6b39f-101">toodownload hotfixes</span></span>
<span data-ttu-id="6b39f-102">Выполните следующие действия toodownload hello обновления из каталога Центра обновления Майкрософт hello hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="6b39f-103">Запустите Internet Explorer и перейдите слишком[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6b39f-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="6b39f-104">Если вы впервые используете hello каталога Центра обновления Майкрософт на этом компьютере, нажмите кнопку **установить** при запрашиваемые tooinstall hello надстройку каталога Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6b39f-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="6b39f-105">![Установка каталога](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="6b39f-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="6b39f-106">В поле поиска hello hello каталога Центра обновления Майкрософт, введите номер базы знаний (KB) hello hello исправления требуется toodownload, например **3121901**, а затем нажмите кнопку **поиска**.</span><span class="sxs-lookup"><span data-stu-id="6b39f-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3121901**, and then click **Search**.</span></span>
   
    <span data-ttu-id="6b39f-107">Hello исправление вхождение отображаться, например, **совокупное 2.0 обновления пакета программного обеспечения для StorSimple серии 8000**.</span><span class="sxs-lookup"><span data-stu-id="6b39f-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 2.0 for StorSimple 8000 Series**.</span></span>
   
    ![Поиск в каталоге](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="6b39f-109">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6b39f-109">Click **Add**.</span></span> <span data-ttu-id="6b39f-110">Обновление Hello добавляется toohello корзины.</span><span class="sxs-lookup"><span data-stu-id="6b39f-110">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="6b39f-111">Поиск дополнительных исправления, перечисленные в приведенной выше таблице hello (**3121900**, **3080728**, **3090322**, и **3121899**) и добавьте каждый Hello корзины.</span><span class="sxs-lookup"><span data-stu-id="6b39f-111">Search for any additional hotfixes listed in hello table above (**3121900**, **3080728**, **3090322**, and **3121899**), and add each hello basket.</span></span>
6. <span data-ttu-id="6b39f-112">Щелкните **Просмотреть корзину**.</span><span class="sxs-lookup"><span data-stu-id="6b39f-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="6b39f-113">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="6b39f-113">Click **Download**.</span></span> <span data-ttu-id="6b39f-114">Укажите или **Обзор** tooa локального место tooappear загружает hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="6b39f-115">Hello обновления загружаются toohello определенное место и помещается во вложенную папку с точно такое же имя, как и при обновлении hello hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-115">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="6b39f-116">Папка Hello также может быть скопированный tooa сетевая папка, которая доступна из устройства hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="6b39f-117">исправления Hello должен быть доступен с обоих контроллеров toodetect, все потенциальные ошибки сообщений hello однорангового контроллера.</span><span class="sxs-lookup"><span data-stu-id="6b39f-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="6b39f-118">tooinstall исправления обычный режим</span><span class="sxs-lookup"><span data-stu-id="6b39f-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="6b39f-119">Выполните следующие шаги tooinstall hello и проверьте исправления в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="6b39f-119">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="6b39f-120">Если вы установили их с помощью hello портала Azure пропускать слишком[Установка исправлений в режиме обслуживания,](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="6b39f-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="6b39f-121">исправления tooinstall hello, доступа к интерфейсу Windows PowerShell hello в последовательной консоли устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6b39f-121">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="6b39f-122">Выполните hello подробные инструкции в [последовательной консоли используйте PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="6b39f-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="6b39f-123">Hello командной строки, нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="6b39f-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="6b39f-124">Выберите **вариант 1** toolog на устройстве toohello с полным доступом.</span><span class="sxs-lookup"><span data-stu-id="6b39f-124">Select **Option 1** toolog on toohello device with full access.</span></span>
3. <span data-ttu-id="6b39f-125">исправление tooinstall hello в hello командной строке введите:</span><span class="sxs-lookup"><span data-stu-id="6b39f-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="6b39f-126">Используйте IP, а не DNS в пути к папке в hello выше команды.</span><span class="sxs-lookup"><span data-stu-id="6b39f-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="6b39f-127">параметр Hello учетных данных используется только в том случае, если вы обращаетесь ресурс прошедшего проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="6b39f-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="6b39f-128">Рекомендуется использовать параметр tooaccess hello учетных данных долей.</span><span class="sxs-lookup"><span data-stu-id="6b39f-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="6b39f-129">Даже общих папок, которые открыты слишком пребывание «everyone» обычно не открыть toounauthenticated пользователей.</span><span class="sxs-lookup"><span data-stu-id="6b39f-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="6b39f-130">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="6b39f-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```
4. <span data-ttu-id="6b39f-131">Тип **Y** при запрашиваемые tooconfirm hello установки исправления.</span><span class="sxs-lookup"><span data-stu-id="6b39f-131">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="6b39f-132">Мониторинг hello обновления с помощью hello `Get-HcsUpdateStatus` командлета.</span><span class="sxs-lookup"><span data-stu-id="6b39f-132">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="6b39f-133">Hello следующий образец вывода показывает hello обновление выполняется.</span><span class="sxs-lookup"><span data-stu-id="6b39f-133">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="6b39f-134">Hello `RunInprogress` будет `True` при hello идет обновление.</span><span class="sxs-lookup"><span data-stu-id="6b39f-134">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 12/21/2015 10:36:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="6b39f-135">Следующий пример выходных данных Hello указывает, что завершения обновления hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-135">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="6b39f-136">Hello `RunInProgress` будет `False` после завершения обновления hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-136">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 12/21/2015 10:59:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="6b39f-137">В некоторых случаях hello отчеты командлет `False` при обновлении hello она все еще выполняется.</span><span class="sxs-lookup"><span data-stu-id="6b39f-137">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="6b39f-138">tooensure, hello исправление завершена, подождите несколько минут, выполните эту команду повторно и убедитесь, что hello `RunInProgress` — `False`.</span><span class="sxs-lookup"><span data-stu-id="6b39f-138">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="6b39f-139">Если это так, исправление hello завершена.</span><span class="sxs-lookup"><span data-stu-id="6b39f-139">If it is, then hello hotfix has completed.</span></span>

6. <span data-ttu-id="6b39f-140">После программного обеспечения hello обновление является полным, повторите шаги 3 – 5 tooinstall и монитор hello SaaS агента и MDS агента.</span><span class="sxs-lookup"><span data-stu-id="6b39f-140">After hello software update is complete, repeat steps 3-5 tooinstall and monitor hello SaaS agent and MDS agent .</span></span> <span data-ttu-id="6b39f-141">Убедитесь, что `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` установлен до `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span><span class="sxs-lookup"><span data-stu-id="6b39f-141">Ensure that `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is installed before `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span></span>
7. <span data-ttu-id="6b39f-142">Проверка версий программного обеспечения системы hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-142">Verify hello system software versions.</span></span> <span data-ttu-id="6b39f-143">Тип:</span><span class="sxs-lookup"><span data-stu-id="6b39f-143">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="6b39f-144">Вы должны увидеть следующие версии hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-144">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="6b39f-145">HcsSoftwareVersion: 6.3.9600.17673</span><span class="sxs-lookup"><span data-stu-id="6b39f-145">HcsSoftwareVersion: 6.3.9600.17673</span></span>
   * <span data-ttu-id="6b39f-146">CisAgentVersion: 1.0.9150.0</span><span class="sxs-lookup"><span data-stu-id="6b39f-146">CisAgentVersion: 1.0.9150.0</span></span>
   * <span data-ttu-id="6b39f-147">MdsAgentVersion: 30.0.4698.13</span><span class="sxs-lookup"><span data-stu-id="6b39f-147">MdsAgentVersion: 30.0.4698.13</span></span>
     
     <span data-ttu-id="6b39f-148">Если номера версий hello не изменяются после применения обновления hello, это означает, что сбой tooapply исправление hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-148">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="6b39f-149">В этом случае обратитесь за дополнительной помощью в [службу поддержки Майкрософт](../articles/storsimple/storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="6b39f-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
8. <span data-ttu-id="6b39f-150">Повторите шаги 3 – 5 tooinstall hello оставшихся исправления в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="6b39f-150">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="6b39f-151">Hello драйвера LSI - KB3121900</span><span class="sxs-lookup"><span data-stu-id="6b39f-151">hello LSI driver - KB3121900</span></span>
   * <span data-ttu-id="6b39f-152">Обновление Storport - KB3080728 Hello</span><span class="sxs-lookup"><span data-stu-id="6b39f-152">hello Storport update - KB3080728</span></span>
   * <span data-ttu-id="6b39f-153">Обновление Spaceport - KB3090322 Hello</span><span class="sxs-lookup"><span data-stu-id="6b39f-153">hello Spaceport update - KB3090322</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="6b39f-154">tooinstall исправления режима обслуживания</span><span class="sxs-lookup"><span data-stu-id="6b39f-154">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="6b39f-155">Используйте обновления встроенного по диска tooinstall KB3121899.</span><span class="sxs-lookup"><span data-stu-id="6b39f-155">Use KB3121899 tooinstall disk firmware updates.</span></span> <span data-ttu-id="6b39f-156">Эти обновления нарушают работу и занять toocomplete около 30 минут.</span><span class="sxs-lookup"><span data-stu-id="6b39f-156">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="6b39f-157">Вы можете tooinstall в период планового обслуживания, подключающегося последовательной консоли устройства toohello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-157">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="6b39f-158">Обратите внимание, что если встроенного по диска уже обновлена, вам не нужно tooinstall эти обновления.</span><span class="sxs-lookup"><span data-stu-id="6b39f-158">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="6b39f-159">Запустите hello `Get-HcsUpdateAvailability` из последовательной консоли toocheck hello устройства, если обновления доступны, является ли hello обновляет являются критическими (режим обслуживания) или не нарушают работу (обычный режим) обновления.</span><span class="sxs-lookup"><span data-stu-id="6b39f-159">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="6b39f-160">обновления встроенного по диска tooinstall hello, следуйте приведенным ниже инструкциям hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-160">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="6b39f-161">Поместите hello устройства в режим обслуживания hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-161">Place hello device in hello Maintenance mode.</span></span> <span data-ttu-id="6b39f-162">Обратите внимание, что не следует использовать удаленное взаимодействие Windows PowerShell при подключении tooa устройство находится в режиме обслуживания.</span><span class="sxs-lookup"><span data-stu-id="6b39f-162">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="6b39f-163">Вместо этого используйте этот командлет на контроллере устройства hello при подключении через последовательную консоль устройства hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-163">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="6b39f-164">Тип:</span><span class="sxs-lookup"><span data-stu-id="6b39f-164">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="6b39f-165">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="6b39f-165">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17664
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="6b39f-166">Оба контроллера hello перезапустите в режим обслуживания.</span><span class="sxs-lookup"><span data-stu-id="6b39f-166">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="6b39f-167">обновление встроенного по диска hello tooinstall, тип</span><span class="sxs-lookup"><span data-stu-id="6b39f-167">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="6b39f-168">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="6b39f-168">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="6b39f-169">Монитор hello установка выполняется с помощью `Get-HcsUpdateStatus` команды.</span><span class="sxs-lookup"><span data-stu-id="6b39f-169">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="6b39f-170">Hello обновление будет завершено, после hello `RunInProgress` изменяет слишком`False`.</span><span class="sxs-lookup"><span data-stu-id="6b39f-170">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="6b39f-171">По завершении установки hello перезапуска контроллера hello, на какие hello было установлено исправление режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="6b39f-171">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="6b39f-172">Войдите в систему как вариант 1 с полным доступом и проверка версии встроенного по диска hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-172">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="6b39f-173">Тип:</span><span class="sxs-lookup"><span data-stu-id="6b39f-173">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="6b39f-174">Hello ожидаемого версии встроенного по диска:</span><span class="sxs-lookup"><span data-stu-id="6b39f-174">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="6b39f-175">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="6b39f-175">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17664
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
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
   
    <span data-ttu-id="6b39f-176">Запустите hello `Get-HcsFirmwareVersion` команду на второй контроллер tooverify hello, hello версия программного обеспечения был обновлен.</span><span class="sxs-lookup"><span data-stu-id="6b39f-176">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="6b39f-177">Затем можно выйти из режима обслуживания hello.</span><span class="sxs-lookup"><span data-stu-id="6b39f-177">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="6b39f-178">toodo таким образом, введите следующую команду для каждого устройства контроллера hello:</span><span class="sxs-lookup"><span data-stu-id="6b39f-178">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="6b39f-179">контроллеры Hello перезапустите при выходе из режима обслуживания.</span><span class="sxs-lookup"><span data-stu-id="6b39f-179">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="6b39f-180">После встроенного по диска hello успешного применения обновлений и устройство hello вышел из режима обслуживания, возвращаемого toohello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6b39f-180">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="6b39f-181">Обратите внимание, что этот портал hello может показывать установку обновлений в режиме обслуживания hello на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="6b39f-181">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

