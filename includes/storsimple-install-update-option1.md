<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a>toodownload исправления
Выполните следующее обновление программного обеспечения hello toodownload действия hello.

1. Запустите Internet Explorer и перейдите слишком[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Если вы впервые используете hello каталога Центра обновления Майкрософт на этом компьютере, нажмите кнопку **установить** при запрашиваемые tooinstall hello надстройку каталога Центра обновления Майкрософт.
    ![Установка каталога](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)
3. В поле поиска hello hello каталога Центра обновления Майкрософт, введите номер базы знаний (KB) hello hello исправления требуется toodownload, например **3063418**, а затем нажмите кнопку **поиска**.
4. Вы увидите hello **1.2 устройства StorSimple обновление обновление** пакета. Щелкните **Добавить**. Обновление Hello будут добавлены toohello корзины.
5. Поиск дополнительных исправления, перечисленные в приведенной выше таблице hello (**3043005** и **3063416**) и добавьте каждый hello корзины.
6. Щелкните **Просмотреть корзину**.
   
    ![Просмотреть корзину](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. Щелкните элемент **Загрузить**. Укажите или **Обзор** tooa локального место tooappear загружает hello. Hello обновления загружаются toohello определенное место и помещается во вложенную папку с точно такое же имя, как и при обновлении hello hello. Папка Hello также может быть скопированный tooa сетевая папка, которая доступна из устройства hello.

> [!NOTE]
> исправления Hello должен быть доступен с обоих контроллеров toodetect, все потенциальные ошибки сообщений hello однорангового контроллера.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall исправления обычный режим
Выполните следующие шаги tooinstall hello и исправления для hello обычный режим. Если вы установили их с помощью hello портала Azure пропускать слишком[Установка исправлений в режиме обслуживания,](#to-install-and-verify-maintenance-mode-hotfixes).

1. обновления программного обеспечения tooinstall hello, доступа к интерфейсу Windows PowerShell hello в последовательной консоли устройства StorSimple. Выполните hello подробные инструкции в [последовательной консоли используйте PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Hello командной строки, нажмите клавишу **ввод**.
2. Выберите **вариант 1** toolog на устройстве toohello с полным доступом.
3. tooinstall hello пакета обновления на hello командной строке введите:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Используйте IP, а не DNS в пути к папке в hello выше команды. параметр Hello учетных данных используется только в том случае, если вы обращаетесь ресурс прошедшего проверку подлинности.
   
    Рекомендуется использовать параметр tooaccess hello учетных данных долей. Даже общих папок, которые открыты слишком пребывание «everyone» обычно не открыть toounauthenticated пользователей.
   
    Результат выполнения команды показан ниже.
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. Тип **Y** при запрашиваемые tooconfirm hello установки исправления.
5. Мониторинг hello обновления с помощью hello `Get-HcsUpdateStatus` командлета.
   
    Hello следующий образец вывода показывает hello обновление выполняется. Hello `RunInprogress` будет `True` при hello идет обновление.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Следующий пример выходных данных Hello указывает, что завершения обновления hello. Hello `RunInProgress` будет `False` после завершения обновления hello.

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > В некоторых случаях hello отчеты командлет `False` при обновлении hello она все еще выполняется. tooensure, hello исправление завершена, подождите несколько минут, выполните эту команду повторно и убедитесь, что hello `RunInProgress` — `False`. Если это так, исправление hello завершена.
   > 
   > 
6. После завершения обновления программного обеспечения hello проверки версий программного обеспечения системы hello. Введите следующую команду hello:
   
    `Get-HcsSystem`
   
    Вы должны увидеть следующие версии hello.
   
   * HcsSoftwareVersion: 6.3.9600.17584
   * CisAgentVersion: 1.0.9049.0
   * MdsAgentVersion: 26.0.4696.1433
     
     Если номера версий hello не изменяются после применения обновления hello, это означает, что сбой tooapply исправление hello. В этом случае обратитесь за дополнительной помощью в [службу поддержки Майкрософт](../articles/storsimple/storsimple-contact-microsoft-support.md).
7. Повторите шаги 3 – 5 tooinstall hello оставшихся обычный режим исправления (KB3043005).

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall исправления режима обслуживания
Используйте обновления встроенного по диска tooinstall KB3063416. Эти обновления нарушают работу и принимать решения toocomplete 30 – 45 минут. Вы можете tooinstall в период планового обслуживания, подключающегося последовательной консоли устройства toohello.

обновления встроенного по диска tooinstall hello, следуйте приведенным ниже инструкциям hello.

1. Поместите hello устройства в режим обслуживания. Обратите внимание, что не следует использовать удаленное взаимодействие Windows PowerShell при подключении tooa устройство находится в режиме обслуживания. Вам потребуется toorun этот командлет на контроллере устройства hello при подключении через последовательную консоль устройства hello. Тип:
   
    `Enter-HcsMaintenanceMode`
   
    Результат выполнения команды показан ниже.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    Оба контроллера hello перезапустите в режим обслуживания.
2. обновление встроенного по диска hello tooinstall, тип
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Результат выполнения команды показан ниже.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Монитор hello установка выполняется с помощью `Get-HcsUpdateStatus` команды. Hello обновление будет завершено, после hello `RunInProgress` изменяет слишком`False`.
4. По завершении установки hello hello контроллера, на котором была установлена hello исправление режима обслуживания будет перезагружен. Войдите в систему как вариант 1 с полным доступом и проверка версии встроенного по диска hello. Тип:
   
   `Get-HcsFirmwareVersion`
   
   Hello ожидаемого версии встроенного по диска:
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   Запустите hello `Get-HcsFirmwareVersion` команду на второй контроллер tooverify hello, hello версия программного обеспечения был обновлен. Затем можно выйти из режима обслуживания hello. Введите следующую команду для каждого устройства контроллера hello:
   
   `Exit-HcsMaintenanceMode`
5. контроллеры Hello перезапустите при выходе из режима обслуживания. После встроенного по диска hello успешного применения обновлений и устройство hello вышел из режима обслуживания, возвращаемого toohello классический портал Azure. Обратите внимание, что этот портал hello может показывать установку обновлений в режиме обслуживания hello на 24 часа.

