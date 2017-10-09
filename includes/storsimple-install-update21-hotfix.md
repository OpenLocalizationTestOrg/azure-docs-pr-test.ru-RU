<!--author=alkohli last changed: 05/19/16-->

#### <a name="toodownload-hotfixes"></a>toodownload исправления
Выполните следующие действия toodownload hello обновления из каталога Центра обновления Майкрософт hello hello.

1. Запустите Internet Explorer и перейдите слишком[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Если вы впервые используете hello каталога Центра обновления Майкрософт на этом компьютере, нажмите кнопку **установить** при запрашиваемые tooinstall hello надстройку каталога Центра обновления Майкрософт.
    ![Установка каталога](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)
3. В поле поиска hello hello каталога Центра обновления Майкрософт, введите номер базы знаний (KB) hello hello исправления требуется toodownload, например **3179904**, а затем нажмите кнопку **поиска**.
   
    Hello исправление вхождение отображаться, например, **совокупное 2.2 обновление пакета программного обеспечения для StorSimple серии 8000**.
   
    ![Поиск в каталоге](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. Щелкните **Добавить**. Обновление Hello добавляется toohello корзины.
5. Поиск дополнительных исправления, перечисленные в приведенной выше таблице hello (**3103616**, **3146621**) и добавьте каждый toohello корзины.
6. Щелкните **Просмотреть корзину**.
7. Щелкните элемент **Загрузить**. Укажите или **Обзор** tooa локального место tooappear загружает hello. Hello обновления загружаются toohello определенное место и помещается в подпапке с точно такое же имя, как и при обновлении hello hello. Папка Hello также может быть скопированный tooa сетевая папка, которая доступна из устройства hello.

> [!NOTE]
> исправления Hello должен быть доступен с обоих контроллеров toodetect, все потенциальные ошибки сообщений hello однорангового контроллера.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall исправления обычный режим
Выполните следующие шаги tooinstall hello и проверьте исправления в обычном режиме. Если вы установили их с помощью hello портала Azure пропускать слишком[Установка исправлений в режиме обслуживания,](#to-install-and-verify-maintenance-mode-hotfixes).

1. исправления tooinstall hello, доступа к интерфейсу Windows PowerShell hello в последовательной консоли устройства StorSimple. Выполните hello подробные инструкции в [последовательной консоли используйте PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Hello командной строки, нажмите клавишу **ввод**.
2. Выберите **вариант 1** toolog на устройстве toohello с полным доступом. Мы рекомендуем установить исправление hello на пассивный контроллер hello сначала.
3. исправление tooinstall hello в hello командной строке введите:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Используйте IP, а не DNS в пути к папке в hello выше команды. параметр Hello учетных данных используется только в том случае, если вы обращаетесь ресурс прошедшего проверку подлинности.
   
    Рекомендуется использовать параметр tooaccess hello учетных данных долей. Даже общих папок, которые открыты слишком пребывание «everyone» обычно не открыть toounauthenticated пользователей.
   
    Укажите hello пароль при появлении запроса.
   
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
   
   > [!IMPORTANT]
   > Если установка обновления 2.2, установите только двоичный файл hello начинаются с «all hcsmdssoftwareudpate». Не устанавливайте hello Cis и hello MDS обновление агента, предваряемые фразой cismdsagentupdatebundle все. Таким образом toodo сбоя приведет к ошибке. 

5. Мониторинг hello обновления с помощью hello `Get-HcsUpdateStatus` командлета. Обновление Hello сначала будет выполнена на пассивный контроллер hello. Здравствуйте, после обновляется hello пассивного контроллера, произойдет отработка отказа и обновление hello затем будут применяться на другой контроллер. Hello обновления завершается после завершения обновления обоих контроллеров hello.
   
    Hello следующий образец вывода показывает hello обновление выполняется. Hello `RunInprogress` будет `True` при hello идет обновление.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 5/5/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Следующий пример выходных данных Hello указывает, что завершения обновления hello. Hello `RunInProgress` будет `False` после завершения обновления hello.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 5/17/2016 9:15:55 AM
    LastUpdateTimestamp : 5/17/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > В некоторых случаях hello отчеты командлет `False` при обновлении hello она все еще выполняется. tooensure, hello исправление завершена, подождите несколько минут, выполните эту команду повторно и убедитесь, что hello `RunInProgress` — `False`. Если это так, исправление hello завершена.

1. После завершения обновления программного обеспечения hello проверки версий программного обеспечения системы hello. Тип:
   
    `Get-HcsSystem`
   
    Вы должны увидеть следующие версии hello.
   
   * `HcsSoftwareVersion: 6.3.9600.17708`
   * `CisAgentVersion: 1.0.9299.0`
   * `MdsAgentVersion: 30.0.4698.16` 
     
     Если номера версий hello не изменяются после применения обновления hello, это означает, что сбой tooapply исправление hello. В этом случае обратитесь за дополнительной помощью в [службу поддержки Майкрософт](../articles/storsimple/storsimple-contact-microsoft-support.md).
     
     > [!IMPORTANT]
     > Необходимо перезапустить активный контроллер hello через hello `Restart-HcsController` командлет перед применением hello оставшихся обновлений. 
     > 
     > 
2. Повторите шаги 3 – 5 tooinstall hello оставшихся исправления в обычном режиме.
   
   * Обновление iSCSI Hello KB3146621
   * Обновление WMI Hello KB3103616
3. Этот шаг можно пропустить, если обновление выполняется с обновления 2. Если вы обновляете из tooUpdate предыдущие версии 2, необходимо также toodownload:

    - драйвер Hello LSI KB3121900

    - Обновление Spaceport Hello KB3090322

    - Обновление Storport Hello KB3080728

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall исправления режима обслуживания
Используйте обновления встроенного по диска tooinstall KB3121899. Эти обновления нарушают работу и занять toocomplete около 30 минут. Вы можете tooinstall в период планового обслуживания, подключающегося последовательной консоли устройства toohello.

Обратите внимание, что если встроенного по диска уже обновлена, вам не нужно tooinstall эти обновления. Запустите hello `Get-HcsUpdateAvailability` из последовательной консоли toocheck hello устройства, если обновления доступны, является ли hello обновляет являются критическими (режим обслуживания) или не нарушают работу (обычный режим) обновления.

обновления встроенного по диска tooinstall hello, следуйте приведенным ниже инструкциям hello.

1. Поместите hello устройства в режим обслуживания hello. Обратите внимание, что не следует использовать удаленное взаимодействие Windows PowerShell при подключении tooa устройство находится в режиме обслуживания. Вместо этого используйте этот командлет на контроллере устройства hello при подключении через последовательную консоль устройства hello. Тип:
   
    `Enter-HcsMaintenanceMode`
   
    Результат выполнения команды показан ниже.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
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
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Монитор hello установка выполняется с помощью `Get-HcsUpdateStatus` команды. Hello обновление будет завершено, после hello `RunInProgress` изменяет слишком`False`.
4. По завершении установки hello перезапуска контроллера hello, на какие hello было установлено исправление режима обслуживания. Войдите в систему как вариант 1 с полным доступом и проверка версии встроенного по диска hello. Тип:
   
   `Get-HcsFirmwareVersion`
   
   Hello ожидаемого версии встроенного по диска:
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   Результат выполнения команды показан ниже.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
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
   
    Запустите hello `Get-HcsFirmwareVersion` команду на второй контроллер tooverify hello, hello версия программного обеспечения был обновлен. Затем можно выйти из режима обслуживания hello. toodo таким образом, введите следующую команду для каждого устройства контроллера hello:
   
   `Exit-HcsMaintenanceMode`
5. контроллеры Hello перезапустите при выходе из режима обслуживания. После встроенного по диска hello успешного применения обновлений и устройство hello вышел из режима обслуживания, возвращаемого toohello классический портал Azure. Обратите внимание, что этот портал hello может показывать установку обновлений в режиме обслуживания hello на 24 часа.

