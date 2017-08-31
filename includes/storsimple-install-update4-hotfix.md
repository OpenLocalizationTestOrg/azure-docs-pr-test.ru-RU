<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-download-hotfixes"></a>Загрузка исправления

Для загрузки обновления программного обеспечения из каталога обновления Майкрософт выполните следующие действия.

1. Запустите Internet Explorer и откройте страницу [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Если вы впервые используете каталог Центра обновления Майкрософт на этом компьютере, нажмите кнопку **Установить** , когда будет предложено установить надстройку каталога Центра обновления Майкрософт.

    ![Установка каталога](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. В поле поиска каталога Центра обновления Майкрософт введите номер необходимого исправления в базе знаний, например **4011839**, а затем нажмите кнопку **Найти**.
   
    Появится список исправлений, например **Совокупное обновление программного обеспечения версии 4.0 для StorSimple серии 8000**.
   
    ![Поиск в каталоге](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)

4. Щелкните элемент **Загрузить**. Укажите или **выберите** локальное расположение, в которое хотите скачать файлы. Выберите файлы для загрузки в указанное расположение и папку. Этот каталог также можно скопировать в сетевую папку, которая доступна с вашего устройства.
5. Найдите дополнительные исправления, перечисленные в приведенной выше таблице (**4011841**), и скачайте соответствующие файлы в папки, указанные в этой таблице.

> [!NOTE]
> Исправления должны быть доступны с обоих контроллеров, чтобы можно было получить любые возможные сообщения об ошибке от однорангового контроллера.
>
> Исправления необходимо скопировать в 3 отдельные папки. Например, обновление агента программного обеспечения устройства Cis/MDS необходимо скопировать в папку _FirstOrderUpdate_. Все остальные обновления, не нарушающие работу устройства, можно скопировать в папку _SecondOrderUpdate_, а обновления в режиме обслуживания — в папку _ThirdOrderUpdate_.

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a>Установка и проверка исправлений обычного режима

Выполните следующие действия для установки и проверки обычных исправлений. Если вы уже установили их с помощью классического портала Azure, перейдите к [установке и проверке исправлений режима обслуживания](#to-install-and-verify-maintenance-mode-hotfixes).

1. Чтобы установить исправления, откройте интерфейс Windows PowerShell на последовательной консоли своего устройства StorSimple. Подробные инструкции см. в разделе [Подключение к последовательной консоли устройства с помощью PuTTY](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). В командной строке нажмите клавишу **ВВОД**.
2. Выберите **Вариант 1** , чтобы войти на устройство с правами на полный доступ. Рекомендуем сначала установить исправление на пассивный контроллер.
3. Чтобы установить исправление, в командной строке введите следующую команду:
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    В указанной выше команде вместо DNS в адресе общей папки укажите IP-адрес. Параметр "credential" используется только для доступа к общему ресурсу с проверкой подлинности.
   
    Для доступа к общим ресурсам рекомендуем использовать параметр учетных данных. Даже те общие ресурсы, которые доступны для всех, обычно закрыты для пользователей, не прошедших проверку подлинности.
   
    В ответ на запрос введите пароль.
   
    Ниже приведен пример выходных данных для установки обновлений первого типа. Для обновления первого типа необходимо указать определенный файл.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. Введите **Y** , когда будет предложено подтвердить установку исправлений.
5. Проверьте обновление с помощью командлета `Get-HcsUpdateStatus` . Сначала обновится пассивный контроллер. После этого будет выполнена отработка отказа. Затем обновление будет применено на другом контроллере. Установка обновления завершится, когда оба контроллера будут обновлены.
   
    Ниже приведен пример выходных данных для обновления, которое выполняется. Пока обновление выполняется, `RunInprogress` будет иметь значение `True`.

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Ниже приведен пример выходных данных для обновления, установка которого завершена. После установки обновления `RunInProgress` будет иметь значение `False`.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > В некоторых случаях командлет выдает значение `False`, пока обновление еще устанавливается. Чтобы проверить установку обновления, подождите несколько минут, выполните эту команду еще раз и убедитесь в том, что `RunInProgress` имеет значение `False`. Если это так, значит, исправление установлено.

6. Когда установка обновления будет завершена, проверьте версии программного обеспечения системы. Тип:
   
    `Get-HcsSystem`
   
    Номера версий должны быть следующими:
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    Если после установки обновления номер версии не изменился, значит исправление установить не удалось. В этом случае обратитесь за дополнительной помощью в [службу поддержки Майкрософт](../articles/storsimple/storsimple-contact-microsoft-support.md).
     
    > [!IMPORTANT]
    > Прежде чем применять следующее обновление, необходимо перезапустить активный контроллер с помощью командлета `Restart-HcsController`.
     
7. Повторите шаги 3–5, чтобы установить агент Cis/MDS, скачанный в папку _FirstOrderUpdate_. 
8. Повторите шаги 3–5, чтобы установить обновления второго типа. **Для обновлений второго типа можно установить несколько обновлений, просто запустив командлет `Start-HcsHotfix cmdlet` и указав папку, где они находятся. Командлет выполнит все обновления, доступные в папке.** Если обновление уже установлено, логика обновления обнаружит это и не установит его. 

После установки всех исправлений используйте командлет `Get-HcsSystem`. Необходимые версии:

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a>Установка и проверка исправлений режима обслуживания
Используйте статью KB4011837, чтобы установить обновления встроенного ПО дисков. Эти обновления прерывают работу, и на их завершение может потребоваться около 30 минут. Данные обновления можно установить в период планового техобслуживания, подключившись к последовательной консоли устройства.

Обратите внимание, что если встроенное ПО диска уже обновлено, устанавливать эти обновления не требуется. Выполните командлет `Get-HcsUpdateAvailability` в последовательной консоли устройства, чтобы проверить, доступны ли обновления и являются ли они критическими (режим обслуживания) или некритическими (обычный режим).

Чтобы установить обновления встроенного ПО диска, следуйте приведенным ниже инструкциям.

1. Переведите устройство в режим обслуживания. **Обратите внимание, что не следует использовать удаленное взаимодействие Windows PowerShell при переключении устройства в режим обслуживания. Вместо этого запустите следующий командлет при подключении через последовательную консоль устройства.** Тип:
   
    `Enter-HcsMaintenanceMode`
   
    Результат выполнения команды показан ниже.
   
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
   
    После этого оба контроллера перезапускаются и переходят в режим обслуживания.
2. Чтобы установить обновление встроенного ПО диска, введите:
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    Результат выполнения команды показан ниже.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. Отслеживайте ход выполнения установки с помощью команды `Get-HcsUpdateStatus` . Обновление завершится, когда `RunInProgress` поменяется на `False`.
4. После завершения установки контроллер, на котором установлено исправление режима обслуживания, будет перезагружен. В качестве варианта 1 войдите в систему с полным доступом и проверьте версию встроенного ПО диска. Тип:
   
   `Get-HcsFirmwareVersion`
   
   Ожидаемые версии встроенного ПО диска:
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   Результат выполнения команды показан ниже.
   
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
   
    Выполните команду `Get-HcsFirmwareVersion` на втором контроллере, чтобы проверить обновление версии программного обеспечения. Затем можно выйти из режима обслуживания. Для этого введите следующую команду для каждого контроллера устройства:
   
   `Exit-HcsMaintenanceMode`

5. При выходе из режима обслуживания контроллеры перезапускаются. Когда обновления встроенного ПО диска будут успешно установлены, а устройство будет выведено из режима обслуживания, вернитесь в классический портал Azure. Обратите внимание, что для отображения установленных обновлений режима обслуживания на портале может потребоваться до 24 часов.

