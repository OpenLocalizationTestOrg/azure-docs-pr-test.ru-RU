<!--author=alkohli last changed: 02/10/17-->

#### <a name="toodownload-hotfixes"></a>toodownload исправления

Выполните следующие действия toodownload hello обновления из каталога Центра обновления Майкрософт hello hello.

1. Запустите Internet Explorer и перейдите слишком[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Если вы впервые используете hello каталога Центра обновления Майкрософт на этом компьютере, нажмите кнопку **установить** при запрашиваемые tooinstall hello надстройку каталога Центра обновления Майкрософт.

    ![Установка каталога](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. В поле поиска hello hello каталога Центра обновления Майкрософт, введите номер базы знаний (KB) hello hello исправления требуется toodownload, например **4011839**, а затем нажмите кнопку **поиска**.
   
    Hello исправление вхождение отображаться, например, **совокупное 4.0 обновления пакета программного обеспечения для StorSimple серии 8000**.
   
    ![Поиск в каталоге](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)

4. Щелкните элемент **Загрузить**. Укажите или **Обзор** tooa локального место tooappear загружает hello. Выберите файлы hello toodownload toohello указано расположение и папку. Папка Hello также может быть скопированный tooa сетевая папка, которая доступна из устройства hello.
5. Поиск дополнительных исправления, перечисленные в приведенной выше таблице hello (**4011841**), и соответствующего hello загрузки файлов toohello определенные папки, перечисленные в предшествующей таблице hello.

> [!NOTE]
> исправления Hello должен быть доступен с обоих контроллеров toodetect, все потенциальные ошибки сообщений hello однорангового контроллера.
>
> Hello исправления необходимо скопировать в разные папки и 3. Например, обновление программного обеспечения и Cis/MDS агента hello устройства могут быть скопированы в _FirstOrderUpdate_ hello папки, все другие обновления не нарушают работу может быть скопирован в hello _SecondOrderUpdate_ папки, и обновления в режиме обслуживания копируются в _ThirdOrderUpdate_ папки.

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall исправления обычный режим

Выполните следующие шаги tooinstall hello и проверьте исправления в обычном режиме. Если вы установили их с помощью hello классический портал Azure, пропускать слишком[Установка исправлений в режиме обслуживания,](#to-install-and-verify-maintenance-mode-hotfixes).

1. исправления tooinstall hello, доступа к интерфейсу Windows PowerShell hello в последовательной консоли устройства StorSimple. Выполните hello подробные инструкции в [последовательной консоли используйте PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Hello командной строки, нажмите клавишу **ввод**.
2. Выберите **вариант 1** toolog на устройстве toohello с полным доступом. Мы рекомендуем установить исправление hello на пассивный контроллер hello сначала.
3. исправление tooinstall hello в hello командной строке введите:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Используйте IP, а не DNS в пути к папке в hello выше команды. параметр Hello учетных данных используется только в том случае, если вы обращаетесь ресурс прошедшего проверку подлинности.
   
    Рекомендуется использовать параметр tooaccess hello учетных данных долей. Даже общих папок, которые открыты слишком пребывание «everyone» обычно не открыть toounauthenticated пользователей.
   
    Укажите hello пароль при появлении запроса.
   
    Ниже приведен пример выходных данных для установки первого порядка обновления hello. Для первого порядка обновления hello потребуется toopoint toohello определенного файла.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. Тип **Y** при запрашиваемые tooconfirm hello установки исправления.
5. Мониторинг hello обновления с помощью hello `Get-HcsUpdateStatus` командлета. Обновление Hello сначала будет выполнена на пассивный контроллер hello. Здравствуйте, после обновляется hello пассивного контроллера, произойдет отработка отказа и обновление hello затем будут применяться на другой контроллер. Hello обновления завершается после завершения обновления обоих контроллеров hello.
   
    Hello следующий образец вывода показывает hello обновление выполняется. Hello `RunInprogress` будет `True` при hello идет обновление.

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Следующий пример выходных данных Hello указывает, что завершения обновления hello. Hello `RunInProgress` будет `False` после завершения обновления hello.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > В некоторых случаях hello отчеты командлет `False` при обновлении hello она все еще выполняется. tooensure, hello исправление завершена, подождите несколько минут, выполните эту команду повторно и убедитесь, что hello `RunInProgress` — `False`. Если это так, исправление hello завершена.

6. После завершения обновления программного обеспечения hello проверки версий программного обеспечения системы hello. Тип:
   
    `Get-HcsSystem`
   
    Вы должны увидеть следующие версии hello.
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    Если номер версии hello остается неизменным после применения обновления hello, это означает, что сбой tooapply исправление hello. В этом случае обратитесь за дополнительной помощью в [службу поддержки Майкрософт](../articles/storsimple/storsimple-contact-microsoft-support.md).
     
    > [!IMPORTANT]
    > Необходимо перезапустить активный контроллер hello через hello `Restart-HcsController` командлет перед применением hello следующего обновления.
     
7. Повторите шаги 3 – 5 tooinstall hello tooyour загрузить агент Cis/MDS _FirstOrderUpdate_ папки. 
8. Повторите шаги 3 – 5 tooinstall hello второго порядка обновления. **Для второго порядка обновлений, можно установить несколько обновлений, просто выполнив hello `Start-HcsHotfix cmdlet` и указывающего toohello папку, где находятся второго порядка обновления. hello командлет выполнит все hello обновления, доступные в папке hello.** Если обновление уже установлено, логика обновления hello обнаружит и не применить это обновление. 

После установки всех исправлений hello использовать hello `Get-HcsSystem` командлета. должен быть Hello версии:

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall исправления режима обслуживания
Используйте обновления встроенного по диска tooinstall KB4011837. Эти обновления нарушают работу и занять toocomplete около 30 минут. Вы можете tooinstall в период планового обслуживания, подключающегося последовательной консоли устройства toohello.

Обратите внимание, что если встроенного по диска уже обновлена, вам не нужно tooinstall эти обновления. Запустите hello `Get-HcsUpdateAvailability` из последовательной консоли toocheck hello устройства, если обновления доступны, является ли hello обновляет являются критическими (режим обслуживания) или не нарушают работу (обычный режим) обновления.

обновления встроенного по диска tooinstall hello, следуйте приведенным ниже инструкциям hello.

1. Поместите hello устройства в режим обслуживания hello. **Обратите внимание, что не следует использовать удаленное взаимодействие Windows PowerShell при подключении tooa устройство находится в режиме обслуживания. Вместо этого используйте этот командлет на контроллере устройства hello при подключении через последовательную консоль устройства hello.** Тип:
   
    `Enter-HcsMaintenanceMode`
   
    Результат выполнения команды показан ниже.
   
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
   
    Оба контроллера hello перезапустите в режим обслуживания.
2. обновление встроенного по диска hello tooinstall, тип
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Результат выполнения команды показан ниже.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
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
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   Результат выполнения команды показан ниже.
   
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
   
    Запустите hello `Get-HcsFirmwareVersion` команду на второй контроллер tooverify hello, hello версия программного обеспечения был обновлен. Затем можно выйти из режима обслуживания hello. toodo таким образом, введите следующую команду для каждого устройства контроллера hello:
   
   `Exit-HcsMaintenanceMode`

5. контроллеры Hello перезапустите при выходе из режима обслуживания. После встроенного по диска hello успешного применения обновлений и устройство hello вышел из режима обслуживания, возвращаемого toohello классический портал Azure. Обратите внимание, что этот портал hello может показывать установку обновлений в режиме обслуживания hello на 24 часа.

